# BDE Rev2 ZMK Config

## Instructions

1. [Fork this repository](https://docs.github.com/en/get-started/quickstart/fork-a-repo) so you can edit it.
2. Click the [Actions](../Actions) tab on your fork and click the **I understand my workflows, go ahead and run them** button to enable them.
   ![Actions tab with "I understand my workflows" button](https://aws1.discourse-cdn.com/github/original/2X/8/8a28c79db26e3c2d82f2d0694ae0762b2ef7763b.png)
3. Edit the [config/bde_rev2.conf](config/bde_rev2.conf) to enable/disable features. Edit [config/bde_rev2.keymap](config/bde_rev2.keymap) to change the keymap. Lastly, make sure the [build.yml](build.yml) file has your board in the "boards" list.
4. After committing your changes, your firmware will begin compiling. Assuming there are no typos or other problems, it will eventually be [downloadable from the Actions tab](https://zmk.dev/docs/user-setup#installing-the-firmware).
5. [Flash the firmware](https://zmk.dev/docs/user-setup#flashing-uf2-files) that matches the board you're using, e.g. bde_rev2-nice_nano_v2-zmk.uf2 for a nice!nano v2.

## Troubleshooting

Don't forget to [check the ZMK docs](https://zmk.dev/docs/troubleshooting).

### There was an error and the build didn't finish.

**This is probably an error in the keymap.** Look closely at whatever changes you made.

ZMK syntax is very different from QMK syntax. Note that when editing keymaps, each ZMK code is generally preceded by a reference categorizing what that code does.

For example: The letter "A" is categorized as a **k**ey **p**ress; therefore if you want the letter "A"  in your keymap, it must be written `&kp A`.

A few more examples below:

| QMK | ZMK |
| --- | --- |
| `KC_A` | `&kp A` |
| `QK_REBOOT` | `&reset` |
| `LT(1, KC_SPACE)` | `&lt 1 SPACE` |

There are many, many more differences. Don't forget to [check the ZMK docs](https://zmk.dev/docs/features/keymaps).

### The OLED/RGB/encoder(s) don't work.

**Double-check the features in the [config/bde_rev2.conf](config/bde_rev2.conf) file** and make sure the ones you need are enabled. RGB is often turned off.

**The OLED can be a bit finicky** because of [a re-initialization issue](https://github.com/zmkfirmware/zmk/issues/674). Try all of the following:

1. Wait at least one minute and press the physical reset button on the board once.
2. If `CONFIG_ZMK_RGB_UNDERGLOW_EXT_POWER` is set to `y` in [config/bde_rev2.conf](config/bde_rev2.conf), turn on RGB. Then try step 1.
3. Add `&ext_power EP_ON` to your keymap and press the key to *make sure* external power is on. Then try step 2.

### The flash worked, but I'm having inexplicable issues/can't get anything to pair.

**Try flashing the `settings_reset` firmware for your board** to chase off any strange gremlins.
