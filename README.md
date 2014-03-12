PHP Rest CURL
=========
PHP Rest CURL is a wrapper class for PHP, simplifying the typical CRUD requests to the extreme.

## Get Started
Using it is as simple as can be.

The following line:

	<?php
	require_once('rest.inc.php');
	
	// CALL
	$result = RestCurl::get("https://api.mongolab.com/api/1/databases/my-db/collections/bookings?apiKey=0123456789abcde");

$result will contain something like:

	print_r($result);
	
    Array
    (
        [status] => 200
        [header] => HTTP/1.1 200 OK
    Date: Wed, 12 Mar 2014 01:17:53 GMT
    Server: Apache/2.2.22 (Ubuntu)
    Expires: Tue, 01 Feb 2000 08:00:00 GMT
    Last-Modified: Wed, 12 Mar 2014 01:17:53 GMT
    Cache-Control: no-store, no-cache, must-revalidate, max-age=0, post-check=0, pre-check=0
    Pragma: no-cache
    X-Frame-Options: DENY
    Access-Control-Allow-Credentials: true
    Access-Control-Allow-Origin: *
    Transfer-Encoding: chunked
    Content-Type: application/json;charset=utf-8
        [data] => Array
            (
                [0] => stdClass Object
                    (
                        [_id] => stdClass Object
                            (
                                [$oid] => 52476ad1e4b08781144211f3
                            )

                        [city] => Barcelona
                        [date] => 2014-03-10
                        [guest] => Jordi Moraleda
                    )

            )

    )

The result:

* $result['status'] is the HTTP status code.
* $result['header'] is a string with the response headers
* $result['data'] is the JSON response parsed into an array

##CRUD Methods
RestCurl supports the typical CRUD methods (GET, POST, PUT, DELETE) as follows:

	// GET
	$result = RestCurl::get($URL, array('id' => 12345678));
	
	// POST
	$result = RestCurl::post($URL, array('name' => 'RestCurl'));
	
	// PUT
	$result = RestCurl::put($URL, array('$set' => array('version' => 1)));
	
	// DELETE
	$result = RestCurl::delete($URL, array());	

The second parameter is **optional**. 

* In GET requests, $keyValueParams will be appended to the URL
	* array('id' => '12345678') will turn into http://example.net/?id=12345678
	* If GET parameters are already present in the URL, nothing will be appended
* For the rest of methods, the contents of the second parameter will be stringified as **JSON** and passed as the request **body**. 

## Other HTTP methods
If you want to use methods besides GET, POST, PUT, DELETE, you can achieve that by just calling:

	$result = RestCurl::exec('OPTIONS', $URL, array('foo' => 'bar'));

