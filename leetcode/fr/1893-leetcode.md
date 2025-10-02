---
titre: LeetCode 1893. Vérifiez si tous les entiers d'une gamme sont couverts -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1893 – Vérifier si tous les entiers dans une gamme sont couverts

Langue Heure Espace
- C'est quoi ?
*Java * O(n + m)
*Python * O(n + m)
O(n + m)

> *n = nombre d'intervalles, m = taille de l'univers entier

> **Pourquoi cela importe** – Ce problème de « cover-check » est un *classic* pour les entretiens de codage, en particulier pour les rôles qui se concentrent sur la manipulation de l'array, les montants préfixés et les tableaux de différences**. La maîtrise démontre une solution de domaine O(1) propre qui s'échelle à de grandes entrées.

---

Résumé du problème

Vous avez reçu :

- "plages": liste des intervalles entiers inclus "[start1,end1], ...]".
- Deux limites "gauche" et "droite".

**Objectif:** Retour `true` si chaque entier `x` avec `gauche ≤ x ≤ droite` se trouve dans au moins un des intervalles prévus. Sinon, retourner `faux`.

---

Solution Brute-Force (Naïve)

Vérifiez chaque entier dans `[gauche, droite]` par rapport à tous les intervalles.

'`python
def is_covered_bruteforce(ranges, gauche, droite) :
pour x dans la plage (gauche, droite+1):
si ce n'est pas le cas(démarrer <= x <= fin pour le début, terminer dans les plages):
Retour Faux
retour Vrai
«» "

- **Time:** `O(right-left+1) * n)` – pire cas 2500×50 = 125k opérations (acceptable pour LeetCode mais pas élégant).
- **Espace:** "O(1)".

---

Solution optimale – Tableau des différences (plongée en ligne)

Parce que l'univers est délimité (`1..50`), nous pouvons maintenir un tableau *différence* qui enregistre quand une couverture commence et s'arrête.

3.1 Intuition

1. Pour chaque intervalle `[l, r]`, incrément `diff[l]` par `1`.
2. Décret `diff[r+1]` par `1` (puisque `r` est inclusif).
3. Le préfixe `diff` indique le nombre d'intervalles actifs à chaque entier.
4. Lors de la numérisation, si nous touchons un nombre dans `[gauche, droite]` avec 0 intervalles actifs, la réponse est `faux`.

Code ### 3.2

Python

'`python
def is_covered(ranges: list[list[int]], gauche: int, droite: int) -> C'est vrai.
"""
Temps O(n + m), espace O(m)
m == 51 parce que 1 <= début, fin <= 50
"""
diff = [0] * 52 # indices 1..50; 51 utilisé pour r+1 quand r==50

pour l, r dans les fourchettes:
diff[l] += 1
[r + 1] -= 1

actif = 0
pour i à portée(1, 51):
actif += diff[i]
si gauche <= i <= droite et active == 0:
Retour Faux
retour Vrai
«» "

C'est vrai. Java

"Java
solution de classe publique {
public booléen isCovered[[]] gammes, int gauche, int droite) {
int[] diff = nouvelle int[52]; // indices 1..50, 51 pour r+1
pour (int[] r : gammes) {
diff[r[0]]++; // début de la couverture
diff[r[1] + 1]--; // fin de la couverture
}

Int actif = 0;
pour (int i = 1; i <= 50; i++) {
actif += diff[i];
i (i >= gauche && i <= droite && active) 0) {
retourner faux;
}
}
retour vrai;
}
}
«» "

C++

'`cpp
solution de classe {
public:
bool isCovered(vector<vector<int>>& ranges, int gauche, int droite) {
int diff[52] = {}; // 1..50, 51 pour r+1

pour (auto &r : gammes) {
diff[r[0]]++; // démarrage
diff[r[1] + 1]--; // fin+1
}

Int actif = 0;
pour (int i = 1; i <= 50; ++i) {
actif += diff[i];
i (i >= gauche && i <= droite && active) 0) {
retourner faux;
}
}
retour vrai;
}
};
«» "

3.3 Complexité

- **Temps:** `O(n + 50)` -"O(n)` (linéaire dans le nombre de plages).
- **Space:** `O(52)` - "O(1)" - mémoire supplémentaire constante.

