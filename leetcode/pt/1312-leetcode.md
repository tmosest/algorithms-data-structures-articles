---
título: LeetCode 1312. Passos mínimos de inserção para fazer um Palíndromo de Cordas -
Descrição: Posicionador
Data: 2025-09-21
Categorias: []
autor: moses
etiquetas: []
hideToc: verdadeiro
---
## # # Mestre LeetCode 1312 – *Passos mínimos de inserção para fazer um palíndromo de cordas*
* (Um guia completo, pronto para entrevistas para Java, Python & C++) *

---

## # TL;DR
- **Problema**: Dado um string `s`, devolva o número * mínimo* de inserções necessárias para torná-lo um palíndromo.
- **Abordagem Optimal**: Subsequência Palindrômica Mais Longa (LPS) → `minInserções = .s. – LPS.
- **Complexidades**: 'O(n2)' tempo, 'O(n2)' espaço (pode ser reduzido para 'O(n)' se estiver confortável).
- ** Por Que Importa**: Este é um problema clássico de DP que mostra que você pode reduzir um problema de manipulação de strings para LCS/LPS. Os recrutas adoram.

---

Recapitulação de problemas

Texto
Entrada: s = "mbadm"
Saída: 2

Explicação:
"mbadm" → "mbdadbm" (inserir 'd' após 'b', 'a' antes de 'd')
Duas inserções são suficientes, e você pode provar que é mínimo.
«` `

- Comprimento de `s`: `1 ≤ 's' ≤ 500'
- Só letras inglesas minúsculas.

---

# # 2' Por que o LPS funciona

Uma inserção somente *adiciona caracteres *; ele nunca remove ou altera os existentes.
A subsequência mais longa que já é um palíndromo pode ficar intocada – só precisamos inserir os caracteres em falta.
Assim:

Texto
minInserções = □s – length_of_longest_palindromic_subsequence(s)
«` `

Encontrar o LPS é idêntico ao encontrar o LCS entre 's' e seu inverso (`rev(s)`).
É por isso que usamos o clássico ** Longest Common Subsequence DP**.

---

# # 3' DP Recorrência

Deixe `dp[i][j]` ser o comprimento do LCS de `s[0...i-1]` e `rev[0...j-1]`.

«` `
se s[i-1] == rev[j-1] → dp[i][j] = 1 + dp[i-1][j-1]
else → dp[i][j] = max(dp[i-1][j], dp[i][j-1])
«` `

Resposta: `n - dp[n][n]`, onde `n = s.length()`.

---

# # 4 # Complexidade

