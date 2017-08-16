# My Personal website

This website includes documentations for my projects.

*Because your code too needs an editor to manipulate files*.

[![SensioLabsInsight](https://insight.sensiolabs.com/projects/fbe2d89f-f64d-45c2-a680-bbafac4b0d08/mini.png)](https://insight.sensiolabs.com/projects/fbe2d89f-f64d-45c2-a680-bbafac4b0d08)
[![Travis CI](https://travis-ci.org/gnugat/redaktilo.png)](https://travis-ci.org/gnugat/redaktilo)

## Getting started

Use [Composer](http://getcomposer.org/) to install Redaktilo in your projects:

    composer require "gnugat/redaktilo:^1.0"

Redaktilo provides an `Editor` class which can be instanciated using
`EditorFactory`:

```php
<?php
require_once __DIR__.'/vendor/autoload.php';

use Gnugat\Redaktilo\EditorFactory;

$editor = EditorFactory::createEditor();
```
## Further documentation

You can see the current and past versions using one of the following:

* the `git tag` command
* the [releases page on Github](https://github.com/gnugat/redaktilo/releases)
* the file listing the [changes between versions](CHANGELOG.md)

Next readings:

* [Tutorial](doc/01-tutorial.md)
* [Use cases](doc/02-use-cases.md)
* [Reference](doc/03-reference.md)
* [Vocabulary](doc/04-vocabulary.md)
* [Extending](doc/05-extending.md)
* [Exceptions](doc/06-exceptions.md)
