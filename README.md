[![Build Status](https://travis-ci.org/VIPnytt/SitemapParser.svg?branch=master)](https://travis-ci.org/VIPnytt/X-Robots-Tag-parser)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/VIPnytt/SitemapParser/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/VIPnytt/SitemapParser/?branch=master)
[![Code Climate](https://codeclimate.com/github/VIPnytt/SitemapParser/badges/gpa.svg)](https://codeclimate.com/github/VIPnytt/SitemapParser)
[![Test Coverage](https://codeclimate.com/github/VIPnytt/SitemapParser/badges/coverage.svg)](https://codeclimate.com/github/VIPnytt/SitemapParser/coverage)
[![License](https://poser.pugx.org/VIPnytt/SitemapParser/license)](https://github.com/VIPnytt/SitemapParser/blob/master/LICENSE)
[![Packagist](https://img.shields.io/packagist/v/VIPnytt/SitemapParser.svg)](https://packagist.org/packages/VIPnytt/SitemapParser)
[![Join the chat at https://gitter.im/VIPnytt/SitemapParser](https://badges.gitter.im/VIPnytt/SitemapParser.svg)](https://gitter.im/VIPnytt/SitemapParser)

# XML Sitemap parser
An easy-to-use PHP library to parse XML Sitemaps compliant with the [Sitemaps.org protocol](http://www.sitemaps.org/protocol.html).

The [Sitemaps.org](http://www.sitemaps.org/) protocol is the leading standard and is supported by Google, Bing, Yahoo, Ask and many others.

## Installation
The library is available for install via Composer. To install, add the requirement to your `composer.json` file, like this:
```json
{
    "require": {
        "vipnytt/sitemapparser": "1.0.*"
    }
}
```

Then run `composer update`.

[Find out more about Composer here](https://getcomposer.org)

## Features
- Basic parsing
- Recursive parsing
- Custom User-Agent string
- Proxy support
- Offline parsing

### Formats supported
- XML `.xml`
- Compressed XML `.xml.gz`
- Robots.txt rule sheet `robots.txt`
- Plain text


## Getting Started

### Basic example
Returns an list of URLs only.
```php
use vipnytt\SitemapParser;
use vipnytt\SitemapParser\Exceptions\SitemapParserException;

try {
    $parser = new SitemapParser();
    $parser->parse('https://www.google.com/sitemap.xml');
    foreach ($parser->getURLs() as $url => $tags) {
        echo $url . '<br>';
    }
} catch (SitemapParserException $e) {
    echo $e->getMessage();
}
```

### Advanced
Returns all available tags, for both Sitemaps and URLs.
```php
use vipnytt\SitemapParser;
use vipnytt\SitemapParser\Exceptions\SitemapParserException;

try {
    $parser = new SitemapParser('MyCustomUserAgent');
    $parser->parse('http://php.net/sitemap.xml');
    foreach ($parser->getSitemaps() as $url => $tags) {
        echo 'Sitemap<br>';
        echo 'URL: ' . $url . '<br>';
        echo 'LastMod: ' . @$tags['lastmod'] . '<br>';
        echo '<hr>';
    }
    foreach ($parser->getURLs() as $url => $tags) {
        echo 'URL: ' . $url . '<br>';
        echo 'LastMod: ' . @$tags['lastmod'] . '<br>';
        echo 'ChangeFreq: ' . @$tags['changefreq'] . '<br>';
        echo 'Priority: ' . @$tags['priority'] . '<br>';
        echo '<hr>';
    }
} catch (SitemapParserException $e) {
    echo $e->getMessage();
}
```

### Recursive
Parses any sitemap detected while parsing, to get an complete list of URLs
```php
use vipnytt\SitemapParser;
use vipnytt\SitemapParser\Exceptions\SitemapParserException;

try {
    $parser = new SitemapParser('MyCustomUserAgent');
    $parser->parseRecursive('http://www.google.com/robots.txt');
    echo '<h2>Sitemaps</h2>';
    foreach ($parser->getSitemaps() as $url => $tags) {
        echo 'URL: ' . $url . '<br>';
        echo 'LastMod: ' . @$tags['lastmod'] . '<br>';
        echo '<hr>';
    }
    echo '<h2>URLs</h2>';
    foreach ($parser->getURLs() as $url => $tags) {
        echo 'URL: ' . $url . '<br>';
        echo 'LastMod: ' . @$tags['lastmod'] . '<br>';
        echo 'ChangeFreq: ' . @$tags['changefreq'] . '<br>';
        echo 'Priority: ' . @$tags['priority'] . '<br>';
        echo '<hr>';
    }
} catch (SitemapParserException $e) {
    echo $e->getMessage();
}
```

### Additional examples
Even more examples available in the [examples](https://github.com/VIPnytt/SitemapParser/tree/master/examples) directory.

## Final words

Contributing is surely allowed! :-)
