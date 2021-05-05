# Sublime-Alan

![Package Status][Package badge]&nbsp;
[![Alan Version][Alan badge]][Alan SDK]&nbsp;
[![Sublime Text Version][ST3 badge]][ST3 link]&nbsp;
[![MIT License][License badge]][LICENSE]&nbsp;
[![Build Status][Travis badge]][Travis link]


Alan IF 3 syntax for Sublime Text 3.

- https://github.com/tajmone/sublime-alan

> __ALPHA STAGE__ — This project is still a WIP Alpha version! Most features are still experimental and subject to continuos changes. Screenshots and descriptions might not always accurately represent the latest changes.

The following document isn't always updated to cover all the added features, it's mainly intended to illustrate the project goals; for a full list of current features, see the [CHANGELOG].

-----

**Table of Contents**

<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="only_ascii" uri_encoding="true" levels="1,2,3" -->

- [About](#about)
- [Features](#features)
    - [Syntax Highlighting](#syntax-highlighting)
        - [Ligatures Support](#ligatures-support)
    - [Color Schemes](#color-schemes)
    - [Goto Symbols](#goto-symbols)
    - [Build Systems](#build-systems)
    - [Autocompletions](#autocompletions)
    - [Snippets](#snippets)
        - [New Adventure Boilerplate](#new-adventure-boilerplate)
    - [Transcipt and Solution Syntaxes](#transcipt-and-solution-syntaxes)
        - [Alan Solution Files Syntax](#alan-solution-files-syntax)
        - [Alan Transcript Files Syntax](#alan-transcript-files-syntax)
- [Requirements](#requirements)
- [Installation](#installation)
- [License](#license)
- [Acknowledgements](#acknowledgements)
- [Links](#links)

<!-- /MarkdownTOC -->

-----

# About

I've created this Alan 3 syntax package just to add some support for Alan source files in Sublime Text, for my own personal use. I haven't really planned to make this a finished product to share on Package Control. Nevertheless, I've decided to share it publicly — just in case it might be useful to others too, or in the remote chance that someone else will join in the project and give me a hand to flesh it out.

I'll be polishing the sytnax and adding features as needs arise, and try to document changes. As a guideline, I'll be pushing to `master` only tested features, so you should be safe keeping the package synced to `master` branch.

# Features

A brief presentation of the features so far implemented.

## Syntax Highlighting

Although the Alan syntax isn't yet fully implemented, it's already mature enough to provide some decent syntax highlighting.

I still need to implement semantic scoping of syntax elements, so that proper indexing can be achieved (Goto functionality, etc.).

For more info on the roadmap and wishlist, see:

- [`TODO.md`][TODO]
- [`CHANGELOG.md`][CHANGELOG]
- [`WORK_NOTES.md`][WORK_NOTES]

The package also ships with additional syntax definitions and color schemes for:

- Compiler log in the the [Build Systems]
- [__Alan Solution__ files] (aka "commands scripts").
- [__Alan Transcript__ files].

### Ligatures Support

Alan syntax has been optimized to enable support of code ligatures. The following Alan operators and keywords are converted to ligatures (if enabled and if font supports them):

| token | ligature |              syntax element              |
|-------|----------|------------------------------------------|
| `>=`  | `⩾`      | Greater or equal operator                |
| `<=`  | `⩽`      | Less or equal operator                   |
| `==`  | `⩵`      | String identity operator                 |
| `=>`  | `⇒`      | Alternative syntax for `THEN` (in Rules) |

Furthermore, the syntax also treats `-->` as a comment delimiter, in order to support _long rightward arrow_ ligature (`⟶`) substitution of the delimiter (_experimental feature_):

![Screenshot of ligatures][Screenshot Ligatures]

Not all code fonts implement in the same way ligatures for `=>`, `<=`, `>=` and `=<`, depending on which of those are treated as comparison operators and which as arrows (some fonts, like [Fixedsys Excelsior], are available in dual choice). This is a crucial point for rendering correctly Alan's operators in ligatures.

The following code-ligatures fonts have been tested with __Sublime Alan__:

|          |      font name       |                comments               |
|----------|----------------------|---------------------------------------|
| &#x2713; | [Fira Code]          | Highly recommended.                   |
| &#x2713; | [Iosevka]            | Works fine.                           |
| &#x2713; | [DejaVu Sans Code]   | Works fine.                           |
| &#x2713; | [Fixedsys Excelsior] | Must use the "Default" version!       |
| &#x2717; | [Monoid]             | No. Doesn't support "`==`"            |
| &#x2717; | [Hasklig]            | No. Doesn't support "`<=`" and "`>=`" |


[Fira Code]: https://github.com/tonsky/FiraCode
[Hasklig]: https://github.com/i-tu/Hasklig
[Monoid]: https://github.com/larsenwork/monoid
[Fixedsys Excelsior]: https://github.com/kika/fixedsys
[Iosevka]: https://github.com/be5invis/Iosevka
[DejaVu Sans Code]: https://github.com/SSNikolaevich/DejaVuSansCode

To disable ligatures for the Alan syntax, open/create your User settings file for Alan syntax and add `"no_calt"` to the `"font_options"` option:

```json
{
    "font_options":
    [
        "no_calt",
    ],
}
```



## Color Schemes

Sublime-Alan ships with the "__Alan DarkFluo__" color scheme:

![Screenshot of Alan DarkFluo color scheme][Screenshot Alan DarkFluo]

This color scheme is still pretty much work-in-progress. The goal is to provide a palette which doesn't strain the eyes, and where the prose parts of the Alan source stand out from the rest of the code, allowing to easily switch focus between the adventure text and its code.

## Goto Symbols

Amongst the goals of this package is that of providing good indexing functionality of Alan language's symbols in order to maximize Sublime Text's Goto Symbol functionality.

Currently, the following syntax elements are captured and indexed:

- Class declaration identifiers.
- Instance declaration identifiers.

Quoted identifiers are transformed before indexing: the delimiting quotes are removed, and any escaped single quotes inside the identifier are replaced with one single quote (eg: `'Tom''s Cat'` is indexed as `Tom's Cat`). This is intended to facilitate looking up identifiers in Goto Symbol functionality, by representing them sa they are seen in the Alan adventure world.

## Build Systems

The build system allows compiling alan source files directly from within th editor (<kbd>Ctrl</kbd><kbd>B</kbd>). Errors reported by Alan compiler will be overimposed in the sourcecode panel, and the user can navigate through the results via <kbd>F4</kbd> and <kbd>Ctrl</kbd><kbd>F4</kbd>:

![Screenshot of Build system errors navigation in the editor][Screenshot Build Editor]

The full error log from the compiler will also be shown in Sublime Text's console. This package syntax highlights the error log to improve visual navigations of the different error types and messages:

![Screenshot of Build system errors report in Sublime Text console][Screenshot Build Console]

Currently there is only one build system, which compiles the current editor's alan source file  ("`*.alan`" files only) without extra options (except `-cc`, to allow capturing error reports). Additional Build systems will be added soon.

> __NOTE__ — Build functionality requires Alan binary compiler to be available on the system PATH.

## Autocompletions

I'm working on autocompletions to provide a fast coding experience thanks to contextual suggestions.

> __NOTE__ — I haven't yet found the time to list main completions in this document. For a detailed and always up-to-date overview of the available completions, see the contents of `completions/` folder.


## Snippets

Sublime-Alan ships with some useful snippets to simplify writing your adventures.

|        trigger        |           description            |
|-----------------------|----------------------------------|
| "`h1`"+<kbd>Tab</kbd> | Commented Heading 1 Frame        |
| "`h2`"+<kbd>Tab</kbd> | Commented Heading 2 Frame        |
| "`h3`"+<kbd>Tab</kbd> | Commented Heading 3 Frame        |
| "`h4`"+<kbd>Tab</kbd> | Commented Heading 4 Frame        |
| "`h5`"+<kbd>Tab</kbd> | Commented Heading 5 Frame        |
| "`h6`"+<kbd>Tab</kbd> | Commented Heading 6 (underlined) |


### New Adventure Boilerplate

The New Adventure Boilerplate snippet provides a quick template for starting a new adventure using Alan Standard Library v2.1:

By typing "`newadv`"+<kbd>Tab</kbd> inside an Alan source file, you'll get:


![Screenshot of "New Adventure Boilerplate" snippet in action][Screenshot Snippet New Adv]

The snippet provides some presets and placeholder values, you can then edit each field and/or skip to the next one via the <kbd>Tab</kbd> key.

#### Custom Variables Support

The `newadv` snippets also supports custom environment variables as default values for some of its fields:

![Screenshot of "New Adventure Boilerplate" snippet using custom variables][Screenshot Snippet New Adv Vars]

The supported variables are:

- `ALAN_AUTHOR`

When this environment variable is defined, its value will automatically be used to fill the `author` field.

To define these environment variables, create a "`Alan Env Vars.tmPreferences`" file (the actual filename doesn't really matter, only the extension) in "`Packages/User/`", and define them like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>name</key>
    <string>Custom Alan env vars</string>
    <key>scope</key>
    <string>source.alan</string>
    <key>settings</key>
    <dict>
        <key>shellVariables</key>
        <array>
            <dict>
                <key>name</key>
                <string>ALAN_AUTHOR</string>
                <key>value</key>
                <string>Tristano Ajmone</string>
            </dict>
        </array>
    </dict>
</dict>
</plist>
```

After creating this file, the `newadv` snippet will automatically fill-in the `author` field with your custom variable:

```alan

--==============================================================================
-- "Game Title" by Tristano Ajmone, 2018.
--==============================================================================
IMPORT 'library.i'. -- ALAN Standard Library v2.1


THE my_game ISA DEFINITION_BLOCK

  HAS title    "Game Title".
  HAS subtitle "".
  HAS author   "Tristano Ajmone".
  HAS year     2018.
  HAS version  "1".

END THE.


THE start_loc ISA LOCATION

END THE start_loc.


Start at start_loc.
DESCRIBE banner.

```


## Transcipt and Solution Syntaxes

This package also provides additional syntax definitions for Alan game transcripts and solution files:

- [__Alan Solution__ files]: `*.a3s` and `*.a3sol`.
- [__Alan Transcript__ files]: `*.a3t` and `*.a3log`.

The alternative `.a3sol` and `.a3log` extensions were arbitrarily invented and introduced by this package, long before Alan adopted their new official counterparts `.a3s` and `.a3t`, respectively (See [alan-if/alan#2]).
The package currently supports both new (official) and old (arbitrary) extensions because there are various projects still using the older extensions, so we want to provide a grace period to allow them to migrate to the new official extensions, before deprecating them.

The purpose of these syntaxes is to simplify handling of game transcript and solution files by settings Sublime Text to handle these files with ISO-8859-1 encoding, as well as providing some minimal syntax highlighting and allowing the user to associate custom color schemes to them.
Without a basic syntax definition, and its encoding settings, Sublime Text would default to UTF-8 encoding, which would cause lots of problems and errors if the solution file contains special characters (like accented letters), and would not display correctly transcripts containing special chars.

Hopefully, these two extra syntaxes will simplify creating and using command scripts to test adventures during the authoring stage, and to correctly visualize game transcripts (i.e. provided the "`*.a3s`" and "`*.a3t`" file extensions are used).


### Alan Solution Files Syntax

+ [`Alan Solution.sublime-syntax`][Alan Solution]
+ [`Alan Solution.sublime-settings`][Alan Solution Settings]

This package also defines an __Alan Solution__ syntax associated to the `*.a3s`/`*.a3sol` file extensions.

Solution files (aka "commands scripts") are text files containing player commands used to run an adventure in automated mode, by passing the script to the interpreter.
The `*.a3s`/`*.a3sol` file extensions are intuitively similar to the "`*.sol`" extension often used for solution files, but at the same time can be uniquely uniquely associated to Alan (Alan adventures having the `*.a3c` extension), allowing to enforce custom setting without the risk that they might affect other commonly used extensions.

In __Alan Solution__ files, single-line comments are enabled via the usual comment keyboard shortcuts, producing the "`; `" comment delimiter.

#### Alan Solution Color Scheme

+ [`Alan Solution.hidden-tmTheme`][Alan Solution Theme]
+ [`Alan Solution.YAML-propertyList-tmTheme`][Alan Solution tmTheme YAML] (scheme source)

This package also sets a predefined hidden color scheme to preview Alan Solution files:

![Screenshot of Alan Solution file color scheme][Screenshot Alan Solution Color Scheme]

... which is intended to make editing command script file more pleasant to the eye.

The color scheme is created by converting the YAML source file "[`Alan Solution.YAML-propertyList-tmTheme`][Alan Solution tmTheme YAML]" via [PackageDev]'s build system "[Convert to ... - Property List]"; since the YAML format is easier to maintain.

#### Alan Solution Snippets

A few snippets are also available to allow commenting solution files:

|        trigger        |        description        |
|-----------------------|---------------------------|
| "`h1`"+<kbd>Tab</kbd> | Commented Heading 1 Frame |
| "`h2`"+<kbd>Tab</kbd> | Commented Heading 2 Frame |
| "`h3`"+<kbd>Tab</kbd> | Commented Heading 3 Frame |
| "`h4`"+<kbd>Tab</kbd> | Commented Heading 4 Frame |


```

; ==============================================================================
; Heading 1 Frame
; ==============================================================================

; ------------------------------------------------------------------------------
; Heading 2 Frame
; ------------------------------------------------------------------------------

; ===============
; Heading 3 Frame
; ===============

; ---------------
; Heading 4 Frame
; ---------------

```

### Alan Transcript Files Syntax

+ [`Alan Transcript.sublime-syntax`][Alan Transcript]
+ [`Alan Transcript.sublime-settings`][Alan Transcript Settings]

This package also defines an __Alan Transcript__ syntax associated to the `*.a3t`/`*.a3log` file extensions.
While transcripts generated with the Alan interpreters used to have the `.log` file extension, now Alan as officially adopted the `.a3t` extension because `.log` is already being used in so many different contexts that it doesn't allow to enforce special editor settings on it.

The syntax also syntax highlights the player input lines, capturing the prompt (assuming it's always "`>`"), strings and comments. The output text from the adventure is not highlighted, as the scope of this syntax is to provide easy color separation between player commands and game output text.

In trasncripts of adventures which change the prompt (from the default "`>`" symbol) the player input line won't be captured and syntax highlighted.

In __Alan Transcript__ files, single-line comments are enabled via the usual comment keyboard shortcuts, producing a "`> ; `" comment delimiter. The reason why commented lines are preceded by a prompt (unlike Solution files, which use just a semicolon) is that this is the expected behavior in this context. Transcipts are automatically produced by the interpreter, and the purpose of the __Alan Transcript__ syntax is to allow a nicer preview of these files; but in some cases the user might wish to add some comments to the transcipts before sharing them with other (eg, to pinpoint a typo or a bug), and these added comments should be represented as a comment line added by the player during the game session (hence the addition of the prompt before the comment delimiter).


#### Alan Transcript Color Scheme

+ [`Alan Transcript.hidden-tmTheme`][Alan Transcript Theme]
+ [`Alan Transcript.YAML-propertyList-tmTheme`][Alan Transcript tmTheme YAML] (scheme source)

This package also sets a predefined hidden color scheme to preview Alan Transcript files:

![Screenshot of Alan Transcript file color scheme][Screenshot Alan Transcript Color Scheme]

... which is intended to make previewing of game transcript files more pleasant to the eye.

The color scheme is created by converting the YAML source file "[`Alan Transcript.YAML-propertyList-tmTheme`][Alan Transcript tmTheme YAML]" via [PackageDev]'s build system "[Convert to ... - Property List]"; since the YAML format is easier to maintain.

# Requirements

- Minum requirement: __Sublime Text 3__ BUILD `>=3170` (uses new `.sublime-color-scheme` format).
- Recomended: bleeding-edge __Sublime Text 3__ [Dev BUILD][ST3 Dev Builds].

This package is being developed using the latests [ST3 Dev Builds], and it might use features not included in the latest stable build; I can't grant that it will work with [ST3 Stable Builds].

This package is being developed using the latests [ST3 Dev Builds], but now that Sublime Text 3 has reached its end of life, and its next major incarnation is about to be released at any moment, there shouldn't be any longer any differences between [ST3 Dev Builds] and [ST3 Stable Builds], since no further updates are expected, except for bug fixes.


[ST3 Dev Builds]: https://www.sublimetext.com/3dev "Visit Sublime Text 3 Dev Builds page"
[ST3 Stable Builds]: https://www.sublimetext.com/3 "Visit Sublime Text 3 Stable Builds page"

# Installation

Create an "`Alan`" folder inside "`<data_path>/Packages/`", open a shell inside "`<data_path>/Packages/Alan/`" and type:

```
git clone https://github.com/tajmone/sublime-alan .
```

Don't forget the "`.`" after the repository URL! it's needed in order to clone the repository contents directly into the current folder, without creating a "`sublime-alan`" container folder.


# License

- [`LICENSE`][LICENSE]

```
MIT License

Copyright (c) 2018 Tristano Ajmone
https://github.com/tajmone/sublime-alan

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

# Acknowledgements

I would like to thank the following people who have helped me out with the difficulties of creating this syntax:

- [Keith Hall][Keith Hall SF] (@kingkeith)
- [Thomas Smith][Thom Smith SF] (@ThomSmith)
- [@FichteFoll][FichteFoll SF]

Without their precious help I wouldn't have overcome many of the problems related to implementing the syntax and choosing the right scopes.

I'd also like to express my gratitude to the authors of invaluable guidelines and tutorials which fill the huge gaps of undocumented Sublime Text 3 features and guidelines:

- [Daniel Spiewak] (@djspiewak) for his _[Stateful Chaining]_ guidelines.
- [Thomas Smith][Thom Smith GH] for his _[Use the Stack]_ guidelines.


# Links

Alan IF links:

- [Alan website]
- [IFWiki » Alan page]
- [Alan sourcecode on Bitbucket]
- [Alan Standard Library on Bitbucket]
- [Alan-IF mailing list and discussion group at Yahoo]

<!-----------------------------------------------------------------------------
                               REFERENCE LINKS
------------------------------------------------------------------------------>

<!-- CROSS REFERENCES -------------------------------------------------------->

[__Alan Solution__ files]: #alan-solution-files-syntax "Read more about Alan Solution files..."
[__Alan Transcript__ files]: #alan-transcript-files-syntax "Read more about Alan Transcript files..."

[Build Systems]: #build-systems "Read more about Sublime-Alan's Build Systems..."

<!-- ALAN LINKS -------------------------------------------------------------->

[Alan website]: https://www.alanif.se/ "Visit Alan official website"

[Alan SDK]: https://www.alanif.se/download-alan-v3/development-kits "Download the latest Alan SDK"

[Alan sourcecode on Bitbucket]: https://bitbucket.org/alanif/alan
[Alan Standard Library on Bitbucket]: https://bitbucket.org/alanif/alanlib

[Alan-IF mailing list and discussion group at Yahoo]: https://groups.yahoo.com/neo/groups/alan-if/info "Visit Alan-IF discussion group main page at Yahoo Groups"

[IFWiki » Alan page]: http://www.ifwiki.org/index.php/Alan "View Alan entry at IFWiki"

[IFWiki]: http://www.ifwiki.org "Visit IFWiki.org, the Interactive Fiction Wiki"
<!------- OTHER DOC FILES ---------------------------------------------------->

[TODO]: ./TODO.md "View the TODOs-list file"
[CHANGELOG]: ./CHANGELOG.md "View Sublime-Alan's CHANGELOG file"
[WORK_NOTES]: ./WORK_NOTES.md "View my working notes file"

<!--------- SCREENSHOTS ------------------------------------------------------>

[Screenshot Build Console]: ./screenshots/Build_Errors_Console.png "Screenshot of Sublime-Alan build system errors log in ST's console"
[Screenshot Build Editor]:  ./screenshots/Build_Errors_Editor.png "Screenshot of Sublime-Alan build system errors navigation (using 'Monokai' color scheme)"
[Screenshot Alan DarkFluo]:  ./screenshots/Alan_DarkFluo.png "Screenshot of 'Alan DarkFluo' color scheme"
[Screenshot Alan Solution Color Scheme]:  ./screenshots/Alan_Solution_scheme.png "Screenshot of 'Alan Solution' color scheme"
[Screenshot Alan Transcript Color Scheme]:  ./screenshots/Alan_Transcript_scheme.png "Screenshot of 'Alan Transcript' color scheme"
[Screenshot Snippet New Adv]:  ./screenshots/Snippet_New_Adventure.gif "Screenshot of 'New Adventure Boilerplate' snippet in action"
[Screenshot Snippet New Adv Vars]:  ./screenshots/Snippet_New_Adventure_Custom_Vars.gif "Using custom variables with the 'New Adventure Boilerplate' snippet"
[Screenshot Ligatures]:  ./screenshots/Ligatures_Preview.gif "Screenshots animation showing Alan code with ligatures enabled vs disabled"

<!-- USERS LINKS ------------------------------------------------------------->

[Keith Hall SF]: https://forum.sublimetext.com/u/kingkeith "See Keith Hall's Sublime Forum user profile"
[Keith Hall GH]: https://github.com/keith-hall "See Keith Hall's GitHub profile"
[Thom Smith SF]: https://forum.sublimetext.com/u/ThomSmith "See Thomas Smith's Sublime Forum user profile"
[Thom Smith GH]: https://github.com/Thom1729 "See Thomas Smith's GitHub profile"
[FichteFoll SF]: https://forum.sublimetext.com/u/FichteFoll "See FichteFoll's Sublime Forum user profile"
[FichteFoll GH]: https://github.com/FichteFoll "See FichteFoll's GitHub profile"
[Daniel Spiewak]: https://github.com/djspiewak "See @djspiewak's GitHub profile"

<!-- TUTORIALS AND GUIDELINES ------------------------------------------------>

[Stateful Chaining]: https://github.com/sublimehq/Packages/issues/757#issuecomment-269031562

[Use the Stack]: https://github.com/sublimehq/Packages/issues/757#issuecomment-287193733

<!-- EXTERNAL REFERENCES ----------------------------------------------------->

[PackageDev]: https://packagecontrol.io/packages/PackageDev "View PackageDev page at PackageControl.io"
[Convert to ... - Property List]: https://github.com/SublimeText/PackageDev/wiki/Serialized-Conversion "Read online documentation"

<!-- Project files and folders ----------------------------------------------->

[LICENSE]: ./LICENSE "View MIT License"

<!-- Alan Syntax ------------------------------------------------------------->

[Alan]: ./Alan.sublime-syntax "view syntax source file"

<!-- AlanLog Syntax ---------------------------------------------------------->

[AlanLog]: ./AlanLog.sublime-syntax "view syntax source file"
[AlanLog Settings]: ./AlanLog.sublime-settings "view settings source file"
[AlanLog tmTheme]: ./AlanLog.hidden-tmTheme "view color scheme file"
[AlanLog tmTheme YAML]: ./AlanLog.YAML-propertyList "view color scheme file"
[Alan Compiler Output]: ./AlanLog.sublime-syntax "view syntax source file"

[Alan DarkFluo]: ./Alan%20DarkFluo.sublime-color-scheme "view color scheme source file"

<!-- Alan Solution Syntax ---------------------------------------------------->

[Alan Solution]: ./Alan%20Solution.sublime-syntax "view syntax source file"
[Alan Solution Settings]: ./Alan%20Solution.sublime-settings "view settings source file"
[Alan Solution Theme]: ./Alan%20Solution.hidden-tmTheme "view theme source file"
[Alan Solution tmTheme YAML]: ./Alan%20Solution.YAML-propertyList "view color scheme file"

<!-- Alan Transcript Syntax -------------------------------------------------->

[Alan Transcript]: ./Alan%20Transcript.sublime-syntax "view syntax source file"
[Alan Transcript Settings]: ./Alan%20Transcript.sublime-settings "view settings source file"
[Alan Transcript Theme]: ./Alan%20Transcript.hidden-tmTheme "view theme source file"
[Alan Transcript tmTheme YAML]: ./Alan%20Transcript.YAML-propertyList "view color scheme file"

<!-- badges -->

[License badge]: https://img.shields.io/badge/License-MIT-blue
[Package badge]: https://img.shields.io/badge/status-WIP-orange "Sublime Alan is currently in Alpha stage"
[Alan badge]: https://img.shields.io/badge/Alan-3.0Beta6-yellow "Supported Alan version (click for Alan download page)"
[ST3 badge]: https://img.shields.io/badge/ST3-3210-yellow "Supported Sublime Text 3 version (click for Sublime Text 3 download page)"
[ST3 link]: https://www.sublimetext.com/3
[Travis badge]: https://travis-ci.com/tajmone/sublime-alan.svg?branch=master
[Travis link]: https://travis-ci.com/tajmone/sublime-alan "Travis CI: EditorConfig validation status"

<!-- Issues ------------------------------------------------------------------>

[alan-if/alan#2]: https://github.com/alan-if/alan/issues/2

<!-- EOF -->
