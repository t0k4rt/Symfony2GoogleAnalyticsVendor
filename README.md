# Server-Side Google Analytics PHP Client

## Important  
This package is directly based on this project from UnitedPrototype : http://code.google.com/p/php-ga/ 

This package is aimed at using php-ga in symfony 2 as a vendor and a service.


## Summary :
"ga.js in PHP" - Implementation of a generic server-side Google Analytics client in PHP that implements nearly every parameter and tracking feature of the original GA Javascript client.

We love Google Analytics and want to contribute to its community with this PHP client implementation. It is intended to be used stand-alone or in addition to an existing Javascript library implementation.

It's PHP, but porting it to e.g. Ruby or Python should be easy. Building this library involved weeks of documentation reading, googling and testing - therefore its source code is thorougly well-documented.

The PHP client has nothing todo with the Data Export or Management APIs, although you can of course use them in combination.

## Requirements

Requires PHP 5.3 as namespaces and closures are used. Has no other dependencies and can be used independantly from any framework or whatsoever environment.

## Installation :

**In your deps file :**

    [php-ga]
        git=http://github.com/t0k4rt/Symfony2GoogleAnalyticsVendor.git

**Update your vendors :**

    php bin/vendors
    
**Update your autoload.php file :**

 
    $loader->registerNamespaces(array(
        ...
        'GoogleAnalytics'         => __DIR__.'/../vendor/php-ga/src',
        ...
    ));
    
**In your config.yml / config_dev.yml / config_prod.yml :**

To use this as a service add the following lines

    parameters:
        php_ga.class:      GoogleAnalytics\Tracker
        php_ga.accountID:  UA-12345678-9
        php_ga.domain:  yourwebsite.com

    services:
        php_ga:
            class:        %php_ga.class%
            arguments:    [ %php_ga.accountID% , %php_ga.domain% ]
        
        
**In your bundle :**

You now can include the class in your controller

 
    use googleanalytics;

And track page (or events etc.) :

    // Initilize GA Tracker
    $tracker = $this->get('php-ga');
    
    // Assemble Visitor information
    // (could also get unserialized from database)
    $visitor = new GoogleAnalytics\Visitor();
    $visitor->setIpAddress($_SERVER['REMOTE_ADDR']);
    $visitor->setUserAgent($_SERVER['HTTP_USER_AGENT']);
    $visitor->setScreenResolution('1024x768');
    
    // Assemble Session information
    // (could also get unserialized from PHP session)
    $session = new GoogleAnalytics\Session();
    
    // Assemble Page information
    $page = new GoogleAnalytics\Page('/page.html');
    $page->setTitle('My Page');
    
    // Track page view
    $tracker->trackPageview($page, $session, $visitor);
    



        
        

