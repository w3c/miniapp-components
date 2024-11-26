# MiniApp APIs Gap Analysis 

## Scope of the analysis

As we [proposed at TPAC 2024](https://www.w3.org/2024/09/26-miniapp-minutes.html#x388), we have analyzed and collected insights about the requirements for the essential structural [MiniApp elements](./gap-analysis-elements) (i.e., the HTML-like elements used in the MiniApp components) and the API and services associated to different MiniApp platforms (this document). 

The main objective of the analysis is to collect insights on the common requirements for MiniApps, and to understand the feasibility of reusing the wide-spread standard Web standards (i.e., DOM and Web APIs) to solve the needs of these MiniApps.

For the analysis, we have grouped the similar elements of four reference MiniApp platforms - [QuickApps](https://www.quickapp.cn/), [Alipay Mini Programs](https://docs.alipay.com/mini/developer/), [Baidu Smart Mini Programs](https://smartprogram.baidu.com/developer/index.html), and [WeChat Mini Programs](https://developers.weixin.qq.com/miniprogram/dev/framework/)) - and the equivalent [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) to implement the same capabilities.

EDITOR NOTE: The study is __still in progress__ (please file a issue to fix anything that is wrong), and it might have missed important details. It was totally based on public developer information (most of the documentation is in Chinese).


### Summary of common MiniApps APIs and standard equivalent 


Notes: 
- The column number three (`2+`) indicates if the feature was found in two or more MiniApp implementations.
- The last column indicates the existing equivalent W3C solution. 
- See the [full report](#fulltable) for more details.


| Type  | API |  2+ |  Standard |
| ----  | --- |  -- |  -------- | 
| Basic functions  | Application context info |  yes |  ___Permissions API___ | 
|  | Log printing/management |  yes |  ___Console API___ | 
|  | Page routing |  yes |  ___History API___, ___Navigation API___ | 
|  | Web page opening |  yes |  ___DOM - Window.open()___ | 
|  | Background running |   |  ___Service Worker API___, ___Background Synchronization API___ | 
|  | Text decoding tools |   |  ___Encoding API___ | 
|  | App configurations |  yes |  ___Web Application Manifest___ | 
|  | Profiling, debugger |  yes |  ___Compute Pressure API___, ___Performance APIs___ |
|  | Can I Use |  yes |  ___Media Capabilities API___ | 
|  | Async. timeouts, intervals |  yes |  ___Window.setTimeout()___, ___Window.setInterval()___ | 
|  | Environment variables |  yes |   | 
|  | Media Query |  yes |  ___CSSOM View Module API___ | 
|  | Element selector |  yes |  ___DOM Standard___ | 
|  | Workers |  yes |  ___Web Workers API___, ___Prioritized Task Scheduling API___ | 
|  | Base64 - ArrayBuffer operations |  yes |  ___Window.atob()___, ___Window.btoa()___, ___Uint8Array___ | 
|  | Navigation bar |  yes |   | 
|  | Wasm support |   |  ___WebAssembly JavaScript API___ | 
|  | MiniApp routing |  yes |  ___Launch Handler API___ |
|  | WebView messages |   |  ___DOM - Window.postMessage()___ | 
| UI interaction  | External sharing |  yes |  ___Web Share API___ | 
|  | Pull down to refresh |  yes |  ___CSS Overscroll Behavior Module Level 1___ | 
|  | Web Font loader |  yes |  ___CSS Font Loading API___ | 
|  | Scrolling in the app |  yes |  ___Visual Viewport API___ | 
|  | Animations |  yes |  ___Web Animations API___ | 
|  | Dialog management |  yes |  ___Popover API___ | 
|  | Notifications |   |  ___Push API___ | 
|  | On Screenshot |  yes |   | 
|  | Vibration |  yes |  ___Vibration API___ | 
|  | QR code scan |  yes |  ___Barcode Detection API___ |
|  | Calendar event |  yes |   | 
|  | Contacts |  yes |  ___Contact Picker API___ |
|  | Alarms |   |   | 
|  | Driving safety restrictions |   |   | 
|  | Rich editor |  yes |  ___EditContext API___ |
|  | City, region picker |   |   | 
| Network access  | Fetch |  yes |  ___Fetch API___ | 
|  | Prefetch content |  yes |  ___Background Fetch API___, ___Speculation Rules API___ |
|  | Upload and download |  yes |  ___Fetch API___ | 
|  | WebSocket |  yes |  ___The WebSocket API___ | 
|  | mDNS service |   |   | 
| Data management  | Data storage |  yes |  ___Storage API___ (___IndexedDB API___), ___Web Storage API___ | 
|  | File system management |  yes |  ___File System API___, ___File and Directory Entries API___ | 
|  | Data exchange with other MiniApps |  yes |  ___Broadcast Channel API___, ___Channel Messaging API___ | 
|  | Compression/Decompression |  yes |   | 
|  | Clipboard |  yes |  ___Clipboard API___ | 
|  | Cryptography |  yes |  ___Web Crypto API___ | 
|  | Cache |   |  ___Content Index API___ |
| Sensors  | Accelerometer |  yes |  ___Sensor APIs (Accelerometer)___ | 
|  | Compass |  yes |  ___Sensor APIs (Magnetometer)___ | 
|  | Gyroscope |  yes |  ___Sensor APIs (Gyroscope)___ | 
|  | Proximity sensor |   |  ___Proximity Sensor___ |
|  | Step counter |  yes |   | 
|  | Ambient light sensor |   |  ___Sensor APIs (Ambient Light Sensor)___ | 
|  | Shake detection |   |   | 
|  | Location |  yes |  ___Geolocation API___, ___Geolocation Sensor___ | 
|  | Is screen locked? |   |  ___Idle Detection API___ |
|  | Screen orientation |   |  ___Screen Orientation API___ | 
|  | Battery level |  yes |  ___Battery Status API___ |
|  | Memory warning (or available) |  yes |  ___Device Memory API___ |
| System Settings  | System volume |   |  ___HTMLMediaElement.volume___ | 
|  | Wake lock |  yes |  ___Screen Wake Lock API___ | 
|  | Device information |  yes |  ___User-Agent Client Hints API___ |
|  | Screen brightness |  yes |   | 
|  | Open system settings, authorization |  yes |  ___Notifications API___ | 
|  | Accessibility enabled? |  yes |   | 
| Communication  | NFC |  yes |  ___Web NFC API___ |
|  | NFC HCE |   |   | 
|  | Bluetooth |  yes |  ___Web Bluetooth API___ |
|  | Wi-Fi |  yes |   | 
|  | Network status, telecom info |  yes |  ___Network Information API___ |
|  | Phone calls |  yes |   | 
|  | SMS message sending |  yes |   | 
| Multimedia  | Camera (photo/video) |  yes |  ___Media Capture, Streams API___ | 
|  | AR Camera |  yes |  ___WebXR Device API___ |
|  | Audio recording |  yes |  ___MediaStream Recording API___ | 
|  | Image processing |  yes |  ___WebCodecs API___, ___MediaStream Image Capture API___ | 
|  | Video processing |  yes |  WebCodecs API, ___Insertable Streams for MediaStreamTrack API___ | 
|  | Screen recording |   |  ___Screen Capture API___,  ___MediaRecorder API___ | 
|  | Canvas |  yes |  ___Canvas API___ | 
|  | Audio playback |  yes |  ___Web Audio API___, ___Media Capture___, ___Streams API___ | 
|  | Video playback |  yes |  ___Media Capture and Streams API___ | 
|  | System audio player |  yes |  ___Audio Output Devices API___ |
|  | Text to speech |  yes |  ___Web Speech API___ | 
|  | Speech recognition |  yes |  ___Web Speech API___ | 
|  | OCR |  yes |   | 
|  | AI object classification |  yes |   | 
|  | Face detection |  yes |   | 
| Platform-specific  | Login |  yes |  ___FedCM API, Web Authentication API, WebOTP API___ | 
|  | Payments |  yes |  ___Payment Request, Payment Handlers, SPC___ APIs | 
|  | Tokens, cards |  yes |  ___Digital Credentials API___ |
|  | Push notifications |   |  ___Push API___ | 
|  | Ads |  yes |   | 
|  | User credentials management |   |  ___Credential Management API___ | 
|  | Text translation |  yes |   | 
|  | RTC conferences |  yes |   | 
|  | Live video |  yes |   | 
|  | Map management |  yes |   | 
|  | Route management |   |   | 
|  | Biometric authentication |   |  ___Web Authentication API___ | 
|  | AI inferences |   |  ___Web Neural Network API___ | 
|  | Server time |   |   | 
| App Management  | App marketplace management |  yes |   | 
|  | Home screen icon |   |  ___Service Worker API___ | 
|  | Statistics - Analytics |  yes |   | 
|  | Sub-package management |  yes |  ___ECMAScript import___ | 
|  | Update manager |  yes |  ___Server-sent events___ | 


### <a name="fulltable"></a>Common MiniApps APIs and standard equivalent full analysis 

Notes: 
- The eight column (`2+`) indicates if the feature was found in two or more MiniApp implementations.
- Columns 9 and 10 (last one) indicate the existing equivalent W3C solution and if the solution is widely supported or it is under experimentation (exp) or has limited (lim) support. 

| Type | API | Description | QuickApps | Baidu | Alipay | WeChat | 2+ | Standard | WPT |
| ---- | --- | ----------- | --------- | ----- | ------ | ------ | -- | -------- | --- | 
| Basic functions | Application context info | Get contextual info about the app | yes | yes | yes | yes | yes | ___Permissions API___ | [permissions/](https://wpt.fyi/results/permissions) | 
| | Log printing/management | console.debug/log/info/warn/error(message) | yes |  |  | yes | yes | ___Console API___ | [console/](https://wpt.fyi/results/console) | 
| | Page routing | Routing options, navigation. including set/get URL | yes | yes | yes | yes | yes | ___History API___, ___Navigation API___ | [navigation-api/](https://wpt.fyi/results/navigation-api) | 
| | Web page opening | Opening webpages in the WebView | yes |  | yes |  | yes | ___DOM - Window.open()___ | [dom/](https://wpt.fyi/results/dom) | 
| | Background running | Runs apps in the background | yes |  |  |  |  | ___Service Worker API___, ___Background Synchronization API___ | [service-workers/](https://wpt.fyi/results/service-workers), [background-sync/](https://wpt.fyi/results/background-sync) | 
| | Text decoding tools | Text operations | yes |  |  |  |  | ___Encoding API___ | | 
| | App configurations | Locale, screen orientation, theme mode, etc. | yes | yes |  | yes | yes | ___Web Application Manifest___ | | 
| | Profiling, debugger | V8 inspector, information about performance | yes | yes | yes | yes | yes | ___Compute Pressure API___, ___Performance APIs___ | [compute-pressure/](https://wpt.fyi/results/compute-pressure) |
| | Can I Use | Can I use elements from the running platform |  | yes | yes | yes | yes | ___Media Capabilities API___ | [media-capabilities/](https://wpt.fyi/results/media-capabilities) | 
| | Async. timeouts, intervals | Management of timeouts and intervals | yes | yes |  | yes | yes | ___Window.setTimeout()___, ___Window.setInterval()___ | [dom/](https://wpt.fyi/results/dom) | 
| | Environment variables | Access to environment variables |  | yes | yes | yes | yes |  | | 
| | Media Query | Media query listeners, checks | yes |  | yes | yes | yes | ___CSSOM View Module API___ | [css/](https://wpt.fyi/results/css) | 
| | Element selector | Query selector | yes | yes | yes | yes | yes | ___DOM Standard___ | [dom/](https://wpt.fyi/results/dom) | 
| | Workers | Worker management |  | yes | yes | yes | yes | ___Web Workers API___, ___Prioritized Task Scheduling API___ | [workers/](https://wpt.fyi/results/workers), [scheduler/](https://wpt.fyi/results/scheduler) | 
| | Base64 - ArrayBuffer operations | Base64 management tools |  |  | yes | yes | yes | ___Window.atob()___, ___Window.btoa()___, ___Uint8Array___ | [dom/](https://wpt.fyi/results/dom) | 
| | Navigation bar | Navigation bar management |  | yes | yes | yes | yes |  |  | 
| | Wasm support | WebAssembly support |  |  |  | yes |  | ___WebAssembly JavaScript API___ | [wasm/](https://wpt.fyi/results/wasm) | 
| | MiniApp routing | Switch MiniApp programmatically |  | yes | yes | yes | yes | ___Launch Handler API___ |  |
| | WebView messages | Connection with WebView |  |  | yes |  |  | ___DOM - Window.postMessage()___ | [dom/](https://wpt.fyi/results/dom) | 
| UI interaction | External sharing | Shares data with other apps. | yes | yes | yes | yes | yes | ___Web Share API___ | [web-share/](https://wpt.fyi/results/web-share) | 
| | Pull down to refresh | Triggering the feature | yes | yes | yes | yes | yes | ___CSS Overscroll Behavior Module Level 1___ | [css/](https://wpt.fyi/results/css) | 
| | Web Font loader | Dynamically loading web fonts |  | yes | yes | yes | yes | ___CSS Font Loading API___ | [font-access/](https://wpt.fyi/results/font-access) | 
| | Scrolling in the app | Scroll interaction |  | yes | yes | yes | yes | ___Visual Viewport API___ | [visual-viewport/](https://wpt.fyi/results/visual-viewport) | 
| | Animations | Animation of visual elements | yes | yes | yes | yes | yes | ___Web Animations API___ | [web-animations/](https://wpt.fyi/results/web-animations) | 
| | Dialog management | Displaying different messages, dialogues, toasts, popup menus… | yes | yes | yes | yes | yes | ___Popover API___ | [popovers/](https://wpt.fyi/results/html/semantics/popovers/) | 
| | Notifications | Push notifications management | yes |  |  |  |  | ___Push API___ | [push-api/](https://wpt.fyi/results/push-api) | 
| | On Screenshot | Monitor capture events from the user | yes | yes | yes | yes | yes |  | | 
| | Vibration | Different modes of vibration | yes | yes | yes | yes | yes | ___Vibration API___ | [vibration/](https://wpt.fyi/results/vibration) | 
| | QR code scan | QR scan through the camera | yes | yes | yes | yes | yes | ___Barcode Detection API___ | [shape-detection/](https://wpt.fyi/results/shape-detection) |
| | Calendar event | Insert event in the calendar | yes | yes |  | yes | yes |  | | 
| | Contacts | Contact picker (WeChat also add) | yes | yes | yes | yes | yes | ___Contact Picker API___ | [contacts/](https://wpt.fyi/results/contacts) |
| | Alarms | Setting the device's alarm | yes |  |  |  |  |  | | 
| | Driving safety restrictions | Driving mode restrictions | yes |  |  |  |  |  | | 
| | Rich editor | Management of rich editor |  | yes |  | yes | yes | ___EditContext API___ | [editing/](https://wpt.fyi/results/editing) |
| | City, region picker | Location information |  |  | yes |  |  |  | | 
| Network access | Fetch | Fetch resources | yes | yes | yes | yes | yes | ___Fetch API___ | [fetch/](https://wpt.fyi/results/fetch) | 
| | Prefetch content | Prefetch content (video, audio, documents) | yes | yes | yes | yes | yes | ___Background Fetch API___, ___Speculation Rules API___ | [background-fetch/](https://wpt.fyi/results/background-fetch), [background-sync/](https://wpt.fyi/results/background-sync), [speculation-rules/](https://wpt.fyi/results/speculation-rules) |
| | Upload and download | HTTP POST, PUT and GET | yes | yes | yes | yes | yes | ___Fetch API___ | [fetch/](https://wpt.fyi/results/fetch) | 
| | WebSocket | WebSocket management | yes | yes | yes | yes | yes | ___The WebSocket API___ | [websockets/](https://wpt.fyi/results/websockets) | 
| | mDNS service | mDNS discovery |  |  |  | yes |  |  | | 
| Data management | Data storage | Get, set key=value pairs | yes | yes | yes | yes | yes | ___Storage API___ (___IndexedDB API___), ___Web Storage API___ | [storage-access-api/](https://wpt.fyi/results/storage-access-api)
[storage/](https://wpt.fyi/results/storage), [webstorage/](https://wpt.fyi/results/webstorage) | 
| | File system management | Storage, management in the local file system | yes | yes | yes | yes | yes | ___File System API___, ___File and Directory Entries API___ | [file-system-access/](https://wpt.fyi/results/file-system-access), [FileAPI/](https://wpt.fyi/results/FileAPI) | 
| | Data exchange with other MiniApps | Data exchange between installed apps | yes |  | yes | yes | yes | ___Broadcast Channel API___, ___Channel Messaging API___ | [webmessaging/](https://wpt.fyi/results/webmessaging)
 | 
| | Compression/Decompression | ZIP file compression/decompression | yes | yes |  | yes | yes |  | [compression/](https://wpt.fyi/results/compression) | 
| | Clipboard | Clipboard set/get | yes | yes | yes | yes | yes | ___Clipboard API___ | [clipboard-apis/](https://wpt.fyi/results/clipboard-apis) | 
| | Cryptography | Encryption, decryption, random | yes |  | yes | yes | yes | ___Web Crypto API___ | [WebCryptoAPI/](https://wpt.fyi/results/WebCryptoAPI) | 
| | Cache | Cache management (rules, cleaning, etc.) |  |  |  | yes |  | ___Content Index API___ | [content-index/](https://wpt.fyi/results/content-index) |
| Sensors | Accelerometer | Sensors | yes | yes | yes | yes | yes | ___Sensor APIs (Accelerometer)___ | [accelerometer/](https://wpt.fyi/results/accelerometer) | 
| | Compass | Sensors | yes | yes | yes | yes | yes | ___Sensor APIs (Magnetometer)___ | [magnetometer/](https://wpt.fyi/results/magnetometer) | 
| | Gyroscope | Sensors | yes | yes | yes | yes | yes | ___Sensor APIs (Gyroscope)___ | [gyroscope/](https://wpt.fyi/results/gyroscope) | 
| | Proximity sensor | Sensors | yes |  |  |  |  | ___Proximity Sensor___ | [proximity/](https://wpt.fyi/results/proximity) |
| | Step counter | Sensors | yes |  | yes | yes | yes |  | | 
| | Ambient light sensor | Sensors |  |  |  |  |  | ___Sensor APIs (Ambient Light Sensor)___ | [ambient-light/](https://wpt.fyi/results/ambient-light) | 
| | Shake detection | Sensors |  |  | yes |  |  |  | | 
| | Location | Geolocation API | yes | yes | yes | yes | yes | ___Geolocation API___, ___Geolocation Sensor___ | [geolocation-sensor/](https://wpt.fyi/results/geolocation-sensor), [geolocation/](https://wpt.fyi/results/geolocation) | 
| | Is screen locked? | Check if the screen is locked | yes |  |  |  |  | ___Idle Detection API___ | [idle-detection/](https://wpt.fyi/results/idle-detection) |
| | Screen orientation | Information about the screen orientation | yes | yes | yes | yes |  | ___Screen Orientation API___ | [screen-orientation/](https://wpt.fyi/results/screen-orientation) | 
| | Battery level | Status of the battery level | yes | yes | yes | yes | yes | ___Battery Status API___ | [battery-status/](https://wpt.fyi/results/battery-status) |
| | Memory warning (or available) | Warning for low memory in the device |  | yes | yes | yes | yes | ___Device Memory API___ | [device-memory/](https://wpt.fyi/results/device-memory), [measure-memory/](https://wpt.fyi/results/measure-memory) |
| System Settings | System volume | Media volume (get/set) | yes |  |  |  |  | ___HTMLMediaElement.volume___ | [audio_volume_check](https://wpt.fyi/results/html/semantics/embedded-content/media-elements/audio_volume_check.html) | 
| | Wake lock | Force screen on | yes | yes | yes | yes | yes | ___Screen Wake Lock API___ | [screen-wake-lock/](https://wpt.fyi/results/screen-wake-lock) | 
| | Device information | Complete information about the device and the user (CPU, locale, window info, user ID…) | yes | yes | yes | yes | yes | ___User-Agent Client Hints API___ | [client-hints/](https://wpt.fyi/results/client-hints), [ua-client-hints/](https://wpt.fyi/results/ua-client-hints) |
| | Screen brightness | Screen brightness management (get/set) | yes | yes | yes | yes | yes |  | | 
| | Open system settings, authorization | Open system settings (e.g., Bluetooth) |  |  | yes | yes | yes | ___Notifications API___ | [notifications/](https://wpt.fyi/results/notifications) | 
| | Accessibility enabled? | Check if accessibility features enabled |  |  | yes | yes | yes |  | | 
| Communication | NFC | NFC management | yes |  |  | yes | yes | ___Web NFC API___ | [web-nfc/](https://wpt.fyi/results/web-nfc) |
| | NFC HCE | Host card emulation |  |  |  | yes |  |  |  | 
| | Bluetooth | Bluetooth discovery, connection | yes |  | yes | yes | yes | ___Web Bluetooth API___ | [bluetooth/](https://wpt.fyi/results/bluetooth) |
| | Wi-Fi | WiFi connection management | yes | yes | yes | yes | yes |  | | 
| | Network status, telecom info | Info about the network, may even have the carrier and type of connection | yes | yes | yes | yes | yes | ___Network Information API___ | [netinfo/](https://wpt.fyi/results/netinfo) |
| | Phone calls | Enable phone calls |  | yes | yes | yes | yes |  |  | 
| | SMS message sending | Sending SMS | yes |  | yes | yes | yes |  |  | 
| Multimedia | Camera (photo/video) | Image management (pick image/video, take photo/videos, previews) | yes | yes | yes | yes | yes | ___Media Capture, Streams API___ | [mediacapture-image/](https://wpt.fyi/results/mediacapture-image), [mediacapture-streams/](https://wpt.fyi/results/mediacapture-streams)
, [streams/](https://wpt.fyi/results/streams) | 
| | AR Camera | AR features using the camera |  | yes |  | yes | yes | ___WebXR Device API___ | [webxr/](https://wpt.fyi/results/webxr) |
| | Audio recording | Audio recording | yes | yes | yes | yes | yes | ___MediaStream Recording API___ | [mediacapture-streams/](https://wpt.fyi/results/mediacapture-streams) | 
| | Image processing | Compression, EXIF management, edition | yes | yes | yes | yes | yes | ___WebCodecs API___, ___MediaStream Image Capture API___ | [webcodecs/](https://wpt.fyi/results/webcodecs), [mediacapture-image/](https://wpt.fyi/results/mediacapture-image)| 
| | Video processing | Video info, capture of frames… | yes |  | yes | yes | yes | WebCodecs API, ___Insertable Streams for MediaStreamTrack API___ | | 
| | Screen recording | Screen recorder |  |  |  | yes |  | ___Screen Capture API___,  ___MediaRecorder API___ | [screen-capture/](https://wpt.fyi/results/screen-capture), [mediacapture-record/](https://wpt.fyi/results/mediacapture-record) | 
| | Canvas | Canvas management | yes | yes | yes | yes | yes | ___Canvas API___ | [canvas/](https://wpt.fyi/results/html/canvas/element) | 
| | Audio playback | Audio playback | yes | yes | yes | yes | yes | ___Web Audio API___, ___Media Capture___, ___Streams API___ | [html-media-capture/](https://wpt.fyi/results/html-media-capture), [streams/](https://wpt.fyi/results/streams), [webaudio/](https://wpt.fyi/results/webaudio) | 
| | Video playback | Video playback | yes | yes | yes | yes | yes | ___Media Capture and Streams API___ | [html-media-capture/](https://wpt.fyi/results/html-media-capture), [streams/](https://wpt.fyi/results/streams) | 
| | System audio player | Access to the system player |  | yes | yes | yes | yes | ___Audio Output Devices API___ | [audio-output/](https://wpt.fyi/results/audio-output) |
| | Text to speech | Text to Speech (different languages) | yes | yes |  | yes | yes | ___Web Speech API___ | [speech-api/](https://wpt.fyi/results/speech-api) | 
| | Speech recognition | AI speech recognition | yes | yes |  | yes | yes | ___Web Speech API___ |[speech-api/](https://wpt.fyi/results/speech-api) | 
| | OCR | Extraction of information from images (driving license, ID card, etc.) |  | yes |  | yes | yes | ___Shape Detection API___ | [shape-detection/](https://wpt.fyi/results/shape-detection) | 
| | AI object classification | Object recognition and classification from images |  | yes |  | yes | yes | ___Shape Detection API___ | [shape-detection/](https://wpt.fyi/results/shape-detection) | 
| | Face detection | Detection of faces in images and comparisons |  | yes |  | yes | yes |  | ___Shape Detection API___ [shape-detection/](https://wpt.fyi/results/shape-detection) | 
| Platform-specific | Login | Account management | yes | yes | yes | yes | yes | ___FedCM API, Web Authentication API, WebOTP API___ | [fedcm/](https://wpt.fyi/results/fedcm), [webauthn/](https://wpt.fyi/results/webauthn),  [web-otp/](https://wpt.fyi/results/web-otp) | 
| | Payments | In-app payments | yes | yes | yes | yes | yes | ___Payment Request, Payment Handlers, SPC___ APIs | [payment-handler/](https://wpt.fyi/results/payment-handler),[payment-method-basic-card/](https://wpt.fyi/results/payment-method-basic-card), [payment-method-id/](https://wpt.fyi/results/payment-method-id), [payment-request/](https://wpt.fyi/results/payment-request), [secure-payment-confirmation/](https://wpt.fyi/results/secure-payment-confirmation) | 
| | Tokens, cards | Management of wallet |  |  | yes | yes | yes | ___Digital Credentials API___ | [digital-credentials/](https://wpt.fyi/results/digital-credentials) |
| | Push notifications | Push notifications server | yes |  |  |  |  | ___Push API___ | [push-api/](https://wpt.fyi/results/push-api) | 
| | Ads | Ads management | yes | yes |  | yes | yes |  | | 
| | User credentials management | Storage of credentials in the keychain | yes |  |  |  |  | ___Credential Management API___ | [credential-management/](https://wpt.fyi/results/credential-management) | 
| | Text translation | Translation service | yes |  |  | yes | yes |  | | 
| | RTC conferences | Video/audio conference management |  | yes |  | yes | yes |  | [webrtc/](https://wpt.fyi/results/webrtc) | 
| | Live video | Live video component management |  | yes |  | yes | yes |  | | 
| | Map management | Map markers, scale, etc. | yes | yes | yes | yes | yes |  | | 
| | Route management | Route calculation |  |  | yes |  |  |  | | 
| | Biometric authentication | Management of biometric authentication |  |  |  | yes |  | ___Web Authentication API___ | [webauthn/](https://wpt.fyi/results/webauthn) | 
| | AI inferences | AI inference engine |  |  |  | yes |  | ___Web Neural Network API___ | [webnn/](https://wpt.fyi/results/webnn) | 
| | Server time | Get server time |  |  | yes |  |  |  | [server-timing/](https://wpt.fyi/results/server-timing) | 
| App Management | App marketplace management | Offers installation, check if an app is installed, get info and checksums | yes | yes |  |  | yes |  | [installedapp/](https://wpt.fyi/results/installedapp) | 
| | Home screen icon | Install app on home-screen, add widget, and check if installed | yes |  |  |  |  | ___Service Worker API___ | [service-workers/](https://wpt.fyi/results/service-workers), [installedapp/](https://wpt.fyi/results/installedapp) | 
| | Statistics - Analytics | Statistics of usage of the app (clicks, interaction, etc.) | yes | yes |  | yes | yes |  | | 
| | Sub-package management | Control of sub-packages (programmatically) |  |  |  | yes | yes | ___ECMAScript import___ | [ecmascript/](https://wpt.fyi/results/ecmascript) | 
| | Update manager | Management of app updating |  | yes | yes | yes | yes | ___Server-sent events___ | | 


