# Utopia Cache

Utopia framework cache library is simple and lite library for managing application cache storing, loading and purging. This library is aiming to be as simple and easy to learn and use.

Although this library is part of the [Utopia Framework](https://github.com/utopia-php/framework) project it is dependency free and can be used as standalone with any other PHP project or framework.

## Getting Started

**File System Adapter**

```php
<?php

require_once __DIR__ . '/../../vendor/autoload.php';

use Utopia\Cache\Cache;
use Utopia\Cache\Filesystem;

$cache  = new Cache(new Filesystem('/cache-dir'));
$key    = 'data-from-example.com';

$data   = $cache->load($key, 60 * 60 * 24 * 30 * 3 /* 3 months */);

if(!$data) {
    $data = file_get_contents('https://example.com');
    
    $cache->save($key, $data);
}

echo $data;

```

Usage with callback:

```php
<?php

require_once __DIR__ . '/../../vendor/autoload.php';

use Utopia\Cache\Cache;
use Utopia\Cache\Filesystem;

$cache  = new Cache(new Filesystem('/cache-dir'));

$data   = $cache->load('data-from-example.com', 60 * 60 * 24 * 30 * 3 /* 3 months */, function () {
    return file_get_contents('https://example.com'); // If no valid cache, execute the callback
});

echo $data;

```

## Contribute

Currently we support only a Filesystem adapter for usage as a cache storage, send a pull request to add redis, memcached or any other storage adapter you might need to use with this library.

## System Requirements

Utopia Framework requires PHP 7.1 or later. We recommend using the latest PHP version whenever possible.

## Authors

**Eldad Fux**

+ [https://twitter.com/eldadfux](https://twitter.com/eldadfux)
+ [https://github.com/eldadfux](https://github.com/eldadfux)

## Copyright and license

The MIT License (MIT) [http://www.opensource.org/licenses/mit-license.php](http://www.opensource.org/licenses/mit-license.php)