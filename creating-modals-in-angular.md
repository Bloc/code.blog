Modals have been a contention with me since I first started developing for the web. For the most part most my attempts to write a custom modal have been swallowed up with a magical bootstrap implementation that includes a little jQuery sprinkled in. 

My most recent task was to convert a quick survey pop-up to our students into a modal and required me to hand build that reusable magic on my own.

Our tech stack here at [Bloc](http://bloc.io) includes a Rails for Api and Angular 1.2.x to do a lot of driving for the Frontend. It is very apparent that Angular 2 is a rethink and refactoring of Angular, which is causing a lot of companies to rethink the way they are implementing Angular. 

Knowing this, all new Angular code for Bloc has been section off into a folder called `components`, separate pieces of code that could work on its own if needed.

The path to doing this is using an [Angular Directive](https://docs.angularjs.org/guide/directive) to display a reusable modal. The file structure for this directive includes the following files:

```
NpsOverlayForm/
  achievement_nps.gif
  controller.js
  directive.js
  index.js
  style.css.sass
  template.html
```  

*The implementation:*

**index.js**

The `index.js` is the platform to create your Angular module and to be added your in `ng-app-init.js` file for easy access in your file structure.  
```
var angular = require('angular');
var NpsFormOverlay = angular.module('NpsFormOverlay', []);

require('./directive');

module.exports = NpsFormOverlay;
```
This file includes a call to the directive and exports the entire component as it's own `NpsFormOverlay` with the `module.exports` declaration.

**directive.js**

Similar to the `index.js`, the directive collects the work from the controller, stylesheet, and template as it's own and gets required as you recall in the `index.js`.

<script src="https://gist.github.com/bdougie/508172013112b0490a97.js"></script>

Some things to note is that we are using the slightly different [as syntax](http://toddmotto.com/digging-into-angulars-controller-as-syntax/), using `this` in favor of `$scope`.

**controller.js**

<script src="https://gist.github.com/bdougie/6e1b673818929b439a66.js"></script>

**assets and template.html**

Stylesheets and Templates can live inside your directive like a beautiful component. Nothing really different here other than the placement of these files, but just know they live in the directive component and not the normal template and asset folders.

**Rendering this wherever**

Finally the way to implement this modal directive only requires using the Angular directive syntax of a custom `<NpsFormOverlay></NpsFormOverlay>` tags.

**My thoughts:**

What I like about this modal implementation is that it mirrors the popularity of [Webcomponents](http://www.2ality.com/2015/08/web-component-status.html) and this enables us to upgrade portions of our Angular code by component by component if need be.

With this also being a component, I could easily rewrite/test this component using [React](https://github.com/davidchang/ngReact) or any other popular javascript or css library without affecting the rest of our frontend Angular codebase. 
**Perhaps an idea for another blog post*.
