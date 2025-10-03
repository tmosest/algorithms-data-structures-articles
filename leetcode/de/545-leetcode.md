---
Titel: LeetCode 545. Boundary of Binary Tree -
Beschreibung: Platzhalter
Datum: 2025-09-21
Kategorien: []
Verfasser: moses
Schlagworte: []
verstecktToc: wahr
---
📌 LeetCode 545 – Boundary of Binary Tree
**Medium | Binary Tree | DFS / Recursion | Time O(n) | Space O(h)*

Hier finden Sie voll funktionsfähige Lösungen in **Java, Python und C++**.
Nach dem Code haben wir einen kurzen „blog‐style“ Artikel geschrieben, der den Algorithmus erklärt, das Gute, das Böse und das hässliche hervorhebt und mit SEO-optimierten Keywords geschrieben wird, die Rekrutierer gerne in Ihrem Portfolio oder GitHub README sehen.

---

### 1. Java Lösung

``java
java.util importieren. ArrayList;
java.util importieren. Liste

/** Definition für einen binären Baumknoten. *
Volksklasse TreeNode {
int val;
TreeNode links;
TreeNode rechts;
TreeNode(int x) { val = x; }
}

Public class Lösung {\cHFFFF}

Öffentliches Gebiet vonBinaryTree(TreeNode Wurzel) {
Liste<Integer> Ergebnis = neue ArrayList<>>();
wenn (root == null) Rücklaufergebnis;

wenn (!isLeaf(root) result.add(root.val)

// 1. linke Begrenzung (ohne Blätter)
TreeNode cur = root.left;
während (kur != null) {
wenn (!isLeaf(cur)) result.add(cur.val);
cur = (cur.left != null) ? cur.left : cur.right;
}

// 2. Alle Blätter (links bis rechts)
addLeaves(root, Ergebnis);

// 3. Rechte Begrenzung (ohne Blätter) in umgekehrter Richtung
List<Integer> rightBounding = new ArrayList<>;
cur = root.right;
während (kur != null) {
wenn (!isLeaf(cur)) rechtBoundary.add(cur.val)
cur = (cur.right != null) ? cur.right: cur.left;
}
für (int i = rightBoundary.size() - 1; i >= 0; --i)
result.add(rightBoundary.get(i));

Rückgabeergebnis;
}

Private Leere addLeaves(TreeNode node, List<Integer> out) {
wenn (node == null) zurückkehrt;
wenn (isLeaf(node)) {\cHFFFF}
aus.add(node.val)
zurück;
}
addLeaves(node.left, out);
addLeaves(node.right, out);
}

Privat boolean isLeaf(TreeNode node) {
zurückgeben. = null &&-Knoten. = null;
}
}
`` `

---

### 2. Python Lösung

```python
aus der Einfuhr Liste, Optional

# Definition für einen binären Baumknoten.
Klasse TreeNode:
def __init__(self, val: int = 0, links: 'TreeNode' = None, right: 'TreeNode' = None):
selbst.val = val
selbst.left = links
selbst.right = rechts

Klasse Lösung:
Def Grenze VonBinaryTree(self, root: Optional[TreeNode]) -> Liste[int]:
wenn nicht root: return []

= []

# Root (falls kein Blatt)
wenn nicht selbst._is_leaf(root):
res.append(root.val)

# linke Grenze (ohne Blätter)
Node = root.left
während Knoten:
wenn nicht selbst._is_leaf(node):
res.append(node.val)
node = node.left if node. links anderen Knoten. Recht

# Leaves
selbst._add_leaves(root, res)

# Rechte Grenze (ohne Blätter) – Sammeln Sie dann umgekehrt
Recht_gebunden = [
node = root.right
während Knoten:
wenn nicht selbst._is_leaf(node):
Rechts_boundary.append(node.val)
node = node.right wenn node. - Ja. links
res.extend(reversed(right_boundary))

zurück

def _add_leaves(self, node: Optional[TreeNode], out: List[int]) -> Keine
wenn nicht Knoten:
zurück
wenn selbst._is_leaf(node):
aus.append(node.val)
zurück
selbst._add_leaves(node.left, out)
selbst._add_leaves(node.right, out)

@staticmethod
def _is_leaf(node: TreeNode) -> bool:
zurückgeben. links ist None und Knoten. Recht ist Keine
`` `

---

### 3. C++ Lösung

```cpp
#include <vector>
mit Namespace std;

/* Definition für einen binären Baumknoten. *
TreeNode {
int val;
TreeNode *links;
TreeNode *right;
TreeNode(int x) : val(x), links(nullptr), rechts(nullptr) {}
};

Klasse Lösung {
öffentlich:
Vektor<int> vonBinaryTree(TreeNode* Wurzel) {
vektor<int> an;
wenn (!root) Ans zurückgibt;

wenn (!isLeaf(root)) ans.push_back(root>val)

// linke Begrenzung (ohne Blätter)
TreeNode* cur = root->left;
während (kur)
wenn (!isLeaf(cur)) ans.push_back(cur->val)
cur = (cur->left)
}

// Blätter
addLeaves(root, ans);

// Rechte Grenze (ohne Blätter) – Sammeln Sie dann umgekehrt
Vektor<int> RechtsB;
cur = root->right;
während (kur)
wenn (!isLeaf(cur)) rightB.push_back(cur->val)
= (kur->right)
}
für (auto it = rightB.rbegin(); it != rightB.rend(); ++it)
ans.push_back(*it);

Rückgabe ans;
}

privat:
bool isLeaf(TreeNode* node) {
zurück-Knoten->left == Nullptr && node->right == nullptr;
}

Leere addLeaves(TreeNode* node, vector<int>& out) {
wenn (!node) zurückkehrt;
wenn (isLeaf(node)) {\cHFFFF}
out.push_back(node->val);
zurück;
}
addLeaves(node->left, out);
addLeaves(node->right, out);
}
};
`` `

> **Tip:** In allen drei Sprachen ist die Kernidee gleich – *DFS mit drei Pässen*:
> 1. linke Begrenzung (oben-zu-unt, überspringen Blätter)
> 2. Alle Blätter (links bis rechts)
> 3. Rechte Begrenzung (oben-zu-unten, überspringen Blätter) aber in umgekehrter Reihenfolge hinzugefügt

---

📖 Blog‐Style Write‐up: „Boundary of Binary Tree – Good, Bad & Ugly“

> **Keywords**: *LeetCode 545, Boundary of Binary Baum, binäre Baumtransversal, DFS, Interview-Algorithmus, Software-Ingenieur-Interview, Codierung Interview, Zeitkomplexität, Raumkomplexität, Job-Interview-Tipps. *

---

### 1️⃣ Das Gute

| Warum dieser Algorithmus glänzt | Was Rekrutierer sehen |
------------------------------------------------------------
| **Simplicity** – Die Lösung ist nur ein paar Schleifen und ein wiederkehrender Blattkollektor. Keine zusätzliche Zustandsmaschine oder Fahnenlogik. | *Klar, lesbarer Code* |
| **Linear Time** – Jeder Knoten wird maximal einmal besucht → **O(n)**. Perfekt für große Bäume. | *Efficiency Claim* |
| **Low Auxiliary Space* – Nur Recursionstiefe (`O(h)`) und ein paar Zusatzlisten (`O(h)`). | *Space-optimiert*
| **Extensible** – Sie können diese Routine in jedes Interview oder Produktionssystem einfügen, das eine „Straßenperipherie“-Ansicht benötigt. | * Wiederverwendbares Codemuster* |
| **No Double‐Counting** – Blätter werden nur einmal hinzugefügt, ob sie an einer Grenze erscheinen oder nicht. | *Bug-freie Garantie* |

> **Recruiter-freundlicher Takeaway**: *“Ich kann saubere, O(n) Baum-Traversal-Code produzieren, der häufige Fallstricke wie Doppel-Folgeblätter vermeidet.“*

---

### 2️⃣ Das Böse

Häufige Schmerzpunkte | Fix / Vermeiden Sie |
|----------------------------
| **Nullwurzel* – Die Problemerklärung garantiert eine Wurzel, aber eine defensive Kodierung ist immer noch klug. | Überprüfen Sie `root == null` früh. |
| **Single‐child-Grenzknoten* – Ein Knoten mit nur einem Kind muss noch als Teil der Grenze betrachtet werden. Verwenden Sie das „wenn es noch rechts gibt“ (und umgekehrt für die rechte Grenze). |
| **Root ist ein Blatt* – In diesem Fall ist die Grenze nur `[root.val]`. | Skip addieren `root`, wenn es ein Blatt ist. |
| **Language quirks* – In Python kann die Recursionsgrenze `sys.setrecursionlimit` treffen, in C++ müssen die Pointer-Checks vorsichtig sein. | Halten Sie die Rekursionstiefe im Auge, oder wechseln Sie zu einem iterativen Stack, wenn `h` könnte riesig sein. |

---

### 3️⃣ Die Ugly

| Wenn der Code wie ein Spaghetti Monster aussieht |
|-------------------------------------------------------------
| Over‐Engineering mit “Flag” Ganzzahlen (1 = links, 2 = rechts, 3 = andere) und mehrere Helfer-Methoden nur um die Spur von “wo wir sind” zu halten ist **unnötig** für dieses Problem. Es macht den Code härter zu lesen und mehr fehleranfällig. |
| Die Verwendung eines globalen `vector<int>` und die Mutation von der tiefen Rekursion kann knifflig sein, vor allem in C++, wo die manuelle Speicherverwaltung beteiligt ist. |
| Das Vergessen, Blätter beim Hinzufügen der linken/rechts Grenze zu überspringen, führt oft zu Duplikatwerten in der Endliste. Ein „simple‐first“ Ansatz, der die Wurzel, linke Grenze, Blätter, rechte Grenze – und dann de‐dupliziert – hinzufügt, ist sauberer. |

> **Take‐away**: *Schreiben Sie die einfachste DFS, die die Begrenzungsregeln erfüllt. Vermeiden Sie versteckte Fahnen oder State-Maschinen, es sei denn, das Interview erfordert sie ausdrücklich. *

---

### 4️⃣ SEO‐Optimierte Zusammenfassung

Wenn Sie ein GitHub README, eine Portfolio-Seite, oder eine **LeetCode Lösung Set** zur Beeindruckung von Einstellungsmanagern erstellen, verwenden Sie die folgenden Meta-Tags, Überschriften und Keyword-dense Sätze:

- #LeetCode545`, `#BoundaryOfBinaryTree`, `#BinaryTreeTraversal`, `#DFS`, `#Recursion`, `#InterviewAlgorithm`, `#SoftwareEngineer`, `#CodingInterview`, `#JobInterview`, `#AlgorithmDesign`, `#TimeComplexity`, `#SpaceComplexity `

**Sampling README Snippet**

```markdown
# Boundary of Binary Tree – LeetCode 545

- **Problem**: Berechnen Sie die Grenze eines binären Baumes (linke Grenze, Blätter, rechte Grenze) in O(n) Zeit.
- **Sprachen*: Java, Python, C++.
- **Komplexitäten*: `O(n)` Zeit, `O(h)` Hilfsraum (`h` = Baumhöhe).
- **Warum es geht**: Demonstriert Tiefen-erste Suche, Edge-Case-Handling und sauberen Code – Schlüsselfertigkeiten für ein Software-Ingenieur-Interview.
`` `

> **Warum ist das wichtig für Ihre Jobsuche* *
> Recruiter suchen nach Kandidaten, die ** klassische Baumprobleme lösen** schnell und mit sauberem Code. Indem Sie dieses Problem (LeetCode 545) zu Ihrem öffentlichen Repo hinzufügen und einen Blog-Post schreiben, der *gute, schlechte, hässliche* Einsichten erklärt, zeigen Sie:
> * Probleme lösende Fähigkeiten
> * Code Lesbarkeit und Aufrechterhaltungsfähigkeit
* Verständnis von Zeit- und Raumfahrt-Ausflügen
> * Fähigkeit, komplexe Ideen in einem verdaulichen Format zu kommunizieren

---

### 5️⃣ Schnelltest-Harness (Optional)

``java
öffentliche statische Leerstelle (String[] args) {
/* Konstruieren Sie den folgenden Baum
1
/ \
Artikel 3
/ \
4 5 7
*
TreeNode root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);
root.right.right = new TreeNode(7);

Lösungssol = neue Lösung();
System.out.println(sol.boundaryOfBinaryTree(root)); // -> [1, 2, 4, 5, 7, 3]
}
`` `

---

### 🎯 Wie verwenden Sie diese Lösungen in Ihrem Interview Portfolio

ANHANG ** Laden Sie die drei Quelldateien** (`Solution.java`, `solution.py`, `solution.cpp`) auf ein öffentliches GitHub Repo.
2. Fügen Sie den **blog Artikel* als `README.md` oder eine separate `blog.md`-Datei hinzu.
3. In Ihrer LinkedIn oder Portfolio-Seite, Link zum Repo und Erwähnen *“Solved LeetCode 545 – Boundary of Binary Tree with O(n) DFS“*.
4. Wenn Sie sich bewerben, fügen Sie den folgenden Snippet zu Ihrem Titelbrief oder LinkedIn hinzu:

> *“Während meines letzten Interviews habe ich LeetCode angegriffen 545 – Boundary of Binary Tree, Implementierung einer sauberen, linear-time Lösung in Java, Python und C++. Der Algorithmus zeigt meine Fähigkeit, DFS auf binären Bäumen durchzuführen, Edge-case-Logik zu verwalten und produktionsbereiten Code zu produzieren.“*

---

**Happy Codierung & viel Glück Landung, dass nächste Software-Engineering Rolle!** 🚀