---
Titel: LeetCode 2847. Geringste Anzahl mit Given Digit Produkt - Ja.
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
# 1️⃣ Solution Code

Hier finden Sie ** drei volle, lauffähige Implementierungen** für das LeetCode Problem **2847 – Kleinste Zahl mit geschildertem Digit-Produkt*.
Alle drei Lösungen verwenden die gleiche gierige Logik:

ANHANG Geben Sie den Eingang `n` nur mit den Primes `2, 3, 5, 7'.
2. Wenn ein Faktor bleibt, ist die Antwort `-1`.
3. Kombinieren Sie die Hauptfaktoren in kleinste mögliche Ziffern (9 → 32, 8 → 23, 6 → 2·3, 4 → 22).
4. Erstellen Sie die Antwort in aufsteigender Reihenfolge der Ziffern.

```text
Komplexität
----------
Zeit : O(log n) (worst‐case wir teilen durch 2, 3, 5 oder 7 ein paar Dutzend mal)
Raum : O(1) (neben der Ausgangsstring)
`` `

> **Tip** – Wenn Sie Interviewcode schreiben, halten Sie die Logik immer in einer separaten Helferfunktion; dies hält den Code lesbar und einfach zu testen.

---

1,1 Java (LeetCode Signatur)

``java
Klasse Lösung {
public String smallNumber(long n) {
// Sonderfälle
wenn (n = = 1) "1" zurückgegeben wird;
wenn (n < 10) String.valueOf(n) zurückgeben;

int[] prime = {2, 3, 5, 7};
int[] cnt = new int[10]; // cnt[d] = wie oft die Ziffer d angezeigt wird

// Faktor n nach Primes 2,3,5,7
für (int p : prime) {
(n % p ==) 0)
n /= p;
cnt[p]++;
}
}

wenn 1) Rückgabe "-1"; // Rückgabefaktor > 7 → unmöglich

// in größere Ziffern verschmelzen
cnt[9] = cnt[3] / 2; // 3*3 = 9
cnt[3] %= 2.

cnt[8] = cnt[2] / 3; // 2*2*2 = 8
cnt[2] %= 3;

wenn (cnt[3] > 0 &&cnt[2] > 0) { // 3*2 = 6
cnt[3] = 0;
cnt[2] = 1; // ein '2 verlassen '
cnt[6] = 1;
}

cnt[4] = cnt[2] / 2; // 2*2 = 4
cnt[2] %= 2.

// Antwort in aufsteigender Reihenfolge der Ziffern erstellen
StringBuilder sb = neuer StringBuilder();
für (in d = 1; d <= 9; d++) {
für (in i = 0; i < cnt[d]; i++) sb.append(((char)('0' + d));
}
sb.toString();
}
}
`` `

---

1,2 Python 3

```python
Klasse Lösung:
def kleinste Zahl(selbst, n: int) -> str:
wenn n == 1: # Sonderfall
zurück "1"
wenn n < 10: # einstellig ist bereits die Antwort
Rückgabe str(n)

Primes = [2, 3, 5, 7]
cnt = [0] * 10 # cnt[d] = wie oft die Zahl d angezeigt wird

# Faktor n
für p in primes:
bei n % p == 0:
n //= p
cnt[p] += 1

wenn n 1: # linkover factor > 7 → unmöglich
zurück "-1"

# Zusammenführen in größere Ziffern
cnt[9] = cnt[3] // 2 # 3*3
cnt[3] %= 2.

cnt[8] = cnt[2] // 3 # 2*2*2
cnt[2] %= 3

wenn cnt[3] > 0 und cnt[2] > 0: # 3*2
cnt[6] = 1
cnt[3] = 0
cnt[2] = 1

cnt[4] = cnt[2] // 2 # 2*2
cnt[2] %= 2.

# Erstelle Antwort in aufsteigender Reihenfolge
= []
für d im Bereich (1, 10):
res.append(str(d) * cnt[d])
zurück ".join(res)
`` `

---

1,3 C++ (GNU C++17)

