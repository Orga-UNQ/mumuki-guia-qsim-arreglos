En esta guía conoceremos las colecciones de elementos que denominamos arreglos. 

**Arreglo de valores**: es una Colección de elementos, contenidos en posiciones de memoria consecutivas, donde cada elemento puede ocupar más de una celda, o menos. Pero *todos ocupan lo mismo*

De una arreglo debemos conocer dos cosas:

* Tamaño:Cantidad de elementos
* donde termina:
  * Conocemos la cantidad de elementos
  * O tenemos una condición de fin 
  

Veamos un ejemplo. Supongamos que en una porción de memoria tenemos una colección de pedidos de empanadas. Cada celda contiene la cantidad de empanadas de un pedido, y la colección termina con una celda cuyo contenido es **0**, pues no tiene sentido llevar registro de un pedido de 0 empanadas.



<style type="text/css">
table {border-style:none}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;overflow:hidden;word-break:normal;border-style:none}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;overflow:hidden;word-break:normal;border-style:none}
.tg .celda{background-color:#ffffc7;text-align:center;vertical-align:top;border-style:none}
.tg .dir{background-color:#ffffff;text-align:center;vertical-align:top;border-style:none}
</style>

<table class="tg">
  <tr>
    <td class="dir">A000</td> <td class="celda">0010</td>
  </tr>
  <tr>
    <td class="dir">A001</td> <td class="celda">001A</td>
  </tr>
  <tr>
    <td class="dir">A002</td> <td class="celda">0014</td>
  </tr>
  <tr>
    <td class="dir">A003</td> <td class="celda">0000</td>
  </tr>
</table>

