# Home Assistant Raspberry Pi RF custom integration

**This is a spin-off from the original Home Assistant integration which was marked as deprecated and will be removed in Home Assistant Core 2022.4.**

## About
The `rpi_rf` switch platform allows you to control devices over 433/315MHz LPD/SRD signals with generic low-cost GPIO RF modules on a [Raspberry Pi](https://www.raspberrypi.org/).

Interoperable with codes sniffed via [the rpi-rf module](https://pypi.python.org/pypi/rpi-rf) or [rc-switch](https://github.com/sui77/rc-switch).
For more info see the PyPi module description: [rpi-rf](https://pypi.python.org/pypi/rpi-rf).

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
