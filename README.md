# PHP EspoCRM API client

Require with Composer:

```
composer require espocrm/php-espo-api-client
```

## Usage

```php
use Espo\ApiClient\Client;
use Espo\ApiClient\Header;
use Espo\ApiClient\Exception\ResponseError;

$client = new Client($yourEspoUrl);
$client->setApiKey($apiKey);
$client->setSecretKey($secretKey); // if you use HMAC method

try {
    $response = $client->request(
        Client::METHOD_POST,
        'Lead',
        [
            'firstName' => $firstName,
            'lastName' => $lastName,
            'emailAddress' => $emailAddress,
        ],
        [new Header('X-Skip-Duplicate-Check', 'true')]
    );
    
    $parsedBody = $response->getParsedBody();
} catch (ResponseError $e) {
    // Error response.
    $response = $e->getResponse();    
    
    $code = $response->getCode();
    $body = $response->getBodyPart();

    // Consider using some additional library if you need parsed response headers.
}
```

## Changelog

### 1.0.0

* Using new method for constructing *X-Hmac-Authorization* header https://github.com/espocrm/php-espo-api-client/issues/2
