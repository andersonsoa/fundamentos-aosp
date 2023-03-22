## 7. Personalização do Produto - Init, Propriedades
### 7.1. Cópia de Arquivos para a Imagem

```bash
# Entre no diretório do AOSP, configure o seu terminal para usar o novo produto, e entre no diretório do produto:
# feito!
```

```bash
# Crie um novo arquivo de texto no diretório atual. Nós iremos colocar esse arquivo na imagem do Android depois.

gedit palomakoba.txt 
```
![image](https://user-images.githubusercontent.com/19675356/226777269-405a6aaa-4680-40ba-8f6c-28e4fa0ed667.png)

```bash
# Edite o arquivo palomakoba_zeus.mk, criado em laboratório anterior, e adicione o código abaixo no final do arquivo:

gedit palomakoba_onion.mk

# copia o arquivo palomakoba.txt para o /system/etc da imagem do Android
```
![image](https://user-images.githubusercontent.com/19675356/226777418-c8649f75-b0d3-436a-9ec5-529540edc802.png)
![image](https://user-images.githubusercontent.com/19675356/226777542-7686d835-5fd2-496c-9396-4669ba8dc8e5.png)

```bash
# Compile o novo Android e execute o emulator (caso já tenha um aberto, fecho- antes). 
# Espere uns segundos para o emulador iniciar e execute o adb shell:

m                 # Não é necessário ir par ao diretório principal do AOSP
emulator &        # O '&' inicia o emulador em background, liberando o uso do terminal
sleep 20          # Espera o Android iniciar
adb shell         # Acessa o Linux do novo Android
```
![image](https://user-images.githubusercontent.com/19675356/226781437-b0f1cb7e-44aa-4855-b859-704b00ddf99f.png)

```bash
# No adb shell, verifique se o arquivo foi realmente foi criado:

cd /system/etc
ls
```
![image](https://user-images.githubusercontent.com/19675356/226781545-e0c5fd07-5128-4c69-91fb-2acc0fc4a330.png)

```bash
# Confirme que o conteúdo é o mesmo:

cat palomakoba.txt
```
![image](https://user-images.githubusercontent.com/19675356/226781650-0c4f5099-89a0-4719-b2f8-60fb13c0a9db.png)
  
  
### 7.2. Modificando o Init

```bash
# Feche o seu emulador e saia do adb shell. Você deve estar de volta no diretório do 
# seu produto (device/palomakoba/zeus/). Crie um arquivo chamado zeus.rc:

gedit onion.rc
```
![image](https://user-images.githubusercontent.com/19675356/227061522-86943c71-4703-4b23-b7f8-f2f0a33ea771.png)

```bash
# O que o arquivo de inicialização acima irá fazer?

# R: assim que o sistema começar a iniciar ele setara uma variavel ambiente PALOMAKOBA com o valor "Palomakoba Onion! v1.0"
# 
```

```bash
# Modifique o arquivo palomakoba_zeus.mk para incluir a linha abaixo depois do código em destaque. 
# Note que tem um \ adicional no final do código em destaque.

gedit palomakoba_onion.mk
```
![image](https://user-images.githubusercontent.com/19675356/227062152-ea42f8d1-02ff-469d-8ce5-8e6c17ea5b44.png)

```bash
# Compile o novo Android e execute o emulator (caso já tenha um aberto, fecho-o antes). 
# Espere uns segundo para o emulador iniciar e execute o adb shell:

m
emulator &
sleep 20
adb shell
```
![image](https://user-images.githubusercontent.com/19675356/227063269-385ad3a7-3416-4030-b6b8-d5f0252dae2b.png)
![image](https://user-images.githubusercontent.com/19675356/227063380-20035d79-ee01-410f-8ac8-457f6300ebaa.png)

```bash
# No adb shel, verifique se o arquivo foi realmente criado:

cd /vendor/etc/init
ls -al onion.rc
```
![image](https://user-images.githubusercontent.com/19675356/227063487-e88a80c3-ab60-4fd2-8712-c2f502e80aec.png)

```bash
# Agora vamos ver se o arquivo foi realmente lido e executado pelo Init. Começando pela variável de ambiente:

echo $PALOMAKOBA
```
![image](https://user-images.githubusercontent.com/19675356/227063612-17589592-2818-4b28-94d6-a278324ff701.png)

```bash
# Por fim, vamos verificar se a mensagem foi escrita no logcat:

logcat -d | grep "D Palomakoba"
```
![image](https://user-images.githubusercontent.com/19675356/227063858-d75477f1-10ab-4c43-bd44-2694ed0041c9.png)
  
  
### 7.3. Modificando Propriedades do Sistema

```bash
# Inclua as linhas abaixo no final do arquivo palomakoba_zeus.mk

gedit palomakoba_onion.mk
```
![image](https://user-images.githubusercontent.com/19675356/227064097-e74d9156-7413-484a-8c6d-d5ec98ebdfd7.png)

```bash
# Compile, exexute o emulador e inicie o ADB:

m
emulator &
sleep 20
adb shell
```

```bash

```

```bash

```

```bash

```

```bash

```
