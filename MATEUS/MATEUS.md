

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/if.jpg)

Departamento Acadêmico de Eletrônica

Professores: 
* Fernando Miranda - <fernando.miranda@ifsc.edu.br>
* Luís Azevedo - <azevedo@ifsc.edu.br>

Aluno: 
* Mateus Fontana Tatim - mateus.f02@aluno.ifsc.edu.br
***
# Projeto Integrador II - 2020/1
# Sistema de Irrigação automatizado

## **Concepção do Projeto**
A agricultura 4.0 é um termo derivado da indústria 4.0 que se refere a aplicação de tecnologia de ponta na produção agrícola. Tal tecnologia proporciona inúmeras vantagens ambientais, tais como, menor utilização de água na irrigação ou insumos de adubagem no solo (RIBEIRO, 2018). Para que o pequeno produtor e pessoas que não tem acesso a uma casa com espaço para fazer uma horta existe a possibilidade de plantar especiarias, hortaliças e saladas em potes. Em virtude da necessidade de que o usuário geralmente tem de sair de casa por alguns dias e precisa deixar as plantas sozinhas o projeto atual apresenta a solução de tal forma que a irrigação que é algo que precisa ser feito com certa periodicidade será feita de forma automatizada.
Para que as necessidades do usuário sejam atendidas o projeto contará com dois sensores, um para informar as condições climáticas e umidade relativa do ar, e o outro para medir a umidade do solo. Ou seja os sensores realizarão a coleta de informações do ambiente e da planta para que sejam enviadas para o microcontrolador que será configurado de tal modo que toda vez que o solo precisar de água será feito o acionamento de uma válvula para que a água chegue na planta. Tais informações coletadas serão disponibilizadas para o usuário na tela do smartphone.

***

## DESIGN
Antes de tudo foi necessário escolher o microcontrolador para receber os dados e realizar comandos, para tal função foi optado pelo arduino mega 2560 que fornece duas saídas de tensão uma de 3.3V e outra de 5V DC.
![Figura 1](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/1046_1_H.png)

**Figura 1 - Arduino Mega 2560**





Para efetuar o monitoramento das condições que a planta está exposta  utilizou-se sensores que realizarão a coleta das informações do solo e do ambiente. Sendo assim, para informar as condições do ambiente foi escolhido o sensor DHT11, além disso para recolher os dados do solo foi selecionado o higrômetro. 
O sensor de temperatura e umidade DHT11 conta com uma saída digital, ainda conta com um sensor resistivo de componentes úmidos. Opera com uma tensão entre 3.3V e 5V DC, sendo que a faixa de medição de umidade é de 20% a 90%, além disso, apresenta uma faixa de medição de temperatura de 0°C a 50°C.
![Figura 2](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/DHT11-Digital-Relative-Humidity-Temperature-Sensor-Module-ROBU.IN_-2.jpg)

**Figura 2 - Sensor de umidade e temperatura DHT11**



O sensor de umidade do solo (higrômetro) trabalha com uma tensão de operação entre 3.3V e 5V DC. Para coletar os dados do solo existem duas possibilidades, uma com operação analógica e outra digital.
![Figura 3](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/9SS19-1.jpg)

**Figura 3 - Sensor de umidade do solo (Higrometro)**



Além das coletas de dados o projeto irá disponibilizar as informações para o usuário no smartphone, para tal aplicação o HC-05 módulo bluetooth foi escolhido, pois existe uma fácil comunicação com o microcontrolador arduino. O dispositivo opera com uma tensão de alimentação entre 3V e 5V DC, os pinos rx e tx que são responsáveis pela troca de dados operam com uma tensão de 3.3V.
![Figura 4](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/02-30.png)

**Figura 4 - Módulo bluetooth HC-05**



Após a coleta de dados o arduino será programado para armazená-los e analisar se a planta precisa de irrigação, de tal modo, que se o solo estiver seco o arduino ativará o relé que liberará a válvula solenóide para o fluxo de água chegar na planta.
O relé trabalha na região de 5V de tensão de alimentação e tem uma saída digital.
![Figura 5](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/rele%205v%20dc.png)

**Figura 5 - Relé**



![Figura 6](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/valv%20s.png)

**Figura 6 - Válvula Solenóide** 



A válvula solenóide funciona em conjunto com o relé, quando o relé interromper a passagem de corrente a válvula é desacionada.
![Figura 7](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/DESATIVANDO%20VALUVLA.png)

**Figura 7 - Desativando a Válvula**



Quando o relé permitir a passagem de corrente a válvula é acionada
![Figura 8](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/ACIONAMENTO%20VALVULA.png)

**Figura 8 - Válvula sendo acionada**



Para exemplificar todo o processo apresentado acima tem-se o diagrama de blocos a seguir: 
![Figura 9](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/Diagrama%20projeto%20(1).png)

**Figura 9 - Diagrama de blocos**



