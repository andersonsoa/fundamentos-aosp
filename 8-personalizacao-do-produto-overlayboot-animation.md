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
