+++
title = 'JSF vs. Tapestry'
date = 2005-01-04
publishdate = 2005-01-04
thumbnail = "/thumbs/maximalfocus.jpg"
+++

While doing the assignment for the architect exam (SCEA) I'm taking, I was challenged to try out the new JSF web
framework. While doing the first screen everything went amazing, editboxes mapping to a string in a 'managed bean'
worked like a charm. But then the fun only had to start, **checkboxes**... 

One of the more commonly used controls on a webpage is without a doubt a checkbox/radiobutton. 
When you have to map a collection onto a some checkboxes to make a
selection, you have to have make a subclass of your original class of your business model in order to let JSF (ie. the
facesServlet) set the item as being selected. Needless to say is that this kind of plumbing annoys developers to the full
extend, since it requires having n more classes (n being the number of business model classes). If you compare this to
**tapestry**, you enter a complete new ballgame. 

Tapestry allows developers to iterate over a collection and set the
instance of the current iteration in the backing bean. The isSelected property of the backing bean can use this item and
remove it from the collection of move it to a collection of selected items. This is a huge advantage if you ask me. 

The number of lines needed to implement it is really limited to the max. Furthermore, once you get used to this twist of
mind, you get to use it for other items too. 

Second serious malpractice of JSF is the use of Lists!!!, yes
java.util.List instead of generic java.util.Collection. Meaning if you use a Set in your domain model, you have to
convert it into List in order to be useful into JSF. Here goes the plumber again.....BTW, you can use arrays, but unless
you have a good reason, I wouldn't use them in a serious model. Comparing it to the great product Tapesty is, quite
simply it allows arrays/collections AND iterators...what can I say more. 

Voila, so far my humble experience with both products. Most probably I won't have to tell you which product I'll choose 
If given the opportunity to choose one out of 2. If both problems could be solved JSF could be nice, certainly if you take 
the renderkits into account, since this could be the killer item for JSF. Renderkits would allow you to create an application 
for the web and use the same application on a linux console via a telnet renderkit;.. 

Mmmmm, wouldn't that be nice..