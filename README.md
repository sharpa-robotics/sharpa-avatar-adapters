# Sharpa Avatar Adapters

Mechanical adapters and coordinate transforms for the Sharpa Avatar AE01. This repository contains 10 STEP models and five right-hand transforms.

## Repository Structure
```text
README.md
LICENSE
models/
└── AE01/
    ├── vive_tracker/
    ├── pico_controller/
    └── meta_touch_plus_and_pro/
```

| Trackers | Model folder | Files |
| --- | --- | --- |
| VIVE&nbsp;Tracker<br>VIVE&nbsp;Ultimate&nbsp;Tracker | [vive_tracker](models/AE01/vive_tracker/) | `vive_tracker_adapter_AE01.step` |
| PICO&nbsp;controller | [pico_controller](models/AE01/pico_controller/) | `pico_adapter_AE01_left.step`<br>`pico_adapter_AE01_right.step`<br>`pico_cover_AE01_left.step`<br>`pico_cover_AE01_right.step` |
| Meta&nbsp;Quest&nbsp;Touch&nbsp;Plus<br>Meta&nbsp;Quest&nbsp;Touch&nbsp;Pro | [meta_touch_plus_and_pro](models/AE01/meta_touch_plus_and_pro/) | `meta_touch_plus_and_pro_adapter_AE01_left.step`<br>`meta_touch_plus_and_pro_adapter_AE01_right.step`<br>`meta_touch_plus_and_pro_switch_AE01.step`<br>`meta_touch_plus_and_pro_switch_stop_AE01.step`<br>`meta_touch_plus_fixture.step` |


## Coordinate transforms

All five matrices below are **right-hand** transforms named `T_mount_tracker`. They map tracker/controller coordinates into `right_hand_mount_frame` using homogeneous column vectors:

```text
p_mount = T_mount_tracker @ p_tracker

T_mount_tracker = [ R  t ]
                  [ 0  1 ]

T_world_mount = T_world_tracker @ inverse(T_mount_tracker)
```

Each column of `R` is a positive tracker basis axis expressed in mount coordinates. The source drawing places the mount origin at the midpoint of an edge on the interface bottom face, with axes parallel to `right_hand_virtual_base_frame`. A newer manual marks an upper-edge midpoint; the hardware revision correspondence is unresolved.

**Translation unit: mm.** The VIVE derivation explicitly uses millimetres; the other translations are interpreted as millimetres from the same source table and CAD units, pending confirmation. For metre-based calculations, divide only the first three entries of the last column by 1000. Leave the rotation and bottom row unchanged, and use the same length unit for points and poses.

The source values and rounded rotations are preserved below. Use a matrix inverse when reversing the transform. For example, the VIVE Tracker origin maps to `[-10.5, 0, 17.5]` mm, or `[-0.0105, 0, 0.0175]` m, in the mount frame.

These matrices are unvalidated and are not bound to a verified CAD revision. The runtime pose reference is unconfirmed: reconcile tracking, grip or aim frames before use. No left-hand transforms are supplied; do not infer them by mirroring the right-hand matrices. World-to-robot registration is outside the supplied transforms.

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

### Meta Quest 3 / Touch Plus

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
