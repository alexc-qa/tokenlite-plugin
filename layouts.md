# Tokenlite Layout Changer Plugin Documentation

## Overview
Tokenlite, by default, does not allow layout changes for the dashboard. Our custom plugin resolves this limitation, enabling you to modify the dashboard layout as per your preference. After purchasing and installing the plugin, you can easily switch between different layouts through a user-friendly interface.

## Key Features
- **Dynamic dashboard layout customization.**
- **Simple installation process with minimal commands.**
- **Easy-to-use layout selection menu.**

---

## Installation Guide

### Step 1: Purchase and Download
1. **Download the Package:** Once you purchase the plugin, click on the provided link to download the package file.
2. **Save the Package:** Save the file on your system for the next steps.

### Step 2: Upload the Package
1. **Access Your Server:** Log into your server where Tokenlite is installed.
2. **Upload the File:** Upload the downloaded package file to the Tokenlite root directory.

   > **Note:** Once the file is uploaded, you will be automatically redirected to the root directory.

### Step 3: Install the Plugin
1. **Open Terminal/Command Line:** Access your server’s terminal or command line interface.
2. **Run Installation Commands:** Execute the following commands one by one to install the plugin:

   ```bash
   composer dump-autoload
   php artisan optimize
   php artisan vendor:publish
   ```

   > **Note:** After running these commands, the plugin will be installed and ready to configure.

### Step 4: Enable the Layout Package
1. **Go to the Layout Menu:** Navigate to the Tokenlite dashboard and open the “Choose Layout” menu.
2. **Enable the Layout:** Select the layout package you want to apply from the options provided.
3. **Click Submit:** After selecting the layout, click the "Submit" button to apply the changes.

---

## Layouts Package Integration Steps

### Step 1: Add the Package Folder to Root
Place the package folder at the root of your project.

### Step 2: Update `composer.json`
Add the following code under the `autoload` section of your `composer.json` file:

```json
"autoload": {
    "psr-4": {
        "Biz\\Layout\\": "packages/biz/layout/src/"
    }
}
```

### Step 3: Update `config/app.php`
Add the following code under the `providers` section in the `config/app.php` file:

```php
Biz\Layout\Providers\LayoutProvider::class,
```

### Step 4: Run Commands
Execute the following commands to update and optimize your project:

```bash
composer dump-autoload
php artisan optimize
```

### Step 5: Check Changes
Run the following command to publish vendor files:

```bash
php artisan vendor:publish
```

Verify the installation by visiting `yourdomain.com/layouts`.

---

## Using the Plugin
Once the layout package is enabled, the dashboard will instantly reflect the changes, giving you a fresh, customized layout according to your selection.

---

## Troubleshooting and Support

### Error During Installation?
- Double-check the commands you entered in the terminal and ensure the package was uploaded to the correct root directory.

### Layout Not Updating?
- Ensure the layout package is enabled through the “Choose Layout” menu and that you’ve clicked “Submit.”

---

## Conclusion
Our Tokenlite layout changer plugin is designed to simplify and enhance your Tokenlite experience, giving you greater control over the dashboard’s appearance. By following this documentation, you can quickly install and activate the plugin for your customized layout.

