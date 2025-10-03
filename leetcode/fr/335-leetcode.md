---
titre: LeetCode 335. Auto-croisement - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solution – One-pass, O(n) time et O(1) space

Le problème classique de l'auto-croisement peut être résolu en un seul balayage linéaire par
vérifier seulement les derniers mouvements.
Parce que la direction tourne toujours dans le sens contraire des aiguilles d'une montre (Nord → Ouest → Sud → Est → ...),
le chemin ne peut se croiser que dans quelques modèles spécifiques:

Situation Situation Conditions de franchissement
- C'est pas vrai.
**Standard** – le segment i‐th traverse le segment i‐2. Autres
**Special 4‐step** – le segment i‐th touche le segment i‐3 (lorsque i≥4). Dist[i‐1] == dist[i‐3] && dist[i] + dist[i‐4] >= dist[i‐2]» Autres
**Spécial 5-step** – le segment i‐th coupe une boucle ouverte dans les 5 étapes précédentes (lorsque i≥5). Dist[i-2] > dist[i‐4] && dist[i] + dist[i‐4] >= dist[i-2] && dist[i‐1] + dist[i‐5] >= dist[i‐3] && dist[i‐1] <= dist[i‐3]» Autres

Si l'une de ces trois conditions est vraie, le chemin s'est croisé.
Sinon, nous continuons à scanner jusqu'à la fin du tableau.

- Oui. Pourquoi ça marche ?

- Oui. Après chaque quatre déplace la direction se répète, donc le seul nouveau possible
intersection est avec un segment qui a été dessiné **2** ou **4** il y a quelques pas.
- Oui. Le troisième cas traite de la situation d'ensemble où le 5ème segment
chevauche une boucle créée par les segments précédents.
- Oui. Les conditions sont dérivées des longueurs relatives des
segments; ils sont à la fois nécessaires et suffisants pour qu'un passage se produise.

Complexité

Analyse métrique
C'est pas vrai.
**Temps**
**Espace** – seules quelques variables entières sont utilisées

---

- Oui. 2. Code

Ci-dessous sont propres, des implémentations à un passage dans **Java**, **Python** et **C++**.

### 2.1 Java

"Java
solution de classe publique {
***
* Retourne true si le chemin défini par distance[] se croise.
* @param distance un tableau d'entiers positifs
* @return true si se croiser, faux sinon
*/
public booléen isSelfCrossing(int[] distance) {
si (distance) = null.
retourner faux; // moins de 4 mouvements ne peuvent pas traverser
}

pour (int i = 3; i < distance longueur; i++) {
// Cas 1: La ligne actuelle franchit la ligne 2 marches en arrière
si (distance[i] >= distance [i - 2] &&
distance [i - 1] <= distance[i - 3]) {
retour vrai;
}

// Cas 2: La ligne actuelle touche la ligne 3 pas en arrière
si (i >= 4 &&
distance [i - 1] == distance [i - 3] &&
distance [i] + distance[i - 4] >= distance [i - 2]) {
retour vrai;
}

// Cas 3: La ligne actuelle traverse une boucle ouverte dans les 5 derniers mouvements
si (i >= 5 &&
distance [i - 2] > distance [i - 4] &&
distance [i] + distance[i - 4] >= distance [i - 2] &&
distance [i - 1] + distance[i - 5] >= distance [i - 3] &&
distance [i - 1] <= distance[i - 3]) {
retour vrai;
}
}

retourner faux;
}
}
«» "

2.2 Python

'`python
Solution de classe:
def isSelfCrossing(self, distance: list[int]) -> bool:
"""Retour Vrai si la marche se croise."""
si len(distance) < 4:
Retour Faux

pour i dans la plage(3, len(distance)):
# 1ère affaire
si (distance[i] >= distance [i - 2] et
distance [i - 1] <= distance[i - 3]):
retour Vrai

