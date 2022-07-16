## Guia MQTT

Este guia é uma série de experimentos feitos com MQTT, não tem nenhuma pretensão didática.
É suposto que conceitos como Broker, Subscriber, Publisher, Tópico, etc são conhecidos

### MQTT Fast food
O primeiro cenário é uma montagem para quando não se tem dispositivos, nem um servidor para instalar um broker, não temos tempo (ou conhecimento) para "codar" um publisher ou um subscriber mas temos muita pressa. Para essas ocasiões podemos usar um broker online gratuito e um programa que simula publishers e subscribers.

**O Broker:**
Dentre várias opções online gratuitas (EMQx, HiveMQ, Fluux, Eclipse-Mosquitto, etc) escolhemos o Eclipse-Mosquitto !(https://mosquitto.org) por razões arbitrárias...
Neste caso, para usar o broker online mosquitto basta nas configurações seguintes aonde pedir o ip do broker adicionarmos:

`broker_ip: "test.mosquitto.org"`

Nesta primeira montagem, usaremos a porta 1883, lembramos que este broker é **público** então suas telemetrias podem ser interceptadas por qualquer um, sendo um ambiente somente recomendado para testes.

**O Publisher / Subscriber**
Para envio e monitoramento das mensagens, usaremos o MQTTBox, este prático programa pode ser bem útil para testes simples. Existem duas opções de instalação:

a) MQTTBox para Windows (pode ser baixado da Loja do Windows 10, o que dá uma certa sensação de segurança).

b) MQTTBox extensão para Chrome (neste caso sode ser usado em outro Sistemas Operacionais que suportem o Chrome).

Eu usei as duas opções, costumo usar o programa, porém sem nenhuma justificativa racional...

Em ambas as opções, depois de instalado, para rodar são necessários alguns parâmetros, a saber:

1 - MQTTClientName -> Você pode colocar o nome que quiser para seu client, neste experimento não afetará em nada

2 - Protocol -> Necessariamente TCP/IP

3 - Host -> test.mosquitto.org


![config_mqttbox1](https://user-images.githubusercontent.com/44030856/179358155-8582dd0f-7c63-46dc-a58f-55afaf132099.png)

Após finalizar as configurações, aperte o botão **Save** e pronto, o status de conectado deve aparecer, indicando que houve sucesso.

Para testar a comunicação, devemos criar um publisher e um subscriber, com o mesmo tópico:
![image](https://user-images.githubusercontent.com/44030856/179361086-ab546920-c332-4aa2-96d2-91f1ee7f70c4.png)

Apertando o botão **Subscribe** , qualquer mensagem que chegar será mostrada

Essa estrutura pode ser usada parcialmente, por exemplo se um dispositivo que publica telemetrias precisa ser testado, utilizamos somente o Broker e o Subscriber.

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/cassiofm/guia_mqtt/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
