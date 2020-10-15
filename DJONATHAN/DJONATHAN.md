## **Desenvolvimento de sistema de irrigação microcontrolado**
```
Instituto Federal de Santa Catarina - Campus Florianópolis
Bacharelado em Engenharia Eletrônica - Projeto Integrador II - Semestre 2020.1
Professores: Luiz Azevedo & Fernando Miranda
Aluno: Djonathan Hinckel Machado
```
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

#### **Sistema de Irrigação**

As imagens abaixo evidenciam como foi feita a montagem do sistema, mostrando as conexões entre o módulo Arduino e os sensores e também, o sistema de vazão de água e de irrigação por gotejamento que foram criados. O modelo de irrigação por gotejamento foi escolhido para tornar mais precisa a leitura de umidade do solo, pelo fato de ser mais lenta e tornar propícia a melhor distribuição da água pelo solo a ser irrigado.

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Op1.PNG)
![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Op2.png)
![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Op4.png)
![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Op3.png)
![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Op5.png)
![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Op6.png)

#### **Aplicativo Android**

Para que haja o funcionamento do aplicativo desenvolvido, é necessário um smartphone com o aplicativo “AI Companion” instalado, que auxiliará na sincronização e envio do que foi criado na plataforma online ao telefone. Após essa conexão (que pode ser via QR Code). O programa é renderizado e inicia seu funcionamento no Android.

A imagem a seguir evidencia como é o funcionamento e demonstra o layout de nosso aplicativo programado:

![](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/App1.PNG)

```

Na primeira parte temos o início do aplicativo já visto anteriormente, acima da seta temos o módulo HC05 identificado na tela do Smartphone e, após a seta, o aplicativo já funcionando com alguns dados de leitura já obtidos após o clique no botão de "atualizar leitura".

```

### **Considerações finais e Conclusão do projeto**

#### **Sobre o método**

O método do desenvolvimento abordado, denominado CDIO, configura-se como um bom e eficiente método por ser dividido em etapas que caracterizam-se por ser essenciais para o desenvolvimento de um bom projeto. A execução sequencial do projeto também auxilia na organização geral diante do fato de que torna-se fácil apontar as principais dificuldades e problemas que o desenvolvimento irá apresentar.

#### **Percepções Pessoais**

Tratando-se especificamente da montagem e programação deste projeto, apenas há a citar, como dificuldade, a construção do sistema de irrigação em si (desconsiderando-se a parte eletrônica) e a análise do solo a ser trabalhado, para verificar qual o estado dele em que pode ser considerada a necessidade de irrigação. Este projeto agrega muito conhecimento a ser adquirido, tanto na parte eletrônica com o entendimento de cada módulo e de cada sensor, além com o próprio microcontrolador Arduino, como na parte de se criar um sistema eficiente de irrigação, que estimula um raciocínio além do conhecimento que normalmente é adquirido no curso de Engenharia Eletrônica. Tornou-se um grande aprendizado sobre a profissão de Engenheiro, em geral e sobre seu importante papel.

#### **Panorama Geral**

Dentro da evolução atual, é possível visualizar a incrível gama de situações em que a tecnologia pode ser aplicada. O termo IoT (Internet of Things) evidencia isso ainda mais ao se fazer uma conexão com elementos do cotidiano que podem, cada vez mais, ser controlados sem necessidade de interferência humana. O projeto desenvolvido é um reflexo disso, podendo ser especificado para ser utilizado tanto em situação doméstica, como o realizado, como em situações comerciais, ao ampliar-se para controlar uma plantação inteira, por exemplo. Este projeto também pode ser visto como uma introdução ao tema recente da Agricultura 4.0 que agrega-se a IoT como um dos termos mais importantes no estudo do avanço das tecnologias e de suas aplicações em desenvolvimento no mundo.

