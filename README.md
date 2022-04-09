# ExamenCalculadora01152328

Primera parte del examen práctico 1 (calculadora en Angular) para la materia de Aplicaciones Web con Base de Datos.

---
## Funcionamiento lógico de los métodos de la calculadora de Angular



### `getNumber()`
---
El método **getNumber()** obtiene el valor (como una cadena de caracteres, o string) establecido en la plantilla HTML.


Dentro del primer *if*, la variable *waitForSecondNumber* espera que el usuario realice una operación y termine de introducir su primer número para poder introducir un segundo número y completar la operación. Al realizar la operación, el resultado cuenta como el “primer número”, por lo que realizar otra operación cuenta como el “segundo número”, y así será de forma sucesiva hasta que se deseé terminar de realizar operaciones.


El *else* indica que, si el valor no es igual a 0, los números que sean introducidos serán visualizados en pantalla (por ejemplo, si se introduce un “3” y luego un “5”, se mostrará en pantalla el número “35”, y así será sucesivamente. Esto se refiere a que el número no puede comenzar con 0. 


### `getDecimal()`
---
El método **getDecimal()** se asegura de que, si el valor no tiene un punto decimal, el usuario podrá agregarlo. De lo contrario, si se detecta que ya hay un punto decimal, entonces la calculadora no agregará otro punto decimal.


### `getOperation()`
---
Al igual que el método *getNumber()*, **getOperation()** obtiene un string que corresponda a uno de los 4 operadores disponibles: la suma, la resta, la multiplicación, y la división.


El primer *if* indica que si no hay ningún operando, entonces el número seguirá siendo el mismo. Dentro del *else if*, hace uso el método *doCalculation()* para realizar la operación deseada, y guarda tanto el resultado del número en la variable *currentNumber* como el primer operando. Luego, espera al usuario a introducir el segundo número para completar la operación.


### `clear()`
---
Este método sencillo hace que la calculadora cese toda operación. Hace que el número actual sea 0, y que las variables que contengan los operandos y el operador se vacíen. También restablece el valor de la variable booleana *waitForSecondNumber*.


### `doCalculation()`
---
Este es un método privado que solo se utiliza en el código JS de la calculadora. Este método lee qué operador se utilizó y qué números serán sometidos a la operación. Esto se lleva a cabo con un *switch* que lee el operador, y devuelve el resultado final.


---
## Desarrollo de la práctica


### Paso 4: Escuchar eventos de clic en los botones y obtener sus valores asociados
---
Para realizar esto, se tuvieron que añadir bindings de `(click)` dentro de `calculator.component.html` en cada uno de los botones disponibles.


Los botones que contenían números obtuvieron el evento `(click)=”getNumber(‘x’)”`, donde `x` es el número correspondiente a su botón. Asimismo, los botones con operadores (incluyendo el de “igual”), obtuvieron el evento `(click)=”getOperation(‘y’)”`, donde `y` es el operador correspondiente a su botón. Esto fue posible debido a que los valores se consideran cadenas de caracteres, y el código JS se encarga de realizar todo el trabajo necesario para que los valores sean obtenidos.


Hay dos casos especiales: el decimal y el AC. Con el decimal, se utilizó su propio método: `(click)=”getDecimal()”`, y con el botón de AC, se utilizó `(click)=”clear()”`.


El código de los métodos se introdujo dentro del archivo `calculador.component.ts`, y con ello, la calculadora ya es completamente funcional.


### Paso 5: Visualización del valor de las variables en la plantilla
---
Sin embargo, dentro de la plantilla, incluso si se hacen clic en los botones, no se mostrará nada. Esto se debe a que, aunque la lógica está funcionando, el valor del input está fijo en 0, por lo que no cambiará por mucho que se intente.


Por lo tanto, para que se muestre en pantalla, dentro de `calculator.component.html`, se tiene que modificar la línea del `ìnput` de la siguiente manera:
~~~
<input type="text" class="calculator-screen" value="{{currentNumber}}" disabled />
~~~
Con eso, la plantilla mostrará en número actual en tiempo real.
