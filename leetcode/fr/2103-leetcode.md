---
titre: LeetCode 2103. Anneaux et Rods -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Code Leet 2103 – *Ringes et Rods*
## Une plongée profonde dans le problème, le code, et l'esprit d'entrevue

> **Mots clés**: LeetCode 2103, Anneaux et Rods, entretien de codage, Java, Python, C++, bitmask, algorithme, entretien d'emploi, structures de données, complexité temporelle, complexité spatiale, préparation des entretiens

---

- Oui. 1. Récapitulation des problèmes

On vous donne une chaîne `rings` de longueur `2 * n`.
Chaque paire de caractères** décrit une bague :

Position dans la paire
Il n'y a pas de problème.
0 (même index)
1 (index imp.)... "9""

La tâche : **Combien de tiges contiennent au moins un anneau de chacune des trois couleurs. **

---

- Oui. 2. Pourquoi ce problème est-il l'entrevue-Amis

- Oui.
- Oui.
Autres Contraintes simples (= 100 anneaux)= Encourage une solution rapide d'O(n)=
Autres Encodage à deux caractères
La manipulation bitwise montre la connaissance des astuces de bas niveau
10 tiges fixes

---

- Oui. 3. La bonne solution – une solution propre et bit-masque

Idée 3.1

- Utilisez un tableau `masks[10]` – un élément par tige.
- Chaque bit d'un entier représente une couleur:
- `1` → Rouge
- `2` → Vert
- `4` → Bleu
- `7` (`1=2=4`) signifie *toutes les trois* couleurs sont présentes.
- Itérer à travers `rings` deux caractères à la fois, mettre à jour le masque, puis compter combien de masques sont égaux `7`.

Code ### 3.2

C'est vrai. Java

"Java
solution de classe {
public int countPoints(Bagues) {
// 10 tiges → 10 masques, chaque masque stocke des bits pour R/G/B
masques int[] = nouveau int[10];

pour (int i = 0; i < anneaux.longueur(); i += 2) {
couleur du char = anneaux.charAt(i);
la tige d'int = anneaux.charAt(i + 1) - '0';

// définir le bit correspondant à la couleur
bit int = 0;
interrupteur (couleur) {
cas «R»: bit = 1; rupture;
cas «G»: bit = 2; rupture;
case «B»: bit = 4; casse;
}
masques[rode]= bit; // OU pour garder toutes les couleurs visibles
}

nombre int = 0;
pour (int masque : masques) {
if (masque == 7) count++; // 7 = 0b111 → toutes les couleurs présentes
}
le nombre de retours;
}
}
«» "

Python

'`python
Solution de classe:
def countPoints(self, anneaux: str) -> Int:
masques = [0] * 10 # 10 tiges

pour i dans la plage(0, len(rings), 2):
couleur = anneaux[i]
tige = int(rings[i + 1])

si couleur == 'R':
masques[rod]
couleur elif == 'G':
masques 2
Autre: # 'B'
masques[rode]

somme de retour (1 pour m en masques si m == 7)
«» "

C++

'`cpp
solution de classe {
public:
Int countPoints(anneaux de cordes) {
masques vectoriels<int>(10, 0);

pour (int i = 0; i < anneaux.dimension(); i += 2) {
couleur du char = anneaux[i];
la tige d'int = anneaux[i + 1] - '0';

bit int = 0;
si (couleur == 'R') bit = 1;
sinon si (couleur == 'G') bit = 2;
Autre bit = 4; // 'B'

masques[rode]
}

nombre int = 0;
pour (int m : masques)
Si (m) 7) + nombre;
le nombre de retours;
}
};
«» "

3.3 Complexité

Métrique Java/Python/C++
C'est-à-dire
**Temps** **O(n)** – passe au-dessus de la chaîne. Autres
**Espace** **O(1)** – tableau fixe 10-int; mémoire supplémentaire constante. Autres

---

- Oui. 4. Le "Bad" – Sur-penser ou mal lire

Piège Explication
C'est pas vrai.
**Utiliser une carte HashMap de jeux** fonctionne mais subit des insertions log-time et des frais de mémoire. Autres
Autres **Storing Full Strings**=Le fait de garder toute la paire `"R3"` par tige conduit à des attributions de chaînes inutiles. Autres
**Double comptage**= Oublier qu'une tige pourrait recevoir plusieurs anneaux de la même couleur – compter des couleurs uniques est la clé. Autres

