---
title: Excerpts from "Clean Code"
date: 2023-10-11 23:14:00 UTC
categories: [Article Excerpt, Software]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/cleancode.jpg
---

>You are reading this book for two reasons. First, you are a programmer. Second, you want to be a better programmer. Good. We need better programmers.

>Remember that code is really the language in which we ultimately express the requirements. We may create languages that are closer to the requirements. We may create tools that help us parse and assemble those requirements into formal structures. But we will never eliminate necessary precision — **so there will always be code**.

>“Honesty in small things is not a small thing.” It was a good omen consistent with what I already wanted to say here. **Small things matter.**

>_God is in the details_, said the architect Ludwig mies van der Rohe. This quote recalls contemporary arguments about the role of architecture in software development, and particularly in the Agile world. 

>Yet attentiveness to detail is an even more critical foundation of professionalism than is any grand vision. First, it is through practice in the small that professionals gain proficiency and trust for practice in the large. Second, the smallest bit of sloppy construction, of the door that does not close tightly or the slightly crooked tile on the floor, or even the messy desk, completely dispels the charm of the larger whole. **That is what clean code is about.**

>Yet even in the auto industry, the bulk of the work lies not in manufacturing but in maintenance—or its avoidance. In software, **80% or more of what we do is quaintly called “maintenance”**: the act of repair.

>Making your code **readable** is as important as making it executable.

**It takes 10 times longer to read code than to write it!**

>That’s being attentive to every variable name. **You should name a variable using the same care with which you name a first-born child.**

>We should view our code as the beautiful articulation of noble efforts of design -- design as a process, not a static endpoint. It’s in the code that the architectural metrics of coupling and cohesion play out. If you listen to Larry Constantine describe coupling and cohesion, he speaks in terms of code -- not lofty abstract concepts that one might find in UML. Richard Gabriel advises us in his essay, “Abstraction Descant” that abstraction is evil. Code is anti-evil, and clean code is perhaps divine.

>Going back to my little box of Ga-Jol, I think it’s important to note that the Danish wisdom advises us not just to pay attention to small things, **but also to be honest in small things**. This means being **honest to the code**, honest to our colleagues about the state of our code and, most of all, being honest with ourselves about our code. Did we Do our Best to “**leave the campground cleaner than we found it**”? Did we re-factor our code before checking in? 

>We are honest about the state of our code because **code is never perfect**. We become more fully human, more worthy of the divine, and closer to that greatness in the details.


>Learning to write clean code is hard work. It requires more than just the knowledge of principles and patterns. You must sweat over it. You must practice it yourself, and watch yourself fail. You must watch others practice it and fail. You must see them stumble and retrace their steps. You must see them agonize over decisions and see the price they pay for making those decisions the wrong way. 

>I know of one company that, in the late 80s, wrote a killer app. It was very popular, and lots of professionals bought and used it. But then the release cycles began to stretch. Bugs were not repaired from one release to the next. Load times grew and crashes increased. I remember the day I shut the product down in frustration and never used it again. The company went out of business a short time after that.
> 
> Two decades later I met one of the early employees of that company and asked him what had happened. The answer confirmed my fears. They had rushed the product to market and had made a huge mess in the code. As they added **more and more features, the code got worse and worse** until they simply could not manage it any longer. **It was the bad code that brought the company down.**

>We’ve all looked at the mess we’ve just made and then have chosen to leave it for another day. We’ve all felt the relief of seeing our messy program work and deciding that a working mess is better than nothing. We’ve all said we’d go back and clean it up later. Of course, in those days we didn’t know LeBlanc’s law: **Later equals never**.

>As the mess builds, the productivity of the team continues to decrease, asymptotically approaching zero. As productivity decreases, management does the only thing they can; they add more staff to the project in hopes of increasing productivity. But that new staff is not versed in the design of the system. They don’t know the difference between a change that matches the design intent and a change that thwarts the design intent. Furthermore, they, and everyone else on the team, are under horrific pressure to increase productivity. So they all make more and more messes, driving the productivity ever further toward zero.

>If you have experienced even one small part of the story I just told, then you already know that spending time keeping your **code clean is not just cost effective; it’s a matter of professional survival**.

>You will not make the deadline by making the mess. Indeed, the mess will slow you down instantly, and will force you to miss the deadline. The only way to make the deadline — **the only way to go fast — is to keep the code as clean as possible at all times**.

>In short, a programmer who writes clean code is an artist who can take a blank screen through a series of transformations until it is an elegantly coded system.

>Reading clean code will never be quite like reading _Lord of the Rings_. Still, the literary metaphor is not a bad one. Like a good novel, clean code should clearly expose the tensions in the problem to be solved. It should build those tensions to a climax and then give the reader that “Aha! Of course!” as the issues and tensions are resolved in the revelation of an obvious solution. 

>The Boy Scouts of America have a simple rule that we can apply to our profession.
>
>**Leave the campground cleaner than you found it.**
> 
> If we all checked-in our code a little cleaner than when we checked it out, the code simply could not rot. The cleanup doesn’t have to be something big. Change one variable name for the better, break up one function that’s a little too large, eliminate one small bit of duplication, clean up one composite `if` statement.

>Remember the old joke about the concert violinist who got lost on his way to a performance? He stopped an old man on the corner and asked him how to get to Carnegie Hall. The old man looked at the violinist and the violin tucked under his arm, and said: “Practice, son. Practice!”
