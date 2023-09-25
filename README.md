# Angular - The Complete Guide

This project was completed as part of Maximilian Schwarzm&uuml;ller's course [Angular - The Complete Guide](https://pro.academind.com/courses/) in conjunction with the [Codefi CodeLabs](https://www.codelabsdash.com/) bootcamp curriculum.

## Table of Contents

- [Angular - The Complete Guide](#angular---the-complete-guide)
  - [Table of Contents](#table-of-contents)
  - [Course Content](#course-content)
    - [The Basics](#the-basics)
      - [Components](#components)
    - [Debugging](#debugging)
    - [Component \& Databinding Deep Dive](#component--databinding-deep-dive)
    - [Directives Deep Dive](#directives-deep-dive)
    - [Using Services \& Dependency Injection](#using-services--dependency-injection)
    - [Changing Pages with Routing](#changing-pages-with-routing)
    - [Understanding Observables](#understanding-observables)
    - [Handling Forms in Angular Apps](#handling-forms-in-angular-apps)
    - [Using Pipes to Transform Output](#using-pipes-to-transform-output)
    - [Making Http Requests](#making-http-requests)
    - [Authentication \& Route Protection in Angular](#authentication--route-protection-in-angular)
    - [Dynamic Components](#dynamic-components)
    - [Angular Modules \& Optimizing Angular Apps](#angular-modules--optimizing-angular-apps)
    - [Deploying an Angular App](#deploying-an-angular-app)
    - [Standalone Components](#standalone-components)
    - [Angular Signals](#angular-signals)
    - [Angular Animations](#angular-animations)
    - [Adding Offline Capabilities with Service Workers](#adding-offline-capabilities-with-service-workers)
    - [A Basic Introduction to Unit Testing in Angular Apps](#a-basic-introduction-to-unit-testing-in-angular-apps)
    - [Angular as a Platform \& Closer Look at the CLI](#angular-as-a-platform--closer-look-at-the-cli)
  - [Reflection](#reflection)
  - [Acknowledgements](#acknowledgements)

## Course Content

### The Basics

`ng serve` to spin up server

***

* Angular is a JS framework that changes your DOM at runtime

index.html has app-root tag (component)
all app component files are related to app-root component

app.component.ts has { Component }

***

main.ts is first code that gets executed and  has imports including bootstrapModule { AppModule } which references app.module.ts
app.module.ts has @NgModule that lists [AppComponent]

Angular then analyzes the AppComponent, read the set up in app.component.ts and knows the selector app-root
it can now handle app-root in index.html and insert app-root component

main.ts > app.module.ts > app.component.css/html/spec/ts files

#### Components

The entire application is build from components.
The app (root) component holds the entire application
Components allow you to split up your complex application into reusable parts

***

`ng generate component servers` or `ng g c servers`

***

must have templates listed in @Component (*.component.ts)

### Debugging

### Component & Databinding Deep Dive

### Directives Deep Dive

### Using Services & Dependency Injection

### Changing Pages with Routing

### Understanding Observables

### Handling Forms in Angular Apps

### Using Pipes to Transform Output

### Making Http Requests

### Authentication & Route Protection in Angular

### Dynamic Components

### Angular Modules & Optimizing Angular Apps

### Deploying an Angular App

### Standalone Components

### Angular Signals

### Angular Animations

### Adding Offline Capabilities with Service Workers

### A Basic Introduction to Unit Testing in Angular Apps

### Angular as a Platform & Closer Look at the CLI

## Reflection

## Acknowledgements

Shoutout to Maximilian Schwarzm&uuml;ller for his course [Angular - The Complete Guide](https://pro.academind.com/courses/).  Thank you, Max, for your hard work creating such a comprehensive course.

Another shoutout to [Codefi CodeLabs](https://www.codelabsdash.com/) for putting together this course and pulling in the best resources for learning software development.  The code coaches and this semester's cohort have been awesome to work with.
