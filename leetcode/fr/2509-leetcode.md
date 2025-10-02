---
titre: LeetCode 2509. La longueur du cycle interroge dans un arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La longueur du cycle fait l'objet de demandes dans un arbre – un guide complet de solutions optimisées pour le référencement
> *LeetCode 2509 – Hard – Java / Python / C++*

---

Table des matières

Ce que vous apprendrez
- Oui.
Aperçu du problème Comprendre le problème du graphique et pourquoi il est dur
Point de vue sur les clés
Algorithme Solution étape par étape en anglais clair
Analyse de la complexité
Codes Java, Python et C++
Bonne, mauvaise et mauvaise Où l'approche brille, échoue, et comment changer
Pourquoi ce blog aide votre recherche d'emploi
À emporter rapidement

---

- Oui. 1. Aperçu du problème

> **Don** arbre binaire parfait avec des nœuds `2^n - 1` (root = 1).
> Pour chaque requête `[ai, bi]`:
> 1. Ajouter un bord entre les nœuds `ai` et `bi`.
> 2. Trouvez la longueur du cycle unique créé.
> 3. Supprimer le bord ajouté.

**Objectif:** Retourner un tableau de longueurs de cycle pour toutes les requêtes.

**Pourquoi difficile?* *
L'arbre peut avoir jusqu'à 2^30 - 1 noeuds (=1 milliard), mais nous ne recevons que 105 requêtes. Construire explicitement l'arbre est impossible ; nous devons répondre à chaque requête en temps *logarithmique*.

---

- Oui. 2. Aperçu clé – LCA est le secret

Un arbre binaire parfait construit comme un tas binaire a une règle de parent facile:

«» "
parent(v) = v / 2 (division entière)
«» "

Lorsque nous connectons deux nœuds `a` et `b`, le seul cycle qui peut apparaître est:

«» "
(LCA à b)
«» "

La longueur du cycle est égale

«» "
distance(a, LCA) + distance(b, LCA) + 1
«» "

Mais nous pouvons le calculer sans trouver explicitement la distance, en déplaçant simplement le nœud *large* vers le haut jusqu'à ce que les deux se rencontrent. Chaque pas vers le haut compte comme un bord, et nous ajoutons enfin un autre pour le bord nouvellement inséré.

---

- Oui. 3. Algorithme en anglais clair

«» "
pour chaque requête (a, b):
longueur = 1 // le bord ajouté
alors que a != b:
si a > b:
a = a / 2 //
Sinon:
b = b / 2 // déplacer b vers le haut
longueur += 1
durée du stockage
«» "

Pourquoi ça marche ?

- Déplacer le nœud plus grand vers le haut maintient le nombre total de mouvements minimal: nous réduisons toujours le plus grand des deux valeurs jusqu'à ce qu'elles deviennent égales.
- Chaque division correspond à traverser un bord d'arbre.
- La boucle se termine quand `a == b`, qui est exactement la LCA.
- La "longueur" finale est le nombre de bords du cycle.

---

- Oui. 4. Analyse de la complexité

Métrique Calcul Explication
- C'est quoi ?
Autres **Temps par requête**= `O(log n)`= Hauteur de l'arbre ≤ `log2(2n−1)` = `n`. Chaque itération de boucle réduit le noeud plus grand d'au moins un facteur de 2. Autres
**Temps total** Au maximum 30 * 105 φ 3 M opérations – facilement dans les limites. Autres
**Espace** Aucune structure de données auxiliaire n'est nécessaire. Autres

---

- Oui. 5. Code

Vous trouverez ci-dessous la solution **stand‐alone** pour chaque langue.
Chaque implémentation suit l'algorithme exact ci-dessus.

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int[] cycleLengthQueries(int n, int[][] requêtes) {
int m = requêtes. longueur;
int[] ans = nouveau int[m];
pour (int i = 0; i < m; ++i) {
int a = requêtes[i][0];
int b = requêtes[i][1];
longueur int = 1; // le bord ajouté
pendant que (a != b) {
si (a > b) a >>= 1; // a /= 2
b >>= 1; // b /= 2
++ longueur;
}
ans[i] = longueur;
}
le retour des an;
}

/* Facultatif: Main pour des tests manuels rapides */
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
[] [] q = {{5,3},{4,7},{2,3}};
Système.out.println(Arrays.toString(sol.cycleLengthQueries(3, q)));
// Produit: [4, 5, 3]
}
}
«» "

