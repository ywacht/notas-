## CONCEPTO FORMAL DE ESPACIO DE [BUSQUEDA]() 
	EL CONJUNTO DE todos los estados matematicamente alcanzables a partir de un estado inicial dado , optenidos mediante cualquier secuencia posibles de acciones validas .
```
S = (V , E)
```

### PROPIEDASES ESTRUCTURALES DEL ESPACIO DE ESTADOS 
	 B(factor de rAMIFICASION MEDIIO)
	 numero promedio sucesores generados por un nodp

	 D(profundidad maxima/ solucion )
	 longitud del camino tomado del estado inicial acia ala meta 


## grafos de los estados vz Arboles de busqueda
	el grafo implicito (el problema )
	 -topologia matematica real
	 -numero finitos de estados uniocs.
	 -posibilidad de ciclos (bucles)

![](../../Pasted%20image%2020260929153811.png)

	El arbol explicito (la exploracion)
	 -estructura generada en memoria 
	 -desenrolla el grafo
	 -crese infinitamente si no es controlado en ciclos 

![](../../Pasted%20image%2020260929153724.png)


## Representacion y Abtracion de estados 
	el arte del modelado matematicos la eliminacion sistematicos de detalle irrelevantes del mundo real para encapsuiar un problema infinito en un espacio de estados finito y computable .

## Tipos de Espacios de busqueda 
	Espacio finitos:
		limites discretos memorisables.
	 espacios dicretos :
		 trancisiones escalonadas claras 
	 Determinista :