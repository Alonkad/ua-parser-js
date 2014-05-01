# UAParser.js

Lightweight JavaScript-based User-Agent string parser for browsers.
* Forked from : https://github.com/faisalman/ua-parser-js

[![Build Status](https://travis-ci.org/faisalman/ua-parser-js.png?branch=master)](https://travis-ci.org/alonkad/ua-parser-js)

## Features

Extract detailed type of web browser, layout engine, operating system, and device purely from user-agent string with relatively lightweight footprint. Written in vanilla js, which means it doesn't depends on any other library.


## Methods

* `getBrowser()`
    * returns `{ name: '', major: '', version: '' }`

```
# Possible 'browser.name':
Amaya, Arora, Avant, Baidu, Blazer, Bolt, Camino, Chimera, Chrome, Chromium, 
Comodo Dragon, Conkeror, Dillo, Dolphin, Doris, Epiphany, Fennec, Firebird, 
Firefox, Flock, GoBrowser, iCab, ICE Browser, IceApe, IceCat, IceDragon, 
Iceweasel, IE [Mobile], Iron, Jasmine, K-Meleon, Konqueror, Kindle, Links, 
Lunascape, Lynx, Maemo, Maxthon, Midori, Minimo, [Mobile] Safari, Mosaic, Mozilla, 
Netfront, Netscape, NetSurf, Nokia, OmniWeb, Opera [Mini/Mobi/Tablet], Phoenix, 
Polaris, QQBrowser, RockMelt, Silk, Skyfire, SeaMonkey, SlimBrowser, Swiftfox, 
Tizen, UCBrowser, w3m, Yandex

# 'browser.version' & 'browser.major' determined dynamically
```

* `getDevice()`
    * returns `{ model: '', type: '', vendor: '' }` 

```
# Possible 'device.type':
console, mobile, tablet

# Possible 'device.vendor':
Acer, Alcatel, Apple, Asus, BenQ, BlackBerry, Dell, GeeksPhone, HP, HTC, Huawei, 
Lenovo, LG, Meizu, Motorola, Nexian, Nintendo, Nokia, Palm, Panasonic, 
RIM, Samsung, Siemens, Sony-Ericsson, Sprint, ZTE

# 'device.model' determined dynamically
```

* `getEngine()`
    * returns `{ name: '', version: '' }`

```
# Possible 'engine.name'
Amaya, Gecko, iCab, KHTML, Links, Lynx, NetFront, NetSurf, Presto, Tasman, 
Trident, w3m, WebKit

# 'engine.version' determined dynamically
```

* `getOS()`
    * returns `{ name: '', version: '' }`

```
# Possible 'os.name'
AIX, Amiga OS, Android, Arch, Bada, BeOS, BlackBerry, CentOS, Chromium OS, 
Fedora, Firefox OS, FreeBSD, Debian, DragonFly, Gentoo, GNU, Haiku, Hurd, iOS, 
Joli, Linux, Mac OS, Mandriva, MeeGo, Minix, Mint, Morph OS, NetBSD, Nintendo, 
OpenBSD, OS/2, Palm, PCLinuxOS, Plan9, Playstation, QNX, RedHat, RIM Tablet OS, 
RISC OS, Slackware, Solaris, SUSE, Symbian, Tizen, Ubuntu, UNIX, WebOS, 
Windows [Phone/Mobile], Zenwalk

# 'os.version' determined dynamically
```

* `getResult()`
    * returns `{ ua: '', browser: {}, device: {}, engine: {}, os: {} }`

## Example

```html
<!doctype html>
<html>
<head>
<script type="text/javascript" src="ua-parser.min.js"></script>
<script type="text/javascript">

	var parser = new UAParser();

    // by default it takes ua string from current browser's window.navigator.userAgent
    console.log(parser.getResult());
    /*
        /// this will print an object structured like this:
        {
            ua: "",
            browser: {
                name: "",
                version: "",
                major: ""
            },
            engine: {
                name: "",
                version: ""
            },
            os: {
                name: "",
                version: ""
            },
            device: {
                model: "",
                type: "",
                vendor: ""
            }
        }
    */

    // let's test a custom user-agent string as an example
    var uastring = "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/535.2 (KHTML, like Gecko) Ubuntu/11.10 Chromium/15.0.874.106 Chrome/15.0.874.106 Safari/535.2";
    parser.setUA(uastring);

    var result = parser.getResult();
    // this will also produce the same result (without instantiation):
    // var result = UAParser(uastring);

    console.log(result.browser);        // {name: "Chromium", major: "15", version: "15.0.874.106"}
    console.log(result.device);         // {model: undefined, type: undefined, vendor: undefined}
    console.log(result.os);             // {name: "Ubuntu", version: "11.10"}
    console.log(result.os.version);     // "11.10"
    console.log(result.engine.name);    // "WebKit"

    // do some other tests
    var uastring2 = "Mozilla/5.0 (compatible; Konqueror/4.1; OpenBSD) KHTML/4.1.4 (like Gecko)";
    console.log(parser.setUA(uastring2).getBrowser().name); // "Konqueror"
    console.log(parser.getOS());                            // {name: "OpenBSD", version: undefined}
    console.log(parser.getEngine());                        // {name: "KHTML", version: "4.1.4"}

    var uastring3 = 'Mozilla/5.0 (PlayBook; U; RIM Tablet OS 1.0.0; en-US) AppleWebKit/534.11 (KHTML, like Gecko) Version/7.1.0.7 Safari/534.11';
    console.log(parser.setUA(uastring3).getDevice().model); // "PlayBook"
    console.log(parser.getOS())                             // {name: "RIM Tablet OS", version: "1.0.0"}
    console.log(parser.getBrowser().name);                  // "Safari"

</script>
</head>
<body>
</body>
</html>
```
