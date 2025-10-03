---
Titel: LeetCode 1750. Mindestlänge des Streichens nach Deleting ähnliche Enden -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
1750. Mindestlänge des Streichens nach dem Löschen ähnlicher Enden
** Schwierigkeit**: Medium | **Charakter**: `a`, `b`, `c` | **Length**: ≤ 105

---

TL;DR

``java
Klasse Lösung {
öffentliches Mindesteinkommen Länge (String s) {
int l = 0, r = s.length() - 1;
während (l < r && s.charAt(l) == s.charAt(r) {\cHFFFF}
n = s.charAt(l);
während (l <= r && s.charAt(l) == ch) l++;
(l <= r && s.charAt(r) == ch) r---
}
zurück r - l + 1; // kann 0 sein, wenn
}
}
`` `

```python
Klasse Lösung:
def minimumLength(self, s: str) -> int:
l, r = 0, len(s) - 1
bei l < r und s[l] == s[r]:
c = s[l]
bei l <= r und s[l] == ch: l += 1
bei l <= r und s[r] == ch: r -= 1
zurück max(r - l + 1, 0)
`` `

```cpp
Klasse Lösung {
öffentlich:
mindestens Länge (String s) {
int l = 0, r = (int)s.size() - 1;
und {\cHFFFF}
n = s[l];
(l <= r && s[l] == ch) ++l;
(l <= r && s[r] == ch) --r;
}
zurück max(r - l + 1, 0);
}
};
`` `

Die drei Schnipsel verwenden alle die **two‐pointer greedy** Strategie – O(n) Zeit, O(1) extra Platz.

---

oder Warum dieses Problem ist eine “große” Interview Frage

**Good*********************
------------------------
| **Simplicity** – Die Aussage ist kurz und eindeutig. | **Hidden Traps** – Off‐by‐one Fehler bei l > r nach Löschungen. |
| ** Lernwert** – Lehren Sie zwei-Punkte-Technik, gierige Argumentation und Edge-Case-Analyse. | **Complex Constraints* – 105 Länge erfordert lineare Zeit. Einige vermuten, dass Sie * alle* gleichen Enden löschen können, ignorieren, dass Präfixe/Suffixe kontig und nicht-übergreifend sein müssen. |
| **Cross‐Language Transfer** – Gleiche Logik in Java, Python, C++ (und mehr). | **Unklare Optimalität** – Die Studierenden können denken, dass * jede* Sequenz von Löschungen funktioniert, nicht minimal ist. | **Memory Misconception** – Die Erstellung von vielen Substrings ist ein teures Anti-Patern. |

---

In den Warenkorb

ANHANG **Punkte**
* `l` – Index des linken Charakters.
* `r` – Index des rechten Charakters.

2. **Während `l < r` und `s[l] = s[r] `*
* Alle Zeichen von `l` zum ersten anderen sind gleich (`ch`).
* Wechseln Sie *entire* Block von `ch`, beginnend bei `l` → `l++, bis ein anderes Zeichen erscheint.
* Skip *entire* block of `ch` ending bei `r` → `r--, bis eine andere char erscheint.
* Dies simuliert das Löschen des maximalen Gleichzeichen-Präfix und Suffix in einem Schritt.

3. **Terminierung**
* Entweder die beiden Zeiger gekreuzt (`l > r`) → ganze String gelöscht → Antwort `0`.
* Oder die Zeichen bei `l` und `r` unterscheiden → keine Löschungen mehr möglich → `r - l + 1`.

**Warum Greedy Werke*
Wenn die Enden übereinstimmen, kann das Löschen von *any* nicht leeren gleichen Block von jeder Seite die verbleibende Länge nicht erhöhen. Die maximalen Blöcke zu nehmen ist sicher und nie reduziert zukünftige Optionen. Daher ergibt die gierige Strategie die minimal mögliche Restlänge.

---

Analyse der Komplexität

| Metric | Wert |
|--------------------
| Zeit | **O(n)* – jedes Zeichen wird maximal zweimal untersucht. |
| Raum | **O(1)** – nur zwei Indizes und ein temporäres Zeichen. |

---

Â Edge Cases & Pitfalls

| Rechtssache Was zu sehen für |
|-----------------------------
| `"a"`` | Nur ein Zeichen → Antwort `1`. |
| `"aa"`` | Ganze Saite ist die gleiche char → Antwort `0`. |
| `"abca"``` | Ends unterscheiden sich (`a` ≠ `a`? tatsächlich gleich, aber nur ein `a` auf jeder Seite, dann Mittelblock bleibt) → Endlänge `2`. |
| Leerzeichenfolge nach Löschungen | `l > r` → `max(r-l+1,0)` schützt vor negativer Länge. |
| Alle drei Zeichen, die | Algorithm präsentieren, funktionieren noch, weil es nur um die Gleichheit der aktuellen Enden kümmert. |

---

SEO‐Optimierter Blog Artikel

> **Titel:** Master LeetCode 1750 – Mindestlänge des Streichens nach dem Löschen ähnlicher Enden
> Beschreibung:*** Lernen Sie die gierige Zweipunktlösung für LeetCode 1750, mit Java, Python und C++-Code. Steigern Sie Ihr Interview Prep und landen Sie Ihren Traumjob.
> **Keywords:** LeetCode 1750, minimale Stringlänge, zwei Pointer-Algorithmus, Interviewvorbereitung, Codierung Interview, gieriger Algorithmus, Java-Lösung, Python-Lösung, C++-Lösung, Bewerbungsgespräch

---

# Blog Post

> **How to Crush LeetCode 1750 (Minimum Länge des Streichens nach dem Löschen ähnlicher Enden)* *
> *By Your Name – Software Engineer & Interview Coach*

Einleitung

Wenn Sie sich auf ein Codierung Interview bei Unternehmen wie Google, Amazon oder Facebook vorbereiten, werden Sie schnell erkennen, dass viele “medium” LeetCode Probleme einen einfachen, eleganten Trick verstecken. Ein solches Juwel ist **LeetCode 1750 – Mindestlänge des Streichens nach dem Löschen ähnlicher Enden**.

In diesem Beitrag werde ich Sie durch das Problem gehen, erklären, warum der gierige Zwei-Punkter-Ansatz optimal ist, zeigen Sie saubere Java-, Python- und C++-Implementierungen und decken die Fallstricke ab, die sogar erfahrene Kandidaten auf Reisen. Am Ende werden Sie nicht nur dieses Problem angehen, sondern auch verstehen, wie Sie eine präzise, produktionsbereite Lösung in einem Interview präsentieren können.

---

Probleme Wiederherstellung (Short & Sweet)

Sie erhalten eine Saite `s`, bestehend nur aus `'a'`, `'b'` und `'c'`.

Sie können immer wieder ** ein nicht-leeres Präfix und einen nicht-leeren Suffix auslöschen, die denselben Charakter enthalten und sich nicht überschneiden**.
Ihr Ziel: **Minimieren Sie die Länge des Strings** nach Durchführung der Operation beliebig oft (einschließlich Null).

---

oder Intuition: Warum ein Zwei-Punkt-Sweep?

Denken Sie an die Zeichenfolge. Die Operation entfernt immer gleiche Zeichen von *both* Enden.
Wenn die linkssten und rechtssten Zeichen unterschiedlich sind, können Sie nie etwas löschen – die Antwort ist einfach die aktuelle Länge.

Wenn sie gleich sind, haben Sie zwei Möglichkeiten:

ANHANG Löschen Sie den *smallest* möglichen Block (nur das erste Zeichen auf jeder Seite).
2. Löschen Sie den *größten* möglichen Block (alle aufeinanderfolgenden gleichen Zeichen von jeder Seite).

Warum nicht den größeren Block wählen? Weil die Einnahme von mehr des gleichen Charakters von beiden Enden kann nicht schaden. Es reduziert den String schneller und lässt Sie mit dem gleichen mittleren Segment. **Die optimale Strategie besteht daher darin, immer das maximale gleiche Präfix und Suffix* zu löschen. Genau das macht ein Zweipunkt-Scan.

---

The Greedy Two‐Pointer Algorithm

1. **Initialize** zwei Indizes, `l = 0` und `r = s.length() - 1`.
2.
* Let `ch = s[l]`.
* Advance `l` während `s[l] == ch`.
* Retreat `r` während `s[r] == ch`.
3. **Ergebnis** ist `max(r - l + 1, 0)`.
Der `max` behandelt den Fall, in dem `l`` `r` übertrifft (vollständig gelöscht).

