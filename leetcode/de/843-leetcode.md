---
Titel: LeetCode 843. Ratet das Wort -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
**Gut das Wort – 843**
*(Java – interaktive “Master”-Schnittstelle)*

---

oder 1. Problem Recap

Sie erhalten eine *wordlist* von bis zu 10 000 6-Buchstaben-Strings (alle gleiche Länge).
Einer von ihnen ist das **geheime Wort*.

Sie können bis zu **10 Raten** machen.
Nach jeder Vermutung erzählt das `Master`-Objekt, wie viele Zeichen mit dem geheimen Wort ** in den gleichen Positionen* übereinstimmen (eine ganze Zahl `0 ... 6 `).
Wenn Sie das geheime Wort erraten, endet das Spiel erfolgreich; sonst müssen Sie raten, bis Sie das geheime Wort getroffen oder aus Versuchen auslaufen.

Ihre Aufgabe ist es, eine Funktion zu schreiben

``java
Leer findenSecretWord(String[] wordlist, Master master)
`` `

dass die Reihenfolge der Erraten und garantiert einen Sieg innerhalb der erlaubten Anzahl der Versuche.

---

oder 2. Was der Interviewer wirklich fragt

ANHANG ** Können Sie die Interaktion als Suchproblem modellieren? * *
– Jede Vermutung teilt den aktuellen Kandidatensatz nach dem Feedback-Wert.
2. **Welche raten Sie als nächstes? **
– Wir wollen den Kandidatensatz so schnell wie möglich reduzieren (maximierender Informationsgewinn).
3. **Was sind Sie bereit? * *
– Die optimale (minimax) Strategie ist teuer; eine praktische Heuristik reicht oft aus.

Erklären Sie, dass wir ein *imperfect‐Informationsspiel* mit dem Ziel lösen, die schlimmste Anzahl von Erraten zu minimieren.

---

oder 3. Hochrangige Strategie

ANHANG **Start mit einem „pivot“-Rat* *
– Wählen Sie jedes Wort (random oder deterministisch).
– Call `master.guess(pivot)` → `m` Spiele erhalten.

2. ** Filtern Sie die Liste*
– Halten Sie nur Wörter, die auch genau `m`-Spiele mit dem Drehpunkt geben.
– Alle anderen Worte sind unmöglich.

3. **Ihr Name**
– Wenn die gefilterte Liste nur noch ein Wort hat, rate es.
– Andernfalls, wählen Sie ein weiteres Wort aus der gefilterten Liste (oft zufällig).
– Wiederholen Sie den Filterschritt mit der neuen Rate.

4. **Stop**
– Entweder haben Sie 6 Spiele getroffen (das Geheimnis gefunden) oder Sie haben alle 10 Vermutungen verwendet.

---

oder 4. Warum das funktioniert

**Feedback ist genau* – Wenn ein Wort `k` Spiele liefert, muss jeder Kandidat das gleiche `k` geben.
- ** Filtern schrumpft den Raum exponentiell** In einer zufälligen Verteilung eliminiert jede Vermutung etwa einen konstanten Anteil der übrigen Wörter.
- **Random oder deterministisches Drehgelenk** – Beide sind fein; zufällig verhindert pathologische schlimmste Fallkonstruktionen, deterministische (z.B. Ähnlichkeits-basiertes Minimax) Garantien ≤ 10 Vermutungen im Durchschnitt.

---

oder 5. Praktische Algorithmen

### 5.1 Random/Greedy Filtering (simple)

``java
Klasse Lösung {
int match(String a, String b) { ... } // zähle die gleiche Position

öffentliche Leere findenSecretWord(String[] Wörter, Master master) {
List<String> Kandidaten = neue ArrayList<>(Arrays.asList(Worte));

für (int i = 0; i < 10 && !candidates.isEmpty(); i++)
// Wählen Sie das i‐te Wort (oder zufällig aus der Liste)
String rate = Kandidaten.get(0); // deterministisch
Int Spiele = master.guess(gues);
wenn (Matches == 6) zurück; // Erfolg

// filter
List<String> next = new ArrayList>>;
für (String w : Kandidaten) {\cHFFFF}
wenn (w.equals(guess)) weitergeht;
wenn (match(guess, w) == matchs) next.add(w);
}
Kandidaten = nächste;
}
}
}
`` `

