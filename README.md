<div align="center">
  <img width="100px" src="https://maccy.app/img/maccy/Logo.svg" alt="Logo" />
  <h1>
    <a href="https://maccy.app/">Maccy</a>
  </h1>
</div>

Maccy is a lightweight clipboard manager for macOS. It keeps the history of what you copy
and lets you quickly navigate, search, and use previous clipboard contents.

<!-- vim-markdown-toc GFM -->

* [Features](#features)
* [Install](#install)
* [Usage](#usage)
* [Customization](#customization)
  * [Automatically Start at Login](#automatically-start-at-login)
  * [Change Default Settings](#change-default-settings)
    * [Popup Hotkey](#popup-hotkey)
    * [History Size](#history-size)
    * [Show/Hide Icon in Status Bar](#showhide-icon-in-status-bar)
    * [Automatically Paste by Default](#automatically-paste-by-default)
    * [Enable/Disable Fuzzy Search](#enabledisable-fuzzy-search)
    * [Ignore Copied Items](#ignore-copied-items)
    * [Show/Hide Search](#showhide-search)
    * [Show/Hide Title](#showhide-title)
    * [Popup Position](#popup-position)
    * [Sorting](#sorting)
    * [Max Image Height](#max-image-height)
    * [Ignore Custom Copy Types](#ignore-custom-copy-types)
* [Update](#update)
* [Why Yet Another Clipboard Manager](#why-yet-another-clipboard-manager)
* [CI](#ci)
* [License](#license)

<!-- vim-markdown-toc -->

## Features

* Lightweight and fast
* Keyboard-first
* Secure and private
* Native UI
* Open source and free

## Install

Download the latest version from the [releases](https://github.com/p0deje/Maccy/releases/latest) page, or use [Homebrew](https://brew.sh/):

```sh
brew cask install maccy
```

## Usage

1. <kbd>COMMAND (⌘)</kbd> + <kbd>SHIFT (⇧)</kbd> + <kbd>C</kbd> to popup Maccy or click on its icon in the menu bar.
2. Type what you want to find.
3. To select the history item you wish to copy, press <kbd>ENTER</kbd>, or click the item, or use <kbd>COMMAND (⌘)</kbd> + `n` shortcut.
4. To choose the history item and paste, press <kbd>OPTION (⌥)</kbd> + <kbd>ENTER</kbd>, or <kbd>OPTION (⌥)</kbd> + <kbd>CLICK</kbd> the item, or use <kbd>OPTION (⌥)</kbd> + `n` shortcut.
5. To delete the history item, press <kbd>OPTION (⌥)</kbd> + <kbd>DELETE (⌫)</kbd>.
6. To see the full text of the history item, wait a couple of seconds for tooltip.
7. To pin the history item so that it remains on top of the list, press <kbd>OPTION (⌥)</kbd> + <kbd>P</kbd>. The item will be moved to the top with a random but permanent keyboard shortcut. To unpin it, press <kbd>OPTION (⌥)</kbd> + <kbd>P</kbd> again.
8. To clear all unpineed items, select _Clear_ in the menu. To clear all items including pinned, select _Clear_ in the menu with  <kbd>OPTION (⌥)</kbd> pressed.

## Customization

### Automatically Start at Login

Select the "Launch at login" option or add Maccy to your "Login items".

### Change Default Settings

To change default settings, use the following commands in Terminal.

#### Popup Hotkey

```sh
defaults write org.p0deje.Maccy hotKey control+option+m # default is command+shift+c
```

#### History Size

```sh
defaults write org.p0deje.Maccy historySize 100 # default is 200
```

#### Show/Hide Icon in Status Bar

To hide you can simply drag the icon away from the status bar with <kbd>COMMAND (⌘)</kbd> pressed.
To recover the icon, re-open Maccy while it's already running.

You can also control visibility using configuration:

```sh
defaults write org.p0deje.Maccy showInStatusBar false # default is true
```

> Don't forget to restart Maccy after using `defaults` command!


#### Automatically Paste by Default

Select and paste in one go.

```sh
defaults write org.p0deje.Maccy pasteByDefault true # default is false
```

#### Enable/Disable Fuzzy Search

```sh
defaults write org.p0deje.Maccy fuzzySearch true # default is false
```

> Note that enabling fuzzy search will slow down when searching through the long history items list (200+).

#### Ignore Copied Items

You can tell Maccy to ignore all copied items:

```sh
defaults write org.p0deje.Maccy ignoreEvents true # default is false
```

This is useful if you have some workflow for copying sensitive data. You can set `ignoreEvents` to true, copy the data and set `ignoreEvents` back to false.

#### Show/Hide Search

```sh
defaults write org.p0deje.Maccy hideSearch true # default is false
```

#### Show/Hide Title

```sh
defaults write org.p0deje.Maccy hideTitle true # default is false
```

#### Popup Position

By default Maccy will popup at cursor position. You can change it to be always centered on the screen.

```sh
defaults write org.p0deje.Maccy popupPosition center # default is cursor
```

You can also change it to popup at location of icon in status bar:

```sh
defaults write org.p0deje.Maccy popupPosition statusItem
```

#### Sorting

By default Maccy will sort the history by the date of the last time item was copied.

```sh
defaults write org.p0deje.Maccy sortBy lastCopiedAt # default
```

You can change the sorting algorithm so that it sorts by the first time item was copied:

```sh
defaults write org.p0deje.Maccy sortBy firstCopiedAt
```

You can also change the sorting algorithm so that it sorts by the total number item was copied:

```sh
defaults write org.p0deje.Maccy sortBy numberOfCopies
```

#### Max Image Height

```sh
defaults write org.p0deje.Maccy imageMaxHeight 100 # default is 40
```

#### Ignore Custom Copy Types

By default Maccy will ignore certain copy types that are considered to be confidential
or temporary. The default list always include the following types:

* `org.nspasteboard.TransientType`
* `org.nspasteboard.ConcealedType`
* `org.nspasteboard.AutoGeneratedType`

Also, default configuration includes the following types but they can be removed
or overwritten:

* `com.agilebits.onepassword`
* `com.typeit4me.clipping`
* `de.petermaurer.TransientPasteboardType`
* `Pasteboard generator type`

You can add additional custom types:

```sh
defaults write org.p0deje.Maccy ignoredPasteboardTypes -array-add "com.myapp.CustomType"
```

If you accidentally removed default types, you can restore the original configuration:

```sh
defaults write org.p0deje.Maccy ignoredPasteboardTypes -array "de.petermaurer.TransientPasteboardType" "com.typeit4me.clipping" "Pasteboard generator type" "com.agilebits.onepassword"
```

## Update

Download and reinstall the latest version from the [releases](https://github.com/p0deje/Maccy/releases/latest) page, or use [Homebrew](https://brew.sh/):

```sh
brew cask upgrade maccy
open -a Maccy
```

## Why Yet Another Clipboard Manager

There are dozens of similar applications out there, so why build another?
Over the past years since I moved from Linux to macOS, I struggled to find
a clipboard manager that is as free and simple as [Parcellite](http://parcellite.sourceforge.net),
but I couldn't. So I've decided to build one.

Also, I wanted to learn Swift and get acquainted with macOS application development.

## CI

[![Build Status](https://app.bitrise.io/app/716921b669780314/status.svg?token=3pMiCb5dpFzlO-7jTYtO3Q&branch=master)](https://app.bitrise.io/app/716921b669780314)

## License

[MIT](./LICENSE)
