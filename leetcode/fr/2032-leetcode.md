---
titre: LeetCode 2032. Deux sur trois -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2032 – Deux sur trois
**Difficulté:** Facile
**Tag:** Array, HashMap, manipulation bit, deux pointeurs

> **Objectif :** Retournez chaque entier qui apparaît dans *au moins deux* des trois tableaux d'entrée.

> **Constraints**
> * `1 ≤ nums1.longueur, nums2.longueur, nums3.longueur ≤ 100`
> * `1 ≤ nombres1[i], nombres2[i], nombres3[i] ≤ 100`

---

Pourquoi ce problème est une mine d'or pour les entretiens d'embauche

Pourquoi ça compte ?
- Oui.
Autres **Utilisation de l'ensemble / de la carte** Autres
**Bit‐mask tricks**= Montre la créativité algorithmique – surtout pour les langues à faible niveau de support (C++). Autres
**Manipulation d'un boîtier d'Edge**=Illustre la robustesse – manipulation des duplicatas et des intersections vides. Autres
**Analyse de la complexité**= Permet de discuter des solutions O(n) et O(n2) – un point de conversation classique. Autres

> **SEO crochet:** *LeetCode Two of Three solution in Java, Python, C++ – facile interview prep

---

Aperçu de la solution

Le problème est essentiellement un problème de fréquence sur trois petites gammes entières (1‐100).
Quatre approches communes:

1. **HashSet** – ajouter chaque tableau à un ensemble, compter les occurrences.
2. **Fréquence Array (taille 101)** – booléens ou ints; pas de contenants supplémentaires.
3. **Bit‐masque (3 bits)** – représentation compacte de la présence dans chaque tableau.
4. **Trier + Deux points** – pas nécessaire pour les contraintes données mais éducatif.

Le **Frequence Array** (option 2) est le plus simple et le plus rapide en pratique pour ce problème, et fonctionne dans les trois langues sans bibliothèques externes.
Vous trouverez ci-dessous un code propre et prêt à la production dans **Java, Python et C++**.

---

Application Java (pas de collections externes)

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe {
liste publique<entier> deuxOutOffTrois(int[] nums1, int[] nums2, int[] nums3) {
// Des tableaux booléens pour marquer la présence de nombres (1‐100).
booléen[] présent1 = nouveau booléen[101];
booléen[] présent2 = nouveau booléen[101];
booléen[] présent3 = nouveau booléen[101];

pour (int n : nombres1) présent1[n] = vrai;
pour (int n : nombres2) présent2[n] = vrai;
pour (int n : nombres3) présent3[n] = vrai;

Liste du résultat <entier> = nouvelle liste de distribution<>();

// Les nombres sont de 1 à 100 inclusivement; ils sont exprimés sur cette plage fixe.
pour (int i = 1; i <= 100; i++) {
// Comptez combien de tableaux contiennent ce nombre.
nombre int = 0;
si (présent1[i]) count++;
si (présent2[i]) count++;
si (présent3[i]) count++;

si (compter >= 2) résultat.add(i);
}

le résultat du retour;
}
}
«» "

**Complexité* *
- *Heure*: `O(n1 + n2 + n3 + 100)` → `O(n)`
*Espace*: "O(1)" (constant 3 × 101 booléens)

---

Mise en œuvre de Python

'`python
de taper l'importation Liste

Solution de classe:
def twoOutOfThree(self, nums1: List[int], nums2: List[int], nums3: List[int]) -> Liste[int]:
# Tableau de fréquences pour les numéros 1..100
freq = [0] * 101

pour n en nombres1:
[n] += 1
pour n en nombres2:
[n] += 1
pour n en nombres3:
[n] += 1

