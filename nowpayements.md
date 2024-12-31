# Nowpayments Package Integration Guide

## Overview
This guide provides detailed steps to integrate the Nowpayments Package into your project. This package enables seamless payment processing via Nowpayments, enhancing the functionality of your application.

---

## Integration Steps

### Step 1: Add the Package Folder
Place the Nowpayments package folder at the root of your project.

### Step 2: Update `composer.json`
Add the following code under the `autoload` section in your `composer.json` file:

```json
"Biz\\Nowpayments\\": "packages/biz/nowpayments/src/"
```

### Step 3: Update `config/app.php`
Add the following code under the `providers` section in the `config/app.php` file:

```php
Biz\Nowpayments\Providers\NowpaymentsProvider::class,
```

### Step 4: Update `token.blade.php`
Navigate to the `token.blade.php` file and add the following code after the "Make Payment" button:

```php
@if(get_setting('nowpayments_package_active') == 1)
    <li>
        <button type="submit" formaction="{{ url('user/pay') }}" class="btn btn-alt btn-primary payment-btn show_loader">
            Nowpayments <em class="ti ti-arrow-right mgl-2x"></em>
        </button>
    </li>
@endif
```

### Step 5: Run Necessary Commands
Run the following commands to update and optimize your application:

```bash
composer dump-autoload
php artisan optimize
```

### Step 6: Check Changes
Run the following command to publish vendor files:

```bash
php artisan vendor:publish
```
### step 7: Finalize the Installation
Visit yourdomain.com/nowpayments_package
---

## Conclusion
Following these steps will integrate the Nowpayments Package into your project. Ensure all steps are executed correctly for a seamless payment processing experience. For any issues, double-check your configurations and validate that all commands have been executed properly.

