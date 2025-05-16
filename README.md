
# Guia de Instalação do Firmware Tasmota no Wemos D1 Mini Lolin com Módulo Relé Acoplado

Instalação do firmware **Tasmota** no **Wemos D1 Mini (ESP8266)** com o **módulo relé V2 acoplado**, permitindo controle remoto via Wi-Fi, MQTT e integração com Home Assistant.

--

## Repositorios com assuntos relacionados

* http://github.com/epaminondaslage/mini-lolin-relay-mqtt
* http://github.com/epaminondaslage/Wemos-Mini-Lolin

---

## 🧰 Materiais Necessários

- 1x Wemos D1 Mini (ESP8266)
- 1x Módulo Relé Shield V2.0.0 para Wemos
- 1x Cabo micro USB
- Navegador Google Chrome ou Microsoft Edge
- Acesso à internet

---

## 📸 Imagens dos Componentes

### Wemos D1 Mini (ESP8266)
<img src="https://github.com/Epaminondaslage/D1-Mini-Lolin/blob/master/Figuras/wemos di mini lolin.JPG" height="150" width="200">

### Shield Relé V2 para Wemos

<img src="https://github.com/Epaminondaslage/mini-lolin-relay-tasmota/blob/main/rele.jpg" height="150" width="200">

<img src="https://github.com/Epaminondaslage/mini-lolin-relay-tasmota/blob/main/rele1.jpg" height="150" width="200">

---

##  Montagem do Hardware

1. Encaixe o **módulo relé shield V2** diretamente sobre o Wemos D1 Mini.
2. Conecte o conjunto ao computador via **cabo micro USB**.
   
---

##  Tabela de GPIOs recomendados para Botão e Relé no Mini Lolin D1 (ESP8266)

| Função    | Nome na placa | GPIO   | Configuração no Tasmota | Observações                         |
|-----------|----------------|--------|---------------------------|--------------------------------------|
| Relé 1    | D1             | GPIO5  | Relay1 (21)               | Recomendado, seguro no boot          |
| Relé 2    | D5             | GPIO14 | Relay2 (22)               | Opcional                             |
| Relé 3    | D6             | GPIO12 | Relay3 (23)               | Opcional                             |
| Relé 4    | D7             | GPIO13 | Relay4 (24)               | Opcional                             |
| Botão 1   | D2             | GPIO4  | Button1 (17)              | Recomendado, sem problemas           |
| Botão 2 ⚠️ | D3             | GPIO0  | Button2 (18)              | ⚠️ Deve estar em HIGH no boot        |
| Botão 3 ⚠️ | D4             | GPIO2  | Button3 (19)              | ⚠️ Deve estar em HIGH no boot        |

---

### Dicas

- **Relés**: preferencialmente use GPIOs **5, 14, 12, 13** (D1, D5, D6, D7).
- **Botões**: **GPIO4 (D2)** é excelente para isso, sem conflitos de boot.
- **Evite** usar GPIO0, GPIO2 e GPIO15 com relés ou botões, a menos que saiba lidar com suas **restrições de boot**.

---

### Importante

- Sempre conecte **botões entre o GPIO e o GND**.
- O **resistor de pull-up interno** é ativado automaticamente pelo Tasmota para entrada digital.
- Relés ativos em nível **baixo (LOW)** devem ser testados para não ligarem sozinhos ao iniciar o dispositivo.



# Instalação e Configuração do Tasmota via Navegador (CRHOME)

## Acessar o site 