Bem como para exemplificar as conexões dos sensores no arduino foi desenvolvido a planta eletrônica:
![Figura 10](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/Planta%20img.png)

**Figura 10 - Planta eletrônica (FRITZING)**



A alface foi a planta escolhida para o monitoramento, de acordo com  Wien (1997), a média de temperatura onde a alface se desenvolve bem é de 18ºC, ponderando uma faixa entre 7ºC e 24ºC, tais valores de temperatura devem estar em conjunto com umidade relativa do ar entre 60 e 70%.
![Figura 11](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/WhatsApp%20Image%202020-10-06%20at%2017.28.48.jpeg)

**Figura 11 - Planta monitorada**


***
## IMPLEMENTAÇÃO
Após definir qual o microcontrolador e quais os sensores serão utilizados e adquiri-los passamos para a fase de testes. Sendo assim foi testado individualmente cada sensor para certificar que o mesmo está em perfeitas condições de funcionamento. Para o teste foi pesquisado códigos ide para arduino. Primeiramente o DHT11:

```c++
// --- Biblioteca Auxiliar ---
#include <dht.h>   //biblioteca do sensor de umidade e temperatura
// ===============================================================================
// --- Mapeamento de Hardware ---
#define    dht_pin    5   //pino de sinal do dht11 ligado no digital 5
// ===============================================================================
// --- Declaração de Objetos ---
dht   my_dht;   //objeto para o sensor
// ===============================================================================
// --- Variáveis Globais ---
int    temperatura = 0x00,   //armazena a temperatura em inteiro
       umidade     = 0x00;   //armazena a umidade em inteiro
// ===============================================================================
// --- Configurações Iniciais ---
void setup() 
{
   Serial.begin(9600);   //velocidade de leitura do serial
} //end setup
// ===============================================================================
// --- Loop Infinito ---
void loop() 
{
   my_dht.read11(dht_pin);
   temperatura = my_dht.temperature; // le a temperatura do sensor
   umidade     = my_dht.humidity;   // le a umidade do sensor
   Serial.print(temperatura);      //  apresenta na tela serial a temperatura
   Serial.print(" ");
   Serial.println(umidade);      // apresenta na tela serial a umidade
   delay(1000);                 // delay de 1s para refazer a leitura
} //end loop
```
OBS: para poder utilizar esse código foi necessário a biblioteca externa dht.h.

No sensor de temperatura e umidade DHT11 existe a possibilidade de informar a umidade e a temperatura em até duas casas decimais porém deixam a medida muito oscilante. Portanto foi escolhido não informar nenhuma casa decimal apenas o número inteiro.



Na sequência foi testado o sensor de umidade do solo. Para resultados mais precisos foi utilizado a saída analógica A0 e realizado alguns experimentos para definir quando o solo estará precisando de irrigação. O sensor mede de 0 a 1024, sendo 0 o indíce que aponta a maior umidade.

A tabela a seguir mostra os parametros apresentados pelo higrometro após irrigação, de forma que após molhar o solo foi controlado o tempo e observado quando a planta precisaria  ser irrigada novamente e assim sucessiavamente durante os 5 testes.

DIA | HORA | A0  
---|---|---
22/09/2020 | 16:40 | 166
23/09/2020 | 16:40 | 310
23/09/2020 | 16:40 | 159
24/09/2020 | 16:40 | 312
24/09/2020 | 16:40 | 178
25/09/2020 | 16:40 | 320
25/09/2020 | 16:40 | 160
26/09/2020 | 16:40 | 300
26/09/2020 | 16:40 | 165
27/09/2020 | 16:40 | 299


Fazendo a media das medidas encontradas têm-se: media = (310 + 312 + 320 + 300 + 299)/5

media = 308,2. 

Arredondando definiu-se que toda vez que o sensor captar 310 a válvula será acionada para irrigar o solo.
```c++
#define pinSensorA A0

void setup() {
  pinMode(pinSensorA, INPUT);
  Serial.begin(9600);
}

void loop() {

  Serial.print("  Analogico:");
  Serial.print(analogRead(pinSensorA)); 
  Serial.print("  ");

  Serial.print("  Atuador:");
  if (analogRead(pinSensorA) > 310) {
     Serial.println("SOLENOIDE LIGADO");
   
  } else {
    Serial.println("SOLENOIDE DESLIGADO");
 
  }
}
```

HC-05 e bluetooth spp
Para apresentar as informações do serial do arduino foi utilizado o aplicativo bluetooth spp da play store que disponibiliza as informações pareadas via bluetooth na tela do smartphone.

```c++
// --- Bibliotecas Auxiliares ---



// ========================================================================================================
// --- Configurações Iniciais ---
void setup()
{
  Serial.begin(9600);

  
} //end setup


// ========================================================================================================
// --- Loop Infinito ---
void loop()
{
  Serial.println("Hello World WR Bluetooth");

  delay(741);
  

  
} //end loop


```

