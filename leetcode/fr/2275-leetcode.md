---
titre: LeetCode 2275. La plus grande combinaison avec bitwise et plus que zéro -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

## LeetCode 2275 – La plus grande combinaison avec Bitwise et plus Plus que zéro
**Langues:** C++
**Difficulté:** Moyenne
** Pertinence de l'entrevue :** Les opérations, le comptage et la manipulation du réseau sont des éléments essentiels des entrevues de codage de l'ingénierie logicielle.

---

### TL;DR
Pour obtenir le plus grand sous-ensemble de nombres dont AND est > 0, comptez combien de nombres ont chaque bit.
La réponse est le nombre maximum parmi les 32 bits.

Langue Heure Espace
- C'est quoi ?
* * * * * * * * * * *
Python **O(n × 32)**
* * * * * * * * * * *

---

- Oui. Pourquoi ce problème est-il à l'origine de l'entrevue

* **Shows comprehension of bit-wise operators** – le cœur de nombreuses questions de faible niveau et de programmation de systèmes.
* ** Nécessite une observation intelligente** – vous n'avez pas besoin d'examiner tous les sous-ensembles ; un seul passage par bit suffit.
* **Cours en temps linéaire** – parfait pour les grandes entrées (jusqu'à 105).

---

## Aperçu de la solution (Le plus facile)

1. **Il s'agit de 32 bits** (0 ... 31).
2. Pour chaque bit, ** compter combien de nombres contiennent ce bit** (`candidate & (1 < bit)`).
3. Gardez le nombre **maximum** sur tous les bits – c'est la taille de la plus grande combinaison valide.

L'intuition : Si chaque nombre d'une combinaison a le même jeu de bits, l'ET de tous les nombres contiendra également ce bit et sera donc > 0. Inversement, si un peu n'est pas partagé par suffisamment de nombres, l'ET passera à 0.

---

## Mise en œuvre du code

### Java

"Java
Importation de java.util.*;

solution de classe publique {
public int le plus grandCombination(int[] candidats) {
= 0;
// il n'y a que 32 bits dans un int Java
pour (int bit = 0; bit < 32; bit++) {
nombre int = 0;
masque int = 1 << bit;
pour (int num : candidats) {
si ((num & masque) != 0) nombre++;
}
si (compte > max) max = nombre;
}
retour max;
}

public statique vide principal(String[] args) {
Solution s = nouvelle solution();
[] a = {16, 17, 71, 62, 12, 24, 14};
Système.out.println(s.plus grandeCombinaison(a)); // 4
}
}
«» "

Python

'`python
Solution de classe:
plus grandCombination(même, candidats: list[int]) -> Int:
max_cnt = 0
pour la plage de bits(32):
masque = 1 << bits
cnt = somme (1 pour num dans les candidats si num & masque)
si cnt > max_cnt:
max_cnt = cnt
_retour maxcnt


♪ Démo
si __nom__ == "__main__" :
sol = Solution()
[16, 17, 71, 62, 12, 24, 14]
print(sol.plus grandeCombinaison(arr)) # 4
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
dans la plus grandeCombination(vecteur<int> et candidats) {
int best = 0;
pour (int bit = 0; bit < 32; ++ bit) {
masque int = 1 << bit;
cnt = 0;
pour (int num : candidats)
si (num & masque) ++cnt;
best = max (meilleur, cnt);
}
le meilleur retour;
}
};

Int main() {
Solution s;
vecteur <int> a = {16, 17, 71, 62, 12, 24, 14};
cout << s.m.combinaison(a) << endl; // 4
}
«» "

---

## Explication étape par étape (pour les intervieweurs)

1. **Pourquoi 32 bits? **
Tous les nombres indiqués correspondent à un entier signé 32 bits («1 ≤ candidats[i] ≤ 107»). Nous ne pouvons en sécurité itérer que 32 fois.

2. ** Avec un masque* *
`mask = 1 << bit` crée un nombre binaire avec seulement la position *bit‐th* définie.
`num & masque` est non-zéro iff que le bit est défini dans *num*.

3. ** Maximiser le nombre**
Le plus grand ET est réalisé lorsque nous choisissons le morceau qui apparaît le plus souvent. La taille de ce sous-ensemble est exactement ce qui compte.

4. **Heure et espace**
*Temps:* 32 × n opérations → **O(n)**.
*Espace:* Quelques variables entières → **O(1)**.

---

## Bonne, mauvaise et laid de ce problème

Aspect du bien
- C'est quoi ?
**Limpidité conceptuelle**La perspicacité bit-wise est élégante et facile à expliquer. Nécessite la conscience que *toute * commune suffit – pas évident à première vue. Les solutions naïves (vérification de tous les sous-ensembles) sont exponentielles ; beaucoup d'effort gaspillé. Autres
**Efficacité**La solution O(n) fonctionne rapidement même pour 105 entrées. Autres La constante 32 bits pourrait prêter à confusion pour ceux qui pensent en termes de nombres 64 bits. Des implémentations qui pré-calculent les fréquences bit de façon incorrecte (par exemple, en utilisant un `HashMap` par bit) ajoutent des frais généraux inutiles. Autres
**Cas d'Edge**= Fonctionne pour les tableaux de taille 1 ou tous les nombres identiques. Il faut gérer le cas où tous les nombres sont nuls – mais les contraintes interdisent les zéros. Autres
**L'impact de l'entrevue**Le candidat démontre une pensée concise et une manipulation bit. Il est difficile de comprendre que le ET d'un seul numéro peut causer des erreurs hors d'un seul numéro. Autres

