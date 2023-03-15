# Prática no Laboratório - Fundamentos do AOSP
## 4. Explorando o Android/Linux - Eventos, Utilitários, Daemons

### 4.1. Eventos de Dispositivos de Entrada

```bash
getevent
```
![image](https://user-images.githubusercontent.com/19675356/225179192-f4fcca82-0ff5-4a21-821b-336005c41062.png)

```c
#define KEY_VOLUMEDOWN		114
```
![image](https://user-images.githubusercontent.com/19675356/225179311-ba71747a-4198-4028-9b9e-a19403bd74bc.png)

```bash
getevent -l
```
![image](https://user-images.githubusercontent.com/19675356/225179471-67b7f77c-c37f-4e73-ad7a-1bda5ee8e775.png)
![image](https://user-images.githubusercontent.com/19675356/225179595-ed97cd12-1067-4fb5-bdfd-fba33da15666.png)

```bash
sendevent <device> <type> <code> <value>
```
![image](https://user-images.githubusercontent.com/19675356/225180287-9b63e945-9992-46ff-b44a-8162d8fefde6.png)

```bash
sendevent /dev/input/event14 1 114 1 && sendevent /dev/input/event14 0 0 0 && \
sleep 0.5 && \
sendevent /dev/input/event14 1 114 0 && sendevent /dev/input/event14 0 0 0
```
![image](https://user-images.githubusercontent.com/19675356/225180780-ff86167c-8aa4-46cf-b521-b91ea88316c4.png)

```bash
sendevent /dev/input/event14 1 114 1 && sendevent /dev/input/event14 1 116 1 && sendevent /dev/input/event14 0 0 0 && \
sleep 0.2 \
sendevent /dev/input/event14 1 114 0 && sendevent /dev/input/event14 1 116 0 && sendevent /dev/input/event14 0 0 0
```
![image](https://user-images.githubusercontent.com/19675356/225181607-b62c782d-2562-4d33-b9f8-90e11d03ef69.png)

### 4.2. Outros Utilitários do Android

```bash
getprop
```
![image](https://user-images.githubusercontent.com/19675356/225182073-f4dc8c71-1e3a-46a7-b045-336c10677b40.png)

```bash
getprop ro.product.board
```
![image](https://user-images.githubusercontent.com/19675356/225182246-f6c08b15-7691-404e-9418-3b4d78d17d1f.png)

```bash
setprop palomakoba.pi "3.2546373698888"
getprop palomakoba
```
![image](https://user-images.githubusercontent.com/19675356/225182405-83f728db-2349-4a50-bcbe-c170f8939d99.png)

```bash
setprop ro.product.board "CM-89"
```
![image](https://user-images.githubusercontent.com/19675356/225182551-794dfa81-b5fe-427c-8f4f-572d886c5d43.png)

```bash
setprop persist.palomakoba.location "Timber Hearth"
reboot
su
getprop persist.palomakoba.location
```
![image](https://user-images.githubusercontent.com/19675356/225182732-a2ca7057-2420-4f3d-a973-a1294d7f2d43.png)

```bash
screencap /sdcard/photo.png
```
![image](https://user-images.githubusercontent.com/19675356/225182867-9af785e1-09a3-4f4a-99e8-aec1086f8cfe.png)

```bash
adb pull /sdcard/photo.png
eog ~/photo.png
```
![image](https://user-images.githubusercontent.com/19675356/225183071-1b0f8d1f-e279-4752-9512-e3913cfc9605.png)

```bash
adb exec-out screencap -p > ~/screenshop.png
eog ~/screenshop.png
```
![image](https://user-images.githubusercontent.com/19675356/225183341-e33d57b3-1b8f-44c5-8fb7-58ae3288e7bd.png)

```bash
top
```
![image](https://user-images.githubusercontent.com/19675356/225183487-c1ed802d-1550-4d00-bf92-136ffb9f3711.png)

```bash
free -h
```
![image](https://user-images.githubusercontent.com/19675356/225183534-e5b83a6d-f493-4836-9a56-4823e7070157.png)

```bash
cal
```
![image](https://user-images.githubusercontent.com/19675356/225183666-ec456e4a-51e1-4801-8c1b-70b940576f21.png)

### 4.3. Daemons do Android
```bash
ps -ef | grep -v grep | grep -e adbd -e "init sec" -e installd -e lmkd -e "logd" -e tombstoned -e ueventd -e vold
```
![image](https://user-images.githubusercontent.com/19675356/225184203-1ea1b079-088b-4b3c-abef-c05802b25080.png)

```bash
ls -al /system/bin/ueventd
```
![image](https://user-images.githubusercontent.com/19675356/225184310-4af1f652-8376-4bc3-8be6-d4edbc8d8c28.png)

- tres linhas que verificam o argv
![image](https://user-images.githubusercontent.com/19675356/225184482-6845a61a-9ab4-4e94-8e7d-00800f646893.png)

### Sumário

> Primeiramente aprendemos sobre como escutar e disparar eventos no android utilizando o adb e sua toolkit  
> usamos principalmente o getenvt para escutar eventos, pois ele nos da informações muito uteis para que possamos
> disparar eventos manualemtne, verificamos o getevent -l que exibe os eventos de forma mais amigavel, com texto indicando que tipo de evento ocorreu.  
> Sendevent é o comando utilizado para envitar eventos do adb shell, para isso precisamos saber qual device queremos simular, qual tipo de evento queremos disparar,  
> o código referente e tambem o valor.

> Posteriormente aprendi sobre as variaveis de ambiente so android, como listalas e setalas  
> para listar as variaveis basta utilizar um getprop e se quisermos detalhar uma variavel ambiente especifica  
> basta informala Ex: getprop <NOME_DA_VARIAVEL>.
> Já para definir novas variaveis utilizamos o comando setprop (lembrando que para isso precisamos estar com o SU ativo no terminal),
> más variaveis definidas não persistem entre reboots do emulador, para que isso ocorra precisamos criar ela com o prefixo persist,
> lembrando que exitem variaveis somente de leitura que não podem ser sobreescritas.
> vimos tambem que utilizando os comandos screencap e screenrecord podemos tirar screenshots e gravar videos no emulador.

> Na parte final aprendemos sobre os principais serviços rondando no android, que basicamente o mantem funcionando.
