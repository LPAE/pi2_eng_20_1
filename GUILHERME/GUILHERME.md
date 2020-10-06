# Projeto Integrador II - 2020/1

Instituto Federal de Santa Catarina

Departamento Acadêmico de Eletrônica

Professores: 
* Fernando Miranda - <fernando.miranda@ifsc.edu.br>
* Luís Azevedo - <azevedo@ifsc.edu.br>

Aluno: 
* Guilherme da Costa Franco - guilherme3379@gmail.com
  
_________________________________________________________________________  

# Concepção do projeto: Sistema de Irrigação Automatizado <h1>
<p> 
            De grandes hectares de terra a uma pequena horta de varanda. Estes são dois universos, nitidamente distintos por sua proporção espacial, dispõem de uma preocupação em comum: a necessidade de criar um ambiente que monitore e controle a disposição de água de uma forma regular.
</p>
<p>
            Desta forma, far-se-á necessário, como proposta para o Projeto Integrador II de 2020/1, a elaboração de um sistema de irrigação automatizado, cujo foco do projeto consiste em, a partir de um micro controlador, monitorar constantemente um corpo de prova, fornecer automaticamente água em determinadas ocasiões e disponibilizar ao usuário controle do aparelho e dados específicos via aplicativo para celular.
</p>
<p>
            Neste sistema, sensores ficaram responsáveis pela análise constante do nível de umidade do solo. Em resposta a isto, um micro controlador seria responsável por ligar e desligar válvula para fornecer água o suficiente para corrigir quaisquer irregularidades da planta em análise.
</p>
<p>
            Sendo assim, sempre que o sistema liga ou desliga a válvula, uma mensagem é enviada ao usuário via módulo Bluetooth, atualizando o status dos sensores constatemente, tornando este sistema bastante útil em fazendas, jardins e residências. 
</p>

## Tecnologias a serem empregadas
<p>
            O sistema a ser elaborado possui diversos segmentos distintos que serão análisados e interpretados por um microcontrolador e enviados ao usuário. A seguir, serão listados todos os componentes envolvidos para o desenvolvimento do sistema proposto. São eles:
</p>

1. **Arduino MEGA 2560**

<p>
            A placa Arduino Mega 2560 é mais uma placa da plataforma Arduino que possui recursos bem interessantes para prototipagem e projetos mais elaborados. Baseada no microcontrolador ATmega2560, possui 54 pinos de entradas e saídas digitais onde 15 destes podem ser utilizados como saídas PWM. Possui 16 entradas analógicas, 4 portas de comunicação serial.
</p>

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/arduino%20mega.png)

2. **Válvula Solenóide de 12V**

<p>
            Segmento do projeto responsável por controlar o fluxo de água que será direcionado à planta. 

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/v%C3%A1lvula.png)

3. **Módulo relé de 5V**

<p>
        Componente responsável por controlar o funcionamento da vávula solenóide, acionando-o apenas quando os parâmentros do código de programação forem alcançados.
</p>            


![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/rel%C3%A9.jpg)

4. **Sensor de umidade do solo higrômetro**

<p>
            Sensor que fará a leitura da umidade do solo do corpo de prova.
</p>

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/sensor%20umidade%20do%20solo.jpg)

5. **Sensor DHT11**

<p>
            Sensor que fará a leitura da umidade relativa do ar e da temperatura no ambiente em que se encontra o projeto.
</p>

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/dht%2011.jpg)

6. **Módulo Bluetooth HC-05**

<p>
            Este componente será responsável por receber as informações, colhidas pelos sensores e armazenadas pelo Arduino MEGA, e enviá-las ao usuário mediante uso de aplicativos que façam esse tipo de conexão entre o módulo e o celular a fim de exibir, sem o uso de computadores ou notebooks, todos os dados analisados.
</p>            

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/hc%2005.png)

# Design do Projeto <h2>
<p>
  Afim de facilitar a compreensão do funcionamento do projeto, antes de partir para experimentações práticas, foram realizadas a construção de uma Planta Eletrônica e a elaboração de um diagrama de blocos para tanto criar uma visão espacial do projeto, quanto para deixar evidente e inteligível todas as etapas de processos e funções dos componentes envolvidos.
</p>
  
