# Flourite module sources

Base: LineageOS/android_kernel_fairphone_sm7635-modules,
`3adc0650fc8809a097915b89e9590dd9f39a7796`.

Replaced components (complete public source drops, not stock `.ko` files):

| Directory under qcom/opensource | Public repository | Revision |
| --- | --- | --- |
| audio-kernel | MiCode/vendor_qcom_opensource_audio-kernel | 26d5a555078f5dd2053d1d91c580f8d01fd4b00f |
| camera-kernel | MiCode/vendor_qcom_opensource_camera-kernel | 017ae73901de3d6f6cc067cccb5e600a9a71fb9f |
| display-drivers | MiCode/vendor_opensource_display-drivers | f60c37c2d736602a85dcaa84b2ad48918c157133 |
| wlan | MiCode/vendor_qcom_opensource_wlan | a4da9e3b43864da13bc978b8cb6385ba5332a4af |
| touch-drivers | PixelOS-Devices/android_kernel_xiaomi_sm8735-modules, qcom/opensource/touch-drivers | 67985a8d55273472b5f739fd1dfc0e7eb4d58f6f |

MiCode inputs use `flourite-v-oss`. The touch input is a porting reference,
not an official flourite release. Original license/copyright notices are
retained; availability on a public repository is not a new license grant.

All modules must be rebuilt with the matching Xiaomi source kernel, compiler,
configuration, Module.symvers and signing certificate. Do not combine these
modules with the earlier stock-module GKI experiment.
