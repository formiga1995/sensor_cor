# sensor_cor
Código do sensor de cor TCS230
//Pinos de conexao do modulo TCS230  
const int s0 = 7;  
const int s1 = 5;  
const int s2 = 2;  
const int s3 = 4;  
const int out = 3;   
   

    
int red = 0;  
int green = 0;  
int blue = 0;  
    
void setup()   
{  
  pinMode(s0, OUTPUT);  
  pinMode(s1, OUTPUT);  
  pinMode(s2, OUTPUT);  
  pinMode(s3, OUTPUT);  
  pinMode(out, INPUT);  
  Serial.begin(9600);  
  digitalWrite(s0, HIGH);  
  digitalWrite(s1, LOW);  
}  
    
void loop() 
{  
  color();
  Serial.print("Vermelho: ");  
  Serial.print(red, DEC);  
  Serial.print(" Verde: ");  
  Serial.print(green, DEC);  
  Serial.print(" Azul: ");  
  Serial.print(blue, DEC);  
  Serial.println();  

  if( red < 100 && green > 130 && blue > 125  ){
   Serial.println("Vermelho");  
  } else if( red > 70 && red < 140 && green > 180 && green < 300 && blue > 180 && blue < 300  ){
   Serial.println("Laranja");  
  } else if( red < 110 && red > 40 && green > 80 && green < 130 && blue > 130  ){
   Serial.println("Amarelo Queimado");  
  } else if( red < 60 && red > 0 && green < 60 && blue > 75  ){
   Serial.println("Amarelo");  
  }else if( red < 190 && green > 200 && blue < 160  ){
   Serial.println("Roxo");  
  }else if( red > 140 && green > 115 && blue < 95  ){
   Serial.println("Azul");  
  }else if( red > 100 && green < 100 && green > 60 && blue < 95  ){
   Serial.println("Ciano");  
  }else if( red > 200 && green < 150 && blue > 160  ){
   Serial.println("Verde");  
  }else if( red < 50 && green < 60 && blue < 50  ){
   Serial.println("Branco");  
  }else if( red > 350 && green > 350 && blue > 300  ){
   Serial.println("Preto");  
  }else{
    Serial.println("Nada");
  }
  Serial.println();  
 delay(1000);

 }  
    
void color()  
{  
  digitalWrite(s2, LOW);  
  digitalWrite(s3, LOW);  
  //count OUT, pRed, RED  
  red = pulseIn(out, digitalRead(out) == HIGH ? LOW : HIGH);  
  digitalWrite(s3, HIGH);  
  //count OUT, pBLUE, BLUE  
  blue = pulseIn(out, digitalRead(out) == HIGH ? LOW : HIGH);  
  digitalWrite(s2, HIGH);  
  //count OUT, pGreen, GREEN  
  green = pulseIn(out, digitalRead(out) == HIGH ? LOW : HIGH);  
}
