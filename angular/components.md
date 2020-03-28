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
    
At times, need to be able to intercept the value that is being assigned to the class property so that some operation can be performed when the property value changes. The template needs to be able to communicate changes to the component.

#### Structural Directives

* \*ngIf
* \*ngFor

### Ways to notify the component of user changes.
* Two-way binding, the long way
* Getter and Setter
* valueChanges observable



#### Two-way Bind, the hard way

    <input type='text' [(ngModel)]='filterList' />
    
This can be broken down to:

    <input type='text' [ngModel]='firstList'
                       (ngModelChange)='listFilter=$event/>

Then changed to this:

    <input type='text' [ngModel]='firstList'
                       (ngModelChange)='onFilterChange($event)/>

NOTE: $event is the event payload. That is, it holds the contents of the emittted event.

This is not a good way to achieve what is desired.

#### Getters and Setters

There are two ways to define a property in JavaScript: a simple component variable or getters and setters.

In JavaScript a property can also be defined using a getter and a setter.

Common Pattern for Getters and Setters

   private \_listFilter: string;
   
   get listFilter(): string {
      return \_listFilter;
   }
   
   set listFiler(value: string): void {
      \_listFilter = value;
      this.performFilter(value);
   }

#### Guidelines for communication with a template
1. Use the binding and structurall directives
2. Use Getter/Setter if need to check the change and execute some function


### ViewChild

In plain JavaScript:
    let divElement = document.getElementById('divElementId);

In Angular:
    @ViewChild('divElementVar') divElementRef; // divElementVar is the selector for the element

The selector can be an angular directive:
    @ViewChild(**NgModel**) filterInput: NgModel;
    <input type='text' [(ngModel)]='listFilter' />

Can be customer directive or child component:
    @ViewChild(StarComponent) star: StarComponent;
    <pm-star [rating]='product.starRating'></pm-star>
   
   
