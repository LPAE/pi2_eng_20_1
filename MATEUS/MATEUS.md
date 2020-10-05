# Sistema de Irrigação automatizado

## **Concepção do Projeto**
A agricultura 4.0 é um termo derivado da indústria 4.0 que se refere a aplicação de tecnologia de ponta na produção agrícola. Tal tecnologia proporciona inúmeras vantagens ambientais, tais como, menor utilização de água na irrigação ou insumos de adubagem no solo (RIBEIRO, 2018). Para que o pequeno produtor e pessoas que não tem acesso a uma casa com espaço para fazer uma horta existe a possibilidade de plantar especiarias, hortaliças e saladas em potes. Em virtude da necessidade de que o usuário geralmente tem de sair de casa por alguns dias e precisa deixar as plantas sozinhas o projeto atual apresenta a solução de tal forma que a irrigação que é algo que precisa ser feito com certa periodicidade será feita de forma automatizada.
Para que as necessidades do usuário sejam atendidas o projeto contará com dois sensores, um para informar as condições climáticas e umidade relativa do ar, e o outro para medir a umidade do solo. Ou seja os sensores realizarão a coleta de informações do ambiente e da planta para que sejam enviadas para o microcontrolador que será configurado de tal modo que toda vez que o solo precisar de água será feito o acionamento de uma válvula para que a água chegue na planta. Tais informações coletadas serão disponibilizadas para o usuário na tela do smartphone.

_________________________________________________________________________________________________________________________________________________________________________________



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
![Figura 5](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/RELE%205V.jpg)

**Figura 5 - Relé**



![Figura 6]()

**Figura 6 - Válvula Solenóide** 



A válvula solenóide funciona em conjunto com o relé, quando o relé interromper a passagem de corrente a válvula é desacionada.
![Figura 7](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/DESATIVANDO%20VALUVLA.png)

**Figura 7 - Desativando a Válvula**



Quando o relé permitir a passagem de corrente a válvula é acionada
![Figura 8](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/ACIONAMENTO%20VALVULA.png)

**Figura 8 - Válvula sendo acionada**



Para exemplificar todo o processo apresentado acima tem-se o diagrama de blocos a seguir: 
![Figura 9]()

**Figura 9 - Diagram de blocos**



Bem como para exemplificar as conexões dos sensores no arduino foi desenvolvido a planta eletrônica:
![Figura 10]()

**Figura 10 - Planta eletrônica (FRITZING)**



A alface foi a planta escolhida para o monitoramento, de acordo com Santos (2015)  essa verdura necessita de bastante incidência de sol e irrigação abundante.
![Figura 11]()

**Figura 11 - Planta monitorada**



_________________________________________________________________________________________________________________________________________________________________________________
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
   Serial.begin(9600);   //velocida de leitura do serial
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








