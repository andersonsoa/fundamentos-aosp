## 10. Apps em Java

### 10.1. Executando um App no Emulador a partir do Android Studio

Vamos fazer isso agora.  
  
1. Inicie o seu emulator com o seu produto Palomakoba Onion!.  
2. Inicie o Android Studio e peça para criar um novo app no estilo Hello World. Chame esse app de HelloApp.  
3. Pressione a tecla Shift+F10 no Android Studio para executar o app no emulador.  
4. Observe o seu emulador executando o novo app.  
  
Tirar um screenshot do app rodando no seu Android.  
![image](https://user-images.githubusercontent.com/19675356/228988951-3370fcfa-3e98-4129-bd9c-b3d3e432f82a.png)
  
  
Abra a lista dos aplicativos instalados e tire um screenshot do seu app na lista.  
![image](https://user-images.githubusercontent.com/19675356/228989211-eaba3aa9-c2f5-4690-a37c-745fce866b00.png)
  
  
Vá em Settings → Apps → See all 16 apps e clique no nome do seu novo app.  
Tirar um screenshot da tela. Note, em especial, a possibilidade de desinstalar o app.  
![image](https://user-images.githubusercontent.com/19675356/228989338-ace88f79-3058-4017-b9b2-fabcaba6a81a.png)
  
  
Se você reiniciar o seu emulador, você irá notar que o seu novo app continua instalado. Para desinstalá-lo,  
use a tela de settings acima ou (mais lento) execute o comando make installclean seguido de m.  
Faça isso agora, pois será necessário nas próximas seções.  

```bash
make installclean
m
```
![image](https://user-images.githubusercontent.com/19675356/228994431-25531bd3-65d8-4ef8-acfd-0949d06f124f.png)

### 10.2. Incluindo o App no Produto  

O primeiro passo para incluir o HelloApp em nosso produto é copiar os seus arquivos:   
```bash
cp -r -p ~/AndroidStudioProjects/HelloApp /media/arquivos/aosp/device/palomakoba/onion/
```
![image](https://user-images.githubusercontent.com/19675356/228994523-6b1d6de3-305d-4131-bf3f-9d4154c13c2b.png)
  
Salve a tag dependencies do build.gradle do seu app.  
![image](https://user-images.githubusercontent.com/19675356/228994859-e08c42c9-90a3-4d0a-b459-7b4b8cef061d.png)

```bash
dependencies {

    implementation 'androidx.appcompat:appcompat:1.3.0'
    implementation 'com.google.android.material:material:1.4.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.0.4'
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.3'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
}
```
  
Precisamos do Android.bp. Portanto, vamos criá-lo:  
```bash
cd /media/arquivos/aosp/device/palomakoba/onion/HelloApp
gedit Android.bp # Inclua nele o conteúdo abaixo
```
```
  android_app {
    name: "HelloApp",
    vendor: true,
    
    srcs: ["app/src/**/*.java"],
    resource_dirs: ["app/src/main/res"],
    static_libs: [
      "com.google.android.material_material",
      "androidx-constraintlayout_constraintlayout",
      "androidx.test.ext.junit",
      "androidx.test.espresso.core",
    ],
    
    manifest: "app/src/main/AndroidManifest.xml",
    sdk_version: "system_current",
    certificate: "platform",
 }
```
  
Por fim, precisamos mudar a configuração do nosso produto para incluir o pacote criado:
```bash
gedit palomakoba_onion.mk
```
![image](https://user-images.githubusercontent.com/19675356/228995697-741bc8bc-5ad0-426d-b912-31c77f134e5d.png)

```bash
# Compilar o sistema

m
emulator &
```

Vá em Settings → Apps → See all 16 apps e clique no nome do seu novo app.  
Tire um screenshot da tela. Note, em especial, a impossibilidade de desinstalar o app.  
![image](https://user-images.githubusercontent.com/19675356/228998766-2c421531-592c-45fc-a232-7e58034d44fd.png)
![image](https://user-images.githubusercontent.com/19675356/228998930-7dfe9c4b-bc11-4769-8c62-e8e66733d318.png)


Entre no adb shell e execute o comando abaixo para ver aonde ele está armazenado:  
![image](https://user-images.githubusercontent.com/19675356/228999002-c17fa59f-6034-46af-9995-21f0329a199a.png)
  
  
### 10.3. App Customizado: Você é o próximo!

[x] Desenvolva uma App em Java utilizando o Android Studio: 
  O nome de app será Você é o próximo;  
  Sua função é, dada uma lista de alunos pré-estabelecida, sortear aleatoriamente um dos nomes e mostrar na tela o nome e a foto;  
  É importante que as imagens tenham a mesma dimensão para não haver problemas na hora da exibição.  
  Ao clicar no botão "Quem é o próximo?" o app deve substituir a imagem inicial (pode ser a imagem de uma interrogação) pela imagem correspondente ao aluno.  
  A lista de alunos contém, no mínimo, 10 estudantes. Você pode criar seus próprios nomes ou utilizar a própria turma.  
  As Strings utilizadas no App devem ser especificadas no arquivo Strings.xml;   
  As cores utilizadas para construção do tema do App devem ser especificadas no arquivos colors.xml  
  Especifique um tema para sua aplicação. Faça isso por meio do arquivo themes.xml  
