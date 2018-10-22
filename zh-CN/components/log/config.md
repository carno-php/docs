# 动态配置

> 可以通过配置中心对日志的行为进行控制（实时生效）

## 配置项

> 所有的配置项同时还支持 `SCENE.log.xxx` 的键，优先级比 `log.xxx` 高（优先覆盖）

### log.level

- emergency
- alert
- critical
- error
- warning
- notice
- info | 默认
- debug

### log.format

- json
- text | 默认

### log.addr

- tcp
  > tcp://127.0.0.1:5140
- stdout | 默认

### log.replica

[使用 Log.IO](replicas/logio.md)
