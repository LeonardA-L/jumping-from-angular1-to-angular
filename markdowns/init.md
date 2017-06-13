# Installing the Angular cli
**You can skip this part and go directly to _The Application Module_ if you simply want to run all of the examples in this course online. This part helps you create and get started with an Angular project on your own computer.**

The simplest way to get started with Angular is to use the [Angular CLI](https://cli.angular.io/). It is a command line interface that helps you bootstrap a project, initialize modules and components, and serve your application on a local server for development purposes.

Once you have [set up NPM](https://docs.npmjs.com/getting-started/installing-node), you can install the Angular CLI with this command:

```bash
npm install -g @angular/cli
```

Then, use the `new` command to bootstrap a project.

```bash
ng new awesome-project
```

Once finished, you will have successfully created a fully functionnal Angular project. If you want to run your app on a local server, use `ng serve`. Let's take a look at the folder structure:

```
awesome-project/
├── node_modules/
├── package.json
├── src/
│   ├── app/
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.ts
│   │   └── app.module.ts
│   ├── assets/
│   ├── environments/
│   ├── index.html
│   ├── main.ts
│   ├── styles.css
└── tslint.json
```

Some files are not listed in the tree above as they are not within the scope of this course. Most of them are config files used to run tests with karma or protractor. I definitely recommend looking into them later on, but for now, let's focus on:

* the `assets` folder is where you put your graphical assets and resources (possibly some CSS sheets)
* the `environments` folder has two files: a general config file and a production config file. You can use them to set different config values (like API tokens or log levels) between run environments
* `index.html` is the root HTML template for the page
* `main.ts` is the entry point for the application. It calls the ‘AppModule’ we're going to study in this lesson
* the `app` contains the sources for your app and is where you will create your components. The best structure I have found is to create a `components` folder and then creating a subfolder per component within which contains scripts, templates and styles for the component. The main file we are going to focus on in this lesson is `app.module.ts`.

# The Application Module

Let's open `app.module.ts` and see what we've got:

```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

The first six lines are import statements, mainly from the `@angular` packages. Note that we must also import the main component for our app, `AppComponent`.

The class `AppModule` has the `@NgModule` decorator, which makes it our Angular module. This module itself imports some other modules through its own `imports` properties. These modules are part of Angular but you will use this property to import third-party modules or even your own if your app consists of separate modules.

`declarations` lists the components we are going to package with our app. Note that our main component, `AppComponent`, is included.

`providers` is used to register providers to the Dependency Injection System. We will visit this in-depth during the next few lessons.

Finally, `bootstrap` defines the entry point for the **module**, the component that will be used as the root of the module. The module itself is referenced in `main.ts` with the line:

```javascript
platformBrowserDynamic().bootstrapModule(AppModule);
```

It defines that the main module of the app will be the `AppModule` class.

> An `@NgModule` in Angular 2 is very similar to the `angular.module()` in Angular 1, you use it to declare dependencies and components for your app.

[More info on NgModule](https://angular.io/docs/ts/latest/guide/ngmodule.html).
