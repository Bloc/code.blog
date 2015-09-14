Modals have been a source of contention with me since I first started developing for the web. Most of my attempts to write custom modals have been swallowed by bootstrap's magic or jQuery.

My most recent task was to convert a quick survey pop-up to our students into a modal and required me to build that reusable magic on my own.

[Bloc's](https://www.bloc.io) tech stack is comprosed of a Rails for API and Angular 1.2.x to do a lot of driving for the rich frontend. It's apparent that Angular 2 is a rethink of Angular, which is causing a lot of companies to change the way they are implementing Angular. 

Knowing this, all new Angular code for Bloc has been sectioned off into a directory called `components`. Each component is a separate piece of code that could work on independtly if neccessary.

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

The Angular module is created in `index.js` and added to our `ng-app-init.js` file for easy access in the our app structure.  
```
var angular = require('angular');
var NpsFormOverlay = angular.module('NpsFormOverlay', []);

require('./directive');

module.exports = NpsFormOverlay;
```
This file includes a call to the directive and exports the entire component as its own `NpsFormOverlay` with the `module.exports` declaration.

**directive.js**

Similar to `index.js`, the directive collects the work from the controller, stylesheet, and template as it's own and gets required as you recall in `index.js`.

<script src="https://gist.github.com/bdougie/508172013112b0490a97.js"></script>

Some things to note is that we are using the slightly different [as syntax](http://toddmotto.com/digging-into-angulars-controller-as-syntax/), using `this` in favor of `$scope`.

**controller.js**

<script src="https://gist.github.com/bdougie/6e1b673818929b439a66.js"></script>

**assets and template.html**

Stylesheets and templates can live inside your directive like a beautiful component. Nothing really different here other than the placement of these files, but just know they live in the directive component and not the normal template and asset folders.

**Rendering this wherever**

Finally, the way to implement this modal directive only requires using the Angular directive syntax of a custom `<NpsFormOverlay></NpsFormOverlay>` tags.

**My thoughts:**

What I like about this modal implementation is that it mirrors the popularity of [Webcomponents](http://www.2ality.com/2015/08/web-component-status.html) and this enables us to upgrade portions of our Angular code by component by component if need be.

With this also being a component, I could easily rewrite/test this component using [React](https://github.com/davidchang/ngReact) or any other popular Javascript or css library without affecting the rest of our frontend Angular codebase. 
**Perhaps an idea for another blog post*.
