# Bootstrap
[Back](./angular.md)

Go to [Bootstrap Getting Started](https://getbootstrap.com/docs/4.4/getting-started/introduction/) page and copy the starter template into the index.html file.

## Graphic Design

CARP

* Contrast Elements being strikingly different from one another
* Alignment
* Repetition - Repeat various elements in design: color, thickness, graphic, text, ...
* Proximity - Group things together

## Colors

All of the bootstrap colors:

    <div class="myDiv bg-primary">Hello Bootstrap</div>
    <div class="myDiv bg-secondary">Hello Bootstrap</div>
    <div class="myDiv bg-success">Hello Bootstrap</div>
    <div class="myDiv bg-danger">Hello Bootstrap</div>
    <div class="myDiv bg-warning">Hello Bootstrap</div>
    <hr>
    <div class="myDiv bg-info">Hello Bootstrap</div>
    <div class="myDiv bg-light text-dark">Hello Bootstrap</div>
    <div class="myDiv bg-dark">Hello Bootstrap</div>
    <div class="myDiv bg-white text-dark">Hello Bootstrap</div>
    <div class="myDiv bg-transparent text-dark">Hello Bootstrap</div>

The **container** class adds margin and padding to div. It is jumpy when resize window because of the breakpoints.
The **container-fluid** class is smooth when scrolling.

Bootstrap is based on a 12-column layout.

For responsive layout, the container class is optional but to have multi-column layout, need to put columns inside a row tag.
    <div class="container">
        <div class="row"></div>
    </div>
    
### Breakpoints
* min-width: 1200px - XL
* min-width: 992px - LG
* min-width: 768px - MD
* min-width: 576px - SM
* min-width: 578.98px - and below - xtra-SM




## ng-bootstrap

[ng-bootstrap](https://ng-bootstrap.github.io/#/home)

It is a native Angular implementation for Bootstrap components.

* CSS for layout, content, etc
* JavaScript for components.
* No dependency on JQuery



