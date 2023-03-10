# Prática no Laboratório - Fundamentos do AOSP
## 2. Código-fonte do Android

### 2.1. Estudando o código-fonte do Android

> a) Toolchain (Clang) pré-compilado para Linux.
![image](https://user-images.githubusercontent.com/19675356/224193347-3e206731-4f52-428e-82be-03e0db9dce52.png)

> b) Código-fonte da biblioteca C do Android.
![image](https://user-images.githubusercontent.com/19675356/223890653-c75efaf4-1799-40b3-8794-5e635e809484.png)

> c) Código-fonte do SQLite.
![image](https://user-images.githubusercontent.com/19675356/223892983-e148b276-644c-48bb-a0d4-4a1106d5e652.png)

> d) Código-fonte da biblioteca de log (liblog).
![image](https://user-images.githubusercontent.com/19675356/223893910-ce586e03-a858-4410-aa1f-ad88c85bcb10.png)

> e) Arquivos de configuração do produto emulator_x86_64.
![image](https://user-images.githubusercontent.com/19675356/224198026-82a0f238-74c8-421e-be55-db1a8dae3a9f.png)

> f) Código-fonte da máquina virtual ART.
![image](https://user-images.githubusercontent.com/19675356/223894776-e02fcb4d-d37f-4a68-9854-975907a8534c.png)

> g) Código-fonte da API de localização (Location Manager).
![image](https://user-images.githubusercontent.com/19675356/224185240-6d5f27b2-5879-46b3-a774-0841ef23f451.png)

> h) Código-fonte da aplicação padrão de calendário (Calendar).
![image](https://user-images.githubusercontent.com/19675356/224183904-ea5ccc21-7425-4c2c-8531-51c3133a9669.png)

---
### 2.2. Utilizando o site Code Search

> a) Implementação da função open() da Bionic.
![image](https://user-images.githubusercontent.com/19675356/224185867-8f4872dd-b727-4e98-9eb6-ef74ddab5f60.png)
![image](https://user-images.githubusercontent.com/19675356/224187803-d4da4319-e09e-4f4c-bcae-0695c91d3745.png)

> b) Referências à propriedade de sistema ro.debuggable.
![image](https://user-images.githubusercontent.com/19675356/224185982-f4e8ae7f-389f-4158-abdc-343b0edcc597.png)

> c) Implementação da classe SystemServer do framework.
![image](https://user-images.githubusercontent.com/19675356/224186175-8415f346-9464-430c-81d5-e8f5e815354c.png)

> d) Referências à variável de build BOARD_USES_ALSA_AUDIO.
![image](https://user-images.githubusercontent.com/19675356/224186319-72568d01-7056-48f0-8588-4bb3451567e4.png)

---
### 2.3. Compilando o Android

```bash
cd /media/arquivos/aosp
```
![image](https://user-images.githubusercontent.com/19675356/224187957-0d0ac9e9-2932-4638-b0a7-53461c7b0609.png)

```bash
source build/envsetup.sh
```
![image](https://user-images.githubusercontent.com/19675356/224188097-f6340a29-4abb-4e11-9756-15b08aa10e13.png)

```bash
hmm
```
![image](https://user-images.githubusercontent.com/19675356/224188179-5a0cc2c5-f6c6-4742-b91b-c4a9290ee0ae.png)

```bash
lunch sdk_phone_x86_64-userdebug
# ou
lunch 3
# ou
lunch aosp_barbet-userdebug
```
![image](https://user-images.githubusercontent.com/19675356/224188530-282f7890-0bae-424d-aed7-ce4a5872f243.png)

```bash
env | grep "ANDROID\|TARGET"
```
![image](https://user-images.githubusercontent.com/19675356/224188806-79ab50f6-b980-4c64-8e90-039d9b00c5b5.png)

```bash
ls out/target/product/emulator_x86_64
```
![image](https://user-images.githubusercontent.com/19675356/224188917-78d619d5-8b47-4167-986b-1a68d474b633.png)

```bash
emulator -help
```
![image](https://user-images.githubusercontent.com/19675356/224189017-615b159c-cc84-4ee4-a7f5-51bb48660aa8.png)

### Resumo
> 2.1
O principal metodo para encontrar os arquivos na pasta aosp foi entrar na pasta que poderia conter o arquivo e rodar o comando
`find | grep -i <ARQUIVO>` e apos localizar, rodei um `cat` no arquivo e tirei e salvei a imagem do resultado.

> 2.2
Este foi mais simples pois o CodeSearch entrega tudo mastigado.

> 2.3
Inicialmente precisamos entrar na pasta onde baixamos o AOSP de preferencia utilizando o usuario administrador, logo após efetuei um `ls` para certificar-me de estar no local correto.
Após isso, carregamos o envsetup, ele adiciona uma seria de comandos utilitário no bash, como `lunch` e `hmm`, hmm lista todos os comandos que podemos utilizar dentro da pasta do aosp, o lunch serve tanto para listar quanto selecionar os produtos disponiveis no aosp.
Em seguida listamos todas as variáveis de ambiente e filtramos pelas variáveis que o lunch e envsetup inserem no sistema.
É falado tambem sobre o comando `m` que serve para compilar o aosp, gerando assim uma nova imagem que pode ser emulada com o comando `emulator`, a imagem gerada fica localizada em `out/target/product/<NOME_DA_IMAGEM>`, podemos ver outros comandos uteis do emulator rodando um `emulator -help`.