RELÉ
```c++
int rele = 2;

void setup() {
  
  pinMode(rele, OUTPUT); // Configura rele como saida
  Serial.begin(9600); 
}

void loop() {
  digitalWrite(rele, HIGH); // envia sinal alto para rele
  Serial.println("Rele acionado");
  delay(1000);           // 1 segundo
  
  digitalWrite(rele, LOW);  // envia sinal baixo para rele
  Serial.println("Rele desativado");
  delay(1000);           // 1 segundo

}
```
Após todos os testes realizados constatou-se que todos os módulos estavam em perfeitas condições. Sendo assim foi desenvolvido um programa para integrar todos os componentes.
```c++


//--- Biblioteca auxiliar ---
#include <dht.h>  //Biblioteca do DHT11


//===============================================================
//--- Mapeamento de hardware ---
#define dht_pin  24     //pino de sinal digital do dht11 
#define higro A0
#define rele 22

//===============================================================
//--- Declaração de Objetos ---
dht my_dht;   //Objeto para o sensor



//===============================================================
//--- Variáveis Globais ---
int temperatura = 0x00,   // Armazena a temperatura
    umidade     = 0x00;   // Armazena a umidade relativa do ar

    
//===============================================================
//--- Configurações iniciais ---
void setup() {
  Serial.begin(9600);
  Serial.println("Início do programa");
  pinMode(higro, INPUT);
  pinMode(rele, OUTPUT);
  Serial.println("ATENÇÃO");
  Serial.println("A umidade do solo varia de 0 a 1024");
  Serial.println("Quanto mais próximo do zero mais umido o solo está");

}
//===============================================================
//--- loop infinito ---
void loop() {
  my_dht.read11(dht_pin);
  temperatura = my_dht.temperature;
  umidade     = my_dht.humidity;
1  
  Serial.print("\tUmidade do solo=\t");
  Serial.println(analogRead(higro)); 
  Serial.print("\tTemperatura=\t        ");
  Serial.print(temperatura);
  Serial.println("ºC");
  Serial.print("\tUmidade Relativa do ar=\t");
  Serial.print(umidade);
  Serial.println("%");
 
  
  delay(5000);
  if (analogRead(higro)> 310)
  {
  Serial.println("Solo seco ");
  Serial.println("Válvula acionada");
  digitalWrite(rele, HIGH);
  delay(1000);
  }
  else{
  digitalWrite(rele, LOW);
  Serial.println("Solo umido"); 
  Serial.println("Válvula desativada");
  delay(1000);
  }
}
```
***
## OPERACIONALIZAÇÃO

***
## DIFICULDADES
Sem dúvida no projeto existiram algumas dificuldades, vale destacar o local para deixar a planta de modo que fosse exposto ao sol e ao mesmo tempo alcançasse a mangueira da irrigação. Para contorná-lo foi adquirido mais mangueiras para que fosse suficientemente comprida para sair da torneira da lavanderia e chegasse na planta. A alface foi colocada do lado de fora da casa perto de uma janela de modo que fosse bem iluminada pelo sol e ao mesmo tempo protegida da chuva conforme a figura  [numº]. Outro desafio foi onde deixar o protótipo, foi optado por deixa-lo dentro de casa na lavanderia perto da janela, entretanto os sensores precisam estar no mesmo ambiente da planta, sendo assim foi adquirido mais fios para que o sensor de umidade e temperatura DHT11 e o sensor de umidade do solo Higrometro alcancem o local da planta.
***
## RESULTADOS
***
## REFERÊNCIAS


RIBEIRO, Josiana Gonçalves. Agricultura 4.0: desafios à produção de alimentos e inovações tecnológicas. Sienpro, Goiania, ago. 2018. Disponível em: https://files.cercomp.ufg.br/weby/up/1012/o/AGRICULTURA_4.0_DESAFIOS_%C3%80_PRODU%C3%87%C3%83O_DE_ALIMENTOS_E_INOVA%C3%87%C3%95ES_TECNOL%C3%93GICAS.pdf. Acesso em: 30 set. 2020.

WIEN, H. C. (1997) - Lettuce. In: Wien, H. C. The physiology of vegetable crops. New York: Cab International. 

https://www.filipeflop.com/blog/monitore-sua-planta-usando-arduino/  - Modelo para sistema de irrigação automtizado

https://github.com/tinkerall/Tutorial/blob/master/SM0002_RELAY_5V/SM0002_RELAY_5V.ino - Modelo sketch relé

https://mega.nz/file/7BZSQAxa#2n0IW_PF0O01J-AEzzZ40HnBNPlH-m6ikdirVxkyq38 - Modelo sketch DHT11

https://drive.google.com/file/d/1vcQZvi8-_JP-VcpoAb_dvDwUiRI1b4sI/view - Modelo sketch Higrometro3













