
### Namespaces

* `doc` is in `clojure.repl`

### Leiningen

* `lein new app my-app` - make a new project
* (in `my-app` dir): `lein run`
* (in `my-app` dir): `lein repl`
* (in `my-app` dir): `emacs src/my-app/core.clj` and `M-x cider-jack-in`

### Paredit

* Use `M-(` for `paredit-wrap-around` and `C-<right arrow>` and `C-<left arrow>`
in inner parens to "slurp" and "barf".
* `C-M-f` to move to the closing parens.
* `C-M-b` to move to the opening parens.

### CIDER

* `C-x C-e` at the end of a line - eval the line in the REPL
* `C-u C-x C-e` at the end of a line - print the evaluation
* `C-c M-n` set the namespace to the namespace at the top of the current file.
* `C-c C-k` to compile the current file.
* `C-c C-c` to compile the current function.
* `C-<up arrow>` or `M-p` to cycle back through history
* `C-<down arrow>` or `M-n` to cycle forward through history
* `C-c C-d C-d` for documentation for the symbol under the point (`q` to quit)
* `C-c C-d C-a` appropos across documentation (`q` to quit)
* `M-.` and `M-,` navigate source for symbol under point

#### CIDER Error Handling

* `q` to exit the stack trace
* `C-x b *cider-error*` to view the error again (`q` to exit)

