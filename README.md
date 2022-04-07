# Home Assistant Raspberry Pi RF custom integration

**This is a spin-off from the original Home Assistant integration which was deprecated and was removed in Home Assistant Core v2022.4.**

## About
The `rpi_rf` switch platform allows you to control devices over 433/315MHz LPD/SRD signals with generic low-cost GPIO RF modules on a [Raspberry Pi](https://www.raspberrypi.org/).

Interoperable with codes sniffed via [the rpi-rf module](https://pypi.python.org/pypi/rpi-rf) or [rc-switch](https://github.com/sui77/rc-switch).
For more info see the PyPi module description: [rpi-rf](https://pypi.python.org/pypi/rpi-rf).

# Installation

### HACS

The recommend way to install `rpi_rf` is through [HACS](https://hacs.xyz/).

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