# 2ème affaire
si (i >= 4 et
distance [i - 1] == distance [i - 3] et
distance [i] + distance[i - 4] >= distance [i - 2]:
retour Vrai

# Troisième affaire
si (i >= 5 et
distance [i - 2] > distance [i - 4] et
distance [i] + distance[i - 4] >= distance [i - 2] et
distance [i - 1] + distance[i - 5] >= distance [i - 3] et
distance [i - 1] <= distance[i - 3]):
retour Vrai

Retour Faux
«» "

C++

'`cpp
solution de classe {
public:
bool isSelfCrossing(vecteur<int>&distance) {
si (distance.size() < 4) retourner faux;

pour (int i = 3; i < distance.size(); ++i) {
// Cas 1
si (distance[i] >= distance [i - 2] &&
distance [i - 1] <= distance[i - 3]) {
retour vrai;
}

// Affaire 2
si (i >= 4 &&
distance [i - 1] == distance [i - 3] &&
distance [i] + distance[i - 4] >= distance [i - 2]) {
retour vrai;
}

// Affaire 3
si (i >= 5 &&
distance [i - 2] > distance [i - 4] &&
distance [i] + distance[i - 4] >= distance [i - 2] &&
distance [i - 1] + distance[i - 5] >= distance [i - 3] &&
distance [i - 1] <= distance[i - 3]) {
retour vrai;
}
}
retourner faux;
}
};
«» "

Les trois extraits fonctionnent dans le temps `O(n)` et n'utilisent qu'un espace supplémentaire constant.

---

- Oui. 3. Article de blog

> **Titre**
> Auto-croissant dans LeetCode 335: Le bon, le mauvais, et le mauvais

> **Méta—Description* *
> Apprenez à résoudre le LeetCode 335 – Autocroisement – en Java, Python et C++ avec un algorithme O(n) à un seul passage. Comprendre la logique de couplage, les pièges et les cas de bord. Perfect your interview prep for algorithme questions.

---

3.1 Introduction

Lorsqu'il s'agit d'entretiens par algorithme, les problèmes de LeetCode qui impliquent la géométrie ou la simulation de chemin semblent souvent intimidants. L'auto-croisement (problème 335) est un tel défi : vous marchez dans une spirale contre-horaire et devez déterminer si votre chemin se croise.

À première vue, vous pourriez penser que vous devez garder un ensemble complet de coordonnées ou utiliser une routine d'intersection de segment de ligne — un cauchemar O(n2). Mais le vrai secret réside dans le modèle **directionnel** de la marche. Une fois que vous le voyez, la solution s'effondre à une poignée de simples contrôles d'inégalité.

Ce post va passer par cette perspicacité, présenter une solution simple concise, discuter des pièges communs, et vous donner un code prêt à la copie en Java, Python et C++. À la fin, vous pourrez expliquer le problème, l'algorithme et la logique de la casse à n'importe quel panel d'entrevues.

---

3.2 Récapitulation du problème

Vous commencez à l'origine `(0,0)` sur un avion 2-D.
Vous recevez un tableau `distance[]` d'entiers positifs.
Vous bougez :

1. "distance[0]" mètres **Nord**
2. "distance[1]" mètres **Ouest**
3. "distance[2]" mètres **Sud**
4. "distance[3]" mètres **Est**
5. ... et répéter dans le sens contraire des aiguilles d'une montre.

Retourner `true` si le chemin se croise; sinon `faux`.

> **Constraints**
> 1 ≤ distance longueur ≤ 10^5`
> 1 ≤ distance [i] ≤ 10'5'

Le défi est de le faire en **temps linéaire** et **espace constant**.

---

3.3 Le bon – Pourquoi un laissez-passer unique fonctionne

Parce que la direction change de façon prévisible (Nord → Ouest → Sud → Est → Nord ...), chaque nouveau segment ne peut croiser les segments précédents que de manière ** très limitée**.

Après les quatre premiers mouvements la direction se répète, de sorte que tout nouveau segment ne peut que toucher:

- Le segment a tiré deux mouvements (un virage à 90°).
- Oui. Le segment a tiré trois mouvements il y a (un virage de 180°, c'est-à-dire une touche).
- Oui. Le segment a tiré cinq mouvements il y a (une situation over-over-), qui ferme une boucle.

Ce sont les seules possibilités qui peuvent produire une traversée. Le reste de l'avion est déjà nettoyé par le modèle précédent.

Par conséquent, nous n'avons qu'à suivre les dernières distances — pas besoin d'une liste de coordonnées ou d'une routine d'intersection des segments de ligne.

---

3.4 Les mauvaises – erreurs courantes

Une erreur Pourquoi ça fait défaut
- C'est quoi ?
Autres **L'utilisation d'une liste complète des coordonnées**= O(n2) time et O(n) memory, ainsi que des erreurs de point flottant. Autres
**Vérifier seulement deux pas en arrière** Autres Ajouter l'état 4-étapes. Autres
**Utiliser des comparaisons de positions absolues** Utiliser les inégalités relatives entre les distances. Autres
**En supposant une symétrie**Le chemin peut avoir des longueurs asymétriques; le croisement peut se produire dans des motifs irréguliers. Utiliser les conditions exactes dérivées de la géométrie. Autres

---

#### 3.5 Les horribles cas de bord qui vous emportent

Erreur typique de l'algorithme
- C'est quoi ?
**Exactement 4 mouvements** 4 ' correctement. La deuxième condition ('i >= 4) vérifie le scénario tactile. Autres
L'ajout de deux valeurs `int` peut déborder `int` dans Java/C++. Autres
**Longues égales créant des boucles dégénérées** peut sembler non croisant, mais la règle en 5 étapes le capture. La troisième condition explique la boucle "over-over". Autres
Autres **Trois fois plus long** Une boucle itérative avec un stockage auxiliaire constant. Autres

---

3.6 L'algorithme en détail

Texte
pour i de 3 à n-1
si distance[i] >= distance[i-2] // plus longue ou égale au segment 2 marche arrière
et distance[i-1] <= distance[i-3] // le segment médian n'est pas plus long
retour vrai

i >= 4 et
distance[i-1]== distance[i-3] // touchant le segment 3-step-back
et distance[i] + distance[i-4] >= distance [i-2]
retour vrai

i >= 5 et
distance[i-2] > distance[i-4] // ouvrant une boucle
et distance[i] + distance[i-4] >= distance [i-2]
et distance[i-1] + distance[i-5] >= distance[i-3]
et distance[i-1] <= distance[i-3]
retour vrai

retourner faux
«» "

Les trois blocs correspondent exactement aux trois scénarios de croisement expliqués plus haut.

---

3.7 Analyse de la complexité

Métrique
- C'est quoi ?
**Heure**="O(n)" – un scan="O(n)" – un scan="O(n)" – un scan="
**L'espace**=«O(1)» – 5–6 variables entières=«O(1)»=«O(1)» Autres

L'algorithme fonctionne pour `n = 10^5` confortablement sur toutes les grandes plateformes.

---

#### 3.8 Extraits de code

C'est vrai. Java

"Java
solution de classe publique {
public booléen isSelfCrossing(int[] distance) {
si (distance) null (longueur < 4) retourner faux;
pour (int i = 3; i < distance longueur; i++) {
si (distance[i] >= distance[i-2] &&
distance[i-1] <= distance[i-3]) retour vrai;
si (i >= 4 &&
distance[i-1]== distance[i-3] &&
distance[i] + distance[i-4] >= distance[i-2]) retourner vrai;
si (i >= 5 &&
distance[i-2] > distance[i-4] &&
distance[i] + distance[i-4] >= distance[i-2] &&
distance[i-1] + distance[i-5] >= distance[i-3] &&
distance[i-1] <= distance[i-3]) retour vrai;
}
retourner faux;
}
}
«» "

Python

'`python
Solution de classe:
def isSelfCrossing(self, distance: list[int]) -> bool:
si len(distance) < 4:
Retour Faux
pour i dans la plage(3, len(distance)):
si distance[i] >= distance[i-2] et distance[i-1] <= distance[i-3]:
retour Vrai
i >= 4 et distance[i-1] == distance[i-3] et \
distance [i] + distance[i-4] >= distance [i-2]:
retour Vrai
i >= 5 et distance[i-2] > distance[i-4] et \
distance[i] + distance[i-4] >= distance[i-2] et \
distance[i-1] + distance[i-5] >= distance[i-3] et \
distance[i-1] <= distance[i-3]:
retour Vrai
Retour Faux
«» "

C++

'`cpp
solution de classe {
public:
bool isSelfCrossing(vecteur<int>&distance) {
si (distance.size() < 4) retourner faux;
pour (int i = 3; i < distance.size(); ++i) {
si (distance[i] >= distance[i-2] &&
distance[i-1] <= distance[i-3]) retour vrai;
si (i >= 4 &&
distance[i-1]== distance[i-3] &&
distance[i] + distance[i-4] >= distance[i-2]) retourner vrai;
si (i >= 5 &&
distance[i-2] > distance[i-4] &&
distance[i] + distance[i-4] >= distance[i-2] &&
distance[i-1] + distance[i-5] >= distance[i-3] &&
distance[i-1] <= distance[i-3]) retour vrai;
}
retourner faux;
}
};
«» "

N'hésitez pas à copier, coller et courir. N'oubliez pas de tester les cas délicats :

Texte
[1,2,3,4] -> faux
[1,1,1,1] -> vrai (cas de contact)
[1,1,2,1,1] -> true (5-étapes)
«» "

---

3.9 Comment discuter Ceci dans une interview

1. **Exposer le mouvement**: Nous marchons Nord → Ouest → Sud → Est → ..., donc après les 4 premiers pas la direction se répète. (en milliers de dollars)

2. **Énoncer les possibilités d'intersection limitées**:
- Deux pas en arrière (tour 90°).
- Trois marches en arrière (180°).
- Cinq pas en arrière (fermeture de boucle).

3. ** Présenter les inégalités**:
Montrez les trois conditions.
Utilisez un diagramme simple si vous êtes sur papier.

4. **Mentionner la complexité temps/espace**:
Temps "O(n)", espace "O(1)".

5. **Parler de la sécurité des caisses de bord**:
Manipulation des écoulements, contrôle de la longueur du tableau, grandes entrées.

Cette explication concise et rigoureuse démontre la profondeur de la compréhension, caractéristique d'un ingénieur logiciel de premier plan.

---

- Oui. 4. Conclusion

LeetCode 335 L'auto-croisement est trompeurment simple une fois que vous remarquez le modèle *directionnel*. La clé est de traiter le problème comme une **séquence d'inégalités relatives** au lieu de géométrie absolue. Dans cette perspective, un algorithme "O(n)" à passage unique émerge naturellement.

Nous avons couvert :

- Le **pourquoi** derrière le tour d'un passage.
- Les pièges communs.
- Le **how** de la manipulation des caisses.
- Code prêt à utiliser dans **Java, Python, C++**.

Maintenant, vous pouvez aborder cette question avec confiance, expliquer votre solution dans n'importe quelle langue, et impressionner les intervieweurs avec élégance et efficacité. Bon codage – et bonne chance pour votre prochaine entrevue!