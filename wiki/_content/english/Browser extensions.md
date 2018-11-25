Related articles

*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")

This article lists some [browser extensions](https://en.wikipedia.org/wiki/Browser_extension "wikipedia:Browser extension") available for [Firefox](/index.php/Firefox "Firefox") and/or [Chromium](/index.php/Chromium "Chromium").

## Contents

*   [1 Installation](#Installation)
*   [2 Privacy](#Privacy)
    *   [2.1 Content blockers](#Content_blockers)
    *   [2.2 Advanced control](#Advanced_control)
    *   [2.3 Automatic tracker blockers](#Automatic_tracker_blockers)
    *   [2.4 Noise generators](#Noise_generators)
    *   [2.5 Miscellaneous](#Miscellaneous)
*   [3 Website customization](#Website_customization)
*   [4 Keyboard shortcuts](#Keyboard_shortcuts)
*   [5 Edit text with external text editor](#Edit_text_with_external_text_editor)

## Installation

Firefox extensions can be installed from [addons.mozilla.org](https://addons.mozilla.org/firefox/) and managed at `about:addons`.

Chrome extensions can be installed from the [Chrome Web Store](https://chrome.google.com/webstore/category/extensions) and managed at `chrome://extensions/`.

Additionally a few Firefox extensions can be found in the [the official repositories](https://www.archlinux.org/packages/?q=firefox-extension) and some more in the [AUR](https://aur.archlinux.org/packages/?K=firefox-extension).

To simplify maintenance this article does not link store pages or [AUR](/index.php/AUR "AUR") packages of extensions. Readers are advised to obtain extensions through the linked official websites if no package is available.

## Privacy

See also [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy") and [Chromium/Tips and tricks#Security](/index.php/Chromium/Tips_and_tricks#Security "Chromium/Tips and tricks").

**Tip:** It is not recommended to install all the privacy extensions. It can be counterproductive as they conflict with each other and does not increase security whatsoever.

### Content blockers

*   **[uBlock Origin](https://en.wikipedia.org/wiki/uBlock_Origin "wikipedia:uBlock Origin")** — A lightweight, efficient blocker which is easy on [memory and CPU](https://github.com/gorhill/uBlock#performance). It comes with several filter lists ready to use out-of-the-box (including EasyList, Peter Lowe's, several malware filter lists). The lead developer of uBlock forked the project and created uBlock Origin. As of July 2015, most of the development is being done on uBlock Origin and the codebases are deviating substantially.

	[https://github.com/gorhill/uBlock/](https://github.com/gorhill/uBlock/) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **[Adblock Plus](https://en.wikipedia.org/wiki/Adblock_Plus "wikipedia:Adblock Plus")** — Was a popular extension to block ads. Now that it is not blocking some ads on purpose [[1]](https://adblockplus.org/acceptable-ads), it may be a better idea to use a different blocker like uBlock Origin.

	[https://adblockplus.org/](https://adblockplus.org/) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

### Advanced control

*   **uMatrix** — Fork of HTTP Switchboard. Lets you selectively block Javascript, plugins or other resources and control third-party resources. It also features extensive privacy features like user-agent masquerading, referering blocking and so on. It effectively replaces NoScript and RequestPolicy. See the [old HTTP Switchboard wiki](https://github.com/gorhill/httpswitchboard/wiki/How-to-use-HTTP-Switchboard:-Two-opposing-views) for different ways how to use it.

	[https://github.com/gorhill/uMatrix](https://github.com/gorhill/uMatrix) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **ScriptSafe** — Gives users control of the web and more secure browsing while emphasizing simplicity and intuitiveness. Due to the nature of this extension, this will break most sites! It is designed to learn over time with sites that you allow.

	[https://github.com/andryou/scriptsafe](https://github.com/andryou/scriptsafe) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **NoScript** — Disables JavaScript and Flash on any website not specifically whitelisted by the user. This extension will protect you from exploitation of security vulnerabilities by not letting anything but trusted sites (e.g: your bank, webmail) serve you executable content. Once installed you can configure settings for NoScript by either clicking its icon on the toolbar or right clicking a page and navigating to NoScript. You will then have the option to enable/disable scripts for the current page, as well as any third party scripts that the page is linking to. Alternatively you can choose to enable scripts temporarily for that session only. Be aware a lot of modern websites use scripts for layout purposes, hence content may look different. For example, failed rendering due to missing fonts might occur on websites that load fonts at runtime via scripts, which were blocked by NoScript.

	[http://noscript.net/](http://noscript.net/) || [Firefox](/index.php/Firefox "Firefox")

*   **ScriptBlock** — Similar to NoScript, which is a Firefox add-on. Both extensions stop a website from executing any kind of JavaScript. However, ScriptBlock is a much simpler design thus it's easier to use. It blocks JavaScript by default. You can allow and temporary allow JavaScripts. Once you allow them to run, it lets all the JavaScripts run on that page so you might want ScriptBlock to work in conjunction with [Privacy Badger](#Automatic_tracker_blockers). It's also worth checking it's default whitelist, which might be permissive to you.

	[https://github.com/compvid30/scriptblock](https://github.com/compvid30/scriptblock) || [Chromium](/index.php/Chromium "Chromium")

*   **Cookie AutoDelete** — Deletes cookies as soon as the tab closes. Supports automatic and manual cookie cleaning modes. (Support for clearing LocalStorage was added in version 2.1, but only for Firefox versions 58+. The same release added support for first party isolation, but only for Firefox versions 59+).

	[https://github.com/Cookie-AutoDelete/Cookie-AutoDelete](https://github.com/Cookie-AutoDelete/Cookie-AutoDelete) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **Vanilla Cookie Manager** — A cookie whitelist manager that automatically removes unwanted cookies. Cookies can be used for authentication, storing your site preferences or anything else that can be saved as text data. Unfortunately they can also be used to track you. You could turn off cookies completely or just shut off third-party cookies. But that would also keep out useful cookies that many web apps rely upon to work (like Google Mail or Calendar). With Vanilla you can select which cookies you want to keep on a whitelist. All unwanted cookies are deleted automatically (or manually if you prefer).

	[https://github.com/laktak/vanilla-chrome](https://github.com/laktak/vanilla-chrome) || [Chromium](/index.php/Chromium "Chromium")

### Automatic tracker blockers

*   **Privacy Badger** — Monitors third-party trackers loaded with web content. It blocks trackers once they appear on different sites. It does not block advertisements in the first place, but since a lot of ads are served based on tracking information these are blocked as well. For more information on the mechanism, see its [FAQ](https://www.eff.org/privacybadger#faq-How-is-Privacy-Badger-different-to-Disconnect,-Adblock-Plus,-Ghostery,-and-other-blocking-extensions?).

	[https://www.eff.org/privacybadger](https://www.eff.org/privacybadger) || [firefox-extension-privacybadger](https://www.archlinux.org/packages/?name=firefox-extension-privacybadger), [Chromium](/index.php/Chromium "Chromium")

*   **Disconnect** — Aims to stop 2,000 third-party sites from tracking the user. It encrypts data sent to popular sites and claims to loads web pages 27 percent faster. Disconnect shows its users, in real time, how many tracking attempts from Google, Twitter, Facebook, and more are stopped. It categorizes tracking attempts into advertising, analytical, social, and content, which makes it easy to monitor how one is being tracked. Disconnect can also stop side-jacking, which utilizes stolen cookies to steal personal data. It is easy to use and well supported. Firefox gained a feature based on the Disconnect list, see [Firefox/Privacy#Tracking protection](/index.php/Firefox/Privacy#Tracking_protection "Firefox/Privacy").

	[https://disconnect.me/](https://disconnect.me/) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

### Noise generators

*   **AdNauseam** — A lightweight browser extension that blends software tool and artware intervention to fight back against tracking by advertising networks. AdNauseam works like an ad-blocker (it is built atop uBlock-Origin) to silently simulate clicks on each blocked ad, confusing trackers as to one's real interests.

	[https://adnauseam.io/](https://adnauseam.io/) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **TrackMeNot** — Periodically issues randomized search-queries to popular search engines and helps you hide your real ones in a cloud of 'ghost' queries.

	[https://cs.nyu.edu/trackmenot/](https://cs.nyu.edu/trackmenot/) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

### Miscellaneous

*   **HTTPS Everywhere** — Encrypts your communication with a website. It forces a connection over HTTPS instead of HTTP wherever possible. HTTPS Everywhere will be automatically configured and enabled upon restarting Firefox. For information on how to set up your own rules for different websites please visit [the official website](https://www.eff.org/https-everywhere/rulesets). HTTPS Everywhere does not magically enable HTTPS for every site on the internet. The site needs to support HTTPS and HTTPS Everywhere should have a ruleset configured for that site.

	[https://www.eff.org/https-everywhere](https://www.eff.org/https-everywhere) || [firefox-extension-https-everywhere](https://www.archlinux.org/packages/?name=firefox-extension-https-everywhere), [Chromium](/index.php/Chromium "Chromium")

*   **Decentraleyes** — Protects you against tracking through "free", centralized, content delivery. It prevents a lot of requests from reaching networks like Google Hosted Libraries, and serves local files to keep sites from breaking. Complements regular content blockers.

	[https://decentraleyes.org/](https://decentraleyes.org/) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **CanvasBlocker** — Blocks or fakes the JS-API for modifying <canvas> to prevent Canvas-Fingerprinting. Firefox has a built-in anti-fingerprinting feature that can be enabled by setting `privacy.resistFingerprinting` to `true` in `about:config`.

	[https://github.com/kkapsner/CanvasBlocker/](https://github.com/kkapsner/CanvasBlocker/) || [Firefox](/index.php/Firefox "Firefox")

*   **Privacy Settings** — Provides a toolbar panel for easily altering the browser's built-in privacy settings.

	[https://add0n.com/privacy-settings.html](https://add0n.com/privacy-settings.html) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

## Website customization

Websites can be augmented using user style sheets and JavaScript [userscripts](https://en.wikipedia.org/wiki/userscript "wikipedia:userscript").

*   **Stylus** — User style sheets manager, fork of defunct [Stylish](https://en.wikipedia.org/wiki/Stylish "wikipedia:Stylish").

	[https://add0n.com/stylus.html](https://add0n.com/stylus.html) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **Violentmonkey** — Open source userscript manager.

	[https://violentmonkey.github.io/](https://violentmonkey.github.io/) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **Tampermonkey** — Proprietary userscript manager.

	[https://tampermonkey.net/](https://tampermonkey.net/) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

## Keyboard shortcuts

There are various extensions providing [vi](/index.php/Vi "Vi")-style keyboard shortcuts.

*   **Vimium** — Allows mouse-less browsing, has an experimental Firefox version.

	[https://github.com/philc/vimium](https://github.com/philc/vimium) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **Saka Key** — Allows mouse-less browsing, focused on accessibility.

	[https://key.saka.io/](https://key.saka.io/) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **wasavi** — Can transform textareas into Vi editors.

	[https://github.com/akahuku/wasavi](https://github.com/akahuku/wasavi) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

## Edit text with external text editor

Extensions to edit <textarea>s with native [text editors](/index.php/Text_editor "Text editor"):

*   **Textern** — Add-on for editing text in your favorite external editor, requires [Python](/index.php/Python "Python") script, available as [firefox-extension-textern-native-git](https://aur.archlinux.org/packages/firefox-extension-textern-native-git/).

	[https://github.com/jlebon/textern](https://github.com/jlebon/textern) || [Firefox](/index.php/Firefox "Firefox")

*   **withExEditor** — View source, selection, and edit text with the external editor, requires [Node.js](/index.php/Node.js "Node.js").

	[https://github.com/asamuzaK/withExEditor](https://github.com/asamuzaK/withExEditor) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")

*   **GhostText** — Use your text editor to write in your browser. Everything you type in the editor will be instantly updated in the browser (and vice versa). Has plugins for [Vim](/index.php/Vim "Vim"), [Emacs](/index.php/Emacs "Emacs"), [Neovim](/index.php/Neovim "Neovim"), [Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code") and [Atom](/index.php/Atom "Atom").

	[https://github.com/GhostText/GhostText](https://github.com/GhostText/GhostText) || [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium")