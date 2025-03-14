---
title: "Configure a fake motor"
linkTitle: "fake"
weight: 10
type: "docs"
description: "Configure a fake motor to test software without any hardware."
images: ["/components/img/components/motor.svg"]
# SMEs: Rand, James
---

Configuring a `fake` motor can be convenient for testing software without using any hardware.
For example, you can use a `fake` component as a placeholder while waiting on a hardware shipment, so that other components that depend on this motor (for example, a [base](/components/base/)) won't fail to initialize, and your SDK code won't throw errors when it fails to find a physical motor connected to your robot.

{{< tabs name="fake-config">}}
{{% tab name="Config Builder" %}}

Navigate to the **Config** tab of your robot's page in [the Viam app](https://app.viam.com).
Click on the **Components** subtab and navigate to the **Create component** menu.
Enter a name for your motor, select the type `motor`, and select the `fake` model.

Click **Create component**.

![A fake motor config.](../../img/motor/fake-config-ui.png)

Edit and fill in the attributes as applicable.

{{% /tab %}}
{{% tab name="JSON Template" %}}

```json
{
  "components": [
    {
      "name": "<your-motor-name>",
      "type": "motor",
      "model": "fake",
      "attributes": {
        <...>
      },
      "depends_on": []
    }
  ]
}
```

{{% /tab %}}
{{% tab name="JSON Example" %}}

```json
{
  "components": [
    {
      "name": "fake-motor",
      "type": "motor",
      "model": "fake",
      "attributes": {
        "pins": {
          "dir": "",
          "pwm": ""
        },
        "board": "",
        "dir_flip": false
      },
      "depends_on": []
    }
  ]
}
```

{{% /tab %}}
{{< /tabs >}}

Since a `fake` motor isn't a physical piece of hardware, attributes are only representational and not required.
However, if you would like to mock up a virtual placeholder for a real, physical motor, you can configure some or all of the following attributes:

| Name | Type | Inclusion | Description |
| ---- | ---- | --------- | ----------- |
| `board` | string | Optional | `name` of the [board](/components/board/) to which the motor driver is wired. |
| `min_power_pct` | number | Optional | Sets a limit on minimum power percentage sent to the motor. <br> Default: `0.0` |
| `max_power_pct` | number | Optional | Range is 0.06 to 1.0; sets a limit on maximum power percentage sent to the motor. <br> Default: `1.0` |
| `pwm_freq` | int | Optional | Sets the PWM pulse frequency in Hz. Many motors operate optimally in the kHz range. <br> Default: `800` |
| `encoder` | string | Optional | The name of an encoder attached to this motor. See [encoded motor](/components/motor/gpio/encoded-motor/). *If an encoder is configured on a `fake` motor, `ticks_per_rotation` becomes required.* |
| `max_rpm` | number | Optional | An estimate of the max revolutions per minute (RPM) the motor will run at with full power under no load. The [`GoFor`](/components/motor/#gofor) method calculates how much power to send to the motor as a percentage of `max_rpm`. If unknown, you can set it to 100, which will mean that giving 40 as the `rpm` argument to `GoFor` or `GoTo` will set it to 40% speed. *For non-encoded fake motors, this is required or a default is assigned.* |
| `ticks_per_rotation` | int | Optional | *Becomes required for calculations if an encoder is configured (unlike on a real motor).* For a stepper motor, the number of steps in one full rotation (200 is common). For an encoded motor, how many encoder ticks in one full rotation. See data sheet (for a real motor). |
| `dir_flip` | bool | Optional | Flips the direction of "forward" versus "backward" rotation. <br> Default: `false` |
| `pins` | object | Optional | A struct that holds pin configuration information. |

Nested within `pins`:

| Name | Type | Inclusion | Description |
| ---- | ---- | --------- | ----------- |
| `a` | string | Optional | See [Pin Information](#pin-information). Corresponds to "IN1" on many driver data sheets. {{< glossary_tooltip term_id="pin-number" text="Pin number" >}} of the GPIO pin this is wired to on the [board](/components/board/). |
| `b` | string | Optional | See [Pin Information](#pin-information). Corresponds to "IN2" on many driver data sheets. {{< glossary_tooltip term_id="pin-number" text="Pin number" >}} of the GPIO pin this is wired to on the [board](/components/board/). |
| `dir` | string | Optional | See [Pin Information](#pin-information). {{< glossary_tooltip term_id="pin-number" text="Pin number" >}} of the GPIO pin this is wired to on the [board](/components/board/). |
|`pwm` | string | Optional | See [Pin Information](#pin-information). {{< glossary_tooltip term_id="pin-number" text="Pin number" >}} of the GPIO pin this is wired to on the [board](/components/board/). |

#### Pin Information

There are three common ways for the computing device to communicate with a brushed DC motor driver chip.
The driver data sheet (for a real, not fake, motor) will specify which one to use.

- PWM/DIR: One digital input (such as a GPIO pin) sends a [pulse width modulation (PWM)](https://en.wikipedia.org/wiki/Pulse-width_modulation) signal to the driver to control speed while another digital input sends a high or low signal to control the direction.
- In1/In2 (or A/B): One digital input is set to high and another set to low turns the motor in one direction and vice versa, while speed is controlled with PWM through one or both pins.
- In1/In2 + PWM: Three pins: an In1 (A) and In2 (B) to control direction and a separate PWM pin to control speed.
