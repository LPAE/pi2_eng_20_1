# Projeto Integrador II - 2020/1

Instituto Federal de Santa Catarina

Departamento Acadêmico de Eletrônica

Professores: Fernando Pedro Henrique de Miranda e Luiz Alberto de Azevedo

Aluno: Guilherme da Costa Franco - guilherme3379@gmail.com
  
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

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/arduino%20mega.png)

2. **Válvula Solenóide de 12V NC**

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/v%C3%A1lvula.png)

3. **Módulo relé de 5V**

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/rel%C3%A9.jpg)

4. **Sensor de umidade do solo higrômetro**

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/sensor%20umidade%20do%20solo.jpg)

5. **Sensor DHT11**

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/dht%2011.jpg)

6. **Módulo Bluetooth HC-05**

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/hc%2005.png)

# Design do Projeto <h2>
<p>
  Afim de facilitar a compreensão do funcionamento do projeto, antes de partir para experimentações práticas, foram realizadas a construção de uma Planta Eletrônica, explicitada pela Figura 1, e a elaboração de um diagrama de blocos, Figura 2, para tanto criar uma visão espacial do projeto, quanto para deixar evidente e inteligível todas as etapas de processos e funções dos componentes envolvidos.
</p>
  
![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/projeto%20fritzing.png)
Figura 1

Obs: as pilhas estão representando fontes de 9V, para a alimentação do Arduino, e de 12V, para a alimentação da válvula solenóide, devido a ausência destes componentes na biblioteca do Fritzing.

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/GUILHERME/Fotos%20PI/diagrama%20de%20bloco.png)
Figura 2

## Implementação

<pre>

#include <dht.h>
#define pinSensorA A0 //sensor ANALÓGICO do solo
#define pinSensorD 8  //sensor DIGITAL do solo
#define dht_pin 2     //pino de sinal do DHT-11

//===============================================================================

bool leituraSensor;
bool leituraAnterior;

dht  my_dht;

float temperatura;
float umidade;
//===============================================================================

void setup() 
{
  pinMode(pinSensorA, INPUT); //Sensor de umidade do solo
  pinMode(12, OUTPUT);        //Atuador -> solenóide
  Serial.begin(9600);
  Serial.println("Início da análise");
}

void loop() 
{
//===============================================================================
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
//===============================================================================  
  Serial.print("Status do sensor digital: ");
  
  if (digitalRead(pinSensorD)) 
  {
     Serial.println("POUCA UMIDADE");
  } 
  if (!digitalRead(pinSensorD)) 
  {
     Serial.println("ÚMIDO");
  }
//===============================================================================
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
//===============================================================================  
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
//===============================================================================
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
  
  if (analogRead(pinSensorA) > 0 && analogRead(pinSensorA) < 500)
  {
     Serial.println("O solo se encontra suficientemente úmido");
  } 
  
  if (analogRead(pinSensorA) > 500 && analogRead(pinSensorA) < 700)
  {
     Serial.println("O solo se encontra razoaveltemente úmido");
  } 
  
  if (analogRead(pinSensorA) > 700 && analogRead(pinSensorA) < 1023)
  {
     Serial.println("O solo se encontra seco, recomenda-se irrigação");
     
  }         
     
} 
//===============================================================================

</pre>
