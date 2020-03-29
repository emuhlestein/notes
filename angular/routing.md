# Routing

this.route.snapshot.paramMap.get('id') is used to get the parameters from the route. snapshot is fine if the route parameters won't change.

Moving away from a component because of a route event, the component is destroyed. When the back button is clicked, the component needs to be re-created.

# Routing
If a component is displayed as part of a route and is not embedded in the template of another component, the selector properity is not needed.

Routing is component based. Need to identify the target component for each route.

The <router-outlet> element determines where the content for each route will be displayed.

    <div class="containter">
        <router-outlet></router-outlet>
    </div>
    
Need to decide whether to nest a component inside another component or route to a component.

For nest-able components, need to define a selector so that it can be nested inside the template of another component. It needs no route.

For routed components, no selector is needed. A route is configured so the component can be rendered. The route needs to be tied to an action.

* Configure routes
* Tie Routes to actions
* Place the view

## Configure Routes
1. Define base element in index.html
2. Add RouterModule
    * Add each route to RouterModule.forRoot()
    * Order matters
3. Define path url segment
    * No leading slash
    * '' for default route
    * '\*\*' for wildcard route if not other route matches
4. A component

## Type Routes to Actions
1. Add the [RouterLink] directive as an attribute to any clickable element.
2. Bind to a link parameters array
    * First element is the path
    * All other elements are route parameters
    
## Place the View
1. Use <router-outlet> directive to identify where the routed component's view will be displayed.
2. Is specified in the host component's template