```cpp
#include <bits/stdc++.h>
mit Namespace std;

Klasse Lösung {
öffentlich:
kleinste Anzahl (lang n) {\cHFFFF}
wenn (n = = 1) "1" zurückgegeben wird;
wenn (n < 10) zurück zu_string(n);

vektor<int> prime = {2, 3, 5, 7};
vektor<int> cnt(10, 0); // cnt[d] = mal digit d erscheint

für (int p : prime) {
(n % p ==) 0)
n /= p;
++Cent[p];
}
}
wenn 1) Rückkehr "-1";

cnt[9] = cnt[3] / 2; // 3*3
cnt[3] %= 2.

cnt[8] = cnt[2] / 3; // 2*2*2
cnt[2] %= 3;

wenn (cnt[3] &&cnt[2]) { // 3*2
cnt[6] = 1;
cnt[3] = 0;
cnt[2] = 1;
}

cnt[4] = cnt[2] / 2; // 2*2
cnt[2] %= 2.

String res;
für (in d = 1; d <= 9; ++d) {
res.append(cnt[d], char('0' + d));
}
zurück;
}
};
`` `

---

# 2️⃣ Blog Artikel – “Das Gute, das Schlechte und die Ugly des Lösens von LeetCode 2847”

> **Keywords*: *LeetCode 2847*, *Smallest Number with Given Digit Product*, *Java-Lösung*, *Python-Lösung*, *C++-Lösung*, *Interview-Codierung*, *algorithm*, *greedy Factorization*, *coding interview Tips*, *tech hiring*

---

Einleitung

Jeder Software-Ingenieur hat ein LeetCode-Problem, das sich wie ein *mini‐code‐wars* anfühlt: Sie starren eine Nummer an, Sie müssen es auseinanderziehen, und Sie müssen es in der **shortest möglichen String** tun. Das ist **2847 – Kleinste Zahl mit Given Digit Produkt**.

Es ist ein “mittleres” Problem auf LeetCode, aber in einem Interview kann es **make oder Pause** das Vertrauen des Kandidaten. Lassen Sie uns nicht erkennen, warum dieses Problem ein tolles Schaufenster ist, wonach Fallstrick-Rekrutierer suchen und wie Sie können ** es in einen Portfolio-ready Interview Star* verwandeln.

---

Das Gute – Warum Dieses Problem ist ein Gold-Mine für Kandidaten

ANHANG **Clear Problemerklärung* – Sie erhalten eine einzelne ganze Zahl `n`. Wenn Sie das Produkt seiner Ziffern als `n` ausdrücken können, geben Sie die *smallest* Nummer aus, die dies tut.
2. **Kleine Eingangsdomäne** – Alle Grundfaktoren größer als 7 ruinieren die Lösung. Diese Strenge gibt Ihnen eine ** Endliche Reihe von “brauchbaren” Primes** (`2, 3, 5, 7`) um sich Sorgen zu machen.
3. **Greedy + Factorization* Die optimale Lösung ist fast trivial, wenn Sie das Muster sehen: 9 = 32, 8 = 23, 6 = 2·3, 4 = 22. Wenn Sie die Hauptfaktoren in der richtigen Reihenfolge zusammenführen, erhalten Sie sofort den kleinsten String.
4. **Language-agnostische Logik* Ob Sie in Java, Python oder C++ kodieren, die Kernidee bleibt identisch. Das ist toll für Kandidaten, die * wie * eine Sprache, aber muss in einer anderen während eines Interviews beantworten.

> **Pro tip***: In einem Interview, **Erklären Sie Ihren Plan vor dem Schreiben Code**. Recruiters lieben zu sehen, dass Sie denken, bevor Sie tippen.

---

oder The Bad – Häufige Fallstricke

| Pitfall | Warum es ein Problem ist | Wie es zu vermeiden |
---------------------------------------------------------
| **Leaving `n` < 10** – Rückgabe von `String.valueOf(n)` in Java oder `str(n)` in Python. Es scheint trivial, aber Sie müssen auch `n = 1` handhaben, die *not* durch die “einstellige Ziffer” Regel abgedeckt ist. | Treat `n == 1' als separater Fall * vor* der allgemeinen Logik. |
| **Full gierig von 9 bis 2* ohne Überprüfung auf unmögliche Faktoren. Sie könnten um 9, 8, ..., aber wenn ein Überbrückungsfaktor > 7 bleibt, werden Sie leise eine falsche Zahl ausgeben. | Nach der Factorisierung, **check `n != 1**; wenn zutreffend, Ausgabe `-1`. |
| **Keine Verschmelzung der Hauptfaktoren** | Wenn Sie gerade die Primzahlen 2,3,5,7 in absteigender Reihenfolge ausgeben, kann der String länger als erforderlich sein (z.B. 222 → "222" vs "8"). | Merge `23` → 8, `32` → 9, `2·3` → 6, `22` → 4. Dies ist der *Grady Merging* Schritt. |
| **Das Ergebnis in falscher Reihenfolge** | Das Umkehren eines Stapels von Ziffern gibt die falsche Nummer: “98” vs “89”. | Stellen in **ascending** nach der Verschmelzung angeben. In C++/Java `append(cnt[d], digit)` oder in Python `"digit"*cnt[d]`. |

