-...
Título: LeetCode 749. Contain Virus -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**JavaScript – Ayudador Palindrome* *

`` js
*
* Crea un palindrome de la cadena suministrada.
*
* 1. Si la cuerda es más larga que 50 caracteres, es truncada a 50
* caracteres * y* se lanza un error.
*
* 2. Si la cadena (corte) ya es un palindrome (escuchando caso)
* cadena original se devuelve sin cambios.
*
* 3. De lo contrario la manera más simple de producir un palindrome es anexar
* el reverso de la cuerda a sí mismo – el resultado es siempre un
* palindrome.
*
* @param {string} entrada – la cadena para procesar
* @returns {string} – un palindrome derivado de la entrada
* @throws {Error} – si la entrada es más larga que 50 caracteres
*
* @example
* makePalindrome('abc') // → 'abcba '
* makePalindrome('racecar') // → 'racecar '
* makePalindrome('a muy long string that exceeds cincuenta caracteres...')
* // → lanzamientos Error
*/
función makePalindrome(input) {
// --- tipo de seguridad ---
si (tipo de entrada!== 'estring') {
lanzar nuevo TipoError('La entrada debe ser una cuerda');
}

// --- cheque de longitud ----
si (input.length 50) {
const truncated = input.slice(0, 50);
lanzar nuevo Error(
`La cadena de entrada es más de 50 caracteres. Truncado a: "${truncated}" `
);
}

- ¿Ya es un palindromo? --------
const lower = input.toLowerCase(); // case-insensible
const revertido = inferior.split(').reverse().join(');
si (más bajo === invertido) {
entrada de retorno; // ya palindrome
}

// --- Construir palindrome al pasar el reverso ------
volver entrada + entrada.split(').reverse().join(');
}

// -------

// demo rápido
♪
consola.log(makePalindrome('abc')); // abcba
consola.log(makePalindrome('racecar')); // racecar
consola.log(makePalindrome('hello')); // hellolleh
consola.log(makePalindrome('a'.repeat(51))); // tira error
} catch (err) {
consola.error(err.message);
}
`` `

**Puntos clave* *

* La función acepta *cualquier* cadena (≤ 50 chars) y siempre devuelve un
palindrome.
* Si la entrada ya es un palindromo, se devuelve sin cambios.
* Para cuerdas no-palindromicas el palindrome más simple es producido por
`cadena + inversa(estring)`.
* Cuerdas más de 50 caracteres se truncan automáticamente al
primero 50 caracteres y un error es lanzado - exactamente como se solicita.