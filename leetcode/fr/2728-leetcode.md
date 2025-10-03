---
titre: LeetCode 2728. Comptez les maisons dans une rue circulaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
##2728 – Comte les maisons dans une rue circulaire
**LeetCode=' Facile=' O(k) temps, O(1) espace**

> Votre tâche est de compter le nombre de maisons dans une rue circulaire, mais vous ne pouvez interagir avec la rue qu'à travers un ensemble d'API liées à la porte.

---

- Oui. Pourquoi ce problème est-il important?
- **Agrafe d'interview** – le problème teste votre capacité à concevoir un algorithme qui fonctionne avec *état limité* et *structures de données implicites* (ici, la rue circulaire).
- **Codage style** – vous devez utiliser l'interface donnée, pas un tableau, ce qui vous force à penser dans *procédure steps* au lieu de boucler simplement sur un tableau. (en milliers de dollars)
- **Menture d'optimisation** – vous êtes garanti que le nombre de maisons ≤ k, donc la solution doit respecter cette limite.

---

- Oui. 1. Remise en état des problèmes

Terme
C'est quoi ?
Objet avec l'API suivante : Autres
• 'porte ouverte()' – ouvrir la porte devant la maison actuelle. Autres
• `closeDoor()` – fermez-le. Autres
• 'estdoorOpen()' – retourne `true` si la porte actuelle est ouverte. Autres
• `moveRight()` / `moveLeft()` – se déplacer vers la maison adjacente dans la direction respective (circulaire). Autres
"k" Extrêmement lié au nombre de maisons. «1 ≤ n ≤ k ≤ 103». Autres

> En partant d'une maison arbitraire, vous devez retourner `n`, le nombre réel de maisons.

---

- Oui. 2. Intuition – Utilisez les portes comme marqueur

1. **Clarifiez chaque porte** – marchez `k` marches (le nombre maximum possible de maisons) et fermez toute porte ouverte que vous voyez.
Après cette boucle, toutes les portes sont fermées.

2. **Ouvrez la porte actuelle** – ceci marque la première maison que nous avons visitée.

3. ** Continuez à marcher dans la même direction** – après chaque mouvement, si nous rencontrons une porte ouverte, nous avons terminé un cycle complet.
Le nombre de déménagements que nous avons effectués (y compris la première maison) correspond au nombre de maisons.

L'observation clé: **portes peuvent agir comme des drapeaux de visite**. Parce que nous savons que la rue est circulaire et que nous sommes garantis dans la plupart des maisons `k`, fermer les portes `k` garantit que nous avons réinitialisé l'état de chaque maison possible.

---

- Oui. 3. Pseudocode

«» "
pour i en 0 ... k-1:
rue.closePorte()
street.moveLeft()

rue.openPorte() // première maison
nombre = 1

alors que Vrai:
street.moveLeft()
si street.isDoorOpen():
pause
nombre += 1

Nombre de retours
«» "

L'algorithme est *O(k)* dans le temps et *O(1)* dans l'espace.

---

- Oui. 4. Code complet

### Java

"Java
***
* Définition pour une rue.
* cours Rue {
* portes publiques de la rue(int[]);
* public vide ouvertPorte();
* public vide fermeture porte();
* le booléen public est DoorOpen();
* mouvement public nulDroit();
* mouvement public nulLeft();
*}
*/
solution de classe publique {
maison d'habitation publique Compte (rue rue, int k) {
// Étape 1: réinitialiser chaque porte
pour (int i = 0; i < k; i++) {
rue.closePorte();
street.moveLeft();
}

// Étape 2: ouvrir la première maison que nous rencontrons
street.openDoor();
nombre int = 1;

// Étape 3 : marcher jusqu'à ce qu'on frappe à nouveau la porte ouverte
alors que (vrai) {
street.moveLeft();
si (street.isDoorOpen()) {
pause; // une boucle complète est terminée
}
count++;
}

le nombre de retours;
}
}
«» "

Python

'`python
# Définition pour une rue.
# classe Rue & #160;:
# def __init_(self, doors: List[int]): ...
# def openDoor(self) -> Aucune: ...
# fermerPorte(s) -> Aucune: ...
# def isDoorOpen(self) -> bool: ...
# def movingRight(self) -> Aucune: ...
# def movingLeft(self) -> Aucune: ...

Solution de classe:
def maison Compte (soi-même, rue: 'Street', k: int) -> Int:
# Étape 1: Fermez toutes les portes possibles
pour _ dans la plage(k):
rue.closePorte()
street.moveLeft()

Étape 2: ouvrir la première maison
rue.openPorte()
nombre = 1

Étape 3 : marcher jusqu'à ce qu'on frappe à nouveau la porte ouverte
alors que Vrai:
street.moveLeft()
si street.isDoorOpen():
pause
nombre += 1