5.2 Python

'`python
Solution de classe:
def cycleLengthQueries(self, n: int, requêtes: List[List[int]]) -> Liste[int]:
ans = []
pour a, b dans les requêtes:
longueur = 1
alors que a != b:
si a > b:
a/= 2
Sinon:
b/= 2
longueur += 1
(longueur)
retour et

# Test rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.cycleLengthQueries(3, [[5,3],[4,7],[2,3]))
# Produit: [4, 5, 3]
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> CycleLengthQueries(int n, vector<vector<int>>& requêtes) {
vecteur <int> ans;
pour (auto &q : requêtes) {
int a = q[0], b = q[1];
int len = 1; // bord ajouté
pendant que (a != b) {
si a > b) a /= 2;
b/= 2;
++len;
}
le nom et l'adresse de l'utilisateur;
}
le retour des an;
}
};

// Main optionnelle pour les tests rapides
Int main() {
Solution sol;
vecteur<vector<int>> q = les points suivants sont ajoutés:
vector<int> res = sol.cycleLengthQueries(3, q);
pour (int x : res) cout << x << " ";
// Produit: 4 5 3
retour 0;
}
«» "

---

- Oui. 6. Bien, mal et mal

Aspects Bons Mauvaises / Gotchas
- Oui.
**Temps***** Rapide (`O(log n)` par requête). Pour *extrêmement* de nombreuses requêtes (`>106`), vous pouvez frapper le facteur constant d'E/S. Autres
**L'espace**
**Readability**= Logique très claire.= Néant.= Nécessite une compréhension de la division entière en tant que mouvement parent. Autres
Autres **Cas d'Edge**=Poigne les nœuds racine et feuille de façon transparente.=–=Si vous échangez accidentellement `a` et `b`, l'algorithme fonctionne toujours à cause de la symétrie. Autres
**Extensibilité**= Fonctionne pour *toute* arbre binaire complet.=–= Ne généralise **pas** aux arbres arbitraires – nécessite une fonction parentale. Autres
En Python, utiliser `//` (division entière). En C++, utilisez `/`. En Java, soyez prudent avec `>>` vs `/`. Autres

---

- Oui. 7. Faits saillants du référencement – Pourquoi ce blog aide votre carrière

1. **Mot-clé – titre* *
*La longueur du cycle interroge dans un arbre – LeetCode 2509 Solution dure (Java / Python / C++)* – correspond à ce que les recruteurs recherchent.

2. **Problèmes et étiquettes linguistiques* *
Utilise des balises comme `BinaryTree`, `LCA`, `LeetCodeHard`, `Interview`, `CodingInterview`, `Java`, `Python`, `C++`.
Les recruteurs filtrent souvent les candidats par ces étiquettes.

3. **Code clair et structuré**
Fournit des solutions *copie-colle*, réduisant la friction pour les recruteurs qui veulent voir le code propre.

4. ** Débat sur le rendement**
Affiche que vous pouvez résoudre d'énormes contraintes avec la complexité `O(log n)` – un vrai point de brag d'interview.

5. ** Autocontenu* *
Comprend `main` / harnais de test afin que vous puissiez exécuter et vérifier localement.

6. **Explication des cas de bord**
Montre la profondeur de la compréhension – les recruteurs aiment les candidats qui pensent aux conditions de bord.

---

- Oui. 7. TL;DR

- **Vue :** La longueur du cycle est égale au nombre de mouvements ascendants vers la LCA plus un.
- **Loop:** `alors que (a != b) { si (a > b) a /= 2; autre b /= 2; longueur++; }»
- **Résultat:** temps `O(m · log n)`, espace supplémentaire `O(1)`.
- **Langues:** Java, Python, C++ – même algorithme, petites différences de syntaxe.

---

- Oui. 8. Mots définitifs

Ce blog vous donne:

- Une solution *complete* pour LeetCode 2509 en **Java, Python et C++**.
- Un algorithme **facile à mettre en œuvre** qui fonctionne dans le temps *logarithmique* – un must-know pour toute entrevue algorithmique.
- Une rédaction claire et facile à lire* qui met en valeur vos compétences en résolution de problèmes et en codage auprès des employeurs potentiels.

Bon codage – et bonne chance d'atterrir ce rôle de rêve! Les