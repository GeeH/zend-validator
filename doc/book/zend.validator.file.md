# File Validation Classes

Zend Framework comes with a set of classes for validating files, such as file size validation and
CRC checking.

> ## Note
All of the File validators' `filter()` methods support both a file path `string` *or* a `$_FILES`
array as the supplied argument. When a `$_FILES` array is passed in, the `tmp_name` is used for the
file path.

## Crc32

`Zend\Validator\File\Crc32` allows you to validate if a given file's hashed contents matches the
supplied crc32 hash(es). It is subclassed from the \[Hash validator\](zend.validator.file.hash) to
provide a convenient validator that only supports the `crc32` algorithm.

> ## Note
This validator requires the [Hash extension](http://php.net/manual/en/book.hash.php) from PHP with
the `crc32` algorithm.

### Supported Options

The following set of options are supported:

- **hash** `(string)`  
    Hash to test the file against.

### Usage Examples

```php
// Does file have the given hash?
$validator = new \Zend\Validator\File\Crc32('3b3652f');

// Or, check file against multiple hashes
$validator = new \Zend\Validator\File\Crc32(array('3b3652f', 'e612b69'));

// Perform validation with file path
if ($validator->isValid('./myfile.txt')) {
    // file is valid
}
```

### Public Methods

getCrc32()

> Returns the current set of crc32 hashes.
rtype  
`array`
addCrc32(string|array $options)

> Adds a crc32 hash for one or multiple files to the internal set of hashes.
param $options  
See \[Supported Options\](zend.validator.file.crc32.options) section for more information.
setCrc32(string|array $options)

> Sets a crc32 hash for one or multiple files. Removes any previously set hashes.
param $options  
See \[Supported Options\](zend.validator.file.crc32.options) section for more information.
## ExcludeExtension

`Zend\Validator\File\ExcludeExtension` checks the extension of files. It will assert `false` when a
given file has one the a defined extensions.

This validator is inversely related to the \[Extension validator\](zend.validator.file.extension).

Please refer to the \[Extension validator\](zend.validator.file.extension.options) for options and
usage examples.

## ExcludeMimeType

`Zend\Validator\File\ExcludeMimeType` checks the MIME type of files. It will assert `false` when a
given file has one the a defined MIME types.

This validator is inversely related to the \[MimeType validator\](zend.validator.file.mime-type).

Please refer to the \[MimeType validator\](zend.validator.file.mime-type) for options and usage
examples.

## Exists

`Zend\Validator\File\Exists` checks for the existence of files in specified directories.

This validator is inversely related to the \[NotExists validator\](zend.validator.file.not-exists).

### Supported Options

The following set of options are supported:

- **directory** `(string|array)`  
    Comma-delimited string (or array) of directories.

### Usage Examples

```php
// Only allow files that exist in ~both~ directories
$validator = new \Zend\Validator\File\Exists('/tmp,/var/tmp');

// ...or with array notation
$validator = new \Zend\Validator\File\Exists(array('/tmp', '/var/tmp'));

// Perform validation
if ($validator->isValid('/tmp/myfile.txt')) {
    // file is valid
}
```

> ## Note
This validator checks whether the specified file exists in **all** of the given directories. The
validation will fail if the file does not exist in one (or more) of the given directories.

## Extension

`Zend\Validator\File\Extension` checks the extension of files. It will assert `true` when a given
file has one the a defined extensions.

This validator is inversely related to the \[ExcludeExtension
validator\](zend.validator.file.exclude-extension).

### Supported Options

The following set of options are supported:

- **extension** `(string|array)`  
    Comma-delimited string (or array) of extensions to test against.

- **case** `(boolean) default: "false"`  
    Should comparison of extensions be case-sensitive?

### Usage Examples

```php
// Allow files with 'php' or 'exe' extensions
$validator = new \Zend\Validator\File\Extension('php,exe');

// ...or with array notation
$validator = new \Zend\Validator\File\Extension(array('php', 'exe'));

// Test with case-sensitivity on
$validator = new \Zend\Validator\File\Extension(array('php', 'exe'), true);

// Perform validation
if ($validator->isValid('./myfile.php')) {
    // file is valid
}
```

### Public Methods

addExtension(string|array $options)

> Adds extension(s) via a comma-delimited string or an array.

## Hash

`Zend\Validator\File\Hash` allows you to validate if a given file's hashed contents matches the
supplied hash(es) and algorithm(s).

> ## Note
This validator requires the [Hash extension](http://php.net/manual/en/book.hash.php) from PHP. A
list of supported hash algorithms can be found with the [hash\_algos()
function](http://php.net/manual/en/function.hash-algos.php).

### Supported Options

The following set of options are supported:

- **hash** `(string)`  
    Hash to test the file against.

- **algorithm** `(string) default: "crc32"`  
    Algorithm to use for the hashing validation.

### Usage Examples

```php
// Does file have the given hash?
$validator = new \Zend\Validator\File\Hash('3b3652f', 'crc32');

// Or, check file against multiple hashes
$validator = new \Zend\Validator\File\Hash(array('3b3652f', 'e612b69'), 'crc32');

// Perform validation with file path
if ($validator->isValid('./myfile.txt')) {
   // file is valid
}
```

### Public Methods

getHash()

> Returns the current set of hashes.
rtype  
`array`
addHash(string|array $options)

> Adds a hash for one or multiple files to the internal set of hashes.
param $options  
See \[Supported Options\](zend.validator.file.hash.options) section for more information.
setHash(string|array $options)

> Sets a hash for one or multiple files. Removes any previously set hashes.
param $options  
See \[Supported Options\](zend.validator.file.hash.options) section for more information.
## ImageSize

`Zend\Validator\File\ImageSize` checks the size of image files. Minimum and/or maximum dimensions
can be set to validate against.

### Supported Options

The following set of options are supported:

- **minWidth** `(int|null) default: null`
- **minHeight** `(int|null) default: null`
- **maxWidth** `(int|null) default: null`
- **maxHeight** `(int|null) default: null`  
    To bypass validation of a particular dimension, the relevant option should be set to `null`.

### Usage Examples

```php
// Is image size between 320x200 (min) and 640x480 (max)?
$validator = new \Zend\Validator\File\ImageSize(320, 200, 640, 480);

// ...or with array notation
$validator = new \Zend\Validator\File\ImageSize(array(
    'minWidth' => 320, 'minHeight' => 200,
    'maxWidth' => 640, 'maxHeight' => 480,
));

// Is image size equal to or larger than 320x200?
$validator = new \Zend\Validator\File\ImageSize(array(
    'minWidth' => 320, 'minHeight' => 200,
));

// Is image size equal to or smaller than 640x480?
$validator = new \Zend\Validator\File\ImageSize(array(
    'maxWidth' => 640, 'maxHeight' => 480,
));

// Perform validation with file path
if ($validator->isValid('./myfile.jpg')) {
    // file is valid
}
```

### Public Methods

getImageMin()

> Returns the minimum dimensions (width and height)
rtype  
`array`
getImageMax()

> Returns the maximum dimensions (width and height)
rtype  
`array`
## IsCompressed

`Zend\Validator\File\IsCompressed` checks if a file is a compressed archive, such as zip or gzip.
This validator is based on the \[MimeType validator\](zend.validator.file.mime-type) and supports
the same methods and options.

The default list of [compressed file MIME
types](https://github.com/zendframework/zf2/blob/master/library/Zend/Validator/File/IsCompressed.php#L48)
can be found in the source code.

Please refer to the \[MimeType validator\](zend.validator.file.mime-type) for options and public
methods.

### Usage Examples

```php
$validator = new \Zend\Validator\File\IsCompressed();
if ($validator->isValid('./myfile.zip')) {
    // file is valid
}
```

## IsImage

`Zend\Validator\File\IsImage` checks if a file is an image, such as jpg or png. This validator is
based on the \[MimeType validator\](zend.validator.file.mime-type) and supports the same methods and
options.

The default list of [image file MIME
types](https://github.com/zendframework/zf2/blob/master/library/Zend/Validator/File/IsImage.php#L49)
can be found in the source code.

Please refer to the \[MimeType validator\](zend.validator.file.mime-type) for options and public
methods.

### Usage Examples

```php
$validator = new \Zend\Validator\File\IsImage();
if ($validator->isValid('./myfile.jpg')) {
    // file is valid
}
```

## Md5

`Zend\Validator\File\Md5` allows you to validate if a given file's hashed contents matches the
supplied md5 hash(es). It is subclassed from the \[Hash validator\](zend.validator.file.hash) to
provide a convenient validator that only supports the `md5` algorithm.

> ## Note
This validator requires the [Hash extension](http://php.net/manual/en/book.hash.php) from PHP with
the `md5` algorithm.

### Supported Options

The following set of options are supported:

- **hash** `(string)`  
    Hash to test the file against.

### Usage Examples

```php
// Does file have the given hash?
$validator = new \Zend\Validator\File\Md5('3b3652f336522365223');

// Or, check file against multiple hashes
$validator = new \Zend\Validator\File\Md5(array(
    '3b3652f336522365223', 'eb3365f3365ddc65365'
));

// Perform validation with file path
if ($validator->isValid('./myfile.txt')) {
    // file is valid
}
```

### Public Methods

getMd5()

> Returns the current set of md5 hashes.
rtype  
`array`
addMd5(string|array $options)

> Adds a md5 hash for one or multiple files to the internal set of hashes.
param $options  
See \[Supported Options\](zend.validator.file.md5.options) section for more information.
setMd5(string|array $options)

> Sets a md5 hash for one or multiple files. Removes any previously set hashes.
param $options  
See \[Supported Options\](zend.validator.file.md5.options) section for more information.
## MimeType

`Zend\Validator\File\MimeType` checks the MIME type of files. It will assert `true` when a given
file has one the a defined MIME types.

This validator is inversely related to the \[ExcludeMimeType
validator\](zend.validator.file.exclude-mime-type).

> ## Note
This component will use the `FileInfo` extension if it is available. If it's not, it will degrade to
the `mime_content_type()` function. And if the function call fails it will use the MIME type which
is given by HTTP. You should be aware of possible security problems when you do not have `FileInfo`
or `mime_content_type()` available. The MIME type given by HTTP is not secure and can be easily
manipulated.

### Supported Options

The following set of options are supported:

- **mimeType** `(string|array)`  
    Comma-delimited string (or array) of MIME types to test against.

- **magicFile** `(string|null) default: "MAGIC" constant`  
    Specify the location of the magicfile to use. By default the `MAGIC` constant value will be
used.

- **enableHeaderCheck** `(boolean) default: "false"`  
    Check the HTTP Information for the file type when the fileInfo or mimeMagic extensions can not
be found.

### Usage Examples

```php
// Only allow 'gif' or 'jpg' files
$validator = new \Zend\Validator\File\MimeType('image/gif,image/jpg');

// ...or with array notation
$validator = new \Zend\Validator\File\MimeType(array('image/gif', 'image/jpg'));

// ...or restrict an entire group of types
$validator = new \Zend\Validator\File\MimeType(array('image', 'audio'));

// Use a different magicFile
$validator = new \Zend\Validator\File\MimeType(array(
    'image/gif', 'image/jpg',
    'magicFile' => '/path/to/magicfile.mgx'
));

// Use the HTTP information for the file type
$validator = new \Zend\Validator\File\MimeType(array(
    'image/gif', 'image/jpg',
    'enableHeaderCheck' => true
));

// Perform validation
if ($validator->isValid('./myfile.jpg')) {
    // file is valid
}
```

> ## Warning
Allowing "groups" of MIME types will accept **all** members of this group even if your application
does not support them. When you allow 'image' you also allow 'image/xpixmap' and 'image/vasa' which
could be problematic.

## NotExists

`Zend\Validator\File\NotExists` checks for the existence of files in specified directories.

This validator is inversely related to the \[Exists validator\](zend.validator.file.exists).

### Supported Options

The following set of options are supported:

- **directory** `(string|array)`  
    Comma-delimited string (or array) of directories.

### Usage Examples

```php
// Only allow files that do not exist in ~either~ directories
$validator = new \Zend\Validator\File\NotExists('/tmp,/var/tmp');

// ...or with array notation
$validator = new \Zend\Validator\File\NotExists(array('/tmp', '/var/tmp'));

// Perform validation
if ($validator->isValid('/home/myfile.txt')) {
    // file is valid
}
```

> ## Note
This validator checks whether the specified file does not exist in **any** of the given directories.
The validation will fail if the file exists in one (or more) of the given directories.

## Sha1

`Zend\Validator\File\Sha1` allows you to validate if a given file's hashed contents matches the
supplied sha1 hash(es). It is subclassed from the \[Hash validator\](zend.validator.file.hash) to
provide a convenient validator that only supports the `sha1` algorithm.

> ## Note
This validator requires the [Hash extension](http://php.net/manual/en/book.hash.php) from PHP with
the `sha1` algorithm.

### Supported Options

The following set of options are supported:

- **hash** `(string)`  
    Hash to test the file against.

### Usage Examples

```php
// Does file have the given hash?
$validator = new \Zend\Validator\File\Sha1('3b3652f336522365223');

// Or, check file against multiple hashes
$validator = new \Zend\Validator\File\Sha1(array(
    '3b3652f336522365223', 'eb3365f3365ddc65365'
));

// Perform validation with file path
if ($validator->isValid('./myfile.txt')) {
    // file is valid
}
```

### Public Methods

getSha1()

> Returns the current set of sha1 hashes.
rtype  
`array`
addSha1(string|array $options)

> Adds a sha1 hash for one or multiple files to the internal set of hashes.
param $options  
See \[Supported Options\](zend.validator.file.sha1.options) section for more information.
setSha1(string|array $options)

> Sets a sha1 hash for one or multiple files. Removes any previously set hashes.
param $options  
See \[Supported Options\](zend.validator.file.sha1.options) section for more information.
## Size

`Zend\Validator\File\Size` checks for the size of a file.

### Supported Options

The following set of options are supported:

- **min** `(integer|string) default: null`
- **max** `(integer|string) default: null`  
    The integer number of bytes, or a string in SI notation (ie. 1kB, 2MB, 0.2GB).

    The accepted SI notation units are: kB, MB, GB, TB, PB, and EB. All sizes are converted using
1024 as the base value (ie. 1kB == 1024 bytes, 1MB == 1024kB).

- **useByteString** `(boolean) default: true`  
    Display error messages with size in user-friendly number or with the plain byte size.

### Usage Examples

```php
// Limit the file size to 40000 bytes
$validator = new \Zend\Validator\File\Size(40000);

// Limit the file size to between 10kB and 4MB
$validator = new \Zend\Validator\File\Size(array(
    'min' => '10kB', 'max' => '4MB'
));

// Perform validation with file path
if ($validator->isValid('./myfile.txt')) {
    // file is valid
}
```

## UploadFile

`Zend\Validator\File\UploadFile` checks whether a single file has been uploaded via a form `POST`
and will return descriptive messages for any upload errors.

> ## Note
\[Zend\\InputFilter\\FileInput\](zend.input-filter.file-input) will automatically prepend this
validator in it's validation chain.

### Usage Examples

```php
use Zend\Http\PhpEnvironment\Request;

$request = new Request();
$files   = $request->getFiles();
// i.e. $files['my-upload']['error'] == 0

$validator = new \Zend\Validator\File\UploadFile();
if ($validator->isValid($files['my-upload'])) {
    // file is valid
}
```

## WordCount

`Zend\Validator\File\WordCount` checks for the number of words within a file.

### Supported Options

The following set of options are supported:

- **min** `(integer) default: null`
- **max** `(integer) default: null`  
    The number of words allowed.

### Usage Examples

```php
// Limit the amount of words to a maximum of 2000
$validator = new \Zend\Validator\File\WordCount(2000);

// Limit the amount of words to between 100 and 5000
$validator = new \Zend\Validator\File\WordCount(100, 5000);

// ... or with array notation
$validator = new \Zend\Validator\File\WordCount(array(
    'min' => 1000, 'max' => 5000
));

// Perform validation with file path
if ($validator->isValid('./myfile.txt')) {
    // file is valid
}
```
