---
titre: LeetCode 2054. Deux meilleurs événements sans débordement -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Comment faire pour éponger le LeetCode -Deux meilleurs événements non exhaustifs - Un guide de préparation à l'emploi

> **Vous voulez passer votre prochaine entrevue de codage? * *
> La maîtrise de ce problème de niveau moyen montre que vous pouvez trier, rechercher en binaire et optimiser en temps linéarithmique – toutes les compétences que les gestionnaires d'embauche aiment.

---

Récapitulation des problèmes (Code de bord 2054)

Vous avez une liste d'événements, chacun défini par **heure de départ, heure de fin,** et **valeur**:

Texte
events[i] = [start_i, end_i, value_i]
«» "

* ** Les événements sont inclus.**
Si l'on se termine à l'heure `t`, la suivante doit commencer à `t + 1` ou plus tard.
* Vous pouvez assister à **au plus deux** événements sans chevauchement.
* Retourner la valeur totale ** maximale** réalisable.

**Contrôles* *

Champ
C'est pas vrai.
Durée des événements
"start_i, fin_i" 1 ...
1 ... 106

---

- Oui. Pourquoi ce problème est-il à l'origine de votre portefeuille d'entrevues

Compétences Comment le problème le teste
C'est ce que j'ai dit.
Tri & Greedy Vous devez trier par heure de départ pour raisonner sur les événements futurs. Autres
Vous devez rapidement trouver le prochain événement compatible. Autres
Prefix/Suffix Arrays Vous stockez la meilleure valeur future pour les recherches rapides. Autres
Atteignez le temps O(n log n) et l ' espace O(n). Autres
Une bordure Pensée de cas ► Temps inclus, optimisation d'un événement, grandes tailles d'entrée. Autres

---

- Oui. Aperçu de la solution de haut niveau

1. **Trier** tous les événements par "démarrage".
2. Construire un tableau **suffix maximum**:
`maxVal[i] = max(valeur de tout événement de i à fin)`.
Cela nous donne la meilleure valeur future de l'événement dans *O(1)*.
3. Pour chaque événement «i»:
* Utilisez ** recherche binaire** pour localiser le premier événement `j` dont le début > `end_i`.
* Calculer les montants des candidats :
* `value_i` (événement unique)
* `value_i + maxVal[j]` (paire)
* Gardez le maximum mondial.

La paire de deux événements se compose toujours de l'événement actuel et de l'événement futur *meilleur* possible qui commence après sa fin.

---

Algorithme détaillé

Texte
Tri(événements par début)

suffixeMax[n-1] = événements[n-1]. valeur
pour i = n-2 jusqu ' à 0:
suffixeMax[i] = max(events[i].value, suffixeMax[i+1])

réponse = 0
pour i = 0 ... n-1:
# Recherche binaire pour le premier événement qui commence après les événements[i].
l = i+1, r = n-1, idx = -1
alors que l <= r:
milieu = (l+r)//2
si events[mid].start > events[i].end:
idx = milieu
r = milieu-1
Sinon:
l = milieu+1

# Seulement l'événement actuel
réponse = max(réponse, événements[i].value)

# Paire avec le meilleur événement futur
Si idx != - 1 :
réponse = max(réponse, événements[i].valeur + suffixeMax[idx])

réponse de retour
«» "

**Pourquoi ça marche* *

* Le tri garantit que tout événement futur commence à ou après le début de l'événement actuel.
* La recherche binaire garantit une recherche logarithmique de l'événement *suivant non-overlaping*.
* Le tableau suffixe stocke la valeur maximale de *any* event commençant à ou après l'index `j`, ce qui est exactement ce dont nous avons besoin pour l'appariement.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Trier "O(n log n)" "O(1)" (en place)
Bâtiment suffixe tableau Autres
Boucle + recherche binaire Autres
**Total**** Autres

Tant le temps que l'espace satisfont les contraintes de problème confortablement.

---

## 6--Cas de bord & Gotchas

Pourquoi ça compte ?
- Oui.
Autres Deux événements se chevauchent exactement (`start2 == fin1`) Les temps inclus signifient qu'ils ne peuvent pas tous les deux être choisis.
Autres Tous les événements se chevauchent.Le meilleur choix est un seul événement.Le code est déjà géré avec `max(réponse, valeur)` Autres
Autres Très grande entrée (événements `105`)

---

Mise en œuvre du code

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.
Tous compilent avec les dernières normes et fonctionnent dans le temps `O(n log n)`.

Autres Conseil : Lors de l'affichage sur LeetCode, coller la définition de classe uniquement – la plate-forme fournit le pilote.

---

Java

"Java
Importer java.util. Les tableaux;

solution de classe {
int maxTwoEvents(int[][] events) {
// Trier par heure de début
les tableaux.sort(événements, a, b) -> Integer.compare(a[0], b[0]);

int n = événements. longueur;
int[] suffixeMax = nouvelle int[n];
suffixeMax[n - 1] = événements[n - 1][2];

// Construire un tableau de suffixe maximum
pour (int i = n - 2; i >= 0; i--) {
suffixeMax[i] = Math.max(events[i][2], suffixeMax[i + 1]);
}

int best = 0;

// Pour chaque événement, recherche binaire prochain événement compatible
pour (int i = 0; i < n; i++) {
// Valeur de l'événement unique
best = Math.max(best, events[i][2]);

int l = i + 1, r = n - 1, idx = -1;
pendant que (l <= r) {
int milieu = l + (r - l) / 2;
si (événements [milieu][0] > événements[i][1]) {
idx = milieu;
r = milieu - 1;
} autre {
l = milieu + 1;
}
}

Si (idx != -1) {
best = Math.max(best, events[i][2] + suffixeMax[idx]);
}
}

le meilleur retour;
}
}
«» "

