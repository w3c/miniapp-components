# MiniApp Components Explainer 

## Authors

- Zitao Wang (Huawei)
- Martin Alvarez (Huawei)

## 1. Introduction

### What is this?

MiniApp Components are the building blocks to creating MiniApp pages. Each component encapsulates functionality, data, and styles, enabling developers to create custom and reusable items that can be combined to develop MiniApps. MiniApps include essential components like page containers, textual and multimedia content, and other interactive elements such as forms.

This document aims to specify a set of common practices to define MiniApps Components that allow developers to build similar user interfaces across MiniApp platforms efficiently.

### Why should we care?

Although MiniApps Components share the same concept as Web Components, their capabilities and development features differ. The main differences are motivated by the architecture of the existing implementations along the MiniApp ecosystem following the MVVM pattern, based on components developed through domain-specific markup languages and without access to the standard DOM. 

Even though [[[MINIAPP-PACKAGING]]] recommends MiniApp agents to support standard Web Components, MiniApp vendors might opt to implement the internal components using the traditional MVVM architecture and, subsequently, manage them through non-standard mechanisms like virtual DOM (VDOM) or content interpolation.


## 2. Differences with Web Components

This section analyzes the differences between the standard Web Components and the MiniApp components, considering the existing vendor-specific implementations, Baidu Smart Mini Programs, Alipay Mini Programs, and Quick Apps (Huawei, Xiaomi). 

The main differences identified are:

- __Component resources__. MiniApps require specific resource types, including markup languages, and file system structure. 
- __Component interface__. MiniApp components have specific properties and methods. Access to global variables and page elements differs in all versions. 
- __Template definition__. MiniApps have advanced `{{moustache}}` templating mechanism with data binding and conditional rendering.
- __Event management__. MiniApp event listeners are similar, but developers cannot use the `addEventListener()` method from the logic. Event interfaces are different.
- __Stylesheets__. MiniApps are based on CSS3 profiles, with minor additions. Imports, properties and rules are similar. 


### Component resources

Depending on the implementation, MiniApp components are defined using specific file formats and resources to describe templates, logic and styles.

#### Quick App (Xiaomi, Huawei)

