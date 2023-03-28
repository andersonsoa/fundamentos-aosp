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
![image](https://user-images.githubusercontent.com/19675356/227396886-26848fd9-3579-41ac-b528-fa5681aebc04.png)

```bash
# Tirar um screenshot do Android mostrando a caixa de diálogo de confirmação.
```
![image](https://user-images.githubusercontent.com/19675356/227397080-e99f2bc6-9711-426d-9b6d-120da1a5f666.png)
  
  
### 8.2. Overlay - Modificando o App Settings
```bash
# Acesse o arquivo mencionado, copie e salve a tag de nome build_number.

    <string name="build_number">Build number</string>
    
```

```bash
# Para fazer essa alteração, crie o arquivo de overlay com o conteúdo abaixo:

cd device/palomakoba/onion/
mkdir -p overlay/packages/apps/Settings/res/values/
```
![image](https://user-images.githubusercontent.com/19675356/227397525-83096a58-5312-4156-ba27-f6e2b86626ab.png)
![image](https://user-images.githubusercontent.com/19675356/227397653-fa4733e8-54a5-4763-ad4e-b6631a146e9e.png)
![image](https://user-images.githubusercontent.com/19675356/227399359-13043f6a-7b0a-4cbd-82a5-6cb5963c105d.png)

```bash
# Tire um screenshot do Android mostrando o Settings.
```
![image](https://user-images.githubusercontent.com/19675356/227399645-d8764cb2-4202-4d0a-8a73-6ebcfd217fbc.png)
  
  
### 8.3. Overlay - Modificando o Wallpaper Padrão
```bash
# Vamos substituí-lo usando o overlay. Para isso, execute:
# Feche o emulador, compile o AOSP, inicie o emulador novamente. Note o novo wallpaper. 
# Tire um screenshot do Android mostrando o novo wallpaper.

```
![image](https://user-images.githubusercontent.com/19675356/227403065-5b5fb13d-324c-48d9-9aac-300e00e7f4f2.png)
![image](https://user-images.githubusercontent.com/19675356/227403161-e4ec5818-0544-4789-8b54-77c3d391e3c8.png)
  
  
### 8.4. Modificando a Animação de Boot
```bash
# Liste abaixo os arquivos procurados, na ordem.
```
![image](https://user-images.githubusercontent.com/19675356/228384491-a4234148-b5a8-44ca-a98d-a04e910491c4.png)

```bash
# Copiando arquivo de animation
```
![image](https://user-images.githubusercontent.com/19675356/228385096-cb986828-29d4-4bac-aaa0-d5de7e4a33dd.png)

```bash
# Adicionando comando para copiar o bootanimation durante o build
```
![image](https://user-images.githubusercontent.com/19675356/228385447-65d9585b-97be-492a-a5f1-e8d8e5214197.png)

```bash
# Por fim, feche o seu emulador e compile o novo Android. Inicie o emulador. 
# Imediatamente, clique no botão abaixo para preparar o screenshot. 
```
![image](https://user-images.githubusercontent.com/19675356/228386719-f8aa165a-d872-4a1f-b5d1-40074e971517.png)
![image](https://user-images.githubusercontent.com/19675356/228386872-0101d66e-2b14-421b-9a7c-9741915a0674.png)
  
  
### 8.6. Desafio II - Wallpaper

```text
 - Em uma seção anterior, alteramos o wallpaper padrão substituindo o arquivo default_wallpaper.png usando overlay.
Entretanto, se você for no início da classe WallpaperManager, você verá que existe uma propriedade de sistema 
que permite mudar também esse wallpaper e que possui, inclusive, prioridade sobre o arquivo padrão.

 - Sua missão é alterar novamente o wallpaper do Android para ser o arquivo disponível em ~/default_wallpaper2.png 
 ou algum outro de sua escolha. Mas, desta vez, você deve fazer isso usando as propriedades do sistema, ao invés 
 de overlays. Após obter sucesso em sua missão, envie o código relevante do seu palomakoba_zues.mk na tarefa 
 especificada no módulo da disciplina.
```

```bash

```

```bash

```

```bash

```
