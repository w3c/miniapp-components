# MiniApp Element Gap Analysis 

## Scope of the analysis

As we [proposed at TPAC 2024](https://www.w3.org/2024/09/26-miniapp-minutes.html#x388), we have analyzed and collected insights about the requirements for the essential structural MiniApp elements (i.e., the HTML-like elements used in the MiniApp components). 

The main objective of the analysis is to collect insights on the common requirements for MiniApps, and to understand the feasibility of reusing the wide-spread standard HTML elements to solve the needs of these MiniApps.     

For the analysis, we have grouped the similar elements of four reference MiniApp platforms - [QuickApps](https://www.quickapp.cn/), [Alipay Mini Programs](https://docs.alipay.com/mini/developer/), [Baidu Smart Mini Programs](https://smartprogram.baidu.com/developer/index.html), and [WeChat Mini Programs](https://developers.weixin.qq.com/miniprogram/dev/framework/)) - and the equivalent [HTML elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element). The analysis includes annotations on the type of the component (i.e., input, container, etc.) and the intended purpose beyond the semantics (i.e., is it used only for layout?, it for additional functionality?).      

EDITOR NOTE: The study is __still in progress__ (please file a issue to fix anything that is wrong), and it might have missed important details. It was totally based on public developer information (most of the documentation is in Chinese).


### Summary of common MiniApps elements and standard equivalent 

Notes: 
- The second column (2+ implementations) indicates if the feature was found in two or more implementations.
- Columns 4 and 5 indicate if the element is defined beyond structure and semantics. Column four showing if it is only for styling (e.g.,to facilitate layout) and column five just to add additional functionality. 
- The last column (Standard solution) shows a potential way to implement the feature by reusing existing standards. 

| Type | 2+ impl? | Feature | Style? | Funct.? | W3C Rec. | Standard solution |
| ---- | -------- | ------- | ------ | ------- | -------- | ----------------- |
| Container | yes | Content Division Element | | | `<div>` | direct usage |
|  | yes | Content Span (Inline container) | | | `<span>` | direct usage |
|  |  | Dialog | | | `<dialog>` | direct usage |
|  | yes | Stacking container | yes | | `<div>`[*](#block-element) | HTML + CSS (`div { position: relative; }`) |
|  | yes | Slideshow (carousel) | yes | | `<div>`[*](#block-element) | HTML + CSS Flexbox + `overscroll-behavior` + `scroll-behavior`... |
|  | yes | Tabs | yes | | `<nav> <section>`[*](#block-element) | (OpenUI) (`nav`s + `section` + CSS) |
|  | yes | List container | yes | | `<ul><li>` | HTML + CSS |
|  | yes | Fixed container | yes | | `<div>`[*](#block-element) | HTML + CSS |
|  | yes | Scrolling container | yes | | `<div>`[*](#block-element) | HTML + CSS |
|  | | Grid layout | yes | | `<div>`[*](#block-element) | HTML + CSS |
|  | | Nested scroll layout | yes | | `<div>`[*](#block-element) | HTML + CSS |
|  | | Marquee | yes | | `<marquee>` (deprecated)[*](#block-element) | HTML + CSS |
|  | yes | Drag and drop container | | yes | `<div>`[*](#block-element) | HTML + _Drag and Drop API_ |
|  | | Pull to refresh | | yes | `<div>`[*](#block-element) | HTML + JS + CSS |
|  | yes | Conditional block (media query) | | | `@style` | CSS media queries |
|  | | Navigation Bar | | | `<nav>` | HTML + CSS |
| Content | yes | Image | | | `<img>`, `<picture>` | direct usage |
|  | yes | Icon | yes | | `<img>`, `<span>` | (OpenUI) HTML + CSS |
|  | yes | Progress indicator | | | `<progress>` | HTML + CSS |
|  | yes | Anchor | | | `<a>` | direct usage |
|  | yes | Text  (no semantics) | | | `<span>` | direct usage |
|  | yes | Web-view (external URL) | | | `<iframe>` | direct usage |
|  | yes | HTML-rich content | | | [standard elements](#safe-html) | subset of HTML elements | 
|  | yes | Map | | | | (need additional services) |
|  | yes | Advertisement | | | | (need additional services) |
|  | | 3D-model | | | `<model>` (WIP) | direct usage |
|  | | Comment list | | | `<ul>``<q>` | (need additional services) |
| Forms | yes | Textual input | | | `<input>` | direct usage (limiting types) |
|  | yes | Image capture input | | | `<input type="file" accept="image/\*" capture...` | direct usage |
|  | yes | Multiple-line input | | | `<textarea>` | direct usage |
|  | yes | Checkbox | | | `<input type="checkbox">` | direct usage |
|  | yes | Radio button | | | `<input type="radio">` | direct usage |
|  | yes | Form | | | `<form>` | direct usage |
|  | yes | Button | | | `<button>` | direct usage |
|  | yes | Label | | | `<label>` | direct usage |
|  | yes | Select list | | | `<select>`, `<optgroup>`, `<option>` | direct usage + CSS |
|  | yes | Slider | | | `<input type="range">` | direct usage |
|  | yes | Picker (scroll selector) | | | `<select>`, `<option>` | direct usage + CSS |
|  | yes | Switch button | yes | | `<input type="checkbox">` | HTML + CSS |
|  | | Sharing button | | yes | `<button>` | _Web Share API_ |
|  | | Like button | yes | yes | `<button>` | (need additional services) |
|  | | Specific action button | yes | yes | `<button>` | (need additional services) |
|  | | Rating panel | yes | yes | `<radio>` | HTML + CSS |
|  | | Rich text editor | | yes | | (need additional services) |
|  | | Selection of text | | yes | | _Selection API_ |
|  | | Keyboard overlay (input) | | yes | | _VirtualKeyboard API_ |
|  | | Payment panel | | yes | | (need additional services) |
| Media | yes | Audio content | | | `<audio>` | direct usage |
|  | yes | Video content | | | `<video>` | direct usage |
|  | | AR Camera | | | | _WebXR Device API_ |
|  | yes | Canvas | | | `<canvas>` | direct usage |
|  | | Video/audio conference | | | | (need additional services) |
| Animations | yes | Lottie animation | yes | | | _Web Animations API_ |
|  | | Video animation | yes | | `<video>` | direct usage |
|  | | Transition of pages | yes | | | _View Transitions API_ |
|  | | Transition of element between pages | yes | | | _View Transitions API_ |
| Metadata | yes | Page metadata | | | `<meta>` | direct usage |

<a name='block-element'>*</a> `div` or any other semantic block element.

### <a name='safe-html'>Safe MiniApp HTML Elements</a>

MiniApps usually support raw HTML within a specific container (see [HTML-rich content](#html-rich-content)). 
The following table includes the HTML elements commonly accepted by the MiniApp platforms analyzed.

| HTML element | Baidu | Alipay | WeChat | In gap analysis? |
| ------------ | ----- | ------ | ------ | ---------------- |
| `a`            | yes   | yes    | yes    | yes              |
| `abbr`         | yes   | yes    | yes    |                  |
| `address`      | yes   | yes    | yes    |                  |
| `article`      | yes   | yes    | yes    |                  |
| `aside`        | yes   | yes    | yes    |                  |
| `b`            | yes   | yes    | yes    |                  |
| `bdi`          | yes   | yes    | yes    |                  |
| `bdo`          | yes   | yes    | yes    |                  |
| `big`          | yes   | yes    | yes    |                  |
| `blockquote`   | yes   | yes    | yes    |                  |
| `br`           | yes   | yes    | yes    |                  |
| `caption`      | yes   | yes    | yes    |                  |
| `center`       | yes   | yes    | yes    |                  |
| `cite`         | yes   | yes    | yes    |                  |
| `code`         | yes   | yes    | yes    |                  |
| `col`          | yes   | yes    | yes    |                  |
| `colgroup`     | yes   | yes    | yes    |                  |
| `dd`           | yes   | yes    | yes    |                  |
| `del`          | yes   | yes    | yes    |                  |
| `div`          | yes   | yes    | yes    | yes              |
| `dl`           | yes   | yes    | yes    |                  |
| `dt`           | yes   | yes    | yes    |                  |
| `em`           | yes   | yes    | yes    |                  |
| `fieldset`     | yes   | yes    | yes    |                  |
| `font`         |       | yes    | yes    |                  |
| `footer`       | yes   | yes    | yes    |                  |
| `h1`           | yes   | yes    | yes    |                  |
| `h2`           | yes   | yes    | yes    |                  |
| `h3`           | yes   | yes    | yes    |                  |
| `h4`           | yes   | yes    | yes    |                  |
| `h5`           | yes   | yes    | yes    |                  |
| `h6`           | yes   | yes    | yes    |                  |
| `header`       | yes   | yes    | yes    |                  |
| `hr`           | yes   | yes    | yes    |                  |
| `i`            | yes   | yes    | yes    |                  |
| `img`          | yes   | yes    | yes    | yes              |
| `ins`          | yes   | yes    | yes    |                  |
| `label`        | yes   | yes    | yes    | yes              |
| `legend`       | yes   | yes    | yes    |                  |
| `li`           | yes   | yes    | yes    |                  |
| `mark`         | yes   | yes    | yes    |                  |
| `nav`          | yes   | yes    | yes    |                  |
| `ol`           | yes   | yes    | yes    |                  |
| `p`            | yes   | yes    | yes    |                  |
| `pre`          | yes   | yes    | yes    |                  |
| `q`            | yes   | yes    | yes    |                  |
| `rt`           | yes   | yes    | yes    |                  |
| `ruby`         | yes   | yes    | yes    |                  |
| `s`            | yes   | yes    | yes    |                  |
| `section`      | yes   | yes    | yes    |                  |
| `small`        | yes   | yes    | yes    |                  |
| `span`         | yes   | yes    | yes    | yes              |
| `strong`       | yes   | yes    | yes    |                  |
| `sub`          | yes   | yes    | yes    |                  |
| `sup`          | yes   | yes    | yes    |                  |
| `table`        | yes   | yes    | yes    |                  |
| `tbody`        | yes   | yes    | yes    |                  |
| `td`           | yes   | yes    | yes    |                  |
| `tfoot`        | yes   | yes    | yes    |                  |
| `th`           | yes   | yes    | yes    |                  |
| `thead`        | yes   | yes    | yes    |                  |
| `tr`           | yes   | yes    | yes    |                  |
| `tt`           | yes   | yes    | yes    |                  |
| `u`            | yes   | yes    | yes    |                  |
| `ul`           | yes   | yes    | yes    |                  |



### Observations on Accessibility
  
We have examined the developer documentation, looking at the accessibility features for the four MiniApp platforms. 
Based on the high-level documentation, we observe a __lack of accessibility support in general__. Only some platforms may include effective accessibility mechanisms.

- __Alipay Mini Programs__ support ARIA roles and labels to enhance the semantics of the elements `view`, `text`, `icon`, `button`, `label`, `checkbox`, `switch`, `image`, and `radio`. In concrete, this platform supports `aria-label`, `aria-labelledby`, `role`, `aria-expanded` and `aria-checked`. 	
- No references to WAI, WCAG, ARIA or accessibility in [__Baidu__'s documentation](https://smartprogram.baidu.com/).
- __QuickApps__ supports `aria-label`.						
- __WeChat__: Extensive ARIA support, [only in Windows and MacOS](https://developers.weixin.qq.com/miniprogram/dev/component/aria-component.html).


One of the benefit of using standard HTML components is the (current) supported accessibility mechanisms, extensively tested and validated by assistive technologies. 


### Complete MiniApp/HTML Elements Table 

| Type | 2+ impl? | Feature | Just style? | Just funct.? | W3C Rec. | Standard solution | QuickApp | Alipay | Baidu | WeChat | Annotations |
| ---- | -------- | ------- | ----------- | ------------ | -------- | ----------------- | -------- | ------ | ----- | ------ | ----------- |
| Container | yes | Content Division Element | | | `<div>` | direct usage | `<div>` | `<view>` | `<view>` | `<view>`, `<page-container>` | |
|  | yes | Content Span (Inline container) | | | `<span>` | direct usage | `<span>` | | | `<span>` | |
|  |  | Dialog | | | `<dialog>` | direct usage | `<popup>` | | | | |
|  | yes | Stacking container | yes | | | block + CSS (`div { position: relative; }`) | `<stack>` | `<cover-view>`, `<cover-image>` | `<cover-view>`, `<cover-image>` | `<cover-view>` `<cover-image>` | Could be done just with specific CSS classes and styles. Custom Element? |
|  | yes | Slideshow (carousel) | yes | | | HTML + CSS (block + CSS Flexbox + `overscroll-behavior` + `scroll-behavior`...) | `<swiper>` | `<swiper>` | `<swiper>`, `<swiper-item>` | `<swiper>`, `<swiper-item>` | Could be done just with specific CSS classes and styles. Custom Element? |
|  | yes | Tabs | yes | | | (OpenUI) (`nav`s + `section` + CSS) | `<tabs>`, `<tab-bar>`, `<tab-content>` | `<tabs>`, `<tab-content>` | `<tabs>`, `<tab-item>` | | Could be done just with specific CSS classes and styles. Custom Element? |
|  | yes | List container | yes | | | `<ul>``<li>` | `<list>`, `<list-item>` | | | `<list-builder>`, `<list-view>` | Could be done just with specific CSS classes and styles. Custom Element? |
|  | yes | Fixed container | yes | | `<div>` or any other block element | block elements + CSS | | | `<root-portal>` | `<root-portal>` | Could be done just with specific CSS classes and styles. Custom Element? |
|  | yes | Scrolling container | yes | | `<div>` or any other block element | block elements + CSS | | `<scroll-view>` | `<scroll-view>` | `<scroll-view>` | Could be done just with specific CSS classes and styles. Custom Element? |
|  | | Grid layout | yes | | `<div>` or any other block element | block elements + CSS | | | | `<grid-builder>`, `<grid-view>`, `<sticky-header>`,  `<sticky-section>` | Could be done just with specific CSS classes and styles. Custom Element? |
|  | | Nested scroll layout | yes | | `<div>` or any other block element | block elements + CSS | | | | `<nested-scroll-body>`, `<nested-scroll-header>` | Could be done just with specific CSS classes and styles. Custom Element? |
|  | | Marquee | yes | | `<marquee>` (deprecated) | block elements + CSS | `<marquee>` | | | | Could be done just with specific CSS classes and styles. Custom Element? |
|  | yes | Drag and drop container | | yes | | `div` + Drag and Drop API | | `<movable-view>`, `<movable-area>` | `<movable-view>`, `<movable-area>` | `<movable-view>`, `<movable-area>`, `<draggable-sheet>` | Could be done just with specific CSS classes and styles. Custom Element? |
|  | | Pull to refresh | | yes | | `div` + JS + CSS | `<refresh>` | | | | Could be done just with specific CSS classes and styles. Custom Element? |
|  | yes | Conditional block (media query) | | | | CSS media queries | | `<match-media>` | | `<match-media>` | Alternative for rendering |
|  | | Navigation Bar | | | `<nav>` | direct usage + CSS | | | | `<navigation-bar>` | |
| Content | yes | Image | | | `<img>`, `<picture>` | direct usage | `<image>` | `<image>` | `<image>` | `<image>` | |
|  | yes | Icon | yes | | `<img>`, `<span>` | OpenUI research HTML + CSS | | `<icon>` | `<icon>` | `<icon>` | Could it be a good opportunity to propose new works on this? (OpenUI activities) |
|  | yes | Progress indicator | | | `<progress>` | HTML + CSS | `<progress>` | `<progress>` | `<progress>` | `<progress>` | Differences in the attributes (includes attributes for styling) |
|  | yes | Anchor | | | `<a>` | direct usage | `<a>` | `<navigator>` | `<navigator>` | `<navigator>` | Same functionality, different attributes, CSS atrributes |
|  | yes | Text  (no semantics) | | | `<span>` | direct usage | `<text>` | `<text>` | `<text>` | `<text>` | Just text, no semantics |
|  | yes | Web-view (external URL) | | | `<iframe>` | direct usage | `<web>` | `<web-view>` | `<web-view>` | `<web-view>` | |
|  | yes | <a name="html-rich-content">HTML-rich content</a> | | | standard elements | subset of HTML elements | `<richtext>` | `<rich-text>` | `<rich-text>` | `<rich-text>` | Reduced [set of HTML](#trusted-html) |
|  | yes | Map | | | | (need additional services) | `<map>`, `<custommarker>` | `<map>` | `<map>` | `<map>` | Could it be a good opportunity to propose new works on this? |
|  | yes | Advertisement | | | | (need additional services) | `<ad>` | `<ad>` | `<ad>` | `<ad>`, `<ad-custom>` | Could it be a good opportunity to propose new works on this? |
|  | | 3D-model | | | `<model>` (WIP) | direct usage | | | `<modelviewer>` | | |
|  | | Comment list | | | `<ul>` with `<q>` | (need additional services) | | | `<comment-list>`, `<comment-detail>` | | |
| Forms | yes | Textual input | | | `<input>` | direct usage (limiting types) | `<input>` | `<input>` | `<input>` | `<input>` | Input mechanism and type of data |
|  | yes | Image capture input | | | `<input type="file" accept="image/\*" capture...` | direct usage | `<camera>` | `<camera>` | `<camera>` | `<camera>`, `<live-pusher>` | Control of the outcome with functions, better integration with the camera (flash) |
|  | yes | Multiple-line input | | | `<textarea>` | direct usage | `<textarea>` | `<textarea>` | `<textarea>` | `<textarea>` | |
|  | yes | Checkbox | | | `<input type="checkbox">` | direct usage | `<input type="checkbox">` | `<checkbox>`, `<checkbox-group>` | `<checkbox>`, `<checkbox-group>` | `<checkbox>`, `<checkbox-group>` | |
|  | yes | Radio button | | | `<input type="radio">` | direct usage | `<input type="radio">` | `<radio>`, `<radio-group>` | `<radio>`, `<radio-group>` | `<radio>`, `<radio-group>` | |
|  | yes | Form | | | `<form>` | direct usage | | `<form>` | `<form>` | `<form>` | |
|  | yes | Button | | | `<button>` | direct usage | `<input type="button">` | `<button>` | `<button>` | `<button>` | |
|  | yes | Label | | | `<label>` | direct usage | `<label>` | `<label>` | `<label>` | `<label>` | |
|  | yes | Select list | | | `<select>`, `<optgroup>`, `<option>` | direct usage + CSS | `<select>`, `<option>` | `<picker>`, `<picker-view>` | `<picker>`, `<picker-view>`, `<picker-view-column>` | `<picker>`, `<picker-view>`, `<picker-view-column>` | Similar to `<input>` (time, date, region) or `<select>` (selector, multiSelector) |
|  | yes | Slider | | | `<input type="range">` | direct usage | `<slider>` | `<slider>` | `<slider>` | `<slider>` | |
|  | yes | Picker (scroll selector) | | | `<select>`, `<option>` | direct usage + CSS | `<picker>` | `<picker>`, `<picker-view>` | `<picker>`, `<picker-view>`, `<picker-view-column>` | `<picker>`, `<picker-view>`, `<picker-view-column>` | Similar to `<input>` (time, date, region) or `<select>` (selector, multiSelector) |
|  | yes | Switch button | yes | | `<input type="checkbox">` (OpenUI) | HTML + CSS | `<switch>` | `<switch>` | `<switch>` | `<switch>` | Could be done just with specific CSS classes and styles. Custom Element? |
|  | | Sharing button | | yes | `<button>` | Web Share API | `<share-button>` | | | | May be implemented as a Web Component |
|  | | Like button | yes | yes | `<button>` | (need additional services) | | | `<like>` | | May be implemented as a Web Component |
|  | | Specific action button | yes | yes | `<button>` | (need additional services) | | `<contact-button>`, `<lifestyle>`, `<join-group-chat>`… | `<like>`, `<follow-swan>`, `<inline-payment>`, `<login>`, `<comment-list>`… | `<official-account>`, `<store-home>`, `<store-product>` | May be implemented as a Web Component |
|  | | Rating panel | yes | yes | `<radio>` | HTML + CSS | `<rating>` | | | | May be implemented as a Web Component |
|  | | Rich text editor | | yes | | (need additional services) | | | | `<editor>` | May be implemented as a Web Component |
|  | | Selection of text | | yes | | Selection API | | | | `<selection>` | May be implemented as a Web Component |
|  | | Keyboard overlay (input) | | yes | | Implementation-specific | | | | `<keyboard-accessory>` |  _VirtualKeyboard API_ |
|  | | Payment panel | | yes | | (need additional services) | | | `<inline-payment-panel>` | | May be implemented as a Web Component |
| Media | yes | Audio content | | | `<audio>` | direct usage | `<video>` | `<video>` | `<audio>` | `<audio>` | |
|  | yes | Video content | | | `<video>` | direct usage | `<video>` | `<video>` | `<video>` | `<video>`, `<channel-live>`, `<channel-video>`, `<live-player>`, | |
|  | | AR Camera | | | | _WebXR Device API_ | | | `<ar-camera>` | | |
|  | yes | Canvas | | | `<canvas>` | direct usage | `<canvas>` | `<canvas>` | `<canvas>` | `<canvas>` | |
|  | | Video/audio conference | | | | (need additional services) | | | `<rtc-room>`, `<rtc-room-item>` | `<voip-room>` | |
| Animations | yes | Lottie animation | yes | | | (need additional services) | `<lottie>` | `<lottie>` | `<animation-view>` | | Could it be a good opportunity to propose new works on this? |
|  | | Video animation | yes | | `<video>` | direct usage | | | `<animation-video>` | | _Web Animations API_ |
|  | | Transition of pages | yes | | | | | | | `<open-container>` | _View Transitions API_ |
|  | | Transition of element between pages | yes | | | | | | | `<share-element>` | _View Transitions API_ |
| Metadata | yes | Page metadata | | | `<meta>` | direct usage | | | `<page-meta>` | `<page-meta>` | |












