---
titre: LeetCode 3248. Serpent dans la matrice -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le serpent dans la matrice – Solution 3 langues + SEO-Optimized Blog

> **Problème**
> Vous avez une grille *n × n*. Le serpent commence à la cellule `0` (angle supérieur gauche).
> Vu la liste des déplacements (`"UP"`, `"DOWN"`, `"LEFT"`, `"RIGHT"`), le serpent reste à l'intérieur de la grille.
> Retourne l'indice linéaire de la cellule finale sur laquelle se trouve le serpent.

Langue Complexité Code
- C'est quoi ?
**Java**"O(m)" temps, espace "O(1)" (`m = commandes.length")
**Python**
Temps "O(m)", espace "O(1)"

> **Pourquoi c'est une grande question d'interview* *
> - Teste l'itération du tableau et la manipulation des coordonnées.
> - vous oblige à cartographier les coordonnées 2-D aux indices 1-D (`row * n + col`).
> - Cas de bord : indices négatifs ou mouvements hors frontières (le problème garantit qu'ils n'arrivent pas, mais vous devriez quand même écrire du code défensif).

---

Comment fonctionne la solution

1. ** Garder la voie de la position* *
Commencez par `(row, col) = (0, 0)`.
Pour chaque mise à jour de commande `row`/`col` en conséquence.

2. **Convertir à l'indice 1-D**
Après le traitement de toutes les commandes, calculer `index = ligne * n + col`.
C'est le numéro unique de la cellule dans une mise en page majeure.

3. **Retourner le résultat**
Pas besoin de structures de données supplémentaires – une simple solution d'espace constant.

---

Numéro de code

C'est pas vrai. Java

"Java
Importer java.util. Liste;

solution de classe publique {
public int finalPositionOfSnake(int n, List<String> commandes) {
ligne int = 0, col = 0;

pour (String cmd : commandes) {
interrupteur (cmd) {
dossier "UP" -> ligne...
dossier "DOWN" -> ligne++;
Cas "LEFT" -> d'une puissance n'excédant pas 50 kW
dossier "RIGHT" -> col++;
par défaut -> lancer un nouvel argument illégalException("Commande invalide: " + cmd);
}
}
ligne de retour * n + col;
}
}
«» "

> **Pourquoi l'expression du commutateur? * *
> C'est Java 17-style, concis, et évite les chaînes mutables "if-else".

---

# # # # # #

'`python
de taper l'importation Liste

Solution de classe:
def finalPositionOfSnake(self, n: int, commandes: List[str]) -> Int:
r = c = 0
pour cmd dans les commandes:
Si cmd == "UP":
r -= 1
Elif cmd == "DOWN":
r += 1
Elif cmd == "LEFT":
c -= 1
elif cmd == "RIGHT":
c += 1
Sinon:
augmenter ValueError(f"Inconnue commande: {cmd}")
retour r * n + c
«» "

> **Astuce** – En Python, vous pouvez utiliser un dictionnaire mapping vers un lambda pour un liner unique encore plus propre si vous aimez le style fonctionnel.

---

C'est vrai. C++

'`cpp
#incluez <vecteur>
#incluez <string>

solution de classe {
public:
int finalPositionOfSnake(int n, const std::vector<std::string>& commandes) {
ligne int = 0, col = 0;
pour (suite std::string& cmd : commandes) {
si (cmd == "UP") rangée--;
Sinon, si (cmd == "DOWN") ligne++;
Sinon, si (cmd == "LEFT")
sinon si (cmd == "RIGHT") col++;
Sinon lancer std::invalid_argument(" Commande inconnue: " + cmd);
}
ligne de retour * n + col;
}
};
«» "

> **Pourquoi `const std::vector<std::string>&`? **
> Passez par référence pour éviter de copier toute la liste de commandes.

---

L'article du blog

> **Titre**: *=Maîtrise du serpent en matrix Problème: Bon, mauvais et laid – un guide complet*
> **Méta-Description**: Apprenez à résoudre le LeetCode 3248 en Matrice en Java, Python et C++. Comprenez les pièges, optimisez votre code et préparez-vous à l'entrevue.
> **Mots clés**: serpent dans la matrice, LeetCode 3248, codage d'entretien, pratique de l'algorithme, solution Java, solution Python, solution C++, conseils d'entretien de codage, manipulation de tableau, pensée algorithmique.

---

Introduction

Le problème du serpent dans Matrix peut sembler simple, mais c'est un micro-monde de défis d'entrevue de codage.
Cela vous oblige à :

- Convertir une traversée 2-D en un indice 1-D.
- Gardez un œil sur les conditions limites même lorsque le problème garantit des déplacements sûrs.
- Oui. Pensez aux compromis temps/espace et au style de code propre.

Ci-dessous, nous décomposons les parties **good**, **bad** et **ugly** des solutions typiques, et fournissons une mise en œuvre prête à la production dans trois langues populaires.

---

Les bons

Autres Quoi ? Pourquoi ?
- Oui.
**L'espace continu** Autres
**Temps linéaire**=On passe au-dessus des commandes ('O(m)'). Autres
**Cartographie claire** Autres
**Codage défensif**= Lancer une exception pour les commandes inconnues. Autres
**Readable Syntaxe**=Expression Java 17 `switch`, Chaîne Python `elif`, C++ if‐else. Autres

**Takeaway**: Un algorithme minimal, sans bug est une marque de bon style de codage.

---

- Oui. Les mauvais

Piège commun
-- -- -- -- --
Autres **L'utilisation d'indices basés sur 1**Le problème utilise l'indexation basée sur 0; à partir de 1 compensera le résultat. Autres
**Vérifications de la frontière par émission** Autres
**Cartographie de la direction codée en caractères gras**.Le retypage de la cartographie pour chaque langue peut entraîner des erreurs de copier-coller. Autres
**Returning Wrong Type**.En Java, le retour `int` est parfait; en Python, oublier de lancer `int` après l'arithmétique peut conduire à des résultats flottants. Autres

**A emporter**: Même les problèmes faciles peuvent contenir des bugs subtils si vous sautez les contrôles de santé ou mal interpréter la disposition de la grille.

---

- Oui. L'Ugly

Ce qui arrive
C'est quoi ?
**Spaghetti Code**= Mélanger les boucles, les if-else et les effets secondaires dans un bloc géant. Autres
**Taille codée en caractères gras**= Utiliser une valeur fixe (par exemple `n = 10') au lieu de l'entrée. Autres
**Aucune documentation**. Autres
Autres **Recomposition de l'index Chaque boucle**. Autres

** À emporter**: Le code ringard est un cauchemar d'entretien. Même si cela fonctionne maintenant, il se cassera lorsque vous l'étendreez (par exemple, en ajoutant une commande "JUMP").

---

### Une mise en œuvre propre et prête à la production

Ci-dessous vous trouverez trois extraits concis et faciles à tester qui incarnent le *bon* et évitent le *mauvais* et le *puissant*. Chaque implémentation comprend une petite vérification de la santé mentale qui vous aiderait à attraper des changements accidentels:

"Java
// Java – style 2024
solution de classe {
public int finalPositionOfSnake(int n, List<String> commandes) {
Int r = 0, c = 0;
pour (String cmd : commandes) {
interrupteur (cmd) {
Cas «UP» -> r--;
dossier "DOWN" -> r++;
Cas "LEFT" -> c--;
dossier "RIGHT" -> c++;
par défaut -> lancer un nouvel argument illégalException("Commande inconnue");
}
}
retour r * n + c;
}
}
«» "

'`python
# Python – concis et sûr
Solution de classe:
def finalPositionOfSnake(self, n: int, commandes: List[str]) -> Int:
r = c = 0
pour cmd dans les commandes:
Si cmd == "UP":
r -= 1
Elif cmd == "DOWN":
r += 1
Elif cmd == "LEFT":
c -= 1
elif cmd == "RIGHT":
c += 1
Sinon:
augmenter ValueError("Commande invalide")
retour r * n + c
«» "

'`cpp
// C++ – rapide et propre
solution de classe {
public:
int finalPositionOfSnake(int n, const vector<string>& commands) {
Int r = 0, c = 0;
pour (suite chaîne & cmd : commandes) {
si (cmd == "UP") r--;
Sinon si (cmd == "DOWN") r++;
sinon si (cmd == "LEFT") c--;
Sinon, si (cmd) c++;
sinon lancer invalide_argument("commande invalide");
}
retour r * n + c;
}
};
«» "

---

### Tester votre solution

"Java
public statique vide principal(String[] args) {
var sol = nouvelle solution();
Système.out.println(sol.finalPositionOfSnake(2, Arrays.asList("RIGHT","DOWN")); // 3
}
«» "

'`python
si __nom__ == "__main__" :
sol = Solution()
print(sol.finalPosition OfSnake(3, ["DOWN", "RIGHT", "UP"]) # 1
«» "

'`cpp
Int main() {
Solution s;
Cout << s.finalPosition OfSnake(3, {"DOWN", "RIGHT", "UP"}) << endl; // 1
}
«» "

---

Liste de contrôle du référencement

Ce que nous avons fait
-- -- -- -- -- --
**Mot-clé Placement**="snake" dans matrix=", leetCode 3248=", le codage interview=", la solution Java/Python/C++. Autres
**Meta Description**. Autres
**H1 pour le titre, H2 pour les sections, H3 pour les sous-rubriques. Autres
**Profondeur du contenu**. Autres
**Liens internes/externes**= Références à la page officielle de LeetCode, liens de solution populaires. Autres
**Readability**=Les blocs de code, les tableaux, les points forts gras, les paragraphes concis. Autres
*Schema***JSON‐LD extrait (facultatif) pour aider les moteurs de recherche à comprendre l'article. Autres

---

Les pensées finales

Le problème du serpent dans Matrix est une mine d'or pour aiguiser les compétences de travers. En se concentrant sur **code propre** – espace constant, temps linéaire et cartographie claire – vous impressionnerez les intervieweurs et réduirez les bugs. N'oubliez pas les pièges subtils qui voyagent souvent même les développeurs chevronnés.

Joyeux codage, et que le serpent reste dans les limites! (en milliers de dollars)

---