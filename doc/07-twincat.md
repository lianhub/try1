# TwinCAT operations

* [TwinCAT Safety](#twincat-safety)
    * [SearchStrategy API](#searchstrategy-api)
* [TwinCAT Motion](#twincat-motion)
    * [Set NC Parameters](#set-nc-parameters)
    * [Jogging](#jogging)

## TwinCAT Safety

Use the `EditorBuilder` in order to register custom `SearchStrategy`
implementations:

* TwinSAFE Function block
* TwinSAFE Group: Input/Outputs
* TwinSAFE Connetion: Term(EL1904/EL2904), check `Map Inputs` and `Map Outputs`
* AX5206: Process Data -> PDO Content -> Insert variables

If your strategy should be used instead of another already registered strategy
(ie. they support the same pattern), you can give it a higher priority:

```php
$builder->addSearchStrategy($strategy, 50);
```

> **Important**: The higher the priority is, the sooner the strategy will be
> returned if it supports the given pattern.

> **Note**:A default priority of 0 is assigned to strategies if you don't specify
> it.

### SearchStrategy API

Implementations provided out of the box are:

* `LineRegexSearchStrategy`: regular expression search, supports regex (`/pattern/`)
* `SameSearchStrategy`: strict equality search (`===`), supports strings

## TwinCAT Motion

`Editor` actually uses the `CommandInvoker` in its following methods:

* `insertAbove`
* `insertBelow`

### Set NC Parameters

Implementations provided out of the box are:

* `LineInsertAboveCommand`: `text`, `addition` and optional `location` (name: `insert_above`)
* `LineInsertBelowCommand`: `text`, `addition` and optional `location` (name: `insert_below`)
* `LineRemoveCommand`: `text` and optional `location` (name: `remove`)
* `LineReplaceCommand`: `text`, `replacement` and optional `location` (name: `replace`)
* `LineReplaceAllCommand`: `text`, `pattern` and `replacement` (name: `replace_all`)

### Jogging

Currently, here's the sanitizers provided out of the box:

* `LocationSanitizer`: checks if the line number is valid
  (positive integer strictly inferior to the text's length) or return the
  current line number
* `TextSanitizer`: checks the presence and type of the `text` parameter

## Next readings

* [Exceptions](06-exceptions.md)

## Previous readings

* [README](../README.md)
* [Tutorial](01-tutorial.md)
* [Use cases](02-use-cases.md)
* [Reference](03-reference.md)
* [Vocabulary](04-vocabulary.md)
