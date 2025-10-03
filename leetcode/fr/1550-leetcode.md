---
titre: LeetCode 1550. Trois chances consécutives -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Trois chances consécutives – LeetCode 1550
**Java • Python • C++***** **Approche de calcul (O(n), O(1))******Interview-Ready**

---

TL;DR

> *=Avec un tableau entier, retourner `true` s'il existe trois nombres impairs consécutifs; sinon retourner `false`.

La solution la plus simple et la plus efficace est un seul balayage linéaire qui maintient un compteur de nombres impairs consécutifs.
complexité du temps : **O(n)* *
complexité spatiale: **O(1)**

Ci-dessous vous trouverez un code propre, prêt à la production dans **Java, Python et C++**, suivi d'un court article de blog qui explique le problème, l'approche, et les avantages/cons de différentes méthodes.

---

Code

C'est pas vrai. Java

"Java
solution de classe publique {
public booléen troisConsécutiveOdds(int[] arr) {
Int consécutif Odds = 0; // compte combien de chances nous avons vu dans une rangée

pour (int num : arr) {
si ((num & 1)] 1) { // essai impair rapide (num % 2 == 1 est aussi très bien)
consécutive Indiques++;
si (conséquences) 3) {
retour true; // trouvé trois cotes consécutives
}
} autre {
consécutive Odds = 0; // réinitialiser le nombre pair
}
}
retourner faux; // jamais atteint une série de 3 cotes
}
}
«» "

---

# # # # # #

'`python
Solution de classe:
def threeConsecutiveOdds(self, arr: list[int]) -> C'est vrai.
nombre = 0 # compteur impair consécutif

pour num in arr:
si num & 1: # contrôle bit-wise pour impair
nombre += 1
si vous comptez == 3:
retour Vrai
Sinon:
nombre = 0
Retour Faux
«» "

---

C'est vrai. C++

'`cpp
#incluez <vecteur>

solution de classe {
public:
Bool threeConsecutiveOdds(std::vector<int>& arr) {
= 0; // compteur impair consécutif

pour (int num : arr) {
si (num & 1) { // essai impair rapide
+ nombre;
si (compter) 3) {
retour true; // stries de 3 cotes trouvées
}
} autre {
nombre = 0; // réinitialiser le nombre pair
}
}
retourner faux;
}
};
«» "

> **Pourquoi ce code? * *
> *Single pass* – une seule boucle sur le tableau.
> * Mémoire constante* – juste un compteur entier.
> *Détection impair rapide* – `num & 1` est légèrement plus rapide que `% 2` et est idiomatique dans de nombreux paramètres d'entrevue.

---

## Article du blog – Trois chances consécutives : le bon, le mauvais et le mauvais

> *Description détaillée:* Découvrez comment résoudre LeetCode 1550 – Trois dates consécutives – en Java, Python et C++. Explorez la force brute, le comptage et les approches monolignes, et préparez-vous à l'entrevue avec une solution O(n) concise.

---

- Oui. 1. Récapitulation des problèmes

- **Input:** `int[] arr` (Java), `list[int] arr` (Python), `vector<int> arr` (C++)
- **Durée:** 1 ≤ "longueur normale" ≤ 1000
- **Valeur :** 1 ≤ `arr[i]` ≤ 1000
- **Objectif:** Retourner `true` si trois **éléments consécutifs** sont tous étranges; sinon `faux`.

---

- Oui. 2. La stratégie de comptage – Le bien –

La stratégie de comptage est la solution d'entrevue canonique :

Texte
nombre = 0
pour chaque nombre en arr:
si num est impair: compter += 1
Autre: nombre = 0
3 : retour vrai
retourner faux
«» "

**Pourquoi c'est bon**

Critère Pourquoi il marque haut
- C'est pas vrai.
**Heure**= O(n) – un passage, linéaire à la taille du tableau==
**Space**
Très petite intention claire
**Robustness**
**Performance** Autres

---

- Oui. 3. La Force Brute Naïve

Texte
pour i de 0 à arr.longueur-3:
si arr[i], arr[i+1], arr[i+2] sont tous étranges:
retour vrai
retourner faux
«» "

**Quartiers* *

Sujet Impact
C'est quoi ?
Re-vérifie les fenêtres qui se chevauchent.
Autres Moins intuitif peuvent être mal typés dans les entrevues
Autres Plus de code Augmentation des chances de bugs

