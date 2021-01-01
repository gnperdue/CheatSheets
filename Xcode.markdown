
## Move text

* Move line up or down: `cmd-option-[` or `cmd-option-]`

## View

* Center screen around cursor: `^l`

## Edit multiple lines

See:  https://developer.apple.com/videos/play/wwdc2018/102/?time=2518

* Create new cursors: `shift + control + left click`
* New cursor above: `shift + control + <up arrow>`
* New cursor below: `shift + control + <down arrow>`
* Create a new cursor on every line: `option + drag`

## Swift notes

* Use ctrl-6 to quick access `MARK`ed sections, `struct`s, etc.
* The `MARK: -` construct creates a divider line
* The `MARK: note` or `MARK: - note` constructs create notes
* Also useful: `// TODO: -` and `// FIXME: -`
* Use `#warning("message")` to create compiler warnings.
* Use `#error("message")` to create compiler errors.
* Use `@available(swift, deprecated: <version number>)` to check on progress on
  bugs in the language. If you use a current version number, you will get a
  "deprecated" warning anywhere you've used that code (e.g., put the mark on
  the line above the definition of a `struct` or a `protocol`, etc.). Can
  include a message: `@available(swift, deprecated: -, message: -)`. Also may
  use `obsoleted` instead of `deprecated` to generate a compiler error instead
  of a warning. And `swift` here is a platform argument, so it could be
  `iOS`, etc.
