# Sharpa Avatar Adapters

Mechanical adapters and coordinate transforms for the Sharpa Avatar AE01. This repository contains 10 STEP models and five right-hand transforms.

## Repository Structure
```text
README.md
LICENSE
assembly_photos/
models/
└── AE01/
    ├── vive_tracker/
    ├── pico_controller/
    └── meta_touch_plus_and_pro/
```

| Trackers | Model folder | Files | Assembly instructions |
| --- | --- | --- | --- |
| VIVE&nbsp;Tracker<br>VIVE&nbsp;Ultimate&nbsp;Tracker | [vive_tracker](models/AE01/vive_tracker/) | `vive_tracker_adapter_AE01.step` | Photos pending |
| PICO&nbsp;controller | [pico_controller](models/AE01/pico_controller/) | `pico_adapter_AE01_left.step`<br>`pico_adapter_AE01_right.step`<br>`pico_cover_AE01_left.step`<br>`pico_cover_AE01_right.step` | Photos pending |
| Meta&nbsp;Quest&nbsp;Touch&nbsp;Plus<br>Meta&nbsp;Quest&nbsp;Touch&nbsp;Pro | [meta_touch_plus_and_pro](models/AE01/meta_touch_plus_and_pro/) | `meta_touch_plus_and_pro_adapter_AE01_left.step`<br>`meta_touch_plus_and_pro_adapter_AE01_right.step`<br>`meta_touch_plus_and_pro_switch_AE01.step`<br>`meta_touch_plus_and_pro_switch_stop_AE01.step`<br>`meta_touch_plus_fixture.step` | Photos pending |

Assembly photos are stored in [assembly_photos/](assembly_photos/) and will be displayed in the table above.


## Coordinate transforms

All five matrices below are **right-hand** transforms named `T_mount_tracker`. They map tracker/controller coordinates into `right_hand_mount_frame` using homogeneous column vectors:
```t
p_mount = T_mount_tracker @ p_tracker

T_mount_tracker = [ R  t ]
                  [ 0  1 ]

T_world_mount = T_world_tracker @ inverse(T_mount_tracker)
```

Each column of `R` is a positive tracker basis axis expressed in mount coordinates. Translation unit is mm.

### VIVE Tracker 3.0

```text
[ 0  -1  0  -10.5 ]
[ 1   0  0    0   ]
[ 0   0  1   17.5 ]
[ 0   0  0    1   ]
```

### VIVE Ultimate Tracker

```text
[ -1   0  0  -20.6 ]
[  0  -1  0    0   ]
[  0   0  1  -19.1 ]
[  0   0  0    1   ]
```

### PICO controller

```text
[ -0.99871     0.050223   0.0069817   -8.0421 ]
[  0.0037749   0.21095   -0.97749    15.278  ]
[ -0.050566   -0.97621   -0.21087   -59.188  ]
[  0          0          0           1      ]
```

### Meta Touch Plus

```text
[ -0.98798   -0.085132   0.12907   -24.981 ]
[ -0.1244    -0.05803   -0.99053    46.203 ]
[  0.091816  -0.99468    0.046742  -38.765 ]
[  0         0          0           1     ]
```

### Meta Quest Touch Pro

```text
[ -0.99205   -0.069042   0.10526   -23.086 ]
[ -0.098608  -0.093511  -0.99072    48.502 ]
[  0.078244  -0.99322    0.085959  -37.87  ]
[  0         0          0           1     ]
```

## License and support

See [LICENSE](LICENSE) for the current license status, which remains pending owner review.

Hardware and integration support: [support@sharpa.com](mailto:support@sharpa.com).
