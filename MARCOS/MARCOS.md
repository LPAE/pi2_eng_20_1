# Regador automático de plantas com sistema de reconhecimento de umidade do solo.

Em meados do século passado uma grande dificuldade em que os agricultores ou até mesmo jardineiros tinham era de saber a quantidade de água o suficiente para regar uma planta. O teste feito por eles era através de tocar o solo e verificar se o mesmo encontrava-se umido, caso não estivesse seria hora de regar novamente. Porém como controlar a quantidade de água necessária. A frequência de regas variam segundo a espécie, a quantidade de insolação, vento, e a estação do ano.  Algumas plantas podem até morrer por ter seu solo encharcado, isto acontece porque algumas plantas quando são regadas demais não conseguem reverter a absorção de água, e ocasionando a dificuldade da passagem de oxigênio das raizes causando assim a sua morte. Lugares com muito vento precisam uma frequência maior de rega, para deixar as raizes mais fortes.

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

O diagrama de blocos diferente do design mostra como o projeto é subdividido, afim de melhor entendê-lo. As divisões são conforme suas especialidades assim como em uma empresa, no qual se divide em setores. Segue abaixo o diagrama de blocos deste projeto.

![alt text](https://github.com/LPAE/pi2_eng_20_1/blob/master/MARCOS/diagrama%20de%20blocos.jpg)

# Fluxograma
 
Como o próprio nome já diz é um tipo de diagrama, ou uma representação esquemática de um processo ou algoritmo. Nele é mostrado a sequência operacional de um algoritmo infomando todas as situações em que o projeto irá se comportar. Abaixo mostra o fluxograma do código implementado neste projeto. 

![alt text](https://github.com/LPAE/pi2_eng_20_1/blob/master/MARCOS/Fluxograma.jpg)

# Algoritmo

O algoritmo nada mais é que um conjunto de códigos que tem a finalidade de resolver um problema , ou realizar uma tarefa. Neste projeto utilizamos o software próprio do arduino. Segue abaixo todo o codigo implementado na linguagem C++.

![alt text](https://github.com/LPAE/pi2_eng_20_1/blob/master/MARCOS/algoritmo.jpg)


# Implementação

Partiremos agora para a parte prática do projeto, onde analisaremos se o protótipo irá se comportar de forma adequada e esperada. É esperado que o sistema através de um sensor verifique a umidade do solo de uma planta, esta umidade é recebida no valor de 0 até 1024, onde no código é transformada em porcentagem. A porcentagem deverá ser menor ou igual a 45 para que o microcontrolador envie um pulso de 5V para chavear um relé acionando o circuito de 12V em conjunto com a válvula solenóide e assim deixando a água passar. Caso a porcentagem seja maior que 45, a agua deverá ser cessada e a planta parará de ser regada. Este projeto também contará com um display LCD que receberá todas as informações do arduino através da comunicação i2c, o microcontrolador também enviará estes mesmos dados para um aplicativo de celular via UART, por comunicação serial. Outro sensor implementado foi um DHT11, sensor de temperatura e umidade do ambiente, o mesmo também enviará dados para o arduino que enviará os dados novamente para um LCD e para a tela do celular como foi mencionado. Estes valores são atualizado a cada 2 segundos. A comunicação por bluetooth acontece graças a placa HC-05.

Abaixo Segue a foto do protótipo já pronto, logo mais terá um vídeo explicativo.

![alt text](https://github.com/LPAE/pi2_eng_20_1/blob/master/MARCOS/Foto%20de%20todo%20o%20projeto.jpeg)

Segue o vídeo explicativo
![watch the video](https://github.com/LPAE/pi2_eng_20_1/blob/master/MARCOS/Video%20Explicativo%20do%20projeto.mp4)

# Resultados

Em meio a pandemia causada pelo coronavirus que estamos passando e pela dificuldade de acesso aos materiais, o projeto teve um resultado satisfatório, isso porque teve o comportamento esperado, sem gerar nenhum tipo de problema. Tentamos nos preocupar com a água, por isso foi utilizado um pote de sorvete que é feito de plastico justamente para que caso respingasse água não comprometesse o circuito. Tivemos que deixar a matriz de contato fora, por não caber no nosso "case". O ideal seria fazer uma placa de circuito impresso de fato, para que possamos eliminar de fato o uso da matriz de contato.   


















