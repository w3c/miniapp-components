# MiniApp APIs Gap Analysis 

## Scope of the analysis

As we [proposed at TPAC 2024](https://www.w3.org/2024/09/26-miniapp-minutes.html#x388), we have analyzed and collected insights about the requirements for the essential structural [MiniApp elements](./gap-analysis-elements) (i.e., the HTML-like elements used in the MiniApp components) and the API and services associated to different MiniApp platforms (this document). 

The main objective of the analysis is to collect insights on the common requirements for MiniApps, and to understand the feasibility of reusing the wide-spread standard Web standards (i.e., DOM and Web APIs) to solve the needs of these MiniApps.

For the analysis, we have grouped the similar elements of four reference MiniApp platforms - [QuickApps](https://www.quickapp.cn/), [Alipay Mini Programs](https://docs.alipay.com/mini/developer/), [Baidu Smart Mini Programs](https://smartprogram.baidu.com/developer/index.html), and [WeChat Mini Programs](https://developers.weixin.qq.com/miniprogram/dev/framework/)) - and the equivalent [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) to implement the same capabilities.

EDITOR NOTE: The study is __still in progress__ (please file a issue to fix anything that is wrong), and it might have missed important details. It was totally based on public developer information (most of the documentation is in Chinese).


### Summary of common MiniApps APIs and standard equivalent 

Notes: 
- The eight column (`2+`) indicates if the feature was found in two or more MiniApp implementations.
- Columns 9 and 10 (last one) indicate the existing equivalent W3C solution and if the solution is widely supported or it is under experimentation (exp) or has limited (lim) support. 

| Type | API | Description | QuickApps | Baidu | Alipay | WeChat | 2+ | Standard | Exp?/lim? |
| ---- | --- | ----------- | --------- | ----- | ------ | ------ | -- | -------- | --------- | 
| Basic functions | Application context info | Get contextual info about the app | yes | yes | yes | yes | yes | ___Permissions API___ | | 
| | Log printing/management | console.debug/log/info/warn/error(message) | yes |  |  | yes | yes | ___Console API___ | | 
| | Page routing | Routing options, navigation. including set/get URL | yes | yes | yes | yes | yes | ___History API___, ___Navigation API___ | | 
| | Web page opening | Opening webpages in the WebView | yes |  | yes |  | yes | ___DOM - Window.open()___ | | 
| | Background running | Runs apps in the background | yes |  |  |  |  | ___Service Worker API___, ___Background Synchronization API___ | | 
| | Text decoding tools | Text operations | yes |  |  |  |  | ___Encoding API___ | | 
| | App configurations | Locale, screen orientation, theme mode, etc. | yes | yes |  | yes | yes | ___Web Application Manifest___ | | 
| | Profiling, debugger | V8 inspector, information about performance | yes | yes | yes | yes | yes | ___Compute Pressure API___, ___Performance APIs___ | yes|
| | Can I Use | Can I use elements from the running platform |  | yes | yes | yes | yes | ___Media Capabilities API___ | | 
| | Async. timeouts, intervals | Management of timeouts and intervals | yes | yes |  | yes | yes | ___Window.setTimeout()___, ___Window.setInterval()___ | | 
| | Environment variables | Access to environment variables |  | yes | yes | yes | yes |  | | 
| | Media Query | Media query listeners, checks | yes |  | yes | yes | yes | ___CSSOM View Module API___ | | 
| | Element selector | Query selector | yes | yes | yes | yes | yes | ___DOM Standard___ | | 
| | Workers | Worker management |  | yes | yes | yes | yes | ___Web Workers API___, ___Prioritized Task Scheduling API___ | | 
| | Base64 - ArrayBuffer operations | Base64 management tools |  |  | yes | yes | yes | ___Window.atob()___, ___Window.btoa()___, ___Uint8Array___ | | 
| | Navigation bar | Navigation bar management |  | yes | yes | yes | yes |  | | 
| | Wasm support | WebAssembly support |  |  |  | yes |  | ___WebAssembly JavaScript API___ | | 
| | MiniApp routing | Switch MiniApp programmatically |  | yes | yes | yes | yes | ___Launch Handler API___ | yes |
| | WebView messages | Connection with WebView |  |  | yes |  |  | ___DOM - Window.postMessage()___ | | 
| UI interaction | External sharing | Shares data with other apps. | yes | yes | yes | yes | yes | ___Web Share API___ | | 
| | Pull down to refresh | Triggering the feature | yes | yes | yes | yes | yes | ___CSS Overscroll Behavior Module Level 1___ | | 
| | Web Font loader | Dynamically loading web fonts |  | yes | yes | yes | yes | ___CSS Font Loading API___ | | 
| | Scrolling in the app | Scroll interaction |  | yes | yes | yes | yes | ___Visual Viewport API___ | | 
| | Animations | Animation of visual elements | yes | yes | yes | yes | yes | ___Web Animations API___ | | 
| | Dialog management | Displaying different messages, dialogues, toasts, popup menus… | yes | yes | yes | yes | yes | ___Popover API___ | | 
| | Notifications | Push notifications management | yes |  |  |  |  | ___Push API___ | | 
| | On Screenshot | Monitor capture events from the user | yes | yes | yes | yes | yes |  | | 
| | Vibration | Different modes of vibration | yes | yes | yes | yes | yes | ___Vibration API___ | | 
| | QR code scan | QR scan through the camera | yes | yes | yes | yes | yes | ___Barcode Detection API___ | yes |
| | Calendar event | Insert event in the calendar | yes | yes |  | yes | yes |  | | 
| | Contacts | Contact picker (WeChat also add) | yes | yes | yes | yes | yes | ___Contact Picker API___ | yes |
| | Alarms | Setting the device's alarm | yes |  |  |  |  |  | | 
| | Driving safety restrictions | Driving mode restrictions | yes |  |  |  |  |  | | 
| | Rich editor | Management of rich editor |  | yes |  | yes | yes | ___EditContext API___ | yes |
| | City, region picker | Location information |  |  | yes |  |  |  | | 
| Network access | Fetch | Fetch resources | yes | yes | yes | yes | yes | ___Fetch API___ | | 
| | Prefetch content | Prefetch content (video, audio, documents) | yes | yes | yes | yes | yes | ___Background Fetch API___, ___Speculation Rules API___ | yes |
| | Upload and download | HTTP POST, PUT and GET | yes | yes | yes | yes | yes | ___Fetch API___ | | 
| | WebSocket | WebSocket management | yes | yes | yes | yes | yes | ___The WebSocket API___ | | 
| | mDNS service | mDNS discovery |  |  |  | yes |  |  | | 
| Data management | Data storage | Get, set key=value pairs | yes | yes | yes | yes | yes | ___Storage API___ (___IndexedDB API___), ___Web Storage API___ | | 
| | File system management | Storage, management in the local file system | yes | yes | yes | yes | yes | ___File System API___, ___File and Directory Entries API___ | | 
| | Data exchange with other MiniApps | Data exchange between installed apps | yes |  | yes | yes | yes | ___Broadcast Channel API___, ___Channel Messaging API___ | | 
| | Compression/Decompression | ZIP file compression/decompression | yes | yes |  | yes | yes |  | | 
| | Clipboard | Clipboard set/get | yes | yes | yes | yes | yes | ___Clipboard API___ | | 
| | Cryptography | Encryption, decryption, random | yes |  | yes | yes | yes | ___Web Crypto API___ | | 
| | Cache | Cache management (rules, cleaning, etc.) |  |  |  | yes |  | ___Content Index API___ | yes |
| Sensors | Accelerometer | Sensors | yes | yes | yes | yes | yes | ___Sensor APIs (Accelerometer)___ | | 
| | Compass | Sensors | yes | yes | yes | yes | yes | ___Sensor APIs (Magnetometer)___ | | 
| | Gyroscope | Sensors | yes | yes | yes | yes | yes | ___Sensor APIs (Gyroscope)___ | | 
| | Proximity sensor | Sensors | yes |  |  |  |  | ___Proximity Sensor___ | yes |
| | Step counter | Sensors | yes |  | yes | yes | yes |  | | 
| | Ambient light sensor | Sensors |  |  |  |  |  | ___Sensor APIs (Ambient Light Sensor)___ | | 
| | Shake detection | Sensors |  |  | yes |  |  |  | | 
| | Location | Geolocation API | yes | yes | yes | yes | yes | ___Geolocation API___, ___Geolocation Sensor___ | | 
| | Is screen locked? | Check if the screen is locked | yes |  |  |  |  | ___Idle Detection API___ | yes |
| | Screen orientation | Information about the screen orientation | yes | yes | yes | yes |  | ___Screen Orientation API___ | | 
| | Battery level | Status of the battery level | yes | yes | yes | yes | yes | ___Battery Status API___ | yes                  |
| | Memory warning (or available) | Warning for low memory in the device |  | yes | yes | yes | yes | ___Device Memory API___ | yes |
| System Settings | System volume | Media volume (get/set) | yes |  |  |  |  | ___HTMLMediaElement.volume___ | | 
| | Wake lock | Force screen on | yes | yes | yes | yes | yes | ___Screen Wake Lock API___ | | 
| | Device information | Complete information about the device and the user (CPU, locale, window info, user ID…) | yes | yes | yes | yes | yes | ___User-Agent Client Hints API___ | yes |
| | Screen brightness | Screen brightness management (get/set) | yes | yes | yes | yes | yes |  | | 
| | Open system settings, authorization | Open system settings (e.g., Bluetooth) |  |  | yes | yes | yes | ___Notifications API___ | | 
| | Accessibility enabled? | Check if accessibility features enabled |  |  | yes | yes | yes |  | | 
| Communication | NFC | NFC management | yes |  |  | yes | yes | ___Web NFC API___ | yes |
| | NFC HCE | Host card emulation |  |  |  | yes |  |  | | 
| | Bluetooth | Bluetooth discovery, connection | yes |  | yes | yes | yes | ___Web Bluetooth API___ | yes |
| | Wi-Fi | WiFi connection management | yes | yes | yes | yes | yes |  | | 
| | Network status, telecom info | Info about the network, may even have the carrier and type of connection | yes | yes | yes | yes | yes | ___Network Information API___ | yes |
| | Phone calls | Enable phone calls |  | yes | yes | yes | yes |  | | 
| | SMS message sending | Sending SMS | yes |  | yes | yes | yes |  | | 
| Multimedia | Camera (photo/video) | Image management (pick image/video, take photo/videos, previews) | yes | yes | yes | yes | yes | ___Media Capture, Streams API___ | | 
| | AR Camera | AR features using the camera |  | yes |  | yes | yes | ___WebXR Device API___ | yes |
| | Audio recording | Audio recording | yes | yes | yes | yes | yes | ___MediaStream Recording API___ | | 
| | Image processing | Compression, EXIF management, edition | yes | yes | yes | yes | yes | ___WebCodecs API___, ___MediaStream Image Capture API___ | | 
| | Video processing | Video info, capture of frames… | yes |  | yes | yes | yes | WebCodecs API, ___Insertable Streams for MediaStreamTrack API___ | | 
| | Screen recording | Screen recorder |  |  |  | yes |  | ___Screen Capture API___,  ___MediaRecorder API___ | | 
| | Canvas | Canvas management | yes | yes | yes | yes | yes | ___Canvas API___ | | 
| | Audio playback | Audio playback | yes | yes | yes | yes | yes | ___Web Audio API___, ___Media Capture___, ___Streams API___ | | 
| | Video playback | Video playback | yes | yes | yes | yes | yes | ___Media Capture and Streams API___ | | 
| | System audio player | Access to the system player |  | yes | yes | yes | yes | ___Audio Output Devices API___ | yes |
| | Text to speech | Text to Speech (different languages) | yes | yes |  | yes | yes | ___Web Speech API___ | | 
| | Speech recognition | AI speech recognition | yes | yes |  | yes | yes | ___Web Speech API___ | | 
| | OCR | Extraction of information from images (driving license, ID card, etc.) |  | yes |  | yes | yes |  | | 
| | AI object classification | Object recognition and classification from images |  | yes |  | yes | yes |  | | 
| | Face detection | Detection of faces in images and comparisons |  | yes |  | yes | yes |  | | 
| Platform-specific | Login | Account management | yes | yes | yes | yes | yes | ___FedCM API, Web Authentication API, WebOTP API___ | | 
| | Payments | In-app payments | yes | yes | yes | yes | yes | ___Payment Request, Payment Handlers, SPC___ APIs | | 
| | Tokens, cards | Management of wallet |  |  | yes | yes | yes | ___Digital Credentials API___ | yes |
| | Push notifications | Push notifications server | yes |  |  |  |  | ___Push API___ | | 
| | Ads | Ads management | yes | yes |  | yes | yes |  | | 
| | User credentials management | Storage of credentials in the keychain | yes |  |  |  |  | ___Credential Management API___ | | 
| | Text translation | Translation service | yes |  |  | yes | yes |  | | 
| | RTC conferences | Video/audio conference management |  | yes |  | yes | yes |  | | 
| | Live video | Live video component management |  | yes |  | yes | yes |  | | 
| | Map management | Map markers, scale, etc. | yes | yes | yes | yes | yes |  | | 
| | Route management | Route calculation |  |  | yes |  |  |  | | 
| | Biometric authentication | Management of biometric authentication |  |  |  | yes |  | ___Web Authentication API___ | | 
| | AI inferences | AI inference engine |  |  |  | yes |  | ___Web Neural Network API___ | | 
| | Server time | Get server time |  |  | yes |  |  |  | | 
| App Management | App marketplace management | Offers installation, check if an app is installed, get info and checksums | yes | yes |  |  | yes |  | | 
| | Home screen icon | Install app on home-screen, add widget, and check if installed | yes |  |  |  |  | ___Service Worker API___ | | 
| | Statistics - Analytics | Statistics of usage of the app (clicks, interaction, etc.) | yes | yes |  | yes | yes |  | | 
| | Sub-package management | Control of sub-packages (programmatically) |  |  |  | yes | yes | ___ECMAScript import___ | | 
| | Update manager | Management of app updating |  | yes | yes | yes | yes | ___Server-sent events___ | | 


