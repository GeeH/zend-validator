# Standard Validation Classes

Zend Framework comes with a standard set of validation classes, which are ready for you to use.

## Included Validators

- \[Alnum\](zend.i18n.validator.alnum)
- \[Alpha\](zend.i18n.validator.alpha)
- \[Barcode\](zend.validator.barcode)
- \[Between\](zend.validator.between)
- \[Callback\](zend.validator.callback)
- \[CreditCard\](zend.validator.creditcard)
- \[Date\](zend.validator.date)
- \[Db\\RecordExists and Db\\NoRecordExists\](zend.validator.db)
- \[Digits\](zend.validator.digits)
- \[EmailAddress\](zend.validator.email\_address)
- \[File Validation Classes\](zend.validator.file)
- \[GreaterThan\](zend.validator.greaterthan)
- \[Hex\](zend.validator.hex)
- \[Hostname\](zend.validator.hostname)
- \[Iban\](zend.validator.iban)
- \[Identical\](zend.validator.identical)
- \[InArray\](zend.validator.in\_array)
- \[Ip\](zend.validator.ip)
- \[Isbn\](zend.validator.isbn)
- \[IsFloat\](zend.i18n.validator.float)
- \[IsInt\](zend.i18n.validator.int)
- \[LessThan\](zend.validator.lessthan)
- \[NotEmpty\](zend.validator.notempty)
- \[PostCode\](zend.validator.post\_code)
- \[Regex\](zend.validator.regex)
- \[Sitemap\](zend.validator.sitemap)
- \[Step\](zend.validator.step)
- \[StringLength\](zend.validator.stringlength)
- \[Timezone\](zend.validator.timezone)
- \[Uri\](zend.validator.uri)

## Deprecated Validators

### Ccnum

The `Ccnum` validator has been deprecated in favor of the `CreditCard` validator. For security
reasons you should use CreditCard instead of Ccnum.