Complexidade
----------------------
Tempo (`n ≤ 500` → 250 k operações, trivial para qualquer idioma)
□ Espaço □ 'O(n2)' tabela DP (□ 250 k ints □ 1 MB)
(Opcional) (Reduzir o espaço para 'O(n)' por linhas de rolamento (não mostradas abaixo para clareza). □

---

Casos de borda e armadilhas comuns

Pitfall!
------------------
□ Esquecer de reverter a cadeia de caracteres □ `StringBuilder(s).reverse()` (Java), `s[::-1]’ (Python), `reverse()` (C++)
• indexação off-by-one em loops DP • Utilização `i <= n`, `j <= n` e acesso `s[i-1]» □
□ Grande uso de memória em array 2-D;

---

6 Implementos de Código

> . ** Todas as três versões usam a mesma lógica DP – apenas mudanças de sintaxe. **

## # 6.1 Java

```java
Solução de classe pública {
Inserções públicas(String s) {
int n = s.length();
String rev = novo StringBuilder(s).reverse().toString();

int[][] dp = nova int[n + 1][n + 1];

para (int i = 1; i <= n; i++) {
para (int j = 1; j <= n; j++) {
Se (s.charAt(i - 1) == rev.charAt(j - 1)) {
dp[i][j] = dp[i - 1][j - 1] + 1;
} outros {
dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
}
}
}
retornar n - dp[n][n];
}
}
«` `

## 6.2 Python

«```python
Solução de classe:
def minInserções(self, s: str) -> int:
n = len(s)
rev = s[::-1]
dp = [[0] * (n + 1) para _ no intervalo(n + 1)]

para i na gama(1, n + 1):
para j na gama(1, n + 1):
if s[i - 1] == rev[j - 1]:
dp[i][j] = dp[i - 1][j - 1] + 1
Caso contrário:
dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

retornar n - dp[n][n]
«` `

## # 6.3 C++

«```cpp
Classe Solução {
Público:
int minInserções( texto s) {
int n = s.size();
string rev(s.rbegin(), s.rend();
vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));

para (int i = 1; i <= n; ++i) {
para (int j = 1; j <= n; ++j) {
se (s[i - 1] == rev[j - 1])
dp[i][j] = dp[i - 1][j - 1] + 1;
outro
dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
}
}
retornar n - dp[n][n];
}
};
«` `

---

# # 7 # Testando sua solução

□ Teste □ Entrada
-------------------------
* "zzazz" * "0" *
2 * "mbadm" * .
3 , "code leet"
4 , "a" , "o"
5 , "ab" , "1"
6 "abca" 1
7 , "abcda"

Execute os testes de unidade fornecidos no seu IDE ou editor online do LeetCode para verificar a exatidão.

---

# # 8o Relevância do Mundo Real

- ** Editores de texto e IDEs**: Motores de verificação ortográfica e autocompleto precisam comparar strings com edições mínimas.
- ** Sequência de ADN**: Encontrar subsequências palindrômicas é essencial para a análise do genoma.
- **Compiladores**: Padrões palindrômicos ajudam no realce de sintaxe e verificação de sintaxe.

---

# Oh, não, não. Lições Home

Bom, mau, feio
----------------------
• Redução de problemas**: LPS → LCS → DP □ ⇩ Algumas soluções usam abordagens *brute-force* ou *recursivas* que explodem exponencialmente
Código modular**: Método de 'minInsertions' separado, reutilizável em entrevistas: usando 'HashMap' ou 'LinkedList', onde um array simples é suficiente.
Variante otimizada para o espaço**: DP unidimensional (se solicitado)

---

Bônus ####: Implementação Python otimizada por espaço (O(n))

«```python
def minInserções( s: str) -> int:
rev = s[::-1]
n = len(s)
prev = [0] * (n + 1)
para i na gama(1, n + 1):
cur = [0] * (n + 1)
para j na gama(1, n + 1):
cur[j] = prev[j - 1] + 1 se s[i-1] == rev[j-1] else max(prev[j], cur[j-1])
prev = cur
retornar n - prev[n]
«` `

---

# # # Por que este Blog ajuda você a ter um emprego

- **Conteúdo rico em palavras-chave**: “LeetCode 1312”, “palíndromo mínimo de inserções”, “entrevista de programação dinâmica”, “preparação de entrevista de engenheiro de software”.
- **Estrutura clara**: Introdução → Intuição → DP → Código → Testes → Takeaways.
- **Código acionável**: Excertos prontos para cópia para Java, Python, C++.
- ** Tom profissional**: Demonstra profunda compreensão dos conceitos algorítmicos.

> . **Quer mais guias prontos para entrevista?** Subscreva nossa newsletter ou confira a série completa em *Programação dinâmica, gráficos e estruturas de dados*.

---

## ## Final Code Cheat- Folha

```java
// Java
Classe Solução {
int minInserções públicas (String s) { /* DP como acima */ }
}
«` `

«```python
Python
Solução de classe:
def minInserções(self, s: str) -> int: # DP como acima
«` `

«```cpp
// C++
Classe Solução {
Público:
int minInserções( texto s) { / * DP como acima */ }
};
«` `

Copie, cole, corra e você está pronto para sua próxima pergunta de entrevista. Feliz codificação