# browser
A package providing a simple wrapper around ua-parser-js.

## Basic Usage

This library can be used both in a browser and in a NodeJS environment.

### Browser usage

You can find the user-agent of the current browser by accessing `navigator.userAgent`. Passing this value to the constructor of `Browser` will allow you to use all of the class's convenience methods.

```tsx
import {Browser} from '@bipboys/browser';
const browser = new Browser({userAgent: navigator.userAgent});
document.body.innerHTML = `
  your browser is: ${browser.name} v${browser.version}
  ${browser.isMobile ? 'on a mobile device'}
`;
```

### Node usage

You can find the user-agent of incoming requests by accessing the `user-agent` header. Many web frameworks also provide convenience methods for accessing it.

Passing this value to the constructor of `Browser` will allow you to use all of the class's convenience methods.

```tsx
import Koa from 'koa';
import {Browser} from '@bipboys/browser';
const app = new Koa();
app.use(ctx => {
  const userAgent = ctx.get('user-agent');
  const browser = new Browser({userAgent});
  ctx.body = `
    your browser is: ${browser.name} v${browser.version}
    ${browser.isMobile ? 'on a mobile device'}
  `;
});
```

## API

### The `Browser` class

The primary API of this package is the `Browser` class. This class represents information about an individual browser as gleaned from it's user-agent.

```tsx
import {Browser} from '@bipboys/browser';
const chromeUA =
  'Mozilla/5.0 (Linux; Android 6.0; ALE-L23 Build/HuaweiALE-L23) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Mobile Safari/537.36';
const browser = new Browser({userAgent: chromeUA});
```

The class provides a number of convenience methods and properties for categorizing the browser, detailed below.

#### name

The name of the browser.

```tsx
const chromeUA =
  'Mozilla/5.0 (Linux; Android 6.0; ALE-L23 Build/HuaweiALE-L23) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Mobile Safari/537.36';
const browser = new Browser({userAgent: chromeUA}).name;
=>  'Chrome'
```

#### version

The (semver) version of the browser.

```tsx
const chromeUA =
  'Mozilla/5.0 (Linux; Android 6.0; ALE-L23 Build/HuaweiALE-L23) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Mobile Safari/537.36';
const browser = new Browser({userAgent: chromeUA}).version;
=>  '69.0.3497.100'
```

#### majorVersion

The current major version of the browser.

```tsx
const chromeUA =
  'Mozilla/5.0 (Linux; Android 6.0; ALE-L23 Build/HuaweiALE-L23) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Mobile Safari/537.36';
const browser = new Browser({userAgent: chromeUA}).majorVersion;
=>  '69'
```

#### unknown

Whether the browser is unknown to the parser.

```tsx
const fakeUA = 'totally not real';
const browser = new Browser({userAgent: fakeUA}).unknown;
=>  true
```

#### isMobile

Whether the browser is a mobile browser.

```tsx
const iOSUA = 'Mozilla/5.0 (iPhone; CPU iPhone OS 9_3_5 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13G36 Safari/601.1';
const browser = new Browser({userAgent: iOSUA}).isMobile;
=>  true
```

#### isDesktop

Whether the browser is a desktop (not mobile) browser.

```tsx
const iOSUA = 'Mozilla/5.0 (iPhone; CPU iPhone OS 9_3_5 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13G36 Safari/601.1';
const browser = new Browser({userAgent: iOSUA}).isDesktop;
=>  false
```

#### os

The operating system the browser runs on.

```tsx
const iOSUA = 'Mozilla/5.0 (iPhone; CPU iPhone OS 9_3_5 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13G36 Safari/601.1';
const browser = new Browser({userAgent: iOSUA}).os;
=>  'iOS'
```

#### isWindows

Whether the operating system of the browser is any version of windows.

```tsx
const iOSUA = 'Mozilla/5.0 (iPhone; CPU iPhone OS 9_3_5 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13G36 Safari/601.1';
const browser = new Browser({userAgent: iOSUA}).isWindows;
=>  false
```

#### isMac

Whether the operating system of the browser is any version of macOS.

```tsx
const iOSUA = 'Mozilla/5.0 (iPhone; CPU iPhone OS 9_3_5 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13G36 Safari/601.1';
const browser = new Browser({userAgent: iOSUA}).isMac;
=>  false
```

#### isSafari

Whether the operating system of the browser is any version of macOS.

```tsx
const iOSUA = 'Mozilla/5.0 (iPhone; CPU iPhone OS 9_3_5 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13G36 Safari/601.1';
const browser = new Browser({userAgent: iOSUA}).isMac;
=>  true
```

#### isChrome

Whether the browser is any version of chrome.

```tsx
const chromeUA =
  'Mozilla/5.0 (Linux; Android 6.0; ALE-L23 Build/HuaweiALE-L23) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Mobile Safari/537.36';
const browser = new Browser({userAgent: chromeUA}).isChrome;
=>  true
```

#### isAndroidChrome

Whether the browser is specifically an Android build of Chrome.

```tsx
const chromeUA =
  'Mozilla/5.0 (Linux; Android 6.0; ALE-L23 Build/HuaweiALE-L23) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Mobile Safari/537.36';
const browser = new Browser({userAgent: chromeUA}).majorVersion;
=> true
```

#### isFirefox

Whether the browser is any version of Firefox.

```tsx
const firefoxUA =
  'Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:47.0) Gecko/20100101 Firefox/47.0';
const browser = new Browser({userAgent: firefoxUA}).isFirefox;
=>  true
```

#### isIE

Whether the browser is any version of Internet Explorer.

```tsx
const ieUA =
  'Mozilla/5.0 (compatible; MSIE 9.0; Windows Phone OS 7.5; Trident/5.0; IEMobile/9.0)';
const browser = new Browser({userAgent: ieUA}).isIE;
=>  true
```

#### isEdge

Whether the browser is any version of edge.

```tsx
const edgeUA = 'Mozilla/5.0 (Windows NT 10.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/42.0.2311.135 Safari/537.36 Edge/12.10136';
const browser = new Browser({userAgent: edgeUA}).isEdge;
=>  true
```

#### isNativeApp

Whether the browser is a bipboys Mobile web-view

```tsx
const nativeAppUA = 'bipboys Mobile/iOS/9.3.1';
const browser = new Browser({userAgent: nativeAppUA}).isNativeApp;
=>  true
```

#### asPlainObject()

Returns basic information about the browser as a readily serializable plain object.

```tsx
const userAgent =
  'Mozilla/5.0 (Linux; Android 6.0; ALE-L23 Build/HuaweiALE-L23) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Mobile Safari/537.36';
new Browser({userAgent}).asPlainObject();
=> {
  name: 'Chrome',
  version: '69.0.3497.100',
  isMobile: true,
  isNativeApp: false,
  isDesktop: false,
}
```