
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


### 