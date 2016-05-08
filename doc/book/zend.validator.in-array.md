# InArray Validator

`Zend\Validator\InArray` allows you to validate if a given value is contained within an array. It is
also able to validate multidimensional arrays.

## Supported options for Zend\\Validator\\InArray

The following options are supported for `Zend\Validator\InArray`:

- **haystack**: Sets the haystack for the validation.
- **recursive**: Defines if the validation should be done recursive. This option defaults to
`FALSE`.
- **strict**: Three modes of comparison are offered owing to an often overlooked, and potentially
dangerous security issue when validating string input from user input.
- *InArray::COMPARE\_STRICT*

        > This is a normal in\_array strict comparison that checks value and type.

- *InArray::COMPARE\_NOT\_STRICT*

        > This is a normal in\_array non-strict comparison that checks value only.

> ## Warning
This mode may give false positives when strings are compared against ints or floats owing to
in\_array's behaviour of converting strings to int in such cases. Therefore, *"foo"* would become
*0*, *"43foo"* would become *43*, while *"foo43"* would also become *0*.

Defines if the validation should be done strict. This option defaults to `FALSE`.

## Simple array validation

The simplest way, is just to give the array which should be searched against at initiation:

```php
$validator = new Zend\Validator\InArray(array('haystack' => array('value1', 'value2',...'valueN')));
if ($validator->isValid('value')) {
    // value found
} else {
    // no value found
}
```

This will behave exactly like *PHP*'s `in_array()` method.

> ## Note
Per default this validation is not strict nor can it validate multidimensional arrays.

Alternatively, you can define the array to validate against after object construction by using the
`setHaystack()` method. `getHaystack()` returns the actual set haystack array.

```php
$validator = new Zend\Validator\InArray();
$validator->setHaystack(array('value1', 'value2',...'valueN'));

if ($validator->isValid('value')) {
    // value found
} else {
    // no value found
}
```

## Array validation modes

As previously mentioned, there are possible security issues when using the default non-strict
comparison mode, so rather than restricting the developer, we've chosen to offer both strict and
non-strict comparisons and adding a safer middle-ground.

It's possible to set the strict mode at initialisation and afterwards with the `setStrict` method.
`InArray::COMPARE_STRICT` equates to `true` and
`InArray::COMPARE_NOT_STRICT_AND_PREVENT_STR_TO_INT_VULNERABILITY` equates to false.

```php
// defaults to InArray::COMPARE_NOT_STRICT_AND_PREVENT_STR_TO_INT_VULNERABILITY
$validator = new Zend\Validator\InArray(
    array(
         'haystack' => array('value1', 'value2',...'valueN'),
    )
);

// set strict mode
$validator = new Zend\Validator\InArray(
    array(
         'haystack' => array('value1', 'value2',...'valueN'),
         'strict'   => InArray::COMPARE_STRICT  // equates to ``true``
    )
);

// set non-strict mode  
$validator = new Zend\Validator\InArray(
    array(
         'haystack' => array('value1', 'value2',...'valueN'),
         'strict'   => InArray:COMPARE_NOT_STRICT  // equates to ``false``
    )
);

// or

$validator->setStrict(InArray::COMPARE_STRICT); 
$validator->setStrict(InArray::COMPARE_NOT_STRICT);
$validator->setStrict(InArray::COMPARE_NOT_STRICT_AND_PREVENT_STR_TO_INT_VULNERABILITY);
```

> ## Note
Note that the **strict** setting is per default `FALSE`.

## Recursive array validation

In addition to *PHP*'s `in_array()` method this validator can also be used to validate
multidimensional arrays.

To validate multidimensional arrays you have to set the **recursive** option.

```php
$validator = new Zend\Validator\InArray(
    array(
        'haystack' => array(
            'firstDimension' => array('value1', 'value2',...'valueN'),
            'secondDimension' => array('foo1', 'foo2',...'fooN')),
        'recursive' => true
    )
);

if ($validator->isValid('value')) {
    // value found
} else {
    // no value found
}
```

Your array will then be validated recursively to see if the given value is contained. Additionally
you could use `setRecursive()` to set this option afterwards and `getRecursive()` to retrieve it.

```php
$validator = new Zend\Validator\InArray(
    array(
        'firstDimension' => array('value1', 'value2',...'valueN'),
        'secondDimension' => array('foo1', 'foo2',...'fooN')
    )
);

$validator->setRecursive(true);

if ($validator->isValid('value')) {
    // value found
} else {
    // no value found
}
```

> ## Note
#### Default setting for recursion
Per default the recursive validation is turned off.

> ## Note
#### Option keys within the haystack
When you are using the keys '`haystack`', '`strict`' or '`recursive`' within your haystack, then you
must wrap the `haystack` key.
