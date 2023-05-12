#include <Servo.h>  /*Se descraga la libreria que se va a ocupar*/
/*Se declaran las variables y lospines en donde estara conectado el sensor ultrasónico*/
const int trigPin = 10;
const int echoPin = 11;
long duration;
int distance;
Servo myServo;


void setup() {

  /*Configura cada uno de los pines es decir cual sera como entrada y cual como salida*/

  pinMode(trigPin, OUTPUT); 
  pinMode(echoPin, INPUT);
  Serial.begin(9600); /* Proceso de envio de datos*/
  myServo.attach(3);
}
void loop() { /*Imprime la distancia y al mismo tiempo la calcula */
  for(int i=15;i<=165;i++){  
  myServo.write(i);
  delay(30);
  distance = calculateDistance();
  Serial.print(i); 
  Serial.print(","); 
  Serial.print(distance);
  Serial.print(".");
  }
  for(int i=165;i>15;i--){  
  myServo.write(i);
  delay(30);
  distance = calculateDistance();
  Serial.print(i);
  Serial.print(",");
  Serial.print(distance);
  Serial.print(".");
  }
}
/*Hace el retorno de la distancia y aparte la pausa que se le da al momento de detectar los objetos.*/
int calculateDistance(){
  digitalWrite(trigPin, LOW); 
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH); 
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance= duration*0.034/2;
  return distance;
}
