**Projeto Arduino: Relógio**

-----------------------------

Este projeto foi desenvolvido para a disciplina SS0180 - Eletrônica para Computação, ministrada pelo professor Eduardo Simões no Instituto de Ciências de 
Matemática e Computação (ICMC) da Universidade de São Paulo (USP) no ano de 2022.

-----------------------------

**A plataforma Arduino:**

O Arduino é uma plataforma de prototipagem de hardware livre e que também conta com uma IDE gratuita, é amplamente usada para criação de circuitos eletrônicos 
de pequena/média escala. A plataforma conta com um microcontrolador modelo Atmel AVR - ATMega, com capacidade de memória de até 256kB, com suporte para até 100 
pinos de conexão I/O e com suporte para uma grande gama de periféricos, como sensores, pequenos motores, displays, módulos, entre outros. Esse microcontrolador 
pode ser programado com o uso de linguagem C++, muito simples e intuitiva, o que faz com que o Arduino seja amplamente utilizado com fins educacionais e por 
pessoas sem experiência prévia, nos projetos chamados _Do It Yourself (DIY)_(faça você mesmo). Além disso, existem vários modelos de Arduino disponíveis, como o Uno
(mais comum, utilizado nesse projeto), Arduino Nano, Arduino Leonardo, Arduino Mega, entre outros.

----------------------------

**O relógio implementado na plataforma Arduino:**

O projeto visa implementar um relógio que exiba, por meio de um display LCD de dimensões 16x2 e de um monitor serial, data e horas completos para o usuário.
No projeto, é solicitado ao usuário que ele digite as informações iniciais referentes a dia, mês, ano, hora e minutos por meio de uma ferramenta disponibilizada
na IDE do Arduino, o chamado monitor serial, muito útil em diversas situações, como o  monitoramento de dados que são retornados por sensores, módulos e outros
dispositivos, e também em situações em que se deseja enviar informações ao circuito, como é o caso desse projeto. Abaixo temos uma imagem da IDE do Arduino, com
destaque para a inicialização do monitor serial.

