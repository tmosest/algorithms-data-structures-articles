-...
Título: LeetCode 1758. Cambios Mínimos Para Hacer Pendiente Binaria Suplente -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**JavaScript (Node.js) – “Minium Changes to Make Alternating Binary String”* *
*Time O(n) Space O(1)*

`` js
/* Cambios Mínimos para Hacer Pendiente Binaria Suplente
- Sí.
Lee una cadena binaria de la línea de comandos (por ejemplo:
node solution.js 10010100
e imprime el número mínimo de giros de caracteres necesarios
para transformarlo en una cuerda perfectamente alternada
("1010..." o "0101...").

El algoritmo cuenta con desajustes cuando intentamos forzar el
patrón que comienza con '1' (es decir, 1,0,0,...).
Para cualquier posición i el dígito esperado es:
i%2===0 → '1' (porque el patrón comienza con '1')
I%2===1 → '0'
Si el dígito actual es igual al esperado, necesitamos cambiarlo,
Así que aumentamos el contador. El número de vueltas necesarias para el
patrón opuesto ("0101...") es simplemente
longitud - flipsForPatternStartingCon1
La respuesta es el mínimo de los dos.

El script no contiene funciones ni clases – sólo de nivel superior
código que se ejecuta en un solo archivo.
*/

const s = process.argv[2] Silencioso ''; // read binaria string from args

dar vueltasIniciarCon1 = 0;

// Cuenta desajustes para el patrón 1.0,1,0,...
para (que yo = 0; i) i++) {
si (parseInt(s[i], 10) === i % 2) {
flipsStartingWith1+;
}
}

// Mínimas vueltas entre los dos posibles patrones alternantes
resultado const = Math.min(flipsStartingWith1, s.length - flipsStartingWith1);

consola.log(resultar);
`` `

*Cómo correr*

``bash
# Ejemplo
node solution.js 10010100
# Output: 3
`` `

El script utiliza sólo funciones de JavaScript incorporadas, funciona en tiempo lineal y utiliza espacio adicional constante.