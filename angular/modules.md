# Modules
In ES 2015 a file is a module and a module is a file. Angular has its own modules.

This is a module in ES 2015:

Product.ts
export class Product{
}
Here the module is imported and used:

Product-list.ts
import { Product } from './Product';
The imported file is actually a .js file. Product.ts is transpiled into JavaScript.

An Angular component can only belong to one and only one Angular module.

ES code modules are about organizing code. Angular modules are about organizing the application.

## Angular Modules
An Angular Module is a class that have been decorated with the NgModule decorator. They are used to organize the code into managable blocks. They are also used to make functionality available to other parts of the application. They also provide the context in which templates are resolved.

    @NgModule({
        // class properties
    })
    export class AppModule {}
