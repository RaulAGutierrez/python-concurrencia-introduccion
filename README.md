# To `join()` or not to `join()`...

En `dormilones.py` vimos tres ejemplos básicos de ejecución:

- Clásico secuencial,
- Con threads,
- Y con threads, pero esperando a que terminen usando `join()`.

Entonces responda:
- ¿Por qué los segundos que se imprimen que pasaron son 2, 0 y 1 (aprox.) respectivamente?
Por en el primer ejemplo, los procesos se ejecutan al terminar el anterior, en el segundo caso, el proceso del hilo principal (main) termina antes que el proceso de dormir instanciado en otros dos hilos termine, y el tercer ejemplo el hilo principal espera que los hilos de las instancias de dormir, terminen, para  finalizar.
- ¿Cuántos hilos o threads hay en cada caso?
en el primer ejemplo hay 1, en el los dos ejemplos siguientes, 3 en cada uno.
- Los últimos dos ejemplos tienen la misma cantidad de threads cada uno, ¿cuál sería la diferencia entonces?
que en el ultimo ejemplo el principal, espera a que los hilos que instancian dormir(), terminen.
- En el último ejemplo, ¿qué desventaja o desventajas le ve al uso del `join()`?
En verdad es una ventaja. Mejora el tiempo respecto al primero ejemplo y ademas asegura que todos los hilos del codigo terminen.


# Muchos threads

En `muchosThreads.py` hay algunas cosas básicas de Python:
- `from tiempo import Contador` importa desde `tiempo.py` la clase `Contador`.
- Cómo crear una lista vacía.
- Cómo hacer un loop con cantidad de iteraciones fija.
- Cómo agregar elementos (al final) a una lista.
- Cómo hacer un loop que itere sobre una lista.

## Parte 1
Mirá el código y fijate de entender la sintaxis. 

## Parte 2
Ahora corré el script: ¿por qué tarda lo que tarda? 
Porque genera una lista de hilos, que tienen un duracion de 1.5 seg. Cuando termina el for que genera esta lista, se estable otro que espera que termine cada uno. La ejecucion de los for es secuencia por parte del hilo principal, pero la finalizacion de cada hilo, es independiente dentro de la lista.

# Intercalación en concurrencia

**Dos reglas importantes** para `contadorConcurrente.py`:
- Mirá el código pero _no lo ejecutes_,
- Mirá el código pero _no lo ejecutes_.

(Referencia [The First Rule of Fight Club (1999)](https://www.youtube.com/watch?v=dC1yHLp9bWA))

Mirando el código de `contadorConcurrente.py`, pero sin ejecutarlo:
- Al ejecutar la función `cuenta()`, ¿cuántas veces se ejecuta el `for` que tiene adentro, y qué hace cada iteración del `for`?
cuántas veces se ejecuta el `for` que tiene adentro?: 500000 veces.
qué hace cada iteración del `for`?: suma un 1 en la variable global counter, en cada iteracion.
- ¿Es verdad que cada thread lanza una ejecución de la función `cuenta()`?
Si. 
- ¿Es verdad que se está esperando a que termine cada thread?
Si.
- ¿Cúal te parece que es el valor que se imprime de `counter`?
1000000.

Ahora corré `contadorConcurrente.py`:
- Correlo varias veces, ¿qué observás que pasa?
Da disintos valores.
- ¿Por qué está pasando eso que observás?
Porque amdos hilos, acceden simultaneamente al valor sin que el otro haya terminado.


# ¿Secuencial clásico, concurrente o paralelo?

Para cada una de las siguiente situaciones, decidí si es secuencial clásico, concurrente o paralelo. Intentá justificar señalando las ideas esenciales de cada caso.

- Cuál persona de un total de 50 corre más rápido una maratón.
    - opción 1) Cada persona corre secuencialmente en la pista, y medimos cada tiempo. Secuencial. Dado que se repite el proceso de control de tiempo segun la cantidad de personas que corren, sobre la misma pista, y al finalizar todas las mediciones se elige al mas rapido.
    - opción 2) Todas las personas corren en la misma pista, y la que llega primero listo. Concurrente.
		- Preguntas: ¿hay algún recurso compartido? ¿genera problemas? Si, e tal caso, puede ser que no todas las personas entren en la pista por ejemplo, y/o que una persona que sea rapida no pueda demostrar eso, dado que la pista va a estar colapsada. O No, ya que si la pista es lo suficientemente grande para que corran 50 personas, se va a poder medir quien es el mas rapido, en igualdad de condiciones y reglas claras de medicion, como largada y llegada. El recurso compartido seria la pista y los metodos de medicion.
    - opción 3) Cada persona corre en una pista distinta, todas al mismo tiempo. Paralelo.
		- Pregunta: ¿hay un aumento de recursos respecto al anterior?. Si, se van a necesitar N cantidad de pistas para que la personas corran simultaneamente.
    - Pregunta: ¿pros y contras de cada opción?
    En la opcion1, se demora mas tiempo en llegar al resultado. En la opcion2, dependiente de los recursos con los que se cuenta, se pude obtener resultados validos dependiendo de que tambien los metodos de medicion sean correctos, y en la opcion3, hay un gran incremente en los recursos necesarios para ejecutar lo necesario.    
    
- Competencia de triples en basquet: quién mete más en 10 intentos.
    - opción 1) Cada persona secuencialmente realiza 10 intentos, y anotamos la cantidad de triples. Secuencial. Se establece un orden de ejecucion, y hasta no terminar los 10 intentos, no se pasa a la siguiente persona.
    - opción 2) Todas las personas tiran los 10 intentos al mismo tiempo. Concurrente.
		- Preguntas: ¿hay algún recurso compartido? ¿genera problemas?. Si, el aro y el metodo de medicion es compartidos, y teniendo especial cuidado en el metodo de contar los intentos de cada persona hace contra el aro. El problema en cuestion, es que los controles que cuentan los triples, no sean buenos y que le asignen puntos a otras personas, por ejemplo.
    - opción 3) Cada persona tira en un aro distinto, todas al mismo tiempo. Paralelo. cada persona tiene su propio aro, y un control de medicion de puntos propio, por lo que se necesitarian mas recursos.
    - Pregunta: ¿pros y contras de cada opción?. 
    En la opcion1, se necesita mas tiempo para poder medir correctamente la cantidad de puntos por persona, en la opcion2, detener un metodo de medicion de puntos, no habria problema, dado que todas las personas tirarian la mismo tiempos, si no se puede controlar la medicion, este metodo no es confiable, y en la opcion3, se necesitan mas recursos para poder medir los intentos.