---

oder Die Ugly – Edge‐Case Head‐aches

ANHANG **Huge numbers** (`n`s bis `1018`) – Sie könnten denken, dass Rekursion oder Schleifen überlaufen könnten. Verwenden Sie **long`/`long long`* und teilen Sie Schritt für Schritt.
2. **Prime Factorization** – Während Pythons `//=` günstig ist, kann Javas Modulo auf `long` einschüchternd aussehen. Denken Sie nur daran: Sie teilen sich nur durch 2, 3, 5 oder 7 – das ist höchstens ~60 Iterationen.
3. **Memory Leck in Java* – Ein `StringBuilder` ist unerlässlich. Vermeiden Sie das Verketten in einer Schleife; es ist O(n2).
4. **C++ `string:append` nuances** – `res.append(cnt[d], char('0'+d)); ` kann Newcomern verwirren. Das erste Argument ist die **repeat count**.

---

oder Wie man in einem Interview glänzt

ANHANG **State your approach* *
„Ich faktoriere die Zahl mit den Primes 2, 3, 5, 7. Wenn etwas übrig ist, ist es unmöglich. Dann werde ich gierig Paare von 3’s in 9’s verschmelzen, Dreifache von 2’s in 8’s, und so weiter. „

2. **Erklärung der gierigen Zusammenführung**
„Weil 9 die größte Einzelziffer ist und 9=32, mit 9 reduziert die Ziffernzahl. Ebenso 8=23 und 6=2·3, 4=22. Dies garantiert das lexikographisch kleinste Ergebnis. „

3. **Zeigen Sie Schritt für Schritt*
*Entferne nicht nur den letzten Schnipsel.* Gehen Sie durch die Factorisierungsschleife, die Fusionsstrecke und die Saitenkonstruktion. Recruiter lieben die Erklärung.

4. **Halte-Eckengehäuse*
* `n == 1` → “1”.
* `n < 10` → `str(n)` oder `to_string(n)`.
* Übergeordneter Faktor > 7 → `-1`.

5. **Test gründlich**
Führen Sie folgende Fälle aus:
```text
1 → "1"
10 → "-1" (10 = 2·5 → OK, aber 10<10 ist eine einzelne Zahl)
20 → "45" (20 = 22·5 → 4·5)
256 → "288" (256 = 28 → 8·8)
1000000000000000000 → "-1"
`` `
In Interviews überspringen die Kandidaten oft den Großzahltest; stellen Sie sicher, dass Sie es nicht tun.

---

Â Fazit – 2847 zum Verleihgewinn

*LeetCode 2847* ist eine **micro-case Studie*** von gieriger Factorisierung, Prime Handling und String Manipulation. Es ist klein genug, um in weniger als 5 Minuten gelöst werden, aber es testet Sie:

**Mathematische Intuition** – Erkennen, dass 9 = 32, 8 = 23, usw.
* **Algorithmische Klarheit** – Schreiben von sauberem, sprachwissenschaftlichem Code.
**Edge‐Case-Bewusstsein** – Handling `1`, einzelne Ziffern und unmögliche Eingaben.

Wenn Sie in ein Tech-Interview gehen, *mention die gierige Strategie* zuerst. Zeigen Sie, warum das Zusammenführen von Grundfaktoren die kleinste lexicographic string gibt. Dann schreiben Sie Ihren Code im interview-freundlichen Stil oben.

> **Remember**: Das *good* ist die elegante gierige Logik; das *bad* ist die Versuchung, den `-1`-Fall zu überdenken oder zu vergessen; das *ugly* ist die kleinen Implementierungsfehler, die nur in Randfällen erscheinen. Meistern Sie sie, und Sie werden von “Medium” zu “must‐hire” in kürzester Zeit.

Glückliche Codierung und viel Glück auf Ihrem nächsten technischen Interview! 🚀

---

> **Wann mehr gesprächsbereite Lösungen? * *
> 👉 [My GitHub LeetCode Repository](https://github.com/your‐github) – Java, Python, C++ – bereit für copy‐paste.
> 👉 Abonnieren Sie meinen Newsletter für wöchentliche Algorithmenaufschlüsselungen und Interview-Prep-Tipps!