*Komplexität:*
- `match()` ist `O(6)` → konstant.
- Jede Iteration scannt alle übrigen Wörter → `O(n)` pro Runde.
- Im schlimmsten Fall `O(n2)`, aber in der Praxis schrumpft die Liste schnell.

### 5.2 Ähnlichkeitsbasiertes Greedy (besser für Zufallsdaten)

ANHANG **Pre-compute Ähnlichkeiten**
- Für jedes Wort zählen, wie viele andere Wörter mindestens ein gleiches Zeichen an der gleichen Position teilen.

2. **Sort die Wortliste, die von dieser Partitur absinkt* *
- Das "popularste" Wort wird, auf einem `0` Match-Feedback, beseitigen viele Kandidaten.

3. **Guess in dieser Reihenfolge, Filtern nach jeder Vermutung* *
- Wie oben.

*Warum hilft das: *
Wenn Sie erwarten, dass die meisten Vermutungen, `0`-Spiele zurückzugeben (≈80 % Chance), Picking ein Wort, das vielen anderen in mindestens einer Position entspricht, entfernt ein großes Stück von Möglichkeiten, wenn das Feedback `0` ist.

---

oder 6. Edge Cases & Diskussion

| Scenario | Was passiert | Warum es OK ist |
--------------------------
| Alle Wörter sind ganz deutlich (z.B. "abcdef", "ghijkl", ...") | Nach der ersten Vermutung bleibt nur das genaue Wort | Eine Vermutung ist genug |
| Worst‐case adversarial list | Random Pivot könnte noch innerhalb von 10 Vermutungen erfolgreich sein | Auch wenn der deterministische Ähnlichkeitsansatz scheitern kann, garantiert die zufällige Filterung Erfolg in 10 Versuchen, weil die schlimmste Fallgröße ≤ 10 |
| `wordlist.length` > 10 000 | Filtern noch `O(n)`` jede Runde | n wird durch die Problemzwänge gebunden |

---

oder 7. Zusammenfassung der Komplexität

- **Zeit:**
`O(n2 * 6)`` schlimmsten Fall, aber Durchschnittsfall ist `O(n log n)` aufgrund exponentieller Schrumpfung.
- **Space:**
`O(n)` für die Liste der Kandidaten.

---

oder 8. Wie man das einem Interviewer vorstellt

ANHANG **Erhebung des Problems:**
„Wir spielen ein interaktives Spiel; jede Rate gibt uns die Anzahl der richtigen Positionen. „

2. **Die Kernidee:**
„Filtern Sie den Kandidatensatz mit dem genauen Match-Feedback; jede Vermutung, die nicht übereinstimmen, beseitigt eine große Anzahl von Wörtern. „

3. **Erklären Sie die algorithmische Wahl:**
- “Ich wähle das erste Wort (oder ein zufälliges) wie mein Pivot, frage den Master, und dann nur die Worte, die das gleiche Feedback erzeugen. „
- „Ich wiederhole, bis ich das Geheimnis finde oder die Liste auf einen steht. „

4. **Diskusse Zeit/Raum-Ausflüge*
„Wir scannen die Liste jede Runde, also ist es `O(n)` pro Vermutung. Weil die Liste schnell schrumpft, ist dies akzeptabel. „

5. **Mention Erweiterungen*
- „Wenn wir cleverer sein wollen, könnten wir eine Ähnlichkeitsnote berechnen und immer das „informative“ Wort wählen. „
- „Das bringt Minimax- oder Entropie-basierte Ideen, aber die einfache gierige Lösung erfüllt die 10-Gäste-Grenze. „

6. **Zeichenschnipsel anzeigen* *
„Hier ist eine präzise Umsetzung, die den obigen Schritten folgt. „

---

### Endnote

Kern der Lösung ist **iterative Filterung** basierend auf exakten Positionsspielen.
Ob Sie eine zufällige Pivot, das erste Wort oder eine ähnlich gewichtete Pivot wählen, die Idee bleibt gleich: jede Vermutung reduziert den Suchraum, und nach einer Handvoll Runden können Sie immer das geheime Wort innerhalb der erlaubten Versuche treffen.