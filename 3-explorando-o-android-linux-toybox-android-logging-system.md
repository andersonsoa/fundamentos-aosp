# Prática no Laboratório - Fundamentos do AOSP
## 3. Explorando o Android/Linux - Toybox, Android Logging System

### 3.1. Toybox

```bash
adb shell
cd /system/bin
ls -al
```
![image](https://user-images.githubusercontent.com/19675356/225171906-72fc76d0-bd6c-4dae-84dc-baa5c988f7f0.png)


```bash
ls -al | grep toybox | wc -l
```
![image](https://user-images.githubusercontent.com/19675356/225172846-b65f9569-ee05-496b-8036-9e3c944dddaf.png)


```bash
toybox
```
![image](https://user-images.githubusercontent.com/19675356/225172960-8623f3a2-6bd9-4298-b5f4-2904c8ae9a8d.png)


### 3.2. Logs do Kernel: dmesg

```bash
su
dmesg -T
```
![image](https://user-images.githubusercontent.com/19675356/225174235-63dd26ef-8aba-4874-b953-54a3beac8607.png)


```bash
dmesg -T -w
```
![image](https://user-images.githubusercontent.com/19675356/225174375-1921dd44-94b1-4f06-9f81-8c20fb89875d.png)


```bash
echo "Planet: Omicron Persei 8" > /dev/kmsg
dmesg -T
```
![image](https://user-images.githubusercontent.com/19675356/225174635-d837198b-d094-4ccc-a15f-a94f0005a504.png)


```bash
cat /dev/kmsg
```
![image](https://user-images.githubusercontent.com/19675356/225174800-b16a7fcd-8465-4682-a391-fc6817dee30d.png)


### 3.3. Logs do Android: Android Logging System

```bash
logcat
```
![image](https://user-images.githubusercontent.com/19675356/225175063-ee731da3-ddee-410c-8aae-b04ac5dcbcff.png)


```bash
exit # para sair do adb shell
adb logcat
```
![image](https://user-images.githubusercontent.com/19675356/225175247-8950f607-e4cc-4d39-b8f4-f0c564ed38ab.png)


```bash
logcat -s Galley:I
```
![image](https://user-images.githubusercontent.com/19675356/225175988-824d02f9-5359-47b5-94ad-a9347bdbd46e.png)


```bash
logcat -s Zygote
```
![image](https://user-images.githubusercontent.com/19675356/225176057-5dbe0d64-cbc6-4bb6-8efa-f1b6c2b7e7de.png)


```bash
logcat -s *:I
```
![image](https://user-images.githubusercontent.com/19675356/225176101-25dee7d5-c01e-41d9-937f-c5995745f685.png)


```bash
logcat -s Zygote:I
```
![image](https://user-images.githubusercontent.com/19675356/225176147-b52c7222-0408-493f-9bb4-19cd12905b6c.png)


```bash
logcat -b events
```
![image](https://user-images.githubusercontent.com/19675356/225176505-81478888-25e2-4c52-b12b-11de9b807d3a.png)


```bash
logcat -h
```
![image](https://user-images.githubusercontent.com/19675356/225176864-613ff07a-deb5-4be1-94b7-385a7ba1cbf1.png)


```bash
log -p I -t "book" "To the 8th Dimension and Back Again"
logcat
```
![image](https://user-images.githubusercontent.com/19675356/225177670-4a4e7b28-7377-4524-a6bc-ec8620b6db8a.png)


```bash
su
ls -al /dev/socket/logd*
```
![image](https://user-images.githubusercontent.com/19675356/225177913-c4354d67-b85d-4255-a992-c81988031501.png)


```bash
echo -n 'getLogSize 0\0EXIT\0' | nc -U /dev/socket/logd
```
![image](https://user-images.githubusercontent.com/19675356/225178157-a6ca8b20-7fbe-4cf5-a07d-f2345adf2359.png)


```bash
logcat -g
```
![image](https://user-images.githubusercontent.com/19675356/225178261-b89c7d47-75dd-4f58-8b1a-b0ae4a839ec2.png)

### Sumário
> Neste laboratório relembramos alguns conceitos referentes ao toybox e os logs na plataforma android  
> o toybox nada mais é do que o mesmo conjunto de comandos utilitários presentes no linux, porem com diversas melhorias  
> no desempenho e no tamanho, já que os dispositivos onde geralmente o android e instalado não possuem estapoço e memorias abuntantes

> Relembramos as principais formas de capturar logs utilizando o adb shell e tambem fora dele
> desde o dmesg que armazena logs em arquivos ao logcat que utiliza sockets de logs do sistema
> e o mais interessante a meu ver e a utilização de varios buffers diferentes para agrupar os logs
