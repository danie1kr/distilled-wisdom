# Issue

My devices features absurdly long audio device names like `Tiger Lake-LP Smart Sound Technology Audio Controller HDMI / DisplayPort 1 Output` which are truncated in every audio output selector I use. So it is impossible to directly switch to the desired audio output.

# Solution

Using wireplumber, it is as easy as creating a file in .config/wireplumber/wireplumber.conf.d/device-rename.conf with the following content:
```
monitor.alsa.rules = [
   {
    matches = [
      {
        node.name = "-your-alsa-device-name-"
      }
    ]
    actions = {
      update-props = {
        node.nick              = "-your-favored-short-name-in-the-ui-"
        node.description       = "-your-favored-short-name-in-the-ui-"
      }
    }
  }
  { another ruleset if you fancy ... }
]
```

and then restart the services via  `ystemctl restart wireplumber --user`

# More info

For more info, check [here](https://bbs.archlinux.org/viewtopic.php?id=297803) and [here](https://wiki.archlinux.org/title/WirePlumber).