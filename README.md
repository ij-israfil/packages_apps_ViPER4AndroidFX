## ViPER4Android FX

Integrate V4A by completing these three steps:

1.  **Build System:** Add the config to **`device.mk`**:

    ```makefile
    $(call inherit-product, packages/apps/ViPER4AndroidFX/config.mk)
    ```

2.  **Audio Effects:** Add these lines to the `<libraries>` block in **`audio_effects.xml`** (`/vendor/etc/` or `/etc/`):

    ```xml
    <library name="v4a_fx" path="libv4a_fx.so"/>
    <effect name="v4a_standard_fx" library="v4a_fx" uuid="41d3c987-e6cf-11e3-a88a-11aba5d5c51b"/>
    ```

3.  **SELinux Policy:** Add these rules to your **`audioserver.te`** file:

    ```te
    get_prop(audioserver, vendor_audio_prop) # If Google or MTK device skip line

    allow audioserver unlabeled:file { read write open getattr };
    allow hal_audio_default hal_audio_default:process { execmem };
    ```
