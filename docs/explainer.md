# MiniApp Components Explainer 

## Authors

- Zitao Wang (Huawei)
- Martin Alvarez (Huawei)

## 1. Introduction

### What is this?

MiniApp Components are the building blocks to creating MiniApp pages. Each component encapsulates functionality, data, and styles, enabling developers to create custom and reusable items that can be combined to develop MiniApps. MiniApps include essential components like page containers, textual and multimedia content, and other interactive elements such as forms.

This document aims to specify a set of common practices to define MiniApps Components that allow developers to build similar user interfaces across MiniApp platforms efficiently and provide a consistent user experience.


### Why should we care?

Although MiniApps Components share the same concept as Web Components, their capabilities and development features differ. The main differences are motivated by the architecture of the existing implementations along the MiniApp ecosystem following the MVVM pattern, based on components developed through domain-specific markup languages and without access to the standard DOM. 

Even though the MiniApp Packaging specification recommends that MiniApp agents support standard Web Components, MiniApp vendors might opt to implement the internal components using the traditional MVVM architecture and, subsequently, manage them through non-standard mechanisms like virtual DOM (VDOM) or content interpolation.

## 2. Scope of work

The MiniApp Components specification aims to collect the minimum set of common features from all the MiniApp versions, including: 

- Built-in components (elements), names, and properties
- Event handling and basic event types 
- High-level features for component definition

### Out of scope

- Definition of HTML elements
- Definition of behavior or appearance of elements.
- Definition of a markup language for MiniApp

### What kind of document will be produced?

To avoid overlap and confusion with Web Components and other recommendations in W3C, this specification aims to be an informative reference and is not intended to be a formal standard. Thus, this specification will be published as a Group Note with a formal review but not be endorsed by W3C.

This document will follow the principles below:

- Identify the common practices and existing implementations regarding MiniApp components;
- Maximize reuse and alignment of the specification with the existing standards (especially HTML, CSS, and DOM); and
- Alignment with other groups in W3C (i.e., [OpenUI CG](https://open-ui.org/)) providing feedback and collecting new requirements that could serve to enhance the existing standards.


## 3. Key considerations

### Differences with Web Components

This section analyzes the differences between the standard Web Components and the MiniApp components, considering the existing vendor-specific implementations, Baidu Smart Mini Programs, Alipay Mini Programs, and Quick Apps (Huawei, Xiaomi). 

The main differences identified are:

- __Component resources__. MiniApps require specific resource types, including markup languages and file system structure. 
- __Component interface__. MiniApp components have specific properties and methods. Access to global variables and page elements differs in all versions. 
- __Template definition__. MiniApps have an advanced `{{moustache}}` templating mechanism with data binding and conditional rendering.
- __Event management__. MiniApp event listeners are similar, but developers cannot use the `addEventListener()` method from the logic. Event interfaces are different.
- __Stylesheets__. MiniApps are based on CSS3 profiles, with minor additions. Imports, properties, and rules are similar. 


#### Component resources

Depending on the implementation, MiniApp components are defined using specific file formats and resources to describe templates, logic, and styles.

##### Quick App (Xiaomi, Huawei)

Quick App uses [UX documents](https://doc.quickapp.cn/framework/source-file.html) (`.ux`) to describe and use components. These documents contains three sections, `<template>`, `<script>`, and `<style>`, that include the specific template definition, logic and styling respectively. 

Example:

```xml
<template>
  <div>
    <text class="title" onclick="press">Hello</text>
  </div>
</template>

<script>
  export default {
    press(e) {
      this.title = 'Hello'
    }
  }
</script>

<style>
  .title {
    color: red;
  }
</style>
``` 

##### Alipay Mini Program

Alipay Mini Program components may have four resources in the same directory: `.axml`, `.js`, `.json`, and `.acss`.

`.axml` with a AXML file that includes the template.

```xml
<!-- /components/index/index.axml -->
<view>
  Hi, I'm a component.
</view>
```

`.js` for component registration.

```js
// /components/index/index.js
Component ( {
  mixins :  [ ] ,
  data :  { x : 1 } ,   
  props :  { y : 1 } ,   
  methods :  {  
    handleTap ( )  {} , 
  },
})
```

`.json` to indicate that the current directory files define a component.

```js
// /components/index/index.json
{
  "component" : true 
}
```

`.acss`. ACSS document with the stylesheet.

```css
/** /components/index/index.acss **/
.md-button  {
  padding : 15px ; 
}
```

[Read more](https://opendocs.alipay.com/mini/framework/custom-component-overview).


##### Baidu Smart Mini Program

Baidu Smart Mini Programs enable the creation of components using four resources in the same directory: `.swan`, `.js`, `.json`, and `.css`.

`.swan` with the SWAN file, including the template.

```xml
<!-- /components/custom/custom.swan -->
<view class="name" bindtap="tap">
    {{name}}{{age}}
</view>
```

`.js` for component registration.

```js
// /components/custom/custom.js
Component ({
  properties: { 
    name: {
      type: String,
      value: 'swan',
    }
  },
  data: {
    age: 1
  },
  methods: {
    tap(){}
  }
})
```

`.json` to indicate that the current directory files define a component.

```js
// /components/custom/custom.json
{
  "component" : true 
}
```

`.css`. CSS document with the stylesheet.

```css
/** /components/index/index.css **/
.name {
    color: red;
}
```

[Read more](https://smartprogram.baidu.com/docs/develop/framework/custom-component/).


#### Component markup language

Although the MiniApp components templates are based on HTML, the concrete implementations use their domain-specific markup languages.    

##### Quick App (Xiaomi, Huawei)

Quick Apps use a concrete notation for UX documents. Scripts, stylesheets and templates are defined under the same document, marked with the elements `<script>`, `<style>`, and `<template>`. 

The component [templates are described](https://doc.quickapp.cn/framework/template.html) as an XML fragment within the `<template>` section, using HTML-like elements.

```xml
<template>
  <div>
    <div for="{{list}}" tid="uniqueId">
      <text>{{$idx}}</text>
      <text>{{$item.uniqueId}}</text>
    </div>
  </div>
</template>
```

Quick Apps offer advanced rendering controls (including conditionals, loops, and decorators) and data and event binding. 


##### Alipay Mini Program

Alipay Mini Programs use a concrete AXML notation for the templates described in `.axml` documents. These documents are similar to XML, but without a root node.

The component [templates are described](https://opendocs.alipay.com/mini/framework/axml) using specific elements.

```xml
<!-- axml -->
<template  name="task">
  <view  class="task-item" >
    <text  class= "desc" > {{taskDescription}} </text>
  </view>
</template>
```

Alipay Mini Programs offer advanced rendering controls (including conditionals and loops), and data and event binding. 

##### Baidu Smart Mini Program

Baidu Smart Mini Programs use [SWAN resources](https://smartprogram.baidu.com/docs/develop/framework/dev/). Developers use `.swan` documents to create rendering templates for the pages. 

```xml
<view>
    <custom-component>
        <view>{{name}}</view>
    </custom-component>
</view>
```

Baidu Smart Mini Programs offer advanced rendering controls (including conditionals and loops), as well as data and event binding. 


#### Templating

Web Components are defined in terms of [Custom Elements](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements) and [templating](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_templates_and_slots) with	`<template>` and `<slot>`.	MiniApps have different specifications.
 

##### Quick App (Xiaomi, Huawei)

Definition of `<template>` element in the root of a `.ux` document.

```xml
<!–- file.ux -->
<template>
  <div class="demo-page">
    <text class="title">Hi World</text>
  </div>
</template>
``` 

[More information](https://doc.quickapp.cn/framework/template.html).	

##### Alipay Mini Program

AXML’s `<template>` element in an `.axml` document.

```xml
<!-- header.axml -->
<template name="header">
  <view>
    <text>{{index}}:{{msg}}</text>
  </view>
</template>
```

[More information](https://opendocs.alipay.com/mini/framework/axml-template).	

##### Baidu Smart Mini Program

SWAN document with elements within.

```xml
<view>
    <text class="wrap">hello world</text>
</view>
<text Class="wrap">hello world</text>
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/dev/).


#### Component reuse (instantiation)

How developers reuse the components defined in the [previous section](#templating). 

##### Quick App (Xiaomi, Huawei)

`<import>` element in the root of the `.ux` document.

```xml
<import name="comp" src="./comp"></import>

<template>
  <div>
    <comp></comp>
  </div>
</template>
```

[More information](https://doc.quickapp.cn/framework/template.html).	

##### Alipay Mini Program

AXML’s `<import>` and `<template is=...` elements.

```xml
<import src="./header.axml" />

<template is="header" data="{{...item}}"/>
```

[More information](https://opendocs.alipay.com/mini/framework/axml-template).

##### Baidu Smart Mini Program

Declaration in the configuration (`.json`) document. 

```js
// home.json
{
  "usingComponents": {
     "custom": "/components/custom/custom"
   }
}
```

And declaration in the SWAN document using the ID in the configuration file.

```xml
<!-- home.swan -->
<view>
   <custom name="swanapp"></custom>
</view>
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/dev/).


#### Component properties (definition)

How the properties (attributes) of the components are defined in each MiniApp version. 

##### Quick App (Xiaomi, Huawei)

Components define properties in a `props` array within the object declared in the `<script>` section.     

```html
<!-– comp.ux -->
<script>
  export default {
    props: ['say', 'propObject'],
    onInit() {
      console.info(this.say);    
      console.info(this.propObject)
    }
  }
</script>
```
[More information](https://doc.quickapp.cn/tutorial/framework/parent-child-component-communication.html).

##### Alipay Mini Program

Definition of the component using `Component()` and the properties as pairs in the `props` object.

```js
// /components/index/index.js
Component ({
  props : { 
    name : 'My name'}
});
```
[More information](https://opendocs.alipay.com/mini/framework/component_object).


##### Baidu Smart Mini Program

Definition of the component using `Component()` and the properties in the `properties` object.

```js
// (custom.js)
Component({
  properties: {
    name: {
      type: String,
      value: 'swan',
    }
  }
})
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/custom-component/).


#### Component arguments

How the properties (attributes) are passed to the components when new instances are created. 

##### Quick App (Xiaomi, Huawei)

Use the defined `props` directly as instance attributes.

```xml
<import name="comp" src="./comp"></import>

<template>
  <div>
    <comp 
      say="First Test" 
      prop-object="{{obj}}">
    </comp>
  </div>
</template>
```

[More information](https://doc.quickapp.cn/tutorial/framework/parent-child-component-communication.html).	


##### Alipay Mini Program

Pass the properties as instance attributes.

```xml
<!-- /pages/index/index.axml -->
<comp name='Another name'></comp> 
```

[More information](https://opendocs.alipay.com/mini/framework/component_object).	

##### Baidu Smart Mini Program

Properties as instance attributes

```js
// home.json
{
  "usingComponents": {
     "custom": "/components/custom/custom"
   }
}
```

```xml
// .swan document
<view>
    <custom name="Passing text" >
    </custom>
</view>
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/custom-component/).


#### Data binding

All the MiniApp versions have [`{{moustache}}` notation](https://en.wikipedia.org/wiki/Mustache_%28template_system%29) to bind variables from the logic part of the component.

##### Quick App (Xiaomi, Huawei)

[`{{moustache}}` notation](https://en.wikipedia.org/wiki/Mustache_%28template_system%29) with variables and methods under the `private` or `public` object in the script.

```xml
<template>
  <text>{{message}}</text>
</template>

<script>
  export default {
    private: {
      message: 'Hello'
    }
  }
</script>
```

[More information](https://doc.quickapp.cn/framework/template.html).	


##### Alipay Mini Program

[`{{moustache}}` notation](https://en.wikipedia.org/wiki/Mustache_%28template_system%29) with variables in the AXML file linked to the `Page()` corresponding `data` object variables.

```xml
<view> {{ message }} </view>
```

```js
Page({ 
   data: { 
     message: 'Hello alipay!', 
    }, 
});
```
                                
[More information](https://opendocs.alipay.com/mini/framework/data-binding).

##### Baidu Smart Mini Program

[`{{moustache}}` notation](https://en.wikipedia.org/wiki/Mustache_%28template_system%29) with variables in SWAN template, linked to the `Page()` corresponding `data` object variables.

```xml
<!-- index.swan -->
<view>{{text}}</view>
```

```js
// index.js
Page({
    data: {
        text: 'init data',
    }
});
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/app_service_pagedata/).
	

#### Event binding

All the MiniApp versions have a similar mechanism to add event handlers from the template. MiniApps cannot bind listeners using `addEventListener()` from scripts.

##### Quick App (Xiaomi, Huawei)

`on+eventtype` (or `@+eventtype`) attribute in the template. 

```xml
<text onclick="loadMore"></text>
```

[More information](https://doc.quickapp.cn/tutorial/framework/event-on.html).	

##### Alipay Mini Program

`on+eventtype` attribute in the template.

```xml
<view onTap="loadMore">
  More items…
<view> 
```

[More information](https://opendocs.alipay.com/mini/framework/events).	

##### Baidu Smart Mini Program

`bind:+eventtype` attribute in the template.

```xml
<view bind:tap="loadMore">
   More items…
</view>
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/view_incident/).


#### Event listener definition

In MiniApps, listeners must be defined in specific places in the logic of the component. 

##### Quick App (Xiaomi, Huawei)

`function()` declaration as root of the object in `<script>`.

```html
<script>
  export default {
    loadMore(e) {
      console.log(e);
    }  
  }
</script>
```

[More information](https://doc.quickapp.cn/tutorial/framework/event-on.html).	

##### Alipay Mini Program

`function()` declaration in the root of the `Page({})` declaration in the script.

```js
Page ({
  loadMore(e) {
    console.log(e);
  },
});
```

[More information](https://opendocs.alipay.com/mini/framework/events).	

##### Baidu Smart Mini Program

`function()` declaration in the root of the `Page({})` declaration in the script.

```js
Page({
  loadMore(e) {
    swan.showToast(e.type);
  }
});
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/view_incident/).


#### Event types

Event types by default are different. Not all the standard [event types](https://html.spec.whatwg.org/multipage/indices.html#events-2) are supported. 

Different vendors use different names for the same event type. For example, `tap` event in Alipay and Baidu Mini Programs, but `click` in Quick Apps. 

Also, implementations are different even if vendors use the same name for the same event. For example, the `longtap` event, Alipay Mini Programs trigger the event 500 ms after the first contact, while Baidu Smart Mini Programs' period is 350 ms.

##### Quick App (Xiaomi, Huawei)

[Basic events](https://doc.quickapp.cn/tutorial/framework/event-on.html):

- `touchstart`
- `touchmove`
- `touchend`
- `touchcancel`
- `click`
- `longpress`
- `focus`
- `blur`
- `appear`
- `disappear`
- `swipe`
- `resize`

##### Alipay Mini Program

[Basic events](https://opendocs.alipay.com/mini/framework/events):

- `touchStart`
- `touchMove`
- `touchEnd`
- `touchCancel`
- `tap`
- `longTap`

##### Baidu Smart Mini Program

[Basic events](https://smartprogram.baidu.com/docs/develop/framework/view_incident/):

- `touchstart`
- `touchmove`
- `touchend`
- `touchcancel`
- `tap`


#### Event interface properties

MiniApps have different basic event interfaces. Standard [`Event` interface properties](https://dom.spec.whatwg.org/#interface-event) are not implemented.	

##### Quick App (Xiaomi, Huawei)

[`Event` interface's](https://doc.quickapp.cn/widgets/common-events.html) properties:

- `type`
- `timeStamp`
- `target`
- `currentTarget`

##### Alipay Mini Program

[`BaseEvent` interface's](https://opendocs.alipay.com/mini/framework/event-object) properties:

- `type`
- `timeStamp`
- `target`

##### Baidu Smart Mini Program

Properties of the [Event interface](https://smartprogram.baidu.com/docs/develop/framework/view_incident/).

- `type`
- `timeStamp`
- `target`
- `currentTarget`
- `detail`
- `touches`
- `changedTouches`


#### Stylesheets (CSS Profile)

MiniApp vendors use CSS3 profiles (a subset of the [standard](https://www.w3.org/TR/CSS/)) with minor additions.

##### Quick App (Xiaomi, Huawei)

CSS3 profile, and supports preprocessing (i.e., LESS and SASS).

Only supports a [subset of selectors and properties](https://doc.quickapp.cn/widgets/common-styles.html), and `px`, `dp` (device independent pixels), and `%` as units

Read [the specification](https://doc.quickapp.cn/tutorial/framework/page-style-and-layout.html).

##### Alipay Mini Program

CSS3 profile named [ACSS](https://opendocs.alipay.com/mini/framework/acss), compatible with CSS3.

ACSS adds `rpx` (responsive pixel), and a specific `page` selector.

##### Baidu Smart Mini Program

Specific CSS3 profile. 

It adds `rpx` (responsive pixel).

See [the specification](https://smartprogram.baidu.com/docs/develop/framework/view_css/).


#### Stylesheets (inline declaration)

The different MiniApp versions use the same `style` attribute to declare inline styles.  

##### Quick App (Xiaomi, Huawei)

`style` attribute in the template elements.	

```xml
<template> 
   <div style="flex-direction: column;"></div>
</template>	
```

##### Alipay Mini Program

`style` attribute in the template elements.

```xml
<view style="color:#ffffff“ />		
```

##### Baidu Smart Mini Program

`style` attribute in the SWAN template elements.	

```xml
<view style="color: #ffffff"> swan </view>
```

#### Web Components

`style` attribute in the elements.	


#### Stylesheets (import)

The different MiniApp versions use similar [`@import`](https://developer.mozilla.org/en-US/docs/Web/CSS/@import) at-rule mechanisms.  

##### Quick App (Xiaomi, Huawei)

`@import` at-rule within the `<style>` section.

```html
<style>
  @import './style.css';
</style>	
```

##### Alipay Mini Program

`@import` at-rule within the `.acss` document.

```css
@import "./button.acss" ; 
@import "/common/button.acss" ;
```

##### Baidu Smart Mini Program

`@import` at-rule within the `.css` document.

```css
@import "header.css";
```
	
#### Component interface (properties)

All the MiniApp versions have different component interfaces (they don't use [`HTMLElement` interface](https://html.spec.whatwg.org/multipage/dom.html#htmlelement)).  

##### Quick App (Xiaomi, Huawei)

[Predefined components' properties](https://doc.quickapp.cn/framework/script.html):

- `data`
- `props`
- `computed`
- `externalClasses`
- `$app`
- `$page`

##### Alipay Mini Program

[Predefined components' properties](https://opendocs.alipay.com/mini/framework/component_object): 

- `data`
- `props`
- `is`
- `$id`
- `router`
- `pageRouter`
- `$page`

##### Baidu Smart Mini Program

[Predefined components' properties](https://smartprogram.baidu.com/docs/develop/framework/custom-component_comp/):

- `is`
- `id`
- `dataset`
- `data`
- `properties`

#### Component interface (methods)

All the MiniApp versions have different non-standard component interfaces (they don't use [`HTMLElement` interface](https://html.spec.whatwg.org/multipage/dom.html#htmlelement)).  

##### Quick App (Xiaomi, Huawei)

Predefined [component's methods](https://doc.quickapp.cn/framework/script.html):

- `$valid()`
- `$visible()`
- `$attrs()`
- `$listeners()`
- `$element()`
- `$root()`
- `$parent()`
- `$child()`
- `$nextTick()`
- `$forceUpdate()`


##### Alipay Mini Program

Predefined [component's methods](https://opendocs.alipay.com/mini/framework/component_object):

- `setData()`
- `$spliceData()`
- `createSelectorQuery()`
- `createIntersectionObserver()`
- `selectOwnerComponent()`
- `selectComponsedParentComponent()`

##### Baidu Smart Mini Program

Predefined [component's methods](https://doc.quickapp.cn/framework/script.html):

- `setData()`
- `hasBehavior` 
- `createSelectorQuery()`
- `createIntersectionObserver()`
- `triggerEvent()`
- `selectComponent()`
- `selectAllComponents()`
- `groupSetData()`

### Essential MiniApp elements

MiniApp elements are the building blocks for describing the structure and content of MiniApp Components. This section will analyze the differences between the built-in components or elements in each MiniApp version and the standard HTML. 

The table below includes an analysis of the MiniApp elements available in the existing MiniApp specifications. Each row represents an element and the semantically equivalent(s) from each specification without considering the details in terms of attributes or behavior.


| Feature        | W3C Spec                                                        | [QuickApp (Xiaomi, Huawei)](https://www.quickapp.cn/) | [Alipay Mini Program](https://docs.alipay.com/mini/developer/) | [Baidu Smart Mini Program](https://smartprogram.baidu.com/developer/index.html) |
| -------------- | --------------------------------------------------------------- | ----------------------- | ---------------- | ---------------------- |
| div            | `<div>`                                                         | `<div>`                   | `<view>`           | `<view>`                 |
| span           | `<span>`                                                        | `<span>`                  |                  |                        |
| stack          |                                                                 | `<stack>`                 | `<cover-view>`     | `<cover-view>`           |
| carousel       |                                                                 | `<swiper>`                | `<swiper>`         | `<swiper>`               |
| tabs           | [OpenUI research](https://open-ui.org/components/tabs.research) | `<tabs>`                  |                  | `<tabs>`                 |
| refresh        |                                                                 | `<refresh>`               |                  |                        |
| icon           | [OpenUI research](https://open-ui.org/components/icon.research) |                         | `<icon>`           | `<icon>`                 |
| progress       | `<progress>`                                                    | `<progress>`              | `<progress>`       | `<progress>`             |
| anchor         | a                                                               | `<a>`                       | `<navigator>`      | `<navigator>`            |
| text           | `<span>`                                                        | `<text>`                  | `<text>`           | `<text>`                 |
| text input     | `<input>`                                                       | `<input>`                 | `<input>`          | `<input>`                |
| camera         | `<input>`                                                       | `<camera>`                |                  | `<camera>`               |
| textarea       | `<textarea>`                                                    | `<textarea>`              | `<textarea>`       | `<textarea>`             |
| checkbox       | `<input type="checkbox">`                                       | `<input type="checkbox">` | `<checkbox>`       | `<checkbox>`             |
| radio          | `<input type="radio">`                                          | `<input type="radio">`    | `<radio>`          | `<radio>`                |
| form           | `<form>`                                                        |                         | `<form>`           | `<form>`                 |
| button         | `<button>`                                                      | `<input type="button">`   | `<button>`         | `<button>`               |
| label          | `<label>`                                                         | `<label>`                 | `<label>`          | `<label>`                |
| select         | [`<select>`](https://open-ui.org/components/select)               | `<select>`                | `<picker>`         | `<picker>`               |
| slider         | `<input>`                                                         | `<slider>`                | `<slider>`         | `<slider>`               |
| switch         | [OpenUI research](https://open-ui.org/components/switch)        | `<switch>`                | `<switch>`         | `<switch>`               |
| picker         | [OpenUI proposal](https://open-ui.org/components/select)        | `<picker>`                | `<picker>`         | `<picker>`               |
| image          | `<img>`                                                           | `<image>`                 | `<image>`          | `<image>`                |
| audio          | `<audio>`                                                         |                         |                  | `<audio>`                |
| video          | `<video>`                                                         | `<video>`                 | `<video>`          | `<video>`                |
| canvas         | `<canvas>`                                                        | `<canvas>`                | `<canvas>`         | `<canvas>`               |
| animation      |                                                                 | `<lottie>`                | `<lottie>`         | `<animation-video>`      |
| web-view       | `<html>`                                                          | `<web>`                   | `<web-view>`       | `<web-view>`             |
| map            |                                                                 | `<map>`                   | `<map>`            | `<map>`                  |
| list           |                                                                 | `<list>`                  |                  |                        |
| popup          | `<dialog>`                                                        | `<popup>`                 |                  |                        |
| rtc-room       |                                                                 |                         |                  | `<rtc-room>`             |
| ad             |                                                                 |                         |                  | `<ad>`                   |
| payment        |                                                                 |                         |                  | `<inline-payment-panel>` |
| comments       |                                                                 |                         |                  | `<comment-list>`         |
| like           |                                                                 |                         |                  | `<like>`                 |
| 3d-model       | `<model>` (WIP)                                                   |                         |                  | `<modelviewer>`          |
| rating         |                                                                 | `<rating>`                |                  |                        |
| marquee        |                                                                 | `<marquee>`               |                  |                        |
| share-button   |                                                                 | `<share-button>`          |                  |                        |
| drawer         |                                                                 | `<drawer>`                |                  |                        |
| match-media    |                                                                 |                         | `<match-media>`    |                        |
| aria-component |                                                                 |                         | `<aria-component>` |                        |
| page metadata  |                                                                 |                         | `<page-meta>`      |                        |