---

Python 3

'`python
Solution de classe:
def max TwoEvents(self, events: List[List[int]]) -> Int:
1. Tri par heure de début
events.sort(key=lambda e: e[0])

n = len(événements)
suffixe_max = [0] * n
suffixe_max[-1] = événements[-1][2]

2. Construire suffixe max
pour i dans la plage (n - 2, -1, -1):
suffixe_max[i] = max(events[i][2], suffixe_max[i + 1])

meilleur = 0

pour i dans la plage(n):
# Événement unique
best = max(meilleur, événements[i][2])

# Recherche binaire pour le premier événement avec début > end_i
l, r, idx = i + 1, n - 1, -1
alors que l <= r:
milieu = (l + r) // 2
si des événements[milieu][0] > événements[i - Oui.
idx = milieu
r = milieu - 1
Sinon:
l = milieu + 1

Si idx != - 1 :
best = max(meilleur, événements[i][2] + suffixe_max[idx])

le meilleur retour
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxTwoEvents(vector<vector<int>>& events) {
// Trier par heure de début
tri(events.begin(), events.end(),
[](const vector<int>& a, const vector<int>& b) {
retourner a[0] < b[0];
});

int n = events.size();
vecteur<int> suffixeMax(n);
suffixeMax[n - 1] = événements[n - 1][2];

Nombre maximal
pour (int i = n - 2; i >= 0; --i)
suffixeMax[i] = max(events[i][2], suffixeMax[i + 1]);

int best = 0;

pour (int i = 0; i < n; ++i) {
best = max(meilleur, événements[i][2]);

int l = i + 1, r = n - 1, idx = -1;
pendant que (l <= r) {
int milieu = l + (r - l) / 2;
si (événements [milieu][0] > événements[i][1]) {
idx = milieu;
r = milieu - 1;
} autre {
l = milieu + 1;
}
}

Si (idx != -1)
best = max(meilleur, événements[i][2] + suffixeMax[idx]);
}

le meilleur retour;
}
};
«» "

---

Cas d'essai rapide

Autres Test d'entrée prévu
- C'est quoi ?
[[[1,3],[2,5],[7,9]]» (événements 1 et 3)
[[[1,3],[4,5,5],[6,7]» "12" (événements 2 et 3)
[[1,3,10],[2,4,5],[5,65]]» "15" (événement 1 + événement) 3)
[[1,10,10],[2,3],[4,5,5],[6,7]]""18" (événement 1 + événement) 4)

---

C'est pas vrai. Comment présenter cette solution dans une entrevue

1. **Exposer la raison d'être du tri** – Nous trions pour faciliter les décisions futures. (en milliers de dollars)
2. **Afficher le suffixe idée max** – Nous voulons le meilleur événement possible après le présent. (en milliers de dollars)
3. **Démonstration de la recherche binaire** – Nous avons besoin de la recherche O(log n) pour éviter le piège quadratique. (en milliers de dollars)
4. **Énoncer la complexité** – temps O(n log n), espace O(n) – optimal pour 105 entrées. (en milliers de dollars)
5. **Manipulation d'un coin de mention** – temps inclusif, optimisation d'un seul événement. (en milliers de dollars)

N'hésitez pas à modifier le code à la volée : remplacez la recherche binaire par un balayage *deux points* pour un `O(n)` solution lorsque tous les événements sont triés par heure de fin d'abord.

---

## 10:00 Takeaways pour votre prochaine entrevue de codage

Ce que vous avez prouvé
-- -- -- -- -- -- -- --
**Données-Structure Choice** Autres
**Gestion de la complexité**= Solution équilibrée `O(n log n)`. Autres
**Décomposition du problème**= Analyse de l'événement unique par rapport à l'événement apparié. Autres
**Robustness**. Autres
**Codage Style** Autres

*Montrez au recruteur que vous pouvez écrire un code propre et prêt à la production dans toutes les langues – exactement ce qu'ils recherchent chez un ingénieur logiciel senior. *

---

Liste de contrôle finale avant votre prochaine entrevue

** Comprendre la contrainte de temps inclusive. **
- **Mettre en œuvre le suffixe max tableau** pour éviter les scans répétés.
**Binary-search** pour le premier événement dont le début > fin actuelle.
- **Retourner le maximum de sommes pour un événement et une paire. **
- Test avec des cas de bord (overlap, unique meilleur événement, énorme N).

---

Mots-clés prêts à l'emploi

- LeetCode 2054
- Deux meilleurs événements non exhaustifs
- Problème d'entretien de recherche binaire
- Question d'entretien en algorithme de tri
- Algorithme d'entretien d'emploi
- complexité temporelle O(n log n)
- Job interview prep LeetCode

---

La pensée finale

Résoudre deux des meilleurs événements non-overlaping est une simple victoire technique, c'est un **histoire** que vous pouvez dire aux recruteurs : *=J'ai trié, j'ai fait des recherches binaires, j'ai stocké des maximums suffixes, et j'ai obtenu le résultat optimal en temps log-linéaire.
Ajoutez ceci à votre portfolio, vantez votre CV, et vous serez prêt pour la prochaine entrevue. Bonne chance ! C'est ce qu'il a dit