---

## 4-

Aspect du bien
- C'est quoi ?
**Le concept **Utilise un tableau de différence* – un trick classique linéaire-temps.
**Mise en oeuvre** Extrêmement concis; seulement deux boucles ); l'index `r+1` peut sembler étrange; les bogues hors-par-un sont courants.
**Performance**. O(1) espace, O(n) temps – optimal.
**Readability**= Facile pour les ingénieurs chevronnés==Peut être intimidant pour les débutants==Si l'intervieweur s'attend à une solution d'intervalles ===, ce diff‐array pourrait être vu comme surkill===

> **Takeaway** – Master the *difference array* trick; il s'agit d'un modèle go-to pour les problèmes de mise à jour/compte de gamme. Dans les entrevues, vous pouvez commencer par une explication claire de l'idée, puis implémenter la version du tableau de taille constante. Si l'intervieweur pousse vers une solution générique (univers non consolidé), vous pouvez passer à une ligne de balayage basée sur un événement.

---

C'est pas vrai. Essais

'`python
Exemple 1
est_couvert([[[1,2],[3,4],[5,6], 2, 5)== Vrai

Exemple 2
est_couvert([[1,10],[10,20]], 21, 21) == Faux

# Bord : intervalles de chevauchement
est_couvert([[1,3],[2,5],[4,6], 1, 6)== Vrai

# Edge: numéro unique non couvert
est_couvert([[1,5]], 6, 6) == Faux

♪ Couverture complète
est_couvert([[[1,50]]], 1, 50) == Vrai
«» "

---

Article sur le blog optimisé du SEO

> - Oui. Comment cracker LeetCode 1893 en 5 minutes – Un guide Java/Python/C++ pour les entrevues d'emploi

---

Mots clés

- LeetCode 1893
- Vérifiez si tous les entiers dans une gamme sont couverts
- entretien de codage
- tableau de différence
- la somme du préfixe
- balayage de ligne
- question d'entretien par algorithme
- Solution Java LeetCode
- Code Python Leet
- Entretien de codage C++

---

Article

---

- Oui. 1. Présentation

Dans les entrevues d'ingénierie logicielle, vous verrez souvent des questions qui vous demandent si *chaque entier d'une gamme est couvert par un ensemble d'intervalles*. LeetCode 1893 est l'exemple canonique. Bien que les contraintes semblent minuscules (`1 ≤ début ≤ fin ≤ 50`), le problème est un **portée** vers les concepts d'algorithme de base: préfixer les sommes, les tableaux de différence, et line-sweep. Maîtriser cela non seulement renforce votre cote LeetCode, mais aussi indique aux recruteurs que vous comprenez la manipulation efficace du tableau.

---

- Oui. 2. Récapitulation des problèmes

Vous recevez une gamme d'intervalles inclusifs et deux limites `gauche` et `droit`. Retour `true` if chaque entier `x` avec `gauche ≤ x ≤ droite` se trouve dans au moins un intervalle. Il s'agit d'un test *couverture*: `[[1,2],[3,4],[5,6]` couvre `[2,5]` → `true`; `[[1,10],[10,20]` ne **pas** couvrir `21` → `faux`.

---

- Oui. 3. Pourquoi une approche naïve est mauvaise

Une double boucle qui teste chaque entier par rapport à chaque intervalle est simple, mais elle est **O(right‐left+1) × n)**. Sur LeetCode vous pouvez encore passer (opérations 125 k), mais dans une interview vous passerez de précieuses secondes sur une solution * légèrement non-optimale*. Les recruteurs veulent voir que vous penserez **line‐sweep** avant de "brute‐forcing" .

---

3.1 Stratégie optimale : répartition des différences

Mesure prise Justification
C'est quoi ?
**Incrément** `diff[l]` par `1` pour chaque intervalle `[l,r]`. Autres
Autres **Décret** `diff[r+1]` par `1`. Autres
Autres Calculer une somme préfixe sur `diff`. Autres
Autres Lors de la numérisation, si un entier dans `[gauche, droite]` a 0 intervalles actifs → `false`. Autres

> **Pourquoi O(n + m) vs O(à droite +1)*n)** – Nous *pré-aggregate* tous commence/se termine en une seule passe, puis une seule passe linéaire sur le tableau 51-slot (constante). Aucun contrôle répété par rapport à chaque intervalle.

---

- Oui. 4. Faits saillants de la mise en œuvre

C'est vrai. Java

"Java
public booléen isCovered[[]] gammes, int gauche, int droite) { ... }
«» "

