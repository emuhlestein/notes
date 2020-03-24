# Angular Course Notes #

An Angular application is conprized of one or more components and can include one or more services.

An Angular component is comprised of a **template** that consists of HTML for the interface fragment. A **class** for the code associated with the view. The class contains the properties used by the view and the methods needed to respond to the actions of the view. Also there is **metadata** that provides additional information. The **metadata** identifies the class as an angular component.

It is a view defined with a template, its associated code defined with a class and addiational information defined with metadata.

An Angular application is organized into **Modules**. Each Module is comprized of one or more component. Each applicaton has at least one module known as the root module.

**npm** is the package manager. It is used to install all the dependencies for an Angular project and all sub-dependencies. All of the dependencies are listed in the package.json file. ALl of the dependencies are installed in the node_modules folder.

## Modules ##
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

Component = Template + Class + Metadata

### Template ###
Has the view layout created with HTML and includes bindings and directives. 
### Class ###
Supports the view and is created in TypeScript. It contains the properties and methods needed by the view. 
### Metadata ###
Has extra data needed by Angular. 

