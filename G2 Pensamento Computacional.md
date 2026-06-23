Parte escrita: https://docs.google.com/document/d/1X0MRe4_LUPw_WML4_k1gj5AA9WbJiOWZ0t8QTSpMFUQ/edit?tab=t.0 


![imagem da montagem](montagem.png) 


Algoritmo do projeto:
const int sensorBaixo = 11;
const int sensorAlto  = 6;

const int led1 = 9;
const int led2 = 7;

const int rele = 3;

const int RELE_LIGA    = LOW;   // ajuste se necessário
const int RELE_DESLIGA = HIGH;

bool bombaLigada = false;

void setup() {
  Serial.begin(9600);

  pinMode(sensorBaixo, INPUT_PULLUP);
  pinMode(sensorAlto, INPUT_PULLUP);

  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);

  pinMode(rele, OUTPUT);

  digitalWrite(rele, RELE_DESLIGA);
}

void loop() {

  int valor1 = digitalRead(sensorBaixo);
  int valor2 = digitalRead(sensorAlto);

  digitalWrite(led1, (valor1 == LOW) ? HIGH : LOW);
  digitalWrite(led2, (valor2 == LOW) ? HIGH : LOW);

  
  if (valor2 == LOW) {
    
    bombaLigada = false;
  }
  else if (valor1 == HIGH) {
    
    bombaLigada = true;
  }

  digitalWrite(rele, bombaLigada ? RELE_LIGA : RELE_DESLIGA);

  
  Serial.print("{\"sensor1\":");
  Serial.print(valor1);

  Serial.print(",\"sensor2\":");
  Serial.print(valor2);

  Serial.print(",\"led1\":");
  Serial.print((valor1 == LOW) ? 1 : 0);

  Serial.print(",\"led2\":");
  Serial.print((valor2 == LOW) ? 1 : 0);

  Serial.print(",\"rele\":");
  Serial.print(bombaLigada ? 1 : 0);

  Serial.println("}");

  delay(500);
}
