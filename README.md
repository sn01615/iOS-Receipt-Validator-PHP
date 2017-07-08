Install
=======

```bash
composer require sn01615/i-os-receipt-validator-php
```
Usage
=====
```php
$data = new \stdClass();
$data->receipt = $_POST['receipt-data'];
$data->sandbox = $_POST['sandbox'];

$endpoint = $data->sandbox ? \itunesReceiptValidator::SANDBOX_URL : \itunesReceiptValidator::PRODUCTION_URL;

try {
    $rv = new \itunesReceiptValidator($endpoint, $data->receipt);

    $data->environment = ($rv->getEndpoint() === \itunesReceiptValidator::SANDBOX_URL) ? 'Sandbox' : 'Production';

    $data->info = $rv->validateReceipt();
    # TODO 业务逻辑处理

    $data->result = 'Success';
} catch (\Exception $ex) {
    $data->result = 'Fail';
}

print_r($data);
```

In App Purchase Receipt Validator - PHP
=======================================

Host this on any box which is running PHP and has direct outbound web access and it will be able to validate iOS IAP receipts for you (Sandbox or Production environment configurable).

Feel free to use this code in anything you make, with the standard disclaimer that if it doesn't work / blows up the universe, you're on your own.

Alternatively, the latest version is hosted at: http://www.chrismaddern.com/validate-itunes-receipt/

This points to production.

There is a Sandbox version embedded here:
http://www.chrismaddern.com/validate-app-store-iap-receipt-codes-online-tool/

The PHP is rough, but it works - any forks / pull requests are more than welcome!!
