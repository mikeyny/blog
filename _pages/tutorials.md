---
layout: page
title: Tutorials
permalink: /tutorials/
---

In this part of the blog , i will be sharing tutorials on programming.

Jekyll provides a very easy way to highlight code snippets,i will be taking advantage of it to highlight some cool 
programming challenges one can partake in.Tutorials will range from build simple browser extensions to developing complex systems and sites. As part of my open source movement ,i will be publishing all my work online.If you have any queries about my work ,just contact me and i'll publish a tutorial on the site.

{% highlight javascript %}
function meow() {
    return 'meow';
}

function bark() {
    return 'woof';
}

function getRandomAnimal() {

    var animals = [
        'cat',
        'dog',
        'hippo',
        'lion',
        'bear',
        'zebra'
    ];

    return animals[Math.floor(Math.random()*animals.length)];
}

console.log(meow());
console.log(bark());
console.log(hoofhoof());
console.log(getRandomAnimal());
{% endhighlight %}

