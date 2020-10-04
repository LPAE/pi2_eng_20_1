# Sistema de Irrigação automatizado

## **Concepção do Projeto**
A agricultura 4.0 é um termo derivado da indústria 4.0 que se refere a aplicação de tecnologia de ponta na produção agrícola. Tal tecnologia proporciona inúmeras vantagens ambientais, tais como, menor utilização de água na irrigação ou insumos de adubagem no solo (RIBEIRO, 2018). Para que o pequeno produtor e pessoas que não tem acesso a uma casa com espaço para fazer uma horta existe a possibilidade de plantar especiarias, hortaliças e saladas em potes. Em virtude da necessidade de que o usuário geralmente tem de sair de casa por alguns dias e precisa deixar as plantas sozinhas o projeto atual apresenta a solução de tal forma que a irrigação que é algo que precisa ser feito com certa periodicidade será feita de forma automatizada.
Para que as necessidades do usuário sejam atendidas o projeto contará com dois sensores, um para informar as condições climáticas e umidade relativa do ar, e o outro para medir a umidade do solo. Ou seja os sensores realizarão a coleta de informações do ambiente e da planta para que sejam enviadas para o microcontrolador que será configurado de tal modo que toda vez que o solo precisar de água será feito o acionamento de uma válvula para que a água chegue na planta. Tais informações coletadas serão disponibilizadas para o usuário na tela do smartphone.



## **Design** 
Antes de tudo foi necessário escolher o microcontrolador para receber os dados e realizar comandos, para tal função foi optado pelo arduino mega 2560 que fornece duas saídas de tensão uma de 3.3V e outra de 5V DC.
![Figura 1](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/1046_1_H.png)

**Figura 1 - Arduino Mega 2560**

Para efetuar o monitoramento das condições que a planta está exposta  utilizou-se sensores que realizarão a coleta das informações do solo e do ambiente. Sendo assim, para informar as condições do ambiente foi escolhido o sensor DHT11, além disso para recolher os dados do solo foi selecionado o higrômetro. 
O sensor de temperatura e umidade DHT11 conta com uma saída digital, ainda conta com um sensor resistivo de componentes úmidos. Opera com uma tensão entre 3.3V e 5V DC, sendo que a faixa de medição de umidade é de 20% a 90%, além disso, apresenta uma faixa de medição de temperatura de 0°C a 50°C.
![Figura 2](https://github.com/LPAE/pi2_eng_20_1/blob/master/MATEUS/DHT11-Digital-Relative-Humidity-Temperature-Sensor-Module-ROBU.IN_-2.jpg)

**Figura 2 - Sensor de umidade e temperatura DHT11**






