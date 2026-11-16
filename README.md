# Sharpa Avatar Adapters

Mechanical adapters and coordinate transforms for the Sharpa Avatar AE01. This repository contains 14 STEP models and five right-hand transforms.

## Repository Structure
```text
README.md
LICENSE
models/
└── AE01/
    ├── vive_tracker/
    ├── pico_controller/
    ├── meta_touch_plus/
    └── meta_touch_pro/
```

| Adapter | Parts | Hand | Model folder | Files |
| --- | --- | --- | --- | --- |
| VIVE Tracker / VIVE Ultimate Tracker | Tracker adapter | Shared | [vive_tracker](models/AE01/vive_tracker/) | `AE01_vive_tracker_adapter.step` |
| PICO controller | Main-hand adapters, robot-arm adapters and covers | Left / right | [pico_controller](models/AE01/pico_controller/) | `AE01_pico_cover_left.step`<br>`AE01_pico_cover_right.step`<br>`AE01_pico_main_hand_adapter_left.step`<br>`AE01_pico_main_hand_adapter_right.step`<br>`AE01_pico_robot_arm_adapter_left.step`<br>`AE01_pico_robot_arm_adapter_right.step` |
| Meta Quest 3 / Touch Plus | Quest 3 fixture | Unspecified | [meta_touch_plus](models/AE01/meta_touch_plus/) | `AE01_quest_3_fixture.step` |
| Meta Quest Touch Pro | Main-hand adapters, robot-arm adapters, switch and switch stop | Left / right; switch unspecified | [meta_touch_pro](models/AE01/meta_touch_pro/) | `AE01_touch_pro_main_hand_adapter_left.step`<br>`AE01_touch_pro_main_hand_adapter_right.step`<br>`AE01_touch_pro_robot_arm_adapter_left.step`<br>`AE01_touch_pro_robot_arm_adapter_right.step`<br>`AE01_touch_pro_switch_stop_right.step`<br>`AE01_touch_pro_switch.step` |

VIVE Tracker 3.0 and VIVE Ultimate Tracker share the VIVE adapter according to the source document, but use different transforms. The Ultimate assembly also uses its mounting base, which is not keyed against reversed insertion; confirm its installation orientation.

The exact PICO controller generation is unspecified. The Quest 3 / Touch Plus model is a fixture only; its handedness and complete assembly are unresolved. Touch Plus and Touch Pro parts are not established as interchangeable.

Physical fit, retention and calibration have not been verified. Confirm the AE01 interface revision, model, hand and assembly orientation before use. Left-hand model availability does not provide a left-hand calibration.

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

Matrix source: the project multi-tracker coordinate table, revision 390, retrieved on 2026-11-10.

## License and support

See [LICENSE](LICENSE) for the current license status, which remains pending owner review.

Hardware and integration support: [support@sharpa.com](mailto:support@sharpa.com).