![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/projeto%20fritzing.png)


Obs: as pilhas estão representando fontes de 9V, para a alimentação do Arduino, e de 12V, para a alimentação da válvula solenóide, devido a ausência destes componentes na biblioteca do Fritzing.

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/diagrama%20de%20bloco.png)

# Implementação

<p>
   Nesta etapa de desenvolvimento do projeto, foi implementado o algoritmo para a leitura e tratamento dos sensores, bem como a sua exibição no painel serial do Arduino, sendo escrito inteiramente em linguagem C++.         
</p>

A imagem abaixo retrata os primeiros testes do projeto.

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/testes%20iniciais.jpg)

## Código base para exibição no Serial Bluetooth

```c++

#include <dht.h>
#define pinSensorA A0 //sensor ANALÓGICO do solo
#define pinSensorD 8  //sensor DIGITAL do solo
#define dht_pin 2     //pino de sinal do DHT-11

dht  my_dht;

float temperatura;
float umidade;

void setup() 
{
  pinMode(pinSensorA, INPUT); //Sensor de umidade do solo
  pinMode(12, OUTPUT);        //Atuador -> solenóide
  Serial.begin(9600);
  Serial.println("Início da análise");
}

void loop() 
{
  {
  my_dht.read11(dht_pin);
  temperatura = my_dht.temperature;
  umidade     = my_dht.humidity;
  
  Serial.println(" ");
  Serial.print("Temperatura atual: ");
  Serial.print(temperatura);
  Serial.println("ºC");

  Serial.print("Umidade relativa do ar atual: ");
  Serial.print(umidade);
  Serial.println("%");
  Serial.println("");
  
  Serial.print("Status do sensor digital: ");
  
  if (digitalRead(pinSensorD)) 
  {
     Serial.println("POUCA UMIDADE");
  } 
  if (!digitalRead(pinSensorD)) 
  {
     Serial.println("ÚMIDO");
  }

  Serial.print("Status do sensor analógico: ");
  Serial.print(analogRead(pinSensorA)); 
  Serial.println(" ");
  
  {
  Serial.print("Status geral: ");
  if (analogRead(pinSensorA) > 700 && analogRead(pinSensorA) < 1023)
  {
    Serial.println("Solo seco");
  }
  if (analogRead(pinSensorA) > 0 && analogRead(pinSensorA) < 500)
  {
    Serial.println("Solo úmido");
  }
  if (analogRead(pinSensorA) > 500 && analogRead(pinSensorA) < 700)
  {
    Serial.println("Umidade moderada");
  }
  }

  Serial.print("Atuador: ");
  if (analogRead(pinSensorA) > 700 && analogRead(pinSensorA) < 1023) 
  {
     Serial.println("A VÁLVULA SERÁ LIGADA");
  } 
  if (analogRead(pinSensorA) > 0 && analogRead(pinSensorA) < 500)  
  {
    Serial.println("A VÁLVULA SERÁ DESLIGADA");   
  }
  if (analogRead(pinSensorA) > 500 && analogRead(pinSensorA) < 700)
  {
    Serial.println("AGUARDANDO");
  }
  } 

//Controle do relé
 
  if (analogRead(pinSensorA) > 700 && analogRead(pinSensorA) < 1023)
  {
        delay(5000); //tempo para o solo absorver a água
    
        digitalWrite(12, HIGH);   
        delay(500); //pulso de água
        digitalWrite(12, LOW);  

        delay(10000); //tempo para fazer uma nova análise         
      }
      
  Serial.println("");
  delay(5000);
  
  if (analogRead(pinSensorA) > 0 && analogRead(pinSensorA) < 499)
  {
     Serial.println("O solo se encontra suficientemente úmido");
  } 
  
  if (analogRead(pinSensorA) >= 500 && analogRead(pinSensorA) < 699)
  {
     Serial.println("O solo se encontra razoaveltemente úmido");
  } 
  
  if (analogRead(pinSensorA) >= 700 && analogRead(pinSensorA) < 1023)
  {
     Serial.println("O solo se encontra seco, recomenda-se irrigação");  
  }            
} 

```

A imagem a seguir ilustra o funcionamento do código acima utilizando o aplicativo Serial Bluetooth.

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/serial%20bluetooth%20test.jpg)

