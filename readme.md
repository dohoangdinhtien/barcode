[![Packagist Downloads](https://img.shields.io/packagist/dt/milon/barcode.svg)](https://packagist.org/packages/milon/barcode) 
[![Stable version](https://img.shields.io/packagist/v/milon/barcode.svg)](https://packagist.org/packages/milon/barcode) 
[![License](https://img.shields.io/packagist/l/milon/barcode.svg)](https://packagist.org/packages/milon/barcode)

![Banner](./banner.png)

This is a barcode generation package inspired by <https://github.com/tecnickcom/TCPDF>. Actually, I use that package's underline classes for generating barcodes. This package is just a wrapper of that package and adds compatibility with Laravel.

I used the following classes of that package.

- src/Milon/Barcode/Datamatrix.php (include/barcodes/datamatrix.php)
- src/Milon/Barcode/DNS1D.php (tcpdf_barcodes_1d.php)
- src/Milon/Barcode/DNS2D.php (tcpdf_barcodes_2d.php)
- src/Milon/Barcode/PDF417.php (include/barcodes/pdf417.php)
- src/Milon/Barcode/QRcode.php (include/barcodes/qrcode.php)

[Read More on TCPDF website](http://www.tcpdf.org)

This package relies on [php-gd](http://php.net/manual/en/book.image.php) extension. So, make sure it is installed on your machine.

## Installation

Begin by installing this package through Composer. Just run following command to terminal-

```shell script
composer require milon/barcode
```

You can also edit your project's `composer.json` file to require `milon/barcode`. Just make sure you choosed the compatible version of the package from the following table.

## Compatibility

| Laravel Version | Barcode Package Version |
|-----------------|-------------------------|
| 12.*            | ^12.0                   |
| 11.*            | ^11.0                   |
| 10.*            | ^10.0                   |
| 9.*             | ^9.0                    |
| 8.*             | ^8.0                    |
| 7.*             | ^7.0                    |
| 6.*             | ^6.0                    |
| 5.0 and 5.1     | ^5.1                    |
| 4.0, 4.1, 4.2   | ^4.2                    |

## Configuration

> If you are using version 6 or above, then the Service Provider and aliases will be published automatically. For prior versions, please follow the below instruction.

After updating Composer, add the service provider to your `config/app.php` file:

```php
'providers' => [
    // ...
    Milon\Barcode\BarcodeServiceProvider::class,
]
```

For Laravel version 4.*, add the following lines to your `app/config/app.php` file:

```php
'providers' => array(
    // ...
    'Milon\Barcode\BarcodeServiceProvider',
)
```

**Make sure you have write permission to the storage path. By default it sets to `/storage` folder.**

```php
'aliases' => [
    // ...
    'DNS1D' => Milon\Barcode\Facades\DNS1DFacade::class,
    'DNS2D' => Milon\Barcode\Facades\DNS2DFacade::class,
]
```

For version 4.2 alias will be like this-

```php
'aliases' => array(
    // ...
    'DNS1D' => 'Milon\Barcode\Facades\DNS1DFacade',
    'DNS2D' => 'Milon\Barcode\Facades\DNS2DFacade',
)
```

## Publishing Configuration

To customize the barcode settings (e.g., store path), publish the configuration file(s) by running the appropriate command in the terminal:

```shell
# Laravel 5.x
php artisan vendor:publish

# Laravel 4.x
php artisan config:publish milon/barcode
```

## Usage

Bar-code generator like Qr Code, PDF417, C39, C39+, C39E, C39E+, C93, S25, S25+, I25, I25+, C128, C128A, C128B, C128C, 2-Digits UPC-Based Extention, 5-Digits UPC-Based Extention, EAN 8, EAN 13, UPC-A, UPC-E, MSI (Variation of Plessey code)

generator in html, png , jpeg embedded base64 code and SVG canvas

```php
echo DNS1D::getBarcodeSVG('4445645656', 'PHARMA2T');
echo DNS1D::getBarcodeHTML('4445645656', 'PHARMA2T');
echo '<img src="data:image/png,' . DNS1D::getBarcodePNG('4', 'C39+') . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath('4445645656', 'PHARMA2T');
echo '<img src="data:image/png;base64,' . DNS1D::getBarcodePNG('4', 'C39+') . '" alt="barcode"   />';
echo DNS1D::getBarcodeJPGPath('4445645656', 'PHARMA2T');
echo '<img src="data:image/jpeg;base64,' . DNS1D::getBarcodeJPG('4', 'C39+') . '" alt="barcode"   />';
```

```php
echo DNS1D::getBarcodeSVG('4445645656', 'C39');
echo DNS2D::getBarcodeHTML('4445645656', 'QRCODE');
echo DNS2D::getBarcodePNGPath('4445645656', 'PDF417');
echo DNS2D::getBarcodeSVG('4445645656', 'DATAMATRIX');
echo '<img src="data:image/png;base64,' . DNS2D::getBarcodePNG('4', 'PDF417') . '" alt="barcode"   />';
```

## Width and Height example

```php
echo DNS1D::getBarcodeSVG('4445645656', 'PHARMA2T',3,33);
echo DNS1D::getBarcodeHTML('4445645656', 'PHARMA2T',3,33);
echo '<img src="' . DNS1D::getBarcodePNG('4', 'C39+',3,33) . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath('4445645656', 'PHARMA2T',3,33);
echo '<img src="data:image/png;base64,' . DNS1D::getBarcodePNG('4', 'C39+',3,33) . '" alt="barcode"   />';
echo DNS1D::getBarcodeJPGPath('4445645656', 'PHARMA2T',3,33);
echo '<img src="data:image/jpeg;base64,' . DNS1D::getBarcodeJPG('4', 'C39+',3,33) . '" alt="barcode"   />';
```

## Color

```php
echo DNS1D::getBarcodeSVG('4445645656', 'PHARMA2T',3,33,'green');
echo DNS1D::getBarcodeHTML('4445645656', 'PHARMA2T',3,33,'green');
echo '<img src="' . DNS1D::getBarcodePNG('4', 'C39+',3,33,array(1,1,1)) . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath('4445645656', 'PHARMA2T',3,33,array(255,255,0));
echo '<img src="data:image/png;base64,' . DNS1D::getBarcodePNG('4', 'C39+',3,33,array(1,1,1)) . '" alt="barcode"   />';
echo DNS1D::getBarcodeJPGPath('4445645656', 'PHARMA2T',3,33,array(255,255,0));
echo '<img src="data:image/jpeg;base64,' . DNS1D::getBarcodeJPG('4', 'C39+',3,33,array(1,1,1)) . '" alt="barcode"   />';
```

## Show Text

```php
echo DNS1D::getBarcodeSVG('4445645656', 'PHARMA2T',3,33,'green', true);
echo DNS1D::getBarcodeHTML('4445645656', 'PHARMA2T',3,33,'green', true);
echo '<img src="' . DNS1D::getBarcodePNG('4', 'C39+',3,33,array(1,1,1), true) . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath('4445645656', 'PHARMA2T',3,33,array(255,255,0), true);
echo '<img src="data:image/png;base64,' . DNS1D::getBarcodePNG('4', 'C39+',3,33,array(1,1,1), true) . '" alt="barcode"   />';
echo DNS1D::getBarcodeJPGPath('4445645656', 'PHARMA2T',3,33,array(255,255,0), true);
echo '<img src="data:image/jpeg;base64,' . DNS1D::getBarcodeJPG('4', 'C39+',3,33,array(1,1,1), true) . '" alt="barcode"   />';
```

## 2D Barcodes

```php
echo DNS2D::getBarcodeHTML('4445645656', 'QRCODE');
echo DNS2D::getBarcodePNGPath('4445645656', 'PDF417');
echo DNS2D::getBarcodeSVG('4445645656', 'DATAMATRIX');
```

## 1D Barcodes

```php
echo DNS1D::getBarcodeHTML('4445645656', 'C39');
echo DNS1D::getBarcodeHTML('4445645656', 'C39+');
echo DNS1D::getBarcodeHTML('4445645656', 'C39E');
echo DNS1D::getBarcodeHTML('4445645656', 'C39E+');
echo DNS1D::getBarcodeHTML('4445645656', 'C93');
echo DNS1D::getBarcodeHTML('4445645656', 'S25');
echo DNS1D::getBarcodeHTML('4445645656', 'S25+');
echo DNS1D::getBarcodeHTML('4445645656', 'I25');
echo DNS1D::getBarcodeHTML('4445645656', 'I25+');
echo DNS1D::getBarcodeHTML('4445645656', 'C128');
echo DNS1D::getBarcodeHTML('4445645656', 'C128A');
echo DNS1D::getBarcodeHTML('4445645656', 'C128B');
echo DNS1D::getBarcodeHTML('4445645656', 'C128C');
echo DNS1D::getBarcodeHTML('4445645656', 'GS1-128');
echo DNS1D::getBarcodeHTML('44455656', 'EAN2');
echo DNS1D::getBarcodeHTML('4445656', 'EAN5');
echo DNS1D::getBarcodeHTML('4445', 'EAN8');
echo DNS1D::getBarcodeHTML('4445', 'EAN13');
echo DNS1D::getBarcodeHTML('4445645656', 'UPCA');
echo DNS1D::getBarcodeHTML('4445645656', 'UPCE');
echo DNS1D::getBarcodeHTML('4445645656', 'MSI');
echo DNS1D::getBarcodeHTML('4445645656', 'MSI+');
echo DNS1D::getBarcodeHTML('4445645656', 'POSTNET');
echo DNS1D::getBarcodeHTML('4445645656', 'PLANET');
echo DNS1D::getBarcodeHTML('4445645656', 'RMS4CC');
echo DNS1D::getBarcodeHTML('4445645656', 'KIX');
echo DNS1D::getBarcodeHTML('4445645656', 'IMB');
echo DNS1D::getBarcodeHTML('4445645656', 'CODABAR');
echo DNS1D::getBarcodeHTML('4445645656', 'CODE11');
echo DNS1D::getBarcodeHTML('4445645656', 'PHARMA');
echo DNS1D::getBarcodeHTML('4445645656', 'PHARMA2T');
```

# Running without Laravel

You can use this library without using Laravel.

Example:

```php
use \Milon\Barcode\DNS1D;

$d = new DNS1D();
$d->setStorPath(__DIR__.'/cache/');
echo $d->getBarcodeHTML('9780691147727', 'EAN13');
```

## License

This package is published under `GNU LGPLv3` license and copyright to [Nuruzzaman Milon](http://milon.im). Original Barcode generation classes were written by Nicola Asuni. The license agreement is on project's root.

### [Buy me a coffee ☕](https://paypal.me/tomilon?locale.x=en_US)

License: GNU LGPLv3<br>
Package Author: [Nuruzzaman Milon](http://milon.im)<br>
Original Barcode Class Author: [Nicola Asuni](http://www.tcpdf.org)<br>
Package Copyright: Nuruzzaman Milon<br>
Barcode Generation Class Copyright:<br>
Nicola Asuni<br>
Tecnick.com LTD<br>
www.tecnick.com
