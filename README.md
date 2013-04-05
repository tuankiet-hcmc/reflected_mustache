# Mustache templates

A Dart library to parse and render [mustache templates](http://mustache.github.com/mustache.5.html).

[![Build Status](https://drone.io/github.com/xxgreg/mustache/status.png)](https://drone.io/github.com/xxgreg/mustache/latest)

## Example
```dart
	import 'package:mustache/mustache.dart' as mustache;

	main() {
		var source = '{{#names}}<div>{{lastname}}, {{firstname}}</div>{{/names}}';
		var template = mustache.parse(source);
		var output = template.renderString({'names': [
			{'firstname': 'Greg', 'lastname': 'Lowe'},
			{'firstname': 'Bob', 'lastname': 'Johnson'}
		]});
		print(output);
	}
```

## API

```dart

Template parse(String source, {bool lenient : false});

abstract class Template {
	String renderString(values, {bool lenient : false});
	void render(values, StringSink sink, {bool lenient : false});
}

```

Once a template has been created it can be rendered any number of times.

Both parse and render throw a FormatException if there is a problem with the template or rendering the values.

When lenient mode is enabled tag names may use any characters, otherwise only a-z, A-Z, 0-9, underscore and minus. Lenient mode will also silently ignore nulls passed as values.


## Supported 
```
 Variables             {{var-name}}
 Sections              {{#section}}Blah{{/section}}
 Inverse sections      {{^section}}Blah{{/section}}
 Comments              {{! Not output. }}
```
See the [mustache templates tutorial](http://mustache.github.com/mustache.5.html) for more information.

## To do
```
Escape tags {{{ ... }}}, and {{& ... }}
Partial tags {{>partial}}
Allow functions as values (See mustache docs)
Collect some test files, make a test harness to compare the output against another mustache lib.
```

