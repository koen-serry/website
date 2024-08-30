+++
title = 'JavaPolis: First day of Conference (3/5)'
date = 2005-12-26
publishdate = 2005-12-26
thumbnail = "/thumbs/maximalfocus.jpg"
+++

Third day at Javapolis was kind of strange if you ask me.
The keynotes were nothing extraordinary and then we were already halfway the day...

So at 11.30 I went to What's new in NG Mobile Java as this is a bigger market than J2SE/J2EE will ever be. Even though
job demand isn't that big here in Belgium for these kind of jobs. Beside the updates to the CDC / MIDP API's one thing
caught my attention. JSR-180 which allows you to connect to an SIP proxy from your mobile device. This could turn out
interesting, as soon as your mobile can connect to either to a WLAN or via bluetooth to the internet, it could connect
to your SIP proxy avoiding the usage of the mobile network (and reducing those pesky bills :) )

Next talk was unanimous: EJB3 by Linda DeMichiel and Mike Keith, the room was filled to the brim. Although I didn't hear
a lot of new things I was still exited about how SUN finally did the right thing (even though they are screwing up JSF).
So after lunch most of the crowd still exited about EJB3 wend to Seam. That seems to integrate EJB3 and JSF. Oh my...
even though expectations were set at the beginning of the presentation regarding 'fix for back button' and '2 windows to
the same webapp' the end of the presentation was undermined <<completely>> by the lack of knowledge of either the
English language or Http Sessions. I hope it was the first. When people asked how they'd fixed the "2 open windows"
problem Thomas answered 'we handle it on the server side, with cookies'. Well, sorry, at that time I wasn't the only one
leaving the presentation.

One thing I was really looking forward too was the presentations by Brian Goetz about Concurrency Utilities and the
Memory Model in JDK1.5. Among others he talked about :

* Executors: objects that define how, when and how many concurrent Runnable tasks will be executed. Even though one may
think this is trivial, it's nice that SUN made a couple of default implementations like ScheduledThreadPoolExecutor and
ThreadPoolExecutor.
* ConcurrentHashMap which allows concurrent access to a Map without throwing the notorious ConcurrentModificationException
as it doesn't block concurrent access, but does impose some restrictions on modifications in terms of concurrent threads
* Condition / Lock in order to keep your code somehow cleaner than with the wait/notify. Like this rip from the javadoc
clearly shows,

```java
class BoundedBuffer {
    final Lock lock = new ReentrantLock();
    final Condition notFull = lock.newCondition();
    final Condition notEmpty = lock.newCondition();

    final Object[] items = new Object[100];
    int putptr, takeptr, count;

    public void put(Object x) throws InterruptedException {
        lock.lock();
        try {
            while (count == items.length)
                notFull.await();
            items[putptr] = x;
            if (++putptr == items.length) putptr = 0;
            ++count;
            notEmpty.signal();
        } finally {
            lock.unlock();
        }
    }

    public Object take() throws InterruptedException {
        lock.lock();
        try {
            while (count == 0)
                notEmpty.await();
            Object x = items[takeptr];
            if (++takeptr == items.length) takeptr = 0;
            --count;
            notFull.signal();
            return x;
        } finally {
            lock.unlock();
        }
    }
}
```

About the talk of the Java Memory Model I remembered that one have to be extremely careful with assuming stuff in java.
The compiler can do stuff you didn't think of initially
For example who would think that

```java
while(!asleep)
    sheep++;
```

could turn by the compiler into something like

```java
if(!asleep)
    while(true)
        sheep++;
```

Keeps me up at night :)