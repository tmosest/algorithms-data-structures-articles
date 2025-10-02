---
titre: LeetCode 2296. Concevoir un éditeur de texte - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – LeetCode 2296

Ci-dessous sont **trois solutions complètes et autonomes** – une en **Java, Python et C++** – qui satisfont aux contraintes de LeetCode et fonctionnent en **O(k)** temps par opération.

> **Pourquoi cette solution? * *
> * Il utilise la structure de données la plus simple qui donne *O(k)* temps: deux objets `Stack` (ou un `StringBuilder` avec un index de curseur).
> * Pas de liste liée, pas de bibliothèque lourde – parfaite pour un entretien ou un code de production.
> * Toutes les cases d'angle (dépassant le texte, supprimant plus que disponible, curseur vide) sont manipulées proprement.

---

### 1.1 Java – `StringBuilder` + index du curseur

"Java
Importation de java.util.*;

classe TextEditor {
texte privé StringBuilder; // le texte actuel
curseur privé int; // position du curseur (0 ... text.length())

public TextEditor() {
ce.text = nouveau StringBuilder();
ce.curseur = 0;
}

/** Ajouter `text` au curseur, puis déplacer le curseur à l'extrémité droite. */
public vide ajouterText(String newText) {
text.insert(curseur, nouveau texte); // O(nouveau texte.longueur())
curseur += nouveauText.length();
}

*** Supprimer jusqu'à `k` chars à gauche du curseur.
* Retourner le nombre de caractères effectivement supprimés. */
texte(int k) {
int remove = Math.min(k, curseur); // ne peut pas supprimer au-delà du début
i (supprimer > 0) {
text.delete(curseur - supprimer, curseur);
curseur -= supprimer;
}
retour supprimer;
}

*** Déplacer le curseur vers les positions `k`.
* Retournez les derniers caractères min(10, curseur) à gauche du curseur. */
public Chaîne curseurLeft(int k) {
curseur = Math.max(0, curseur - k);
int start = Math.max(0, curseur - 10);
retourner text.substring(démarrer, curseur);
}

*** Déplacez le curseur jusqu'aux positions `k`.
* Retournez les derniers caractères min(10, curseur) à gauche du curseur. */
public Chaîne curseurRight(int k) {
curseur = Math.min(text.length(), curseur + k);
int start = Math.max(0, curseur - 10);
retourner text.substring(démarrer, curseur);
}
}
«» "

---

#### 1.2 Python – deux piles `deque`

'`python
à partir de collections import deque
de taper l'importation Liste

TextEditor de classe :
def _init_(self):
# pile gauche tient les caractères à gauche du curseur
# pile droite tient les caractères à droite du curseur
auto-gauche = deque()
Self.right = deque()

def addText(self, texte: str) -> Aucun:
pour ch dans le texte:
auto.left.append(ch) # O(1) chacun

def deleteText(self, k: int) -> Int:
enlevé = 0
tout en étant enlevé < k et soi-même. gauche:
auto.gauche.pop()
enlevé += 1
retour enlevé

def screenLeft(self, k: int) -> str:
déplacé = 0
tout en se déplaçant < k et soi. gauche:
Self.right.appendleft(self.left.pop())
mouvementé += 1
# last min(10, curseur) chars à gauche du curseur
retourner ''.join(list(self.left)[-10:])

def curseurRight(self, k: int) -> str:
déplacé = 0
tout en se déplaçant < k et soi. à droite :
Self.left.append(self.right.popleft())
mouvementé += 1
retourner ''.join(list(self.left)[-10:])

♪ Exemple d'utilisation
# éditeur = TextEditor()
# editor.addText("leetcode")
«» "

*Pourquoi deux piles? *
Ils nous laissent **pousser/pop en O(1)**, donnant globalement **O(k)** pour chaque opération, même pour le plus grand `k=40` et des millions d'appels.

---

### 1.3 C++ – `string` + index du curseur

'`cpp
#incluez <string>
#incluez <algorithme>

classe TextEditor {
std::texte de chaîne; // texte actuel
Size_t curseur; // 0 ... text.size()

public:
TextEditor() : text(""), curseur(0) {}

vide addText(const std::string &s) {
text.insert(curseur, s);
curseur += s.size();
}

int supprimerText(int k) {
int remove = std::min(k, static_cast<int>(cursor));
i (supprimer > 0) {
text.erase(curseur - supprimer, supprimer);
curseur -= supprimer;
}
retour supprimer;
}

std::string curseurLeft(int k) {
curseur = std::max<size_t>(0, curseur - k);
size_t start = (curseur >= 10) ? curseur - 10 : 0;
retour du texte. substr(démarrer, curseur - démarrer);
}

std::string curseurRight(int k) {
curseur = std::min<size_t>(text.size(), curseur + k);
size_t start = (curseur >= 10) ? curseur - 10 : 0;
retour du texte. substr(démarrer, curseur - démarrer);
}
};
«» "

---

- Oui. 2. Article sur le blog – Concevoir un éditeur de texte (LeetCode 2296) : Les bons, les mauvais et les méchants

