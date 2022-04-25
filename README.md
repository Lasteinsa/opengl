# OpenGL
Source : 
<br>
<a href="https://android.googlesource.com/platform/frameworks/native/+/master/opengl/">Android Source</a>
<br>
<a href="https://review.lineageos.org/c/LineageOS/android_frameworks_native/+/325520">LineageOS Gerrit (Framework Native</a>
<br>
<a href="https://review.lineageos.org/c/LineageOS/android_vendor_lineage/+/327290">LineageOS Gerrit (Vendor)</a>

<hr width="90%">

This is opengl patched which caused random camera crashes on sony tama devices. <br>
<small>Thanks to <a href="https://github.com/dtrunk90">dtrunk90</a> for patching</small>

## Vendor Patch
Soong: Add TARGET_USES_EGL_DISPLAY_ARRAY conditional. This soong variable is used to conditionally
### build/soong/Android.bp
```
soong_config_module_type {
    name: "egl_display_array",
    module_type: "cc_defaults",
    config_namespace: "lineageGlobalVars",
    bool_variables: ["uses_egl_display_array"],
    properties: ["cflags"],
}

egl_display_array {
    name: "egl_display_array_defaults",
    soong_config_variables: {
        uses_egl_display_array: {
            cflags: ["-DEGL_DISPLAY_ARRAY"],
        },
    },
}
```
### config/BoardConfigSoong.mk 

```
    uses_camera_parameter_lib \
    uses_egl_display_array
```
```
SOONG_CONFIG_lineageGlobalVars_uses_egl_display_array := $(TARGET_USES_EGL_DISPLAY_ARRAY)
```
