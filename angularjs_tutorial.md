#  AngularJS Tutorial

## Introduction
AngularJS is a JavaScript Framework and distributed as a JavaScript file, and can be added to a web page with a script tag:
```JavaScript
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
```

###  AngularJS Directive

 AngularJS extends HTML with *ng-directives*.

 The directives usually fall into one of two categories:

  * Observing directives, such as double-curly expressions {{expression}}, register listeners using the $watch() method. This type of directive needs to be notified whenever the expression changes so that it can update the view.

  * Listener directives, such as ng-click, register a listener with the DOM. When the DOM listener fires, the directive executes the associated expression and updates the view using the $apply() method.
  *

A special type of scope is the isolate scope, which does not inherit prototypically from the parent scope. This type of scope is useful for component directives that should be isolated from their parent scope.

  directive | comments
  ----------|----------
   ng-app   | defines an AngularJS application
   ng-model | binds the value of HTML controls (input, select, textarea) to application data.
   ng-bind  | binds application data to the HTML view.
   ng-init  | initializes AngularJS application variables

*use data-ng-, instead of ng-, if you want to make your page HTML valid*


###  AngularJS Expressions
AngularJS expressions are written inside double braces: {{ expression }}.

#### AngularJS Expressions vs. JavaScript Expressions
AngularJS expressions are like JavaScript expressions with the following differences:

*  Context: JavaScript expressions are evaluated against the global window. In AngularJS, expressions are evaluated against a scope object.
*  Forgiving: In JavaScript, trying to evaluate undefined properties generates ReferenceError or TypeError. In AngularJS, expression evaluation is forgiving to undefined and null.
*  Filters: You can use filters within expressions to format data before displaying it.
*  No Control Flow Statements: You cannot use the following in an AngularJS expression: conditionals, loops, or exceptions.
*  No Function Declarations: You cannot declare functions in an AngularJS expression, even inside ng-init directive.
*  No RegExp Creation With Literal Notation: You cannot create regular expressions in an AngularJS expression. An exception to this rule is ng-pattern which accepts valid RegExp.
*  No Object Creation With New Operator: You cannot use new operator in an AngularJS expression.
*  No Bitwise, Comma, And Void Operators: You cannot use Bitwise, , or void operators in an AngularJS expression.

If you want to run more complex JavaScript code, you should make it a controller method and call the method from your view. If you want to eval() an AngularJS expression yourself, use the $eval() method.

#### Context
AngularJS does not use JavaScript's eval() to evaluate expressions. Instead AngularJS's $parse service processes these expressions.

AngularJS expressions do not have direct access to global variables like window, document or location. This restriction is intentional. It prevents accidental access to the global state – a common source of subtle bugs.

Instead use services like $window and $location in functions on controllers, which are then called from expressions. Such services provide mockable access to globals.

It is possible to access the context object using the identifier **this** and the locals object using the identifier **$locals**.

**$event**

