# PHP-API-AUTH

Single file PHP script that adds authentication to a [PHP-CRUD-API](https://github.com/mevdschee/php-crud-api) project.

NOTE: This repo is a fork of the original.  Use the master branch if you want all the features mentioned below.
If you want certain features, you can start with bugfix and then merge in specific features.   The features are
branches of bugfix.

Branches:

  - master : Merge of all features below
  - bugfix : Branch that mirrors original master, used for sending bugfixes
    - apiKey : apiKey support for swagger.io
    - php53  : Additional support for prior versions of PHP

## Requirements

  - PHP 5.3 or higher
  - apache_request_headers() not available in earlier versions of 5.3 (see Issue #1)

## Simple username + password

On API server

- login.html is loaded
- sends username + password via POST to "api.php/"
- api.php (POST on "/" gets hijacked by auth.php) is loaded
- sends back csrf token + http-only session cookie
- call API as: api.php?csrf=\[csrf token] (session cookie is sent automatically)
- (when using Angular2 or Vue2 the CSRF token is sent automatically)

## With authentication server

On authentication server

- login_token.html is loaded
- sends username + password via POST to "login_token.php"
- login_token.php is loaded
- sends token via POST to "api.php/"

On API server

- api.php (POST on "/" gets hijacked by auth.php) is loaded
- sends back csrf token + http-only session cookie
- call API as: api.php?csrf=\[csrf token] (session cookie is sent automatically)
- (when using Angular2 or Vue2 the CSRF token is sent automatically)

## With apiKey

- Tested with swagger.io editor under Chrome
- Both query and header methods are supported
- See api.php for examples
