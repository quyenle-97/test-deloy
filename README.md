## Mô tả
1. Chọn country proxy muốn mua
2. Chọn số lượng
3. Thanh toán

## Giao diện
giao diện tương tự: https://proxyaz.com/order

## Giao diện panel user:
| Proxy IP | Port HTTP(s) | Port SOCKS5 |	USER | PASSWORD | IP AUTHENTICATON | MAC AUTHENTICATON |
| -------- | ------------ | ----------- | ---- | -------- | ---------------- | ----------------- |

## Thông tin khách hàng có thể thay đổi
- PASSWORD: Từ 6-12 ký tự
- IP AUTHENTICATON: Mặc định khi mới tạo là 255.255.255.255
- MAC AUTHENTICATON: khách hàng có thể điền định dạng (ví dụ): 00-15-5d-a9-53-50, 00:15:5d:a9:53:50 nhưng khi đẩy lệnh lên api quy về định dạng 00155da95350

## Server test
Khi KH đổi tự động đẩy api lên server chứa proxy đó. Server test:
- http://103.89.90.199:88/account
- admin
- zxc123123

## API
Sử dụng HTTP request trong laravel để gửi API
https://laravel.com/docs/8.x/http-client#making-requests

## Resource
- Font icon: https://iconify.design/icon-sets/typcn/
- Template demo: https://www.bootstrapdash.com/demo/azia/v1.0.0/template/table-basic.html

## How to run
Clone and prepare source code:
- `git clone git@github.com:mysang/vnproxy.vn.git`
- `cd vnproxy.vn`
- `cp .env.example .env`
- `cp src/laravel/.env.example src/laravel/.env`
- Config host with contents:
  ```
  127.0.0.1 vnproxy.vn
  127.0.0.1 db.vnproxy.vn
  ```
- `docker-compose up`

## Guide
Phương thức khai báo trong route và controller
| Verb      | URI               | Action  | Route Name      |
| --------- | ----------------- | ------- | --------------- |
| GET       | /photos           | index   | photos.index    |
| GET       | /photos/create    | create  | photos.create   |
| POST      | /photos           | store   | photos.store    |
| GET       | /photos/{id}      | show    | photos.show     |
| GET       | /photos/{id}/edit | edit    | photos.edit     |
| PUT/PATCH | /photos/{id}      | update  | photos.update   |
| DELETE    | /photos/{id}      | destroy | photos.destroy  |

Mẫu route
```php
# Proxy server
Route::prefix('proxy-servers')->name('proxy_servers.')->group(function() {
    Route::get('/', 'ProxyServerController@index')->name('index');
    Route::get('add', 'ProxyServerController@create')->name('create');
    Route::post('/', 'ProxyServerController@store')->name('store');
    Route::get('{id}/edit', 'ProxyServerController@edit')->name('edit');
    Route::put('{id}', 'ProxyServerController@update')->name('update');
    Route::delete('{id}', 'ProxyServerController@destroy')->name('destroy');
});
```

## Autodeploy
Using Github Actions to implement auto deploy
#### Create environment variable
- `export ENV_PATH=/home/vnproxy/.env`
- `export BACKUP_PATH=/home/vnproxy/backups`
- Create `.env` file at /home/vnproxy/.env

## Note
- Server A admin tạo sẵn 100 proxies
- Server B admin tạo sẵn 100 proxies
- Server C admin tạo sẵn 100 proxies

Tổng hệ thống sẽ có 300 proxies, admin add (import) lên web sẵn. Khách order sẽ nhấc random ra. Họ có quyền chỉnh sửa pass, mac và IP

## Release Change Logs
Version 1.0
Date: 2020/08/28
Domain: https://iproxy.vn
