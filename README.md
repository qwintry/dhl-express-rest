# Very short description of the package

[![Latest Version on Packagist](https://img.shields.io/packagist/v/booni3/dhl-express-rest.svg?style=flat-square)](https://packagist.org/packages/booni3/dhl-express-rest)

Package to work with the DHL Express Rest API (v2). This package is currently in development. 

## Installation

You can install the package via composer:

```bash
composer require booni3/dhl-express-rest
```

## Usage

Domestic Shipments
```php
$dto = new ShipmentCreator();
$dto->setShipperAccountNumber(954103895);
$dto->setShipper(
    (new CustomerDetails('John Smith','21 Apple Drive','Malmesbury','Wiltshire',
        'Malmesbury','SN16 4TB','GB','My Awesome Company','071111111112','a@b.com',
    ))
        ->addVat('GB1234')
        ->addEORI('GB1234')
);
$dto->setProductCode('N'); // GB
$dto->setReceiver(new CustomerDetails('Helen Jones', '4 Drive', 'London', 'E14 8DW', 'GB'));
$dto->addReference('123456-custom-ref');
$dto->addPackage(new Package(12.5, 20, 10, 10, 'Jumpers', 'order-ref-1244'));

$dhl = DHL::make([
    'user' => 'DHLUSER',
    'pass' => 'dsdfsedf',
    'sandbox' => true, // false or remove for production
]);

$res = $dhl->shipments()->create($dto);
$res->trackingUrl; // tracking number
$res->trackingNumber; // url for api tracking
$res->labelData(); // decoded label data
```
Customs Declarable Shipments
```php
$dto->setCustomsDeclarable($declarable, true, 954103895);
$dto->setInvoice('PS-1234', now(), 'Adam Lambert');
$dto->setExportDecliration('sale', 'GBP');
$dto->addExportLineItem(new LineItem('Red Jumper', 12.99, 1, 12456, 'GB', 12));
$dto->addExportLineItem(new LineItem('Blue Jumper', 12.99, 1, 12456, 'GB', 12));
```

### Testing

``` bash
composer test
```

### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

### Security

If you discover any security related issues, please email adam@profilestudio.com instead of using the issue tracker.

## Credits

- [Adam](https://github.com/booni3)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

## PHP Package Boilerplate

This package was generated using the [PHP Package Boilerplate](https://laravelpackageboilerplate.com).