Directives like ngClick and ngFocus expose a $event object within the scope of that expression. The object is an instance of a [jQuery Event Object](http://api.jquery.com/category/events/event-object/) when jQuery is present or a similar jqLite object.

**One-time binding**

An expression that starts with :: is considered a one-time expression. One-time expressions will stop recalculating once they are stable, which happens after the first digest if the expression result is a non-undefined value (see value stabilization algorithm below).

If the expression will not change once set, it is a candidate for one-time binding.


### [Interpolation and data-binding](https://docs.angularjs.org/guide/interpolation)
During the compilation process the compiler uses the **$interpolate** service to see if text nodes and element attributes contain interpolation markup with embedded expressions.

If that is the case, the compiler adds an interpolateDirective to the node and registers watches on the computed interpolation function, which will update the corresponding text nodes or attribute values as part of the normal [digest](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$digest) cycle.

Note that the interpolateDirective has a priority of 100 and sets up the watch in the preLink function.

#### Binding to boolean attributes
Attributes such as disabled are called boolean attributes, because their presence means true and their absence means false. We cannot use normal attribute bindings with them, because the HTML specification does not require browsers to preserve the values of boolean attributes. This means that if we put an AngularJS interpolation expression into such an attribute then the binding information would be lost, because the browser ignores the attribute value.

AngularJS provides special ng-prefixed directives for the following boolean attributes: disabled, required, selected, checked, readOnly , and open.

If one wants to modify a camelcased attribute (SVG elements have valid camelcased attributes), such as viewBox on the svg element, one can use underscores to denote that the attribute to bind to is naturally camelcased.


#### ngAttr for binding to arbitrary attributes
If an attribute with a binding is prefixed with the ngAttr prefix (denormalized as ng-attr-) then during the binding it will be applied to the corresponding unprefixed attribute.

#### Dynamically changing an interpolated value
You should avoid dynamically changing the content of an interpolated string (e.g. attribute value or text node). Your changes are likely to be overwritten, when the original string gets evaluated. This restriction applies to both directly changing the content via JavaScript or indirectly using a directive.

For example, you should not use interpolation in the value of the style attribute (e.g. style="color: {{ 'orange' }}; font-weight: {{ 'bold' }};") and at the same time use a directive that changes the content of that attribute, such as ngStyle.



### AngularJS Applications
AngularJS modules define AngularJS applications.

AngularJS controllers control AngularJS applications.

```JavaScript
<div ng-app="myApp" ng-controller="myCtrl">

First Name: <input type="text" ng-model="firstName"><br>
Last Name: <input type="text" ng-model="lastName"><br>
<br>
Full Name: {{firstName + " " + lastName}}

</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.firstName= "John";
    $scope.lastName= "Doe";
});
</script>
```

## AngularJS Expressions
Two ways to use expressions:

 * written inside double braces: {{ expression }}
 * written inside a directive: ng-bind="expression"

AngularJS expressions are much like JavaScript expressions

If the ng-app directive is removed, HTML will display the expression as it is, without solving it

#### AngularJS Objects
```JavaScript
<div ng-app="" ng-init="person={firstName:'John',lastName:'Doe'}">

<p>The name is {{ person.lastName }}</p>

</div>
```

#### AngularJS Arrays
```JavaScript
<div ng-app="" ng-init="points=[1,15,19,2,40]">

<p>The third result is <span ng-bind="points[2]"></span></p>

</div>
```
#### AngularJS Expressions vs. JavaScript Expressions

|                                          |  AngularJS  |  JavaScript|
|------------------------------------------| ------------|------------|
|Contain literals, operators, and variables| Yes| Yes|
|  Written inside HTML                     | Yes  | No|
|  Support filters|  Yes | No  |


#### AngularJS Modules
An AngularJS module defines an application.

The module is a container for the different parts of an application.

The module is a container for the application controllers.

Controllers always belong to a module.

##### Adding a Controller
refer to the controller with the ng-controller directive

##### Adding a Directive
built-in directives:
https://www.w3schools.com/angular/angular_ref_directives.asp

In addition you can use the module to add your own directives to your applications:
```JavaScript
<div ng-app="myApp" w3-test-directive></div>

<script>
var app = angular.module("myApp", []);

app.directive("w3TestDirective", function() {
    return {
        template : "I was made in a directive constructor!"
    };
});
</script>

```
>The [] parameter in the module definition can be used to define dependent modules.
>Without the [] parameter, you are not creating a new module, but retrieving an existing one.



#### When to Load the Library
While it is common in HTML applications to place scripts at the end of the <body> element, it is recommended that you load the AngularJS library either in the <head> or at the start of the <body>. This is because calls to angular.module can only be compiled after the library has been loaded.


#### AngularJS Directives
AngularJS directives are extended HTML attributes with the prefix ng-.

>Using ng-init is not very common.


#### Repeating HTML Elements
The ng-repeat directive repeats an HTML element:
```JavaScript
<div ng-app="" ng-init="names=['Jani','Hege','Kai']">
  <ul>
    <li ng-repeat="x in names">
      {{ x }}
    </li>
  </ul>
</div>
```

#### Create New Directives

New directives are created by using the .directive function. module.directive takes the normalized directive name followed by a factory function. This factory function should return an object with the different options to tell $compile how the directive should behave when matched.

The factory function is invoked only once when the compiler matches the directive for the first time. You can perform any initialization work here. The function is invoked using $injector.invoke which makes it injectable just like a controller.

To invoke the new directive, make an HTML element with the same tag name as the new directive.

When naming a directive, you must use a camel case name, w3TestDirective, but when invoking it, you must use - separated name, w3-test-directive:

```JavaScript
<body ng-app="myApp">

<w3-test-directive></w3-test-directive>

<script>
var app = angular.module("myApp", []);
app.directive("w3TestDirective", function() {
    return {
        template : "<h1>Made by a directive!</h1>"
    };
});
</script>

</body>

```
You can invoke a directive by using:

  Methods | Example
  --------|--------
  Element name|  ```  <w3-test-directive></w3-test-directive> ```
  Attribute|  ```<div w3-test-directive></div>```
  Class|  ``` <div class="w3-test-directive"></div>```
  Comment | ``` <!-- directive: w3-test-directive -->```

>  Best Practice: Unless your template is very small, it's typically better to break it apart into its own HTML file and load it with the templateUrl option.

#### Restrictions
You can restrict your directives to only be invoked by some of the methods.

```JavaScript
var app = angular.module("myApp", []);
app.directive("w3TestDirective", function() {
    return {
        restrict : "A",
        template : "<h1>Made by a directive!</h1>"
    };
});
```

The restrict option is typically set to:

* 'A' - only matches attribute name
* 'E' - only matches element name
* 'C' - only matches class name
* 'M' - only matches comment

By default the value is EA, meaning that both Element names and attribute names can invoke the directive.

### AngularJS ng-model Directive

To create a component, we use the .component() method of an AngularJS module. We must provide the name of the component and the Component Definition Object (CDO for short).

Remember that (since components are also directives) the name of the component is in camelCase (e.g. myAwesomeComponent), but we will use kebab-case (e.g. my-awesome-component) when referring to it in our HTML. (See here for a description of different case styles.)

#### Validate User Input
```JavaScript
<form ng-app="" name="myForm">
    Email:
    <input type="email" name="myAddress" ng-model="text">
    <span ng-show="myForm.myAddress.$error.email">Not a valid e-mail address</span>
</form>

```


#### Application Status
```JavaScript
<form ng-app="" name="myForm" ng-init="myText = 'post@myweb.com'">
    Email:
    <input type="email" name="myAddress" ng-model="myText" required>
    <h1>Status</h1>
    {{myForm.myAddress.$valid}}
    {{myForm.myAddress.$dirty}}
    {{myForm.myAddress.$touched}}
</form>
```

#### CSS Classes
```JavaScript
<style>
input.ng-invalid {
    background-color: lightblue;
}
</style>
<body>

<form ng-app="" name="myForm">
    Enter your name:
    <input name="myName" ng-model="myText" required>
</form>
```

### AngularJS Controllers
A controller is a JavaScript Object, created by a standard JavaScript object constructor.

```JavaScript
<div ng-app="myApp" ng-controller="myCtrl">

First Name: <input type="text" ng-model="firstName"><br>
Last Name: <input type="text" ng-model="lastName"><br>
<br>
Full Name: {{firstName + " " + lastName}}

</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.firstName = "John";
    $scope.lastName = "Doe";
});
</script>
```
Application explained:

The AngularJS application is defined by  ng-app="myApp". The application runs inside the <div>.

The ng-controller="myCtrl" attribute is an AngularJS directive. It defines a controller.

The myCtrl function is a JavaScript function.

AngularJS will invoke the controller with a $scope object.

In AngularJS, $scope is the application object (the owner of application variables and functions).

The controller creates two properties (variables) in the scope (firstName and lastName).

The ng-model directives bind the input fields to the controller properties (firstName and lastName).

#### Controller Methods

### AngularJS Scope
The scope is the binding part between the HTML (view) and the JavaScript (controller).

The scope is an object with the available properties and methods.

The scope is available for both the view and the controller.

When you make a controller in AngularJS, you pass the $scope object as an argument

#### Understanding the Scope
If we consider an AngularJS application to consist of:

* View, which is the HTML.
* Model, which is the data available for the current view.
* Controller, which is the JavaScript function that makes/changes/removes/controls the data.

Then the scope is the Model.

It is important to know which scope you are dealing with, at any time.

#### Root Scope
All applications have a $rootScope which is the scope created on the HTML element that contains the ng-app directive.

The rootScope is available in the entire application.

If a variable has the same name in both the current scope and in the rootScope, the application uses the one in the current scope.

Scopes can propagate events in similar fashion to DOM events. The event can be broadcasted to the scope children or emitted to scope parents.

[Scope Life Cycle](https://docs.angularjs.org/guide/scope)

The normal flow of a browser receiving an event is that it executes a corresponding JavaScript callback. Once the callback completes the browser re-renders the DOM and returns to waiting for more events.

When the browser calls into JavaScript the code executes outside the AngularJS execution context, which means that AngularJS is unaware of model modifications. To properly process model modifications the execution has to enter the AngularJS execution context using the $apply method. Only model modifications which execute inside the $apply method will be properly accounted for by AngularJS. For example if a directive listens on DOM events, such as ng-click it must evaluate the expression inside the $apply method.

After evaluating the expression, the $apply method performs a $digest. In the $digest phase the scope examines all of the $watch expressions and compares them with the previous value. This dirty checking is done asynchronously. This means that assignment such as $scope.username="angular" will not immediately cause a $watch to be notified, instead the $watch notification is delayed until the $digest phase. This delay is desirable, since it coalesces multiple model updates into one $watch notification as well as guarantees that during the $watch notification no other $watches are running. If a $watch changes the value of the model, it will force additional $digest cycle.


### AngularJS Filters

AngularJS provides filters to transform data:

* currency Format a number to a currency format.
* date Format a date to a specified format.
* filter Select a subset of items from an array.
* json Format an object to a JSON string.
* limitTo Limits an array/string, into a specified number of elements/characters.
* lowercase Format a string to lower case.
* number Format a number to a string.
* orderBy Orders an array by an expression.
* uppercase Format a string to upper case.

```JavaScript
<div ng-app="myApp" ng-controller="personCtrl">

<p>The name is {{ lastName | uppercase }}</p>

</div>
```
Filters may have arguments. The syntax for this is:
```
{{ expression | filter:argument1:argument2:... }}
```
#### When filters are executed
In templates, filters are only executed when their inputs have changed. This is more performant than executing a filter on each $digest as is the case with expressions.

There are two exceptions to this rule:

 1. In general, this applies only to filters that take primitive values as inputs. Filters that receive Objects as input are executed on each $digest, as it would be too costly to track if the inputs have changed.

 2. Filters that are marked as $stateful are also executed on each $digest. See Stateful filters for more information. Note that no AngularJS core filters are $stateful.

### AngularJS Services
In AngularJS, a service is a function, or object, that is available for, and limited to, your AngularJS application.

AngularJS has about 30 built-in services.

The $location service has methods which return information about the location of the current web page.

$http Service makes a request to the server, and lets your application handle the response.

$timeout is AngularJS' version of the window.setTimeout function.

$interval service is AngularJS' version of the window.setInterval function.

#### Create Your Own Service
```JavaScript
app.service('hexafy', function() {
    this.myFunc = function (x) {
        return x.toString(16);
    }
});


app.controller('myCtrl', function($scope, hexafy) {
    $scope.hex = hexafy.myFunc(255);
});

```

### ngRoute


### Promise

P&S

P: a modal dialog was hide behinde backdrop, that made the dialog look tinted and made the dialog not to get inputs
S:  If the modal container has a fixed or relative position or is within an element with fixed or relative position this behavior will occur. *Make sure the modal container and all of its parent elements are positioned the default way to fix the problem.*
https://stackoverflow.com/questions/10636667/bootstrap-modal-appearing-under-background


## Reference
http://www.bogotobogo.com/AngularJS/AngularJS_Introduction.php
