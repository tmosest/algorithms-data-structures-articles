---
titolo: LeetCode 1312. Passi di inserimento minimo per fare un Palindrome di stringa -
descrizione: Portaoggetti
data: 2025-09-21
categorie: []
autore: moses
[]
hideToc: vero
---
## 📌 Master LeetCode 1312 – *Minimo Inserimento passi per fare un Palindrome di stringa*
*(Una guida completa e pronta per l'intervista per Java, Python & C++) #

---

### TL;DR
- **Problem**: Data una stringa `s`, restituire il numero *minimo* di inserimenti necessari per renderlo un palindrome.
- **Optimal Approach**: Longest Palindromic Subsequence (LPS) → `minInsertions = |s| – LPS`.
- **Complexities**: `O(n2)` time, `O(n2)` space (può essere ridotto a `O(n)` se sei comodo).
- **Perché Matters**: Questo è un classico problema DP che mostra che è possibile ridurre un problema di manipolazione delle stringhe a LCS/LPS. I reclutatori lo adorano.

---

# 1️⃣ Problem Recap

``text
Input: s = "mbadm"
Uscita: 2

Spiegazione:
"mbadm" → "mbdadbm" (inserto 'd' dopo 'b', 'a' prima 'd')
Due inserzioni sono sufficienti, e si può dimostrare che è minimo.
# #

- Lunghezza `s`: `1 ≤ |s| ≤ 500`
- Solo lettere inglesi minuscole.

---

# Perché LPS funziona

Un inserimento solo *adds* caratteri; non rimuove mai o cambia quelli esistenti.
La più lunga sottosequenza che è già un palindrome può rimanere intatta – abbiamo solo bisogno di inserire i personaggi mancanti.
Così:

``text
minInserzioni = |s| – long_of_longest_palindromic_subsequence(s)
# #

Trovare il LPS è identico a trovare il LCS tra `s` e il suo contrario (`rev(s)`).
Ecco perché usiamo il classico **Longest Common Subsequence DP**.

---

## 3️⃣ D Ricorso

Let `dp[i][j]` essere la lunghezza del LCS di `s[0...i-1]` e `rev[0...j-1]`.

# #
se s[i-1] == rev[j-1] → dp[i][j] = 1 + dp[i-1][j-1]
altro → dp[i][j] = max(dp[i-1][j], dp[i][j-1])
# #

Risposta: `n - dp[n][n]`, dove `n = s.length()`.

---

## 4️⃣ Complessità

| Metric | Complessità |
-----
| Time | `O(n2)` (`n ≤ 500` → operazioni da 250 k, banali per qualsiasi lingua) |
| Spazio | `O(n2)` tavolo DP (≈ 250 k ints ≈ 1 MB) |
| Optional | Ridurre lo spazio a `O(n)` da filari rotanti (non mostrati qui sotto per chiarezza). #

---

## 5️⃣ Bordo Cases & Common Pitfalls

| Pitfall | Fix |
Traduzione:
| Dimentica di invertire la stringa | `StringBuilder(s).reverse()` (Java), `s[:-1]` (Python), `reverse()` (C++)
| Indicizzazione off-by-one in loop DP | Utilizzare `i <= n`, `j <= n` e accedere `s[i-1]` #
# Grande uso della memoria su 2-D array | `vector Пvector > dp(n+1, vector <int>(n+1, 0)); ` va bene per n ≤ 500 |

---

## 6️⃣ Attuazioni del codice

> > ** Tutte e tre le versioni utilizzano la stessa logica DP – solo cambiamenti di sintassi. E' una cosa da fare.

## 6.1 Java

♪ ``java
Soluzione di classe pubblica (')
int public minInserzioni(String s) {
int n = s.length();
String rev = nuovo StringBuilder(s).reverse().toString();

int[][] dp = nuovo int[n + 1][n + 1];

per (int i = 1; i <= n; i++) {
per (in j = 1; j <= n; j++) (')
se (s.charAt(i - 1) == rev.charAt(j - 1)) {
dp[i][j] = dp[i - 1][j - 1] + 1;
} altro {
dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
#
#
#
ritorno n - dp[n][n];
#
#
# #

## 6.2 Python

♪ ``python
Soluzione di classe:
de minInserzioni(io, s: str) -> Int:
n = len(s)
rev = s[:-1]
dp = [[0] * (n + 1) per _ in range(n + 1)]

per i nella gamma(1, n + 1):
per j in gamma (1, n + 1):
se s[i - 1] == rev[j - 1]:
dp[i][j] = dp[i - 1][j - 1] + 1
Altro:
dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]

torna n - dp[n]
# #

## 6.3 C++

#
Soluzione di classe {
pubblico:
int minInserzioni(stringa s) {
int n = s.size();
rev(s.rbegin(), s.rend());
> dp(n + 1, vettore > (n + 1, > n + 1, 0);

per (int i = 1; i <= n; ++i) (')
per (in j = 1; j <= n; ++j) {
se [i - 1] == rev[j - 1]
dp[i][j] = dp[i - 1][j - 1] + 1;
Altro
dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
#
#
ritorno n - dp[n][n];
#
}
# #

---

## 7️⃣ Testare la tua soluzione

# Test | Input | atteso |
Traduzione:
| 1 | `"zzazz"` | `0` |
| 2 | `"mbadm"` | `2` |
| 3 | `"leetcode"` | `5` |
| 4 | `"a"` | `0` |
| 5 | `"ab"` | `1` |
| 6 | `"abca"` | `1` |
| 7 | `"abcda"` | `2` |

Eseguire i test unità forniti nel vostro editor IDE o LeetCode online per verificare la correttezza.

---

## 8️⃣ Rilevamento mondiale

- ** Editor di testo & IDEs**: I motori Autocomplete e spell-checker devono confrontare stringhe con modifiche minime.
- #DNA Sequencing # Trovare sottosequenze palindromiche è essenziale per l'analisi del genoma.
- **Compilers**: I modelli Palindromici aiutano a evidenziare la sintassi e a controllare la sintassi.

---

## 9️⃣ Take- Home Lezioni

| Good | Bad | Ugly |
Traduzione:
| ✅ Clear **problem loss****: LPS → LCS → DP | 😉 Alcune soluzioni utilizzano *brute‐force* o *recursive* approcci che esplodono esponenzialmente | ↓ Dimenticare la stringa *reverse* o indicizzare fuori da una causa risposte sbagliate |
| ✅ **Codice modulare**: Metodo di `minInsertions` separato, riutilizzabile nelle interviste | Allegato Over‐engineering: utilizzando `HashMap` o `LinkedList` dove una semplice matrice basta | 日 Usando recursion senza memoization porta a impoverimento |
| ✅ **Space-optimised variant**: one-dimensional DP (se richiesto) | agganciare le lingue nella stessa repo senza separazione chiara | Allegato Unnecessary print/debugging dichiarazioni che clutter logs |

---

## 🔧 Bonus: Space‐Optimised (O(n) Python Implementation

♪ ``python
> Int:
rev = s[:-1]
n = len(s)
* (n + 1)
per i nella gamma(1, n + 1):
* (n + 1)
per j in gamma (1, n + 1):
[j] = prev[j - 1] + 1 se s[i-1] == rev[j-1] altro max(prev[j], cur[j-1])
prev = cur
torna n - prev[n]
# #

---

## 🎯 Perché questo blog ti aiuta a trovare un lavoro

- **Contenuto ricco di parole chiave**: “LeetCode 1312”, “minimo insertions palindrome”, “intervista di programmazione dinamica”, “software engineering prep”.
- **Clear struttura**: Intro → Intuizione → DP → Codice → Test → Takeaways.
- **Codice azionabile**: Snippet pronti per Java, Python, C++.
- Tono confessionale. Dimostra la comprensione profonda dei concetti algoritmici.

> > **Cerca altre guide per interviste?** Iscriviti alla nostra newsletter o controlla la serie completa su *Programmazione dinamica, grafici e strutture dati*.

---

## 📚 Codice finale Cheat‐ Foglio

♪ ``java
// Java
Soluzione di classe {
minInserzioni pubbliche (String s) { /* DP come sopra */ }
#
# #

♪ ``python
# Python #
Soluzione di classe:
de minInserzioni(io, s: str) -> int: # DP come sopra
# #

#
// C++
Soluzione di classe {
pubblico:
int minInserzioni(stringa s) { /* DP come sopra */ }
}
# #

Copia, incolla, esegui e sei pronto per la tua prossima domanda intervista. Codifica felice