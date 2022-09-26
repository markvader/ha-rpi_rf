# Home Assistant Raspberry Pi RF custom integration

**This is a spin-off from the original Home Assistant integration which was deprecated and was removed in Home Assistant Core v2022.4.**

## About
The `rpi_rf` switch platform allows you to control devices over 433/315MHz LPD/SRD signals with generic low-cost GPIO RF modules on a [Raspberry Pi](https://www.raspberrypi.org/).

Interoperable with codes sniffed via [the rpi-rf module](https://pypi.python.org/pypi/rpi-rf) or [rc-switch](https://github.com/sui77/rc-switch).
For more info see the PyPi module description: [rpi-rf](https://pypi.python.org/pypi/rpi-rf).

# Installation

### HACS

The recommended way to install `rpi_rf` is through [HACS](https://hacs.xyz/).

### Manual installation

Copy the `rpi_rf` folder and all of its contents into your Home Assistant's `custom_components` folder. This folder is usually inside your `/config` folder. If you are running Hass.io, use SAMBA to copy the folder over. You may need to create the `custom_components` folder and then copy the `rpi_rf` folder and all of its contents into it.

## Configuration

To enable, add the following to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
switch:
  - platform: rpi_rf
    gpio: 17
    switches:
      bedroom_light:
        code_on: 1234567
        code_off: 1234568
      ambilight:
        pulselength: 200
        code_on: 987654
        code_off: 133742
        length: 24
      living_room_light:
        protocol: 5
        code_on: 654321,565874,233555,149874
        code_off: 654320,565873,233554,149873
        signal_repetitions: 15
```

### Options

| Key                  | Required | Default | Type    | Description                                                                                                                   |
| -------------------- | -------- | ------- | ------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `gpio`               | yes      |         | integer | GPIO to which the data line of the TX module is connected.                                                                    |
| `switches`           | yes      |         | list    | The array that contains all switches.                                                                                         |
| `entry`              | yes      |         | list    | Name of the switch. Multiple entries are possible.                                                                            |
| `code_on`            | yes      |         | list    | Decimal code(s) to switch the device on. To run multiple codes in a sequence, separate the individual codes with commas ‘,’.  |
| `code_off`           | yes      |         | list    | Decimal code(s) to switch the device off. To run multiple codes in a sequence, separate the individual codes with commas ‘,’. |
| `protocol`           | no       |  `1`    | integer | RF Protocol.                                                                                                                  |
| `pulselength`        | no       |         | integer | Pulselength.                                                                                                                  |
| `signal_repetitions` | no       |  `10`   | integer | Number of times to repeat transmission.                                                                                       |
| `length`             | no       |  `24`   | integer | Code Length |



## Additional Customisation

Thanks to the [work](https://github.com/markvader/ha-rpi_rf/pull/48) of [@oskargert](https://www.github.com/oskargert) this integration's switch entities now utilises unique_id's which allow us to customise a lot more features within home assistant such as Icons, Show as, Area and the ability to quickly rename the Entity Name & Entity ID. Just click on the entity name, then go to the settings tab, and make it your own.

![additional customisation rpi-rf](https://user-images.githubusercontent.com/217953/192374175-fe598f1b-e1c0-45ab-a167-d6c199902100.png)


**An important note on this.**
- The unique_id for each entity is generated from the code_on & code_off values.
- Should you change these in the future and/or add additional code(s) to a code sequence, the unique_id will be regenerated and Home Assistant will recognise a new entity.
- It is safe to remove the old entity (It will show as "restored" in the list of entities).
- The old entity and its customisation (icon, area etc) will be lost and you will need to reenter these customisations for the new entity.

- Additionally, you will be unable to have two entities with identical code_on & code_off values (not sure thats ever likely to happen as if you had more than one device in a home with the same RF codes as it would be impossible to control a single device.)
