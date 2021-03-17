# config
config
mixup 0.2 0.5 0.8
multiscalflip [(800, 600),(1000. 750)]
anchor 2    scales=[2],
            ratios=[0.5, 1.0, 2.0, 3.0, 4.0],## weight/height
            strides=[4, 8, 12, 16, 20]),
anchor 4    scales=[4],
            ratios=[0.5, 1.0, 2.0, 3.0, 4.0],## weight/height
            strides=[2, 4, 6, 8, 10]),

albu_train_transforms = [
    dict(type='RandomRotate90', always_apply=False, p=0.5)
	dict(
        type='ShiftScaleRotate',
        shift_limit=0.0625,
        scale_limit=0.0,
        rotate_limit=0,
        interpolation=1,
        p=0.5),
    dict(
        type='RandomBrightnessContrast',
        brightness_limit=[0.1, 0.3],
        contrast_limit=[0.1, 0.3],
        p=0.2),
    dict(
        type='OneOf',
        transforms=[
            dict(
                type='RGBShift',
                r_shift_limit=10,
                g_shift_limit=10,
                b_shift_limit=10,
                p=1.0),
            dict(
                type='HueSaturationValue',
                hue_shift_limit=20,
                sat_shift_limit=30,
                val_shift_limit=20,
                p=1.0)
        ],
        p=0.1),
    dict(
        type='OneOf',
        transforms=[
            dict(type='Blur', blur_limit=3, p=1.0),
            dict(type='MedianBlur', blur_limit=3, p=1.0)
        ],
        p=0.1),
]
