# Angular Course notes
Notes for the [cource from Deborah](https://app.pluralsight.com/player?course=angular-2-getting-started-update&author=deborah-kurata&name=angular-2-getting-started-update-m7&clip=0&mode=live)

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
By convesntion each feature of an application has its own folder under the app folder in the application.  
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

The convention is to give a Class the name of the feature followed by the word Component using PascalCase. The class is identified by the class keyword. The Component Name is referenced when used in Code. The export keyword makes this class available to other code in the application. 
Because the script now exports something the module loader wil load this class dynamically, so no script tag is required to load.  
The class only contains a property, a data element having a camelCase Name using a Noun describing the use of the data followed by a : and the data type followed optionally by = and the value assigned.  
The Methods of the class are usually following all the properties of a class. The naming convention is to use verbs that describe the action the method performs given in camelCase as well.  
The Angular @Component() decorator function that defines the metadata of a component and adds that metadata to a class, its members or its method arguments. The decorator must immediately precede the object it describes (note in the example there is no ; after the function. 
This is similar to attributes used in other languages. The object passed into the function only has 2 properties in the example case. The selector gives a means of a directive by which use the class in HTML in the example that would be <pm-app />. Every component must always specify a layout, where the HTML fragment is specified to render the class.  
Angular is modular, each library is a collection of modules [see](https://www.npmjs.com/~angular) for a list of standard modules e.g. @angular/core and @angular/http. Modules need to be loaded. To tell Angular where to find the component the import statement is added on top of the code. 
This statement uses the import keyword, { <Member Name> } from <Angular library or module name>.  
Bootstrapping the component to be loaded by Angular. The index.html is the only true html page, hence SPA. The Index.Html file contans a HTML tag for the class: <pm-app />. 
The rest is done through the system.config.js file which is loaded from the index.html file. This file calls the main.js file in the app folder after the call in the index.html: System.import('app').catch(function(err){ console.error(err); });  
The main.ts loads the app.module which contains reference to the AppComponent section. The appModule is defined with the Angular @NgModule() decorator function and this defines the module for the application. 
The properties of the passed into the function define the imported Modules that are made available to all classes in this module. The declarations property adds a list of Components defined in this module, and the bootstrap property defines the component that initiates the functionality.

## Templates

One can use an in-line template as a single lien with "" or an multi-line template with ``(ES2015 Back Ticks). This keeps the code and the view for that code in one file. Downside is that the intellisense does not work.
One can reference a HTML template file using the templateUrl: property linking to a full reference of a HTML file from the index.html. By convention the name of the template is the same name as the component followed by html

## Components as directives

The components have selectors defined that can be used in other components templates. The directive needs to be declared in the module or imported into the module. In the app.module.ts in the @NgModule add the declaration for the directive (case sensitive).
Also make sure to include the import statement for that component. Directives extend the HTML structure.

## Binding with Logic

Binding is always defined in the template. Interpolation is used with {{}} this is a one-way binding from property to a place. One can use concatenation such as {{'Title: ' + pageTitle}}, maths as {{2*20+1}} and function calls {{'Title: '+ getTitle()}}. Which could be leveraged by:

``` export class AppComonent {
    pageTitle: string = 'Acme Product Management';
    getTitle(): string {};
}```

Binding can be handled inside of html tags such as template interpolation:<h1>{{pageTitle}}</h1> or with property assignment such as <h1 innerText={{pageTitle}}></h1>.

## Angular Directives
Angular's structural directives start with a * in the name.
*ngIf if the value is false then the html directive in which the angular directive is used will be removed from HTML DOM.
*ngFor will iterate over the iterable list and render the html directive for each entry in the iteration. The *ngFor='let item of items' will take an entry from the items property and assign itme to every entry while creating the dom structure for that entry.
In ES2015 For..of iterates over the iterable and For..in iterates over the index.

## Property binding

Binding of DOM with component values e.g. <img [src]='product.imageUrl'> where between [] is the binding target and between '' is the binding source. The same using interpolation would be <img src={{product.imageUrl}}>.
Inside of interpolation JavaScript Expressions can be used e.g. {{showImage ? 'Hide' : 'Show'}}.

## Event binding

Binding of DOM events to methods on a component e.g. <button (click)='toggleImage()'> where between () is the target event and between '' is the template statement targetting the component method.
see [events](https://developer.mozilla.org/en-US/docs/Web/Events) for a list of possible target events.
To define a method in typescript, after the properties of a class:

```showImage : boolean - false;
toggeleImage(): void {
    this.showImage = !this.showImage;
}```
The above example flips the value.

## Two way binding

To use two way binding in Angular use the ngModel directive with [] and () as follows: <input [(ngModel)]='listFilter'> which associates the property binding and sends events back to listFilter. 
Make sure to import { FormsModule } from '@angular/forms'; and include FormsModule in the @NgModule ({ imports: }) segment in the app.module.ts. Note that this is an external feature that is used so it is in imports, not in declaration, where self-defined segments go.

## Transforming data with pipes

An example: {{ product.productCode | lowercase }} the code is then automatically transformed in interpolation before rendering.
Another example using binding: <img [title]='product.productName | uppercase'> which will convert the text to upper case in the binding process.
Pipes can be concatenated such as: {{ product.price | currency | lowercase }} or given parameters such as {{product.Price | currency:'USD':true:'1.2-2'}}.

## More on components

Strong type the components and use interfaces, encapsulate types, have lifecycle hooks, use custom pipes and have relative paths using module ID.
Type all properties and methods of a class. Type also all parameters of the methods. when not knowing a type one can use any or any[] to define the type is not known. on these all type chacking is lost. to help here one can use the interface.
Interfaces are development and compile time addidtions from TypeScript only. an example:

```export interface IProduct {
    productId: number;
    productName: string;
    productCode: string;
    releaseDate: Date;
    price: number;
    calculateDiscount(percent:number): number;
}```

To use the interface as a data type one needs to ```import { IProduct } from './product';``` and use the interface in a property or method: ```products : IProduct[] = [...];```.
Strong typing will allow for Intellisense support to validate the definitions in the component.

## Encapsulating component styles

Using ```styles``` and ```styleUrls``` in the @component segment. Wehn using styles the value is a list of , separated style definitions. better is to use styleUrls, which is a list of , separated references to css files referenced from the index.html file.
This way styles will be uniquely defined for the styles in the component.

## Component lifecycle hooks
Look for the most common lifecycle hooks: OnInit, OnChanges and OnDestroy. See following example on using a LifeCycle hook:

```import { Component, OnInit } from '@angular/core';
export class ProductListComponent implements OnInit {
    pageTitle: string = 'Product List';
    ngOnInit(): void { console.log('In Oninit');
}```

## Transforming data with custom pipes

The pipe is using an interface PipeTransform that has one method transform. The custom pipe needs a decorator thet this is can be used as a pipe. The following is a full example of the implementation of a custom pipe:

```import {Pipe, PipeTransform } from '@angular/core';
@Pipe({name:'productFilter'})
export class ProductFilterPipe implements PipeTransform {
    transform(value:IProduct[], filterBy:string):IProduct[]{}
}```

Before one can use the custom pipe it needs to be added to the declarations section of the module in which it is used.

## Relative paths and ModuleID
When referencing paths inside of a module the relative path from the index.html is required. 
In the .component.ts file the @component() decorater can be given an object with a moduleId property setting this to module.id (as long as coded in Common JS module format using SystemJS module loader, the module.id contains the absolute path to the module).
This can then be re-used in the paths as follows:

```@component({
    selector: 'rm-products',
    moduleId: module.id,
    templateUrl: 'product-list.component.html',
    styleUrls: ['product-list.component.css']
})```
The templete and style Urls will resove to the full reletive path from the index.html

## using DOM objects in Angular

When using angular 2.0 in html one can call angular class methods in the template as follows: '''<input id="name" class="form-control" #name (keyup)="keyPressed($event, name)" />'''.
Here the #name creates a unique reference to teh object and in any event the name referecne will now refere to this specific instance of the <input/> object. The $event is the specific event causing the event triggered.
The code would look something like this:

''' keyPressed($event, input) {
    if($event.which === 13) {
        this.addItem(input);
    }
}'''
Where additem is another method taking the input box and processing the data.

