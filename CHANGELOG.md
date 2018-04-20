# CHANGELOG

### 2018-04-20

- New hidden syntax "__[Alan Compiler Output]__" — this syntax is used to syntax higlight Alan compiler's error log in Sublime Text's console during Buil operations (using the "__[Alan DarkFluo]__" color scheme).
- New cholor scheme "__[Alan DarkFluo]__"
    + A darkish scheme with contrasting colors (still WIP).
    + Also defines colors targetting the "__[Alan Compiler Output]__" syntax.
- __[Build System]__:
    + Added syntax highlighting of Alan compiler output.

[Alan Compiler Output]: ./Alan%20Compiler%20Output.sublime-syntax "view syntax source file"
[Alan DarkFluo]: ./Alan%20DarkFluo.sublime-color-scheme "view color scheme source file"

### 2018-04-18

- Added default __[Build System]__:
    +  Available for "`*.alan`" files.
    +  Captures errors and warnings for results navigation (via `-cc` option).
    +  Requires alan compiler binary to be on system PATH.
- `Alan.sublime-syntax` v0.0.7:
    + Now `END` in `END IF` is scoped as `keyword.control.conditional` too.

[Build System]: ./Alan.sublime-build "view build system source file"

### 2018-04-14:4

- `Alan.sublime-syntax` v0.0.6:
    + Cleaned Up __Quoted Identifiers__: smaller code; now can handle  2 consecuitve escaped SQ (`''''`) in the middle without prematurely ending.
- Added to [`/tests/`][tests]:
    + [`syntax_test_QuotedIdentifiers.alan`][test_QuotedIdentifiers]


### 2018-04-14:3

- `Alan.sublime-syntax` v0.0.5:
    + Bug Fix: __String__ containing 2 escaped DQ inside (`"""""`) was ending string prematurely
    + [`syntax_test_Strings.alan`][test_Strings] (_**now succeeds**_)
- Now __empty strings__ get additional `empty` scope:

    ```
    string.quoted.double.empty.alan
    ```

### 2018-04-14:2

- Added `CHANGELOG.md`
- Added [`TODO.md`](./TODO.md)
- Added [`/tests/`][tests] folder for automated testing syntax scopes:
    + [`syntax_test_Strings.alan`][test_Strings] (_**fails!!!**_)


### 2018-04-14:1

- First commit on GitHub
- `Alan.sublime-syntax` v0.0.4


[tests]: ./tests/ "See 'tests' folder"
[test_Strings]: ./tests/syntax_test_Strings.alan "Open file..."
[test_QuotedIdentifiers]: ./tests/syntax_test_QuotedIdentifiers.alan "Open file..."

