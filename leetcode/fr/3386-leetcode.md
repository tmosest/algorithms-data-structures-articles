---
titre: LeetCode 3386. Bouton avec le temps de poussée le plus long -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3386. Bouton avec le temps de poussée le plus long – Solution de LeetCode multilangue

Récapitulation des problèmes
Vous êtes donné un tableau trié chronologiquement `events` où chaque élément `[index, time]` vous dit que le bouton avec ID `index` a été appuyé à l'instant `time`.
Le temps *push* pour une pression de bouton est:

- **Première presse :** "temps" (pas de presse précédente à soustraire).
- **Presses ultérieures:** `time_current – time_previous`.

Votre tâche : retourner l'ID du bouton qui a exigé le temps de poussée **le plus long**.
Si plusieurs boutons s'attachent le plus longtemps, retournez celui avec le **le plus petit ID**.

---

Aperçu de l'algorithme

1. **Initialiser** le temps de poussée maximum avec l'heure du premier événement ('events[0][1]') et stocker le premier bouton ID comme la meilleure réponse actuelle.
2. **Itérer** dans le tableau à partir du deuxième événement.
3. Pour chaque événement, calculer la durée = événements[i - Oui. [1] - événements[i-1][1]».
4. **Mise à jour** si :
- La durée est ** strictement supérieure** au maximum actuel, **ou**
- `duration` correspond au maximum actuel **et** l'ID du bouton actuel est **plus petit** que la réponse stockée.
5. Après la boucle, la réponse stockée est l'ID du bouton souhaité.

L'algorithme fonctionne dans **O(n)** temps et utilise **O(1)** espace supplémentaire.

---

Mise en œuvre du code

C'est pas vrai. Java

"Java
solution de classe publique {
bouton int public AvecLongestTime(int[][] événements) {
// Cas de bord : au moins un événement est garanti par des contraintes
int maxTime = événements[0][1];
réponse int = événements[0][0];

pour (int i = 1; i < events.longueur; i++) {
durée int = événements[i ][1] - événements[i - 1][1];
si (durée > maxTime=" (durée == maxTime && events[i][0] < reponse) {
maxTime = durée;
réponse = événements[i][0];
}
}
réponse de retour;
}
}
«» "

# # # # # #

'`python
Solution de classe:
bouton de défi Avec le plus long Time(self, events: List[List[int]]) -> Int:
max_time = événements[0][1]
réponse = événements[0][0]

pour i dans la plage(1, len(events)):
durée = événements[i ][1] - événements[i - 1][1]
si la durée > max_time ou (durée) == max_time et événements[i][0] < réponse):
_temps max = durée
réponse = événements[i][0]

réponse de retour
«» "

C'est vrai. C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
bouton int AvecLongestTime(vecteur<vecteur<int>>& événements) {
int max_time = événements[0][1];
réponse int = événements[0][0];

pour (size_t i = 1; i < events.size(); ++i) {
durée int = événements[i ][1] - événements[i - 1][1];
si (durée > max_time) (durée == max_time && events[i][0] < reponse) {
max_time = durée;
réponse = événements[i][0];
}
}
réponse de retour;
}
};
«» "

---

La complexité temporelle et spatiale

La complexité temporelle La complexité spatiale Autres
Il s'agit d'un projet pilote.
* * * * * * *
Python **O(n)**
* * * * * * * * *

*`n` = nombre d'événements. *

---

Cas et pièges de bord

Scénario Que regarder
-- -- -- -- -- -- -- -- --
Autres **Un seul événement**=Le premier événement lui-même est le plus long; aucun calcul de différence n'est nécessaire. Autres
**Attache sur la durée**= Doit retourner l'ID du bouton *le plus petit*. Vérifiez les deux "durée > max" ** et** "durée == max && id < response". Autres
**Plus grande entrée**= Toutes les solutions fonctionnent dans le temps linéaire, en respectant confortablement la limite de 1 000 événements. Autres
**Négatif ou zéro fois**=Les contraintes garantissent `timei ≥ 1`, donc aucune durée négative. Autres

---

Les bons, les mauvais et les méchants

Les bons
- **Simplicité :** Une passe, des variables minimales, une logique claire.
- **Efficacité:** "O(n)" temps, "O(1)" espace – idéal pour les paramètres d'entrevue.
- **Language-agnostique:** Le même concept est propre à Java, Python, C++.

- Oui. Les mauvais
- **Misscompréhension du premier temps de presse Certaines solutions traitent incorrectement la durée du premier événement comme zéro.
- **Bogues hors pair:** Oublier de démarrer la boucle à l'index 1 ou utiliser le mauvais index précédent conduit à de mauvaises durées.

- Oui. L'Ugly
- **Suringénierie:** L'utilisation de cartes de hachage ou de structures de données complexes pour cette analyse linéaire est inutile et distrait les intervieweurs.
- **Ignorer la règle de l'égalité des chances:** Retourner le mauvais bouton ID lorsque plusieurs boutons partagent la durée la plus longue donne une mauvaise réponse qui est difficile à repérer sans une suite de test approfondie.

---

Comment expliquer Ceci dans une interview

1. **Retrait le problème** dans vos propres mots pour confirmer la compréhension.
2. **Extrait l'algorithme** (premier passage, maintien du maximum et réponse).
3. **Écrire un pseudocode** ou un croquis rapide sur le tableau blanc.
4. **Cas de bord de Mention** explicitement.
5. **Discuse la complexité** juste après le codage.

Si l'intervieweur demande : Pouvons-nous faire mieux ?

---

La pertinence réelle du monde

Ce modèle — suivi des valeurs maximales/minimales lors de la numérisation d'un flux — est commun dans:

- ** Traitement des données du capteur** (détectant les périodes d'inactivité les plus longues).
- **Logage des événements** (identification des événements les plus retardés).
- **Game analytics** (recherche d'une pression ou d'une interaction plus longues).

La maîtrise de cette approche démontre de solides compétences en manipulation de réseaux et un knack pour un suivi efficace de l'état, tous deux prisés dans les rôles d'ingénierie logicielle.

---

Liste de contrôle rapide pour votre préparation d'entrevue

• Comprendre le format d'entrée (par ordre chronologique).
- Prendre en charge le premier événement séparément.
- Mise à jour sur une durée strictement plus longue ou la liaison avec une identification plus petite.
- Fournir des cas d ' essai pour les conditions de bord.
- Expliquez la complexité du temps et de l'espace.

---

Résumé amical

Vous cherchez une solution *Button avec le temps de poussée le plus long*? Découvrez ce guide **Java, Python et C++** couvrant l'algorithme, les cas de bord et une explication complète prête à l'entrevue. Idéal pour toute personne se préparant à des entrevues de codage, à la pratique LeetCode ou à la construction de systèmes de traitement d'événements efficaces.

**Mots clés**: Bouton avec le temps de poussée le plus long, LeetCode 3386, solution Java, solution Python, solution C++, entretien de codage, algorithme, complexité du temps, complexité de l'espace, préparation de l'entrevue, conseils d'entrevue.

---