# CHANGELOG

### 2018-05-14:2

- `Alan.sublime-syntax` v0.0.26:
    + _BUG FIX_: __initial location__ context now expects only one identifier after `AT`/`IN`, and correctly bails out if anything other than the (optional) dot terminator follows it.
- [`syntax_test_InitialLocation.alan`][test_InitialLocation] — new test file for __initial location__.
- Updated [`syntax_test_Attributes.alan`][test_Attributes] — removed __initial location__ references from tests (in case I change scope name, I won't have to update multiple files).

### 2018-05-14:1

- `Alan.sublime-syntax` v0.0.25:
    + Annotated bug which needs to be fixed in __initial location__ context.

### 2018-05-13

- `Alan.sublime-syntax` v0.0.24:
    + Added __initial location__ (`IN contID`/`AT locationID`) to `property_context`. ~~Although this should only apply to instances, I've included it also in classes (declarations and additions) for easier maintainance and also to cover malformed code without breaking~~ (__WRONG__: it can be found also in classes declarations).
- Updated [`syntax_test_Attributes.alan`][test_Attributes]

### 2018-05-12

- __[Snippets]__:
    + Clean-Up "__New Adventure Boilerplate__"
    + New «commented headings» set of snippets for formatting comments as various heading levels:
        * `cmh1`: Commented Heading Frame 1
        * `cmh2`: Commented Heading Frame 2
        * `cmh3`: Commented Heading Frame 3
        * `cmh4`: Commented Heading Frame 4
        * `cmh5`: Commented Heading Frame 5
        * `cmh6`: Commented Heading 6 (underlined)
        * `cmhr`: Commented Horizontal Rules

### 2018-05-11:2

- [`syntax_test_Attributes.alan`][test_Attributes] — new test file for attributes; still very limited testing capabilities due to lack of other surrounding contexts, but at least can serve to check if syntax breaks up.


### 2018-05-11:1

- `Alan.sublime-syntax` v0.0.23: minor fixes: include strings context in prototype, cleanup code and apply new  `eol_POP` context.
- Cleanup [`README.md`][README] and [`TODO.md`][TODO].

### 2018-05-08

- New attribures completions (some very experimental)
- `Alan.sublime-syntax` v0.0.22:
    + __properties__ context: small bug fix that prevented handling a `NOT` bool attr. when inside a block of attributes with one `IS`, etc.

### 2018-05-07

- `Alan.sublime-syntax` v0.0.21:
    + Added __properties__ context (incomplete):
        * Now classes, instances and additions reckognize attributes statements (except for _Set Attributes_). Still a draft but tests have shown it handles well partial syntaxes.
        * `(IS|ARE|HAS|CAN)[NOT]`:
            - [x] `ID.` — boolean attr.
            - [x] `ID INT.` — Numeric attr.
            - [x] `ID STRING.` — string attr.
            - [x] `ID ID.` — Event/Instance attr.
            - [ ] `ID { MEMBERS }.` — Set attr.

### 2018-05-06

- __[Completions]__:
    + New [`Anywhere.sublime-completions`][Anywhere]:
        * Formatting Styles:
            - `styalert`: STYLE ALERT
            - `styem`: STYLE EMPHASIZED
            - `stynorm`: STYLE NORMAL
            - `stypre`: STYLE PREFORMATTED
            - `styquote`: STYLE QUOTE


### 2018-05-04:2

- __[Snippets]__:
    + new "__Alan Boilerplate__" ("`abp`").
    + tweaked "__New Adventure Boilerplate__" ("`newadv`").
- __[Completions]__ — Started to create auto-completions:
    + [`Global.sublime-completions`][Global]:
        * `class`: Class Declaration
        * `addition`: Class Addition
        * `instance`: Instance Declaration


### 2018-05-04:1

- Update __Goto Symbol__ indexing:
    + Add __instances__
    + Don't index class and instance tail identifiers.
    + Enable Indexing in Project (global symbol list).
    + Apply Symbol transformation rules also to global symbol list.

### 2018-05-03:3

- `Alan.sublime-syntax` v0.0.20:
    + some scope names fixed
    + new `tail_class_&_terminator` reusable context now shared between:
        * `class_declaration`
        * `addition_declaration`
- Added to [`/tests/`][tests]:
    + [`syntax_test_Additions.alan`][test_Additions]

### 2018-05-03:2

- `Alan.sublime-syntax` v0.0.19:
    + __additions__: A first draft of the context to capture `ADD TO EVERY` statements. In lack of better scope names, I've used `meta.addition` to scope it, but this might not be the best choice.

### 2018-05-03:1

- `Alan.sublime-syntax` v0.0.18:
    + improved identifiers reusabilty by managing to use `generic_identifier` instead of:
        * `inherited_class_identifier` (_DELETED_)
        * `class_tail_identifier` (_DELETED_)
        * `instance_tail_identifier` (_DELETED_)
- Added to [`/tests/`][tests]:
    + [`syntax_test_Instances.alan`][test_Instances]
### 2018-05-02:3

- `Alan.sublime-syntax` v0.0.17:
    + __instances__: A first draft of the context to capture instances (`THE Id IsA ...`). In lack of better scope names, I've used `meta.instance` amd `entity.name.instance` to scope them, but these might not be the best choice.

### 2018-05-02:2

- __[AlanLog]__ now uses a dedicated hidden color scheme, instead of relying on "__[Alan DarkFluo]__":
    + [`AlanLog.hidden-tmTheme`][AlanLog tmTheme] v0.0.1 — hidden color scheme for __AlanLog__ syntax. Build from YAML source:
    + [`AlanLog.YAML-propertyList`][AlanLog tmTheme YAML] — YAML source used for creating `AlanLog.hidden-tmTheme` via [PackageDev]'s build system "[Convert to ... - Property List]".
- "__[Alan DarkFluo]__" v0.3 — removed end-section targetting __AlanLog__ syntax coloring.

> __NOTES__ — The new __AlanLog__ color scheme uses a temporary color palette which needs to be fixed. Also, all the scope names in the syntax need to be redefined.


### 2018-05-02:1

- "__[Alan Compiler Output]__" renamed to __[AlanLog]__:
    + [`AlanLog.sublime-syntax`][AlanLog]
    + [`AlanLog.sublime-settings`][AlanLog Settings]

### 2018-04-29

- `Alan.sublime-syntax` v0.0.16:
    + __identifiers__: tweaked the `ID` variable so that all valid characters are covered by identifiers's RegExs:

        ```yaml
        LETTER: 'a-zA-Zà-þ&&[^÷]'
        ID: '(\b[{{LETTER}}][0-9_{{LETTER}}]*\b)'
        ```

        The definition of `LETTER` now includes also unicode points in the ranges `U+00E0..U+00F6` and `U+00F8..U+00FE` ([Latin-1 Supplement]). Thoroughly tested against Alan compiler (using default enconding options, [ISO-8859-1]).

    + __quoted identifiers__: now the single-quote delimiters are always part of the identifier (same scope), they just get the additional `punctuation.definition.identifier.alan` scope. This simplifies reusable contexts; also, it seems appropriate. Of course, in the Goto Symbol functionality, all quoted identifiers are indexed without the delimiting quotes, and with all internal escaped quotes (ie `''`) shown as a single quote. This simplifies fuzzy search of the identifier, and is also how the identifier is actually rendered in the game world.
- [`syntax_test_ClassDeclarations.alan`][test_ClassDeclarations] — updated with new tests to check that the delimiting quotes of __quoted identifiers__ always get scoped as part of the identifier.


### 2018-04-28

- Color scheme "__[Alan DarkFluo]__" v0.2:
    + Changed BG color to slightly less darker shade.
    + Better color choices for selections.

### 2018-04-27:3

- Goto Symbols:
    + quoted identifiers are transformed to remove the delimiting single-quotes, and transform double (escaped) single-quotes into a single one (eg: `'Denny''s Cat'` » `Denny's Cat`). This is the transformation rule:

    ```
    s/^'(.+)'$/$1/;
    s/(')\1/$1/g;
    ```

> __NOTE__ — Currently, some class symbols quoted identifiers are scoped without the delimiting quotes (eg: `inherited_class_identifier`), while others include them. This is due to the reusable `generic_identifier` introduced lately, which leverages being included in a (optional) `set` context that uses `scope_meta` to scope it to the current need. The previous system of using context variants for each identifier, had the advantage of allowing to leave out the delimiting SQ symbols from the `entity.name`. It looks like I'll have to switch back to the old system at the cost of redundancy, having to create multiple identifiers, one for each specific scope (inherited class, class, class tail, and so on).

### 2018-04-27:2

- `Alan.sublime-syntax` v0.0.15:
    + Major cleanup of the syntax following [__@djspiewak's__ guidelines].
    + Now partially valid syntax fragments are handled better:
        + omitted expected tokens are skipped, so tha the next expected token is caught.
        + Failsafe bail-outs: partial/broken code doesn't trap the highlighter in a syntax context looping for ever.
        + Scopes spillings fixed: now scopes don't eat up whitespace of neighbouring elements.
- Syntax [`/tests/`][tests]:
    + [`syntax_test_ClassDeclarations.alan`][test_ClassDeclarations] — updated with new tests against context spilling and partial/broken code fragments.


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
    + [`syntax_test_ClassDeclarations.alan`][test_ClassDeclarations]


### 2018-04-24

- `Alan.sublime-syntax` v0.0.9:
    + simplified the context for capturing __quoted identifiers__.
    + new __class definition__ context (`EVERY ... END EVERY`) — still drafty, and contains a couple of hugly workarounds.
- new [`Alan-GotoSymbol.tmPreferences`][GotoSymbol]:
    + indexes class names (at their `EVERY` definition)


### 2018-04-23

- `Alan.sublime-syntax` v0.0.8:
    - added to comments scope delimiter character specification: `comment.line.double-dash`
    - fixed identifiers base regex (`[A-Z][A-Za-z0-9_]*` => `[A-Za-z][A-Za-z0-9_]*`)

### 2018-04-21

- "__New Adventure Boilerplate__" snippet ("`newadv`").

### 2018-04-20

- New hidden syntax "__[Alan Compiler Output]__" — this syntax is used to syntax higlight Alan compiler's error log in Sublime Text's console during Buil operations (using the "__[Alan DarkFluo]__" color scheme).
- New color scheme "__[Alan DarkFluo]__"
    + A darkish scheme with contrasting colors (still WIP).
    + Also defines colors targetting the "__[Alan Compiler Output]__" syntax.
- __[Build System]__:
    + Added syntax highlighting of Alan compiler output.


### 2018-04-18

- Added default __[Build System]__:
    +  Available for "`*.alan`" files.
    +  Captures errors and warnings for results navigation (via `-cc` option).
    +  Requires alan compiler binary to be on system PATH.
- `Alan.sublime-syntax` v0.0.7:
    + Now `END` in `END IF` is scoped as `keyword.control.conditional` too.


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


<!------------------------------------------------------------------------------
                                REFERENCE LINKS                                 
------------------------------------------------------------------------------->

[CHANGELOG]: ./CHANGELOG.md "View Sublime-Alan's CHANGELOG file"
[README]: ./README.md "View README file"
[TODO]: ./TODO.md "View the TODOs-list file"
[WORK_NOTES]: ./WORK_NOTES.md "View my working notes file"


<!-- TEST FILES -->
[tests]: ./tests/ "See 'tests' folder"
[test_Additions]: ./tests/syntax_test_Additions.alan "Open file..."
[test_Attributes]: ./tests/syntax_test_Attributes.alan "Open file..."
[test_InitialLocation]: ./tests/syntax_test_InitialLocation.alan "Open file..."
[test_ClassDeclarations]: ./tests/syntax_test_ClassDeclarations.alan "Open file..."
[test_Instances]: ./tests/syntax_test_Instances.alan "Open file..."
[test_QuotedIdentifiers]: ./tests/syntax_test_QuotedIdentifiers.alan "Open file..."
[test_Strings]: ./tests/syntax_test_Strings.alan "Open file..."

<!-- SNIPPETS -->
[Snippets]: ./snippets/ "Go to 'snippets' subfolder"

<!-- COMPLETIONS -->
[Completions]:  ./completions/ "Go to 'completions' subfolder"
[Global]: ./completions/Global.sublime-completions
[Anywhere]: ./completions/Anywhere.sublime-completions


[Build System]: ./Alan.sublime-build "view build system source file"

[GotoSymbol]: ./Alan-GotoSymbol.tmPreferences "view GotoSymbol settings file"

[AlanLog]: ./AlanLog.sublime-syntax "view syntax source file"
[AlanLog Settings]: ./AlanLog.sublime-settings "view settings source file"
[AlanLog tmTheme]: ./AlanLog.hidden-tmTheme "view color scheme file"
[AlanLog tmTheme YAML]: ./AlanLog.YAML-propertyList "view color scheme file"
[Alan Compiler Output]: ./AlanLog.sublime-syntax "view syntax source file"

[Alan DarkFluo]: ./Alan%20DarkFluo.sublime-color-scheme "view color scheme source file"

[PackageDev]: https://packagecontrol.io/packages/PackageDev "View PackageDev page at PackageControl.io"
[Convert to ... - Property List]: https://github.com/SublimeText/PackageDev/wiki/Serialized-Conversion "Read online documentation"

[Latin-1 Supplement]: http://jrgraphix.net/r/Unicode/00A0-00FF
[ISO-8859-1]: https://en.wikipedia.org/wiki/ISO/IEC_8859-1

[__@djspiewak's__ guidelines]: https://github.com/sublimehq/Packages/issues/757#issuecomment-269031562 "View @djspiewak's notes on writing syntaxes"
