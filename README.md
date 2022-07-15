# BDE Rev2 ZMK Config

## Instructions

1. [Fork this repository](https://docs.github.com/en/get-started/quickstart/fork-a-repo) so you can edit it.
2. Navigate to the **Actions** tab and click the "I understand my workflows, go ahead and run them" button to enable builds.
   ![Actions tab with "I understand my workflows" button](https://aws1.discourse-cdn.com/github/original/2X/8/8a28c79db26e3c2d82f2d0694ae0762b2ef7763b.png)
3. Edit the [config/bde_rev2.conf](config/bde_rev2.conf) to enable/disable features. Edit [config/bde_rev2.keymap](config/bde_rev2.keymap) to change the keymap. Lastly, make sure the [build.yaml](build.yaml) file has your board in the "boards" list.
4. After committing your changes, your firmware will begin compiling. Assuming there are no typos or other problems, it will eventually be [downloadable from the Actions tab](https://zmk.dev/docs/user-setup#installing-the-firmware).
5. [Flash the firmware](https://zmk.dev/docs/user-setup#flashing-uf2-files) that matches the board you're using, e.g. `bde_rev2-nice_nano_v2-zmk.uf2` for a nice!nano v2.

## Quick Questions

### There was an error and the build didn't finish.

#### There is probably an error in your keymap.

Carefully double-check the last changes you made. ZMK syntax is very different from QMK syntax. Note that when editing keymaps, each ZMK code is generally preceded by a reference categorizing what that code does.

For example: the letter "Z" is categorized as a **k**ey **p**ress. To add the letter "Z" to a keymap, it must be written `&kp Z`.

A few more examples below:

| QMK | ZMK |
| --- | --- |
| `KC_A` | `&kp A` |
| `QK_REBOOT` | `&reset` |
| `LT(1, KC_SPACE)` | `&lt 1 SPACE` |

There are many, many more differences. Don't forget to [check the ZMK docs](https://zmk.dev/docs/features/keymaps).

### The OLED/RGB/encoder(s) don't work.

#### Double-check the features in the [config/bde_rev2.conf](config/bde_rev2.conf) file.

And double-check the Kconfig file in the build results to make sure what you've enabled is really enabled. As of mid-July 2022, [there are also some issues regarding default board/shield configurations taking precedence over user configurations](https://github.com/zmkfirmware/zmk/issues/1382).

#### The OLED can be a bit finicky.
- As of mid-July 2022, [there is a known issue with OLEDs not being re-initialized after power off](https://github.com/zmkfirmware/zmk/issues/674).
- If using a nice!nano v2 without a battery, the RAW pin does not always deliver consistent voltage.

Try the following:

1. Wait at least one minute and press the physical reset button on the board once.

### The flash worked, but I'm having inexplicable issues/can't get anything to pair.

#### Try flashing the `settings_reset` firmware for your board.

## Further Troubleshooting Resources

- [ZMK's troubleshooting page](https://zmk.dev/docs/troubleshooting)
- Stop by #keyboard-help in [MechWild's Discord](https://discord.gg/nfxHnsm)
- Ask the ZMK experts in [ZMK's Discord](https://zmk.dev/community/discord/invite)