> **Méta—Description* *
> Master LeetCode 2296 Concevoir un éditeur de texte. Explorez trois implémentations propres en Java, Python et C++, comprenez les compromis et apprenez comment ace interviewer des questions sur la manipulation de chaînes et la simulation de curseurs.

---

2.1 Introduction

Avez-vous déjà regardé le problème de LeetCode "Design a Text Editor" et vous êtes-vous demandé pourquoi il a noté "Hard" ?
La difficulté principale est que chaque opération – ajouter, supprimer, déplacer à gauche, déplacer à droite – doit être **O(k)**, et la structure des données doit garder le curseur en synchronisation avec le texte.

Dans ce post, nous lisons:

- Briser l'énoncé du problème et les contraintes.
- Montrer trois solutions **idiomatic** (Java, Python, C++).
- Discutez des parties *bon*, *mauvais* et *doucement* de chaque approche.
- Souligner pourquoi la méthode basée sur la pile est la norme d'or pour les intervieweurs.
- Une feuille pour impressionner les recruteurs.

Laisse plonger.

---

2.2 Énoncé du problème (simplifié)

Opération: Ce qu'il fait: Valeur de retour:
- C'est quoi ?
"addText(string text)"" Insérer au curseur, le curseur se déplace à droite. "Sans"
Supprimez les caractères `k` gauche du curseur.
"cursorLeft(int k)"" Déplacer le curseur gauche "k" étapes.
"cursorRight(int k)"" Déplacer le curseur à droite `k` steps.

*Constraints*: `text.length`, `k ≤ 40`; jusqu'à 2 × 104 appels; seulement lettres minuscules.

---

### 2.3 La solution "Good" – Deux piles (ou Deque)

**Pourquoi c'est génial**

Raisons Détails
C'est quoi ?
**O(k) temps**= Chaque opération touche au plus des caractères `k`. Autres
**L'espace constant par char**= Deux deques stockent des personnages directement, sans pointeur de gymnastique. Autres
**Code simple**= Pas de nœuds personnalisés liés à la liste, pas de jonglage de cas de bord au-delà de la pile pops. Autres
**Language-agnostique** ► Œuvres en Java (`ArrayDeque`), Python (`collections.deque`), C++ (`std::deque`). Autres
**Parfait pour les interviews**= Les intervieweurs aiment la simulation basée sur la pile; facile à expliquer et à tester. Autres

**Idée de base**

- **La pile gauche** contient des caractères **gauche** du curseur.
- **La pile droite** contient des caractères **right** du curseur.
- **Insertion** → pousser sur la pile gauche.
- **Deletion** → pop de la pile gauche.
- **Déplacer à gauche** → Déplacer à gauche → Pousser à droite.
- **Déplacer à droite** → Déplacer à droite → Pousser à gauche.
- **Chiffres de résultats** → Regardez les 10 éléments du haut de la pile gauche.

Le **curseur** est implicitement la limite entre les deux piles.

---

### 2.4 L'Énorme – CordeBuilder + Indice de Curseur (Java)

**Pour**

- Utilise JavaS rapide `StringBuilder` pour la concaténation.
- Un seul tableau (chaîne) – pas de deques supplémentaires.

**Cons**