Acesse: [https://tasmota.github.io/install](https://tasmota.github.io/install)

<img src="./img/tela1.jpg" alt="Tela 1" width="40%">

Conecte seu dispositivo ao computador. O navegador solicitará permissão para acessar a porta serial. 

Selecione a porta correta (ex: `COM6`) e clique em **Conectar**2. Clique em **"Connect"**

<img src="./img/tela2.jpg" alt="Tela 2" width="20%">

---

Clique em **Install Tasmota Lite** para iniciar o processo de gravação do firmware.

<img src="./img/tela3.jpg" alt="Tela 3" width="40%">

---

## Confirmação para apagar o dispositivo
Você deverá apagar a memória do dispositivo antes da gravação. Marque a caixa **Erase device** caso deseje apagar tudo.

<img src="./img/tela4.jpg" alt="Tela 4" width="40%">

---

## Progresso da instalação
Aguarde enquanto o firmware Tasmota é gravado. Essa etapa pode levar alguns minutos.

<img src="./img/tela5.jpg" alt="Tela 5" width="40%">

---

## Configuração de Wi-Fi
Após a gravação, o Tasmota solicitará os dados da sua rede Wi-Fi. Informe o SSID e a senha e clique em **Connect**.

<img src="./img/tela6.jpg" alt="Tela 6" width="40%">

Caso pule esta etapa, o wifi pode ser confifurado posteriormente, conforme o procedimento:

1. Ligar o  ESP e ele entrará em modo AP com nome **`tasmota-XXXX`**
2. Conecte-se a esse Wi-Fi (senha: `tasmota123`)
3. Acesse automaticamente a página de configuração
4. Insira os dados da sua rede Wi-Fi local
5. O dispositivo reiniciará e se conectará à sua rede
---

## Tela inicial do Tasmota
Ao conectar à rede Wi-Fi, acesse o IP mostrado. Esta é a interface inicial do Tasmota.

<img src="./img/tela8.jpg" alt="Tela 7" width="40%">

## Seleção de tipo de módulo
Na opção **Module**, escolha o tipo de dispositivo que está utilizando. Por padrão, o Sonoff Basic é selecionado, mas você pode alterar para **Generic** se estiver usando outro hardware. 

<img src="./img/tela9.jpg" alt="Tela 8" width="40%">

1. Acesse o IP do dispositivo na rede local
2. Vá em **Configuration > Configure Module**
3. Em “Module Type”, selecione: `Generic (18)`

<img src="./img/tela10.jpg" alt="Tela 9" width="40%">

## Mapeamento dos pinos (GPIOs)
Configure os pinos GPIO conforme necessário. No exemplo, o **GPIO5** está configurado como **Relay**.

| GPIO        | Função no Tasmota | Conectado a...     |
|-------------|-------------------|---------------------|
| GPIO5 (D1)  | Relay1            | Entrada do Relé     |
| GPIO0 (D3)  | Switch1           | Botão físico (opcional) |

<img src="./img/tela11.jpg" alt="Tela 10" width="40%">

5. Salve e aguarde o reinício

---
## Menu de configuração
Clique em **Configuration** para acessar as opções de configuração como WiFi, MQTT, módulo, etc.

### Configurar o Broker MQTT (caso tenha um)

1. Vá em **Configuration > Configure MQTT**
2. Preencha os campos conforme abaixo:

```
Host: 192.168.0.10 (ip do Broker- caso tenha)
Port: 1883
User: seuusuario
Password: suasenha
Topic: tasmota_%06X
Full Topic: %prefix%/%topic%/
```
3. Clique em **Save** e o dispositivo se conectará ao broker MQTT
   
<img src="./img/tela13.jpg" alt="Tela 13" width="40%">
---

##  Interface principal

Você pode usar o botão **Toggle** para testar o funcionamento do relé ou dispositivo configurado.

<img src="./img/tela12.jpg" alt="Tela 11" width="40%">

## Testar e Integrar

- Acesse novamente a interface web
- Pressione **TOGGLE** para acionar o relé
- Monitore a conexão MQTT no broker (ex: com MQTT Explorer)

#  Configuração Tasmota: Manter Relé (GPIO5) Ligado por 3 Segundos

Como configurar o relé conectado à **GPIO5 (D1)** no Mini Lolin D1 (ESP8266) para **ligar por 3 segundos** sempre que acionado, usando **regras (Rules)** no Tasmota.

---

##  Configuração do GPIO no Tasmota

| Função  | Nome na placa | GPIO   | Configuração no Tasmota |
|---------|----------------|--------|--------------------------|
| Relé 1  | D1             | GPIO5  | `Relay1 (21)`            |

---

# 🧠 Uso de Regras (Rules) no Tasmota

O Tasmota permite criar **regras (rules)** para executar ações automáticas com base em eventos, como ligar ou desligar um relé após um tempo, ao pressionar um botão ou ao receber um comando MQTT.

---

## 🧩 Estrutura básica de uma regra

```bash
Rule1 on <EVENTO> do <AÇÃO> endon
```

Você pode usar até 3 regras: `Rule1`, `Rule2` e `Rule3`.

---

## 📌 Exemplo prático: ligar o relé no D1 (GPIO5) por 3 segundos

### 🛠️ Configuração

- **GPIO5 (D1)** configurado como `Relay1 (21)` no menu `Configure Module`
- A regra será ativada quando o relé for ligado e desligará automaticamente após 3 segundos

### 📋 Comando para definir a regra:

```bash
Rule1 on Power1#State=1 do backlog Delay 30; Power1 0 endon
```

### ✔️ Ativar a regra:

```bash
Rule1 1
```

---

## 📖 Explicação do exemplo

- `on Power1#State=1` → dispara a regra quando o relé 1 for ligado
- `backlog Delay 30; Power1 0` → espera 3 segundos (30 × 0.1s) e desliga o relé
- `endon` → fim da definição da regra

---

## 🔍 Como verificar a regra atual

No console do Tasmota, digite:

```bash
Rule1
```

---

## 🔧 Comandos úteis

| Ação                         | Comando             |
|------------------------------|---------------------|
| Ativar a regra               | `Rule1 1`           |
| Desativar a regra            | `Rule1 0`           |
| Limpar a regra               | `Rule1 ""`          |
| Ver conteúdo da regra        | `Rule1`             |

---

## 🧪 Teste

1. Defina e ative a regra como mostrado acima
2. Ligue o relé com `Power1 ON` (via botão, MQTT ou interface)
3. Ele desligará automaticamente após 3 segundos

---

## ⚠️ Dica importante

- Regra e `PulseTime` **não devem ser usados ao mesmo tempo** para o mesmo relé, pois podem gerar conflitos
- Use `Rule` se você quiser **lógicas mais complexas** que `PulseTime` não permite

---

Regras são muito poderosas e podem responder a botões físicos, sensores, horário, comandos MQTT e muito mais.

---
# ⏱️ Uso do PulseTime no Tasmota

`PulseTime` é uma funcionalidade do Tasmota que permite **ligar um relé por um tempo determinado automaticamente**. É ideal para controles temporizados, como sirenes, lâmpadas ou motores que devem desligar sozinhos.

---

##  Sintaxe do comando

```bash
PulseTimeX Y
```

- `X` → Número do relé (ex: 1 para Power1, 2 para Power2...)
- `Y` → Duração do tempo (veja explicação abaixo)

---

##  Interpretação dos valores

| Valor de Y       | Tempo Real                    |
|------------------|-------------------------------|
| 0                | Desativa o temporizador       |
| 1 a 111          | Tempo em **segundos**         |
| 112 a 64999      | Tempo em **décimos de segundo** (`Y / 10`) |

> Exemplo: `PulseTime1 30` → liga o relé 1 por **3 segundos**

---

##  Exemplos práticos

###  Ligar relé por 15 segundos:
```bash
PulseTime1 15
```

###  Ligar relé por 3 segundos:
```bash
PulseTime1 30
```

### Desativar o desligamento automático:
```bash
PulseTime1 0
```

---

##  Como testar

1. Acesse o console do Tasmota via navegador (`http://IP_DO_DISPOSITIVO`)
2. Envie o comando `PulseTime1 30`
3. Ligue o relé com `Power1 ON`
4. Ele desligará automaticamente após 3 segundos

---

## 🔎 Verificando o estado atual do PulseTime

Use este comando:

```bash
PulseTime1
```

Exemplo de resposta:

```json
{"PulseTime1":{"Set":30,"Remaining":0}}
```

- `Set`: tempo configurado
- `Remaining`: tempo restante (mostra 0 se o relé estiver desligado)

---

##  Importante

- `PulseTime` **funciona sem regras** (`Rule`) — é mais simples para ações temporizadas
- Serve para **qualquer relé configurado** como `RelayX`
- Pode ser usado em conjunto com botão físico ou comandos MQTT

---


