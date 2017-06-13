In Angular1, you used to create `component` or directives in Angular1 to make reusable web components. They still exist in Angular, and they are awesome!

Most of the things you do in Angular will be components. For example:

* Where you used AngularJS directives, you will use components
* Where you used AngularJS modules, you will almost always use components
* Where you used AngularJS components, you will use components

# Syntax

In Angular1, you would declare a component like this:

```javascript
theModule.component('componentName', {
  templateUrl: 'path/to/template.html',
  controller: function() {
    ...
  }
});
```

But hey, how does it work? How do I use this component in a template? There is some angular1 magic where camel case `<componentName>` will become `<component-name>` but it's kinda odd, especially since you didn't ask for it. What if I want to specify a custom tag name that is different from the name of the component?

Let's look at how Angular does it. You need a class and a `@Component` decorator:

```javascript
@Component({
  selector: 'compo',
  templateUrl: './compo.html',
  styleUrls: ['./compo.css'],
})
class Compo {
  awesome: string = 'yes';
}
```

* `selector` is the tag name
* `templateUrl` is the same as in Angular1, you can also use inline `template`
* `styleUrls`, this is the cool new feature as you can add a list of stylesheets to include. You can also use inline `styles`

The class serves as a controller for your component.

Cleaner. Leaner. Let's try it out:

@[Component demo]({"stubs": ["components/app/sample.ts"], "command": "echo 'CG> open --static-dir /project/target/components index.html'"})

In order to register and use them, declare your components in your `@NgModule`, in order to register it and be able to use it. Add it to the list of component declarations of your module:

```javascript
@NgModule({
  ...
  declarations: [
    TheComponent,
    ...
  ],
  ...
}
```

# Advanced

There are a bunch of other properties associated with the `@Component` decorator, like a list of `providers` it will use. You need to reference these providers if your component uses them.

Refer to [the official Component documentation](https://angular.io/docs/ts/latest/api/core/index/Component-decorator.html) for a list of usable properties.

## What happened to...

### The `$onInit`, `$onDestroy`, `$onChanges` hooks?

Angular component have a series of lifecycle hooks you can use. A complete list and guide are [available here](https://angular.io/docs/ts/latest/guide/lifecycle-hooks.html).

To use one of these hooks, `OnInit` for instance, first thing first you will need to import it from the Angular core library:

```javascript
import { OnInit } from '@angular/core';
```

Next, you will need to have your component class implement `OnInit` (and any other hook you need):

```javascript
@Component({
  ...
})
class Compo implements OnInit {
  ...
}
```

Lastly, you can add a `ngOnInit` function to this component class:

```javascript
ngOnInit() {
  this.logIt('On Init');
}
```

### Transclusion?

AngularJS directives used to have a `transclude` property, but now Angular components support transclusion by default. Just use the `<ng-content>` tag in your template like so:

```html
<div class="component">
  <ng-content><!-- Transcluded data, if any, will come here --></ng-content>
</div>
```

Then, call your component with data that will be transcluded automatically

```html
<my-component>Data to be transcluded</my-component>
```
