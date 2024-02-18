---
sidebar_position: 5
---

# Rule Engine

## Input Data

Conceptually, the Rule Engine deals with a stream of tuples (including message, timestamp, topic, message type). When writing rules, users can access the input data through corresponding variables (msg, ts, topic, msgtype).

Depending on the file type being processed, the coScene agent will populate the variables according to the following table:

|               | Bag file (ROS, MCap, etc) | Log file                                                                                                                                   |
| ------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `msg: any`    | Message data              | Encapsulated from a line in the log file as [Foxglove.Log](https://github.com/foxglove/schemas/blob/main/schemas/proto/foxglove/Log.proto) |
| `ts: float`   | Timestamp                 | Parsed from a single line log                                                                                                              |
| `topic: str`  | Topic name                | Log file name                                                                                                                              |
| `msgtype:str` | Message type              | `Foxglove.Log`                                                                                                                             |

Note:

- Timestamp is the number of seconds elapsed since 1970/01/01 00:00:00, in float type.
- Efforts will be made to parse the timestamp, for more information see [Supported Timestamp Formats](https://docs.coscene.cn/docs/recipes/data-diagnosis/rule-format#Prerequisites-for-Using-Rules)

## Log Data

To facilitate the reading of log data, we provide additional extractors for the following log data types (`log`, `log_level`):

- Protobuf or JSON: `foxglove.Log`
- ROS: `foxglove_msgs/Log`
- ROS: `rosgraph_msgs/Log`

**`log`: Filters the supported message types and returns the log content**

```yaml
log == 'Error occurred!' # Triggers when a line of log is 'Error occurred!'
```

**`log_level`: Filters the supported message types and returns the log level**

Users can enumerate different log levels using log_level

- INFO
- WARN
- ERROR
- FATAL

```yaml
log_level == LogLevel.FATAL # Triggers whenever a FATAL log appears
```

## Operators

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

## Sequence Matchers

- **sustained**

  `sustained(context, condition, duration)`

  Triggers when the given `condition` is true for a duration longer than `duration`. (`context` is the message filter used to evaluate `condition`.)

  ```python
  # The syntax below monitors all messages with topic '/velocity',
  # and triggers if the value of liner.x is greater than 20 for more than 10 s
  sustained(
    topic == '/velocity',
    msg.linear.x > 20,
    10
   )
  ```

- **repeated**

  `repeated(condition, times, duration)`

  Triggers when the given `condition` is triggered `times` within the specified `duration`.

  ```python
  # Triggers when 'Error 12345 happened' is included in the log, and occurs 5 times within 60 seconds
  repeated(
    'Error 12345 happened' in log,
    5,
    60
  )
  ```

- **sequential**

  `sequential(c1, c2, ..., duration)`

  Sequential can set any number of conditions, and triggers if all conditions are triggered in order within the `duration` in seconds.

  If no `duration` is set, then there is no time limit.

  ```python
  # Triggers if all initialization is executed and time is less than 10 seconds
  sequential(
    'Initialization start' in log,
    'All modules loaded' in log,
    'Localization initialized' in log,
    'Initialization complete' in log,
    duration=10
  )

  # Triggers if the task fails, with no time limit
  sequential(
    'Task started' in log,
    'Task failed' in log
  )
  ```

- **throttle**

  `throttle(condition, duration)`

  The `condition` triggers no more than once within the `duration` in seconds. If triggered multiple times within the `duration`, only the first data meeting the `condition` triggers the condition.

  ```python
  throttle(
      "123" in log,
      2
  )
  ```

- **debounce**

  `debounce(condition, duration)`

  Triggers when the `condition` is met. This syntax includes a timer; if the `condition` is triggered again within the `duration` in seconds, `debounce` does not trigger and the timer is reset.

  ```python
  # Triggers when 'Error 12345' is detected, if 'Error 12345' triggers multiple times within 2 seconds,
  # only the first detected 'Error 12345' triggers
  debounce(
    'Error 12345' in log_text,
    2
  )
  ```

- **any_order**

  `any_order(condition1, condition2, ...)`

  All `conditions` trigger, regardless of the order of occurrence.

  ```python
  any_order("123" in log, "789" in log, "456" in log)
  ```

- **timeout**

  `timeout(condition1, condition2, ..., duration)`

  If all `condition1` triggers, but the remaining `condition` fails to be sequentially triggered within the `duration`, this rule triggers.

  ```python
  # The condition triggers if all conditions are not triggered within the duration period

  timeout("123" in log, "456" in log, duration=1)
  ```

## Value Passing

`get_value(key)` and `set_value(key, value)`, two methods are used for passing values between different conditions.

```python
# Triggers if a request completes within the given time.
# Requests are matched by id
sequential(
  set_value('req_id', regex_search(log_text, 'Send request (\\d+)').group(1)),
  regex_search(log_text, 'Request (\\d+) completed').group(1) == get_value('req_id'),
  duration=10
)
```

## Utilities

- **`concat(...)`: String concatenation**

  ```python
  concat('a', 'b', 123) # 'ab123'
  ```

- **`regex_search(value, pattern)`: Checks if `value` matches `pattern`**

  If successfully matched, returns a Python `Match` object.

  ```python
  regex_search('Current speed is 20', 'speed is (\\d+)').group(1) # 20
  ```
