Desenvolvimento de sistema de irrigação microcontrolado

**1 - Concepção do projeto**			

Neste projeto será desenvolvido um sistema de irrigação para plantas de pequeno porte (que posteriormente pode ser ampliado e aplicado em diferentes tipos de planta) que utilizará, dentro de um circuito microcontrolado, medições de algumas grandezas como temperatura ambiente e umidade do ambiente e do solo para determinar a abertura da válvula de um compartimento de água. Além do próprio sistema, será desenvolvido um aplicativo compatível com smartphone/tablet para monitoramento do sistema e das condições atuais da planta.

**2 - Design do projeto**

**Componente por componente**
	
O sistema de irrigação microcontrolado possui “blocos” específicos para cada medida. 
Abaixo serão listados todos os componentes do sistema e qual função realizarão dentro do projeto:
	
​	**- Arduino MEGA 2560 R3:** Placa microcontroladora programável que é responsável por comandar todo o sistema, recebendo e enviando dados para os demais módulos.

​	**- Módulo DHT11:** É um sensor responsável pela medição da temperatura e umidade do ambiente, fatores importantes para determinar a necessidade de irrigação ou não.

**- Sensor de Umidade do Solo Higrômetro:** Responsável por enviar um sinal analógico ao Arduino referente a umidade do solo no qual ele está depositado. 

**- Módulo Relé 5v de um canal:** Dispositivo eletromecânico que trabalha com a comutação de contatos. Por ter apenas um canal, ele tem apenas dois estados de chaveamento e irá determinar o envio de corrente ou não a válvula solenóide.

**- Válvula Solenóide 12v:** Responsável pelo controle de fluxo de água, ao receber corrente, ela é aberta, liberando a passagem de água e permitindo a irrigação da planta.
	
**- Módulo HC 05:** Será o módulo Bluetooth responsável por fazer a comunicação entre o sistema de irrigação e um aplicativo de smartphone que irá informar através de uma interface, os dados recolhidos pelos sensores.

![alt text](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Diagrama%20de%20blocos.PNG)
![alt text](https://github.com/LPAE/pi2_eng_20_1/blob/master/DJONATHAN/Planta%20-%20Sist_irrig_2020_1.PNG)
