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

*Test* evalúa el valor de esta variable (para el caso del primer código, revisa si `i` sigue siendo menor que 400). *Update* cambia el valor de la variable, agregando 60 antes de repetir el *loop*.

Un diagrama puede clarificar el flujo de un *for loop* 

Cabe destacar que la declaración *text* es siempre una expresión relacional que compara dos valores con un operador relacional. En el ejemplo de arriba, la expresión es "i < 400" y el operador es < (menor que). Los operadores relacionales más comunes son: 

| Símbolo | Operación        |
|:-------:|:----------------:|
| >       | Mayor que        | 
| <       | Menor que        |
| >=      | Mayor o igual que|
| <=      | Menor que        |
| ==      | Igual a          |
| !=      | No es igual a    |

El resultado de la evaluación siempre es cierto o falso. 

## Transformaciones 

### translate(), rotate() y scale()

La función translate sirve para cambiar el sistema de coordenadas, por default (0, 0) a una localización diferente. 


```java
void setup() {
size(120, 120);
}
void draw() {
translate(mouseX, mouseY);
rect(0, 0, 30, 30);
}
```

Para el caso del ejemplo anterior, el sistema de coordenadas cambia de (0, 0) a la posición del mouse. cada vez que draw() dibuja algo, rect() se dibuja en el nuevo origen

La función rotate() rota el sistema de coordenadas. Tiene un solo parámetro, que es el ángulo (en radianes) de rotación. Su rotación es relativa a (0, 0), es decir, rota alrrededor del origen. 

```java
void setup() {
size(120, 120);
}
void draw() {
rotate(mouseX / 100.0);
rect(40, 30, 160, 20);
}
```

Es posible utilizar una función para convertir grados sexagesimales a radianes: radians(). Esta función toma el ángulo en grados y los cambia a su valor equivalente en radianes. 

Para usar las medidas en grados y no en radianes.

```java
void setup() {                                                                                                                                                                                
size(520, 520);                                                                                                                                                                               
}                                                                                                                                                                                             
void draw() {                                                                                                                                                                                 
rotate(radians(mouseX % 360));                                                                                                                                                                
rect(140, 130, 160, 20);                                                                                                                                                                      
} 
```

La transformación `scale()` cambia el tamaño de la figura seleccionada. Debido a que las coordenadas expanden o contraen en la medida que la escala cambia, todo lo que se dibuja en la ventana aumenta o disminuye proporcionalmente. Usamos scale(1.5) para aumentar todo a 150% de su tamaño original. 


```java
void setup() {
size(120, 120);
}

void draw() {
translate(mouseX, mouseY);
scale(mouseX / 60.0);
rect(-15, -15, 30, 30);
}
```


### `pushMatrix() y popMatrix()`

Para aislar los efectos de una transformación de forma tal que no afecten a otros comandos, usamos las funciones `pushMatrix()` y `popMatrix()`

Cuando `pushMatrix()` está corriendo, salva una copia del sistema de coordenadas que está en ejecución y reanuda ese sistema después de `popMatrix()`; 

Esto es útil cuando requerimos hacer transformaciones para una figura, pero no queremos que tenga consecuencias para otras. 

```java
void setup() {
size(120, 120);
}
void draw() {
pushMatrix();
translate(mouseX, mouseY);
rect(0, 0, 30, 30);
popMatrix();
translate(35, 10);
rect(0, 0, 15, 15);
}
```

Para rotar una figura en su propio eje: 

```java
void setup() {
size(120, 120);
}
void draw() {
rotate(mouseX / 100.0);
rect(40, 30, 160, 20);
}
```