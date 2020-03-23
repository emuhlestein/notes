# Link and NavLink #
In a traditional website, when you navigate through the application using anchor links, it results in a page refresh, and all the components in the page are re-rendered. Navigation links created with <Link> and <NavLink> do not result in a page refresh; only those certain sections of the page that are defined using the <Route> and that match the URL path are updated.

A **\<Link\>** component is used to navigate to an existing route that is defined using the **\<Route\>** component. To navigate to a route, specify the pathname used in the route as a value to the **to** prop.

    <Route path="/items" component={ItemList}><Route>
    