As próximas imagens ilustram os primeiros testes com o sistema completo e com água.

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/testes%20com%20%C3%A1gua.jpg)

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/execu%C3%A7%C3%A3o%20final%20sem%20app.jpg)

## Código para exibição e controle no Blynk

```c++

#define BLYNK_PRINT Serial
 
#define pinSensorA A0 //sensor ANALÓGICO do solo
#define pinSensorD 8  //sensor DIGITAL do solo (não será usado)

#define DHTPIN 2          
#define DHTTYPE DHT11  

#include <BlynkSimpleSerialBLE.h>
#include <DHT.h>

#include <SoftwareSerial.h>
SoftwareSerial SerialBT(10, 11); //TX e RX respectivamente (e não RX e TX como mostrado no sketch exemplo do próprio Blynk)

char auth[] = "lOemBm3KeH63tiZiumYy145WEkcggEs3";

DHT dht(DHTPIN, DHTTYPE);
BlynkTimer timer;

WidgetLED led1(V10); //LED de exibição do funcionamento da válvula

void setup()
{
  pinMode(pinSensorA, INPUT); //Sensor de umidade do solo
  pinMode(12, OUTPUT);        //Válvula/relé
  
  Serial.begin(9600);

  SerialBT.begin(9600);
  Blynk.begin(SerialBT, auth);

  Serial.println("Aguardando por conexão...");

  dht.begin();

  timer.setInterval(1000L, enviarSensor);
  timer.setInterval(1000L, molharSolo);
}

void enviarSensor() //Fará a análise do DHT 11
{
  float u = dht.readHumidity();
  float t = dht.readTemperature(); 

  if (isnan(u) || isnan(t)) //Se os dados recebidos não forem um número, o sistema gera uma mensagem de erro
  {
    Serial.println("Falha ao ler o sensor DHT 11!");
    return;
  }
  
  Blynk.virtualWrite(V5, u); 
  Blynk.virtualWrite(V6, t);
}

void molharSolo() //Fará a análise do sensor de umidade do solo e controlará o relé automaticamente
{
  if (analogRead(pinSensorA) >= 700 && analogRead(pinSensorA) < 1023)
  {
        digitalWrite(12, HIGH);
        led1.on();   
        delay(1000);               //pulso de água
        digitalWrite(12, LOW);
        led1.off();
        delay(5000);               //tempo para o solo absorver a água   
  }
  
  Blynk.virtualWrite(V1,analogRead(pinSensorA)); //Mostrará, no monitor LCD do app, os dados do sensor analógico do solo

  if (analogRead(pinSensorA) >= 700 && analogRead(pinSensorA) < 1023)
  {
    Blynk.virtualWrite(V0, "Seco");
  }

  if (analogRead(pinSensorA) > 0 && analogRead(pinSensorA) < 499)
  {
    Blynk.virtualWrite(V0, "Úmido");
  }

   if (analogRead(pinSensorA) >= 500 && analogRead(pinSensorA) < 699)
  {
    Blynk.virtualWrite(V0, "Moderado");
  }
}

  BLYNK_WRITE(V7) //Botão que fará o acionamento manual do relé/válvula pelo usuário do app
{
    int pinValue = param.asInt();
     
  if (pinValue == 1)         
  {
    digitalWrite(12, HIGH);
    led1.on();
  }
  else
  {
    digitalWrite(12, LOW);
    led1.off();
  } 
} 

void loop()
{
  Blynk.run();
  
  if (analogRead(pinSensorA) > 700 && analogRead(pinSensorA) < 1023)
  {
    Blynk.notify("O solo está seco, recomenda-se irrigação"); //Notificação no celular do usuário 
    delay(5000);                                              //Tempo para receber uma nova notificação
  }
  timer.run();
}

```
## Resultados 

<p>
            Com a portabilidade para o Blynk pronta, foi iniciado a etapa de desenvolvimento do layout do aplicativo. A fim de exibir as informações analisadas pelos sensores da forma mais simples e compreensível possível, foram utilizados:

* Painel LCD: para exibir o status atual do solo (que é dividido em seco, moderado e úmido) e o quanto ele está úmido (representado por valores de 0 a 1023);

