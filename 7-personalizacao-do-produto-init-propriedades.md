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
