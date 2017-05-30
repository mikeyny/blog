---
layout: post
section-type: post
comments: true
title:  "Angular 4 with the angular-cli ,A quick primer"
category: tutorial
tags: [ 'angular','javascript','angularjs','single page apps','web dev' ]
---
## Angular 4

![image](/img/ng.jpg)
As most of you already know angular 4 is now out , only 6 months after the release of angular 2. Now if you are like me and had been putting off learning angular 2 because it was so different from the original angularjs then this must have been a heavy blow. Now you have two new frameworks versions to learn (yes , just 2 ,there is now angular 3 ,whew !!!) , and thats only if they don't release angular 5 while you still doing it. At first I thought of switch to another (hopefully less shifty) framework , maybe react or ember. Starting on the angular 2/4 journey seemed a bit daunting , i had already learned a bit of typescript but setting up gulp processes for development , using components instead of controllers ,learning rxjs ,modules and bundling - argggghhh ,i got a headache just thinking about it.

After a bit of research , i learned angular 4 is backwards compatible with angular 2  , this just means it was not a complete rewrite like with the second version of angular ,but rather some improvements in performance and functionality. This meant i could forego learning angular 2 ,and just move to the up to date angular 4. Now i could enjoy the a faster performance of angular 4, improved syntax of typescript and do away with the messy nested scopes of angularjs. But wait I still had my originals problems to deal with :( .

## Enter Angular-cli

The [Angular CLI](https://github.com/angular/angular-cli) is a command line interface tool that can create a project, add files, and perform a variety of ongoing development tasks such as testing, bundling, and deployment.
Basically a lot of things get easier and faster if you are using Angular CLI, no more manually setting up gulp processing to convert your typescript or bundle your app ,or having to remember a vast amount of boilerplate code for your project , the CLI has you covered.
Installing the cli is easy , and is done with the node packet manager (npm) using
```
npm install -g @angular/cli
```

Once this is installed you can easy start a new angular 4 project using the command
```
ng new PROJECT-NAME
```
This generates boilerplate code for your new projects and installs all your dependencies.
A screenshot of the generated files is shown below

![screenshot](/img/ng-template.png)
Running the project is as simple as going into the project direcory and running `ng serve` for a dev server. Navigating to `http://localhost:4200/` will open up your angular app in the browser. The app will automatically reload if you change any of the source files.
No more running `npm start`, you will just only have to `ng serve`.

## Generating Components, Directives, Pipes and Services

Creating components ,directives ,pipes and services is now as easy as just typing in a command into your terminal.You can use the `ng generate`(or just `ng g`) command to generate new files. Most importantly the angular-cli will add reference to components, directives and pipes automatically in the app.module.ts.

Usage
---

Component :  

 `ng g component my-new-component`


Directive :  

 `ng g directive my-new-directive`


Service

`ng g service my-new-service`

Pipe

`ng g pipe my-new-pipe`

Class

`ng g class my-new-class`

Guard

`ng g guard my-new-guard`

Interface

`ng g interface my-new-interface`

Enum

`ng g enum my-new-enum`

Module

`ng g module my-module`

## Still not convinced ??

The angular-cli comes with extra features which make it easy for you to develop your angular app. For instance when your genearte your project or additional files (componets, directives ,services) you get tests added to you project by default — both Unit Testing (using Karma) as well as End-to-end testing (using Protractor).

Additionally your app is git initialized by default, the .gitignore file is already setup correctly to ignore all the extra files that you might never edit and work with, but will be required for your application to run.

## Ready to learn Angular 4

You can try [Tour of Heroes](https://angular.io/docs/ts/latest/tutorial/) tutorial by the angular team.

[Here](https://www.youtube.com/watch?v=cdlbFEsAGXo&list=PLz5rnvLVJX5VQZdTz4MTE52aKto-MoPwB) is a great youtube playlist on angular 4 by Awais Mirza.

Read documention at the [Angular](https://angular.io) and [Angular-cli](https://cliangular.io) Website.

Enjoy !
