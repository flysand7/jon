
# JON

JON - Joined object notation. A configuration format made to occupy small
space on screen and be easier to write compared to JSON.

## Basic syntax example:

JSON:

```json
{
    "name": "Jon",
    "age": 30,
    "hobbies": [
        "programming",
        "baking",
        "chilling",
    ],
    "contacts": {
        "phone": "123456",
        "email": "jon@jon.com",
    },
}
```

JON:

```
name "Jon"
age 30
hobbies [
    'programming'
    'baking'
    'chilling'
]
contacts {
    phone '123456'
    email 'jon@jon.com'
}
```

1. JSON requires root object explicitly specified, in JON the root object is implied
2. JSON requires the keys to be quoted, in JON the keys of the object must be unquoted
3. JON removes the need for `:` separating keys and values
4. in JON commas are optional, instead you can separate fields with newlines

## Object and array merging

Given the earlier example, JON allows merging multiple fields with the same name to be merged
into an array, or merging kv pairs into objects. Assume the earlier example of an object, then
you could specify the person as:

```json
name 'Jon'
age 30
hobbies 'programming'
hobbies 'baking'
hobbies 'chilling'
contacts phone '123456'
contacts email 'jon@jon.com'
```

A reasonable question to ask here is how do you specify an array of length 1. This is one of
the weird parts of JON, it requires the implementation to behave a certain way. There are
two ways you can use a JON parser for your purposes:

1. Manually retrieve the fields via the `get_array`, `get_string` and similar calls.
2. Deserialize into native object

For the first case, `get_array(object, key)` function would return an array of size one
even if the field under the key `key` is not an array. It shall create a new array containing
that element.

For the second case the handling is a bit more difficult, please check out reference Odin
implementation.