- `insert` et `delete` sont **O(n)** dans le pire des cas car `StringBuilder` doit déplacer les caractères.
Pour les contraintes données (k ≤ 40' et total ops ≤ 20 k), il est très bien, mais la complexité théorique est plus faible.
- Code doit gérer soigneusement les limites d'index; un petit bug peut causer `IndexOutOfBoundsException`.
- Pas idéal pour les intervieweurs qui s'attendent à des solutions de pile *pure* ou deque.

> **Quand l'utiliser? **
> Si vous codez un prototype à petite échelle ou une soumission LeetCode, cela fonctionne parfaitement. Pour une entrevue, mettez l'approche de pile à la place.

---

### 2.5 La liste "Ugly" – Classic Singly-Linked

Certaines personnes implémentent l'éditeur avec une liste de liens personnalisée ** basée sur des nœuds**:

- Chaque noeud stocke un caractère et un pointeur `next`.
- Oui. Le curseur est un pointeur vers un noeud.
- Insertion / suppression / mouvement sont tous O(k) en traversant les nœuds `k`.

Pourquoi c'est moche ?

Numéro
C'est pas vrai.
**Complexité du pointeur** Autres
**Mémoires en tête**= Chaque noeud est un objet – 8 octets (pointeur) + en-tête de l'objet. Autres
**Les erreurs hors-par-un sont fréquentes. Autres
**Les intervieweurs rejettent souvent le code de pointeur de bas niveau, sauf si vous êtes explicitement invité à mettre en place une liste liée. Autres

Si vous avez besoin d'une liste *real* doublement liée, vous devriez utiliser la bibliothèque standard (`LinkedList<Caracter>`) au lieu d'écrire la vôtre.

---

#### 2.5 La suite – Pourquoi être liée Liste nécessaire

Le problème est petit `k` (40) permet à *toute solution qui touche au plus des caractères `k` de passer.
Cependant, les intervieweurs testent aussi *en pensant à la complexité*.
Une solution basée sur la pile vous montre comment maintenir des opérations * amorties* O(1), ce qui est plus impressionnant qu'un hack "StringBuilder" naïf.

---

2.6 Cas de bord que vous devez tester

Bordure Quoi vérifier
C'est pas vrai.
Autres Déplacer à gauche le début passé. Autres
Autres Déplacer l'extrémité droite du curseur `cursorRight(100)` → s'arrête à `text.length()`. Autres
Autres Supprimez plus que la disponibilité. 3.
Toutes les opérations doivent fonctionner, en retournant des chaînes vides pour des mouvements de curseur. Autres
Ajouter une chaîne vide Aucun changement, le curseur reste. Autres
Return tous les caractères gauches. Autres

Toujours exécuter un script rapide pour vérifier ces dans la langue de votre choix.

---

2.7 Analyse de la complexité

Opération de l'espace supplémentaire
C'est quoi ?
"addText" **O(k)**O(k) pour les nouveaux caractères
"deleteText" **O(k)** Autres
"CursorLeft" (en anglais seulement) **O(k)** (en anglais seulement) O(1) – il suffit de déplacer des objets entre les piles
"MursorRight" **O(k)**

L'utilisation de la mémoire est linéaire dans le nombre de caractères stockés (2 × `n` octets pour deux piles).

---

### 2.8 Extraits de code de référence rapide

La langue Structure des données clés Autres
-- -- -- -- -- -- -- -- -- -- --------------------------------------------------
**Java**="StringBuilder text; int curseur;`=" retourne Math.min(k, curseur);` Autres
**Python**="deque gauche, droite;=" tout en étant enlevé < k et self.left: self.left.pop();=" Autres
**C++**=___________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________ Autres

> *Astuce*: Gardez la pile **left** comme l'histoire de l'éditeur. Cela rend la chaîne de résultat trivial: il suffit de regarder les 10 derniers éléments.

---

2.9 Comment réussir l'entrevue

1. ** Expliquez d'abord l'idée de la pile. **
Afficher les deux limites et la façon dont chaque opération cartographie pour empiler ops.
2. **Afficher la complexité sur papier** – O(k) pour les quatre méthodes.
3. **Écrire le code** – le garder court; ajouter des commentaires pour expliquer chaque ligne.
4. **Testez rapidement** – écrivez quelques assertions qui couvrent l'échantillon de l'énoncé du problème.
5. **Mentionner le suivi** – Et si k pouvait atteindre 105 ? → vous seriez toujours en territoire O(k).

Les recruteurs aiment les candidats qui peuvent *absorber* un problème (curseur + texte) dans une structure de données propre (deux piles). C'est ça le truc.

---

### 2.10 Appel à l'action

- **Essayez le code sur LeetCode** – copiez les extraits dans l'éditeur et exécutez le test d'échantillon.
- **Push votre solution à GitHub** avec un README clair; recruteurs souvent vérifier votre GitHub.
- **Appliquer aux postes d'entrevue de codage** qui nécessitent des compétences en manipulation de chaîne* – p. ex., ingénieur de backend, développeur mobile ou DevOps.
- **Planifier un entretien simulé** avec un ami; utiliser ce problème comme l'exercice de base*.

> *Votre prochaine question d'entrevue pourrait être : - Pouvez-vous implémenter un éditeur de texte basé sur un curseur dans votre langue préférée ? – être préparé avec la solution de pile ci-dessus! *

---

2.11 Pensées finales

Le LeetCode (Concevoir un problème d'éditeur de texte) n'est pas sur les algorithmes magiques ; c'est un puzzle de simulation** qui teste :

- Compréhension du temps amorti.
- Maîtrise des structures de données de base (piles, deques).
- Un code propre, sans bug.

La solution à deux piles est la norme **or** pour les entrevues. L'approche StringBuilder est soignée en Java, tandis que C++ offre un modèle très similaire `string + curseur`.

Choisissez la langue avec laquelle vous êtes le plus à l'aise, lancez le code contre le juge LeetCode, et vous allez entrer dans votre prochaine interview avec confiance.

> **Prêt à relever le prochain défi de LeetCode ? * *
> Restez à l'écoute pour plus de solutions prêtes à l'entrevue – laissez un commentaire ou DM moi si vous avez besoin d'aide pour préparer votre prochaine entrevue de codage!

---

### 2.12 Mots-clés

- `Concevoir un éditeur de texte "
- `Code de bord 2296 "
- 'Java StringBuilder "
- "Python deque" "
- `C++ deux piles "
- Entretien de manipulation de chaînes "
- "Mouvement de cursor" "
- Code d ' entretien d ' emploi "
- "O(k) complexité du temps "
- "Codage de la préparation de l'entrevue"

---

> **Codage heureux – et bonne chance d'atterrir ce travail de technologie de rêve! * *