> • `int[] diff = nouvelle int[52];» – mémoire constante.
> • Deux boucles: une pour remplir `diff`, une autre pour scanner et sortir tôt.

Python

'`python
def is_covered(ranges, gauche, droite): ...
«» "

> • `diff = [0] * 52` – La liste Python est efficace pour la mémoire des petits domaines.
> • Utilisez `any(start <= x <= fin pour commencer, fin dans les plages)` dans la version naïve pour voir la différence.

C++

'`cpp
bool isCovered(vector<vector<int>>& ranges, int gauche, int droite) { ... }
«» "

> • Tableau statique `int diff[52]` – l'initialisation zéro en C++ est banale.
> • Temps de compilation le plus rapide en raison de l'attribution de la pile.

---

- Oui. 5. Ce que les intervieweurs recherchent vraiment

Autres Conseil Pourquoi
- Oui.
Explication du tableau *différence* en anglais clair avant codage. Ça montre que vous comprenez le truc "préfixe-sum" et que vous pouvez l'articuler. Autres
Mentionnez que `r+1` est sûr parce que l'univers est limité. Évite les surprises. Autres
Proposer une solution alternative pour les intervalles de tri, si demandé. Flexibilité: vous pouvez pivoter vers une ligne de balayage sur les événements pour les grands univers. Autres

> ** Conseil professionnel :** Si la première solution de l'interviewé est *naïve*, pivotez rapidement vers le tableau de différence. Les recruteurs aiment un candidat qui peut ** reconnaître une opportunité d'optimisation**.

---

- Oui. 6. Feuille de chaleur de complexité

Langue Heure Espace
- C'est quoi ?
**O(n + m)** → **O(n)**
Python **O(n + m)**
* * * * * *

> *n = nombre d'intervalles (= 50), m = taille de l'univers (= 51). *

---

- Oui. 7. Pensées finales

- **LeetCode 1893** n'est pas seulement un contrôle de portée – c'est un *signal* que vous saisissez les astuces de la structure des données de base.
- Oui. Le motif différence-array est **portable**: utilisez-le pour l'ajout de gamme, les requêtes de somme de gamme, et beaucoup d'autres agrafes d'entrevue.
- Oui. Dans un entretien de codage, présentez d'abord l'idée, puis livrez l'implémentation du tableau de taille constante. Si le recruteur s'interroge sur l'évolutivité, expliquez comment le même concept peut être étendu à un *sweep‐line* sur des points d'événement.

---

- Oui. 8. Prêt à faire votre prochain entretien d'embauche?

- Ecrire la solution dans **Java** (dactylographie statique + style OOP).
- Oui. Testez-le en **Python** (concise, lisible).
- Valider avec **C++** (orienté performance).

Ajoutez ces solutions à votre portfolio, poussez-les vers GitHub, et lorsque les recruteurs recherchent le code Leet 1893 Java, votre code apparaîtra en haut. Bonne chance avec votre interview prep! C'est ce qu'il a dit.

---

TL; RD

- **Utilisez un tableau de différence** – 2 boucles, mémoire constante, temps linéaire.
- **Exposer clairement la logique**; les recruteurs aiment une réponse bien structurée.
- **Inclure les tests de cas de bord** – il vous montre que vous avez pensé à travers les scénarios de "bad" et "ugly".

---

Télécharger tout le code

"""
♪ Java
Curl -o Solution.java https://pastebin.com/raw/xxxxxxx

# Python
solution de boucle -o. py https://pastebin.com/raw/xxxxxxx

Numéro C++
-o solution.cpp https://pastebin.com/raw/xxxxxxx
«» "

(Remplacez `xxxxxx` avec le vrai hash de Pastebin ou votre propre copie hébergée.)

---

( ) *Maintenant vous êtes prêt à répondre LeetCode 1893 comme un pro, impressionner les recruteurs, et atterrir ce travail d'ingénierie logicielle. *