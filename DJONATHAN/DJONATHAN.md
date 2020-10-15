## **Desenvolvimento de sistema de irrigação microcontrolado**

### **1 - Concepção do projeto**			

Neste projeto será desenvolvido um sistema de irrigação para plantas de pequeno porte (que posteriormente pode ser ampliado e aplicado em diferentes tipos de planta) que utilizará, dentro de um circuito microcontrolado, medições de algumas grandezas como temperatura ambiente e umidade do ambiente e do solo para determinar a abertura da válvula de um compartimento de água. Além do próprio sistema, será desenvolvido um aplicativo compatível com smartphone/tablet para monitoramento do sistema e das condições atuais da planta.

Abaixo temos, já com as especificações dos módulos e equipamentos, como será conectado e esquematizado o sistema:

![alt text](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Diagrama%20de%20blocos.PNG)

### **2 - Design do projeto**


#### **Componente por componente**
	
O sistema de irrigação microcontrolado possui “blocos” específicos para cada medida. 
Abaixo serão listados todos os componentes do sistema e qual função realizarão dentro do projeto:
	
​	**- Arduino MEGA 2560 R3:** Placa microcontroladora programável que é responsável por comandar todo o sistema, recebendo e enviando dados para os demais módulos.

​	**- Módulo DHT11:** É um sensor responsável pela medição da temperatura e umidade do ar, fatores importantes para determinar se o ambiente é propenso a criação da planta a ser cultivada.

**- Sensor de Umidade do Solo Higrômetro:** Responsável por enviar sinais analógicos e digitais ao Arduino correspondentes a umidade do solo no qual ele está inserido. 

**- Módulo Relé 5v de um canal:** Dispositivo eletromecânico que trabalha com a comutação de contatos. Por ter apenas um canal, ele tem apenas dois estados de chaveamento e irá determinar o envio de corrente ou não a válvula solenóide.

**- Válvula Solenóide 12v:** Responsável pelo controle de fluxo de água, ao receber corrente, ela é aberta, liberando a passagem de água e permitindo a irrigação da planta.
	
**- Módulo HC 05:** Será o módulo Bluetooth responsável por fazer a comunicação entre o sistema de irrigação e um aplicativo de smartphone que irá informar através de uma interface, os dados recolhidos pelos sensores.


#### **Planta Eletrônica do Projeto**

A imagem abaixo demonstra a planta eletrônica feita para este projeto, a qual evidencia como são feitas as ligações de cada módulo e quais pinos do microcontrolador foram selecionados para transmitir os dados recolhidos pelos sensores.

![alt text](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Planta%20-%20Sist_irrig_2020_1.PNG)





#### **Sistema de Irrigação**

O sistema que executa a abertura da válvula ao necessitar-se de irrigação foi implementado no microcontrolador através do código abaixo, que foi construído consultando diversos modos de funcionamento de cada módulo e adaptando-os ao objetivo deste projeto:

``` c++

#include <dht.h>   //biblioteca auxiliar para o sensor de umidade e temperatura

//declaração dos pinos digitais e analógicos utilizados
#define dht_pin 5
#define inDigitalHigro 52
#define inAnalogHigro A0
#define signalRelay 8

dht   my_dht;

//declaração das constantes
bool dSensor;
const int led =13;
const int btpwr=12;
int aSensor,
    temperatura = 0x00,   
    umidade     = 0x00;
char pin[5]="0000";
char modo='1';

// função principal declarando frequência de atuação, 
// determinando os pinos I/O e determinando auxílio visual 
// para pareamento do HC05.
void setup() {
  Serial.begin (9600);
  pinMode (signalRelay, OUTPUT);
  pinMode (inDigitalHigro, INPUT);
  pinMode(led, OUTPUT);
  pinMode(btpwr, OUTPUT);

  digitalWrite(led, HIGH);
  delay(4000);
  digitalWrite(led, LOW);

  digitalWrite(btpwr, HIGH);
  delay(3000);

  digitalWrite(led, HIGH);
}

//função em loop responsável pela leitura constante dos valores obtidos
void loop () {
  my_dht.read11(dht_pin);
  temperatura = my_dht.temperature;
   umidade     = my_dht.humidity;
  dSensor = digitalRead(inDigitalHigro);
  aSensor = analogRead (inAnalogHigro);
  
    if (dSensor == 0){
  Serial.println ("Estado do sistema: fechado");
  }

  else {
   Serial.println ("Estado do sistema: irrigando");
  }
  Serial.print ("Leitura analógica (higrômetro): ");
  Serial.println(aSensor);

  Serial.print ("Temperatura: ");
  Serial.print(temperatura);
  Serial.println("°C");
  
  Serial.print ("Umidade do ar: ");
   Serial.print(umidade);
   Serial.println ("%");
   Serial.println ();
  if (dSensor == 0){
    digitalWrite (signalRelay, LOW);
  }

  else {
   digitalWrite (signalRelay, HIGH);
  }
  if(Serial.available()>0){
   char txt = Serial.read(); 
   Serial.print(txt);
  }
  delay(10000); //Indica que o tempo entre leituras do sistema é de 10 segundos
}
```

#### **Aplicativo Android**

O aplicativo que apresentará uma interface visual para o usuário foi desenvolvido através do MIT App Inventor, um sistema disponível em navegador que é utilizado para criar aplicativos com uma vasta gama de recursos disponíveis que podem realizar diversos tipos de funções. Utilizando-se dos recursos do App Inventor, o aplicativo foi desenvolvido para ter duas etapas: A conexão ao módulo HC-05 e, após tal conexão, a atualização dos dados de leitura. 

**- Layout:** A primeira etapa a ser desenvolvida foi a de criação do layout do aplicativo através da aba “Designer” do sistema. É nesta seção que são inseridos todos os componentes que farão parte do aplicativo, como por exemplo, botões, caixas de texto, o cliente de Bluetooth, etc. Abaixo temos o resultado do layout do aplicativo desenvolvido para este projeto e, ao lado, os componentes utilizados para sua confecção:

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Capturar.png) ![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Components.png)

```

Legenda:

1 - Título especificando o tipo de conexão a ser realizada;

2 - Botão que irá direcionar a conexão Bluetooth com o módulo HC-05;

3 - Título da caixa onde serão exibidas as leituras feitas;

4 - Botão responsável por atualizar as leituras recebidas.

```

**- Blocos (Programação):** Na aba “Blocks” do App Inventor, é possível realizar a programação de todas as etapas do aplicativo. Para facilitar, o próprio sistema já disponibiliza ações que podem ser efetuadas em relação a cada objeto inserido anteriormente na parte de “Designer”. Abaixo temos o código em blocos montado para satisfazer nosso problema:

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Blocks.png)

### **4 - Operacionalização do sistema**



