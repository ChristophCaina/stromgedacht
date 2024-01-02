# stromgedacht
Template for StromGedacht Rest-API sensor
---

## How To

1. Create a Sensor in your sensor.yaml file:
```
- platform: rest
  resource: https://api.stromgedacht.de/v1/now?zip={PLZ}
  name: Stromgedacht Status
  json_attributes: 
    - state
  value_template: >
    {% set mapper = {
        -1: "Super-Grüne Phase",
        1: "Grüne Phase",
        3: "Orange Phase",
        4: "Rote Phase",
    } %}
    {% set state = value_json.state %}
    {{ mapper[state] if state in mapper else state }}
```

2. Replace `{PLZ}` in the above resource URL with your post-code

3. Add the sensor to your Dashboard -> I prefer to use a TileCard

4. If you are using Card-Mod (HACS), you can use the following yaml template to change the Icon Color based on the
Sensors Value:
```
card_mod:
  style: |
    ha-card {
              {% if is_state_attr('sensor.stromgedacht_status', 'state', -1) %}
                --tile-color:var(--lime-color) !important;
              {% elif is_state_attr('sensor.stromgedacht_status', 'state', 1) %}
                --tile-color:var(--green-color) !important;
              {% elif is_state_attr('sensor.stromgedacht_status', 'state', 3) %}  
                --tile-color:var(--orange-color) !important;
              {% elif is_state_attr('sensor.stromgedacht_status', 'state', 4) %}  
                --tile-color:var(--red-color) !important;
              {% endif %}  
            }
```

![grafik](https://github.com/ChristophCaina/stromgedacht/assets/26391061/205bc607-7172-4d5f-b8aa-955c34e32836)
![grafik](https://github.com/ChristophCaina/stromgedacht/assets/26391061/11bee6d5-e149-462d-8816-7467ca384a67)
![grafik](https://github.com/ChristophCaina/stromgedacht/assets/26391061/0ccae035-6006-40bb-8a0e-ad0f07b6251f)
![grafik](https://github.com/ChristophCaina/stromgedacht/assets/26391061/1967c99a-090d-458a-842e-ab4f4faf9cab)