---

## Article de blog optimisé du SEO

> **Titre:** *Cracking LeetCode 2275 – La plus grande combinaison avec Bitwise ET > 0 (Java, Python, C++)*
> **Meta Description:** Apprenez la solution la plus rapide à LeetCode 2275, une question d'entrevue bitwise moyennement difficile. Obtenez le code Java, Python et C++, le raisonnement étape par étape et les conseils d'entrevue pour aser votre entretien d'emploi.

---

- Oui. 1. Présentation

Lorsque vous préparez des entrevues d'ingénierie logicielle, vous rencontrez souvent des problèmes **bitwise ET**. Un défi populaire LeetCode est **2275 – La plus grande combinaison avec Bitwise ET plus grand que zéro**. Dans ce billet, nous allons:

- Divisez la déclaration de problème
- Présenter une solution O(n) claire
- Fournir des implémentations complètes Java, Python et C++
- Discutez pourquoi cette question est une mine d'or pour les intervieweurs
- Offrez des idées et des conseils d'entrevue -

---

- Oui. 2. Rétablissement des problèmes

> **Donné :** Une série d'entiers positifs "candidats".
> **Tâche:** Trouvez la taille du plus grand sous-ensemble dont ET est **plus grand que 0**.
> **Retour :** Taille maximale.

---

- Oui. 3. Intuition et perspectives clés

Pour que l'ET d'un ensemble soit > 0, il doit y avoir au moins un bit qui est **set dans chaque élément** de cet ensemble.
Le problème se réduit donc à:

> *Trouvez le bit qui apparaît dans le plus de nombres et retournez qui comptent. *

---

- Oui. 4. Algorithme en Pseudocode

«» "
Taille max = 0
pour bit de 0 à 31:
nombre = 0
masque = 1 << bits
pour les candidats:
si num & masque & #160;:
nombre += 1
maxSize = max(maxSize, nombre)
retour maxSize
«» "

---

- Oui. 5. Analyse de la complexité

Métrique
- C'est quoi ?
Temps O(n × 32) → O(n)= O(n × 32) → O(n)= O(n × 32) → O(n)=
Espace

---

- Oui. 6. Extraits de code complet

*Voir la section précédente sur l'implémentation du code pour le code propre et commenté dans chaque langue. *

---

- Oui. 7. Pourquoi les intervieweurs aiment cette question

- **Maîtrise bitwise** – fait preuve de confort avec les opérateurs de bas niveau.
- **O(n) solution** – test la capacité de transformer un problème combinatoire en un problème de comptage.
- ** raisonnement clair** – les candidats peuvent articuler une preuve courte et élégante de la justesse.

---

- Oui. 8. Bien, mal, Méchant

- **Bien:** Tout droit, rapide et facile à expliquer.
- **Bad:** L'hypothèse 32-bit peut faire monter les gens s'ils ne sont pas conscients de la taille entière.
- **Ugly:** La génération du sous-ensemble Brute-force conduit à un temps exponentiel, un piège facile pour les candidats non préparés.

---

- Oui. 9. Conseils d'entrevue

1. **Décrivez d'abord les principaux points de vue** – Nous avons besoin d'un peu commun à tous les nombres dans un sous-ensemble. (en milliers de dollars)
2. **Parcourez l'algorithme** – mentionnez le masque de bits et les deux boucles.
3. **Cas de bord de discussion** – p.ex., tableaux à éléments uniques, nombres identiques.
4. **Les compromis entre le temps et l'espace** – confirment que nous faisons O(n) et O(1).
5. **Afficher le code** – écrire à la main les boucles de base; la lisibilité est importante.

---

10 ans. Réflexions finales

Mastering LeetCode 2275 non seulement stimule votre portefeuille, mais montre également les recruteurs, vous pouvez repérer les motifs et écrire un code efficace. Gardez cette solution dans votre playbook d'entrevue, et vous allez gérer n'importe quel bitwise ET questionner avec confiance.

---

11 ans. Appel à l'action

Vous voulez d'autres solutions prêtes à l'entrevue?
- **S'abonner** à notre newsletter pour les défis de codage hebdomadaires.
- **Télécharger** notre guide interview‐prep pour une plongée plus profonde dans les problèmes bitwise.
- **Partager** votre propre approche dans les commentaires ci-dessous!

---

**Codage heureux, et bonne chance pour votre prochaine interview! * *

---

*Word compter:* - 1 200
*Mots clés:* LeetCode 2275, bitwise ET, question d'entrevue, solution Java, solution Python, solution C++, entretien d'emploi, génie logiciel, pensée algorithmique

---

Ceci complète le guide complet, prêt à l'entrevue et un billet de blog SEO-friendly pour vous aider à présenter ce défi LeetCode dans votre recherche d'emploi. Bonne chance ! C'est ce qu'il a dit