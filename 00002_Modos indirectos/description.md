### Modo indirecto

El modo indirecto tiene dos formatos:

* por registro, donde la sintaxis es [Rx], siendo Rx un registro de la CPU
* por memoria, donde la sintaxis es [[0x????]], siendo 0x???? cualquier dirección de memoria.

Veamos un programa que suma entonces los elementos de un arreglo que comienza en 
`0xA000` y termina con el primer valor cero:

```
sumArreglo:
      MOV R3,0x000
      Mov R0, A000  --> inicializamos el indice
arriba: Mov R1, [R0]
      CMP R1 , 0x0000
      JE fin
      ADD R3, R1
      ADD R0, 0x0001 
      JMP arriba
fin: RET
```


### Un elemento a la vez

Supongamos ahora que necesitamos escribir un programa que calcule el promedio entre los valores del arreglo, y sabemos que el promedio se calcular parcialmente. Es decir que el promedio entre 3 valores puede calcularse de dos formas:

* (a+b+c)/3
* ((a+b)/2) + c )/2

La primera tiene en cuenta cuantos elementos en total se tienen (en el ejemplo, 3) y la ultima expresión muestra que puedo calcularlo sin saber cuantos son. 

Usemos esa idea para escribir la rutina:

```
promArreglo:
      MOV R3,0x000
      Mov R0, A000  
arriba: Mov R1, [R0]
      CMP R1 , 0x0000
      JE fin
      
      ADD R3, R1     *
      DIV R3,0x0002  *
      
      rADD R0, 0x0001 
      JMP arriba
fin: RET
```

### Desacoplar

En el codigo de la rutina anterior vemos que hay un conjunto de instrucciones que se encarga de procesar un solo elemento del arreglo. Sería de mucha utilidad desacoplarlo en otra rutina auxiliar, que tiene la siguiente documentación:

```
RUTINA avg
Requiere: en R1 un valor a promediar y en R3 el promedio parcial
Modifica: --
Retorna: El promedio entre R3 y R1, es decir: R3=(R3+R1)/2
```

Utilizando dicha rutina, el programa anterior queda:



```
promArreglo:MOV R3,0x000
      Mov R0, A000  
arriba: Mov R1, [R0]
      CMP R1 , 0x0000
      JE fin
      
      CALL avg
      
      ADD R0, 0x0001 
      JMP arriba
fin: RET
```

### A trabajar

> Escribí la rutina `avg`