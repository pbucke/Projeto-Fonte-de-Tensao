**Projeto fonte de tensão**

O seguinte projeto, desenvolvido para a disciplina de Eletrônica para computação (SSC180) disponibilizada no ICMC/USP tem como objetivo aplicar os conhecimentos adquiridos em aula para dimensionarmos, projetarmos e montarmos uma fonte de tensão ajustável entre 3V e 12V e com corrente de 100mA.

-----------------------------------------

**Funcionamento:**

O objetivo geral de uma fonte de tensão é realizar a conversão de uma tensão, geralmente 110V ou 220V com corrente alternada (CA), em uma tensão com corrente contínua (CC), para que seja possível alimentar equipamentos que operam com CC.


- Transformador: Transforma a tensão AC de entrada em uma tensão AC mais baixa, facilitando a utilização.
- Retificador: Retifica o formato de onda para obtermos uma tensão DC.
- Filtro: Filtra a tensão transformando-a em CC.
- Regulador: Regula a saída para obtermos uma tensão contínua e ajustável.

----------------------------------------

**Passo a passo:**

O circuito tem entrada AC de 127V provenientes da rede elétrica (tomada) que é levada a um transformador capaz de reduzir a tensão para um valor mais baixo, que pode ser utilizado pelo restante do circuito.

O próximo passo é transformar essa corrente alternada em uma corrente contínua com uma senoide em semi ciclo positivo, isso é feito quando utilizamos uma ponte de diodos completa, que permite a passagem de corrente em apenas parte do ciclo.

O passo seguinte é a instalação de um filtro de onda capaz de “corrigir” a oscilação da tensão, impedindo que a tensão chegue a 0, ou seja, fazendo com que o sinal pulsante se aproxime de uma constante. Tal filtro é constituído por um capacitor que carrega durante o semi ciclo positivo e descarrega durante o semi ciclo negativo.

O último passo é a instalação de um retificador para fazer com que o sinal de saída seja o mais linear o possível. Em fontes mais simples, esse retificador é constituído por um diodo zener polarizado inversamente e um resistor. O diodo zener é um dispositivo com propriedades especiais, como uma tensão de ruptura e uma potência máxima, ambos especificados no datasheet do componente (algo parecido com um manual de especificações). Como no projeto desejamos uma tensão ajustável entre 3V e 12V, utilizamos também um potenciômetro capaz de realizar essa operação.

------------------------------------

**Cálculos:**

A tensão de pico que a fonte de tensão pode atingir pode ser calculada a partir da tensão da fonte multiplicada por √2.

![v_pico](https://user-images.githubusercontent.com/102189064/176514418-557a7ba6-8536-4318-80a4-e0df05f57da8.png)

A razão de operação do transformador pode ser calculada a partir da relação entre a tensão de saída do transistor e a tensão de pico que o circuito pode atingir, conforme a figura abaixo.

![razao_e_vsp](https://user-images.githubusercontent.com/102189064/176514646-5eea7fd1-5190-432f-adde-3ac73f7061e1.png)

Com a tensão entre os polos da ponte de diodos podemos calcular o valor de ripple, que consiste em 10% da tensão que chega ao capacitor, o que nos possibilita de calcular a capacitância necessária em nosso capacitor e a tensão de saída.

![vripple](https://user-images.githubusercontent.com/102189064/176514500-a9950cfa-0fb9-4337-ac77-cad49aa37cc3.png)

Contudo, para calcularmos a capacitância, é necessário sabermos toda a corrente do circuito e, para isso, vamos calculá-las a seguir, com base na faixa de ajuste da fonte (entre 3V e 12v), no diodo zener e no transistor: 

- Características do diodo zener:

![correntes_zener](https://user-images.githubusercontent.com/102189064/176514706-999864b1-7769-479e-a741-2e6d92c6b34a.png)


- Cálculos quando temos 3V na fonte:

![info_pot](https://user-images.githubusercontent.com/102189064/176514793-f48d05af-c5ba-4a26-a964-477bb4de5824.png)


Com isso, escolhermos um potenciômetro de valor comercial 5kΩ

- Fonte com 12V:

![transistoo](https://user-images.githubusercontent.com/102189064/176514903-871e9c7f-f7cb-49dc-ab5f-310216eaa9b9.png)


- Dimensionamento do resistor que acompanha o LED:

![rsm](https://user-images.githubusercontent.com/102189064/176515003-ce3cdb9f-ec5f-4418-87cc-dcc196fbb7da.png)


Com isso escolhemos um resistor de valor comercial de 1kΩ

- Correntes complementares e corrente total:

![correntes](https://user-images.githubusercontent.com/102189064/176515052-0e2fba6b-7f88-4fa7-8e2e-1393120e07df.png)


- Com isso podemos finalmente calcular a capacitância:

![capacitor](https://user-images.githubusercontent.com/102189064/176515105-ca133117-bbe9-41d5-9760-6e6d7ab71940.png)


Com isso, descobrimos que a capacitância mínima deve ser de 462uF, mas escolhemos um capacitor de 680uF por ser de um valor comercial mais comum e facilmente encontrado em lojas de eletrônicos.

-----------------------------------------

**Tabela de referência dos componentes utilizados no projeto**


|**Componente**|**Valor (por unidade)**|**Quantidade**|
| :-: | :-: | :-: |
|Capacitor 680uF|R$ 1,00|1|
|Diodo 1N4007|R$ 0,20|5|
|Diodo Zener 13V|R$ 0,50|1|
|LED vermelho 5mm|R$ 0,50|1|
|Potenciômetro 5kΩ|R$ 7,00|1|
|Resistor 120Ω|R$ 0,07|1|
|Resistor 1KΩ|R$ 0,07|1|
|Resistor 2.2KΩ|R$ 0,07|2|
|Transformador 12/24V|R$ 34,99|1|
|Transistor BC548|R$ 0,50|1|

-----------------------------

**Link para o vídeo explicativo:** https://drive.google.com/file/d/1_NWhUf14gy4CsD5PvgrdcseWQrl45HKv/view?usp=sharing



----------------------------

**Circuito desenvolvido no software EAGLE**

https://tinyurl.com/2m9m5d2la


![circuito_falstad](https://user-images.githubusercontent.com/102189064/176531771-5f13a306-8c09-452b-92c3-4120f58ff4b6.png)

-----------------------------------

**PCB do circuito desenvolvido no EAGLE**

![pcb_layout](https://user-images.githubusercontent.com/102189064/176524882-84bef9b6-0da2-4e9a-8237-c9da81837575.png)

------------------------------------

**Alunos envolvidos no projeto**

- Gustavo Gabriel Ribeiro
- Marina Souza Figueiredo
- Pedro Henrique Gonçalves Bucke
- Vicenzo D'Arezzo Zilio