Il est toujours *acceptable* pour de petites entrées, mais inutile lorsque la méthode de comptage est disponible.

---

- Oui. 4. Le "Ugly" – One-Liner avec `search_n` (C++) / `any` (Python)

> *Exemple (C++): *
> `return std::search_n(arr.begin(), arr.end(), 3, 0, [](int a){ return a & 1; }) != arr.end(); "

**Pour**

- Très court
- Exprime l'intention dans un style fonctionnel

**Cons**

- Difficile à lire pour les non-experts
- S'appuie sur des utilitaires linguistiques spécifiques que beaucoup d'intervieweurs ne s'attendent pas
- Mauvaise performance en raison de frais généraux supplémentaires potentiels (comparaisons d'itérateurs, objets fonctionnels)

> *Quand utiliser:* Lorsque vous travaillez dans une base de code de production qui a déjà de tels utilitaires, ou lorsque vous voulez impressionner avec -C++ magic – mais soyez prêt à expliquer la mécanique sous-jacente dans une discussion.

---

- Oui. 5. Résumé de la complexité

L'approche Temps Espace
- C'est quoi ?
Dénombrement
(facteur constant) 3)) **O(1)**
Une seule ligne **O(n)**

La méthode de comptage domine en *chaque* métrique.

---

- Oui. 5. Conseils d'entrevue

1. **Énoncez le problème dans vos propres mots. **
Nous sommes à la recherche d'une série de trois chances — donc nous avons juste besoin de garder une trace du nombre de chances que nous avons vus de suite. (en milliers de dollars)

2. ** Expliquez l'idée contraire avant d'écrire le code. **
Cela montre que vous comprenez *pourquoi* vous effectuez un balayage linéaire et *comment* l'algorithme garantit la justesse.

3. **Mention bitwise étrange vérification. **
`num & 1` est une astuce classique dans le codage des interviews et montre que vous connaissez les astuces de faible performance.

4. **Demandez des contraintes. **
Vos contraintes (1 000) rendent le passage d'une force brute possible, mais la solution de comptage est encore meilleure. (en milliers de dollars)
Cela ouvre une discussion sur *les compromis d'optimisation*.

5. **Échange de temps.**
Montrez que vous pouvez choisir le bon algorithme pour la situation – *bonne contre mauvaise* approches.

---

- Oui. 6. À emporter – Comment faire face à cette question

Étape
- C'est quoi ?
Autres **1. Comprendre la cohérence**. Clarifier que les fenêtres peuvent se chevaucher; réinitialiser le compteur sur des nombres égaux. Autres
**2. Utilisez un seul compteur**. Autres
**3. Vérifier les cas de bord**. Longueur < 3 → `faux`; nombres alternés → `faux`; triples cotes à n'importe quelle position → `true`. Autres
**4. Expliquez la complexité** Autres
**5. Soyez prêt à expliquer les solutions de rechange. Autres

---

- Oui. 7. SEO et conseils professionnels

Mots-clés Pourquoi ça compte
C'est-à-dire
"Three Consecutive Odds LeetCode" (Three Consecutive Odds LeetCode) Terme de recherche utilisé par les recruteurs qui chassent pour l'expérience LeetCode. Autres
`Java Three Consecutive Odds`=Cible les développeurs Java. Autres
Code Python Leet 1550'-- Tire des interviews Python-centric. Autres
`C++ Comptage de l'algorithme`= Points saillants de l'efficacité algorithmique, un plus pour les positions de conception système. Autres
"La pratique de l'algorithme de l'interview" Autres

> **Recherche d'emploi Conseil :**
> Ajoutez ce problème à votre portfolio sur GitHub, liez-le dans votre Linked En gros titre, et écrire un billet de blog comme celui-ci. Les recruteurs filtrent souvent les candidats par la performance de LeetCode, de sorte qu'une solution claire et optimisée avec une explication d'accompagnement peut vous donner un avantage mesurable.

---

- Oui. 8. Pensées finales

- **Count** est la solution *de-facto* LeetCode 1550.
- Brute-force est rapide mais redondant.
- Un liner est mignon, mais la lisibilité compte le plus dans les entrevues.

Avec les trois extraits ci-dessus et l'explication prête à l'entrevue, vous avez obtenu un paquet poli qui est prêt à impressionner les gestionnaires d'embauche et passer le checker LeetCode.

Bon codage ! C'est ce qu'il a dit