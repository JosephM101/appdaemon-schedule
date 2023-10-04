# appdaemon-schedule
A simple scheduler for Home Assistant/AppDaemon.
Originally written for controlling an irrigation system, but can be used to control anything with a binary on/off function.

I wrote this because I couldn't find a library/applet for Home Assistant that was good enough to suit my needs, so I decided to make my own, aimed at being flexible and easy to set up, even for multiple schedules.


## Install
- Download this repository, and copy the "schedule" folder to "appdaemon/apps".
- Add your configuration to `apps.yaml` using one of the examples below.

  <i>This repo is not currently in HACS. Maybe a future endeavor?</i>


## Usage
### Example `apps.yaml` configuration
```yaml
# Irrigation system
my_schedules:
  module: schedule
  class: Schedule
  schedules:
    water_the_plants:
      on_at: "8:00:00" # 24hr
      off_at: "8:10:00"
      target_entity: switch.irrigator_switch
```

## 12-hour (AM/PM) time support
#### <i>This feature was introduced with version 1.0.1.</i>

The variables `on_at` and `off_at`, by default, take 24-hour time strings. But optionally, you can provide 12-hour times using the `hour`, `minute`, `second` and `meridiem` parameters in place of the standard 24-hour time string.


### Here's an example of the 12-hour format in action:
```yaml
# Irrigation system
my_schedules:
  module: schedule
  class: Schedule
  schedules:
    water_the_plants:
      on_at:
        hour: 8
        meridiem: AM  # Accepts either AM or PM; not case-sensitive
      off_at: 
        hour: 8
        minute: 15
        meridiem: AM
      target_entity: switch.irrigator_switch
```
In the above example, you might have noticed that the `minute` variable was missing from `on_at`. That's because `hour` and `meridiem` are the only required variables; `minute` and `second` default to 0 if not specified.

### 12-hour time parameters:
| Parameter name | Optional | Description | Default value |
| --- | --- | --- | --- |
| `hour`     | <i> No </i> | An hour value (1 to 12)
| `minute`   | <i> Yes  </i> | A minute value (0 to 59) | `0`
| `second`   | <i> Yes  </i> | A second value (0 to 59) | `0`
| `meridiem` | <i> No </i> | AM/PM



## <b>TODO: Plans for the future</b>
- Add the ability to specify run conditions for schedules
- Allow for specifying a run duration instead of an end time
