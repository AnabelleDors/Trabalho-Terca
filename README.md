Para o funcionamento deste projeto, o funcionamento é o seguinte: Quando dizemos pra acender a lampada, a Alexa não se comunica diretamente com o nosso microcontrolador,
ela manda um comando para a nuvem que repassa para a plataforma SinricPro, essa plataforma é o nosso elo que permite que a interação da nossa Alexa com a nossa lampaa ( ou qualquer outro objeto fisico).
O SinricPro é basicamente nosso "balcão de recados", ele vai guardar os recados (comandos) ali, como por exemplo "alexa, acender a luz", e vai se comunicar com o nosso ESP8266 (microcontrolador) para acender a lampada.
É claro que para isso acontecer o nosso microcontrolador (ESP8266) precisa estar conectado ao wifi e registrado com as mesmas chaves que foram configuradas na plataforma SinricPro, essas chaves são as = APP_KEY, APP_SECRET, SWITCH_ID
Com o ESP8266 conectado ao wifi e com as credenciais do SinricPro corretas, ele mantem a comunicação constante com a plataforma SinricPro, sendo assim quando o SinricPro manda o comando "Ligar",
o nosso microcntrolador ESP8266 recebe o comando e chama a função responsável por ligar a lampada ( onPowerState(deviceId, true); ) com isso o ESP8266 manda energia para o pino de relé ( rele aqui é o nosso interrruptor elétrico), 
ligando-o!

O nosso relé ( Interruptor Elétrico) funciona da seguinte maneira: ele exerce o papel de um interruptor elétrico que funciona a partir de um sinal elétrico), e ele tem duas partes 
1- Lado do Controle: 5V/ ou 3.3V = lado ligado ao microcontrolador ESP8266 que recebe o sinal lógico de LOW: Liga e HIGH: Desliga 
2- Lado de Potencia: 110V ou 220V : lado ligado a lâmpada e a tomada, é o lado responsável por fechar ou interromper o circuito da rede elétrica

A parte da Lampada e os Cabos: Quando o relé está fechado ( ligado) a corrente passa e a lâmpada acende   /  Quando o relé está aberto ( desligado) a corrente é interrompida e a lâmpada apaga
Quando o relé liga, o ESP8266 envia para o SinricPro o comando: mySwitch.sendPowerStateEvent(true); assim tanto o SinricPro quanto a Alexa sabem que a lâmapda está ligada e mantem tudo sincronizado

O fluxo resumido disso é o seguinte:

- Você fala para a Alexa ligar a luz
- A Alexa envia o comando ao SinricPro
- O SinricPro envia o comanda via internet ao ESP8266
- O ESP8266 aciona o relé
- o relé liga a lampada

<img width="347" height="337" alt="image" src="https://github.com/user-attachments/assets/cd583d69-cc6c-47f5-86f9-3bf0d4912b7b" />

