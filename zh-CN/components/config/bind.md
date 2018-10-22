# 对象绑定

先创建一个 demo 对象

```php
class Opts
{
    public $opt1 = 'conf1';
    public $opt2 = 123;
}
```

和 Config 绑定起来

```php
$opts = config()->bind(
    new Opts,
    [
        'some-key-in-consul' => [
            'c.opt1' => 'opt1',
            'c.opt2' => 'opt2'
        ]
    ]
);
```

* $opts 是一个支持配置自动同步的对象（Opts）
* "some-key-in-consul" 是后端 KV 上的一个目录
* c.opt1 和 c.opt2 是目录下的配置项，数据有变化时 $opts 对象的 opt1 和 opt2 会自动同步
