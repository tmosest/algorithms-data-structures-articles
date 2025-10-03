---
Titel: LeetCode 2531. Stellen Sie die Anzahl der Störzeichen gleich -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
**Kurze Antwort** – ja.
Sie können die Antwort in *O(|w1|+|w2|)* entscheiden Zeit nur durch Prüfung
Häufigkeit jedes Buchstabens (es gibt nur 26 davon).
Die Schlüsselidee ist, die *Anzahl der eindeutigen Buchstaben* in jedem String zu verfolgen
(`c1` und `c2`) und sehen, was mit diesen Zahlen passiert, wenn Sie zwei
Briefe.

---

oder Warum brute‐force unnötig ist

Wenn wir buchstäblich jedes Paar von Positionen in `w1` und `w2` versuchten, würden wir
Notwendigkeit

`` `
O(|w1| · |w2|)
`` `

Operationen.
Da ein Swap nur den *Typ* der beiden beteiligten Buchstaben beeinflussen kann
(`a` von `w1` und `b` von `w2`) hängt der Effekt nur von der
*Frequenz* von `a` in beiden Strings und von `b` in beiden Strings.
Es gibt nur 26 mögliche Buchstaben, so können wir alle `26 × 26` Paare probieren
und den Effekt in konstanter Zeit berechnen.

---

oder Was ändert sich beim Swap `a` (aus `w1`) mit `b` (aus `w2`)

| Situation | Wirkung auf die *unique‐letter* Anzahl der Zeichenkette, die es hinterlässt |
------------------------------------------------------------------------------------------
| `a` erscheint **once** in `w1` → es wird einzigartig, wenn wir es herausnehmen → **c1–=1**
| `a` erscheint **not** in `w2` → es wird ein neuer einzigartiger Buchstabe in `w2` → **c2+=1**
| `b` erscheint **once** in `w2` → es wird einzigartig, nachdem wir es herausnehmen → **c2–=1**
| `b` erscheint **not** in `w1` → es wird ein neuer einzigartiger Buchstabe in `w1` → **c1+=1** |

Wenn `a` und `b` das *same*-Zeichen sind, stornieren die ersten beiden Änderungen
gegenseitig aus – wir enden tatsächlich mit dem gleichen `c1` und `c2` wie wir
mit gestartet, so dass dieser Swap nur erfolgreich sein kann, wenn `c1 == c2` bereits.

Mit diesen Regeln können wir die *neue* Anzahl der einzigartigen Buchstaben berechnen
ohne die eigentlichen Strings zu berühren.

---

oder Java Implementierung (O(|w1|+|w2|) Zeit, O(1) Raum)

``java
Import java.util.*;

Public class Lösung {\cHFFFF}

public boolean isItPossible(String w1, String w2) {
// Häufigkeit jedes Briefes
Int[] f1 = neuer Int[26];
int[] f2 = neuer Int[26];

// Zählen Sie einzigartige Buchstaben in jedem String
int uniq1 = 0, uniq2 = 0;
für (char c : w1.toCharArray()) {\cHFFFF}
(f1[c - 'a')++ == 0) uniq1++;
}
für (char c : w2.toCharArray()) {\cHFFFF}
(f2[c - 'a')++ == 0) uniq2++;
}

/* Früher Ausgang: wenn der Unterschied > 2 ist, kann sich ein Swap ändern
die Zählung um maximal 2 (entfernen Sie eine einzigartige Char und/oder fügen Sie ein
neues einzigartiges Zeichen). Wenn es unmöglich ist, die beiden Zählungen zu bringen
innerhalb 2, die Antwort ist definitiv falsch. *
wenn (Math.abs(uniq1 - uniq2) > 2) fälschlich zurückkehren;

/* Probieren Sie jedes Paar (a von w1, b von w2) */
für (in a = 0; a < 26; a++) {\cHFFFF}
wenn (f1[a) == 0) weiter; // ein Muss in w1

// aktuelle einzigartige Zählungen dafür kopieren
int newUniq1 = uniq1;
int newUniq2 = uniq2;

// Entfernen eines von w1
wenn (f1[a) == 1) neuUniq1--; // a was einzigartig
wenn (f2[a) == 0) neuUniq2++; // a ist neu in w2

für (int b = 0; b < 26; b++) {
wenn (f2[b) == 0) weiter; // b muss in w2 existieren

int curUniq1 = newUniq1;
int curUniq2 = newUniq2;

// Wenn a == b wir den gleichen Buchstaben tauschen
wenn (a = = b) {
// In diesem Fall haben wir bereits die Wirkung von
// Entfernen eines w1, Hinzufügen zu w2. Keine Veränderung
// zu den einzigartigen Zahlen – wir müssen nur überprüfen
// ob die aktuellen Zähler bereits gleich sind.
wenn (curUniq1 ==curUniq2) wahr werden;
weiter;
}

// Hinzufügen von b zu w1
wenn (f1[b) == 0) curUniq1++; // b ist neu in w1

// Entfernen b von w2
wenn (f2[b) == 1) curUniq2--; // b war einzigartig

/* Jetzt curUniq1 / curUniq2 sind die einzigartigen Zählungen nach
mit b. Wenn sie übereinstimmen, haben wir eine gefunden
gültiger Swap. *
wenn (curUniq1 ==curUniq2) wahr werden;
}
}
Rückgabe falsch; // kein Paar erfolgreich
}
}
`` `

### Wie es funktioniert – Schritt für Schritt

ANHANG **Build-Frequenztabellen* – O(ww1|+|w2|)
`f1[i]` ist die Anzahl der Zeiten Buchstaben `'a'+i` erscheint in `w1`;
`f2[i]` das gleiche für `w2`.

2. **Die einmaligen Buchstaben** ein Buchstabe ist einzigartig, wenn seine Frequenz
genau 1.
Das gibt uns `uniq1` und `uniq2`.

3. **Early pruning** – wenn `uniuniq1 – uniq2| > 2`, können wir `false zurückgeben `
sofort.

4. **Alle 26×26 Paare* – für jeden `a`, der in `w1` erscheint
und jeder `b`, der in `w2` erscheint, berechnen wir die Wirkung auf die beiden
unique‐letter zählt mit der Tabelle oben.
Alle Operationen innerhalb der Schleifen sind konstante Zeit, so dass die Gesamt
Zeit ist `26 × 26 = 676`, d.h. **O(1)** gegenüber dem String
Längen.

5. **Return** – das erste Paar, das gleiche Zahlen liefert, ist ein Erfolg;
wenn wir alle paare erschöpfen wir `false` zurück.

---

Die Komplexität

- **Zeit** – `O(|W1| + |w2|)` zum Aufbau der Frequenztabellen, plus
die Konstante 26×26 Schleife (≈ 676 Stufen).
Die Gesamtlaufzeit ist also linear in der Eingangsgröße.

- **Space** – wir verwenden zwei Arrays der Länge 26, d.h. `O(1)` zusätzlich
Gedächtnis.

---

♪ Takeaway

Sie müssen nicht jede Position in den Strings ausprobieren.
Denn nur die *letter-Typen* sind wichtig für den einzigartigen -Brief zählt,
Sie können die Wirkung eines einzelnen Swaps in konstanter Zeit analysieren und
versuchen Sie alle `26 × 26` möglichen Buchstabenpaare. Das Ergebnis ist ein
O(|w1|+|w2|) Algorithmus, der sowohl einfach zu implementieren als auch einfach zu bedienen ist
verstehen.