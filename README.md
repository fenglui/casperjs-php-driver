Fork of the Original CasperJS PHP Driver
https://github.com/DiceHoldingsInc/casperjs-php-driver

### Changelog

- Accept Language fix
- Custom CasperJS Path fix
- SetCookies, LoadCookies, SaveCookies methods
- AppendToScript method


## Installation
You can use this package in your project via composer. Add these lines to your `composer.json`:
```
"require": {
  "pruiti/casperjs-php-driver": "1.*"
},
…
```

or

```
composer require pruiti/casperjs-php-driver
```

Latest stable release is 1.0

## Examples

### Basic usage
```php
$driver = new CasperJs\Driver();
$output = $driver->start('http://someurl.com')
                 ->run();
```

### Setting request parameters and interacting with the page
The entire point of using a tool like Casper is to be able to properly interact with the DOM for both testing and scraping purposes. This driver tries to expose a friendly interface to do so where you can define both request params and DOM interaction before making the actual call.

```php
$driver = new CasperJs\Driver();
$driver->start('http://someurl.com')
       ->setUserAgent('AmericanPizzaiolo')
       ->setHeaders([
           'Accept-Language' => ['en-US'],
           'Some-Header' => 'Foo-bar',
       ])
       ->evaluate('make me a pizza')
       ->setViewPort(1024, 768)
       ->waitForSelector('.selector', 30000)
       ->wait(10000)
       ->click('.selector');

$output = $driver->run();
```

### Using a proxy for your call
```php
$driver = new CasperJs\Driver();
$driver->start('http://someurl.com')
       ->useProxy('1.1.1.1');

$output = $driver->run();
```

## Getting the Casper Output

Whenever you execute `Driver::run()` the `Driver` will return an `Output` object that will encapsulate the Casper output. `Output` will expose the captured casper data or throw an exception in case the desired behaviour wasn't performed (i.e. if a css selector to be present in the page after timeout expired).

### Extracting Data
```php
$html = $output->getHtml();
$statusCode = $output->getStatusCode();
$currentUrl = $output->getCurrentUrl();
```

## More examples
For more examples check out `test/DriverTest.php`

## Credits
This driver is essentially an enhanced and improved version of [the original alwex/php-casperjs](https://github.com/alwex/php-casperjs).
