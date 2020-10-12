# Regador automático de plantas com sistema de reconhecimento de umidade do solo.

Em meados do século passado uma grande dificuldade em que os agricultores ou até mesmo jardineiros tinham era de saber a quantidade de água o suficiente para regar uma planta. O teste feito por eles era através de tocar o solo e verificar se o mesmo está umido, caso não estivesse seria hora de regar novamente. Porém como controlar a quantidade de água necessária. A frequência de regas variam segundo a espécie, a quantidade de insolação, vento, e a estação do ano.  Algumas plantas podem até morrer por ter seu solo encharcado, isto acontece porque algumas plantas quando são regadas demais não conseguem reverter a absorção de água, e ocasionando a dificuldade da passagem de oxigênio das raizes causando assim a sua morte. Lugares com muito vento precisam uma frequência maior de rega, para deixar as raizes mais fortes.

Este projeto será possível verificar a umidade do solo, através de um sensor de umidade do solo, onde um solo seco seria mais resistivo que um solo molhado pois, a água é um excelente condutor de corrente elétrica. O sensor funciona da seguinte forma, quando o solo está seco a saida do sensor ficará no estado alto, e quando úmido fica no estado de baixo. 
Para visualizar o nível de umidade vindo da leitura do sensor, será utilizado um display LCD, e será possível também verificar o nivel e umidade do solo através de um smartphone com S. O. Android.

O protótipo também contará com uma válvula solenóide e um relé para chaveamento da mesma. O sensor de umidade será conectado no solo, onde o sistema fará a leitura do mesmo, verificando se haverá necessidade de fazer a irrigação ou não.

# Tecnologias presentes no projeto.

Neste tópico será detalhado de forma simples quais tencologias foram utilizadas para construção do projeto:

1 - Arduino Mega 2560 R3
Placa utilizada para programação, parte lógica do projeto. A placa possui 54 entradas/saídas digitais e 16 entradas analógicas mais pinos de TX e RX, SCL e SDA.
Liguagens utilizada C e C++.

2 - Módulo Bluetooth RS232 HC-05
Placa utilizada para parte fazer de comunicação serial entre o celular android com as informações da porta serial da placa do arduino Mega 2560 R3.

3 - Sensor de umidade do solo
PLaca utilizada para verificar a umidade do solo. A saída do sensor fica em estado alto quando o solo apresenta seco , e a saída do sensor fica em estado baixo quando o solo está molhado. A corrente do solo passa por este sensor que utiliza duas pontas de prova. A resistência elétrica resultante basea-se a sua leitura. Quanto mais o solo estiver enxarcado , menor é a resistência do mesmo o que facilita a condução entre as pontas de prova. O solo estando seco, a condutividade é baixa.

4 - Sensor de Umidade e Temperatura DHT11
O DHT11 é um sensor de temperatura e umidade muito utilizado para projetos de arduino, capaz de fazer leituras de temperaturas entre 0 a 50 graus celsius e umidade de 20 a 90%. Neste projeto estas informações são enviadas para uma tela de LCD e um aplicativo.

5 - Módulo Relé 5V 1 canal
Compatível com arduino. Lâmpadas, motores, eletrodomésticos e outros equipamentos pode ser controlado utilizando apenas um pino de controle do Módulo Relé 5V 1 Canal , isto porque o circuito alimentado pelo reé fica isolado do microcontrolador. Neste projeto a função desta placa é fazer o chaveamento do circuito de ativação da válvulva solenóide.

6 - Válula Solenóide
Muito utilizada juntamente com microcontroladores para sistema de irrigação ou mesmo para encher caixas d’água, especificações 12V 180° (¾ x ¾). Neste projeto será utilizada para chavear a entrada de água, em conjunto com o relé.

7 - Módulo Serial I2C para Display LCD Arduino
Este módulo, faz com que você controle um display LCD, não importando se é 16×2 ou 20×4, a vantagem é que é utilizado apenas dois pinos do Arduino (SDA) e o (SCL). Neste projeto foi utilizado a comunicação i2c entre arduino e a placa. Todas as informações do arduino estarão presentes no LCD.

# Design do Projeto

O Design do projeto serve para se ter uma visão espacial do projeto, se preocupando com o tamanho e ligações das placas envolvidas, afim de otimizar o tempo na hora da montagem de fato e diminuir maiores chances de erro de conexão. Segue abaixo de como ficaram as ligações do projeto proposto.


![alt text](https://github.com/LPAE/pi2_eng_20_1/blob/master/MARCOS/design.jpg)

# Diagrama de Blocos

O diagrama de blocos diferente do design mostra como o projeto é subdividido em camadas, afim de melhor entende-lo. Ao invés de o projeto ser todo um bloco só ele é dividido assim como em uma empresa, no qual se divide os setores.














