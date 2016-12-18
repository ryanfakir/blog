---
title: "Angular Checkbox"
date: "2016-12-18"
description: "v0.01"
categories:
    - "angualr"
---

If we need make some directives like widgets — meaning drag and use, how to we want to design it, let’s practice from ground.  
Right now we have  

```html
<input id="action" type="checkbox">  
<label for="action">Action will triggerlabel>  
```

### Case 1

When I check the checkbox, I want to fire event which will call backend service.  
You may want to code like this:  


```golang
@Directive({
  selector: 'input[action]',
  events: ['callBackend'],
  host: {
    '(change)': 'emitOut()'
  }

})
export class CheckboxTriggerActionDirective {
  callBackend: EventEmitter<any> = new EventEmitter();

  emitOut() {
    this.callBackend.emit('checkbox emit data out side');
  }
} 
```

And you put directive like this:  


```javascript
 ||         ||  
 \/         \/  
<input id="action" type="checkbox" action (callBackend)="callbackend($event)">  
<label for="action">Action will triggerlabel>  
```

Let’s talk basic angular2 important knowledge real quick:

1.  Angular2 have two main decorators (@Directive and @Component), or you can understand as Annotation if you are Java Guy, which put the metadata(additional informative data) above class definition, to let Angular2 compiler to know when and where to apply the functionality you are defined.
2.  You can briefly take @Component = @Directive + Template.
3.  In Angular2 Data flow is one way, always from Component class instance member(Ex. callBackend is instance member of class CheckboxTriggerActionDirective) to template.

* * *

In our example,  
[selector] will ask angular to parse template to find tag input which have attribute “action”.  
[events] which tell angular this directive will have customize-event which in our application somewhere it can be listen to or subscribe to.  
[host] means the DOM element which hosts our directive, in our case is input, it means when we hear some change events happened from host element, our directive will call function emitOut().  
Remember (xxx) means output from DOM element, it can be built-in event or customize function call. In emitOut() our customized event will shout out, our application can listen to the value or message it sends(this message can be object or internal usefully information which can let whole world know you LOL), and do some action(EX. call backend service).

* * *

### Data flow:

checkbox status changed ——> call emitOut() ——> callBackend emit message ——> observer or listener will do operations

Next we will make our checkbox more generic and reusable.

* * *