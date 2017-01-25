# Angular Course notes
Notes for the [cource from Deborah](https://app.pluralsight.com/player?course=angular-2-getting-started-update&author=deborah-kurata&name=angular-2-getting-started-update-m2&clip=8&mode=live)

## Anatomy
Applications = Component[] + Services[]
Component = Template + class ( propert[], method[]) + metadata
Angular Modules = component[]
* Have a root angular Modules and a set of feature Modules
* TypeScript is language of choice, open source and superset of JavaScript
    * Open source language
    * Superset of JavaScript
    * Transpiled to plain JavaScript
    * Strongly typed (uses type definition files *.d.ts)
    * class based object orientation

## References
* [Github repo](https://github.com/DeborahK/Angular2-GettingStarted)
* [Typescript Playground](http://www.typescriptlang.org/Playground/)
* [Visual Studio Code](https://code.visualstudio.com/)
* [manual setup of Angular](www.angular.io) Quick Start guide

## Setting up an environment
Using TypeScript and Visual Studio Code:
* Set Up npm
    * Node Package Manager
    * Command Line Utility
    * Installs libararies, packages and Applications
    * [Download](https://www.npmjs.com/)

* Set up Angular 2 application
    * Make sure npm is installed
    * Setting up in steps
        1. Create application folder
        2. Add package definition and configuration files
        3. Install the packages
        4. Create the app's Angular module
        5. create the main.ts file and hook the modules in
        6. Create the host Web page (index.html)
    * Alternative options
        * Download the results of these setps from [Github](https://github.com/angular/quickstart)
            * Use to create a clone: git clone https://github.com/angular/quickstart my-proj
            * remove the .git folder and associate the folder with your own project
            * remove non-essential files using: for /f %i in (non-essential-files.txt) do del %i /F /S /Q
        * Use [AngularCLI](https://github.com/angular/angular-cli)
    * For this course use the [Starter Files](https://github.com/DeborahK/Angular2-GettingStarted/) look for the APM Start set
        * Add missing libraries with: npm install
        * Test the application with: npm start
        * The effects of changes will be detected from the setup.

## Modules
In javascript there is an issue with Namespaces. In Typescript helps with code organization. In Typescript the class is made usefull by:
```    export class Product {
        ...
    }```
The Namespace is now Product for the class. This can be used inside another unit by using:
```    import {Product} from './product' ```
This will make all Product class functions available under Product.<name of method or property>
In Angular there is always a root module, by convention called appModule. When growing an application there will be featureModules and Shared Modules. Each module will have one or more components. These modules can be loaded on start or lazy loaded when needed. 
A component belongs to only one Angular Module.

## Aplication lifecycle
Whe loading an application the index.html gets loaded first. That is the file that requestst the browser to load the javascripts to do work.
In Angular there is a tag loading a system configuration app, so no changes to the main.html need to occur. all is now done from code.
The call in the header is:
```    <script>
        System.import('app').catch(function(err){console.error(err);});
    </script>```
This loads from the system.config.js file the segment that states:
```    packages:{
        app:{
            main: './main.js',
            defaultExtension: 'js'
        },
        rxjs:{
            defaultExtension: 'js'
        }
    }```
This points the app from the ./main.js file and all references will be js files so no extension is required.

## Components
An application is a set of components, that work together. As stated in the Anatomy a component is defined as below:  
Component = Template + class ( propert[], method[]) + metadata  
The Template has a view layout, defined in HTML and includes binding and directives.  
the Class is the code that supports the view. It is created with TypeScript and contains properties (Data), the Methods (Logic) and metadata that is used by Angular which is defined with a decorator.
``` import { Component } from '@angular/core';
@Component({
    selector: 'pm-app',
    template: '<div><h1>{{pageTitle}}</h1><div>My First Component</div></div>'
})
export class AppComponent {
    pageTitle: string = 'Acme Product Management';
}```
