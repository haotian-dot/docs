---
sidebar_position: 5
---
# 规则引擎

## 输入数据

从概念上来说，RuleEngine 处理的是一个元组的数据流（元组包含 message, timestamp, topic, message type），当编写规则时，使用者可以通过相应变量来访问输入数据（msg, ts, topic, msgtype）。

根据处理的文件类型，coScene agent 将会根据下列图表填充变量：

|  | Bag file (ROS， Mcap，etc) | Log file |
| -- | -- | -- |
| `msg: any` | Message 数据 | 由log文件中的一行信息封装成的 [Foxglove.Log](https://github.com/foxglove/schemas/blob/main/schemas/proto/foxglove/Log.proto) |
| `ts: float` | 时间戳 | 从单行log中解析出的时间戳 |
| `topic: str` | Topic 名称 | log文件名 |
| `msgtype:str` | 消息类型 | `Foxglove.Log` |

注：
  - 时间戳为自 1970/01/01 00:00:00 经历的秒数，float 类型
  - 时间戳的解析将尽力完成，相关信息见[支持的时间戳格式](https://docs.coscene.cn/docs/recipes/data-diagnosis/rule-format#%E8%A7%84%E5%88%99%E7%9A%84%E4%BD%BF%E7%94%A8%E5%89%8D%E6%8F%90)

<br />

## Log 数据

为了方便读取日志数据，我们为以下 log 数据类型提供了额外的提取器 (`log`、`log_level`)
- Protobuf or JSON: `foxglove.Log`
- ROS: `foxglove_msgs/Log`
- ROS: `rosgraph_msgs/Log`

<br />

**`log`: 过滤支持的消息类型，并且返回 log 内容**
  
```yaml
log == 'Error occurred!' # 当一行日志信息为 'Error occurred!'时触发
```

<br />

**`log_level`: 过滤支持的消息类型，并返回 log 的等级**

用户可以使用 log_level 枚举不同的日志等级
- INFO
- WARN
- ERROR
- FATAL

```yaml
log_level == LogLevel.FATAL # 每当出现 FATAL 日志时触发
```

<br />

## 运算符

- `==`
- `!=`
- `>`
- `>=`
- `<`
- `<=`
- `a and b`
- `a or b`
- `not a`
- `a in b`

<br />

## 序列匹配器

- **sustained**
  
  `sustained(context, condition, duration)`

    当给定 `condition` 为真的持续时间超过 `duration` 时，条件会被触发。 (`context` 是用于评估 `condition` 的消息过滤器。)
  
    ```python
    # 下面的语法会监测所有 topic 为 ‘/velocity’的消息，
    # 如果其 liner.x 的值大于 20 且持续时间大于 10 s
    # 该条件将会被触发
    sustained(
      topic == '/velocity',
      msg.linear.x > 20,
      10
     )
    ```

<br />

- **repeated**
  
  `repeated(condition, times, duration)`
  
  当给定 `condition` 在给定的 `duration` 内被触发 `time` 次时，条件会被触发。

  ```python
  # 当日志中包含‘Error 12345 happened’，且在 60 秒内出现了 5 次，条件被触发
  repeated(
    'Error 12345 happened' in log,
    5,
    60
  )
  ```

<br />

- **sequential**

  `sequential(c1, c2, ..., duration)`

  sequential 可以设定任意数量的条件，如果在以秒为单位的 `duration` 内，所有的条件都按顺序触发，条件会被触发。

  如果没有设置 `duration`，则没有时间限制

  ```python  
  # 初始化全部执行，且时间小于 10 秒，则被触发
  sequential(
    'Initialization start' in log,
    'All modules loaded' in log,
    'Localization initialized' in log,
    'Initialization complete' in log,
    duration=10
  )

  # 任务失败则被触发，无时间限制
  sequential(
    'Task started' in log,
    'Task failed' in log
  )
  ```

<br />

- **throttle**
  
  `throttle(condition, duration)`

  `condition` 在以秒为单位的 `duration` 内触发不多于 1 次，如果 `duration` 内多次被触发，仅第一次满足 `condition` 的数据会触发该条件

  ```python
  throttle(
      "123" in log,
      2
  )
  ```

<br />

- **debounce**
  
  `debounce(condition, duration)`

  `condition` 被满足时会被触发。在这个语法中包含了一个定时器，如果在以秒为单位的 `duration` 内` condition` 再次被触发，` debounce` 不会被触发，且定时器会被重置

  ```python  
  # 当监测到‘Error 12345’时会被触发，‘Error 12345’在 2 秒内多次触发时，
  # 仅第一次监测到的‘Error 12345’会被触发
  debounce(
    'Error 12345' in log_text,
    2
  )
  ```
  
<br />

- **any_order**
  
  `any_order(condition1, condition2, ...)`
  
  所有 condition 被触发，无视触发数顺序

  ```python
  any_order("123" in log, "789" in log, "456" in log)
  ```

<br />

- **timeout**
  
  `timeout(condition1, condition2, ..., duration)`

  所有的 `condition1` 触发后，剩余的 `condition` 未能在 `duration` 时间段内被依次触发，则该条件触发

  ```python
  # 如果所有的condition没有在duration时间段内被触发，则该条件被触发
  
  timeout("123" in log, "456" in log, duration=1)
  ```
  
<br />

## 值传递

`get_value(key)` 和 `set_value(key, value)` 两个方法用于在不同的条件之间进行值传递。 

```python
# Triggers if a request completes within the given time.
# Requests are matched by id
sequential(
  set_value('req_id', regex_search(log_text, 'Send request (\\d+)').group(1)),
  regex_search(log_text, 'Request (\\d+) completed').group(1) == get_value('req_id'),
  duration=10
)
```

<br />

## 功能函数

- **`concat(...)`: 字符串连接**

  ```python
  concat('a', 'b', 123) # 'ab123'
  ```

<br />

- **`regex_search(value, pattern)`: 监测 `value` 与 `pattern` 是否匹配**
  
  如果成功匹配，则返回 Python `Match` 对象
  
  ```python
  regex_search('Current speed is 20', 'speed is (\\d+)').group(1) # 20
  ```
