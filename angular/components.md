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
    <input type='text' [(**ngModel**)]='listFilter' />

Can be customer directive or child component:

    @ViewChild(**StarComponent**) star: StarComponent;
    <**pm-star** [rating]='product.starRating'></pm-star>
    
Template Reference variable

   @ViewChild('divElementVar') divElementRef: ElementRef;  
   \<div #divElementVar>{{pageTitle}}\</div>

Component life cycle
1. Component is constructed - constructor()
2. Component is initilaized - ngOnInit()
3. The view is initialized and rendered - ngAfterViewInit()

     @ViewChild('filterElement') filterElementRef: ElementRef;  
    ngAfterViewInit(): void {
       this.filterElementRef.nativeElement.focus();
    }

Good to check for existance of nativeElement:

    if ( this.filterElementRef.nativeElement) {
       this.filterElementRef.nativeElement.focus();
    }

Accessing Native Elements
* Directly accesses the DOM
* Tightly coupled to the browser
* May not be able to use server-side rendering or web workers
* Can pose a security threat: cross side scripting attacks XXX

Be careful when there are \*ngIfs. NOTE: need to look at this in more depth. Maybe better to not use \*ngIf when needing to access child elements.

ngOnChanges(changes: SimpleChanges){} is a lifecycle hook that gets called whenever any input property changes. The changes parameter has the current and previous value of all the input properties. Can only use this in a child component with @Input().

    ngOnChanges(changes; SimpleChanges): void {
       if (changes['hitCount'] && !changes['hitCount'].currentValue) {
          this.hitMessage = 'No matches found';
       } else {
          this.hitMessage = 'Hits: ' + this.hitCount;
       }
    }

If there is a child property, that is not designated as an @Output property, there is a way to communicate the value change to the parent.

    someValue: number: // a value bound in the template that a parent is interested in
    
Need to add getter and setter for the property.

    _someValue: number;
    get someValue(): number{
        return this._someValue;
    }
    
    set someValue(value: number) {
        this_someValue = value;
    }
    
The next thing that is needed is an @Output property so the changed value can be emitted to the parent.

    @Output() valueChange: EventEmitter<number> = new EvenetEmitter<number>();
    _someValue: number;
        get someValue(): number{
        return this._someValue;
    }
    
    set someValue(value: number) {
        this_someValue = value;
        // the value has changed, notify the parent
        this.valueChange.emit(value); // The value is the event payload
    }

In the parent template, a method is called when the value changes. The $event is the payload.
    <child (valueChange)='onValueChange($event)'><child>
    
### Communicating Through A Service

A service can maintain state and communicate that state with other components.
What is State?

* View State - What is rendered in the template
* User Information - maybe user settings
* Entity Data - Data retrieved from the backend server
* User Selection and Input
* etc

Types of services:

* Property Bag - a service that just has properties that it shares amoung components. There is no logic.
* State Management - a service that manages application state. It can communicate state changes with built notifications
* State Management with Notifications - State management with notifications using Subject, BehaviorSubject
* ngrx/Redux - Uses State(immutable), Actions(State Changes, Reducers(State+Action=New State), Store(Observableof state...)

When a user navigates away from a component, the component is destroyed and all its state is lost. To remember the state of a component, a service can be used as a means to remember the state. The navigated component is initialized and displayed. When returning to the former component, it is re-created and displayed. All of its state is gone. It is back to its default state.

A service that is used only for maintaining component state is sometimes called a property bag. So the component will not use local properties to save state data, it will store its values in a service.

    export class ProductComponent {
        constructor(private paramService: ParameterService){}
        
        set someProperty(value: number) {
           this.paramService.someProperty = value;
        }
        
        get someProperty(): number {
           return this.paramService.someProperty;
        }
    }

A component cannot remember its state. When navigating away from a component, it is destroyed along with all of its state.

### Services

* Provide funtionaliy across components
* Logging, calculations, data access, data sharing, ...
* Is registered with the angular injector
* Inject service into any component that needs it
* Services are singletons

### Data Access Service

A service that interacts with a backend for retrieving and storing data.

### Keeping Component States in Sync

When a product item is selected in the product list component, need to inform product details component of the selected product.
    export class ProductService {
       currentProduct: IProduct | null;
    }

    <button (click)=onSelected(product)</button>

    export class ProductShellListComponent {
        onSelected(product) {
           this.productService.currentProduct = product;
        }
    }
    
    export class ProductShellDetailsComponent {
       get product() {
          return this.productService.currentProduct;
       }
    }

#### Getter
A getter is a great way to keep bound data in sync
* Define a property in a service
* Bind that property in a template
* Use a getter in the component class
* Angular's change detection does the rest

#### Subject

    export class ProductService {
        private selectedProductSource = new Subject<IProduct | null>();
        selectProductChanges$ = selectedProductSource.asObservable();
        
        changeSelectedProduct(selectedProduct: IProduct | null) {
            selectedProductChanges$.next(selectedProduct);
        }
        
        
        this.changeSelectedProduct(null);
    }

    export class ProductShellListComponent {
        onSelected(product: IProduct) {
            this.productService.changeSelectedProduct(product);
        }
    }
    
    
    export class ProductShellDetailComponent implements  OnInit{
        product: IProduct;
        ngOnInit() {
            this.productService.selectedProductChanges$.subscribe(
                selectedProduct => this.product = selectedProduct;
        }
    }
    
#### BehaviorSubject
* Requires an initial value
* Provides the current value on a new subscription

 export class ProductService {
        private selectedProductSource = new BehaviorSubject<IProduct | null>(null);
        selectProductChanges$ = selectedProductSource.asObservable();
        
        changeSelectedProduct(selectedProduct: IProduct | null) {
            selectedProductChanges$.next(selectedProduct);
        }
        this.changeSelectedProduct(null);
    }

    export class ProductShellListComponent {
        onSelected(product: IProduct) {
            this.productService.changeSelectedProduct(product);
        }
    }
    
    
    export class ProductShellDetailComponent implements  OnInit{
        product: IProduct;
        ngOnInit() {
            this.productService.selectedProductChanges$.subscribe(
                selectedProduct => this.product = selectedProduct;
        }
    }

#### In ProductShellListComponent

    selectedProduct: IProduct | null;
    
    <button [ngClass]="{'active': product?.id === selectedProduct?.id}">{{product.name}}</button>
    
    
    this.subscription = this.productService.selectedProductChanges$.subscribe(
                selectedProduct => this.product = selectedProduct;
                
    ngOnDestroy() {
        this.subscription.unsubscribe();
    }
    
### Routing

    <a [routerLink]="['products']">Product List</a>
This updates the address bar and then the router sees this change then sequentually exams the router table. It the selects the first match it finds:

    { path: 'welcome', component: WelcomeComponent },
    { path: 'products', comopnent: ProductListComponent },
    { path: 'products/:id", component: ProductDetailComponent }
    
The router then takes the selected component and renders it using the <router-outlet></router-outlet> directive.

app router outlet
app shell router outlet
product shell component

#### Route Parameters
* Required - parameter must be defined as part of the router configuration
    * <a [routerLink]="['/products', product.id]">Product List</a>
    * this.router.navigate(['/products', product.id]);
    * this.route.snapshot.paramMap.get('id');
* Optional - Parameters are not defined as part of the router configuration
    * <a [routerLink]="['/products', {name: cart, code: g}]">Product List</a>
    * this.router.navigate(['/products', {name: cart, code: g}]);
    * this.route.snapshot.paramMap.get('name');
* Query - Parameters are not defined as part of the router configuration
    * <a [routerLink]="['/products']" [queryParams]="{name: cart, code: g}">Product List</a>
    * this.router.navigate(['/products'], {queryParams, {name: cart, code: g}});
    * this.route.snapshot.queryParamMap.get('name');
    * retains parameters and can return them.
    