# Recueillir des chiffres qui apparaissent au moins deux fois
retour [i pour i dans l'intervalle(1, 101) si freq[i] >= 2]
«» "

**Complexité** – identique à Java.

---

## C++ Implémentation (aucun conteneur STL, seul vecteur)

'`cpp
#incluez <vecteur>

solution de classe {
public:
std::vector<int> deuxOutOfThree(std::vector<int>& nums1,
À noter::vector<int>& nums2,
L'objectif est de faire en sorte que l'utilisation de l'énergie nucléaire puisse être considérée comme une source d'énergie.
// Drapeaux booléens pour chaque valeur possible
bool p1[101] = {faux};
bool p2[101] = {faux};
bool p3[101] = {faux};

pour (int n : nombres1) p1[n] = vrai;
pour (int n : nombres2) p2[n] = vrai;
pour (int n : nombres3) p3[n] = vrai;

std::vector<int> res;
pour (int i = 1; i <= 100; ++i) {
(p1[i] ? 1 : 0) + (p2[i] ? 1 : 0) + (p3[i] ? 1 : 0);
si (cnt >= 2) res.push_back(i);
}
retour rés;
}
};
«» "

**Complexité** – temps `O(n)`, espace supplémentaire `O(1)`.

---

Les bons, les mauvais et les méchants

Le bon Le mauvais Le mauvais
- C'est quoi ?
**Readability**La fréquence-array approche utilise une seule boucle et une taille fixe, ce qui la rend *très* facile à comprendre. Elle s'appuie sur l'hypothèse cachée selon laquelle les valeurs se situent dans le «1‐100». Des limites codées en dur rendent la solution fragile pour d'autres contraintes. Autres
**Performance** Aucun inconvénient de performance pour des limites données. L'utilisation d'un jeu ajouterait des frais généraux `O(1)` par insert mais toujours O(n). Autres
**Scalabilité**= Fonctionne pour toute plage entière délimitée; il suffit d'ajuster la taille du tableau. Si la plage d'entrée s'étend à `109`, une carte de hachage devient obligatoire. Autres Sur-ingénierie : des astuces bit-mask pour une saisie aussi petite ajoutent une complexité inutile. Autres
**Language-agnostic** ► Fonctionne sous forme inchangée en Java, Python, C++.

### À emporter pour les entrevues de travail

- **Expliquez vos compromis**: -J'ai utilisé un tableau de fréquences parce que la plage de valeurs est petite (1‐100). S'il était plus grand, j'utiliserais une carte de hachage ou un bit-mask. (en milliers de dollars)
- **Cas de bord de Mention**: les duplicata à l'intérieur d'un seul tableau ne comptent pas parce que nous utilisons des drapeaux booléens.
- **Afficher votre style de code**: Gardez de petites fonctions, utilisez des noms descriptifs et commentez lorsque la logique n'est pas évidente.

---

Article de blog optimisé du SEO

> **Titre**
> *LeetCode Two of Three – Java, Python, C++ Solutions pour les ingénieurs logiciels*

> **Description détaillée**
> Master LeetCodeS est un problème de deux sur trois avec des solutions Java, Python et C++ propres. Comprendre les meilleurs compromis algorithmiques, les cas de bord et les points d'entrevue.

> **Mots clés**
> LeetCode Two of Three, solution LeetCode, prép d'interview, solution Java, solution Python, solution C++, jeu de hachage, masque bit, problèmes de tableau, codage d'entretien d'emploi

---

Introduction

Si vous êtes à la recherche d'un rôle front-end, back-end ou full-stack, la question de LeetCode « Deux sur trois » apparaît dans de nombreuses piles d'entrevues. C'est un problème classique *fréquence-compte* qui vous permet de montrer vos connaissances sur les structures de données, l'analyse de l'espace temporel et les pratiques de codage propres.

Dans ce post, nous lisons:

1. Passez par le problème et les contraintes.
2. Comparez trois stratégies de solutions populaires.
3. Présentez le code Java, Python et C++ prêt à la production.
4. Mettez en avant le bon, le mauvais, et le laid.
5. Enveloppez-vous de points de discussion prêts à l'entrevue.

---

Récapitulation du problème

On vous donne trois tableaux entiers `nums1`, `nums2`, `nums3`.
Retourner une liste de tous les entiers distincts qui apparaissent dans **au moins deux** des tableaux. L'ordre de la sortie ne compte pas.

Contraintes:

- Chaque longueur de tableau est de 1 à 100.
- Les éléments sont entre 1 et 100.

---

### Stratégies de solution

Démarche
C'est quoi ?
**HashSet** (3 jeux + carte de comptage) . Simple à comprendre; généralité .
**Fréquence Array** (taille 101 booléens)
**Bit-mask** (3 bits par numéro) Extrêmement compact; idéal pour l'interview show‐off , plus difficile à lire; seulement utile pour les contraintes serrées ,

Pour les contraintes de LeetCode, le tableau **fréquence** est le bon endroit. Il fonctionne dans le temps linéaire et utilise une mémoire négligeable. C'est exactement pourquoi c'est la première solution dans l'éditorial.

---

Captures de code

C'est vrai. Java

"Java
solution de classe {
liste publique<entier> deuxOutOffTrois(int[] nums1, int[] nums2, int[] nums3) {
booléen[] p1 = nouveau booléen[101];
booléen[] p2 = nouveau booléen[101];
booléen[] p3 = nouveau booléen[101];

pour (int n : nombres1) p1[n] = vrai;
pour (int n : nombres2) p2[n] = vrai;
pour (int n : nombres3) p3[n] = vrai;

Liste <Integer> res = nouvelle liste de distribution<>();
pour (int i = 1; i <= 100; i++) {
(p1[i] ? 1 : 0) + (p2[i] ? 1 : 0) + (p3[i] ? 1 : 0);
si (cnt >= 2) res.add(i);
}
retour rés;
}
}
«» "

Python

'`python
Solution de classe:
def twoOffOfTrois (soi, nums1, nums2, nums3):
freq = [0] * 101
pour n en nombres1: freq[n] += 1
pour n en nombres2: freq[n] += 1
pour n en nombres3: freq[n] += 1
retour [i pour i dans l'intervalle(1, 101) si freq[i] >= 2]
«» "

C++

'`cpp
solution de classe {
public:
vectorielle<int> deuxOutreTrois(vecteur<int>&nums1,
vectorielle<int> & nums2,
vecteur <int>& nums3) {
bool p1[101] = {faux}, p2[101] = {faux}, p3[101] = {faux};

pour (int n : nombres1) p1[n] = vrai;
pour (int n : nombres2) p2[n] = vrai;
pour (int n : nombres3) p3[n] = vrai;

vecteur<int> rés;
pour (int i = 1; i <= 100; ++i) {
(p1[i] ? 1 : 0) + (p2[i] ? 1 : 0) + (p3[i] ? 1 : 0);
si (cnt >= 2) res.push_back(i);
}
retour rés;
}
};
«» "

---

Les bons, les mauvais, les méchants

- **Bonne**: Les trois extraits partagent la même idée de base — compter chaque nombre une fois par tableau — et tourner dans le temps "O(n)".
- **Bad**: La valeur de 100 est cachée dans le code. Si les contraintes changent, la solution se brise.
- **Ugly**: Il n'est pas nécessaire de faire une surcomplication avec le bit-masking pour une gamme 1‐100. Gardez-le simple, sauf si l'interview demande explicitement la solution la plus compacte.

---

### Points d'entrevue prêts à parler

1. **Pourquoi un tableau de fréquence? * *
Le problème garantit que toutes les valeurs sont ≤ 100, donc un simple tableau booléen suffit.

2. **Doublons à main**
L'utilisation de drapeaux booléens garantit que chaque tableau est compté au plus une fois par valeur, ce qui rend les duplications à l'intérieur d'un seul tableau non pertinentes.

3. ** compromis temps/espace**
Temps O(n), espace O(1). Si la plage de valeurs était plus grande, le changement d'i=d vers un `HashMap`.

4. **Délibérations**
- Un tableau vide ? Impossible en raison de contraintes.
- Les trois tableaux contiennent le même numéro ? Produit ce numéro.

5. **Tests**
- Présenter quelques essais unitaires (par exemple, solution d'assert). [1,2,3].»
- Oui. Cela démontre le codage défensif.

---

Clôture

Deux sur trois est trompeurment simple, mais ouvre une fenêtre dans votre état d'esprit de résolution de problèmes. En maîtrisant la stratégie d'arrachage de fréquences à travers **Java, Python et C++**, vous êtes prêt à répondre à des questions similaires, qu'elles apparaissent sur LeetCode, lors d'entretiens techniques ou lors de vos tâches quotidiennes de codage.

Bon codage, et bonne chance d'obtenir cet entretien d'embauche! C'est ce qu'il a dit.

---

**Références**
- LeetCode Editorial – Deux sur trois
- [Cracking the Coding Interview] (https://www.oreilly.com/library/view/craking-the-coding/9780988785857)

---

> **Appel à l'action**
> Vous voulez plus d'extraits de code prêts à l'entrevue? Abonnez-vous à notre newsletter et recevez les dernières informations de LeetCode directement dans votre boîte de réception.

---

C'est fait !

Vous avez maintenant une solution polie et conviviale d'entrevue et un billet de blog qui se classe bien pour les mots-clés les plus recherchés autour de LeetCode et la préparation d'entrevue. Partagez-le sur LinkedIn, GitHub ou votre blog personnel pour mettre en valeur votre maîtrise algorithmique et améliorer votre profil de recherche d'emploi. Bonne chance !