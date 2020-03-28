# Flex Layout

Need to include FlexLayoutModule.

    import { FlexLayoutModule } from @angular/flex-layout;

    @NgModule({
    ...
    imports: [
       FlexLayoutModule
    ]
    ...
    })
    export class AppModule {}

Good idea to create a material module for all material modules.

[Flex Wiki](https://github.com/angular/flex-layout/wiki)
[CSS Flex](https://developer.mozilla.org/en-US/docs/Web/CSS/flex)

"CSS breakpoints are points where the website content responds according to the device width, allowing you to show the best possible layout to the user.

"CSS breakpoints are also called media query breakpoints, as they are used with media query."

Media query

It uses the @media rule to include a block of CSS properties only if a certain condition is true.

Media queries can help with that. We can add a breakpoint where certain parts of the design will behave differently on each side of the breakpoint.

