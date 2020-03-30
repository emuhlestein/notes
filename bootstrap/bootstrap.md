# Bootstrap
[Back](../README.md)

Go to [Bootstrap Getting Started](https://getbootstrap.com/docs/4.4/getting-started/introduction/) page and copy the starter template into the index.html file.

## Graphic Design

CARP

* Contrast Elements being strikingly different from one another
* Alignment
* Repetition - Repeat various elements in design: color, thickness, graphic, text, ...
* Proximity - Group things together

## Colors

![Alt text](./yellow.svg)  

All of the [bootstrap colors](./bootstrap-colors.md)

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


    \<section class="container">  
      \<section class="row">  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
        \<div class="col">Equal\</div>  
      \</section>  
    \</section>  
    
    // this is not responsive, ie as the window width is shrunk, the columns don't stack
     <section class="container">
      <section class="row">
        <div class="col">Auto</div> // this takes up the remaining space. it is auto.
        <div class="col-8">Auto</div>
        <div class="col-2">Auto</div>
      </section>
    </section>

This is a responsive layout

   <section class="container">
      <section class="row">
        <div class="col-sm">Auto</div>
        <div class="col-sm">Auto</div>
        <div class="col-sm">Auto</div>
      </section>
    </section>
    
    
    nesting 2 columns inside the first column
    
       <section class="container">
      <section class="row">
        <div class="col bg-warning">
          First
          <section class="row">
            <div class="col bg-info">Second</div>
            <div class="col bg-success">Third</div>
          </section>
        </div>
      </section>
    </section>
    
    
      <section class="container">
      <section class="row">
            <div class="col-6ol-xl-8 bg-warning">
                <p>SM: 576px<br>MD: 768px<br>LG: 992px<br>XL: 1200px</p>
            </div>
      </section>
    </section>


    <section class="container">
      <section class="row">
        <div class="col-6 bg-info">1</div>
        <div class="col-6 bg-secondary">2</div>
      </section>
      <section class="row">
        <div class="col-4 bg-info">1</div>
        <div class="col-4 bg-secondary">2</div>
        <div class="col-4 bg-success">3</div>
      </section>
      <section class="row">
        <div class="col-3 bg-info">1</div>
        <div class="col-3 bg-secondary">2</div>
        <div class="col-3 bg-success">3</div>
        <div class="col-3 bg-danger">4</div>
      </section>
    </section>
