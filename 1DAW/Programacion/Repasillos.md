# Ternario
`expresionLogica ? valorTrue : ValorFalse`

# Operadores lógicos

- &&
 A       B      A&&B
falso falso falso
cierto falso falso
falso cierto falso
cierto cierto cierto
- ||
A       B       A||B
flaso falso falso
cierto falso cierto
falso cierto cierto
cierto cierto cierto

# Switch

```java
switch (expresion) {
case 1 -> {}
case 2 -> {}
default -> {}
}
diasDelMes = switch(mes){
case 1 -> {}
case 2 -> {}
default -> {}
};
```

# Recursividad
Llamamos a una función dentro de la función, creando un ciclo infinito, tenemos que controlar como salir. 

```java
int funcionRecursiva(datos) {
	int resultado;
	if (caso base){
		resultado = valorBase;
	} else {
		resultado = funcionRecursiva(nuevosDatos);//llamada recursiva
			... lo que vayamos a hacer...
	}
	return (resultado);
}
```

