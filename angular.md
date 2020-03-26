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
Has extra data needed by Angular defined with a decorator.

**Decorator** is a function that adds metadata to a class, its members, or its method arguments. A Decorator is a JavaScript language feature. Adding the @Component decorator to a class makes that class an Angular component.

A directive is a custom html element or html tag. The name of the directive is specified by the selector property. The directive can be inserted into any template. Where the directive is in the template, the directive's html is inserted.

In NgModule, the declarations property is an array of the components that belong to this module. The imports property is an array of the external modules that are needed by the components in this module. The bootstrap property is an array that defines the startup component of the application.

In a component, the templateUrl property defines the file that is the Linked Template.

Binding is for data communication between a template and its associated class.

Interpolation is a data binding function that passes data from the class property to the template.

{{title}} This is an example of interpolation. title is a property of the associated class. This is a template expression. The expression is evaluated in the context of an expression.

Angular has built-in directives like \*ngIf and \*ngFor. These are known as structural directives. The alter the structure of the view by adding, removing or manipulatin DOM elements. The \* in front of \*ngIf or \*ngFor marks it as a structural directive.

If the expression in \*ngIf="expression" evaluates to true, elements will be added to the DOM. If the expression evaluates to false, then elements are removed from the DOM.

\*ngIf and \*ngFor are exposed in the BrowserModule.

    <ts *ngFor="let product of products>
    
The let keyword is used to define template input variable. The example above, product is a template input variable. It can be referenced anywhere in the element in which it was defined.

    for...of // loops over iterable objects like arryas
    
    for...in // iterates over properties of an object

    This is one-way data binding or property binding:
    <img [src]='product.imageUrl'>
    
    This is interpolation
    <img src={{product.imageUrl}}
    
These two bindings do the same thing.

**ngOnChanges** 
A lifecycle hook that is called when any data-bound property of a directive changes. This is called only when an Input property changes.

**Service**

The recommended way to register a service is in the root injector. This is done using the @Injection decorator. This was introduced in Angular 6.

    @Injectable({
       providedIn: 'root'
    })
    export class ProdService {}
    
    The old way is no longer recommended: registering in the service as a provider in an NgModule.
    
    @NgModule({
       imports: [ BrowserModule ],
       declarations: [ AppComponent ],
       providers: [ ProdService ]
    })

If a service is to be used only my a single component and its children, the service is registered in the providers property of the @Component decorator.
    @Component({
       providers: [ ProdService ]
    })
    
## Observable ##

Observables are for handling asynchronous data. They emit values as they are received by the observable. You need to subscribe to an observable in order for it to emit values. If you don't subscribe to it, it does nothing. Operartors are methods on observables that create new observables. They transform the observable in a defined way. Operators are composed using the pipe method.

##### Example #####

    import { take } from 'rxjs/operators';
    import { Observable, of } from 'rxjs';
    cancel(run: Run): Observable<Object> {
        return this.take(this.http.put(`${this.url}cancel/${id}`, JSON.stringify({}), {
            headers: new HttpHeaders().set('accept', 'text/plain'),
            responseType: 'text' as 'json' }));
      }

      /**
       * This function enusres that an observable is unsubscribed after use.
       *  it prevents having to call explicitly call unsubscribe on every observable
       * @param obs - An Observable
       * @param freq - the number of times the observable is expected to emit (default value is 1)
       */
      private take<T>(obs: Observable<T>, freq: number = 1): Observable<T> {
        return obs.pipe(take(freq));
      }

# Unit Testing #
    it('should get list of projects', () => {
        service.getProjects().subscribe((response) => {
            expect(response).toBeDefined();
            expect(response.length).toEqual(3);
            expect(response[0]['ProjectName']).toEqual('project 1');
            expect(response[1]['ProjectName']).toEqual('project 2');
            expect(response[2]['ProjectName']).toEqual('project 3');
        });

        const url = service.getProjectsURL;
        const request = http.expectOne(req => req.url === url && req.method === 'GET');
        request.flush({value: projects});
        http.verify();
    });

    const request = http.expectOne(req => test(req, url));

    function test(req, url): boolean {
        return (req.url === url && req.method === 'GET');
    }

Another example:  

    it(`sendData() should update a model where the version has changed`, async(() => {
        const formData: FormData = new FormData();
        component.modelService.selectedDataModel = testDataModel;
        component.formData = formData;
        spyOn(component.dataModelService, 'uploadDataModel').and.returnValue(of(component.dataModelService.selectedDataModel));
        spyOn(component, 'updateModelList');
        spyOn(component, 'cleanUp');
        component.sendData(component.dataModelService.selectedDataModel, true, true);
        expect(component.dataModelService.uploadDataModel).toHaveBeenCalledWith(component.formData);
        expect(component.updateModelList).toHaveBeenCalled();
        expect(component.saveMessage).toEqual('The data model has been successfully updated ');
        expect(component.resultStatus).toBeTruthy();
        expect(component.cleanUp).toHaveBeenCalled();
    }));

