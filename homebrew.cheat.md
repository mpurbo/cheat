# [Homebrew](http://brew.sh/) and [Cask](http://caskroom.io/) Cheat Sheet

## Homebrew Commands

Command|Description
-------|----------------
`brew install $FORMULA` | Install formula with name `$FORMULA`.
`brew install --HEAD $FORMULA` | Install the HEAD of formula with name `$FORMULA`.
`brew install --force --HEAD $FORMULA` | Install the HEAD new version of formula with name `$FORMULA`.
`brew search` | List all installable formulae.
`brew search $FORMULA_SUBSTR` | List all installable formulae containing `$FORMULA_SUBSTR` in the name.
`brew search /$FORMULA_REGEX/` | List all installable formulae with `$FORMULA_REGEX` name regular expression.
`brew list` | List all installed formulae.
`brew list $FORMULA` | List all files in an installed formulae named `$FORMULA`.
`brew info` | Display installed formulae summary.
`brew info $FORMULA` | Display `$FORMULA` formula detailed information.
`brew info --github $FORMULA` | Open `$FORMULA` formula's GitHub on the browser.
`brew home` | Display Homebrew home page on the browser.
`brew home $FORMULA` | Display `$FORMULA` formula's home page on the browser.
`brew update` | Update Homebrew and formulae.
`brew outdated` | List outdated formulae.
`brew upgrade` | Upgrade all outdated formulae.
`brew upgrade $FORMULA` | Upgrade `$FORMULA` formula.
`brew pin $FORMULA` | Stop `$FORMULA` formula from being upgraded/updated.
`brew unpin $FORMULA` | Allow `$FORMULA` formula to be upgraded/updated.
`brew cleanup $FORMULA` | Uninstall old versions of `$FORMULA` formula.
`brew cleanup` | Uninstall all old versions.
`brew cleanup -n` | List all old versions that can be uninstalled by using `cleanup`.
`brew uninstall $FORMULA --force` | Uninstall `$FORMULA` formula.

Source:
- [Homebrewの導入と使い方](http://tech.caph.jp/2011/04/06/homebrew%E3%81%AE%E5%B0%8E%E5%85%A5%E3%81%A8%E4%BD%BF%E3%81%84%E6%96%B9/)
- [Official FAQ](https://github.com/Homebrew/homebrew/blob/master/share/doc/homebrew/FAQ.md)
