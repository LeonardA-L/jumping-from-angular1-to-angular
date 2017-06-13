Let's take a look at how Data-Binding works in Angular. Displaying stuff in your template is still done with the `{{ doubleCurlyBrackets }}` notation. Other than that, passing variables and events to components happens with different notations.

# Variables (input)

You use input binding to pass the value of a variable to a child component. In **Angular1** you used to do something like this:

```html
<directive child-name="scopeVariable">
```

But now with **Angular**, you will use the `[]` square bracket notation, like so:

```html
<directive [childName]="scopeVariable">
```

This binds *value*. It actually binds to an attribute of the child component that has been marked as an input with the `@Input` decorator.

```javascript
@Component({
  ...
})
class Compo {
  @Input()
  public param;
}
```

Let's try it out, shall we?

@[Input demo]({"stubs": ["input/app/box.ts", "input/app/app.component.ts"], "command": "/bin/sh /project/target/input/run.sh"})

# Events (output)

Two-ways binding doesn't really exist in Angular anymore. Now, when you want to send data upward to the parent component, you need to use events. Events are defined with the `()` notation like this:

```html
<directive (theEvent)="theScopeFunction($event)">
```

Guess what? A bunch of events already exist, known as the [HTML DOM events](https://www.w3schools.com/jsref/dom_obj_event.asp). The same ones you used to prepend `ng-` to. You can now use what used to be `ngClick` like this:

```html
<button (click)="clickButton()">
```

You can also define your own output events using the *EventEmitter* system. Let's say you want to create a `highlight` event that is triggered when the user highlights an *item* in a *list*. First, you define an event emitter with the `@Output` decorator, use it to send events with the `next` method. It will then be exposed to the parent component via the `(highlight)` attribute (note the use of the event syntax `()`). Here's a simple snippet:

@[Output demo]({"stubs": ["output/app/list.ts", "output/app/app.component.ts"], "command": "echo 'CG> open --static-dir /project/target/output index.html'"})

## What happened to...

### `ng-class` and angular-specific directives?

`ngClass`, and others such as `ngStyle` are bound like regular variables,

```html
<directive [ngClass]="scopeVariable">
```

### `ng-model`?

`ngModel` is a bit different because it is both downward and upward, both input and output, right? No worries, Angular got you covered:

```html
<input [(ngModel)]="scopeVariable">
```

