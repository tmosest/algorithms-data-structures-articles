-...
Título: LeetCode 555. Split Concatenated Strings -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Respuesta*

El problema de la “concatenación rotacional” es, de hecho, un problema clásico de la manipulación de cuerdas: la rotación **minimum (lexicográficamente más pequeña)** (a veces llamada el cambio cíclico *menos* o el problema del cambio cíclico mínimo*).

La forma estándar de resolverlo es unir primero todas las piezas en una cadena larga (por ejemplo, "BABC" para la lista '['B','AB','C']). Luego ejecuta un algoritmo de tiempo lineal como **El algoritmo de Booth** (o usa un enfoque de sufijo-array/rolling-hash) para encontrar el índice de la rotación lexicográfica más pequeña de esa cadena concatenada. La rotación que comienza en ese índice es el único orden “válido” que está buscando.

Si, por alguna razón, sólo quieres considerar rotaciones que comienzan en un límite de palabras (así que las palabras no se dividen), simplemente prueba cada una de las rotaciones posibles N (cada palabra se convierte en la primera pieza) y elige la lexicografía más pequeña. Esto es trivial para hacer en el tiempo O(N·L) (o con un algoritmo de estilo Booth restringido a esas posiciones de inicio N).

En resumen, el problema es el problema de rotación léxico ** (o “menos cambio cíclico”), y puede ser resuelto en tiempo lineal por el algoritmo de Booth (o equivalentemente por duplicación de cuerdas con un sufijo-array, sufijo-árbol, o incluso la comparación de fuerza bruta para una pequeña N).