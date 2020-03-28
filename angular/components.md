# Components
[Back](./angular.md)

## Component Communication
* Communicating with a template  
* Communicating with a service  
* Communicating with the router  

### Communicating With A Template
#### Interpolation

Interpolation binds a property of the class with its template. The property is rendered in the view of the template.

Template

    <div>
        {{pageTitle}}
    </div>
    
Component

    pageTitle: string = 'The title page';
    
#### Property Binding

Template

    <img [style.width.px]='imageWidth>
    
Component

    imageWidth: number = 50;
    
#### Event Binding

Template
    
    <button (click)='toggleItem'>Show Item</button>
    
Component

    toggleItem(): void {
      this.showItem = !this.showItem;
    }
    
#### Two-Way Binding

Template
    <input type='text' [(ngModel)]='firstName' />
    
Component
    firstName: string;
    
At times, need to be able to intercept the value that is being assigned to the class property so that some operation can be performed when the property value changes.
    
#### Structural Directives

* \*ngIf
* \*ngFor
