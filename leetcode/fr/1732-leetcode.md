---
titre: LeetCode 1732. Trouvez la plus haute altitude -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## ♫ Mastering LeetCode 1732 – *Trouver la plus haute altitude*
**Java, Python & C++ Solutions du SEO-Optimized Interview Guide**

---

Déclaration de problème (LeetCode 1732)

> Un motard commence au point 0 avec une altitude 0.
> Pour un tableau `gain` de longueur `n`, `gain[i]` est le changement d'altitude nette entre le point `i` et `i+1`.
> **Retourner la plus haute altitude que le motard atteint. **

Exemple Entrée Sortie Altitudes
- C'est quoi ?
[5,5,0,-7] Autres
[4, 3, 2] Autres

**Contrôles* *

Valeur de la propriété
C'est quoi ?
1 ≤ n ≤ 100
100 ≤ gain [i] ≤ 100 %

---

Pourquoi ce problème se pose pour la préparation de l'entrevue

Raison
C'est pas vrai.
**Facile**
**Scan linear**
**Somme cumulée**
**Numbers négatifs**

---

Intuition et approche

1. **Tirer l'altitude du courant** tout en passant par «gain».
2. **Tenir un maximum de course** de l'altitude vue jusqu'ici.
3. Retournez le maximum après la fin de la boucle.

> Il s'agit d'un simple problème de somme * courante*.
> Pas de structures de données supplémentaires, juste deux entiers.

---

Mise en œuvre (Java, Python, C++)

Voici des solutions propres et prêtes à la production dans les trois langues d'entrevue les plus populaires. Chaque solution fonctionne dans **O(n)** temps et **O(1)** espace supplémentaire.

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
publique Altitude(int[] gain) {
int maxAltitude = 0; // commencer au point 0
courant int = 0;

pour (int delta : gain) {
courant += delta; // mettre à jour l'altitude actuelle
maxAltitude = Math.max(maxAltitude, courant);
}
retour maxAltitude;
}

// Harnais d'essai rapide
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.plus grandeAltitude(nouvelle int[]{-5,1,5,0,-7}); // 1
Système.out.println(s.plus grandeAltitude(nouvelle int[]{-4,-3,-2,-1,4,3,2}); // 0
}
}
«» "

# # # # # #

'`python
Solution de classe:
plus Altitude(self, gain: List[int]) -> Int:
max_alt = 0
courant = 0
pour le delta en gain:
courant += delta
max_alt = max(max_alt, courant)
_retourner max

♪ Démo
si __nom__ == "__main__" :
s = Solution()
imprimer(s.plus grandeAltitude([-5, 1, 5, 0, -7])) # 1
imprimer(s.plus grandeAltitude([-4, -3, -2, -1, 4, 3, 2]) # 0
«» "

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
la plus grande Altitude(vecteur<int> et gain) {
Int maxAlt = 0, cur = 0;
pour (int d : gain) {
cur += d;
maxAlt = max(maxAlt, cur);
}
retour max Alt;
}
};

// Main simple pour un test rapide
Int main() {
Solution s;
vecteur <int> g1 = {-5, 1, 5, 0, -7};
vecteur<int> g2 = {-4, -3, -2, -1, 4, 3, 2};
cout << s.plus grandeAltitude(g1) << endl; // 1
Cout << s.plus grandeAltitude(g2) << endl; // 0
}
«» "

---

Les bons, les mauvais et les affreux

Catégorie: Ce que cela signifie Comment gérer les entrevues
Ce n'est pas le cas.
** Bon** **Complexité temporelle**: O(n) (linéaire). <br>• **Complexité spatiale**: O(1). <br>• Logique rectiligne. Mentionnez qu'il est souvent utilisé pour les questions d'interview -préfix sum. Autres
**Bad**) • Tous les nombres peuvent être négatifs → altitude max peut rester à 0. <br>• Le nom «gain» peut induire en erreur les débutants en pensant que vous devez trier ou utiliser une file d'attente prioritaire. Clarifier l'altitude initiale est 0, et vous n'ajoutez jamais * le point de départ au tableau. Autres
Erreurs hors-par-un: oubliant que la longueur du tableau est `n`, pas `n+1`. <br>• Sur-ingénierie: en utilisant un tableau ou une liste préfixe. Afficher une boucle concise; expliquer pourquoi vous pouvez garder un entier pour l'altitude actuelle. Autres

---

La complexité temporelle et spatiale

Complexité
C'est pas vrai.
**Heure**="O(n)" – passage unique par le "gain". Autres
**Espace** – seulement deux variables entières (`current`, `maxAltitude`). Autres

---

Cas de bord à tester

Raison du résultat prévu
- C'est pas vrai.
Autres Tous les positifs. L'altitude la plus élevée augmente monotoniquement.
Autres Tous les négatifs
Aucun effet sur l'altitude
Élément unique Taille minimale de l'entrée Autres
Une grande plage positive/négative.

---

Conseils d'entrevue

1. **Exposer l'intuition d'abord** – parler de la somme de course et de suivi max.
2. **Mention temps et espace** avant de plonger dans le code.
3. **Demander des éclaircissements**: L'altitude initiale est-elle toujours 0? Le tableau peut-il contenir des valeurs négatives ? (en milliers de dollars)
4. **Parcourez un exemple** dans l'entrevue pour montrer les changements d'état.
5. **Parler des cas de bord** – surtout tous les négatifs ou un seul élément.

---

À emporter

- **LeetCode 1732** est une victoire rapide* qui démontre la maîtrise des sommes préfixes et des scans linéaires.
- La maîtrise de ce problème met en évidence votre capacité à résoudre *clean, O(n) time, O(1) space* challenges – un ensemble attrayant de compétences pour les entretiens d'ingénierie logicielle.
- Oui. En fournissant des implémentations concises, lisibles, Java, Python et C++, vous impressionnerez les recruteurs qui apprécient la polyvalence du langage.

Bonne chance pour votre prochain entretien de codage ! C'est ce qu'il a dit.

---

**Mots-clés**: LeetCode 1732, Trouvez la plus haute Altitude, solution Java, solution Python, solution C++, somme d'exécution, somme de préfixe, question de codage d'entretien, interview d'algorithme, interview d'ingénieur logiciel, prép d'entretien de codage.