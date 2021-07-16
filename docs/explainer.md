# MiniApp UI Components Explainer 
## Authors
Zitao Wang (Huawei)
## 1. Introduction

### What is this?
MiniApps are made of high-level building blocks called UI Components, which allow developers to quickly construct the UI for a MiniApp.
### Why should we care?
For MiniApp, there are some pre-standard implementations and wildly used. But these implementations may follow different vendor-specific development guidelines for developing MiniApp UI components. And some of them are defining their own markup languages (WXML, SWAN, AXML), specific event handling, data-binding and rending methods. For example:

- Wechat WXML:
```html
  <!--wxml-->
    <view class="page-section page-section-spacing swiper">
      <swiper indicator-dots="{{indicatorDots}}"
        autoplay="{{autoplay}}" interval="{{interval}}" duration="{{duration}}">
        <block wx:for="{{background}}" wx:key="*this">
          <swiper-item>
            <view class="swiper-item {{item}}"></view>
          </swiper-item>
        </block>
      </swiper>
    </view>
```
- Baidu SWAN:
```html
<!-- template-demo.swan-->
<view class="wrap">
    <view class="card-area">
        <swiper 
            class="swiper"
            indicator-dots="{{switchIndicateStatus}}" 
            indicator-color="rgba(0,0,0,0.30)"
            indicator-active-color="#fff">
            <swiper-item 
                s-for="item in swiperList"
                item-id="{{itemId}}"
                class="{{item.className}}">
                <view class="swiper-item">{{item.value}}</view>
            </swiper-item>
        </swiper>
  </view>
</view>     
```
- Alipay AXML:
```.html
<!-- pages/index/index.axml -->
 <view class="page-section-demo">
  <swiper
    style="height:150px"
    class="demo-swiper">
    <swiper-item key="swiper-item-{{index}}" a:for="{{background}}">
     <view class="swiper-item bc_{{item.color}}">{{item.text}}</view>
    </swiper-item>
  </swiper>
 </view>
```
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
























