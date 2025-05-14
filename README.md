
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

### ▶️ Wemos D1 Mini (ESP8266)
<img src="https://github.com/Epaminondaslage/D1-Mini-Lolin/blob/master/Figuras/wemos di mini lolin.JPG" height="150" width="200">

### ▶️ Shield Relé V2 para Wemos
![Módulo Relé V2](https://ae01.alicdn.com/kf/HTB1k1xHbUCF3KVjSZJnq6znHFXaC.jpg)

---

## 🔌 Etapa 1 – Montagem do Hardware

1. Encaixe o **módulo relé shield V2** diretamente sobre o Wemos D1 Mini.
2. Conecte o conjunto ao computador via **cabo micro USB**.

---

## 🌐 Etapa 2 – Instalar o Firmware Tasmota via Navegador

1. Acesse: [https://tasmota.github.io/install](https://tasmota.github.io/install)
2. Clique em **"Connect"**
3. Selecione a porta USB do Wemos D1 Mini
4. Clique em **"Install Tasmota"**
5. Aguarde a gravação e configure o Wi-Fi

---

## 📶 Etapa 3 – Configurar Wi-Fi

1. O ESP entrará em modo AP com nome **`tasmota-XXXX`**
2. Conecte-se a esse Wi-Fi (senha: `tasmota123`)
3. Acesse automaticamente a página de configuração
4. Insira os dados da sua rede Wi-Fi local
5. O dispositivo reiniciará e se conectará à sua rede

---

## ⚙️ Etapa 4 – Configurar o Módulo Relé

1. Acesse o IP do dispositivo na rede local
2. Vá em **Configuration > Configure Module**
3. Em “Module Type”, selecione: `Generic (18)`
4. Configure os GPIOs:

| GPIO        | Função no Tasmota | Conectado a...     |
|-------------|-------------------|---------------------|
| GPIO5 (D1)  | Relay1            | Entrada do Relé     |
| GPIO0 (D3)  | Switch1           | Botão físico (opcional) |

5. Salve e aguarde o reinício

---

## ☁️ Etapa 5 – Configurar o Broker MQTT

1. Vá em **Configuration > Configure MQTT**
2. Preencha os campos conforme abaixo:

```
Host: 10.0.0.141
Port: 1883
User: mqtt
Password: planeta
Topic: tasmota_%06X
Full Topic: %prefix%/%topic%/
```

3. Clique em **Save** e o dispositivo se conectará ao broker MQTT

---

## 🧪 Etapa 6 – Testar e Integrar

- Acesse novamente a interface web
- Pressione **TOGGLE** para acionar o relé
- Monitore a conexão MQTT no broker (ex: com MQTT Explorer)

---

