# Sublime-Alan TODOs

Pending tasks and bugs list.


-----

**Table of Contents**

<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="only_ascii" uri_encoding="true" levels="1,2,3" -->

- [TODOs](#todos)
    - [Alan Syntax:](#alan-syntax)
    - [Syntax Test Files](#syntax-test-files)
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


[ST3Docs syntax test]: https://www.sublimetext.com/docs/3/syntax.html#testing

[tests]: ./tests/ "See 'tests' folder"
[test_Strings]: ./tests/syntax_test_Strings.alan "Open file..."
[test_QuotedIdentifiers]: ./tests/syntax_test_QuotedIdentifiers.alan "Open file..."

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
