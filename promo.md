# Promo Package Integration Guide

## Overview
This guide outlines the steps to integrate the Promo Package into your project. The Promo Package enables promotional features, enhancing your application's functionality with customizable promo codes and related configurations.

---

## Integration Steps

### Step 1: Add the Package Folder
Place the package folder at the root of your project.

### Step 2: Update `composer.json`
Add the following code under the `autoload` section in your `composer.json` file:

```json
"Biz\\Promo\\": "packages/biz/promo/src/"
```

### Step 3: Update `config/app.php`
Add the following code under the `providers` section in the `config/app.php` file:

```php
Biz\Promo\Providers\PromoProvider::class,
```

### Step 4: Run Necessary Commands
Run the following commands to update and optimize your application:

```bash
composer dump-autoload
php artisan optimize
```

### Step 5: Check Changes
Run the following command to publish vendor files:

```bash
php artisan vendor:publish
```

### Step 6: Run Migrations
Run the following command to apply migrations:

```bash
php artisan migrate
```

### Step 7: Update Token File
Navigate to `\resources\views\user` and add the following code to the token file:

```php
<?php if(get_setting('promo_package_active') == 1){ ?>
    @include('promo::user.promo')
<?php  }  ?>
```

### Step 8: Update `TokenController`
Navigate to `app\Http\Controllers\User` and add the following code to the `TokenController`:

#### Use Promo Model
```php
use Biz\Promo\Models\Promo;
```

#### Update Controller Logic
Add the following logic to handle promo-related data:

```php
$save_data = [
    'created_at' => Carbon::now()->toDateTimeString(),
    'tnx_id' => $mycreate_data['payment_id'],
    'tnx_type' => 'purchase',
    'tnx_time' => Carbon::now()->toDateTimeString(),
    'tokens' => $trnx_data['token'],
    'bonus_on_base' => $trnx_data['bonus_on_base'],
    'bonus_on_token' => $trnx_data['bonus_on_token'],
    'stage' => active_stage()->id,
    'user' => Auth::id(),
    'amount' => $trnx_data['amount'],
    'base_amount' => $trnx_data['base_price'],
    'old_base_amount' => $trnx_data['base_price'],
    'base_currency' => $base_currency,
    'base_currency_rate' => $base_currency_rate,
    'currency' => $currency,
    'currency_rate' => number_format($currency_rate, 8, '.', ''),
    'receive_currency' => $currency,
    'receive_amount' => $mycreate_data['amount_received'],
    'all_currency_rate' => $all_currency_rate,
    'payment_method' => strtoupper($currency),
    'payment_to' => $mycreate_data['pay_address'],
    'payment_id' => $mycreate_data['payment_id'],
    'added_by' => set_added_by('00'),
    'details' => __('messages.trnx.purchase_token'),
    'extra' => '',
    'status' => 'pending',
];

$r_promo_code = $request->promo_code ?? '';
$currentDate = Carbon::now();

if (empty($request->promo_end_date)) {
    $promo = Promo::where('promo_status', 1)
        ->whereDate('promo_start_date', '<=', $currentDate)
        ->where('promo_code', $r_promo_code)
        ->first();
} else {
    $promo = Promo::where('promo_status', 1)
        ->whereDate('promo_start_date', '<=', $currentDate)
        ->whereDate('promo_end_date', '>=', $currentDate)
        ->where('promo_code', $r_promo_code)
        ->first();
}

if ($promo) {
    $promo_code = $promo->promo_code;
    $promo_amount = $promo->promo_amount;
    $promo_token = ($token * $promo_amount / 100);

    $save_data['promo_code'] = $promo_code;
    $save_data['promo_amount'] = $promo_amount;
    $save_data['promo_tokens'] = $promo_token;
    $save_data['total_bonus'] = $promo_token + $trnx_data['total_bonus'];
    $save_data['total_tokens'] = $promo_token + $trnx_data['total_tokens'];
} else {
    $save_data['total_bonus'] = $trnx_data['total_bonus'];
    $save_data['total_tokens'] = $trnx_data['total_tokens'];
}
```

---

## Conclusion
By following these steps, you can successfully integrate the Promo Package into your project. This integration allows for advanced promotional features and better user engagement. If you encounter any issues, ensure all steps are completed correctly and verify your configurations.

