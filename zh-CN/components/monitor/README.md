# 监控

## 指标类型

- counter / 计数器
- gauge / 计量器
- histogram / 直方图
- summary / 分位数

## 创建指标

### 基本对象

```php
// 创建一个计数器
Metrics::counter();
// 创建一个计量器
Metrics::gauge();
// 创建一个计量器，初始值为 100
Metrics::gauge(100);

// 创建一个直方图，手动指定 bucket
Metrics::histogram()->fixed(10, 20, 500, 1000);
// 创建一个直方图，生成线状值：初始10，递增5，数量3 -> [10,15,20]
Metrics::histogram()->linear(10, 5, 3);
// 创建一个直方图，生成指数值：初始2，指数2，数量3 -> [2,4,8]
Metrics::histogram()->exponential(2, 2, 3);

// 创建一个分位数，统计 [20%,50%,90%,95%,99%] 的数据分布情况
Metrics::summary(0.2, 0.5, 0.9, 0.95, 0.99);
```

### 通用接口

```php
// named 为指标名称，格式：key1.key2.key3
// labels 为标签列表，格式为数组
Metrics::counter()->named('biz.metric.name')->labels(['label' => 'val']);
```

### 统计接口

```php
Metrics::counter()->inc(float $v = 1);

Metrics::gauge()->inc(float $v = 1);
Metrics::gauge()->dec(float $v = 1);
Metrics::gauge()->set(float $v);

Metrics::histogram()->observe(float $v);

Metrics::summary()->observe(float $v);
```
