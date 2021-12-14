my modifications to pixel_led_mqtt_panel project
------------------------------------------------


https://github.com/widapro/pixel_led_mqtt_panel

automation:

```
alias: wled - clock
description: ''
trigger:
  - platform: time_pattern
    minutes: /1
condition: []
action:
  - service: mqtt.publish
    data:
      topic: wledclock/intensity
      payload: '0'
  - service: mqtt.publish
    data:
      topic: wledclock/scrolleffect_without_exit
      payload_template: PA_MESH
  - service: mqtt.publish
    data:
      topic: wledclock/zone1_text
      payload: C
  - service: mqtt.publish
    data:
      topic: wledclock/zone0_text
      payload_template: '{{ now().strftime(''%d %b, %a'') }}'
  - delay:
      hours: 0
      minutes: 0
      seconds: 5
      milliseconds: 0
  - service: mqtt.publish
    data:
      topic: wledclock/zone1_text
      payload: '3'
  - service: mqtt.publish
    data:
      topic: wledclock/zone0_text
      payload_template: 'out: {{ states(''sensor.weatherstation_temp'') }} C'
  - service: mqtt.publish
    data:
      topic: wledclock/scrolleffect_without_exit
      payload_template: PACMAN
  - delay:
      hours: 0
      minutes: 0
      seconds: 5
      milliseconds: 0
  - service: mqtt.publish
    data:
      topic: wledclock/zone1_text
      payload: c
  - service: mqtt.publish
    data:
      topic: wledclock/zone0_text
      payload_template: '{{ as_timestamp(now()) | timestamp_custom(''%H:%M'') }}'
mode: single
```