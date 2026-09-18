# Medición de velocidad en MRU con Arduino

## Opción A — Con sensores ultrasónicos HC-SR04

```cpp
// Medición de velocidad en MRU con 2 sensores HC-SR04
// v = d / t

const int trigPin1 = 9,  echoPin1 = 10;
const int trigPin2 = 11, echoPin2 = 12;

const float distanciaSensores = 0.50; // metros (AJUSTAR a tu montaje)
const float umbralDeteccion = 15.0;   // cm: distancia por debajo de la cual se considera "objeto presente"

unsigned long tiempoSensor1 = 0;
unsigned long tiempoSensor2 = 0;
bool detectado1 = false;
bool detectado2 = false;

float medirDistanciaCM(int trigPin, int echoPin) {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  long duracion = pulseIn(echoPin, HIGH, 30000); // timeout 30 ms

  if (duracion == 0) return 999; // sin eco = "vacío"

  return duracion * 0.0343 / 2.0; // cm
}

void setup() {
  Serial.begin(9600);

  pinMode(trigPin1, OUTPUT);
  pinMode(echoPin1, INPUT);
  pinMode(trigPin2, OUTPUT);
  pinMode(echoPin2, INPUT);

  Serial.println(
    "Sistema listo. Distancia entre sensores: " +
    String(distanciaSensores) + " m"
  );
}

void loop() {
  float d1 = medirDistanciaCM(trigPin1, echoPin1);
  float d2 = medirDistanciaCM(trigPin2, echoPin2);

  // Detección en sensor 1
  if (d1 < umbralDeteccion && !detectado1) {
    detectado1 = true;
    tiempoSensor1 = micros();

    Serial.println("Objeto detectado en Sensor 1");
  }

  // Detección en sensor 2 (solo cuenta si ya pasó por el 1)
  if (d2 < umbralDeteccion && detectado1 && !detectado2) {
    detectado2 = true;
    tiempoSensor2 = micros();

    float deltaT = (tiempoSensor2 - tiempoSensor1) / 1000000.0;
    float velocidad = distanciaSensores / deltaT;

    Serial.println("Objeto detectado en Sensor 2");

    Serial.print("Tiempo transcurrido: ");
    Serial.print(deltaT, 4);
    Serial.println(" s");

    Serial.print("Velocidad calculada: ");
    Serial.print(velocidad, 3);
    Serial.println(" m/s");

    Serial.println("--------------------------------------");

    // Reiniciar para la siguiente medición
    delay(1500);

    detectado1 = false;
    detectado2 = false;
  }

  delay(20); // pequeña pausa entre lecturas
}

## Opción B — Con sensores IR de barrera
Esta opción utiliza interrupciones, por lo que permite una medición temporal más precisa.

// Medición de velocidad en MRU con 2 sensores IR de barrera
// Usa interrupciones para mayor precisión temporal

const byte pinSensor1 = 2; // debe ser pin de interrupción
const byte pinSensor2 = 3; // debe ser pin de interrupción

const float distanciaSensores = 0.50; // metros (AJUSTAR)

volatile unsigned long t1 = 0;
volatile unsigned long t2 = 0;
volatile bool marco1 = false;
volatile bool marco2 = false;

void ISR_sensor1() {
  if (!marco1) {
    t1 = micros();
    marco1 = true;
  }
}

void ISR_sensor2() {
  if (marco1 && !marco2) {
    t2 = micros();
    marco2 = true;
  }
}

void setup() {
  Serial.begin(9600);

  pinMode(pinSensor1, INPUT);
  pinMode(pinSensor2, INPUT);

  attachInterrupt(
    digitalPinToInterrupt(pinSensor1),
    ISR_sensor1,
    FALLING
  );

  attachInterrupt(
    digitalPinToInterrupt(pinSensor2),
    ISR_sensor2,
    FALLING
  );

  Serial.println("Sistema listo (modo interrupciones).");
}

void loop() {
  if (marco1 && marco2) {
    float deltaT = (t2 - t1) / 1000000.0;
    float velocidad = distanciaSensores / deltaT;

    Serial.print("Delta t: ");
    Serial.print(deltaT, 4);
    Serial.println(" s");

    Serial.print("Velocidad: ");
    Serial.print(velocidad, 3);
    Serial.println(" m/s");

    Serial.println("--------------------------------------");

    delay(1500);

    marco1 = false;
    marco2 = false;
  }
}
