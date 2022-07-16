## Guia MQTT

Este guia contém uma série de experimentos feitos com MQTT, não tem nenhuma pretensão didática.
É suposto que conceitos como Broker, Subscriber, Publisher, Tópico, etc são conhecidos

### MQTT Fast food
O primeiro cenário é uma montagem para quando não se tem dispositivos, nem um servidor para instalar um broker, não temos tempo (ou conhecimento) para "codar" um publisher ou um subscriber mas temos muita pressa. Para essas ocasiões podemos usar um broker online gratuito e um programa que simula publishers e subscribers.

**O Broker:**
Dentre várias opções online gratuitas (EMQx, HiveMQ, Fluux, Eclipse-Mosquitto, etc) escolhemos o Eclipse-Mosquitto (https://mosquitto.org) por razões arbitrárias...
Neste caso, para usar o broker online mosquitto, nas configurações seguintes aonde pedir o ip do broker basta adicionarmos:

`broker_ip: "test.mosquitto.org"`

Nesta primeira montagem, usaremos a porta 1883, lembramos que este broker é **público** então suas telemetrias podem ser interceptadas por qualquer um, sendo um ambiente somente recomendado para testes.

`broker_port: 1883`

**O Publisher / Subscriber:**
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




## MQTT com Publisher feito em Python usando Paho-mqtt

Neste cenário, usaremos a mesma montagem com uma modificação, no lugar do Publisher utilizaremos um script feito em Python, utilizando a biblioteca Paho MQTT, para evitar problemas, foi criado um ambiente virtual em Python (venv) onde rodamos o script nele, também usamos o Python 3.6

Importante comentar que muitas coisas foram inspiradas do seguinte site:

http://www.steves-internet-guide.com/


Utilizamos o VSCode para editar e testar o script.

Para criar o ambiente virtual, depois que definimos uma pasta do projeto no Vscode podemos digitar oseguinte comando na linha do powershel:

`python -m venv venv`

`.\venv\Scripts\Activate.ps1`

Caso você esteja executando pela primeira vez, provavelmente não terá permissão do sistema, para liberar, deverá abrir o Powershell no modo Administrador, e digitar o seguinte comando:

`Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned`

Em seguida use o comando activate novamente, se o ambiente virtual estiver ativo, no prompt do VsCode deverá aparecer um (venv) no início...

a seguir vamos colocar um script mínimo do Paho-mqtt para emitir mensagens:
```
import paho.mqtt.client as paho
broker="test.mosquitto.org"
port=1883

def on_publish(client,userdata,result):             #create function for callback
    print("data published \n")
    pass

client_mqtt= paho.Client("exampleclient")                           #create client object
client_mqtt.on_publish = on_publish                          #assign function to callback
client_mqtt.connect(broker,port)                                 #establish connection
ret= client_mqtt.publish("teste_python","Mensagem de teste")                   #publish

```

Abaixo a imagem do código no VsCode e a saída no terminal, a mensagem enviada pode ser monitorada pelo MQTTBox

![image](https://user-images.githubusercontent.com/44030856/179364653-54273924-8ae9-4d44-91a8-976ba094427d.png)

![image](https://user-images.githubusercontent.com/44030856/179364753-df9e28a9-8cd1-4de1-87e1-4de381376e79.png)






