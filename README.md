# Sublime-Alan

Alan IF 3 syntax for Sublime Text 3.

- https://github.com/tajmone/sublime-alan

```
Sublime Text >= 3149 (DEV BUILD)
Alan IF v3.0 Beta 5
```

> __ALPHA STAGE__ — This project is still a WIP Alpha version! Most features are still experimental and subject to continuos changes. Screenshots and descriptions might not always accurately represent the latest changes.

The following document isn't always updated to cover all the added features, it's mainly intended to illustrate the project goals; for a full list of current features, see the [CHANGELOG].

-----

**Table of Contents**

<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="only_ascii" uri_encoding="true" levels="1,2,3" -->

- [About](#about)
- [Features](#features)
    - [Syntax Highlighting](#syntax-highlighting)
    - [Color Schemes](#color-schemes)
    - [Goto Symbols](#goto-symbols)
    - [Build Systems](#build-systems)
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

The package also ships with additional syntax definitions for:

- Compiler log in the the [Build Systems]
- __[Alan Solution]__ files (aka "commands scripts").
- __[Alan Transcript]__ files.

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

## Snippets

Sublime-Alan ships with some useful snippets to simplify writing your adventures.

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

This package also provides additional syntax definitions for Alan game transcipts and solution files:

- __Alan Solution__ file ("`*.a3sol`").
- __Alan Transcript__ file ("`*.a3log`").

The purpose of these syntaxes is to simplify handling of game transcipt and solution files by settings Sublime Text to handle these files with ISO-8859-1 enconding, as well as providing some minimal syntax highlighting and allowing the user to associate custom color schemes to them.  Without a basic syntax definition, and its encoding settings, Sublime Text would default to UTF-8 encoding, which would cause lots of problems and errors if the solution file contains special characters (like accented letters), and would not display correctly transcripts containing special chars.

Hopefully, these two extra syntaxes will simplify creating and using command scripts to test adventures during the authoring stage, and to correctly visualize game transcipts (ie, provided the "`*.a3sol`" and "`*.a3log`" file extensions are used).


## Alan Solution Files Syntax

This package also defines an __Alan Solution__ syntax associated to the "`*.a3sol`" file extension.

Solution files (aka "commands scripts") are text files containing player commands used to run an adventure in automated mode, by passing the script to the interpreter. Since there is no official extension for Alan solution files, I've chosen to arbitrarily adopt the "`*.a3sol`" file extension, which is intuitively similar to  "`*.sol`" extension often used for solution files, but at the same time is uniquely associated to Alan (Alan adventures having the "`*.a3c`" extension).


## Alan Transcript Files Syntax

This package also defines an __Alan Transcript__ syntax associated to the "`*.a3log`" file extension. While transcripts generated with the Alan interpreters usually have the "`.log`" file extensions, I've opted to associate this syntax to the  "`*.a3log`" extension because "`.log`" is used in so many different contexts that it didn't seem appropriate to enforce special settings on it. The  "`*.a3log`" extensions seemed a good compromise since it blends the "`.a3`" suffix (commonly used by Alan) with "`log`", so it should be an intuitive compromise. 


# Requirements

Requires __Sublime Text 3__ DEV BUILD `>=3149`.

This package uses some new ST3 features which have not yet been included into the latest stable build (`3143`); so, until the next stable release is out you'll need to use [ST Dev Builds] in order to use this package.

[ST Dev Builds]: https://www.sublimetext.com/3dev "Visit Sublime Text 3 Dev Builds page"

# Installation

Create an "`Alan`" folder inside "`<data_path>/Packages/`", open a shell inside "`<data_path>/Packages/Alan/`" and type:

```
git clone https://github.com/tajmone/sublime-alan .
```

Don't forget the "`.`" after the repository URL! it's needed in order to clone the repository contents directly into the current folder, without creating a "`sublime-alan`" container folder.


# License

- [`LICENSE`](./LICENSE)

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

[Alan Solution]: #alan-solution-files-syntax "Read more about Alan Solution files..."
[Alan Transcript]: #alan-transcript-files-syntax "Read more about Alan Transcript files..."

[Build Systems]: #build-systems "Read more about Sublime-Alan's Build Systems..."
<!-- ALAN LINKS -------------------------------------------------------------->

[Alan website]: https://www.alanif.se/ "Visit Alan official website"

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
[Screenshot Snippet New Adv]:  ./screenshots/Snippet_New_Adventure.gif "Screenshot of 'New Adventure Boilerplate' snippet in action"
[Screenshot Snippet New Adv Vars]:  ./screenshots/Snippet_New_Adventure_Custom_Vars.gif "Using custom variables with the 'New Adventure Boilerplate' snippet"

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

