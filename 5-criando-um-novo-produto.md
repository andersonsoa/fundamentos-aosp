# Prática no Laboratório - Fundamentos do AOSP
## 5. Criando um Novo Produto

### 5.1. Convenções de Nomes e Diterórios

```bash
cd device
ls
```
![image](https://user-images.githubusercontent.com/19675356/225475386-6f3d9584-dde0-4d78-a953-419dd0ad7c53.png)


```bash
cd google
ls
```
![image](https://user-images.githubusercontent.com/19675356/225475598-9d93311d-57d8-4708-8d2f-9a5454a7b400.png)

<br />
<br />

### 5.2. Analisando o Produto do Emulador

```bash
gedit /build/target/product/sdk_phone_x86_64.mk
```
![image](https://user-images.githubusercontent.com/19675356/225476331-5829abbb-a4e9-4b39-84b5-59b291556a38.png)


```bash
# Salve a declaração completa das variáveis mencionadas.
```
![image](https://user-images.githubusercontent.com/19675356/225476749-e8b20ca8-b7a2-4ff5-a712-77d3118d56d2.png)


```bash
gedit build/target/board/emulator_x86_64/BoardConfig.mk
```
![image](https://user-images.githubusercontent.com/19675356/225476884-6e2709ba-a8f7-4a4a-b1bc-d06d87f534dc.png)


```bash
# Salve a declaração completa das variáveis mencionadas.
```
![image](https://user-images.githubusercontent.com/19675356/225476979-96f74ac6-3436-4e13-998b-31bd5754e85a.png)

<br />
<br />

### 5.3. Criando e Compilando um Novo Produto

```bash
mkdir -p device/palomakoba/onion
cd device/palomakoba/onion
```
![image](https://user-images.githubusercontent.com/19675356/225477447-55f94fbc-065b-45b2-9d3e-6cb2ac96ffd1.png)

```bash
gedit AndroidProducts.mk
```
![image](https://user-images.githubusercontent.com/19675356/225478172-1599aa1f-4f79-46f3-8900-954edd888773.png)

```bash
gedit palomakoba_onion.mk
```
![image](https://user-images.githubusercontent.com/19675356/225478422-08e19248-1cc2-420b-b3d9-49a69d01ab0c.png)

```bash
gedit BoardConfig.mk
```
![image](https://user-images.githubusercontent.com/19675356/225478862-75ee26a6-0474-4525-9325-2b76f14f5f60.png)

```bash
lunch
```
![image](https://user-images.githubusercontent.com/19675356/225478996-f401221a-d723-47b8-a045-48246ad80e9f.png)

```bash
lunch palomakoba_onion-eng
```
![image](https://user-images.githubusercontent.com/19675356/225479094-2990e33b-2660-4784-bdd9-89961863d187.png)

```bash
m -j8
```
![image](https://user-images.githubusercontent.com/19675356/225773414-c90cae84-29c1-4412-bb83-f0fee1587027.png)

<br />
<br />

### 5.4. Executando o Novo Produto Criado

```bash
emulator &
```
![image](https://user-images.githubusercontent.com/19675356/225774304-7fae8a6b-4d76-4ab1-bc1f-44ee9a4e0416.png)

<br />
<br />

### 5.5. Investigando as Configurações do Emulador

```bash
gedit build/target/product/sdk_phone_x86_64.mk
```

> Relatório de arquivos do "palomakoba_onion.mk"
```bash

$(call inherit-product, $(SRC_TARGET_DIR)/product/core_64_bit.mk)
    # FIM
$(call inherit-product, $(SRC_TARGET_DIR)/product/generic_system.mk)
    $(call inherit-product, $(SRC_TARGET_DIR)/product/handheld_system.mk)
        $(call inherit-product, $(SRC_TARGET_DIR)/product/media_system.mk)
            $(call inherit-product, $(SRC_TARGET_DIR)/product/base_system.mk)
                $(call inherit-product, $(SRC_TARGET_DIR)/product/runtime_libart.mk)
                    $(call inherit-product, $(SRC_TARGET_DIR)/product/default_art_config.mk)
                        # FIM 
            $(call inherit-product, $(SRC_TARGET_DIR)/product/cfi-common.mk)
                #FIM
            $(call inherit-product-if-exists, vendor/google/products/cfi-vendor.mk) # NÂO EXISTE
        $(call inherit-product-if-exists, frameworks/base/data/fonts/fonts.mk) # carrega fontes (tipografia)
            # FIM
        $(call inherit-product-if-exists, external/google-fonts/dancing-script/fonts.mk)
            # FIM
        $(call inherit-product-if-exists, external/google-fonts/carrois-gothic-sc/fonts.mk)
            # FIM
        $(call inherit-product-if-exists, external/google-fonts/coming-soon/fonts.mk)
            # FIM
        $(call inherit-product-if-exists, external/google-fonts/cutive-mono/fonts.mk)
            # FIM
        $(call inherit-product-if-exists, external/google-fonts/source-sans-pro/fonts.mk)
            # FIM
        $(call inherit-product-if-exists, external/noto-fonts/fonts.mk)
            # FIM
        $(call inherit-product-if-exists, external/roboto-fonts/fonts.mk)
            # FIM
        $(call inherit-product-if-exists, external/hyphenation-patterns/patterns.mk)
            # FIM
        $(call inherit-product-if-exists, frameworks/base/data/keyboards/keyboards.mk)
            # FIM
        $(call inherit-product-if-exists, frameworks/webview/chromium/chromium.mk) # NÃO EXISTE
    $(call inherit-product, $(SRC_TARGET_DIR)/product/telephony_system.mk)
        # FIM
    $(call inherit-product, $(SRC_TARGET_DIR)/product/languages_default.mk)
        # FIM
    $(call inherit-product-if-exists, vendor/google/security/adb/vendor_key.mk) # NÃO EXISTE
    $(call inherit-product, $(SRC_TARGET_DIR)/product/updatable_apex.mk)
        # FIM
$(call inherit-product, $(SRC_TARGET_DIR)/product/handheld_system_ext.mk)
    $(call inherit-product, $(SRC_TARGET_DIR)/product/media_system_ext.mk)
        $(call inherit-product, $(SRC_TARGET_DIR)/product/base_system_ext.mk)
            # FIM
$(call inherit-product, $(SRC_TARGET_DIR)/product/telephony_system_ext.mk)
    # FIM
$(call inherit-product, $(SRC_TARGET_DIR)/product/aosp_product.mk)
    $(call inherit-product, $(SRC_TARGET_DIR)/product/handheld_product.mk)
        $(call inherit-product, $(SRC_TARGET_DIR)/product/media_product.mk)
            $(call inherit-product, $(SRC_TARGET_DIR)/product/base_product.mk)
                # FIM
    $(call inherit-product, $(SRC_TARGET_DIR)/product/telephony_product.mk)
        # FIM
    $(call inherit-product-if-exists, frameworks/base/data/sounds/AllAudio.mk)
        # FIM
$(call inherit-product-if-exists, device/generic/goldfish/x86_64-vendor.mk)
    # FIM
$(call inherit-product, $(SRC_TARGET_DIR)/product/emulator_vendor.mk)
    $(call inherit-product, $(SRC_TARGET_DIR)/product/handheld_vendor.mk)
        $(call inherit-product, $(SRC_TARGET_DIR)/product/media_vendor.mk)
            $(call inherit-product, $(SRC_TARGET_DIR)/product/base_vendor.mk)
                # FIM
    $(call inherit-product, $(SRC_TARGET_DIR)/product/telephony_vendor.mk)
        # FIM
    $(call inherit-product-if-exists, device/generic/goldfish/vendor.mk)
        $(call inherit-product-if-exists, frameworks/native/build/phone-xhdpi-2048-dalvik-heap.mk)
            # FIM
        $(call inherit-product, $(SRC_TARGET_DIR)/product/emulated_storage.mk)
            # FIM
$(call inherit-product, $(SRC_TARGET_DIR)/board/emulator_x86_64/device.mk)
    # FIM
$(call inherit-product-if-exists, sdk/build/product_sdk.mk)
    # FIM
$(call inherit-product-if-exists, development/build/product_sdk.mk)
    # FIM
```
  
  
```bash
# gedit build/target/product/handheld_system.mk

PRODUCT_PACKAGES += \
    BasicDreams \
    BlockedNumberProvider \
    Bluetooth \
    BluetoothMidiService \
    BookmarkProvider \
    BuiltInPrintService \
    CalendarProvider \
    cameraserver \
    CameraExtensionsProxy \
    CaptivePortalLogin \
    CertInstaller \
    clatd \
    DocumentsUI \
    DownloadProviderUi \
    EasterEgg \
    ExternalStorageProvider \
    FusedLocation \
    InputDevices \
    KeyChain \
    librs_jni \
    ManagedProvisioning \
    MmsService \
    MtpService \
    MusicFX \
    NfcNci \
    PacProcessor \
    PrintRecommendationService \
    PrintSpooler \
    ProxyHandler \
    screenrecord \
    SecureElement \
    SharedStorageBackup \
    SimAppDialog \
    Telecom \
    TelephonyProvider \
    TeleService \
    Traceur \
    UserDictionaryProvider \
    VpnDialogs \
    vr \
```

```bash
# gedit frameworks/base/data/sounds/AllAudio.mk

PRODUCT_COPY_FILES += \
    $(LOCAL_PATH)/Alarm_Beep_01.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Alarm_Beep_01.ogg \
    $(LOCAL_PATH)/Alarm_Beep_02.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Alarm_Beep_02.ogg \
    $(LOCAL_PATH)/Alarm_Beep_03.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Alarm_Beep_03.ogg \
    $(LOCAL_PATH)/Alarm_Buzzer.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Alarm_Buzzer.ogg \
    $(LOCAL_PATH)/Alarm_Classic.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Alarm_Classic.ogg \
    $(LOCAL_PATH)/Alarm_Rooster_02.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Alarm_Rooster_02.ogg \
    $(LOCAL_PATH)/alarms/ogg/Argon.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Argon.ogg \
    $(LOCAL_PATH)/alarms/ogg/Barium.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Barium.ogg \
    $(LOCAL_PATH)/alarms/ogg/Carbon.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Carbon.ogg \
    $(LOCAL_PATH)/alarms/ogg/Cesium.ogg:$(TARGET_COPY_OUT_PRODUCT)/media/audio/alarms/Cesium.ogg \
    ...

```

```bash
mplayer frameworks/base/data/sounds/Alarm_Rooster_02.ogg
```
![image](https://user-images.githubusercontent.com/19675356/225784237-3f40a124-d8fc-42b5-8abd-30b0d8c48570.png)

```bash
# gedit build/make/target/product/aosp_product.mk

PRODUCT_PRODUCT_PROPERTIES += \
    ro.config.ringtone?=Ring_Synth_04.ogg \
    ro.config.notification_sound?=pixiedust.ogg \
    ro.com.android.dataroaming?=true \
```
