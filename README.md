# Angular - The Complete Guide

This project was completed as part of Maximilian Schwarzm&uuml;ller's course [Angular - The Complete Guide](https://pro.academind.com/courses/) in conjunction with the [Codefi CodeLabs](https://www.codelabsdash.com/) bootcamp curriculum.

## Table of Contents

- [Angular - The Complete Guide](#angular---the-complete-guide)
  - [Table of Contents](#table-of-contents)
  - [Course Content](#course-content)
    - [The Basics](#the-basics)
    - [Getting Started](#getting-started)
      - [Components](#components)
      - [Data Binding](#data-binding)
      - [Directives](#directives)
    - [Debugging](#debugging)
    - [Component \& Data Binding Deep Dive](#component--data-binding-deep-dive)
      - [Property \& Event Binding](#property--event-binding)
      - [View Encapsulation](#view-encapsulation)
      - [Passing data around](#passing-data-around)
      - [Lifecycle hooks](#lifecycle-hooks)
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
  - [Resources](#resources)
  - [Acknowledgements](#acknowledgements)

## Course Content

### The Basics

Angular is an open-source framework for building modern, single-page web applications.  It is based on TypeScript and is known for its modularity, reusability, and rich set of features.

### Getting Started

To start building with Angular:

1. **Setup**: Install Node.js and the Angular CLI (Command Line Interface).
2. **Create a New Project**: `cd` into the directory you want the app to be in.  Run `ng new app-name` to create a new app.  Optionally add `--no-strict` to remove strict mode.
3. **Generate Components**: `cd` into `app-name`.  Run `ng generate component component-name` to create a new component.  Use `ng g c component-name` as shorthand.  Add `--skip-tests` to exclude generating `.spec` files.
4. **Code**: Write the HTML templates, add styles in CSS, and write TypeScript code to define each component's behavior.
5. **Serve**: Run `ng serve` to start a development server that automatically reloads the app when you make changes.  Use `ng s --o` to serve the app and open it in a new browser tab.
6. **Optional Styles**: If you'd like to style with a library such as Bootstrap, `cd` into your project directory.  Run `npm install --save bootstrap@3`.  Add `"node_modules/bootstrap/dist/css/bootstrap.min.css",` to `styles` in the `angular.json` file.

Check out [Resources](#resources) below for official documentation.

#### Components

In Angular, the entire application is built from components.  Each component includes templates (HTML), styles (CSS), and logic (TypeScript) for that part of the UI.  Think of components as the building blocks that make up the app.  They allow you to split up your complex application into reusable parts.

The `app-root` component holds the entire application.  While `index.html`, `styles.css`, and `main.ts` look fairly bare, the `app` component files hold information about the `app` component and any further nested components.  The root component files include:

- `app.component.html`
- `app.component.css`
- `app.component.ts`
- `app.component.spec.ts`
- `app.module.ts`

For a more specific breakdown, `main.ts` is the code the gets executed first.  It has imports including `{ AppModule }`, referencing `app.module.ts`.  `app.module.ts` imports `{ AppComponent }` and lists `AppComponent` in the `@NgModule` decorator, referencing `app.component.ts`.  Angular then reads the set up in `app.component.ts` and sees the selector `app-root`, the tag used in `index.html`, inserting the `app-root` component.

`main.ts` > `app.module.ts` > `app.component.ts/html/css/spec` files

For each new component created, HTML, CSS, and TypeScript files are included.  Examples of components include headers, footers, cards, articles, and sidebars.  These new components are nested in the `app-root` component.  Just as the `app-root` element is used in `index.html`, the `new-component` elements are included in `app.component.html`.  They are also imported to and added to the `@NgModule` decorator of `app.module.ts`.

There are 2 options for creating components:  manually and with the Angular CLI.  Note that using the CLI will do the heavy lifting for you, adding all the import statements and `@NgModule` declarations.

Option A: Manually Create a New Component

1. Create a folder under `app` with the component name
2. Add a `new-component.component.ts` file
3. Include import, decorator, and export statements
   1. Add `import { Component } from '@angular.core'` to the top of the `.ts` file
   2. Add `@Component ({selector: 'app-new-component', templateUrl: 'new-component.component.html', styleUrls: []'new-component-component-css']})`
   3. Add `export class NewComponent { }`
4. Create `new-component.component.html` and `new-component.component.css` files for component content and style.  Alternative use inline templates and styles under the `@Component` decorator
5. Include `import { NewComponent } from './new-component/new-component.component'` statement and `NewComponent` in the `@NgModule` decorator in `app.module.ts`

Option B: Create a New Component with the Angular CLI

1. In the application directory, run `ng generate component new-component` or `ng g c new-component`
2. This option creates all the files for you with the import, decorator, and export statements already in place.  So, you're done!

Now that we've looked at building components, let's take a look at different ways we can output data.

#### Data Binding

Data binding refers to methods to output data.  It establishes a connection between the app's data (typically in the TypeScript code) and the user interface (HTML) so that changes in one are automatically reflected in the other.  The main types of data binding in Angular are:

1. **One-Way Data Binding**:
   - **String Interpolation**:
     - Embed expressions or variables from TypeScript code into HTML templates (print something in the template)
     - When the data in the TypeScript code changes, the HTML content is automatically updated
     - Must return a string
     - Cannot use blocks (single lines only)
     - `{{ variableName }}`
   - **Property Binding**:
     - Bind an HTML element's property (e.g. the 'src' attribute of an image) to a property in the TypeScript code
     - When the TypeScript property changes, the HTML property is updated
     - Do NOT mix string interpolation with property binding as it will break the app (e.g. `[disabled]="{{!allowNewServer}}"`)
     - `[property]="tsProperty"`
2. **Two-Way Data Binding**:
   - Allows changes to propagate in both directions: from the TypeScript code to the HTML template and from the HTML template back to the TypeScript code
   - Commonly used with form elements such as input fields
   - Be sure to `import { FormsModule } from '@angular/forms';` in `app.module.ts`
   - Add `FormsModule` to the `imports` array in the `@NgModule` decorator
   - `[(ngModel)]="tsProperty"`
3. **Event Binding**:
   - Listen to events (e.g., button clicks, mouse events, form submissions) in the HTML templates and respond to them by executing functions in the TypeScript code
   - `(click)="functionName()"`
   - Optionally pass the event object `$event` as an argument in the function to access event information (e.g., mouse coordinates, event target, key codes)

These data binding methods simplify the development process by automatically keeping the user interface in sync with the data model.

#### Directives

Directives are special markers in the HTML that tell Angular to do something to a DOM element.  Add directives with the attribute selector (or CSS classes or element style selectors).

Built-in directives include:

1. **Structural directives**:
   - Add or remove elements from the DOM
   - Typically prefixed with `*`
   - Examples:
     - `*ngIf="property"`: Conditionally adds or removes an element based on a condition
       - Also `*ngIf='property; else localReference'` with `#localReference`
     - `*ngFor="let item of items"`: repeats an element for each item in a collection
2. **Attribute directives**:
   - Modify the appearance or behavior of an element, component, or other directive
   - Look like normal attributes without a star
   - Examples:
     - `[ngStyle]="attribute: property"`: Applies inline CSS styles to elements based on conditions
     - `[ngClass]="{class: condition}"`: Adds or removes CSS classes based on conditions
       - `[ngClass]="{'active': isActive, 'error': hasError}"` is an example
     - `[(ngModel)]="property"`: two-way data binding for form elements, binding input values to variables and vice versa

While these are built-in directives, it is also possible to create custom directives.  It's also important to note that lifecycle hooks as well as `@Input` and `@Output` properties and `@ViewChild` and `@ContentChild` decorators are all other features of directives.  We'll look each of these in upcoming sections.

### Debugging

Angular provides a variety of tools to help you debug your application.  Error messages in the browser console, for example, contain clues as to what may be the cause of a given bug.  The first part of an error is often the error type (e.g., `TypeError`).  Next is a message briefly describing the issue.  The error message also often lists the file and line number where the error occurred.  Often, a stack trace details the function calls that led to the error beginning with the most recent function at the top.  

A sample error message is:

```js
EXCEPTION:
Error in ./AppComponent class 
AppComponent - inline template:4:6 
caused by: Cannot read property 'push' 
of undefined
```

When debugging with Chrome Dev Tools, there are a couple options.  The first to know is that you can access the Sources tab and look for the code you need in `main.bundle.js`.  Clicking a line in the compiled JavaScript code will open up the `app.component.ts` file and you can debug from there.

However, if a file gets large, it can be very difficult to dig through code.  To directly access your code file structure as it is in your IDE, open up `webpack://` in the Sources tab and proceed to the `src` and `app` folders to find all the TypeScript files and debug the code.

### Component & Data Binding Deep Dive

Now that we've gotten a little exposure to components, data binding, and directives, it's time to go a little deeper.

#### Property & Event Binding

We've previously learned about property and event binding.  Remember, we can use property and event binding on:

- HTML elements (native properties & events)
- Directives (custom properties & events)
- Components (custom properties & events)

The next feature to explore related to property and event binding is communication between parent and child components.  The `@Input()` decorator, `@Output()` decorator, and `EventEmitter` are all essential for passing data from a parent to a child and emitting events from a child to a parent.

1. **`@Input()` Decorator**: This decorator allows a parent component to pass data to a child.  It decorates a property in the child component's class, making it a public input property that can be bound to by the parent component in the child's HTML template.  You can pass an optional alias as an argument (e.g., `@Input('alias')`) if you want to refer to the property with a different name outside of the component class.  The following example binds `childMessage` in the child component to `messageFromParent` in the parent:

    ```ts
    // Child Component
    import { Component, Input } from '@angular/core';

    @Component({
      selector: 'app-child',
      template: '<p>{{ childMessage }}</p>',
    })
    export class ChildComponent {
      @Input() childMessage: string;
    }
    ```

    ```ts
    // Parent Component
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-parent',
      template: `
        <app-child [childMessage]="messageFromParent"></app-child>
      `,
    })
    export class ParentComponent {
      messageFromParent = 'Hello from Parent!';
    }
    ```

2. **`@Output()` Decorator and `EventEmitter`**: This combo is used to emit custom events from a child component to a parent component.  It's useful for when you want the child to notify its parent about a specific action or event. `@Output()` can also take an alias.  This example creates an `EventsEmitter` called `childEvent`.  When the button is clicked, `emitEvent()` is called, emitting the custom even with the message.  The parent component listens for this event using `(childEvent)="handleChildEvent($event)"` and updates the `messageFromChild` property when the event is emitted:

    ```ts
    // Child Component
    import { Component, Output, EventEmitter } from '@angular/core';

    @Component({
      selector: 'app-child',
      template: '<button (click)="emitEvent()">Click me</button>',
    })
    export class ChildComponent {
      @Output() childEvent = new EventEmitter<string>();

      emitEvent() {
        this.childEvent.emit('Event emitted from Child');
      }
    }
    ```

    ```ts
    // Parent Component
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-parent',
      template: `
        <app-child (childEvent)="handleChildEvent($event)"></app-child>
        <p>{{ messageFromChild }}</p>
      `,
    })
    export class ParentComponent {
      messageFromChild: string;

      handleChildEvent(message: string) {
        this.messageFromChild = message;
      }
    }
    ```

The combination of `@Input()`, `@Output()`, and `EventEmitter` provides bi-directional communication between parent and child, enabling data to pass from parent to child and event handling from child to parent.

#### View Encapsulation

In Angular, a *view* refers to the UI of a component or application.  It represents anything that is visible to the user and contains the HTML templates, styles, and components that make up the UI.  

With that in mind, Angular encapsulates the CSS styles defined within components.  There are 3 modes for view encapsulation:

1. **Emulated (Default)**: In this mode, Angular emulates shadow DOM behavior by adding unique attributes to HTML elements within a component's view.  Styles are scoped to the component and will not affect elements outside the component.
2. **None**: This mode has no view encapsulation.  Styles defined in a component's CSS are applied globally and can affect elements outside the component.
3. **ShadowDom**: This mode uses the browser's native Shadow DOM to encapsulate styles.  It provides true isolation of styles within a component's view, but it may not be supported in all browsers.

To specify the view encapsulation mode for a component, use the `@Component` decorator's `encapsulation` property.  Be sure to import `ViewEncapsulation` from `@angular/core`:

```ts
@Component({
  selector: 'app-example',
  templateUrl: './example.component.html',
  styleUrls: ['./example.component.css'],
  encapsulation: ViewEncapsulation.Emulated,
})
```

#### Passing data around

Next, let's look at more ways to pass data around.  We've got 3 new methods to do so:

1. **Using Local References**: Local references let you get access to elements in your template and then use them directly in the template or pass them into TypeScript code.  To create one, use `#localReference` with a custom name in the HTML template element tag.  The following example passes input data into the TypeScript code:

    ```html
    <!-- app.component.html -->
    <input #inputRef type="text" placeholder="Enter data">
    <button (click)="handleButtonClick(inputRef.value)">Submit</button>
    ```

    ```ts
    // app.component.ts
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
    })
    export class AppComponent {
      handleButtonClick(data: string) {
        console.log(`Data submitted: ${data}`);
      }
    }
    ```

2. **Using `@ViewChild()` Decorator**:  The `@ViewChild()` decorator allows you to access child components or DOM elements in a parent component.  In this example, we use the decorator to access the `ChildComponent` instance from the parent component.  After the view is initialized (see `ngAfterViewInit` in [Lifecycle Hooks](####lifecycle-hooks)), we can access and use data from the child component:

    ```ts
    // child.component.ts
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-child',
      template: '<p>{{ childData }}</p>',
    })
    export class ChildComponent {
      childData: string = 'Child data';
    }
    ```

    ```ts
    // app.component.ts
    import { Component, ViewChild, AfterViewInit } from '@angular/core';
    import { ChildComponent } from './child.component';

    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
    })
    export class AppComponent implements AfterViewInit {
      @ViewChild(ChildComponent) childComponent: ChildComponent;

      ngAfterViewInit() {
        console.log(`Child data from @ViewChild(): ${this.childComponent.childData}`);
      }
    }
    ```

3. **Using `ng-content`**: The `ng-content` directive allows you to project content form a parent component into a child component's template.  It looks for content between opening and closing tags and then projects that content into the component.  In the following example, we project the `<p>` element content from the parent component into the `ChildComponent` using `ng-content`:

    ```ts
    // child.component.ts
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-child',
      template: '<div><ng-content></ng-content></div>',
    })
    export class ChildComponent {}
    ```

    ```ts
    // app.component.ts
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',
      template: `
        <app-child>
          <p>This is content passed via ng-content.</p>
        </app-child>
      `,
    })
    export class AppComponent {}
    ```

**Bonus**:  While `@ViewChild()` is used to query and access elements, components, or directives a part of a component's view, `@ContentChild()` accesses what is projected into a component through `<ng-content>`.  Here's an example of using `@ContentChild()` in combination with `<ng-content>`:

```ts
import { Component, ContentChild, ElementRef } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <ng-content></ng-content>
  `,
})
export class ChildComponent {
  @ContentChild('projectedContent') projectedContent: ElementRef;
}
```

This example uses `@ContentChild()` to query an element with the reference `#projectedContent` that is projected into `ChildComponent` through `ng-content`.

To sum up, these methods - local references, `@ViewChild()`, and `ng-content` - are ways to pass data around when working with DOM elements, child components, or content projection.

#### Lifecycle hooks

Directives can implement lifecycle hooks to perform actions at different stages of their life cycle. Common lifecycle hooks for directives include `ngOnChanges`, `ngOnInit`, and `ngOnDestroy`. These hooks allow you to perform actions when the directive is created, initialized, or destroyed.  Other hooks include:

- `ngOnChanges`: called after a bound input property changes
- `ngOnInit`: called once the component is initialized
- `ngDoCheck`: called during every change detection run (click, timer fired, observable resolved, etc.); great for changing something manually because Angular didn't pick it up or something like that
- `ngAfterContentInit`: called after content (`ng-content`) has been projected into view
- `ngAfterContentChecked`: called every time the projected content has been checked
- `ngAfterViewInit`: called after the component's view (and child views) has been initialized
- `ngAfterViewChecked`: called every time the view (and child views) has been checked
- `ngOnDestroy`: called once the component is about to be destroyed

It's good to note that you can access `@ViewChild()` in lifecycle hooks.  As explained earlier, after the view is initialized, (`ngAfterViewInit` lifecycle hook), we can access and use data from the child component.  

Similarly, `@ContentChild()` is commonly used with `ngAfterContentInit` to ensure that queried elements are available for interaction at the appropriate time in the component's lifecycle.

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

## Resources

-[Angular Official Documentation](https://angular.io/)
-[Angular CLI Documentation](https://angular.io/cli)
-[Angular Tour of Heroes Tutorial](https://angular.io/tutorial)

## Acknowledgements

Shoutout to Maximilian Schwarzm&uuml;ller for his course [Angular - The Complete Guide](https://pro.academind.com/courses/).  Thank you, Max, for your hard work creating such a comprehensive course.

Another shoutout to [Codefi CodeLabs](https://www.codelabsdash.com/) for putting together this course and pulling in the best resources for learning software development.  The code coaches and this semester's cohort have been awesome to work with.
