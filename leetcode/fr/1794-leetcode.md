---
titre: LeetCode 1794. Nombre de paires de sous-chaînes égales avec différence minimale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Code Leet 1794 – Nombre de paires de sous-chaînes égales avec différence minimale
### A Deep-Dive, "Good-Bad-Ugly" Ventilation + Solution 3-Language (Java-Python C++)

> **SEO Mots-clés** – LeetCode, interview par algorithme, correspondance de chaînes, entretien de codage, solution Java, solution Python, solution C++, entretien d'emploi, structures de données, complexité temporelle, complexité spatiale, préparation d'entrevue, entretien d'ingénierie logicielle

---

Aperçu du problème

> **Code de bord 1794**
> *Moyenne

On vous donne deux chaînes `firstString` et `secondString` (deux lettres minuscules seulement).
Compter tous les quadruples index `(i, j, a, b)` qui satisfont:

Description
C'est pas vrai.
"0 ≤ i ≤ j < firstString.length" Autres
"0 ≤ a ≤ b < deuxièmeString.length" Autres
"FirstString[i ... j] == secondString[a ... b]"
"j - a" est **minimum** parmi tous les quadruples qui satisfont à ce qui précède.

Retournez le nombre de quadruples qui atteignent ce minimum "j - a".

> **Pourquoi est-ce intéressant? **
> Au premier coup d'oeil, il ressemble à un problème classique de sous-chaîne égale qui pourrait exploser combinatoirement.
> La torsion : la réponse n'a jamais besoin d'une sous-chaîne plus longue qu'un personnage !

---

C'est vrai. L'analyse de la qualité de l'eau

Aspect du bien
- C'est quoi ?
**Observations**= Les sous-chaînes 1-char suffisent → temps linéaire. Erreur d'interprétation de la différence minimale comme longueur la plus courte. Oublier que `j - a` peut être négatif; ignorer le signe. Autres
**Algorithme**. Entreposez la première occurrence de chaque lettre dans « firstString ». Itérer `secondString` à partir de la fin, calculer `diff = firstIdx[char] - i`. Edge‐cases: caractères répétés, aucune lettre commune → retourner `0`. Autres
**Complexité**= Temps `O(n + m)`, espace `O(26)`.= `O(n2)` serait temps-out sur `2·105`. La manipulation d'énormes cordes sans débordement (utiliser `int`; la différence correspond à `int`). Autres
**Code** : Clair, concis, aucune structure de données supplémentaire. Trop de boucles imbriquées → la lisibilité souffre. → NullPointerException en Java; erreurs hors-par-un dans les boucles C++. Autres
**SEO**=Utilisez des mots-clés populaires (=LeetCode=,=interview=,=string=,=Java=,=Python=,=C++=). Pauvre référencement : pas de tags, pas de densité de mots clés. Une suroptimisation du référencement peut nuire à la lisibilité. Autres

---

C'est vrai. La solution élégante

Le point de vue clé :
**Si deux sous-chaînes sont égales, vous pouvez toujours les réduire à un seul caractère correspondant sans augmenter `j - a`.**
Par conséquent, le minimum `j - a` est simplement la plus petite différence entre un indice dans `firstString` et un indice dans `secondString` pour un caractère commun.
Comptez combien de paires atteignent cette différence.

---

- Oui. 3‐Mise en œuvre des langues

> Toutes les solutions fonctionnent dans **O(n + m)** temps et **O(1)** espace (seulement 26 tableaux de taille).

---

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe {
public int countQuadruples(String firstString, String secondString) {
// Carte de chaque omble jusqu'à sa première occurrence en premierString
int[] firstIdx = nouveau int[26];
les tableaux.fill(premier Idx, -1);
pour (int i = 0; i < firstString.longueur(); i++) {
int c = firstString.charAt(i) - 'a';
si (premierIdx[c]) -1) premierIdx[c] = i; // stocker le plus tôt possible
}

int minDiff = entier.MAX_VALUE;
réponse int = 0;

// Scanner la secondeString de la fin au début
pour (int i = deuxièmeString.longueur() - 1; i >= 0; i--) {
int c = deuxièmeString.charAt(i) - 'a';
si (premierIdx[c]) -1) continuer;/ Chaîne

int diff = firstIdx[c] - i; // j - a avec j=i, b=i
si (diff < minDiff) {
minDiff = diff;
réponse = 1;
} sinon si (diff == minDiff) {
réponse++;
}
}
réponse de retour;
}
}
«» "

