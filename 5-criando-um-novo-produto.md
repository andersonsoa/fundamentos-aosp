# Prática no Laboratório - Fundamentos do AOSP
## 5. Criando um Novo Produto

### 5.1. Convenções de Nomes e Diterórios

```bash
cd device
ls
```
![image](https://user-images.githubusercontent.com/19675356/225475386-6f3d9584-dde0-4d78-a953-419dd0ad7c53.png)


```bash
cd google
ls
```
![image](https://user-images.githubusercontent.com/19675356/225475598-9d93311d-57d8-4708-8d2f-9a5454a7b400.png)

<br />
<br />
### 5.2. Analisando o Produto do Emulador

```bash
gedit /build/target/product/sdk_phone_x86_64.mk
```
![image](https://user-images.githubusercontent.com/19675356/225476331-5829abbb-a4e9-4b39-84b5-59b291556a38.png)


```bash
# Salve a declaração completa das variáveis mencionadas.
```
![image](https://user-images.githubusercontent.com/19675356/225476749-e8b20ca8-b7a2-4ff5-a712-77d3118d56d2.png)


```bash
gedit build/target/board/emulator_x86_64/BoardConfig.mk
```
![image](https://user-images.githubusercontent.com/19675356/225476884-6e2709ba-a8f7-4a4a-b1bc-d06d87f534dc.png)


```bash
# Salve a declaração completa das variáveis mencionadas.
```
![image](https://user-images.githubusercontent.com/19675356/225476979-96f74ac6-3436-4e13-998b-31bd5754e85a.png)

<br />
<br />
### 5.3. Criando e Compilando um Novo Produto

```bash
mkdir -p device/palomakoba/onion
cd device/palomakoba/onion
```
![image](https://user-images.githubusercontent.com/19675356/225477447-55f94fbc-065b-45b2-9d3e-6cb2ac96ffd1.png)

```bash
gedit AndroidProducts.mk
```
![image](https://user-images.githubusercontent.com/19675356/225478172-1599aa1f-4f79-46f3-8900-954edd888773.png)

```bash
gedit palomakoba_onion.mk
```
![image](https://user-images.githubusercontent.com/19675356/225478422-08e19248-1cc2-420b-b3d9-49a69d01ab0c.png)

```bash
gedit BoardConfig.mk
```
![image](https://user-images.githubusercontent.com/19675356/225478862-75ee26a6-0474-4525-9325-2b76f14f5f60.png)

```bash
lunch
```
![image](https://user-images.githubusercontent.com/19675356/225478996-f401221a-d723-47b8-a045-48246ad80e9f.png)

```bash
lunch palomakoba_onion-eng
```
![image](https://user-images.githubusercontent.com/19675356/225479094-2990e33b-2660-4784-bdd9-89961863d187.png)

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
