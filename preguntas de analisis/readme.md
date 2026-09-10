Análisis de resultados
1. Porcentaje de error debido a una imprecisión de ±0.5 cm

La distancia real entre los sensores es de 50 cm, mientras que la incertidumbre en la medición es de ±0.5 cm.

El porcentaje de error se calcula mediante:

Porcentaje de error = (incertidumbre / valor medido) × 100

Por lo tanto:

Porcentaje de error = (0.5 cm / 50 cm) × 100 = 1 %

Por lo tanto, una imprecisión de ±0.5 cm introduce un error relativo de ±1 % en la medición de la distancia.

2. Efecto del ancho del objeto y del umbral de detección en el tiempo medido

Si el objeto tiene un ancho de 3 cm, el sensor no necesariamente detectará un único punto del objeto. Dependiendo del tipo de sensor y de su umbral de detección, puede comenzar a detectar el objeto antes de que su centro llegue al sensor y dejar de detectarlo después de que el centro lo haya atravesado.

Esto puede provocar que el tiempo registrado tenga un pequeño desplazamiento respecto al tiempo ideal.

En particular, si ambos sensores tienen un comportamiento similar, parte de este efecto puede compensarse. Sin embargo, si los umbrales de detección de los sensores son diferentes, pueden aparecer errores adicionales en el tiempo medido.

Por esta razón, el ancho del objeto y la forma en que cada sensor detecta su presencia deben considerarse como posibles fuentes de incertidumbre experimental.

3. Comparación entre sensores ultrasónicos e IR

Los sensores ultrasónicos y los sensores infrarrojos (IR) pueden presentar diferentes niveles de variabilidad dependiendo de las condiciones del experimento.

En general, los sensores IR pueden proporcionar mediciones más consistentes cuando el objeto presenta una superficie y posición adecuadas para la detección, ya que la señal puede cambiar rápidamente cuando el objeto interrumpe o refleja el haz infrarrojo.

Los sensores ultrasónicos, por otro lado, pueden verse afectados por factores como la distancia, el ángulo de la superficie, la forma del objeto y posibles reflexiones del sonido.

Por lo tanto, si durante el experimento los sensores IR presentaron una menor dispersión entre las mediciones, se puede concluir que tuvieron menor variabilidad bajo las condiciones utilizadas. Esto se debería principalmente a una detección más definida del paso del objeto.

La comparación definitiva debe hacerse utilizando los datos experimentales, por ejemplo, calculando la desviación estándar de los tiempos obtenidos con cada tipo de sensor.

4. ¿Qué ocurre si el objeto acelera entre los dos sensores?

El cálculo habitual de la velocidad es:

v = d / Δt

donde d es la distancia entre los sensores y Δt es el tiempo que tarda el objeto en recorrerla.

Si el objeto acelera entre los dos sensores, su velocidad no es constante durante ese intervalo. Por lo tanto, el valor obtenido mediante v = d / Δt ya no representa exactamente la velocidad instantánea del objeto.

En este caso, el resultado corresponde a la velocidad media durante el recorrido entre los dos sensores.

Si la aceleración es constante, la velocidad media puede expresarse como:

v_media = (v_inicial + v_final) / 2

Por lo tanto, si existe aceleración, es necesario considerar el movimiento como un movimiento acelerado y no como un movimiento de velocidad constante.

5. Modificación del montaje para medir aceleración

Para medir la aceleración se puede modificar el montaje colocando tres sensores en lugar de dos.

Por ejemplo:

Sensor 1          Sensor 2          Sensor 3
   |                  |                  |
   ↓                  ↓                  ↓
---|------------------|------------------|---
       d₁                  d₂


Se registraría el instante en que el objeto pasa por cada sensor:

t₁: tiempo de detección en el sensor 1.
t₂: tiempo de detección en el sensor 2.
t₃: tiempo de detección en el sensor 3.

Con estas mediciones se pueden obtener las velocidades en diferentes intervalos:

v₁₂ = d₁ / (t₂ - t₁)

v₂₃ = d₂ / (t₃ - t₂)

Después, se puede estimar la aceleración mediante el cambio de velocidad dividido entre el intervalo de tiempo correspondiente:

a ≈ (v₂₃ - v₁₂) / Δt

donde Δt representa el intervalo de tiempo entre las mediciones de velocidad.

Una alternativa más precisa consiste en utilizar las tres posiciones y sus respectivos tiempos para ajustar los datos a la ecuación del movimiento uniformemente acelerado:

x = x₀ + v₀t + ½at²

De esta manera, el montaje con tres sensores permite determinar no solamente la velocidad, sino también si el objeto está acelerando y estimar el valor de dicha aceleración.
