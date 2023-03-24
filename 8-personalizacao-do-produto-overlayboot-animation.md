## 8. Personalização do Produto - Overlay,Boot Animation

### 8.1. Overlay - Modificando Arquivos XML

```bash
# No nosso caso, crie o diretório e edite o arquivo palomakoba_zeus.mk e adicione o código abaixo no final do arquivo:

cd /media/arquivos/aosp/device/palomakoba/onion/
mkdir overlay
gedit palomakoba_onion.mk
```
![image](https://user-images.githubusercontent.com/19675356/227388479-4325422b-08ae-445f-a059-3d13314449eb.png)

```bash
# amos agora criar um arquivo para modificar alguma configuração de um XML existente no AOSP. 
# Um dos arquivos mais comuns de serem personalizados é o arquivo frameworks/base/core/res/res/values/config.xml. Este arquivo possui configurações 
# diversas com o objetivo de serem facilmente personalizadas em diferentes produtos e hardwares através deste recurso de overlay.
```
![image](https://user-images.githubusercontent.com/19675356/227388999-56ac4a45-e853-48d8-bc7d-59cfdd5216bd.png)


```bash
# Olhando o arquivo config.xml mencionado, salve o comentário que descreve a configuração de nome config_supportAutoRotation. 
# Note, em especial, a parte que diz que todas as opções de rotação são removidas das configurações (settings).

#        If true, enables auto-rotation features using the accelerometer.
#        Otherwise, auto-rotation is disabled.  Applications may still request
#        to use specific orientations but the sensor is ignored and sensor-based
#        orientations are not available.  Furthermore, all auto-rotation related
#        settings are omitted from the system UI.  In certain situations we may
#        still use the accelerometer to determine the orientation, such as when
#        docked if the dock is configured to enable the accelerometer.

```

```bash
# Antes de modificar essa opção, vamos observar o comportamento dela. Para isso, inicie o seu emulador, caso não esteja aberto:

cd /media/arquivos/aosp/
source build/envsetup.sh
lunch palomakoba_zeus-eng
emulator &
```
![image](https://user-images.githubusercontent.com/19675356/227389466-57a60059-63d4-460c-bb19-d16e580f87b1.png)

```bash
# Agora, vamos modificar esse comportamento usando o overlay. Para isso, crie o  caminho completo do arquivo de overlay e edite-o:

cd /media/arquivos/aosp/
mkdir -p overlay/frameworks/base/core/res/res/values/
gedit overlay/frameworks/base/core/res/res/values/config.xml
```
![image](https://user-images.githubusercontent.com/19675356/227390143-95b71a50-9fe8-4a07-b24f-1cbfbda05f7e.png)

```bash
# Feche o emulator aberto e, em seguida, compile o AOSP e inicie o emulator novamente:

m -j10
emulator &

# Volte para o Settings → Display, no final da tela, e note que não existe mais a opção "Auto-rotate screen". 
# Clique no botão abaixo e tirae um screenshot do Display Settings
```
![image](https://user-images.githubusercontent.com/19675356/227391765-697f122a-1799-49b5-8f4a-d4ee818b1b7a.png)

```bash
# Observando o arquivo original config.xml, copie e salve o comentário que descreve a configuração de nome config_longPressOnPowerBehavior.

#         Control the behavior when the user long presses the power button.
#           0 - Nothing
#           1 - Global actions menu
#           2 - Power off (with confirmation)
#           3 - Power off (without confirmation)
#           4 - Go to voice assist
#           5 - Go to assistant (Settings.Secure.ASSISTANT)
```

```bash
# Modifique o arquivo de overlay já aberto anteriormente e inclua, após a linha do config_supportAutoRotation, o código abaixo:

<!-- O que acontece ao se pressionar o botão power por um tempo longo -->
<integer name="config_longPressOnPowerBehavior">2</integer>
```
![image](https://user-images.githubusercontent.com/19675356/227392639-6d9199d7-8ed2-4f4c-ad70-0fed90f88c03.png)
![image](https://user-images.githubusercontent.com/19675356/227393460-3797ba6f-d579-4bd9-bce1-f551906987a4.png)

```bash
# Tirar um screenshot do Android mostrando a caixa de diálogo de confirmação.
```
![image](https://user-images.githubusercontent.com/19675356/227393616-14343121-15fc-4049-9ea1-ad4e24bd135b.png)

```bash
# Acesse o arquivo original config.xml, copie e salve o comentário que descreve a 
# configuração de nome config_dialogCornerRadius.

#   <!-- Corner radius of system dialogs -->
```
![image](https://user-images.githubusercontent.com/19675356/227393924-faec4d89-a6d9-4ac8-abb3-6026226b5f5a.png)

```bash
# Modifique seu valor como no código abaixo:
<dimen name="config_dialogCornerRadius">50dp</dimen>
```
![image](https://user-images.githubusercontent.com/19675356/227394055-dde7fa2c-435d-4f6a-bf50-fdf3dd4fbc99.png)

```bash

```

```bash

```

```bash

```

```bash

```

```bash

```

```bash

```

```bash

```

```bash

```

```bash

```

```bash

```

```bash

```

```bash

```

```bash

```