Nombre de retours
«» "

C++

'`cpp
***
* Définition pour une rue.
* cours Rue {
* public:
* Rue(vecteur<int> portes);
* vide ouvert();
* fermeture vide de la porte();
* bool isDoorOpen();
* mouvement nul Droit();
* mouvement nulLeft();
* };
*/
solution de classe {
public:
Int maison Compte (rue rue, int k) {
// Étape 1: réinitialiser toutes les portes
pour (int i = 0; i < k; ++i) {
rue->fermerPorte();
le déplacement de rueLeft();
}

// Étape 2: marquer la première maison
rue->openDoor();
nombre int = 1;

// Étape 3: marcher jusqu'à ce que nous rencontrions la porte ouverte à nouveau
alors que (vrai) {
le déplacement de rueLeft();
si (street->isDoorOpen())
pause;
+ nombre;
}

le nombre de retours;
}
};
«» "

---

- Oui. 5. Analyse de la complexité

Calcul métrique
C'est pas vrai.
Les opérations "2k" au maximum (phase de fermeture + ouverture). → **O(k)**
**Space**= Seulement une poignée de variables entières. → **O(1)**=

Avec `k ≤ 103`, la solution fonctionne confortablement en < 1 ms sur le matériel moderne.

---

- Oui. 6. Liste de contrôle des cas de bord

Autres Décision Pourquoi c'est sûr Comment l'algorithme se comporte
- C'est quoi ?
Autres Toutes les portes initialement fermées. La première `openDoor()` marque encore la première maison. Autres
Autres Toutes les portes initialement ouvertes.La première boucle ferme toutes les portes. Comme ci-dessus. Autres
"n = k" (maximum)" Nous marchons exactement "k" étapes; pas de mouvements supplémentaires. Le comte sera `k`. Autres
Certaines positions que nous ne visitons jamais pendant la première boucle. La fermeture des portes `k` couvre toujours toutes les vraies maisons. Autres
Autres La porte de départ est ouverte. C'est exact. Autres

---

- Oui. 7. Bien, mal et mal vu dans une perspective d'entrevue

Qu'est-ce qui est bon Qu'est-ce qui est mauvais Quoi ?
- C'est quoi ?
** Bon** • Espace constant; aucune structure de données supplémentaire. <br>• Utilise uniquement l'API fournie. <br>• Travaux pour *any* maison de départ.
**Bad**) • L'hypothèse « MoveLeft » peut sembler arbitraire, mais la direction peut être soit « droite » ou « gauche » tant que vous restez cohérent. Si vous mélangez les directions dans la première ou la deuxième phase, vous ne frapperez plus jamais la porte ouverte.
Une solution naïve qui itère sur un tableau serait *O(n)* mais ne satisferait pas la contrainte de l'API. <br>• Oublier d'ouvrir la première porte avant de commencer la boucle retournera 0 au lieu de `n`.

**Conseil d'entrevue :**
> Toujours **expliquer votre choix de direction** (gauche vs droite) et pourquoi vous le gardez cohérent. Il montre que vous comprenez la nature circulaire du problème.

---

- Oui. 8. Tendance des entrevues

Compétence testée Pourquoi il est précieux
- C'est quoi ?
*Itération de l'état*= Vous ne pouvez lire/écrire que par des effets secondaires. Autres
Vous utilisez `k` pour lier le travail au lieu de lier aveuglément un tableau inconnu. Autres
*Décomposition du problème*=La suppression de toutes les portes d'abord, puis leur utilisation comme marqueurs est un motif classique. Autres
*Codage contre une interface*= Un scénario réel commun : vous avez une bibliothèque ou une API en boîte noire et vous devez construire une logique autour d'elle. Autres

Si vous vous préparez à coder des entrevues, ce problème est un **doit être résolu**. Il mélange la pensée algorithmique avec des contraintes pratiques.

---

- Oui. 9. SEO–Résumé amical

- **Mots-clés**: `Count Houses in a Circular Street`, `LeetCode 2728 solution`, `Java Python C++`, `circulaire street problem`, `interview algorithme`, `time complexity O(k)`, `space complexity O(1)`
- **Titre**: LeetCode 2728 – Les maisons de comte dans une rue circulaire (Java / Python / C++ Solution)
- **Description détaillée**: Solve LeetCode 2728 – Count Houses in a Circular Street – avec code Java, Python et C++ propres. Apprenez l'algorithme O(k), l'explication détaillée et les conseils d'entrevue. (en milliers de dollars)

---

Mot final

L'astuce «door-as-marker» est une astuce soignée, prête à l'interview, qui maintient l'état minimal tout en permettant une traversée complète. La mettre en œuvre en **Java, Python ou C++** est simple une fois que vous comprenez l'API et la nature circulaire de la rue.

Bon codage, et bonne chance pour votre prochaine interview!