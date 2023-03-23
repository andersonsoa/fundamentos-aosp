## 6. Sistema de Inicialização do Android

### 6.1. Inicialização do Init

```bash
# Analise o código fonte do Kernel Linux e diga os três arquivos que o kernel verifica procurando pelo binário do Init.
```
![image](https://user-images.githubusercontent.com/19675356/226769144-2918a2a4-1041-452c-a67a-7c7cb6485fdd.png)

```bash
#  Caso nem o shell tenha sido encontrado, qual a mensagem impressa pelo kernel?
```
![image](https://user-images.githubusercontent.com/19675356/226769469-94955db9-aff6-41a3-84b5-c281a7e3ec5b.png)

```bash
# Em qual das formas acima o Kernel do Linux encontra o Init no emulador do Android? Vamos investigar! 
# O primeiro passo é verificar as opções passadas para o kernel do emulador. Dentro do adb shell, execute:
cat /proc/cmdline
```
![image](https://user-images.githubusercontent.com/19675356/226769819-82b27731-a0bb-4696-bdbb-57c70c0ac6d9.png)

```bash
# Como você pode ver, no caso do emulador, a opção init= não foi passada. 
# Vamos agora verificar qual dos três arquivos procurados pelo kernel existem.
ls -lhfd /sbin/init /etc/init /bin/init

# O /sbin/init não existe (o Android não tem o diretório /sbin/). Entretanto, temos dois inits! Você consegue identificar qual é o correto?
# "/etc/init" é o correto.
```
![image](https://user-images.githubusercontent.com/19675356/226770165-d615354c-f694-49e4-97f8-4b51e9d059d0.png)
  
  
### 6.2. Configuração do Init  
  
```bash
# O Init é configurado através de arquivos de configurações .rc localizados, principalmente, no diretório /system/etc/init/. 
# Estes arquivos estão no formato Android Init Language, que iremos ver mais adiante.

ls /system/etc/init/
```
![image](https://user-images.githubusercontent.com/19675356/226770673-1d1266bd-1499-45cd-ad9d-6d1bb2cb30bf.png)

```bash
# Quando o Init é iniciado, função LoadBootScripts é chamada para ler os arquivos de configuração. 
# A primeira coisa que é verificada é o conteúdo da propriedade de sistema ro.boot.init_rc. 
# Execute o comando abaixo para ver o conteúdo dessa propriedade no seu sistema:

getprop ro.boot.init_rc
```
![image](https://user-images.githubusercontent.com/19675356/226771029-616aff4e-6b06-4d29-94ff-49426d13e8d6.png)

```bash
# Veja o conteúdo desse arquivo (como o arquivo é grande, usaremos o comando more)

more /system/etc/init/hw/init.rc
```
![image](https://user-images.githubusercontent.com/19675356/226771138-f9f76e40-ebcb-41ef-abc5-a5325d1cf5a1.png)

```bash
# Faça um levantamento de todos os arquivos de configurações lidos pelo Init no emulador. 
# Comece pelo primeiro arquivo lido (/system/etc/init/hw/init.rc/) e vá investigando os arquivos importados por ele. 
# Coloque o nome e o caminho completo dos arquivos mas apenas se eles realmente existirem (alguns não existirão). 
# Se um arquivo for, na verdade, um diretório, coloque o nome seguido de "/*" (e.g., /system/etc/init/*).

system/etc/init/hw/init.rc
    import /init.environ.rc
        # fim
    import /system/etc/init/hw/init.usb.rc
        # fim
    import /init.${ro.hardware}.rc
        # não encontrei
    import /vendor/etc/init/hw/init.${ro.hardware}.rc
        # fim
    import /system/etc/init/hw/init.usb.configfs.rc
        # fim
    import /system/etc/init/hw/init.${ro.zygote}.rc
        # fim
```

```bash
# No total, quantos arquivos .rc diferentes são lidos? Dica: para saber a quantidade de arquivos em um diretório execute: ls | wc -l  dentro do diretório.

# 67
```
![image](https://user-images.githubusercontent.com/19675356/226773961-19e6d528-01d1-4052-8659-b098b1ce0745.png)
  
 
### 6.3. Android Init Language
  
  
```bash
# Como exemplo de um serviço sendo inicializado pelo Init, entre no diretório /system/etc/init 
# e veja o conteúdo do arquivo surfaceflinger.rc:

cd /system/etc/init/
cat surfaceflinger.rc
```
![image](https://user-images.githubusercontent.com/19675356/226774668-150249d0-81bc-40d8-891b-0ff7a3eff402.png)

```bash
# As opções user e group indicam o usuário e os grupos que o processo de serviço de rodar. 
# Por exemplo, execute o comando abaixo para confirmar o usuário e o grupo principal do SurfaceFlinger:

ps -eo CMD,USER,GROUP | grep surfaceflinger
```
![image](https://user-images.githubusercontent.com/19675356/226774991-c069cb68-3288-4b14-af03-d1f2bb1a8012.png)

```bash
# Como um segundo exemplo configuração de serviço do Init, veja o conteúdo do arquivo bootanim.rc:

cat bootanim.rc
```
![image](https://user-images.githubusercontent.com/19675356/226775073-664d0b0c-4244-4173-8af7-158bbad79511.png)
  
  
### 6.4. Android Init Language - Actions
  
```bash
# Como um exemplo, veja o conteúdo do arquivo /init.environ.rc:

cat /init.environ.rc
```
![image](https://user-images.githubusercontent.com/19675356/226775436-b436c5a6-829f-4e6e-9540-147608ec7719.png)

```bash
# Vamos ver se a variável de ambiente ANDROID_DATA foi realmente setada no boot do sistema:

echo $ANDROID_DATA
```
![image](https://user-images.githubusercontent.com/19675356/226775736-16955436-aafa-44ea-a504-03e0f3d8733c.png)

```bash
# Para ver uma lista de todas as ações executadas pelo Init (e seus triggers) no seu sistema atual, execute:

dmesg | grep "processing action"
```
![image](https://user-images.githubusercontent.com/19675356/226775879-e11d2974-425d-4f95-8adb-3e32854e3026.png)

```bash
# No código fonte do init, os estados iniciais são executados no próprio código usando o método 
# QueueEventTrigger. Já os outros estágios são disparados pelo arquivo de configuração principal do init (/system/etc/init/hw/init.rc):

cat /system/etc/init/hw/init.rc | grep -A 35 "Mount filesystems and start core system services"
```
![image](https://user-images.githubusercontent.com/19675356/226776125-bfad98eb-e824-45c3-9629-de9855833877.png)

```bash
# Por fim, um outro evento que pode disparar ações do Init é mudança de propriedades do sistema. 
# Por exemplo, execute o comando abaixo para ver as últimas linhas do arquivo /system/etc/init/bootstat.rc:

tail -8 /system/etc/init/bootstat.rc
```
![image](https://user-images.githubusercontent.com/19675356/226776304-00008474-4f44-4f76-9779-1803ea359e26.png)
  
  
> Descreva sumariamente o processo de execução dos comandos indicados no laboratório, explicando função e/ou significado de cada um

### Sumario

> Neste módulo aprendemos sobre o ciclo de vida da inicialização do android, vimos e aprendemos sobre os principais
> eventos disparados durante o boot, quando ele seta, executa ou delega execução para outros arquivos.
> Vimos que exitem mais de 60 arquivos direfentes que são responsáveis por iniciar diversos serviços responsáveis
> por varias partes do sistema.
