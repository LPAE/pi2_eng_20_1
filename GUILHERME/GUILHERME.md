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
2. **Válvula Solenóide de 12V NC**
3. **Módulo relé de 5V**
4. **Sensor de umidade do solo higrômetro**
5. **Sensor DHT11**
6. **Módulo Bluetooth HC-05**

# Design do Projeto <h2>
<p>
  Afim de facilitar a compreensão do funcionamento do projeto, antes de partir para experimentações práticas, foram realizadas a construção de uma Planta Eletrônica, explicitada pela Figura 1, e a elaboração de um diagrama de blocos, Figura 2, para tanto criar uma visão espacial do projeto, quanto para deixar evidente e inteligível todas as etapas de processos e funções dos componentes envolvidos.
</p>

