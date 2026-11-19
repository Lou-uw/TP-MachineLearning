# Guion: Tema 5 — KNN y Vecinos Más Cercanos

## 1. ¿Cómo predice KNN, qué es $k$ y qué guarda?

* **¿Qué guarda?** KNN no arma una fórmula ni un modelo complejo cuando entrena: **guarda en memoria todos los datos de entrenamiento** (cada punto con sus valores y su etiqueta).
* **¿Cómo predice?** Cuando llega un dato nuevo, mide qué tan lejos está de todos los puntos guardados, elige los **$k$ más cercanos** y decide según ellos. Si es **clasificación**, gana la categoría que tenga más votos entre esos vecinos. Si es **regresión**, se saca el promedio de los valores de esos vecinos.
* **¿Qué significa $k$?** Es la cantidad de vecinos más cercanos que se miran para decidir. Suele usarse un número impar en clasificación con dos clases para evitar empates.

## 2. Ejemplo de clasificación con dos variables ($k = 1, 3, 5$)

Supongamos que queremos saber si un pedido de delivery sale **Rápido (`R`)** o **Demorado (`D`)** mirando dos cosas:

* **Distancia al local** (en km)
* **Tiempo de preparación** (en minutos)

Datos históricos (10 pedidos):

* **P1:** 1.0 km, 10 min → `R` (distancia al nuevo punto: ~4.47)
* **P2:** 1.5 km, 12 min → `R` (distancia al nuevo punto: 2.50)
* **P3:** 2.0 km, 8 min → `R` (distancia al nuevo punto: ~6.08)
* **P4:** 2.5 km, 15 min → `R` (distancia al nuevo punto: ~1.12)
* **P5:** 3.0 km, 11 min → `R` (distancia al nuevo punto: 3.00)
* **P6:** 4.0 km, 20 min → `D` (distancia al nuevo punto: ~6.08)
* **P7:** 5.0 km, 18 min → `D` (distancia al nuevo punto: ~4.47)
* **P8:** 6.0 km, 22 min → `D` (distancia al nuevo punto: ~8.54)
* **P9:** 4.5 km, 14 min → `D` (distancia al nuevo punto: 1.50)
* **P10:** 5.5 km, 25 min → `D` (distancia al nuevo punto: ~11.28)

**Punto nuevo:** **3.0 km** y **14 min**.

Los más cercanos al punto nuevo son, en orden: **P4** (`R`), **P9** (`D`), **P2** (`R`), **P5** (`R`), y luego empatan **P1** (`R`) y **P7** (`D`).

* **Con $k = 1$:** Miramos solo al más cercano (**P4**, que es `R`). Predicción: **`R`**.
* **Con $k = 3$:** Miramos a **P4 (`R`)**, **P9 (`D`)** y **P2 (`R`)**. Gana **`R`** (2 a 1).
* **Con $k = 5$:** Miramos a **P4 (`R`)**, **P9 (`D`)**, **P2 (`R`)**, **P5 (`R`)** y **P1 (`R`)**. Gana **`R`** (4 a 1).

## 3. Distancia euclidiana y qué pasa con escalas distintas

* **Distancia euclidiana:** Es simplemente la distancia en línea recta entre dos puntos en un gráfico.
* **Ejemplo simple:** Entre el punto `(2, 5)` y el punto `(5, 9)`, en X hay una diferencia de `3` y en Y de `4`. Haciendo la cuenta de distancia en línea recta, da **`5`**.
* **¿Qué cambia si una variable tiene números mucho más grandes?** Si una variable va de `1` a `10` (por ejemplo, cantidad de pizzas) y otra va de `1.000` a `50.000` (por ejemplo, precio en pesos), la variable con números grandes va a pesar muchísimo más en la distancia y va a tapar a la otra.

## 4. Estandarización vs. escalado min–max y datos de entrenamiento

* **Estandarización:** Centra los datos alrededor de `0` y ajusta según qué tan dispersos están. Sirve bien cuando hay valores muy extremos que no querés que deformen todo.
* **Escalado min–max:** Lleva todos los valores a un mismo rango, normalmente entre `0` y `1` (donde el mínimo pasa a ser `0` y el máximo pasa a ser `1`).
* **¿Por qué ajustar solo con entrenamiento?** Porque los valores de referencia (mínimo, máximo, promedio o dispersión) se calculan solo con los datos de entrenamiento y luego se aplican a los datos nuevos o de prueba. Si usás los datos de prueba para calcular esos ajustes, hacés trampa sin querer (*data leakage*) y el resultado parece mejor de lo que realmente es.

## 5. Elegir $k$, usar el mismo punto como vecino y KNN en regresión

* **¿Cómo elegir $k$?** Probando distintos valores (por ejemplo, impares como 1, 3, 5, 7) y viendo cuál funciona mejor sin que el modelo se vuelva demasiado estricto ni demasiado vago. Si $k$ es muy chico, se deja llevar por casos aislados; si es muy grande, mezcla cosas distintas.
* **¿Qué pasa si cada punto se usa como vecino de sí mismo al evaluar?** Si evaluás un punto de entrenamiento contra sí mismo con $k = 1$, la distancia es `0` y siempre se acierta a sí mismo, lo que da un puntaje falso y engañoso.
* **KNN en regresión:** En vez de votar una categoría, promedia el número de los $k$ vecinos más cercanos (por ejemplo, estimar cuántos minutos tarda un pedido promediando el tiempo de los pedidos más parecidos).

## 6. Recurso visual y actividad para el curso

* **Visual:** Un gráfico de puntos con los 10 pedidos, el punto nuevo `(3.0, 14)` marcado, los vecinos más cercanos rodeados o unidos con líneas, y al lado un gráfico mostrando cómo quedan los puntos cuando los llevás a una misma escala (por ejemplo, de `0` a `1`).
* **Actividad para el curso:** Pedirles que clasifiquen un segundo punto nuevo: **`4.2 km` y `15 min**`, con **$k = 3$** y con **$k = 5$**, que expliquen los votos y que digan qué cambiaría si antes se normalizan ambas variables entre `0` y `1`.

---
