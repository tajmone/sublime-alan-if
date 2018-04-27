# CHANGELOG

### 2018-04-27:2

- `Alan.sublime-syntax` v0.0.15:
    + Major cleanup of the syntax following [__@djspiewak's__ guidelines].
    + Now partially valid syntax fragments are handled better:
        + omitted expected tokens are skipped, so tha the next expected token is caught.
        + Failsafe bail-outs: partial/broken code doesn't trap the highlighter in a syntax context looping for ever.
        + Scopes spillings fixed: now scopes don't eat up whitespace of neighbouring elements.
- Syntax [`/tests/`][tests]:
    + [`syntax_test_ClassDeclarations`][test_ClassDeclarations] — updated with new tests against context spilling and partial/broken code fragments.


### 2018-04-27:1

- `Alan.sublime-syntax` v0.0.14:
    + __IMPORT context__ — added bail-out failsafe when EOL is reached, to prevent context entrapment when dealing with malformed code.

### 2018-04-26:2

- `Alan.sublime-syntax` v0.0.13:
    + added some comment-notes about upcoming contexts and work.

### 2018-04-26:1

- `Alan.sublime-syntax` v0.0.12:
- __class definition__ context:
    + push `class` context instead of setting it to the stack.
    + added bail-out option to prevent partially valid syntax fragments (or even `ADD TO EVERY...`) to loop forever in the class context (effectively, breaking highlighting of all that follows).

\[thanks to [__@djspiewak's__ guidelines]: "Stateful Chaining » Bail Outs"\]

[__@djspiewak's__ guidelines]: https://github.com/sublimehq/Packages/issues/757#issuecomment-269031562 "View @djspiewak's notes on writing syntaxes"


### 2018-04-25:2

- `Alan.sublime-syntax` v0.0.11:
    + Fixed scope of loose `quoted_identifiers`
    + Fixed scope of out of context `identifier`
- Updated [`/tests/`][tests] to pass with syntax v0.0.11:
    + [`syntax_test_QuotedIdentifiers.alan`][test_QuotedIdentifiers]
    + [`syntax_test_Strings.alan`][test_Strings]

### 2018-04-25:1

- `Alan.sublime-syntax` v0.0.10:
    + __class definition__ context (`EVERY ... END EVERY`):
        * now __inheritance__ is captured and scoped
        * now optional ID and terminator after `END EVERY` are scoped
        * improved overall handling of this syntax
        * __NOTE__: some edge cases still not handled well!
- Added to [`/tests/`][tests]:
    + [`syntax_test_ClassDeclarations`][test_ClassDeclarations]

[test_ClassDeclarations]: ./tests/syntax_test_ClassDeclarations.alan "Open file..."


### 2018-04-24

- `Alan.sublime-syntax` v0.0.9:
    + simplified the context for capturing __quoted identifiers__.
    + new __class definition__ context (`EVERY ... END EVERY`) — still drafty, and contains a couple of hugly workarounds.
- new [`Alan-GotoSymbol.tmPreferences`][GotoSymbol]:
    + indexes class names (at their `EVERY` definition)

[GotoSymbol]: ./Alan-GotoSymbol.tmPreferences "view GotoSymbol settings file"

### 2018-04-23

- `Alan.sublime-syntax` v0.0.8:
    - added to comments scope delimiter character specification: `comment.line.double-dash`
    - fixed identifiers base regex (`[A-Z][A-Za-z0-9_]*` => `[A-Za-z][A-Za-z0-9_]*`)

### 2018-04-21

- "__New Adventure Boilerplate__" snippet ("`newadv`").

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

