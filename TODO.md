# Sublime-Alan TODOs

Pending tasks and bugs list.


-----

**Table of Contents**

<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="only_ascii" uri_encoding="true" levels="1,2,3" -->

- [TODOs](#todos)
    - [Alan Syntax:](#alan-syntax)
    - [Syntax Test Files](#syntax-test-files)
    - [Build Systems](#build-systems)
    - [Snippets](#snippets)
- [Bugs](#bugs)
- [Fixed Bugs](#fixed-bugs)

<!-- /MarkdownTOC -->

-----

# TODOs

List of planned tasks and features:

- [ ] Add some snippets
- [ ] Create dedicate Alan color scheme (light)
- [ ] Create color scheme for testing Alan syntax (color everything)
- [ ] Implement indexing for Goto funcionality
- [ ] Implement autocompletion

## Alan Syntax:

+ [ ] __Quoted Identifiers__:
    * [ ] Add `empty` scope to empty identifiers
    * [ ] Decide semantic scope for identifiers
    * [x] Cleanup __quoted identifiers__ code, along the lines of Strings, and make sure it can handle `'..''''..'`
+ [ ] __Special $ Characters__:
    * [ ] The parameters $ Chars (`$1`, etc.) should be scoped as _placeholders_:

        ```
        constant.other.placeholder
        ```

        (they resemble more the ` %s` in `sprintf()` rather than escape sequences)

## Syntax Test Files

Add [syntax test files][ST3Docs syntax test] to [`/tests/`][tests]:

+ [x] __Strings__:
    * [`syntax_test_Strings.alan`][test_Strings] (__OK!__)
+ [x] __Quoted Identifiers__:
    * [`syntax_test_QuotedIdentifiers.alan`][test_QuotedIdentifiers] (__OK!__)
+ [ ] __Comments__
+ [ ] __Keywords__
+ [ ] __Special $ Characters__


[ST3Docs syntax test]: https://www.sublimetext.com/docs/3/syntax.html#testing "See Sublime Text 3 official documentation for this topic"

[tests]: ./tests/ "See 'tests' folder"
[test_Strings]: ./tests/syntax_test_Strings.alan "Open file..."
[test_QuotedIdentifiers]: ./tests/syntax_test_QuotedIdentifiers.alan "Open file..."

## Build Systems

Add cross-platform [build systems][ST3Docs BuildSys] (alan compiler must be available on path.

> NOTE — the `-ide` options reports the error line, but instead of the column it reports the range of chars offset (relative the beginning of file) of the problematic code. The `-cc` option reports line and column instead (eg `line 5(24)`).

- [x] default build:
    + [x] use options:
        * [x] `-cc`
    + [x] implement navigating results

[ST3Docs BuildSys]: http://www.sublimetext.com/docs/3/build_systems.html "See Sublime Text 3 official documentation for this topic"

## Snippets

Create some useful snippets. 

Should these also cover to StdLib?

# Bugs

Known bugs which need fixing:


# Fixed Bugs

- [x] __Strings__: two consecutive escaped DQs in the middle of a string prematurely end the string:

      ```
      "Enclose in double quotes ("""") what you want to say.".
      ```

      ... strings ends at `("""` and `") what` is treated as normal text.

      __*Fixed*__ (`2018-04-14:3`)

      Now the test file [`syntax_test_Strings.alan`][test_Strings] succeeds.
