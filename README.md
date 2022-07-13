# ArduinoBluethoo_thelectricityProjectApplication
Controlador Arduino para Android

```
const int ledPin = 13; // Built in LED aspersión
const int ledPin2= 12; 
String msg,cmd,msg2;

void setup() {
  // Initialization
  pinMode(ledPin, OUTPUT);
  pinMode(ledPin2, OUTPUT);
  digitalWrite(ledPin2,LOW);
  digitalWrite(ledPin, LOW);
  Serial.begin(9600); // Communication rate of the Bluetooth Module
  msg = "";
  msg2 = "";
}

void loop() {
  
  // To read message received from other Bluetooth Device
  if (Serial.available() > 0){ // Comprueba si hay datos que llgan
    msg = Serial.readString(); // Lee el mensaje como cadena
    msg2= Serial.readString();
    Serial.println("Android Command: " + msg);
    Serial.println("Android Command: " + msg2);
  }

  // Control del Led aspersión con la tarjeta arduino
  if (msg == "<Encendido>"){
    digitalWrite(ledPin, HIGH); // Enciende el led
    Serial.println("Aspersion encendida\n"); // Envia un mensaje de estado al Celular
    msg = ""; // Resetea el comando
  } else {
    if (msg == "<Apagado>"){ //Lo mismo que en el caso anterior, pero apagando el LED
      digitalWrite(ledPin, LOW); // Apaga el LED
      Serial.println("Aspersion apagada\n"); // Envia un mensaje de estado al celular
      msg = ""; // Resetea el comando
    }
  }
  // Control del Led goteo con la tarjeta arduino
  if (msg2 == "<Encendido>"){
    digitalWrite(ledPin2, HIGH); // Enciende el led
    Serial.println("Goteo encendido\n"); // Envia un mensaje de estado al Celular
    msg2 = ""; // Resetea el comando
  } else {
    if (msg2 == "<Apagado>"){ //Lo mismo que en el caso anterior, pero apagando el LED
      digitalWrite(ledPin2, LOW); // Apaga el LED
      Serial.println("Goteo apagado\n"); // Envia un mensaje de estado al celular
      msg2 = ""; // Resetea el comando
    }
  }
}
```
