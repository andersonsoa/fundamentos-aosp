## 9. Novos Módulos e Programas

### 9.1. Adicionando um Módulo Existente no Android

```bash
# Nesta seção, usaremos essa variável para instalar um novo módulo (já existente no AOSP) em nosso produto Palomakoba Zeus! 
# Tal módulo é o app UniversalMediaPlayer.

# Para isso, precisamos mudar a configuração do nosso produto para incluir o pacote criado:

cd devices/palomakoba/onion
gedit palomakoba_onion.mk

# Para testar, feche o seu emulador atual, recompile o AOSP e execute o emulador novamente:

m
emulator &
```
![image](https://user-images.githubusercontent.com/19675356/228690594-9b1c06ab-dc4f-4009-82cb-9bd738a9498d.png)
![image](https://user-images.githubusercontent.com/19675356/228692854-e58246fa-89cd-4804-ba1b-66e9d7ad1633.png)


```bash
# Abra a lista de aplicativos e observe no meio da lista um ícone novo chamado "Personal Universal Media Player"
# Abra o novo app e tire um screenshot.
```
![image](https://user-images.githubusercontent.com/19675356/228693473-b57cdd89-5f26-46b6-93a5-615b34191a0f.png)

  
Copie a tag android_app do Android.bp e salve seu conteúdo.  
```bp
android_app {
    name: "UniversalMediaPlayer",
    min_sdk_version: "24", // TODO(b/123716038) Sync min SDK version with build.gradle
    sdk_version: "28",
    srcs: [
        "gen/**/*.java", // TODO(b/123702784) Remove gen/ (either generate or remove dependencies)
        "java/**/*.java"
    ],
    static_libs: [
        "androidx-constraintlayout_constraintlayout",
        "androidx.media2_media2-widget",
        "androidx.media2_media2-player",
        "com.google.android.material_material"
    ],
    optimize: {
        // TODO(b/123703963) Re-enable. Currently disabled due to issues with media2-exoplayer
        enabled: false
    }
}
```

### 9.2. Criando um Programa Nativo em C

```bash
# Para isso, entraremos no diretório do nosso produto, criaremos um novo diretório para armazenar o novo programa e, 
# por fim, criaremos o código fonte do programa:

cd device/palomakoba/onion/
mkdir HelloC
cd HelloC
gedit hello_c.c
```
```c
#include <stdio.h>
#include <log/log.h>

int main() {
  printf("Hello World in C!\n");
  ALOG(LOG_INFO, "Palomakoba", "Hello World inC (LogCat)!");
  return 0;
}
```
![image](https://user-images.githubusercontent.com/19675356/228694372-e7602308-a678-44dc-a000-c8197ae15216.png)


```bash
# Para fazer isso, precisamos indicar para o sistema de compilação que este diretório contém um módulo. 
# Conforme mencionado anteriormente, isso é feito através do arquivo Android.bp:

gedit Android.bp
```
```bp
cc_binary {
  name: "hello_c",
  srcs: ["hello_c.c"],
  shared_libs: ["liblog"],
  vendor: true,
}
```
![image](https://user-images.githubusercontent.com/19675356/228694700-d2cc233b-5b93-4380-ab57-2011b7234950.png)

```bash
# Por fim, precisamos mudar a configuração do nosso produto para incluir o pacote criado:

cd ..
gedit palomakoba_onion.mk
```
![image](https://user-images.githubusercontent.com/19675356/228694796-d1594c8d-c288-43dd-b80d-863e2b6ecc17.png)


```bash
# Agora é só fechar o emulador, compilar o AOSP, executar o emulador novamente e entrar no adb shell para testar.

m 
emulator &
adb shell
```
![image](https://user-images.githubusercontent.com/19675356/228697386-41ce2c22-6097-4648-be58-b132e190313a.png)


```bash
# Verifique se o arquivo executável foi realmente copiado para a partição /vendor:

ls -lh /vendor/bin/hello_c
```
![image](https://user-images.githubusercontent.com/19675356/228697564-05a6397d-a5d4-408a-b97d-caaed469a5b4.png)


```bash
# Execute-o:

hello_c
```
![image](https://user-images.githubusercontent.com/19675356/228697659-b27ee414-3981-4abe-8b16-1c2d4a675dbc.png)


```bash
# Verifique se a saída foi para o LogCat também:

logcat -d | grep "Hello World"
```
![image](https://user-images.githubusercontent.com/19675356/228697805-2cd9c435-6e43-409a-8529-beafb8441b7c.png)

  
### 9.3. Incluindo um Módulo do GitHub/LineageOS


```bash
# A seguir, nós iremos baixar e instalar o nano, disponível no GitHub do LineageOS (github.com/LineageOS).
# Entretanto, o nano precisa de uma biblioteca chamada libncurses, que também está no GitHub do LineageOS, 
# disponível aqui. Iremos baixar essa biblioteca primeiro. Para isso, execute o comando abaixo:

cd /media/arquivos/aosp/device/palomakoba/zeus/
mkdir external
cd external # Cria um diretório para os módulos externos e entra nele

# Clona o repositório android_external_libncurses, disponível no LineageOS (branch lineage-19.0),
# e coloca o conteúdo dentro do diretório libncurses (output)

git clone https://github.com/LineageOS/android_external_libncurses.git -b lineage-19.0 libncurses
```
![image](https://user-images.githubusercontent.com/19675356/228698230-fc8f0d94-5cda-484d-b8c0-10d16c4bc404.png)


```bash
# Liste todas as variáveis declaradas no Android.mk do libncurses. Diga apenas o nome, sem repetição, 
# na mesma ordem que foram declarados.

LOCAL_PATH
LOCAL_SRC_FILES
LOCAL_CFLAGS
LOCAL_C_INCLUDES
LOCAL_MODULE_TAGS
LOCAL_MODULE
LOCAL_SYSTEM_EXT_MODULE
TERMINFO_FILES
TERMINFO_SOURCE
TERMINFO_TARGET
ALL_DEFAULT_INSTALLED_MODULES


include $(BUILD_SHARED_LIBRARY)
```


```bash
# Como nesse curso nós estamos usando mais a partição vendor e o módulo libncurses está configurado para a 
# partição product, vamos modificar o arquivo acima para trocar a variável LOCAL_PRODUCT_MODULE 
# por LOCAL_VENDOR_MODULE:

```
![image](https://user-images.githubusercontent.com/19675356/228698857-b2b74131-4434-4a37-b897-f62af0f5fa99.png)


```bash
# Pronto! A libncurses está instalada. Vamos agora baixar e configurar o nano da mesma forma:

git clone https://github.com/LineageOS/android_external_nano.git -b lineage-18.1 nano
```
![image](https://user-images.githubusercontent.com/19675356/228699020-9090d142-5d33-44af-b921-461eb15adbd6.png)


```bash
# Note que existem três modificações no código abaixo (Linhas 3, 7, 8 e 9).

gedit nano/Android.mk
```
![image](https://user-images.githubusercontent.com/19675356/228699446-2bfecf70-8248-4860-ab5b-a2f50a12c43a.png)


```bash
# Existe ainda uma última modificação que precisa ser feita. Se você observar no arquivo de configuração do nano, 
# ele depende também do módulo libssh (variável LOCAL_SHARED_LIBRARIES). Esse módulo já existe no AOSP, mas não 
# está configurado para a partição vendor. Vamos resolver isso:

gedit /media/aosp/external/openssh/Android.bp
```
![image](https://user-images.githubusercontent.com/19675356/228699657-8ea5e167-b34c-4747-97a5-11cc986fdba3.png)


```bash
# Finalmente, vamos adicionar o módulo nano à configuração do nosso produto! Não é necessário adicionar o 
# módulo libncurses, pois ele será adicionado automaticamente pela dependência do nano.

cd ..
gedit palomakoba_onion.mk
```
![image](https://user-images.githubusercontent.com/19675356/228699871-4507c3b1-02a4-466f-8bc5-060f5011db66.png)


```bash
# Feche o emulador caso esteja aberto, compile o Android e inicie o emulador:

m
emulator &
adb shell
```
![image](https://user-images.githubusercontent.com/19675356/228700986-531472e7-764b-483b-b4fa-2f7b4e76f415.png)
![image](https://user-images.githubusercontent.com/19675356/228701041-1ead54d3-bfbc-4521-bff2-321a7b7cd4a1.png)

```bash
# Vamos verificar se os arquivos estão presentes:

ls -lh /vendor/lib64/libncurses.so /vendor/bin/nano
```
![image](https://user-images.githubusercontent.com/19675356/228701163-c48ffa31-3365-4c21-977c-4f7dfa642b46.png)

```bash
# Por fim, execute o nano!

nano /data/teste.txt
```
![image](https://user-images.githubusercontent.com/19675356/228701240-3f00819d-8b7f-49f5-a908-8768fcb3db1d.png)

### 9.4. Portando um Novo Programa para o Android


```bash
# Neste exemplo, iremos portar e instalar no Android um dos utilitários mais úteis do Linux: o sl 
# (não confundir com o ls). Primeiro, vamos instalá-lo e executá-lo no seu PC para ver o que ele faz:

sudo apt install sl
sl
```
![image](https://user-images.githubusercontent.com/19675356/228701360-67954c4f-dc8c-41c7-b898-ab576a6fc30c.png)

```bash
# Vamos baixar o código fonte dele:

cd /media/arquivos/aosp/device/palomakoba/onion/external
git clone https://github.com/mtoyoda/sl.git
```
![image](https://user-images.githubusercontent.com/19675356/228701456-74a8f62d-bf36-4e96-a260-fe1daffbce63.png)

```bash
gedit st/Android.mk

# Inclua o conteudo abaixo:

LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)

LOCAL_SRC_FILES := sl.c
LOCAL_C_INCLUDES := device/palomakoba/onion/external/libncurses/include
LOCAL_SHARED_LIBRARIES := libncurses
LOCAL_MODULE := sl
LOCAL_VENDOR_MODULE := true

include $(BUILD_EXECUTABLE)
```
![image](https://user-images.githubusercontent.com/19675356/228701918-a3093486-b835-4184-a470-af5d7299cd5e.png)

```bash
# Por fim, basta agora incluir o novo módulo no arquivo de configuração do nosso produto:

cd ..
gedit palomakoba_onion.mk
```
![image](https://user-images.githubusercontent.com/19675356/228702604-13d2c05c-67d0-44b8-aa9d-91b4f6390702.png)

```bash
# Recompile o AOSP, reinicie o emulador, entre no adb shell e execute o comando sl. Voila! Você 
# acabou de portar um utilitário para o Android. Execute o sl. Quando ele estiver executando, 
# tire um screenshot dele.

m
emulator &
adb shell
```
![image](https://user-images.githubusercontent.com/19675356/228703444-894609e3-a711-4cc0-b786-90792d4ca096.png)
![image](https://user-images.githubusercontent.com/19675356/228703628-fbb1d82f-51e8-4082-81a0-e61a39f9025b.png)
![image](https://user-images.githubusercontent.com/19675356/228703731-32a51e89-d344-4ff1-a3d9-2c867b946705.png)

### Sumario

> 
