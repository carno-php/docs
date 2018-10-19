# 文件上传

```php
$submit = [
    'name' => 'moyo',
    'file' => new \Carno\HTTP\Standard\Streams\File('/tmp/filename.txt'),
];
$resp = yield \Carno\HTTP\Client::post('http://httpbin.org/post', $submit);
```
