
# Guion: Tema 6 — Árboles de Decisión

## 1. Raíz, nodo, rama y hoja; cómo se recorre un árbol

* **Raíz:** Es la primera pregunta o condición arriba de todo del árbol.
* **Nodo:** Cualquier pregunta intermedia por la que vas pasando para dividir los casos.
* **Rama:** Cada camino que sale de una pregunta (por ejemplo, "Sí" o "No").
* **Hoja:** El final del camino, donde ya no hay más preguntas y te da la respuesta o predicción.
* **¿Cómo se recorre?** Empezás en la raíz, respondés la pregunta según los datos del caso, bajás por la rama que corresponde y repetís hasta llegar a una hoja.

## 2. Árbol de tres niveles y recorrido de dos casos

Usamos el mismo problema: saber si el delivery es **Rápido (`Sí`)** o **No (`No`)** usando **tiempo de preparación (`prep`)** y **distancia (`distancia`)**.

* **Nivel 1 (Raíz):** ¿`prep` es menor o igual a 15 min?
* **Si SÍ:** pasa a ¿`distancia` es menor o igual a 3.5 km?
* **Si SÍ:** **Hoja → `Sí**`
* **Si NO:** pasa a ¿`prep` es menor o igual a 10 min?
* **Si SÍ:** **Hoja → `Sí**`
* **Si NO:** **Hoja → `No**`




* **Si NO:** pasa a ¿`distancia` es menor o igual a 2.0 km?
* **Si SÍ:** **Hoja → `Sí**`
* **Si NO:** **Hoja → `No**`





**Dos casos recorridos:**

* **Caso 1 (`prep = 12 min`, `distancia = 4.0 km`):** `prep <= 15` es **Sí** → `distancia <= 3.5` es **No** → `prep <= 10` es **No** → Predicción: **`No`**.
* **Caso 2 (`prep = 18 min`, `distancia = 1.5 km`):** `prep <= 15` es **No** → `distancia <= 2.0` es **Sí** → Predicción: **`Sí`**.

## 3. Cómo aprende cortes y qué es separar mejor las clases

Cuando un árbol aprende solo, prueba distintas preguntas y cortes para dividir los datos. **Separar mejor las clases** significa que, después de hacer un corte, cada grupo quede lo más limpio posible: idealmente que de un lado queden casi todos `Sí` y del otro casi todos `No`, en vez de quedar mezclados mitad y mitad.

## 4. Árbol hecho a mano vs. aprendido con datos

* **Hecho a mano:** Lo arma una persona según su criterio o experiencia para explicar cómo se toma una decisión. Es fácil de entender, pero puede no reflejar lo que pasa en los datos reales.
* **Aprendido con datos:** El algoritmo busca los cortes mirando ejemplos históricos. Para entrenarlo y evaluarlo necesitás datos con respuestas conocidas, separarlos en entrenamiento y prueba (para probarlo con casos que no vio antes) y medir qué tan bien acierta con métricas simples como el porcentaje de aciertos.

## 5. Árbol muy profundo, profundidad máxima, ventaja y limitación

* **¿Qué pasa si tiene demasiados niveles?** Hace preguntas demasiado específicas para pocos casos y termina memorizando detalles o excepciones de los datos de entrenamiento (*sobreajuste*). Después, con datos nuevos, falla más.
* **Profundidad máxima:** Es un límite que se le pone al árbol para que no tenga más de cierta cantidad de niveles de preguntas.
* **Ventaja:** Es muy fácil de leer y explicar (parecen reglas de *"si pasa esto, entonces..."*).
* **Limitación:** Si cambia un poco la información de entrenamiento, el árbol puede cambiar bastante su forma, o sobreajustar si lo dejás crecer sin límite.

## 6. Recurso visual y actividad para el curso

* **Visual:** El dibujo del árbol con sus cajas y flechas (`Sí` / `No`) y una tablita con 3 o 4 casos mostrando el camino que siguen y su resultado final.
* **Actividad para el curso:** Dar dos casos para justificar:
1. **Para recorrer:** **`prep = 14 min`** y **`distancia = 2.5 km`** (pedir que sigan el camino y digan la predicción).
2. **Que podría clasificar mal:** **`prep = 16 min`** y **`distancia = 2.1 km`** (pedir que expliquen por qué caer justo apenas por encima de los cortes de 15 min y 2.0 km puede dar `No` cuando en la práctica está muy cerca del límite).