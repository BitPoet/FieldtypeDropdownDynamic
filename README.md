# FieldtypeDropdownDynamic

Dropdown (select) Fieldtype for the ProcessWire CMS.

Note: this module is still in Beta and prone to have errors. Use at your own risks.

## Requires

ProcessWire 2.5 or higher

## Description

Most times, a regular FieldtypeSelect is exactly what you need to populate a field
in your ProcessWire template, even if you don't think so at first. Whenever you
want to provide both consistency and permanency for selection options, pages
the way to go, because they make the link between linking page (the page with
the select field) and the selected page permanent. And really, database storage
doesn't get much smoother than storing your selection list as pages.

With that out of the way, there are some cases, e.g. when pulling in data from
foreign systems or making heavy use of file system contents, where that pages
approach may get clunky.

## How it works

FieldtypeDropdownDynamic is an extension to FieldtypeText, so make sure that you
don't deal with float values or the likes.

When you add a field and set its type to FieldtypeDropdownDynamic, you'll see two
configuration options:

### The code textarea

This textarea either holds the PHP code that fills your dropdown list, which is
just a simple InputfieldSelect. To fill it, you need to return an array holding
an associative array for each selection entry. Here's a very simple example:

```php
return array(
	array("label" => "First option", value => "first"),
	array("label" => "Second option", value => "second")
);
```

Of course you can use all ProcessWire APIs and any included functions there as
well. You might make a call to a webservice somewhere or even populate your
list with values created through (string) rand(1, 9999999)... it's your choice.

### The include file checkbox

If this option is checked, the contents of the checkbox above it will be used
as the relative path to a PHP include file instead of being evaluated directly.
This include, of course, will also need to return() a fitting array that populates
the dropdown.

The path used there is relative your site's template path.

## Tips and Tricks

### Option Groups

As FieldtypeDropdownDynamic uses InputfieldSelect under the hood, it also allows
you to pass option groups to the select. The downside is that you can't pass
attributes to your nested options.

Example:

```php
return array(
	array("label" => "first", "value" => "firstval"),
	array("value" => "Option Group Title", "label" => array(
		"second" => "secondval",
		"third" => "thirdval"
	)),
	array("label" => "fourth", "value" => "fourthval")
);
```

This code populates the dropdown like this:

![Example Image](https://bitpoet.github.io/img/dddynexample1.png)

## License

This module is released under the MIT license (see LICENSE.TXT). Use it however it
pleases you.
