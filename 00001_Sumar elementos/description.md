Necesitamos saber cuantas empanadas se pidieron en total, es decir realizar la suma de todos los elementos del arreglo ¿como lo resolvemos?

Vemos que una posibilidad es una rutina como la que sigue:

```
MOV R5, 0x0000
ADD R5, [0xA000] 
ADD R5, [0xA001] 
ADD R5, [0xA002] 
ADD R5, [0xA003] 
```

Pero esto no es correcto porque ademas de no ahorrar trabajo al programador  :muscle: no conocemos su tamaño, sino que termina en el primer valor 0, es decir que el tamaño del arreglo es dinámico. 

 :disappointed_relieved:

Pues bien, todo indica que queremos repetir para cada elemento: 

``` 
ADD R5, valor-del-elemento
```

donde el `valor-del-elemento` es algo que cambia con las distintas posiciones de memoria. Dicho de otra manera:


``` 
ADD R5, [dirección-del-elemento]
```

Con esto último vemos que la dirección tiene que ir cambiando, es decir que debe ser una variable. Esta variable puede ser un registro y podríamos escribir algo así:

``` 
ADD R5, [R1]
```

donde R1 tiene el valor `A000` y luego `A001`, `A002`, y así siguiendo.

La buena noticia es que lo anterior es correcto en Q6, y se denomina **Modo de direccionamiento indirecto por registro**.

 :clap:

### Modo indirecto

El modo indirecto tiene dos formatos:

* por registro, donde la sintaxis es [Rx], siendo Rx un registro de la CPU
* por memoria, donde la sintaxis es [[0x????]], siendo 0x???? cualquier dirección de memoria.

Veamos un programa que suma entonces los elementos de un arreglo que comienza en 
`0xA000` y termina con el primer valor cero:

```
      MOV R3,0x000
      Mov R0, A000  // inicializamos el indice
arriba: Mov R1, [R0]
      CMP R1 , 0x0000
      JE fin
      ADD R3, R1
      ADD R0, 0x0001 
      JMP arriba
fin: RET
```
