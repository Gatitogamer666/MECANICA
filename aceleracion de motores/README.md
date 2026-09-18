# Prueba de aceleración de motores

Este programa controla dos motores mediante un driver, aumentando gradualmente la velocidad desde `0` hasta `255`.

## Código

```cpp
// DEFINIR LOS PINES

int ENA = 9;
int IN1 = 8;
int IN2 = 7;
int IN3 = 5;
int IN4 = 4;
int ENB = 3;

// VARIABLES

int vel = 0;       // velocidad
int tiempo = 200;  // tiempo en milisegundos

// INICIA EL METODO SETUP

void setup() {

  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
  pinMode(ENB, OUTPUT);

  Serial.begin(9600); // COMUNICARSE CON LA COMPUTADORA

  Serial.println("Prueba de aceleracion");

  delay(3000);
}

// LO QUE ESTE AQUI SE REPITE UNA Y OTRA VEZ

void loop() {

  digitalWrite(IN1, HIGH); // Valor positivo
  digitalWrite(IN2, LOW);  // Valor negativo
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);

  analogWrite(ENA, vel);
  analogWrite(ENB, vel);

  Serial.print("Velocidad: ");
  Serial.println(vel);

  vel = vel + 1; // MODIFICAR EL VALOR

  if (vel > 255) {
    vel = 255;
  }

  delay(tiempo);
}
