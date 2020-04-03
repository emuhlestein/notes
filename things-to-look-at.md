# Things I need to take a closer look at

## JavaScript
* Array.filter, indexOf, index, find
* Array deconstruction
* 3 == '3' is true

OAuth, web tokens

background: url('img/header.jpg') no-repeat center center;  
background-size: cover;  

IIFE (Immediately-invoked Function Expression). [IIFE](https://flaviocopes.com/javascript-iife/)

 npm install lodash ngx-loading --save  
 
 Angular Routing
 
 Need to look at defining custom colors.  
 transition  
 &.active  
 &hover:not(.active)
 
 
    .navbar {  
        background: $alt-bg;  
        border-bottom: 3px solid $accent;  
        top: 1.5rem;  
        .navbar-nav .nav-link {  
            color: $alt-color;  
            padding: 1rem 0.5rem;  
            transition: color 0.2s ease-in;  
            &.active {  
                color: $accent;  
            }  
            &.hover:not(.active) {  
                color: rgba($alt-color, 0.75);  
            }  
        }  
    }  
