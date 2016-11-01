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

### A pensar

Suponé que R1 tiene el valof `6777` y que tenés la siguiente porción de memoria

<style type="text/css">
table {border-style:none}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;overflow:hidden;word-break:normal;border-style:none}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;overflow:hidden;word-break:normal;border-style:none}
.tg .celda{background-color:#ffffc7;text-align:center;vertical-align:top;border-style:none}
.tg .dir{background-color:#ffffff;text-align:center;vertical-align:top;border-style:none}
</style>

<table class="tg">
  <tr>
    <td class="dir">6775</td> <td class="celda">0010</td>
  </tr>
  <tr>
    <td class="dir">6776</td> <td class="celda">001A</td>
  </tr>
  <tr>
    <td class="dir">6777</td> <td class="celda">0014</td>
  </tr>
  <tr>
    <td class="dir">6778</td> <td class="celda">0000</td>
  </tr>
</table>

> ¿Que valor queda en R4 al ejecutar `MOV R4, [R1]`?