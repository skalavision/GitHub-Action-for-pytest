## GitHub Action to find Python syntax errors and undefined names

An action that runs selected [flake8](http://flake8.pycqa.org) tests on the Python code in your repo. If ___syntax errors or undefined names___ are found in the Python code then the action will fail.

Example workflow:
```
workflow "New workflow" {
  on = "push"
  resolves = ["action"]
}

action "action" {
  uses = "cclauss/Find-Python-syntax-errors-action@master"
}
```
$ __flake8 . --count --select=E901,E999,F821,F822,F823 --show-source --statistics__

__E901,E999,F821,F822,F823__ are the "_showstopper_" [flake8](http://flake8.pycqa.org) issues that can halt the runtime with a SyntaxError, NameError, etc. These 5 are different from most other flake8 issues which are merely "style violations" -- useful for readability but they do not effect runtime safety.
* F821: undefined name `name`
* F822: undefined name `name` in `__all__`
* F823: local variable name referenced before assignment
* E901: SyntaxError or IndentationError
* E999: SyntaxError -- failed to compile a file into an Abstract Syntax Tree