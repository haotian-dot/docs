---
sidebar_position: 4
---

# Rule Configurations and Examples

## Prerequisites for Using Rules

Rules are effective only for data of a particular format, i.e., streaming data that includes a message, timestamp, topic, and message type.

The supported timestamp formats are as follows ([reference document](https://www.w3schools.com/python/python_datetime.asp)):

<table>
    <tr>
        <th>Timestamp Types</th><th>Timestamp Formats</th><th>Examples</th>
    </tr>
    <tr>
        <td rowspan="4">General<p><i>*Timestamp in the file</i></p></td><td>%m%d %H:%M:%S.%f</td><td>0212 12:12:12.548513</td>
    </tr>
    <tr>
        <td>%b %d %H:%M:%S</td><td>Dec 12 12:12:12</td>
    </tr>
    <tr>
        <td>%Y-%m-%d %H:%M:%S.%f</td><td>2023-02-12 12:12:12.548513</td>
    </tr>
    <tr>
        <td>%H:%M:%S.%f</td><td>12:12:12.548513</td>
    </tr>
    <tr>
        <td rowspan="3">Special<p><i>*Filename/Timestamp in the first line of the file content</i></p><p><i>(For cases where the timestamp in the file does not fully include year, month, day, hour, minute, and second.)</i></p></td><td>%Y-%m-%d %H:%M:%S</td><td>2023-02-12 12:12:12</td>
    </tr>
    <tr>
        <td>%Y/%m/%d %H:%M:%S</td><td>2023/02/12 12:12:12</td>
    </tr>
    <tr>
        <td>%Y%m%d%H</td><td>2023021212</td>
    </tr>
</table>

For other timestamp formats, please contact CoScene.

## Basic Structure of Rules

The basic structure of data collection and diagnostic rules is as follows:

```yaml
name: diagnosis rule
rules:
  - when:
      - msg.somevalue > 10
      - msg.othervalue < 10
    actions:
      - upload()
      - create_moment('Value is not expected')
enabled: true
version: v1
```

- **name: Rule Group Name**
  - Custom rule group name; a rule group can contain multiple rules.
- **when: Rule Trigger Conditions**
  - Defines key events in the log, such as the log containing a certain field.
  - Any condition in 'when' triggers all the following actions.
- **actions: Actions After Rule is Triggered**
  - Defines whether to trigger data uploads, create moments, create & assign tasks, etc.
  - Any of the above conditions will trigger all actions.
- **enabled: Whether the Rule Group is Enabled**
  - 'true' means enabled. When the rule group is enabled, data in the device or project will trigger the rule and perform predefined actions.
  - 'false' means disabled. When the rule group is disabled, data in the device and project no longer executes the rules in this rule group.
- **version: Rule Group Version**
  - The current rule group version must be 'version: v1'.

<br />

## Common Rule Usage Examples

> Below are some examples of typical rule trigger conditions.

```yaml
# Triggered a certain error code
'Error code 123 happened' in log

# Check if the speed in the x direction is between 4~10
topic == '/velocity' and 4 < msg.linear.x < 10

# Analyze the value in the log and check if it's between 4~10
4 < regex_search(log, 'X velocity is (\\d+)').group(1) < 10

# Robot did not start charging 30 seconds after returning to the charging station
timeout(
  'Returned to base' in log,
  'charging state: CHARGING' in log,
  duration=30
)

# The command did not complete within 10 seconds
timeout(
  set_value('cmd_id', regex_search(log, 'Sending command id (\\d+)').group(1)),
  regex_search(log, 'Command (\\d+) finished').group(1) == get_value('cmd_id'),
  duration=10
)

# If the temperature rises by 5 within 60 seconds
# Assuming there's a `value` field in the message
topic == '/temp' and sequential(
  set_value('start_temp', msg.value),
  msg.value - get_value('start_temp') > 5,
  duration=60
)

# Check if initialization completes within 20 seconds
timeout(
  'Initialization start' in log,
  # The three modules can finish init in any order
  any_order(
    'GPS started' in log,
    'Localization started' in log,
    'Motor online' in log),
  'Initialization finished' in log,
  duration=20
)

# Detect if a topic hasn't received a message for more than 20 seconds,
# e.g., the localization module is down
timeout(
  topic == '/localization',
  topic == '/localization',
  duration=20
)

# Temperature is above 40 for more than 60 seconds
sustained(
  topic == '/temp',
  msg.value > 40,
  duration=60
)

# Chassis loop frequently times out: more than 10 timeouts within 60 seconds
repeated(
  timeout(
    'Send chassis command' in log,
    'Chassis received' in log,
    duration=1
  ),
  times=10,
  duration=60
)

# Trigger error, but ignore it under the following conditions
# The error occurred within a 10-second interval
debounce(
  'Error 123' in log,
  duration=10
)
```

<br />

## Common Rule Action Examples

> The following shows some typical rule-triggered actions.

```yaml
# Create a record on the Kexing platform and upload files that triggered the corresponding conditions in the record.
upload()

# Create a record named "Localization Error", with the description "Localization anomaly detected, please check", and with labels "Localization" and "Urgent".
# Also, upload the corresponding file in the record.
upload(title="Localization Error", description="Localization anomaly detected, please check", labels=["Localization","Urgent"])

# Create a record named "Localization Error", upload the corresponding file in the record, and also upload an additional file /root/map.png.
upload(title="Localization Error", extra_files=["/root/map.png"])

# Create a moment (mark at the time point when the rule condition is triggered), with the name "Localization Error".
create_moment('Localization Error')

# Create a moment named "Localization Error", with the description "Localization error at this moment", and a duration of 3 seconds.
create_moment(title="Localization Error", description="Localization error at this moment", duration=3)

# Create a moment named "Localization Error", and also create a task.
create_moment(title="Localization Error", create_task=True)
```

<br />
