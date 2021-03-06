# fx_cast

Very WIP! Not ready for release. Expect many bugs. Please don't sign builds on AMO with current ID.

Credit:
* [electron-chromecast](https://github.com/GPMDP/electron-chromecast)
* [node-castv2](https://github.com/thibauts/node-castv2)
* [chrome-native-messaging](https://github.com/jdiamond/chrome-native-messaging)

## Supported platforms

* Linux
* macOS
* Windows (TODO)

Only tested on Linux and macOS. mDNS library issue to be fixed. `mdns` only works on Windows, `mdns-js` only works on Linux.


## Building

### Requirements

* NodeJS
* `node` binary in path
* ~~Bonjour SDK (Windows)~~

### Instructions

````sh
git clone https://github.com/hensm/caster.git
npm install
npm run build
npm run install-manifest
````

### Testing

Testing requires geckodriver (or chromedriver for Chrome parity testing). See [selenium-webdriver](https://www.npmjs.com/package/selenium-webdriver#installation) installation instructions (ignore `npm install`).

Chrome doesn't load the media router in a temporary selenium profile, so there's a bundled profile (`test/ChromeProfile.zip`). Extract the folder within as `test/ChromeProfile/`.

````sh
npm run build
npm test
SELENIUM_BROWSER=chrome npm test
````


## Usage

Extension can be loaded from `about:debugging` as a temporary extension.

Most sites won't load the cast API unless the browser presents itself as Chrome. The extension includes a method of spoofing the user agent string, sites can be whitelisted via the options page. Whitelist entries are specified as [match patterns](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Match_patterns). To whitelist all sites, add `<all_urls>` to the whitelist, though this could cause breakage on random sites.

HTML5 media elements have a "Cast..." context menu item that triggers a sender application. Only works on remote (non-local) media that isn't DRM-encumbered.

Cast-enabled websites will load the sender API shim and display a cast button as in Chrome, provided there are no bugs/incompatibilities with the shim.


## Video Demos

Netflix / HTML5:

[<img width="200" src="https://img.youtube.com/vi/Ex9dWKYguEE/0.jpg" alt="fx_cast Netflix" />](https://www.youtube.com/watch?v=Ex9dWKYguEE)
[<img width="200" src="https://img.youtube.com/vi/16r8lQKeEX8/0.jpg" alt="fx_cast HTML5" />](https://www.youtube.com/watch?v=16r8lQKeEX8)
