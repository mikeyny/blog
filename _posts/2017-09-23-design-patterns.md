---
layout: post
section-type: post
comments: true
title:  "Design Patterns and How to write Brilliant Code"
category: philosophy
tags: [ 'design patterns','clean code','code','developer','OOP' ]
---

![Design Patterns](https://www.dropbox.com/s/v1znitt0umlhenv/designpatterns-720x340.png?dl=1)

How Often do you write code and stop to think , no , they must be a better way of doing this ,then spend the next 4-5 days , sleepless ,whipping up a solution that will either leave you feeling very proud or questioning your competence as a developer. Kudos to you if you can solve the problem ,but why give yourself all that unneccesary stress and waste so much time. You are not the first developer ,developers have been around since the 1940's ,and neither are you the first to encounter that type of problem. So why not leverage on the creative brilliance of over 50 years of programming knowledge ,that's where Design Patterns come in.

### What are Design Patterns

Design Patterns are solutions to commonly occurring problems in software design. Basically what we saying is as programmers we have been having problems and making mistakes for a long time now and through all these we have come up solutions and best practices for tackling these problems , these solutions are the so called Design Patterns.
A famous quotes read "Learning from your mistakes makes you smart. Learning from other people's mistakes makes you a genius. ", don't you want to be a genius ?

 These patterns can help speed up your development process by providing tested and proven development paradigms. So lets say your application need one, and only one instance of an object , why not follow the singleton pattern .Maybe you want to use an a certain component but its API is not compatible with your design , why not use the Adapter pattern. How about that case where you have different implementations of the same functionality and you would like to choose the implementation at runtime without overloading methods and writing duplicating code , well guess what , there is a pattern for that too ,it's called the strategy pattern.

 There is almost a pattern for every single problem known to a programmer , well , except getting you a girlfriend ,you'll have work on that yourself ; )

### Free Code , YIPEE !

 Now let's get one thing straight , design patterns are not code that you can just copy paste into your application & it will work, design patterns a more or less a way of tackling a problem. More of how a architectural blueprint or plan can help you build a great house , but its not the actual house. They are proven methods on how to go about avoiding or solving common problems that developers face.

 Have you ever wondered why there is a  software programmer , software developer and a software engineer , what's the distinction between these titles ? Well a programmer is anyone who can whip up running code ,it may not be the prettiest or most well-factored or even efficient code , but it gets the job done. Developers are just programmers who have been around for a while and now realize they have to maintain their code ,so no more quick fixes ,ambiguous variable names or unreadable code - this is probably where you are right now now.  Software engineers on the other hand treat their work as a craft which they are constantly improving. They read up on best practices( design patterns) and plan and engineer what they build make sure its up to standard and efficient.To drive home the point ,programmer = bad ,developer = ok , engineer = awesome .

![Funny Pic](https://www.dropbox.com/s/zwh7xd9vfwecv4b/wtf.png?dl=1)

 Design patterns also help a lot with readability, this is very important ,as a developer/engineer you rarely write code alone ,your code should communicate itself well with other developers. As design patterns are widely used in programming ,utilizing them in your code will make it easier to understand to your colleagues. When other developers see an AccountBuilder class in your code , they now know this class is following the builder pattern and returns an account object.  It adds a level of professionalism when you no-longer have to say " I passed in these objects into our constructor ,instead of creating them internally ,to reduce operations performed our class and make it more focused " , yes ,this shows you know what you're doing but wouldn't you rather say " I used Dependency Injection to ensure our class is highly cohesive and loosely coupled ,following the Single Responsibility Principle ".


### Design Patterns In the Wild

 Another benefit to learning and using Design Patterns is that they are widely used. No matter what language you use ,there is great use of these patterns , take a look at how Angular a JavaScript framework and Spring a Java framework both extensively use Dependency Injection. Django a popular python web framework makes heavy use of the decorator pattern for authentication. Reactive extensions or Rx , the new IT library , with implementation in almost every language (RxJs ,RxJava ,RxSwift ,Rx.NET ,RxScala ,etc) makes heavy usage of the Observer Pattern. Learning these patterns will help you better understand the framework you're using and use them more efficiently. Regardless of what programming language you use ,or field you're in ,learning design patterns will help you write better and more brilliant code.

  ![Communication Pic](https://www.dropbox.com/s/0bcunzcp8xhmvsu/nimbus-image-1506178304818.png?dl=1)

### So are you ready to learn about design pattern ?

 Here i some resources i would recommend

  [Awesome Youtube Playlist By Christopher Okhravi](https://www.youtube.com/watch?v=v9ejT8FO-7I&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc)

[Head First Design Patterns - O'Reily Media](http://shop.oreilly.com/product/9780596007126.do)

[Design Patterns: Elements of Reusable Object-Oriented Software ](https://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612/ref=sr_1_1?s=books&ie=UTF8&qid=1506175661&sr=1-1&keywords=gang+of+four)(The original deign patterns book by The Gang of Four)

[Blog by AirBrake on Design Patterns ](https://airbrake.io/blog/category/design-patterns)

Did you enjoy this post , feel free to like , leave a comment (good or bad ) or get in touch with me on social media.        