---

- Oui. 5. Les erreurs courantes

1. **Indexation hors-par-un**
Oublier que le chiffre de la tige est un personnage, pas un entier. Toujours soustraire `'0'`.

2. **Cartographie erronée**
Mélanger `1`, `2`, `4` conduit à des masques comme `6` (`0b110`) – vous ne frapperez jamais `7`.

3. ** Erreur de boucle**
Utiliser `i < rings.length() - 1` au lieu de `i < rings.length()` avec l'étape `2` peut sauter la dernière paire.

4. **Ignorer les contraintes**
En supposant que plus de 10 tiges ou couleurs non RGB vont briser votre logique.

---

- Oui. 6. Exemple d'exécution étape par étape

"rings" Iteration de l'Iteration de l'Iteration de l'Iteration après mise à jour
Ce n'est pas le cas.
"B0R0G0R9R0B0G0"" 0" "B"" 0" 4" "[4,0,0,0,0,0]" Autres
"[5,0,0,0,0,0]"
"[7,0,0,0,0,0,0]" Autres
"[7,0,00,1]" Autres
"[7,0,00,1]" Autres
[7,0,00,1] Autres
12.0.0.0.0.0.0.

Masques finals: tige 0 → `7`, tige 9 → `7`.
**Réponse = 2.**

---

- Oui. 7. Questions de style d'entrevue pour prouver votre profondeur

1. * Pouvez-vous adapter la solution si les tiges étaient 1000 au lieu de 10? *
*Aperçu*: Utilisez un tableau `int[1000]` – encore O(1) espace par rapport à la taille d'entrée.

2. Et si nous avions 5 couleurs ? *
Vous avez besoin de 5 bits (`1,2,4,8,16`) et vérifiez pour `31`.

3. Pourriez-vous implémenter ceci sans opération de bit? *
Montrez une solution basée sur HashSet, mais discutez des compromis.

4. * Expliquez pourquoi un seul entier par tige est suffisant. * *
Parlez de *bitmask representation* et *constante-espace garanties*.

---

- Oui. 7. Comment ce blog aide votre recherche d'emploi

1. **SEO Boost** – L'article contient des mots-clés cibles répétés que les recruteurs recherchent :
****************************************************************************************************************************************************************************************************************************************************************

2. ** Apprentissage structuré** – En lisant les sections "good", "bad" et "ugly" vous verrez à la fois la stratégie optimale et les pièges communs, vous donnant confiance dans une interview en direct.

3. **Show‐Off sur votre portfolio** – Insérez ce post sur votre blog personnel ou GitHub README. Les recruteurs aiment voir les solutions réelles expliquées clairement.

4. **LiendIn / Medium Post** – Partagez cet article sur LinkedIn ou Medium avec le titre LeetCode 2103 – Anneaux et barres: Java/Python/C++ Code & Interview Tips** pour augmenter la visibilité parmi les gestionnaires d'embauche.

---

7. TL;DR – Extraits de code rapide

"Java
// Java
nouvelle solution().countPoints("R0G0B0R0G0B0");
«» "

'`python
# Python
Solution().countPoints("R0G0B0R0G0B0")
«» "

'`cpp
// C++
Solution().countPoints("R0G0B0R0G0B0");
«» "

---

- Oui. 8. Pensées finales

- **Lire attentivement les contraintes** – 10 tiges est une limite dure qui économise de l'espace.
- **Préférez des tableaux de taille constante** sur des conteneurs dynamiques lorsque le domaine est fixé.
- **Bitwise tricks** sont un point de départ dans le codage des entretiens; ils démontrent une maîtrise sur la représentation binaire et l'efficacité.
- ** Expliquez votre logique** pendant l'entrevue. Marchez à travers un petit exemple ; il montre l'intervieweur que vous pensez clairement.

---

À emporter

Mastering *Rings and Rods* est une victoire rapide dans votre arsenal d'entretien. En montrant l'approche bit-mask optimale en Java, Python et C++, vous démontrez non seulement la compétence de codage, mais aussi l'état d'esprit analytique que les recruteurs désirent. Postez cette solution, ajoutez une courte vidéo à travers, et vous serez un candidat fort pour toute entrevue de backend ou de conception de système.

Bon codage ! C'est ce qu'il a dit.

---