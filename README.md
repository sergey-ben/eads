[![Maintainability](https://api.codeclimate.com/v1/badges/1ee47671ee08764bfcc8/maintainability)](https://codeclimate.com/github/aaronbullard/eads/maintainability)


# EADS Utility
PHP Utility for Enterprise APIs for Data Sharing Standard

https://eads.540.co/


## Filtering

This is a helper class to translate a string of filters into usable sql.

Example query:
 - `?filters=status==verified,age>18,weight>=<150;200`

This query translates to:
 - WHERE status = 'verified'
 - AND age > 18
 - AND weight BETWEEN 150 AND 200

## Installation
```php
composer require aaronbullard/eads
```

## Usage
See the tests for usage and examples `/tests`

```php
// GET `?filters=status==verified,age>18,weight>=<150;200`

$filterString = Request::get('filters');

$parser = new EADS\Filters\Parser($filterString);

// Get first query
$filter = $parser->getFilters()[0];
$sql = $filter->getSQL(); // "status = ?"
$bindings = $filter->getBindings(); // ['verified']
```

or

```php
// GET `?filters=status==verified,age>18,weight>=<150;200`

$filterString = Request::get('filters');

$filters = EADS::filters($filterString);

// Get first query
$filter = $filters[0];
$sql = $filter->getSQL(); // "status = ?"
$bindings = $filter->getBindings(); // ['verified']
```

## License
The package is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
