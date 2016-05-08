# Digits Validator

`Zend\Validator\Digits` validates if a given value contains only digits.

## Supported options for Zend\\Validator\\Digits

There are no additional options for `Zend\Validator\Digits`:

## Validating digits

To validate if a given value contains only digits and no other characters, simply call the validator
like shown in this example:

```php
$validator = new Zend\Validator\Digits();

$validator->isValid("1234567890"); // returns true
$validator->isValid(1234);         // returns true
$validator->isValid('1a234');      // returns false
```

> ## Note
#### Validating numbers
When you want to validate numbers or numeric values, be aware that this validator only validates
digits. This means that any other sign like a thousand separator or a comma will not pass this
validator. In this case you should use `Zend\I18n\Validator\Int` or `Zend\I18n\Validator\Float`.