![IDE_e_serial](https://user-images.githubusercontent.com/102189064/180839643-1b76e224-e523-4e65-9848-226e68161a99.png)

A implementação física do projeto é consideravelmente simples. A seguir são listados os componentes utilizados e posteriormente, algumas imagens do circuito:

 -  1 x Arduino Uno;
 -  1 x Display LCD 16x2;
 -  1 x Resistor 220 ohms;
 -  1 x Potenciômetro 10k ohms;
 -  Fios;
 
 ![circuito_ard](https://user-images.githubusercontent.com/102189064/180841001-033fcb0a-1d73-400b-b76b-888b5e508ab6.jpeg)
 
 ![circuito](https://user-images.githubusercontent.com/102189064/180841051-661253a0-39df-4353-9cab-fb807ef209ae.jpeg)
 
O código responsável pelo funcionamento do circuito também é consideravelmente simples, visto que, como dito anteriormente, a linguagem de programação é muito
intuitiva. É necessária apenas a importação de uma biblioteca para que o LCD funncione corretamente. Abaixo, o código na linguagem C++.

    #include <LiquidCrystal.h> //Inclui a biblioteca do LCD 

    LiquidCrystal lcd(12, 11, 5, 4, 3, 2); 

    int segundo,minuto, hora, dia, mes,ano; 
    unsigned long UtlTime; 

    void setup() 
    {   

    UtlTime=0;   
    minuto=0;   
    hora=0;   
    dia=0;   
    mes=0;   
    ano=0;   
    Serial.begin(9600);   
    lcd.begin(16, 2);      

    lcd.setCursor(0,0);   
    lcd.print(" Data e hora ");   
    lcd.setCursor(0,1);   
    lcd.print(" com Arduino");   
    delay (2000); 

    //Configura o minuto   
    lcd.clear();   
    lcd.setCursor(0,0);   
    lcd.print("Minuto: ");   
    Serial.print("\nEntre Minuto:");  
    while(minuto==0)   {     
    if (Serial.available() > 0)     
    {       
    minuto= Serial.parseInt();     
    }   
    }   
    lcd.print(minuto);   
    delay(1000); 

    //Configura a hora   
    lcd.clear();   
    lcd.setCursor(0,0);   
    lcd.print("Hora: ");   
    Serial.print("\nEntre Hora:"); 
    while(hora==0)   
    {     
    if (Serial.available() > 0)     
    {       
    hora= Serial.parseInt();     
    }   
    }   
    lcd.print(hora);   
    delay(1000);    

    //Configura o Dia   
    lcd.clear();   
    lcd.setCursor(0,0);   
    lcd.print("Dia: ");   
    Serial.print("\nEntre Dia:");   
    while(dia==0)   
    {     
    if (Serial.available() > 0)     
    {       
    dia= Serial.parseInt();     
    }   
    }   
    lcd.print(dia);   
    delay(1000);    

    //Configura o mês   
    lcd.clear();   
    lcd.setCursor(0,0);   
    lcd.print("Mes: ");   
    Serial.print("\nEntre Mes:");  
    while(mes==0)   
    {     
    if (Serial.available() > 0)     
    {       
    mes= Serial.parseInt();     
    }   
    }   
    lcd.print(mes);   
    delay(1000);    

    //Configura o Ano   
    lcd.clear();   
    lcd.setCursor(0,0);   
    lcd.print("Ano: ");   
    Serial.print("\nEntre ano:");   
    while(ano==0)   
    {     
    if (Serial.available() > 0)     
    {       
    ano= Serial.parseInt();     
    }   
    }   
    lcd.print(ano);   
    delay(1000);   

    lcd.clear(); 

    } 

    void loop() 
    {   

    if(millis()-UtlTime<0)   
    {     
      UtlTime = millis();   
    }   
    else   
    {     
      segundo = int((millis() - UtlTime)/1000);   
    }   
    if(segundo == 59)   
    {     
      segundo = 0;     
      minuto++;     
      UtlTime = millis();     
    if(minuto>59)     
    {       
      hora++;       
      minuto=0;       
      if(hora>23)       
    {         
      dia++;         
      hora=0;         
     if(mes==1||mes==3||mes==5||mes==7||mes==8||mes==10||mes==12)         
    {           
    if(dia>31)           
    {             
      dia=1;             
      mes++;             
    if(mes>12)             
    {               
      ano++;               
    mes = 1;             
    }           
    }         
    }         
    else if(mes==2)         
    {           
    if(ano%400==0)           
    {             
    if(dia>29)             
    {               
    dia=1;               
    mes++;             
    }           
    }           
    else if((ano%4==0)&&(ano%100!=0))           
    {             
    if(dia>29)             
    {              
    dia=1;               
    mes++;             
    }           
    }           
    else           
    {             
    if(dia>28)             
    {               
    dia=1;               
    mes++;             
    }           
    }         
    }         
    else         
    {           
    if(dia>30)           
    {             
    dia=1;             
    mes++;           
    }         
    }       
    }     
    }   
    }    

    Serial.print(dia);   
    Serial.print("/");   
    Serial.print(mes);   
    Serial.print("/");   
    Serial.print(ano);   
    Serial.println();      

    lcd.setCursor(0,0);   
    lcd.print("Data ");   
    lcd.print(dia);   
    lcd.print("/");   
    lcd.print(mes);   
    lcd.print("/");   
    lcd.print(ano);   

    Serial.print(hora);   
    Serial.print(":");   
    Serial.print(minuto);   
    Serial.print(":");   
    Serial.print(segundo);   
    Serial.print("\n");   
    Serial.println();      

    lcd.setCursor(0,1);   
    lcd.print("Hora ");   
    lcd.print(hora);   
    lcd.print(":");   
    lcd.print(minuto);   
    lcd.print(":");   
    lcd.print(segundo); 

    }

--------------------------------

**Imagem do monitor serial em exibindo data e hora em tempo real:**

![hora_serial](https://user-images.githubusercontent.com/102189064/180842151-5355b23c-d94d-446e-8c25-7b275ac9627c.png)

É possível que os segundos se repetem algumas vezes no monitor serial, isso se deve ao fato da taixa de atualização dele ser inferior a um segundo, o que faz
com que o mesmo segundo seja mostrado repetidas vezes.

--------------------------------

**Link para o vídeo explicativo do funcionamento do projeto:**

Link:

--------------------------------

**Imagem esquemática do circuito desenvolvido no software Tinkercad:**

![tinkercad](https://user-images.githubusercontent.com/102189064/180890692-40849d5e-2a10-4251-8b54-70d224bacfcc.png)

--------------------------------

**Alunos envolvidos no desenvolvimento do projeto:**

 - Gustavo Gabriel Ribeiro
 - Marina Souza Figueiredo
 - Pedro Henrique Gonçalves Bucke
 - Vicenzo D'Arezzo Zilio
