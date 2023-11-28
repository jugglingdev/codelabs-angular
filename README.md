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
      - [Custom Directives](#custom-directives)
      - [Renderer](#renderer)
      - [`@HostListener`](#hostlistener)
      - [`@HostBinding`](#hostbinding)
      - [Structural Directives](#structural-directives)
      - [`ngSwitch`](#ngswitch)
    - [Using Services \& Dependency Injection](#using-services--dependency-injection)
      - [Dependency Injection](#dependency-injection)
      - [Hierarchical Injector](#hierarchical-injector)
      - [Injecting Services into Services](#injecting-services-into-services)
      - [Provider Configuration](#provider-configuration)
    - [Changing Pages with Routing](#changing-pages-with-routing)
      - [Using `routerLink`](#using-routerlink)
      - [`Router`](#router)
      - [Query Parameters \& Fragments](#query-parameters--fragments)
      - [Route Redirection](#route-redirection)
      - [Route Guards](#route-guards)
    - [Understanding Observables](#understanding-observables)
      - [Operators in Observables](#operators-in-observables)
      - [Subjects in Observables](#subjects-in-observables)
      - [Toast UI Designs (Notifications)](#toast-ui-designs-notifications)
    - [Handling Forms in Angular Apps](#handling-forms-in-angular-apps)
      - [Template-Driven Approach](#template-driven-approach)
      - [Reactive Approach](#reactive-approach)
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

As a recap, we've learned about 2 types of directives so far:

1. **Attribute**:
   - look like a normal HTML attribute with possible data binding or event binding
   - only affect the element they are added to
   - Examples: `[ngClass]` and `[ngStyle]`
2. **Structural**:
   - look like a normal HTML attribute with a leading * for desugaring
   - affect a whole area in the DOM by adding/removing elements
   - Examples: `*ngFor` and `*ngIf`

Note: You can only have one structural directive on a given element.

#### Custom Directives

While these built-in directives are very useful, it is possible to create your own custom directive.  

To do so manually:

1. Create a `custom-directive.directive.ts` file named after the custom directive that includes the exported class, `@Directive` decorator and `selector`, and appropriate import statements.  
2. Add the directive to `app.module.ts` under `@NgModule` `declarations` with the import statement.  
3. Finally, add the directive as an attribute to the template element you want it to apply to.

Similarly to components, you can also run the command `ng generate directive customDirective` or `ng g d customDirective` to create a new directive through the CLI.

#### Renderer

Directly accessing the native element and style of a given element may result in an error.  Therefore, best practice is to use the service `renderer` and its methods to access the DOM.  This service is used to create elements, add and remove elements, update element properties, and handle events.  To use `renderer`, declare the dependency in the constructor of the component or service (Angular will then provide an instance for you).  The following code shows how you can inject `renderer` into a component:

```ts
  import { Component, Renderer2, ElementRef } from '@angular/core';

  @Component({
    selector: 'app-example',
    template: '<div #targetElement></div>',
  })
  export class ExampleComponent {
    constructor(private renderer: Renderer2, private el: ElementRef) {
      const targetElement = this.el.nativeElement.querySelector('#targetElement');
      
      // Using the renderer to modify the element
      this.renderer.setProperty(targetElement, 'innerText', 'Hello, Angular!');
    }
  }
```

#### `@HostListener`

The `@HostListener` decorator allows you to listen to host events such as `mouseenter` and `mouseleave` on a given element.  It is used within a directive or component class.  It takes two arguments.  The first is the name of the DOM event and the second is an optional array of values that pass data to the event handler.  After the decorator comes a method to handle the event.

An example of a custom directive using `@HostListener` is:

```ts
  import { Directive, HostListener } from '@angular/core';

  @Directive({
    selector: '[appCustomDirective]'
  })
  export class CustomDirective {
    @HostListener('mouseenter', ['$event'])
    onMouseEnter(event: MouseEvent) {
      // This method is called when the mouse enters the host element.
      // You can access the event object and perform actions here.
    }
  }
```

#### `@HostBinding`

In Angular, the `@HostBinding` decorator binds a directive to a given property of the element it's sitting on.  Be sure to import `HostBinding`, apply the decorator to a property, and set the value.  In the following example, we bind the element's background color to a directive property of the same name and change its value based on the events `mouseenter` and `mouseleave`:

```ts
  import { Directive, HostBinding, HostListener } from '@angular/core';

  @Directive({
    selector: '[appHighlight]'
  })
  export class HighlightDirective {
    @HostBinding('style.backgroundColor') backgroundColor: string;

    constructor() {
      this.backgroundColor = 'transparent';
    }

    @HostListener('mouseenter') onMouseEnter() {
      this.backgroundColor = 'lightblue';
    }

    @HostListener('mouseleave') onMouseLeave() {
      this.backgroundColor = 'transparent';
    }
  }
```

In the template, use brackets if you want to bind to a property which has the same name or alias as a directive like so:

```ts
<input [value]="inputValue" />
```

A shortcut syntax is adding property binding without square brackets if you also omit the single quotation marks:

```ts
<div id=myDynamicId></div>
```

#### Structural Directives

The `*` in front of directives means that Angular will transform them into something else.  So, if you want to create your own structural directive, use `*` along with `TemplateRef`, `ViewContainerRef`, and `@Input`.

Creating a custom structural directive:

1. Create the directive class using the `@Directive` decorator.

    ```ts
        import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

      @Directive({
        selector: '[appCustomDirective]'
      })
      export class CustomDirective {
        constructor(
          private templateRef: TemplateRef<any>,
          private viewContainer: ViewContainerRef
        ) {}

        @Input() set appCustomDirective(condition: boolean) {
          if (condition) {
            this.viewContainer.createEmbeddedView(this.templateRef);
          } else {
            this.viewContainer.clear();
          }
        }
      }
    ```

2. Configure the directive.  Inject the `TemplateRef` and `ViewContainerRef` to work with the template and view container.  Use the `@Input` decorator to bind a condition from the template.
3. Apply the directive to an HTML element in the template and provide a condition.

    ```html
      <div *appCustomDirective="condition">
        This content will be displayed when condition is true.
      </div>
    ```

4. In the component, define the condition property.

    ```ts
      import { Component } from '@angular/core';

      @Component({
        selector: 'app-your-component',
        template: `
          <div *appCustomDirective="condition">
            This content will be displayed when condition is true.
          </div>
        `
      })
      export class YourComponent {
        condition: boolean = true; // Change this value to toggle the display.
      }
    ```

#### `ngSwitch`

If you're using a lot of `ngIf` cases, `[ngSwitch]` is a good alternative directive.  It's often used with `*ngSwitchCase` to specify different cases and `*ngSwitchDefault` to define the default case if the `[ngSwitch]` value doesn't match any of the specified cases:

```html
  <div [ngSwitch]="value">
    <div *ngSwitchCase="'case1'">Content for case 1</div>
    <div *ngSwitchCase="'case2'">Content for case 2</div>
    <div *ngSwitchDefault>Default content</div>
  </div>
```

```ts
  import { Component } from '@angular/core';

  @Component({
    selector: 'app-your-component',
    templateUrl: 'your-component.component.html',
  })
  export class YourComponent {
    value: string = 'case1';

    // You can change the value to 'case2' to see the second case's content.
  }
```

### Using Services & Dependency Injection

Services are used to prevent duplication of code and to centralize data storage in Angular apps.  They act as a central repository for functions, data, and business logic that can be shared across components.

#### Dependency Injection

Services are set up as classes and do not require a decorator.  It's important not to manually instantiate services but rather use **Dependency Injection** to provide instances of services when they are needed.

To use a service in a component, add the service name and type to the constructor of the component.  Include the service in the `providers` array of the `@Component` decorator like so:

```ts
  import { Component } from '@angular/core';
  import { MyService } from './path/to/my.service';

  @Component({
    selector: 'app-example',
    templateUrl: 'example.component.html',
    providers: [MyService]
  })
  export class ExampleComponent {
    constructor(private myService: MyService) {
      // Now you can use myService in this component
    }
  }
```

#### Hierarchical Injector

Angular creates an instance of a service for a given component and all its child components (they all share the same instance of the service).  At different levels in the application:

- **AppModule**: The same instance of the service is available **application-wide**
- **AppComponent**:  The same instance of the service is available for **all components** but **not for other services**
- **Any other Component**:  The same instance of the service is available for **the component and all its child components**

If you want to avoid multiple instances of a service, remove it from the `providers` array in the child component TypeScript files (leave it in the import and constructor, though).

#### Injecting Services into Services

If you need a service to be used by another service, add the `@Injectable()` decorator to the service that will be injected:

```ts
  import { Injectable } from '@angular/core';

  @Injectable()
  export class ServiceA {
    // ...
  }

  @Injectable()
  export class ServiceB {
    constructor(private serviceA: ServiceA) {
      // Now you can use serviceA in ServiceB
    }
  }
```

#### Provider Configuration

If you're using Angular 6+ (check your package.json to find out), you can provide application-wide services in a more concise way using the `providedIn` property in the `@Injectable()` decorator:

```ts
  import { Injectable } from '@angular/core';

  @Injectable({
    providedIn: 'root'
  })
  export class MyService {
    // ...
  }
```

This is equivalent to manually adding the service to the `providers` array of the `AppModule`.  The advantage is that Angular can load services lazily, leading to better performance and loading speed for larger applications.  However, the traditional syntax using `providers` still works for providing services.

### Changing Pages with Routing

Routing is Angular's way of simulating the transition between different pages within a single-page application.  It allows you to navigate to different views or components based on the URL.  For example, you can have routes like `/users` and `/about` to represent different pages or views in your app.

#### Using `routerLink`

Instead of using traditional `href` attributes, Angular uses `routerLink` to navigate between pages.  It prevents the default behavior of full-page reloads.  You can specify routes using absolute paths (starting with `/`) or relative paths (`./` or nothing):

```ts
  <a [routerLink]="/users">Users</a>
  <a [routerLink]="./about">About</a>
```

Additionally, add the `[routerLinkActiveOptions]` attribute to an element to control when a link is considered active.  `{exact: true}` ensures that the link is active only for the exact full path.

```ts
  <a [routerLink]="/users" [routerLinkActiveOptions]="{exact: true}">Users</a>
```

#### `Router`

To work with routing in your components, inject the `Router` service:

```ts
  import { Router } from '@angular/router';

  constructor(private router: Router) {
    // Use router methods in your component
  }
```

You can navigate programmatically using the `router.navigate` method, which takes a route path as an argument:

```ts
  this.router.navigate(['/users']);
```

You can include parameters in your routes, like `/:id`, to pass data to a component.  These parameters can be accessed using `route.snapshot.params` or as an observable using `route.params`.

If you create your own observables related to routing, it's important to manage them by unsubscribing in your components.  While Angular handles some automatic unsubscription, you should use the `ngOnDestroy` lifecycle hook to perform any manual unsubscription.  Observables will be covered in more detail in the next section.

#### Query Parameters & Fragments

You can use query parameters and fragments in your route links.  These can be set and accessed using the `queryParams` and `fragment` properties, respectively.  Both can also be subscribe to for changes.

To control how query parameters are handled when navigating between routes, use `queryParamsHandling`.  Options include `preserve` (retains previous query parameters) and `merge` (merges new query parameters with existing ones).

Here's an example of query parameters & fragments working with a component called `ProductDetailsComponent` that displays details about a product.  We pass a product ID as a query parameter and a section as a fragment to this component.

```ts
  // app-routing-module.ts
  import { NgModule } from '@angular/core';
  import { RouterModule, Routes } from '@angular/router';
  import { ProductDetailsComponent } from './product-details.component';

  const routes: Routes = [
    { path: 'product/:id', component: ProductDetailsComponent }
  ];

  @NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule]
  })
  export class AppRoutingModule {}

  // product-details.component.ts
  import { Component } from '@angular/core';
  import { ActivatedRoute } from '@angular/router';

  @Component({
    selector: 'app-product-details',
    template: `
      <h2>Product Details</h2>
      <p>Product ID: {{ productId }}</p>
      <p>Section: {{ section }}</p>
    `
  })
  export class ProductDetailsComponent {
    productId: string;
    section: string;

    constructor(private route: ActivatedRoute) {
      // Access query parameters and fragments using the ActivatedRoute service
      this.route.queryParams.subscribe(params => {
        this.productId = params['id'];
      });

      this.route.fragment.subscribe(fragment => {
        this.section = fragment;
      });
    }
  }

  // Link in product-details.component.html
  <a [routerLink]="'/product/123'" [queryParams]="{ id: '123' }" [fragment]="'overview'">Product 123 Overview</a>
```

In this example, we're linking to the `/product/123` route, passing the `id` query parameter with a value of `123` and setting the fragment to `overview`.  Clicking the link will navigate to the `ProductDetailsComponent` and the component will extract the query parameters and fragment values form the route an display them.

#### Route Redirection

To configure route redirection, use `redirectTo` in the route configuration:

```ts
  { path: '', redirectTo: '/somewhere-else', pathMatch: 'full' }
```

The `pathMatch: 'full'` ensures that the full path must match for the redirection to occur.  This avoids redirecting for paths starting with an empty string.  

`**` serves as a wildcard.  Make sure it's the very last path in the list of routes when in use.

#### Route Guards

Angular provides route guards like `canActivate` and `canActivateChild` that allow you to implement logic to determine if a route should be activated or not.  These guards can be added to route configurations to control access to specific routes based on conditions.

This example of a route guard prevents access to a specific route if the user is not authenticated:

```ts
  // Create the Route Guard (AuthGuard service)
  import { Injectable } from '@angular/core';
  import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, UrlTree, Router } from '@angular/router';
  import { Observable } from 'rxjs';

  @Injectable({
    providedIn: 'root'
  })
  export class AuthGuard implements CanActivate {
    constructor(private router: Router) {}

    canActivate(
      route: ActivatedRouteSnapshot,
      state: RouterStateSnapshot
    ): boolean | UrlTree | Observable<boolean | UrlTree> | Promise<boolean | UrlTree> {
      // Check if the user is authenticated (you would typically have your own authentication logic)
      const isAuthenticated = /* Your authentication logic here */ true;

      if (isAuthenticated) {
        return true; // Allow access to the route
      } else {
        // Redirect to the login page or any other page
        return this.router.createUrlTree(['/login']);
      }
    }
  }

  // Add the Route Guard to your route configuration
  const routes: Routes = [
  // ...
  {
    path: 'dashboard',
    component: DashboardComponent,
    canActivate: [AuthGuard] // Add the AuthGuard to protect this route
  },
  // ...
  ];

  // Use the guard in your component
  <a [routerLink]="'/dashboard'">Go to Dashboard</a>
```

The `AuthGuard` will prevent unauthorized access to the `/dashboard` route and users will be redirected to the login page or another specified route if they are not authenticated.

### Understanding Observables

An observable in Angular is used as a data source, representing a stream of data that can emit values over time.  These data sources can come from various places such as user input, events, HTTP requests, or data generated programmatically.

Observables are part of the RxJS library and rely on the observer pattern.  An observable emits data over time and observers subscribe to receive and react to this data.  Between the observable and the observer lies a stream or timeline where multiple events can be emitted by the observable.

When working with observables, you typically handle data in 3 ways:

1. Handling the **data** emitted by the observable
   - Ex: What should happen when I receive a data package?
2. Handing **errors**
   - Ex: What should happen when I receive an error?
3. Handling the **completion** of the observable (not all complete, e.g., button)
   - What should happen when the observable completes?

Overall, observables play a crucial role in handling asynchronous events and data in Angular applications, enabling responsive and efficient user interfaces.  They allow you to work with data streams, apply transformations, and react to events while maintaining clean and manageable code.

#### Operators in Observables

Operators are methods used in the observable pipeline to transform, filter, and manipulate the data emitted by the observable before it reaches the observer.  These operators are typically used within the `pipe` method.  Examples include `filter`, `map`, and `subscribe`.

```ts
  import { Observable } from 'rxjs';
  import { map, filter } from 'rxjs/operators';

  const source$ = new Observable<number>((observer) => {
    observer.next(1);
    observer.next(2);
    observer.next(3);
    observer.complete();
  });

  source$
    .pipe(
      filter((value) => value % 2 === 0), // Only emit even numbers
      map((value) => value * 2) // Double the values
    )
    .subscribe((value) => {
      console.log(value); // Output: 4
    });
```

#### Subjects in Observables

Subjects are a type of observable and a better alternative to using the EventEmitter for custom event handling in Angular.  You can manually subscribe to a subject or use it as an output for data transmission.

```ts
  import { Subject } from 'rxjs';

  const mySubject = new Subject<number>();

  mySubject.subscribe((data) => {
    console.log(data); // Output: 42
  });

  mySubject.next(42);
```

It is essential to unsubscribe from observables when they are no longer needed to prevent memory leaks.  Angular handles this automatically for some built-in observables, but when you work with custom observables, you must manually unsubscribe.

#### Toast UI Designs (Notifications)

Toast UI designs are a user interface pattern for displaying non-intrusive notifications or messages to users.  They are often used to provide feedback on the outcome of actions or to convey information without disrupting the user's workflow.

Toast designs are often used in conjunction with observables to provide a responsive and user-friendly experience in the context of handling asynchronous events and user notifications.

### Handling Forms in Angular Apps

Angular gives you a JSON representation of your form, making it simple to retrieve user values and see and work with the state of the form.  Handling forms in Angular involves two approaches:  template-driven and reactive.

#### Template-Driven Approach

In the template-driven approach, Angular infers the form structure form the HTML template.

1. **Form Setup**:
   - Use `ngModel` to indicate form controls.  Add a `name` attribute to identify them.  
   - Make the form submittable by using the `(ngSubmit)` directive.
   - Use a local reference set to `ngForm` to the form to work with the form state and use `.value` for access to the form data.
   - Use `@ViewChild` instead of passing in the form to `onSubmit()` if you need to access the form before the point of submission.
   - Define default values with one-way (e.g., `[ngModel]="defaultQuestion"`) or two-way binding.
   - Use `reset()` to reset the form values and state
2. **Validation**:
   - Use directives like `required` and `email` to specify validation rules.
   - Angular dynamically adds CSS classes to indicate control state (e.g., `ng-invalid`, `ng-touched`).  You can use these classes for styling.
   - If a form is not valid, you can disable the submit button with `[disabled]="!f.valid"`.
   - Use `*ngIf` to display a warning/error message depending on the state of the form (e.g., `*ngIf="!email.valid && email.touched"`).
3. **Built-In Validators**:
   - Angular provides a set of built-in validators accessible via the `Validators` class.
   - For template-drive forms, you can use directives marked with "D" from [Angular's official docs](https://angular.io/api/forms/Validators) for validation.
4. **Form Controls**:
   - Use the `ngForm` object properties (e.g. `dirty`, `disabled`, `errors`, `invalid`, `value`) for various form control operations.
   - Group form controls with `ngModelGroup`.
   - Set a local reference equal to `ngModelGroup` to output a message if the values are invalid with `*ngIf`.
   - Use `setValue()` and `patchValue()` to overwrite the values of each control or specific controls respectively

The template-driven approach is used for simple forms, rapid prototyping, integrating with existing HTML, minimized TypeScript, and cases where less custom validation logic is okay.

#### Reactive Approach

The reactive approach involves programmatically defining and configuring the form using TypeScript.

1. **Form Setup**:
   - Add the `ReactiveFormsModule` to your `app.module.ts`.
   - Use `setValue` to prepopulate all form values and `patchValue` to prepopulate specific values.
   - Use `reset` to clear the form.
   - Track changes with `valueChanges.subscribe()` and `statusChanges.subscribe()`.

    ```ts
      import { FormGroup, FormControl, Validators } from '@angular/forms';

      ngOnInit() {
        this.signupForm = new FormGroup({
            username: new FormControl(null, [Validators.required, Validators.email]),
            // Other form controls
        });
      }
    ```

2. **Form Controls**:
   - Create a `FormGroup` object to represent the form structure in TypeScript's `OnInit()`.  Define form controls within the `FormGroup` as key-value pairs.  
   - Add the `[formGroup]` directive to the `<form>` element and `[formControlName]` for individual controls.
   - Group controls using `FormGroup` in TypeScript and `FormGroupName` in the template.
   - Use `FormArray` for arrays of form controls and sync them using `formArrayName` in the template.  You can use `*ngFor` to loop through the array in the template.  Be sure to type cast the `FormArray` (e.g., `(<FormArray>this.signupForm.get('hobbies'))`).

    ```html
      <form [formGroup]="signupForm" (ngSubmit)="onSubmit()">
        <input formControlName="username">
        <!-- Other form controls -->
        <button type="submit">Submit</button>
      </form>
    ```

3. **Validation**:
   - Access control properties and validation using `signupForm.get('controlName)`.
   - CSS styling and error messages are similar to the template-driven approach.

    ```html
      <input formControlName="username">
      <div *ngIf="signupForm.get('username').invalid && signupForm.get('username').touched">Invalid username</div>
    ```

4. **Custom Validators**:
   - Create custom validators by returning `null` for valid or a validation error object for invalid values.
5. **Async Validators**:
   - Implement custom async validators as a third argument in `new FormControl()`.

The reactive approach is used for complex and dynamic forms, type safety, testing, programmatic control, and reactivity to data changes.

### Using Pipes to Transform Output

Pipes in Angular are used to transform output values.  For example, if you're using string interpolation to output a name or date, you can add a pipe (`|`) after the variable name and `uppercase` to output the name in all caps or `date:'fullDate'` to output a date as `Monday, August 16, 2042`.  Notice that the date pipe takes a parameter.  It's also possible to chain multiple pipes together.

#### Custom Pipes

To create a custom pipe, create a new `name.pipe.ts` file that exports the pipe class (alternatively use the CLI shortcut `ng g p name`).  Include a `@Pipe` decorator with the `name` of the pipe that you'll use in the string interpolation and remember to add the class name to the `@NgModule` `declarations`.  Just like built in pipes, custom pipes can be parametized and have custom arguments passed in.

#### Async Pipes

Using the `async` parameter tells Angular to recognize that the output is a Promise and to wait until that Promise is resolved before displaying the data.

### Making Http Requests

In Angular, when you need to interact with a server for data, you use Http requests. Instead of directly connecting to a database, Angular communicates with a server through these requests and receives responses. Here are the key concepts and best practices for making Http requests in Angular:

#### Http Request Components

An Http request includes:

  - **URL (API Endpoint)**: This specifies the server endpoint to which the request is made, such as `/posts/1`
  - **Http Verb (Method)**: The HTTP method used for the request, like `GET`, `POST`, `PUT`, etc.
  - **Headers (Metadata)**: Headers are used to send additional information with the request, like the content type, and are typically defined as an object, for example: `{ "Content-Type": "application/json" }`
  - **Body**: The request body contains the data to be sent to the server.  For example, when making a POST request, you might include a JSON object like `{ title: "New Post" }`

#### Observables and Subscriptions

Observables are important when dealing with Http requests in Angular.  You must subscribe to the observable that wraps the Http request, otherwise Angular will not send the request because nothing is actively listening for the response.

```ts
  import { HttpClient } from '@angular/common/http';

  this.httpClient.get('/posts/1').subscribe(data => {
    // Handle the response data here
  });
```

#### Generics Types

Also note that it's possible to define generic types on the `get()` and `post()` methods, which allows you to specify the expected data type for the response.

```ts
  this.httpClient.get<Post>('/posts/1').subscribe(post => {
    // Handle the Post object
  });
```

#### Best Practices for Http Requests

It's recommended to separate concerns between components and services. Move the parts related to template management, like loading status and loaded data, into the component. For handling Http requests, subscribe in the component while keeping the request setup in the service. However, if your component doesn't need to handle the response and status, you can subscribe in the service.

#### Handling Errors

To handle errors, you can provide a second argument in the `subscribe()` method. Additionally, you can use operators like `catchError` and `throwError` to manage errors within observables.

#### Headers and Query Parameters

To set headers, use the `HttpHeaders` class in key-value notation. For query parameters, use the `HttpParams` class and the `set()` method.  If adding multiple parameters, create a `new HttpParams` instance and use the `append()` method for each parameter.

#### Responses

Http requests can return different types of responses. The default is `observe: body`, which includes the response body. You can also use `response` to get the entire response, including headers and status information, or `events` to observe events like progress. You can configure the `responseType` as `json`, `text`, or `blob` to specify the expected format of the response.

#### Interceptors

Interceptors are commonly used to modify request headers or responses globally within an Angular application. They allow you to add, modify, or remove headers and perform other operations on Http requests and responses.

```ts
  // app.module.ts
  import { NgModule } from '@angular/core';
  import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
  import { AuthInterceptor } from './auth.interceptor';

  @NgModule({
    declarations: [...],
    imports: [HttpClientModule],
    providers: [
      {
        provide: HTTP_INTERCEPTORS,
        useClass: AuthInterceptor,
        multi: true,
      },
    ],
    bootstrap: [...],
  })
  export class AppModule {}

  // AuthInterceptor
  import { Injectable } from '@angular/core';
  import {
    HttpInterceptor,
    HttpRequest,
    HttpHandler,
    HttpEvent,
  } from '@angular/common/http';
  import { Observable } from 'rxjs';

  @Injectable()
  export class AuthInterceptor implements HttpInterceptor {
    intercept(
      request: HttpRequest<any>,
      next: HttpHandler
    ): Observable<HttpEvent<any>> {
      // Add an authorization header to the request
      const authToken = 'your-auth-token';
      const authRequest = request.clone({
        setHeaders: { Authorization: `Bearer ${authToken}` },
      });

      return next.handle(authRequest);
    }
  }
```

The above interceptor adds an authorization header to all outgoing Http requests.

#### Resolver

Resolvers are a crucial part of Angular's routing system. They are used to fetch data before a route is activated. Resolvers are often used to ensure that necessary data is available for a component before it is displayed. To use resolvers, you need to define a resolver service and configure it in the route definition.

Here's an example of a resolver (`PostResolver`) that fetches a list of posts using a service (`PostService`) before activating a component that displays those posts:

```ts
  // AppRoutingModule
  import { NgModule } from '@angular/core';
  import { RouterModule, Routes } from '@angular/router';
  import { PostListComponent } from './post-list.component';
  import { PostResolver } from './post.resolver';

  const routes: Routes = [
    {
      path: 'posts',
      component: PostListComponent,
      resolve: { posts: PostResolver },
    },
  ];

  @NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule],
  })
  export class AppRoutingModule {}

  // PostResolver
  import { Injectable } from '@angular/core';
  import {
    Resolve,
    ActivatedRouteSnapshot,
    RouterStateSnapshot,
  } from '@angular/router';
  import { Observable } from 'rxjs';
  import { PostService } from './post.service';

  @Injectable()
  export class PostResolver implements Resolve<any> {
    constructor(private postService: PostService) {}

    resolve(
      route: ActivatedRouteSnapshot,
      state: RouterStateSnapshot
    ): Observable<any> {
      return this.postService.getPosts();
    }
  }
```

In this route configuration, the `resolve` property specifies that the `PostResolver` should be used to fetch the `posts` data before activating the `PostListComponent`. The resolved data is made available to the component through the route's data property.

Now, when a user navigates to the `/posts` route, the resolver will ensure that the `posts` data is available before the `PostListComponent` is displayed.

### Authentication & Route Protection in Angular

Authentication in Angular involves the process of verifying the identity of a user before granting access to certain resources or routes within an application. This is typically achieved through the exchange of authentication data between the client and the server.

#### Client-Server Communication for Authentication
When a user attempts to log in, the client sends authentication data (e.g., username and password) to the server for verification. The server then checks the provided credentials and, if valid, establishes a session or issues a token to the client. It's important to note that RESTful APIs, which Angular often interacts with, are stateless, meaning each request from the client is independent and doesn't rely on previous requests.

#### Token-based Authentication
Angular commonly uses token-based authentication for securing communication between the client and the server. After successful authentication, the server generates a JSON Web Token (JWT), which is essentially an encoded string with metadata. This token serves as proof of the user's identity and is sent back to the client.

##### JSON Web Token (JWT) Basics
A JWT consists of three parts: header, payload, and signature. The header contains information about how the JWT is encoded, the payload contains the claims, and the signature is used to verify the authenticity of the token. It's important to emphasize that JWTs are encoded, not encrypted. The client decodes the token to access the information within.

##### Server-Side Token Handling
The server keeps a secret key, known only to the server, which is used to sign the JWT. When the client sends the token in subsequent requests, the server verifies the signature using its secret key to ensure the token is valid and hasn't been tampered with.

##### Client-Side Token Storage
Upon receiving the JWT, the client stores it securely. Common storage options include browser cookies or the browser's local storage or session storage. The stored token is then sent in the header of each authenticated HTTP request to authorize access to protected resources.

#### Route Protection in Angular
Angular provides a mechanism to protect routes based on the user's authentication status. This is often achieved by implementing route guards, which are services that can decide whether a route can be activated or not.

Let's look at a simplified example using Angular's HttpClient for authentication and route protection:

```ts
  // Authentication Service
  import { Injectable } from '@angular/core';
  import { HttpClient } from '@angular/common/http';
  import { Observable } from 'rxjs';

  @Injectable({
    providedIn: 'root',
  })
  export class AuthService {
    private apiUrl = 'your-authentication-api-url';

    constructor(private http: HttpClient) {}

    login(credentials: { username: string, password: string }): Observable<any> {
      return this.http.post(`${this.apiUrl}/login`, credentials);
    }
  }
```

```ts
  // Route Guard
  import { Injectable } from '@angular/core';
  import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';
  import { AuthService } from './auth.service';

  @Injectable({
    providedIn: 'root',
  })
  export class AuthGuard implements CanActivate {
    constructor(private authService: AuthService, private router: Router) {}

    canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): boolean {
      if (this.authService.isAuthenticated()) {
        return true;
      } else {
        this.router.navigate(['/login']);
        return false;
      }
    }
  }
```

In this example, the AuthService handles authentication using HttpClient, and the AuthGuard checks whether the user is authenticated before allowing access to a protected route. The actual implementation may vary based on your specific requirements and authentication flow.

### Dynamic Components

Dynamic components in Angular refer to the ability to load and manipulate components programmatically at runtime. There are two common ways to achieve this: using *ngIf for declarative loading and using Dynamic Component Loader for imperative loading.

#### Declarative Loading with `*ngIf`

You can use *ngIf to dynamically load components by embedding them within the template and controlling their visibility as in this example:

```ts
  // app.component.ts
  import { Component } from '@angular/core';

  @Component({
    selector: 'app-root',
    template: `
      <h1>Welcome to Angular App!</h1>
      <div *ngIf="shouldDisplayComponent">
        <app-dynamic-component></app-dynamic-component>
      </div>
    `
  })
  export class AppComponent {
    shouldDisplayComponent = true;
  }
```

#### Imperative Loading with Dynamic Component Loader

Dynamic Component Loader involves creating and adding components to the DOM programmatically using Angular services.  Developers have more control over when and how the component is added or removed in this method.

```ts
  // dynamic-component-loader.service.ts
  import { Injectable, ComponentFactoryResolver, ViewContainerRef } from '@angular/core';

  @Injectable({
    providedIn: 'root',
  })
  export class DynamicComponentLoaderService {
    constructor(private componentFactoryResolver: ComponentFactoryResolver) {}

    loadComponent(viewContainerRef: ViewContainerRef, componentType: any) {
      // Resolve the factory for the component type
      const factory = this.componentFactoryResolver.resolveComponentFactory(componentType);

      // Create and add the component to the view container
      const componentRef = viewContainerRef.createComponent(factory);

      // Access the instance of the component
      const instance = componentRef.instance;

      // Do additional configuration or interact with the dynamic component as needed
      // ...

      return instance;
    }
  }
```

```ts
  // app.component.ts
  import { Component, OnInit, ViewChild, ViewContainerRef } from '@angular/core';
  import { DynamicComponentLoaderService } from './dynamic-component-loader.service';

  @Component({
    selector: 'app-root',
    template: `
      <h1>Welcome to Angular App!</h1>
      <div #dynamicComponentContainer></div>
      <button (click)="loadDynamicComponent()">Load Dynamic Component</button>
    `
  })
  export class AppComponent implements OnInit {
    @ViewChild('dynamicComponentContainer', { read: ViewContainerRef }) dynamicComponentContainer: ViewContainerRef;

    constructor(private dynamicComponentLoaderService: DynamicComponentLoaderService) {}

    ngOnInit() {
      // Optionally, load dynamic component on component initialization
      // this.loadDynamicComponent();
    }

    loadDynamicComponent() {
      const dynamicComponentType = YourDynamicComponent; // Replace with your dynamic component class
      this.dynamicComponentLoaderService.loadComponent(this.dynamicComponentContainer, dynamicComponentType);
    }
  }
```

This second example demonstrates a service, `DynamicComponentLoaderService`, responsible for dynamically loading components. The `app.component.ts` file then uses this service to load a dynamic component when a button is clicked or during component initialization.

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
