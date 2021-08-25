## Table of Contents

* [Introduction](#introduction)
* [How objects are defined](#how-objects-are-defined)
  * [Python classes](#python-classes)
  * [Angular components](#angular-components)
* [Create a new object](#create-a-new-object)
* [Using objects](#using-objects)

## Introduction

When collecting user input, we often define the kind of input we expect using [[schemas|Schemas]]. These schemas can describe arbitrarily nested collections of base types we call _objects_. For example, consider this schema:

```json
{
  "type": "dict",
  "properties": [
    {
      "name": "version",
      "schema": {
        "type": "int"
      }
    }
  ]
}
```

The schema would match a dictionary like this:

```json
{"version": 34}
```

The `dict` type is a collection, but the `int` type is an object. We define these objects as classes in [`extensions/objects/models/objects.py`](https://github.com/oppia/oppia/blob/develop/extensions/objects/models/objects.py) and components in [`extensions.objects/templates`](https://github.com/oppia/oppia/blob/develop/extensions/objects/templates).

## How objects are defined

### Python classes

The Python classes for objects are defined in `objects.py`. For example, here's the class for the `int` type:

```python
class Int(BaseObject):
    """Integer class."""

    description = 'An integer.'
    default_value = 0

    @classmethod
    def get_schema(cls):
        """Returns the object schema.

        Returns:
            dict. The object schema.
        """
        return {
            'type': 'int'
        }
```

Object classes all meet the following criteria:

* Inherit from either `BaseObject` or another object class.
* Set the class variable `description` to a string describing the object.
* Set the class variable `default_value` to the value that should be the default whenever this type is used in a rule. Note that this variable is technically not required if the object will never be used in a [[rule|Creating-rules]].
* Provide a `normalize` class method that accepts a raw Python object. The method should first validate the raw object to check whether it is malformed. If the validation checks pass, then the method should return a normalized form of the object. Note that in this context, "normalized" means a primitive Python type or multiple primitive types combined with lists and/or dicts.

  * The `BaseObject` class provides a `normalize` class method that can handle normalization for you so long as your object class provides a `get_schema` class method that returns a schema describing the object. `BaseObject.normalize` passes your schema to `schema_utils.normalize_against_schema`, so make sure that `normalize_against_schema` won't try to normalize your object to your schema using your object class. Otherwise, you'll get an endless loop between `normalize_against_schema` and `BaseObject.normalize`.

### Angular components

Every object is accompanied by a component defined in `extensions/objects/templates` and imported in `extensions/objects/object-components.module.ts`. Each component provides the HTML and frontend code needed to create a form for the user to provide input in the form of the object. These components rely heavily on [schema-based forms](https://github.com/oppia/oppia/wiki/Schemas#schema-based-forms). For example, the `int-editor` component's HTML is just this:

```html
<schema-based-editor [schema]="getSchema.bind(this)"
                     [localValue]="value"
                     (localValueChange)="updateValue($event)">
</schema-based-editor>
```

The `getSchema` function is defined in `int-editor.component.ts` and returns this schema:

```json
{
  type: "int",
  validators: [{
    id: "is_integer"
  }]
}
```

The `schema-based-editor` component already knows how to construct a form for this schema.

## Create a new object

Let's suppose you're creating a new object called `MyObject` (in practice you should use a more descriptive name). You'll need to follow these steps:

1. Create a new [object class](#python-classes) named `MyObject`.
2. Add tests for your class in `extensions/objects/models/objects_test.py`. You should add normalization tests to the `ObjectNormalizationUnitTests` class. You can also create a new test class to hold additional test cases.
3. Add a new [Angular component](#angular-components) to accept input in the form of your object. Your component files should be named `my-object-editor.component.*`, and your component class should be named `MyObjectEditorComponent`.
4. Import your component in `extensions/objects/object-components.module.ts` and add it to the module there.

## Using objects

You are unlikely to use objects directly. Instead, you will reference them as you [[create interactions|Creating-Interactions]], [[define rules|Creating-Rules]], or otherwise use [[schemas|Schemas]].
