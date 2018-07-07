# Laravel Adminer 套件範例

LaravelConf Taiwan 2018 套件發表會 (2018.07.08)

Laravel Adminer 套件範例

套件作者：Winnie Lin

## 範例環境

- Laravel 5.6.26
- MySQL 5.5.42
- 套件：[Laravel-Adminer](https://packagist.org/packages/onecentlin/laravel-adminer) v4.6.3

## 建立 Laravel 專案

```
laravel new [project_name]
```

## 修改 `.env` 設定資料庫

依需求變更

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
```

## 安裝內建驗證基架

```
php artisan make:auth
```

## 遷移驗證資料庫

```
php artisan migration
```

## 安裝 laravel-adminer 套件

```
composer require onecentlin/laravel-adminer
```

## 設定套件組態

修改 `config/app.php` 檔案

```php
'providers' => [
    ...

    // 加入套件設定
    Onecentlin\Adminer\ServiceProvider::class,
];
```

變更語系

```php
'locale' => 'zh-TW',
```

修改 `app/Http/Kernel.php` 檔案

```php
protected $middlewareGroups = [
    ...

    // 加入 adminer 群組設定
    'adminer' => [
        \App\Http\Middleware\EncryptCookies::class,
        \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
        \Illuminate\Session\Middleware\StartSession::class,

        // 採用內建的驗證
        \Illuminate\Auth\Middleware\Authenticate::class,
    ],
];
```

## 瀏覽執行 (`php artisan serve`)

```
http://127.0.0.1:8000/adminer
```
