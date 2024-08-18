+++
title = 'Cometd vs BlazeDS : pushing messages to the client'
date = 2009-08-03
publishdate = 2009-08-03
thumbnail = "/craft_header.jpg"
+++

In the constant quest of allowing web applications to use more functionality that was once found in fat clients (eg. VB,
Delphi, C/C++). It has been historically difficult to push messages from the server to the client. Not only were there
hoops to jump through on the network level, almost all (stateful) firewalls only allow sending data to a client that
already established a connection (the famous syn bit). There is also the problem that most http servers (IIS and apache)
don't like too many connections open for too long as they typically allocate memory to a connection. Furthermore on the
client side, browsers didn't (until recently) have a standard way to handle server side events. And if things weren't
bad enough there is still the minor issue with browser incompatibilities with IE as the negative role-model.

There are however a few alternatives to circumvent these limitations on which I'll highlight 2 (that I've used from
personal experience).

The use case for this was in a domotics program (a pet project I work on). Here a java
backend was connected via the serial port to the domotics bus. As soon as an event (being for example a light switched
on) I wanted the status of the light updated in the front end. So the front-end contained a image representing the
living room and smaller images the states of electric bulbs in that room. If one switched on the light then the same
state would be represented on screen as soon as the event occurred with the least possible latency.

* Option 1 : Flex front-end and BlazeDS/GraniteDS backend through JMS

Although a Flex application on the front-end feels a bit like cheating, since the true source code is a bunch of actionscript 
files compiled into a SWF (aka flash file). It still gives the user a natural user experience in the browser. 
This flash file connects to the backend via amf over http. The AMF protocol is a proprietary binary protocol opened up 
recently by Adobe, which allows flash clients to connect to a backend. Until recently their backend of choice was either 
coldfusion or jrun, but since other web application servers (and tomcat/jetty in particular) were so widely used, 
Adobe open source'd BlazeDS as well. This combination has an option to use through JMS push server messages to the client.
BlazeDS and Flex were pretty simple to setup, but on the backend side, one required JMS which was typically not included 
for tomcat/jetty or one should switch over to a full blown J2EE server in which JMS was supported. 
Certainly with the new Web Profile of the J(2)EE version the question pops up again which JMS system to use. 
Here again, tastes may differ, but I have a small tendency towards ActiveMQ as it's really fast and provides all kind of 
features like streaming messages. Towards BlazeDs, there is however an alternative called graniteds which I favor as it 
contains less dependencies (like concurrent.jar, which is the predecessor of a backport of java.util.concurrent, old in other words) 
Their implementation is based on option 2 and is an implementation of the Bayeux spec as well.

* Option 2 : Html/javascript front-end and cometd backend

For me this was new (well I had heard about it, but I never came to test/use it). 
So there I was on (another) late nighter trying to find out more about HTML5 which seems to be a hot topic these
days with stuff like the event sources and client-side caches. Problem was that there isn't that much material about the
subject since the final spec is about to be released in **2022**. So looking at event-sources it made me think back about 
cometd and I decided to give it a spin doing just a simple use-case like visualising the amount of free memory on the server. 
Although it didn't have any real immediate benifit, it was easy enough both backend and frontend to get me started to find out if it did fit my use-case
Boy, was I in for a surprise...

First of all, as with html documentation is a little scarce, although better than HTML5. The
things I found however were still usable enough to mash up something usable together. So first step, backend (for me
usually the easiest). Instead of starting my use case I decided to first try it with the proverbial hello world, to
eventually step it up to my use case.

1. Import the required dependencies to use Cometd (or it's Bayeux implementation). These are small "cometd-java-server" is all you need to look for in the maven repository.
2. Implement a listener
3. Start sending messages out (by using the 'publish' method) As a merely sample project I outputted the memory available, the eventual use case would consume events from the serial port.

One note, I needed to import `org.eclipse.jetty.util.ajax.JSON.Literal` as it otherwise seems to escape quotes in the publish of a
JSON message which renders the solution a bit less optimal :(.

On the front end, things couldn't be simpler either.

1. Reference the cometd and it's implementation script (I chose to use jquery)

```javascript
<script type="text/javascript" src="${pageContext.request.contextPath}/org/cometd.js"></script>
<script type="text/javascript" src="${pageContext.request.contextPath}/jquery/jquery.cometd.js"></script>
```

2. Upon handshake, add a listener to the meta channel to listen to the channel on which you publish messages

```javascript
cometd.addListener('/meta/handshake', this, function(){
    cometd.subscribe('/monitor/jvm', receive); // Allow content to show $('#mem').show();
});
```

That's it, now you'll have updates on memory usage on the front-end. 
I added a small visualisation library to the mix so I could come to the following :

![VM Memory pushed](../2009-07-26_224111.png)
