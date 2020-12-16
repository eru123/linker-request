# linker-request
PHP Request parser library
# Installation
### Composer
```bash
composer require eru123/linker-request
```
# How it works?
## Query
### Example Query Usage
```php
<?php
require_once __DIR__."/vendor/autoload.php";

use Linker\Request\Query;

$method = "get";
$parameters = "page:register user:!r pass:!r email";
$callback = function($params){ // It can be also a NULL

    // If the user request match the parameters, this function is called
    // parameters can be access using $params["parameter_name"]
    
    // if the function does not specify the return value, it will return $params by default

}

// Returns TRUE if the parameters are matched, 
// or called the callback function if not NULL
// or returns an array of parameters value
// or return FALSE if the parameters are NOT matched
$register = Query::get($method,$parameters,$callback); 

/*
*EXAMPLE Request
*URL: https://example.com/user.php?page=register&user=H4cK3R&pass=IAmAPassword123
*outputs:
*    $register = [
*        "page" => "register",
*        "user" => "H4cK3R",
*        "pass" => "IAmAPassword123"
*        "email" => NULL
*    ]
*/

/*
*EXAMPLE Request
*URL: https://example.com/user.php?page=register&user=H4cK3R&email=example@email.com
*outputs:
*    $register = FALSE
*/
```
### Availabe methods
 - `request` (default)
 - `get`
 - `post`
 - `put`
 - `files`
 - `delete`
 - `server`
 - `env`
### Parameters
 - `:` Separator
 - `!r` Indicates that a parameter is required
 - ` ` Parameters are strictly separated by a single space
### Parameters example
 - `user:!r pass:!r name` - indicates that user and pass are required and returns true even if the name is undefined.
 - `id:1 token:!r` - indicates that id query must be equal to one and the token is defined.
 - `name:Jericho%20Aquino bio:Hi%20Friends` when requiring a specific value, that value must be in ***url encoded*** format.
## URI
### Example URI usage
```php
<?php
require_once __DIR__."/vendor/autoload.php";
use Linker\Request\URI;

// Example URL: https://example.com/user/1/post/1
$get = URI::getPath();
// outputs: /user/1/post/1

// Example URL: https://example.com/index.php?/user/1/post/1&token=453dfvdiuydfg7dfg&_rdc=sddsfr4dfdf
$get = URI::getQueryPath();
// outputs: /user/1/post/1
```
### URI::getPath()
`URI::getPath()` parse the URL request into a cleaner look, it removes the host and url queries
### URI::getQueryPath()
`URI::getQueryPath()` is an alternative for developers who wants to get a query in url like this `https://example.com/user.php?/1/post/1` (It's just a preference).