> **Warum ist das linear? **
> Jede Iteration der äußeren Schlaufe bewegt mindestens einen Zeiger an einem Block gleicher Zeichen vorbei. Da der String höchstens `n` Zeichen hat, ist das Gesamtwerk `O(n)`.

---

Code in drei Sprachen

Unten sind saubere, produktionsfertige Lösungen in Java, Python und C++. Jeder folgt der gleichen Logik und hat die gleichen Zeit/Raum-Garantien.

### Java

``java
Klasse Lösung {
öffentliches Mindesteinkommen Länge (String s) {
int l = 0, r = s.length() - 1;
während (l < r && s.charAt(l) == s.charAt(r) {\cHFFFF}
n = s.charAt(l);
während (l <= r && s.charAt(l) == ch) l++;
(l <= r && s.charAt(r) == ch) r---
}
zurück r - l + 1; // wird 0 sein, wenn l > R
}
}
`` `

### Python

```python
Klasse Lösung:
def minimumLength(self, s: str) -> int:
l, r = 0, len(s) - 1
bei l < r und s[l] == s[r]:
c = s[l]
bei l <= r und s[l] == ch:
= 1
bei l <= r und s[r] == ch:
-= 1
zurück max(r - l + 1, 0)
`` `

C++

```cpp
Klasse Lösung {
öffentlich:
mindestens Länge (String s) {
int l = 0, r = (int)s.size() - 1;
und {\cHFFFF}
n = s[l];
(l <= r && s[l] == ch) ++l;
(l <= r && s[r] == ch) --r;
}
zurück max(r - l + 1, 0);
}
};
`` `

---

Häufige Fehler & Wie Sie Them vermeiden

| Fehler | Warum es passiert | Fix |
|----------------------------------
| ** Die Verwendung von Rekursion oder DP** | Kandidaten denken, dass jede Operation ein Subproblem ist. | Greedy ist genug; DP fügt unnötige Komplexität hinzu. |
| **Off‐by‐one Fehler** | Vergessen Sie, dass `l` und `r` überqueren können. | Return `max(r - l + 1, 0)` oder check `if (l > r) return 0;`. |
| **Denn nur ein Zeichen** | Denken “Entfernen Sie alle gleichen Enden” bedeutet je ein Zeichen. | Löschen Sie immer den *entire*-Block von gleichen Zeichen. |
| **Creating Substrings in einer Schleife** | Memory-Blowup für 105 Länge. | Nur mit Indizes arbeiten. |

---

oder Warum dieses Problem ein „Must‐Know“ für Interviews ist

ANHANG **Two‐Pointer Mastery** – Ein Heft für viele Interview-Fragen (Rückensaite, Palindrome-Checks, Schiebefenster usw.).
2. **Greedy Insight* – Demonstriert die Fähigkeit zu beweisen, dass eine lokal optimale Wahl zu einer global optimalen Lösung führt.
3. **Edge‐Case Sensitivity** – Zeigt die Liebe zum Detail (leere Saite, Einzelcharakter, vollständige Löschung).
4. **Sprache Flexibilität** – Sie können die gleiche Logik in Java, Python, C++ oder sogar JavaScript präsentieren, beeindrucken Interviewer, die sauberen, plattformübergreifenden Code schätzen.

Wenn Sie diese Lösung artikulieren können, erhalten Sie eine Interview-Frage aus dem Weg *wenn Sie noch warm sind.* Es stellt Sie auch schön für andere Probleme auf mittlerer Ebene, die auf ähnlichen Mustern anhängen.

---

Letzte Gedanken

LeetCode 1750 ist täuschend einfach: ein String, ein paar Zeichen und ein Zweipunkt-Sweep.
Der Schlüssel ist zu erkennen, dass gleiche Enden sollten in Bulk getrimmt werden, nicht eine zu einer Zeit. Diese Einsicht verwandelt das Problem in einen einzigen linearen Pass und gibt Ihnen eine elegante, effiziente Lösung.

Verwenden Sie die Code-Snippets oben in Ihrer Praxis und in Interviews. Markieren Sie den gierigen Beweis, gehen Sie durch ein schnelles Beispiel und seien Sie bereit, zu antworten “Warum das funktioniert.” Mit diesem Problem in Ihrer Toolbox sind Sie ein Schritt näher an der Landung dieser Traumsoftware-Engineering-Rolle.

---

**Happy Coding!**

*Wenn Sie diesen Beitrag hilfreich gefunden haben, teilen Sie ihn auf LinkedIn oder Twitter, und lassen Sie mich in den Kommentaren, die LeetCode Problem, die Sie als nächstes behandeln, wissen. *

---

Schlussfolgerung

LeetCode 1750 ist ein perfektes Beispiel dafür, wie ein gut verstandenes Muster – zwei Zeiger und gieriges Löschen – in linearer Zeit ein scheinbar kompliziertes Problem lösen kann. Meistern Sie das, und Sie werden nicht nur die “Problem-Lösung” Abzeichen auf Ihrem résumé verdienen, sondern auch die analytischen Denkanstrengungen Rekrutierer suchen.

Viel Glück und fühlen Sie sich frei zu erreichen, wenn Sie ein-on-one-Interview-Coaching oder einen tieferen Tauchgang in andere LeetCode Herausforderungen möchten!

---

> **Folgen Sie mir** für mehr Interview Prep Guides, Algorithmen-Tutorials und Karriere-Bauberatung.

---

* Ende der Post*

---

Schlussfolgerung

LeetCode 1750 ist nicht nur ein weiteres String-Manipulationsproblem; es ist ein Mikrokurs in gieriger Zweipunkttechnik. Durch Vermeidung von Über-Engineering und Fokussierung auf maximale Löschungen können Sie es in linearer Zeit mit minimalem Code lösen.

Fühlen Sie sich frei, meine Kontaktdaten zu fallen, wenn Sie ein personalisiertes Mock-Interview oder eine tiefere Analyse ähnlicher Probleme wünschen. Viel Glück – und glückliche Kodierung!