Quick App uses [UX documents](https://doc.quickapp.cn/framework/source-file.html) (`.ux`) to describe and use components. These documents contains three sections, `<template>`, `<script>`, and `<style>`, that include the specific template definition, logic and styling respectively. 

Example:

``` xml
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

#### Alipay Mini Program

Alipay Mini Program components may have four resources in the same directory: `.axml`, `.js`, `.json`, and `.acss`.

`.axml`. AXML file including the template.

``` xml
<!-- /components/index/index.axml -->
<view>
  Hi, I'm a component.
</view>
```

`.js` for component registration.

``` js
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

`.json` to indicate that the current directory files defines a component.

``` json
// /components/index/index.json
{
  "component" : true 
}
```

`.acss`. ACSS document with the stylesheet.

``` css
/** /components/index/index.acss **/
.md-button  {
  padding : 15px ; 
}
```

[Read more](https://opendocs.alipay.com/mini/framework/custom-component-overview).


#### Baidu Smart Mini Program

Baidu Smart Mini Programs enable the creation of components using four resources in the same directory: `.swan`, `.js`, `.json`, and `.css`.

`.swan`. SWAN file including the template.

``` xml
<!-- /components/custom/custom.swan -->
<view class="name" bindtap="tap">
    {{name}}{{age}}
</view>
```

`.js` for component registration.

``` js
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

`.json` to indicate that the current directory files defines a component.

``` json
// /components/custom/custom.json
{
  "component" : true 
}
```

`.css`. CSS document with the stylesheet.

``` css
/** /components/index/index.css **/
.name {
    color: red;
}
```

[Read more](https://smartprogram.baidu.com/docs/develop/framework/custom-component/).


### Component markup language

Although the MiniApp components templates are based on HTML, the concrete implementations use their domain-specific markup languages.    

#### Quick App (Xiaomi, Huawei)

Quick Apps use a concrete notation for UX documents. Scripts, stylesheets and templates are defined under the same document, marked with the elements `<script>`, `<style>`, and `<template>`. 

The component [templates are described](https://doc.quickapp.cn/framework/template.html) as an XML fragment within the `<template>` section, using HTML-like elements.

``` xml
<template>
  <div>
    <div for="{{list}}" tid="uniqueId">
      <text>{{$idx}}</text>
      <text>{{$item.uniqueId}}</text>
    </div>
  </div>
</template>
```

Quick Apps offer advanced rendering controls (including conditionals, loops and decorators), as well as data and event binding. 


#### Alipay Mini Program

Alipay Mini Programs use a concrete AXML notation for the templates described in `.axml` documents. These documents are similar to XML, but without a root node.

The component [templates are described](https://opendocs.alipay.com/mini/framework/axml) using specific elements.

``` xml
<!-- axml -->
<template  name="task">
  <view  class="task-item" >
    <text  class= "desc" > {{taskDescription}} </text>
  </view>
</template>
```

Alipay Mini Programs offer advanced rendering controls (including conditionals and loops), as well as data and event binding. 

#### Baidu Smart Mini Program

Baidu Smart Mini Programs use [SWAN resources](https://smartprogram.baidu.com/docs/develop/framework/dev/). Developers use `.swan` documents to create rendering templates for the pages. 

``` xml
<view>
    <custom-component>
        <view>{{name}}</view>
    </custom-component>
</view>
```

Baidu Smart Mini Programs offer advanced rendering controls (including conditionals and loops), as well as data and event binding. 


### Templating

Web Components are defined in terms of [Custom Elements](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements) and [templating](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_templates_and_slots) with	`<template>`, and `<slot>`.	MiniApps have different specifications.
 

#### Quick App (Xiaomi, Huawei)

Definition of `<template>` element in the root of a `.ux` document.

``` xml
<!–- file.ux -->
<template>
  <div class="demo-page">
    <text class="title">Hi World</text>
  </div>
</template>
``` 

[More information](https://doc.quickapp.cn/framework/template.html).	

#### Alipay Mini Program

AXML’s `<template>` element in an `.axml` document.

``` xml
<!-- header.axml -->
<template name="header">
  <view>
    <text>{{index}}:{{msg}}</text>
  </view>
</template>
```

[More information](https://opendocs.alipay.com/mini/framework/axml-template).	

#### Baidu Smart Mini Program

SWAN document with elements within.

``` xml
<view>
    <text class="wrap">hello world</text>
</view>
<text Class="wrap">hello world</text>
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/dev/).


### Component re-use (instantiation)

How developers reuse the components defined in the [previous section](#templating). 

#### Quick App (Xiaomi, Huawei)

`<import>` element in the root of the `.ux` document.

``` xml
<import name="comp" src="./comp"></import>

<template>
  <div>
    <comp></comp>
  </div>
</template>
```

[More information](https://doc.quickapp.cn/framework/template.html).	

#### Alipay Mini Program

AXML’s `<import>` and `<template is=...` elements.

``` xml
<import src="./header.axml" />

<template is="header" data="{{...item}}"/>
```

[More information](https://opendocs.alipay.com/mini/framework/axml-template).

#### Baidu Smart Mini Program

Declaration in the configuration (`.json`) document. 

``` json
// home.json
{
  "usingComponents": {
     "custom": "/components/custom/custom"
   }
}
```

And declaration in the SWAN document using the ID in the configuration file.

``` xml
<!-- home.swan -->
<view>
   <custom name="swanapp"></custom>
</view>
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/dev/).


### Component properties (definition)

How the properties (attributes) of the components are defined in each MiniApp version. 

#### Quick App (Xiaomi, Huawei)

Components define properties in a `props` array within the object declared in the `<script>` section.     

``` html
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

#### Alipay Mini Program

Definition of the component using `Component()` and the properties as pairs in the `props` object.

``` js
// /components/index/index.js
Component ({
  props : { 
    name : 'My name'}
});
```
[More information](https://opendocs.alipay.com/mini/framework/component_object).


#### Baidu Smart Mini Program

Definition of the component using `Component()` and the properties in the `properties` object.

``` js
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


### Component arguments

How the properties (attributes) are passed to the components when new instances are created. 

#### Quick App (Xiaomi, Huawei)

Use the defined `props` directly as instance's attributes.

``` xml
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


#### Alipay Mini Program

Pass the properties as as instance's attributes.

``` xml
<!-- /pages/index/index.axml -->
<comp name='Another name'></comp> 
```

[More information](https://opendocs.alipay.com/mini/framework/component_object).	

#### Baidu Smart Mini Program

Properties as instance's attributes

``` json
// home.json
{
  "usingComponents": {
     "custom": "/components/custom/custom"
   }
}
```

``` xml
// .swan document
<view>
    <custom name="Passing text" >
    </custom>
</view>
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/custom-component/).


### Data binding

All the MiniApp version have [`{{moustache}}` notation](https://en.wikipedia.org/wiki/Mustache_%28template_system%29) to bind variables from the logic part of the component.

#### Quick App (Xiaomi, Huawei)

[`{{moustache}}` notation](https://en.wikipedia.org/wiki/Mustache_%28template_system%29) with variables and methods under the `private` or `public` object in the script.

``` xml
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


#### Alipay Mini Program

[`{{moustache}}` notation](https://en.wikipedia.org/wiki/Mustache_%28template_system%29) with variables in the AXML file linked to the `Page()` corresponding `data` object variables.

``` xml
<view> {{ message }} </view>
```

``` js
Page({ 
   data: { 
     message: 'Hello alipay!', 
    }, 
});
```
                                
[More information](https://opendocs.alipay.com/mini/framework/data-binding).

#### Baidu Smart Mini Program

[`{{moustache}}` notation](https://en.wikipedia.org/wiki/Mustache_%28template_system%29) with variables in SWAN template, linked to the `Page()` corresponding `data` object variables.

``` xml
<!-- index.swan -->
<view>{{text}}</view>
```

``` js
// index.js
Page({
    data: {
        text: 'init data',
    }
});
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/app_service_pagedata/).
	

### Event binding

All the MiniApp version have similar mechanism to add event handlers from the template. MiniApps cannot bind listeners using `addEventListener()` from scripts.

#### Quick App (Xiaomi, Huawei)

`on+eventtype` (or `@+eventtype`) attribute in the template. 

``` xml
<text onclick="loadMore"></text>
```

[More information](https://doc.quickapp.cn/tutorial/framework/event-on.html).	

#### Alipay Mini Program

`on+eventtype` attribute in the template.

``` xml
<view onTap="loadMore">
  More items…
<view> 
```

[More information](https://opendocs.alipay.com/mini/framework/events).	

#### Baidu Smart Mini Program

`bind:+eventtype` attribute in the template.

``` xml
<view bind:tap="loadMore">
   More items…
</view>
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/view_incident/).


### Event listener definition

In MiniApps, listeners must be defined in specific places in the logic of the component. 

#### Quick App (Xiaomi, Huawei)

`function()` declaration as root of the object in `<script>`.

``` html
<script>
  export default {
    loadMore(e) {
      console.log(e);
    }  
  }
</script>
```

[More information](https://doc.quickapp.cn/tutorial/framework/event-on.html).	

#### Alipay Mini Program

`function()` declaration in the root of the `Page({})` declaration in the script.

``` js
Page ({
  loadMore(e) {
    console.log(e);
  },
});
```

[More information](https://opendocs.alipay.com/mini/framework/events).	

#### Baidu Smart Mini Program

`function()` declaration in the root of the `Page({})` declaration in the script.

``` js
Page({
  loadMore(e) {
    swan.showToast(e.type);
  }
});
```

[More information](https://smartprogram.baidu.com/docs/develop/framework/view_incident/).


### Event types

Event types by default are different. Not all the standard [event types](https://html.spec.whatwg.org/multipage/indices.html#events-2) are supported.	

#### Quick App (Xiaomi, Huawei)

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

#### Alipay Mini Program

[Basic events](https://opendocs.alipay.com/mini/framework/events):

- `touchStart`
- `touchMove`
- `touchEnd`
- `touchCancel`
- `tap`
- `longTap`

#### Baidu Smart Mini Program

[Basic events](https://smartprogram.baidu.com/docs/develop/framework/view_incident/):

- `touchstart`
- `touchmove`
- `touchend`
- `touchcancel`
- `tap`


### Event interface properties

MiniApps have different basic event interfaces. Standard [`Event` interface properties](https://dom.spec.whatwg.org/#interface-event) are not implemented.	

#### Quick App (Xiaomi, Huawei)

[`Event` interface's](https://doc.quickapp.cn/widgets/common-events.html) properties:

- `type`
- `timeStamp`
- `target`
- `currentTarget`

#### Alipay Mini Program

[`BaseEvent` interface's](https://opendocs.alipay.com/mini/framework/event-object) properties:

- `type`
- `timeStamp`
- `target`

#### Baidu Smart Mini Program

Properties of the [Event interface](https://smartprogram.baidu.com/docs/develop/framework/view_incident/).

- `type`
- `timeStamp`
- `target`
- `currentTarget`
- `detail`
- `touches`
- `changedTouches`


### Stylesheets (CSS Profile)

MiniApp vendors use CSS3 profiles (a subset of the [standard](https://www.w3.org/TR/CSS/)) with minor additions.

#### Quick App (Xiaomi, Huawei)

CSS3 profile, and supports preprocessing (i.e., LESS and SASS).

Only supports a [subset of selectors and properties](https://doc.quickapp.cn/widgets/common-styles.html), and `px`, `dp` (device independent pixels), and `%` as units

Read [the specification](https://doc.quickapp.cn/tutorial/framework/page-style-and-layout.html).

#### Alipay Mini Program

CSS3 profile named [ACSS](https://opendocs.alipay.com/mini/framework/acss), compatible with CSS3.

ACSS adds `rpx` (responsive pixel), and a specific `page` selector.

#### Baidu Smart Mini Program

Specific CSS3 profile. 

It adds `rpx` (responsive pixel).

See [the specification](https://smartprogram.baidu.com/docs/develop/framework/view_css/).


### Stylesheets (inline declaration)

#### Quick App (Xiaomi, Huawei)

`style` attribute in the template elements.	

``` xml
<template> 
   <div style="flex-direction: column;"></div>
</template>	
```

#### Alipay Mini Program

`style` attribute in the template elements.

``` xml
<view style="color:#ffffff“ />		
```

#### Baidu Smart Mini Program

`style` attribute in the SWAN template elements.	

``` xml
<view style="color: #ffffff"> swan </view>
```

#### Web Components

`style` attribute in the elements.	


### Stylesheets (import)

The different MiniApp versions use similar [`@import`](https://developer.mozilla.org/en-US/docs/Web/CSS/@import) at-rule mechanisms.  

#### Quick App (Xiaomi, Huawei)

`@import` at-rule within the `<style>` section.

``` html
<style>
  @import './style.css';
</style>	
```

#### Alipay Mini Program

`@import` at-rule within the `.acss` document.

``` css
@import "./button.acss" ; 
@import "/common/button.acss" ;
```

#### Baidu Smart Mini Program

`@import` at-rule within the `.css` document.

``` css
@import "header.css";
```
	
### Component interface (properties)

All the MiniApp versions have different component interfaces (they don't use [`HTMLElement` interface](https://html.spec.whatwg.org/multipage/dom.html#htmlelement)).  

#### Quick App (Xiaomi, Huawei)

[Predefined components' properties](https://doc.quickapp.cn/framework/script.html):

- `data`
- `props`
- `computed`
- `externalClasses`
- `$app`
- `$page`

#### Alipay Mini Program

[Predefined components' properties](https://opendocs.alipay.com/mini/framework/component_object): 

- `data`
- `props`
- `is`
- `$id`
- `router`
- `pageRouter`
- `$page`

#### Baidu Smart Mini Program

[Predefined components' properties](https://smartprogram.baidu.com/docs/develop/framework/custom-component_comp/):

- `is`
- `id`
- `dataset`
- `data`
- `properties`

### Component interface (methods)

All the MiniApp versions have different non-standard component interfaces (they don't use [`HTMLElement` interface](https://html.spec.whatwg.org/multipage/dom.html#htmlelement)).  

#### Quick App (Xiaomi, Huawei)

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


#### Alipay Mini Program

Predefined [component's methods](https://opendocs.alipay.com/mini/framework/component_object):

- `setData()`
- `$spliceData()`
- `createSelectorQuery()`
- `createIntersectionObserver()`
- `selectOwnerComponent()`
- `selectComponsedParentComponent()`

#### Baidu Smart Mini Program

Predefined [component's methods](https://doc.quickapp.cn/framework/script.html):

- `setData()`
- `hasBehavior` 
- `createSelectorQuery()`
- `createIntersectionObserver()`
- `triggerEvent()`
- `selectComponent()`
- `selectAllComponents()`
- `groupSetData()`




Even for similar UI components, there are some gaps for different vendor's events handling. First, different vendors use different names for the same event. For example, for the “tap” event, Alipay and Baidu named “tap” while Huawei named “click”. Second, even if different vendors have the same name for the same event, different deployments may still exist. For example, for the “longtap” event, Alipay describes it as touch and leave after more than 500 ms. Baidu describes as more than 350ms.

This may lead to repeated learning and repeated development by developers. Therefore, we propose to define a standard set of UI common components for MiniApp. That allows codes to easily migrate to different platforms, reduce repetitive development, and provide the same user experience.

## 2. MiniApp Common UI Components
Given the above problems, we select UI components common to existing widely deployed applets and standardize them. The common UI components may include as following.
* **Basic Components**:
Basic components provide the minimum interactive blocks that can be reused for the MiniApp. Developers can define the user interface of the MiniApp by combining these basic components. It may include the following components such as 'Image', 'Progress', 'Text', 'Input', 'Button', 'Label', 'Select', 'Slider', 'Switch', 'Picker', 'Video', and 'Canvas'.
* **Container Components**:
Container components provide the structure of a MiniApp page. It may inculdes the following components such as 'Div', 'List', 'Swiper', 'Tabs', and 'Refresh'.
### Scope of work:
The MiniApp Common UI Components specification aims to standardize on:
- Component names and properties
- States
- Behaviors
- How behaviors transition state 
### Out of Scope:
- Appearance of the component
- Markup Language for MiniApp 

### How to standardize the common UI components
Standardized MiniApp UI proposals will be based on the following principles:
- Identify the scope of the common UI based on the existing implementation;
- Reuse the existing standards as much as possible and extend them to support the attributes and events required by the MiniApp;
- Alignment with standards bodies like OpenUI CG to define new elements (e.g., picker, tab).

### Key Considerations 

#### How to implementate the standard MiniApp common UI components?


## 3. Comparison with existing standard UI components 

The following table mainly describes the comparison between the MiniApp common UI components and W3C standards compontents:
MiniApp Common UI Components | Attributes | Events | Similar Standard Component 
:---    |:---    |:--        |:---     
div | - | - | Constraint of standard attributes and different events
list | - | scrollend | Element event scroll as the standard
list-item | - | - | - |
swiper | index, loop, vertical | change | - |
tabs | index, vertical, disabled, focusable, data | - | tabs for HTML (OpenUI) |
tab-bar | mode | - | - |
tab-content | scrollable | - | CSS overflow: scroll |
refresh | offset, type, refreshing, lasttime, friction, disabled, focusable, data | - | Similar to SwipeRefreshLayout, but more related to the user agent instead of the document. |
image | src, alt, disabled, focusable & complete, error | - | &lt;img&gt; with attributes src and alt are the standard |
progress | type, focusable, data | - | &lt;progress&gt; element (max, value, position, labels) |
text | focusable, data | - | Similar to SVG’s text. |
input | type, placeholder…, headericon, disable, focusable | change | input element (with all types supported), attribute disabled, no headericon. |
button | type (styles instead of function), value, icon, waiting, focusable* | - | button element, attribute disabled, no waiting, no icon. (in OpenUI) |
label | focusable | - | label element. Labelable elements: button, input, meter, output, progress, select, textarea |
select | data | - | select element. Attribute disabled (in OpenUI) |
slider | min, max, value, data | change | input@type=”range” (in OpenUI) |
switch | - | - | - |
picker | type (text, date, time, datetime, multi-text) | - | input element (date, time, datetime-local) and datalist element (with attribute options). |
video | muted, src, autoplay, poster, controls | prepared, seeked, timeupdate, fullscreenchange | video element with all the attributes but (disable, and focusable) + vents: readyState, buffered  (but not prepared, seeked, timeupdate, fullscreenchange) |
canvas | disable, focusable, data | - | canvas element |
























