# Sublime-Alan TODOs

Pending tasks and bugs list.


-----

**Table of Contents**

<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="only_ascii" uri_encoding="true" levels="1,2,3" -->

- [TODOs](#todos)
- [Bugs](#bugs)
- [Fixed Bugs](#fixed-bugs)

<!-- /MarkdownTOC -->

-----

# TODOs

List of planned tasks and features:

- [ ] Alan Syntax:
    + [ ] Cleanup __quoted identifiers__ code, along the lines of Strings, and make sure it can handle `'..''''..'`
- [ ] Add [syntax test files][ST3Docs syntax test] to [`/tests/`][tests]:
    + [x] __Strings__:
        * [`syntax_test_Strings.alan`][test_Strings]
    + [ ] __Comments__
    + [ ] __Keywords__

[ST3Docs syntax test]: https://www.sublimetext.com/docs/3/syntax.html#testing

[tests]: ./tests/ "See 'tests' folder"
[test_Strings]: ./tests/syntax_test_Strings.alan "Open file..."

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