* Gráfico em linhas: utilizado para acompanhar, ao longo do tempo, a temperatura, a umidade relativa do ar e a umidade do solo. Sendo possível traçar dados de até um ano de análises;

* Monitores de valores numéricos: responsáveis por exibir os valores de temperatura e umidade relativa do ar do ambiente em que se encontra o projeto;

* LED: indicativo visual do funcionamento da válvula tanto no seu modo automático, quanto no manual;

* Botão: fará o acionamento manual da válvula;

* Bluetooth: botão que permitirá o usuário conectar-se com o módulo HC-05;

* Notificação: extensão que notificará o usuário quando o solo estiver severamente seco.

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/layout%201.jpg)

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/layout%202.jpg)

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/acionamento%20manual.jpg)

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/notifica%C3%A7%C3%A3o.jpg)

<p>
            A seguir, há um código QR que permitirá a clonagem do projeto desenvolvido para que possa ser reproduzido em qualquer outro aparelho.
</p>

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/clonagem%20do%20projeto.jpg)

# Vídeo de apresentação do Projeto

[![Watch the video](https://i.imgur.com/vKb2F1B.png)](https://youtu.be/vt5fpE0bzSY)

# Dificuldades

<p>
      Em um primeiro momento, começar a programar o Arduino foi uma tarefa bem estressante visto que nunca tive contato com esse tipo de tecnologia antes. Seguindo a tutoriais na internet, consegui remediar minha falta de experiência e contornei uma série de problemas, tais como o serial configurado com o BAUD equivocado, a biblioteca do DHT 11 não funcionando propriamente (o que me levou a testar três tipos de bibliotecas), o reservatório de água utilizado não ter pressão o suficiente para conduzir a coluna d'água até a válvula, erros na liguagem de programação (pois houve um momento em que os dados dos sensores não eram atualizados devido uma função escrita equivocadamente) e um comportamento instável do módulo bluetooth HC-05 (que apresentava uma série de problemas de conectividade com o aplicativo desenvolvido no Blynk).
</p>

<p>
    No que tangencia o módulo bluetooth, vale acrescentar que, para fosse feita a conexão com o celular, foi necessária a substituição das portas RX e TX do componente que, inicialmente, encontravam-se respectivamente nas portas 1 e 0 do Arduino MEGA. Nesta configuração, o módulo não era reconhecido pelo aplicativo visto que os pinos 0 e 1 são usados para o UART de programação integrada. Desta forma, recomenda-se evitar usá-los se for utilizado o Blynk (na aplicação Serial Bluetooth, não foi detectado instabilidade em nenhum dos pinos testados). Com isso, foi feito o uso do SoftwareSerial em pinos alternativos (11 e 10) e, assim, o módulo funcionou como esperado.        
</p>

# Melhorias

<p>
      No que se refere a melhorias do projeto desenvolvido, eu recomendaria a utilização de sensores mais precisos, como o DHT 21 (que possui uma faixa de operação maior que o DHT 11), o HD-38 (sensor de umidade do solo mais preciso que o utilizado neste projeto), a substituição do módulo bluetooth por um módulo WI-FI (a fim de contornar as limitações da conexão bluetooth), a adição de um sensor de luminosidade (para conferir se a planta está recebendo luz solar o suficiente durante as análises) e a substituição da válvula solenóide por uma bomba d'água ou similar.
</p>

# Referências Bibliograficas

https://examples.blynk.cc/?board=Arduino%20Mega%202560&shield=HC05%20or%20HC06&example=More%2FDHT11 - Exemplo para implementação do sensor DHT 11 e do módulo bluetooth HC-05 usando o Blynk;

https://www.hackster.io/shibinkp202/relay-control-using-nodemcu-through-blynk-app-b3750c - Comando para controlar o relé utilizando o Blynk

https://www.filipeflop.com/blog/monitore-sua-planta-usando-arduino/ - Código utilizado como referência para implementação do projeto

https://www.robocore.net/tutoriais/configurando-bluetooth-hc-05-via-arduino 

https://create.arduino.cc/projecthub/officine/monitor-and-control-your-irrigation-system-with-a-mobile-app-0607bf

https://community.blynk.cc/t/login-timeout-with-blutooth-module/19306/2
