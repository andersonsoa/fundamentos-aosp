## Projeto Final
### Athena © 2023

> Tema: Athena (Mitologia/Cavaleiro dos Zodiaco)

Estrutura do Produto.  
![image](https://user-images.githubusercontent.com/19675356/230241612-8b396daf-66d6-475c-b2e7-0b52bebe06e8.png)


BoardConfig.mk  
![image](https://user-images.githubusercontent.com/19675356/230241691-a39e9d84-a22e-4fd1-a7f5-458801975b5a.png)

AndroidProducts.mk
![image](https://user-images.githubusercontent.com/19675356/230241742-495ff4c3-0914-40f8-94f3-aa1e3f52623f.png)

palomakoba_athena.mk  
![image](https://user-images.githubusercontent.com/19675356/230241935-5ce2043b-aa77-4e32-bcc9-b24f6b35ed53.png)

Arquivos editados via 'overlay' (config.xml e strings.xml)
![image](https://user-images.githubusercontent.com/19675356/230242065-bdfdc4a0-a3cd-4ed5-afc8-6fc575874734.png)

Apps criados para o produto (seguindo o tema proposto)
![image](https://user-images.githubusercontent.com/19675356/230242181-6aa9f073-6dc3-4c54-a59f-d1b5de45a8fb.png)

Botanimation criado pelo grupo.  
![image](https://user-images.githubusercontent.com/19675356/230242375-eaf4e6ff-b21f-46be-a4ef-102f22116980.png)

Atravez so overlay alteramos o tema padrão do produto para 'Escuro' e setamos o build number do produto  
- alteração feita no arquivo `overlay/frameworks/base/core/res/res/values/config.xml`
![image](https://user-images.githubusercontent.com/19675356/230242467-1bfe6fdb-7f33-47ec-9af6-46f1bc227efe.png)
- alteração feita no arquivo `overlay/packages/apps/Settings/res/values/strings.xml`
![image](https://user-images.githubusercontent.com/19675356/230242702-3393c88f-8f9f-4fd2-af7c-208ace811aa8.png)

Estes são alguns dos apps adicionados ao produto durante o build  
- podemos comprovar isso nos detalhes do app, não possivel desistalar.

