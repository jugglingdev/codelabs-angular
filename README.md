# Angular - The Complete Guide

This project was completed as part of Maximilian Schwarzm&uuml;ller's course [Angular - The Complete Guide](https://pro.academind.com/courses/) in conjunction with the [Codefi CodeLabs](https://www.codelabsdash.com/) bootcamp curriculum.

## Table of Contents

- [Angular - The Complete Guide](#angular---the-complete-guide)
  - [Table of Contents](#table-of-contents)
  - [Course Content](#course-content)
    - [The Basics](#the-basics)
    - [Getting Started](#getting-started)
      - [Components](#components)
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

There are 2 options to creating components:  manually and with the Angular CLI.  Note that using the CLI will do the heavy lifting for you, adding all the import statements and `@NgModule` declarations.

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

## Resources

-[Angular Official Documentation](https://angular.io/)
-[Angular CLI Documentation](https://angular.io/cli)
-[Angular Tour of Heroes Tutorial](https://angular.io/tutorial)

## Acknowledgements

Shoutout to Maximilian Schwarzm&uuml;ller for his course [Angular - The Complete Guide](https://pro.academind.com/courses/).  Thank you, Max, for your hard work creating such a comprehensive course.

Another shoutout to [Codefi CodeLabs](https://www.codelabsdash.com/) for putting together this course and pulling in the best resources for learning software development.  The code coaches and this semester's cohort have been awesome to work with.