**Explication**
- `firstIdx` stocke l'index le plus proche de chaque lettre.
- Oui. Alors que l' itération `secondString` de dos en front, nous garantissons que `i` est le *dernier* possible `a` pour cette lettre, qui avec le plus tôt `i` de `firstString` donne le minimum `j - a`.
- Oui. Nous conservons le `minDiff` mondial et comptons combien de fois il se produit.

---

4.2 Python

'`python
Solution de classe:
def countQuadruples(self, firstString: str, secondString: str) -> Int:
premier_idx = [-1] * 26
pour i, ch dans l'énumération(premier pilier):
idx = ord(ch) - 97
si first_idx[idx] == - 1 :
first_idx[idx] = i # première occurrence (la plus petite)

min_diff = flotteur('inf')
nombre = 0

# itérer le secondString de la fin au début
pour i dans la plage (len(seconde chaîne) - 1, -1, -1):
idx = ord(secondString[i]) - 97
si first_idx[idx] == - 1 :
continuer # char pas en premier Chaîne

diff = first_idx[idx] - i # j-a avec j=i, b=i
si diff < min_diff:
min_diff = diff
nombre = 1
elif diff == min_diff:
nombre += 1

Nombre de retours
«» "

** Faits marquants de la physique* *
- Oui. Utilise une simple liste de taille 26 au lieu d'un dict pour la vitesse.
- `range(len(secondString) - 1, -1, -1)` donne une boucle inverse.

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int countQuadruples(chaîne première Chaîne, chaîne seconde chaîne) {
vecteur<int> premierIdx(26, -1);
pour (int i = 0; i < (int)firstString.size(); ++i) {
int c = première ligne[i] - 'a';
si (premierIdx[c]) -1) premierIdx[c] = i; // stocker le plus tôt possible
}

int minDiff = INT_MAX;
réponse int = 0;

pour (int i = (int)secondString.size() - 1; i >= 0; --i) {
int c = deuxièmeString[i] - 'a';
si (premierIdx[c]) -1) continuer;/ Chaîne
int diff = firstIdx[c] - i; // j - a
si (diff < minDiff) {
minDiff = diff;
réponse = 1;
} sinon si (diff == minDiff) {
++réponse;
}
}
réponse de retour;
}
};
«» "

**Pourquoi C++ fonctionne* *
- 'vecteur<int>' de taille 26 donne une recherche O(1).
- Oui. Pas de mémoire dynamique au-delà des deux cordes – parfait pour les contraintes d'entrevue.

---

## 5--Pièges communs et comment les éviter

Pourquoi ça arrive
- Oui.
En utilisant `HashMap<Caracter,Integer>` en Java et en accédant à une clé manquante → `NullPointerException` ou un tableau de taille 26
Commencer par `minDiff` à `0`.La différence minimale peut être négative. MAX_VALUE` / `INT_MAX`
Autres Compter les quadruples incorrectement quand `j-a` est négatif. Idx - i` directement
Autres Ignorer que les caractères répétés peuvent produire des paires minimales *multiple*
L'utilisation des sous-chaînes O(n2) est suffisante

---

# # # 6 Pourquoi ce problème a des répercussions sur les entrevues d'emploi

1. **Manipulation de la chaîne + Hashing** – Compétences de base pour de nombreux postes de backend.
2. **Optimisation intelligente** – Démontre la capacité de trouver l'observation clé (="seuls les caractères seuls comptent").
3. **Scalable Code** – la solution O(n+m) passe facilement 200k contraintes.
4. **Langue Agnostique** – Vous pouvez présenter la même logique en Java, Python ou C++ – parfait pour un portfolio.
5. **Edge‐Case Thinking** – Le traitement des différences négatives et des lettres répétées montre une rigueur.

> **Conseil pro**: Lorsque vous résolvez LeetCode 1794, soyez prêt à expliquer *pourquoi* la différence minimale est atteinte par les sous-chaînes 1 caractères. Cette perspicacité est souvent le moment que les intervieweurs cherchent.

---

C'est pas vrai. Dernier départ

> **Le minimum `j - a` est la plus petite différence entre un indice dans `firstString` et un indice ultérieur dans `secondString` pour toute lettre partagée. **
> Comptez les événements de cette différence – vous êtes fait.

Avec les solutions en 3 langues ci-dessus, vous pouvez déposer le code dans votre boîte à outils d'entrevue, flasher votre brillance **O(n+m)** et impressionner les recruteurs avec des explications propres, bien documentées et faciles à utiliser. C'est ce qu'il a dit.

---

**Codage heureux, et bonne chance d'atterrir ce rôle d'ingénierie logiciel!* *
*(Sentez libre pour atteindre si vous souhaitez une visite plus approfondie de l'implémentation Java ou aider à créer un blog avec ces solutions.) *