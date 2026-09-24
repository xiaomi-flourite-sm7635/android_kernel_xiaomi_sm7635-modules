# flourite experimental source-module integration

This is an isolated test branch, not a change to the Fairphone checkout or to
the normal flourite ROM/prebuilt selection. No runtime success is implied.

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

Local adaptations:

- Build flourite NT38771/Xiaomi touch modules, with the 6.1 class_create API.
  Use P16U firmware/config names and stock GPIO1/GPIO2 panel selection.
  VOX firmware revision is selected from lockdown bytes 6/7 (72:21 -> 00,
  otherwise 01); do not guess if lockdown cannot be read. The selection was
  checked against flourite stock nt38771_touch.ko, BuildID
  2b63502952fe069abf259456a1abf6d0ad5c5bb0. Source tree paths/register maps
  and the THP daemon ABI still require real-device testing.
- Use flourite display's doubleclick-enable export for the touch gesture flag.
- Allocate the camera message item off-stack; validate message field lengths
  and reject incomplete userspace copies. This addresses a build-time stack
  limit, not a proven diagnosis of the reported camera reboot.
- Build the msm_video frontend only for flourite; both video frontends share
  object paths and must not compile concurrently. Supply iris2 sizing macros.
- Use external IPA/RMNET header paths, and select the P16U BDF filenames in
  ICNSS without inventing project IDs for unrelated Xiaomi devices.
- Include the FTM cfg80211 object selected by CONFIG_QCA_WIFI_FTM_NL80211,
  and include the kernel HWID header for flourite WLAN.
- Scope the Bluetooth power-source ioctl's local variable to its switch case.

All modules must be rebuilt with the matching Xiaomi source kernel, compiler,
configuration, Module.symvers and signing certificate. Do not combine these
modules with the earlier stock-module GKI experiment.
