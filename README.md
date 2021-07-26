# Tripay Library

### Setting Merchant

Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia.

```php
use Tripay\Constants\Environment;
use Tripay\Merchant;

$environment = Environment::DEVELOPMENT; // DEVELOPMENT atau PRODUCTION.

$apiKey = 'api key anda';
$privateKey = 'private key anda';

$channelCode = 'merchant code'; // BRIVA, BNIVA etc.
$merchantCode = 'merchant code'; // T0005, T0006 etc.

$merchant = new Merchant($environment)
    ->apiKey($apiKey)
    ->privateKey($privateKey)
    ->channelCode($channelCode)
    ->merchantCode($merchantCode);
```

## Merchant

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua.



### Channel Pembayaran

Mendapatkan daftar channel pembayaran yang aktif pada akun Merchant
Anda beserta informasi lengkap termasuk biaya transaksi dari masing-masing channel

```php
$channels = $merchant->channels();

print_r($channels);
```



### Kalkulator Biaya

Mendapatkan rincian perhitungan biaya transaksi untuk masing-masing
channel berdasarkan nominal yang ditentukan

```php
$amount = 100000;

$price = $merchant->calculate($amount);

print_r($price);
```



### Daftar Transaksi

Mendapatkan daftar transaksi merchant


```php
$page = 1;
$per_page = 25;

$transactions = $merchant->transactions($page, $per_page);

print_r($transactions);
```



## Tansaksi

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua.


### Setting Transaksi

Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi.

```php
use Tripay\Constants\Environment;
use Tripay\Transaction;

$environment = Environment::DEVELOPMENT; // DEVELOPMENT atau PRODUCTION.

$returnUrl = 'https://situsku.com/payment/success/thanks';

$transaction = new Transaction($environment)
    ->apiKey($apiKey)
    ->privateKey($privateKey)
    ->channelCode($channelCode)
    ->merchantCode($merchantCode)
    ->returnUrl($returnUrl);
```


### Open Payment

Excepteur sint occaecat cupidatat non proident, sunt in culpa qui
officia deserunt mollit anim id est laborum.


#### Request Transaksi

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua.

```php
$customerName = 'Asep Balon';
$customerEmail = 'asep.balon@gmail.com';
$customerPhone = '081234567890';

$merchantRef = 'TRX-123456'; // isi sembarang, atau kosongkan saja. Tidak wajib.

$transaction->forOpenPayment(); // Untuk open payment

$transaction->merchantRef($merchantRef)
    ->customer(
        $customerName,
        $customerEmail,
        $customerPhone
    );


$result = $transaction->process();

print_r($result);
```


#### Detail Transaksi

Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur.

```php
$uuid = 'T4160-OP1617-TJNCU4'; // Diperoleh dari hasil $transaction->process();

$transaction->forOpenPayment(); // Untuk open payment

$details = $transaction->details($uuid);

print_r($details);
```


#### Daftar Pembayaran

Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur.

```php
$apiKey = 'VIFHCKCPecpF6c7nanddTwu0w0rQ0l8qVY0iUwb0';
$uuid = 'T4160-OP1617-TJNCU4';

$transaction->forOpenPayment();// Untuk open payment

$payments = $transaction->payments($uuid);

print_r($payments);
```


### Closed Payment

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua.

```php
use Tripay\Constants\Environment;
use Tripay\Transaction;

$transaction->forClosedPayment();

$minutes = 1440; // waktu kedaluwarsa invoice (dalam menit, default 1440 = 24 jam);

$transaction->merchantRef($merchantRef)

    ->expiresAfter($minutes);

    ->customer(
        $customerName,
        $customerEmail,
        $customerPhone
    );

    // ->addItem('Nama Produk', 'Harga Satuan', 'Jumlah', 'Kode SKU')

    ->addItem('Nama Produk 1', 100000, 2, 'PROD-1')
    ->addItem('Nama Produk 2', 100000, 6, 'PROD-2')
    ->addItem('Nama Produk 3', 100000, 3, 'PROD-3')
    ->addItem('Nama Produk 4', 100000, 1, 'PROD-4');

$response = $transaction->process();

print_r($response);
```

#### Detail Transaksi

Excepteur sint occaecat cupidatat non  deserunt mollit anim id est laborum.

```php
$reference = 'T0001000000000000006'; // Diperoleh dari hasil $transaction->process();

$details = $transaction->details($reference);

print_r($details);
```