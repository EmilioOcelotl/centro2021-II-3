# Clase 2

Continuaremos con el repaso de Processing

Empezaremos a hablar de modo dinámico, contadores, loops, condicionales y transformaciones. 

Partamos de una premisa de trabajo: Un arreglo de formas en dos dimensiones.

## `setup()` y `draw()`

Processing puede correr continuamente para dibujar o para interactuar en el tiempo. Para realizar esto, Processing tiene la función *draw()*. 

El código que se encuentra en *draw()* corre de arriba a abajo y se repite hasta que detienes el programa. Cada "vuelta" del *draw()* es un *frame*. 

Por *default* Processing corre a 60 fotogramas por segundo, esto quiere decir que hay 60 ciclos por segundo dentro del *draw()* 

```java
void draw() {
println("I'm drawing");
println(frameCount);
}
```

Processing también tiene una función llamada *setup()* que corre una vez que el programa inicia. 

## Condicionales

Las condicionales funcionan de manera parecida a las preguntas. Permiten a un programa realizar una acción si la respuesta a la pregunta es "cierto" o realizar otra acción si la respuesta es "falso". 

Las preguntas formuladas dentro de un programa son siempre declaraciones lógicas o relacionales. 

Por ejemplo, si la variable 'i' es igual a cero, dibuja una línea.

```java
void setup() {
size(240, 120);
strokeWeight(30);
}
void draw() {
background(204);
stroke(102);
line(40, 0, 70, height);
if (mousePressed) {
stroke(0);
} else {
stroke(255);
}
line(0, 70, width, 50);
}
```
## Loops

### `loop()` y `noLoop()`

Como ya vimos, Processing *loopea* continuamente el código escrito en `draw()`. Sin embargo, el *loop* `draw()` puede detenerse cuando escribimos `noLoop()`. En ese caso, el loop `draw()` puede reanudarse con `loop()`; 

Ejemplo: 

```java 
void setup() {
  size(200, 200);
  noLoop();  // draw() will not loop
}

float x = 0;

void draw() {
  background(204);
  x = x + .1;
  if (x > width) {
    x = 0;
  }
  line(x, 0, x, height); 
}

void mousePressed() {
  loop();  // Holding down the mouse activates looping
}

void mouseReleased() {
  noLoop();  // Releasing the mouse stops looping draw()
}
```

### `for()`

Otra estructura de código llamada `for()` hace posible correr una de código más de una vez. Esto permite condensar una repetición en pocas líneas. 

El siguiente ejemplo dibuja un patrón 

```java
size(480, 120);
strokeWeight(8);
line(20, 40, 80, 80);
line(80, 40, 140, 80);
line(140, 40, 200, 80);
line(200, 40, 260, 80);
line(260, 40, 320, 80);
line(320, 40, 380, 80);
line(380, 40, 440, 80);
```

Que puede simplificarse de la siguiente manera: 

```java
size(480, 120);
strokeWeight(8);
for (int i = 20; i < 400; i += 60) {
line(i, 40, i + 60, 80);
}
```

Las llaves, es decir { y }, distinguen a `for()`. El código que se encuentra entre llaves se llama bloque. Este es el código que va a ser repetido en cada iteración del *loop* `for()`. 

Dentro de los paréntesis hay tres declaraciones separadas por punto y coma. De izquierda a derecha, estas declaraciones son: *init, test* y *update*

```java
for (init; test; update) {
statements
}
```
En *init* fijamos el valor inicial, muchas veces declarando una variable que usaremos dentro del loop for. 

El nombre de variable `i` es frecuentemente usado, pero no hay nada especial en él. 

*Test* evalúa el valor de esta variable (para el caso del primer código, revisa si `i` sigue siendo menor que 400). *Update* cambia el valor de la variable, agregando 60 antes de repetir el *loop*