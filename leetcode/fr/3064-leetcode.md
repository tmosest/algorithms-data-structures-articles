---
titre: LeetCode 3064. Devine le nombre en utilisant des questions bitwise I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

♪ Devine le nombre en utilisant des questions bitwise – 3064
C++ – Complet, SEO-Optimized Guide**

> Vouloir casser LeetCode 3064 – *Guess the Number Using Bitwise Questions*?
> Ce post vous fait découvrir le problème, montre la solution **O(1)** la plus rapide, donne du code entièrement travaillé en **Java, Python et C++**, et plonge dans le *bon, le mauvais et le laid* de l'API set-bits commune.
> Parfait pour la préparation d'entrevue, la pratique du codage ou la construction de votre CV.

---

Table des matières

Lien
- Oui.
Aperçu du problème
Intuitive Brute-Force Autres
Une approche rapide
Mise en œuvre Java
Mise en œuvre de Python Autres
Mise en œuvre C++
#complexité
Pièges communs et cas de bordure
Autres stratégies
Conclusion et conseils professionnels

---

Aperçu du problème

> **LeetCode 3064 – Devine le nombre en utilisant des questions bitwise**
> **Difficulté:** Moyenne

On nous donne un entier caché `n` (1 ≤ n < 230).
Le seul outil à notre disposition est une API :

Texte
Int commonSetBits(int num);
«» "

`commonSetBits(num)` renvoie le nombre de positions **bit** où `n` et `num` ont un `1`.
Autrement dit :

Texte
commonSetBits(num) == popcount(n & num)
«» "

Votre objectif est de récupérer `n` en appelant l'API n'importe quel nombre de fois (le moins le mieux) et de le retourner.

> **Insight clé**
> Si nous testons un nombre qui a exactement un jeu de bits (par exemple, `1, 2, 4, 8, ...`), l'API retournera `1` si ce bit est également défini dans `n`.
> Donc nous pouvons simplement vérifier chacun des 30 bits possibles une fois et assembler la réponse.

---

## ♫ Brute-Force intuitive

Une approche naïve consiste à interroger tous les entiers possibles dans la plage autorisée (`1 ... 230-1`).
Pour chaque candidat `x` nous vérifions si `commonSetBits(x) == 1`.
Ceci est **O(230)** appelle – complètement impraticable et contre l'esprit du problème.

Pourquoi c'est mauvais ? *
- 1 073 741 823 AP J'appelle → impossible dans les délais.
- Frais généraux excessifs du réseau/IO.
- Donne peu de vue sur la nature bit-wise du problème.

---

Approche O(1) la plus rapide – Bit by Bit

Idée

1. **Itérer sur chaque position du bit** `i` (0 ... 29).
2. Construire `masque = 1 << i`.
3. Appeler `commonSetBits(masque)`.
* Si la réponse est `1`, définissez ce bit dans `n`.
* Si la réponse est `0`, laissez le bit dégagé.

Puisque nous effectuons **exactement 30 appels d'API**, l'algorithme fonctionne en temps constant par rapport à la taille d'entrée.

Pourquoi 30 appels ?
- Oui. Le nombre maximal autorisé (`230-1`) est de 30 bits.
- Chaque appel nous indique l'état d'un morceau, donc 30 appels suffisent.

Code Pseudo

Texte
résultat = 0
pour i de 0 à 29:
masque = 1 << i
si commonSetBits(masque) == 1 :
résultat = masque
résultat du retour
«» "

---

Mise en œuvre Java

"Java
***
* LeetCode 3064 – Devinez le nombre en utilisant des questions bitwise
* Auteur: Votre nom
* Mots clés: Manipulation Bit, Brute Force, Interview
*/
public classe Solution étend problème {
public int findNumber() {
la valeur n = 0;
// 30 bits (0-base index)
pour (int i = 0; i < 30; i++) {
masque int = 1 << i;
si [commonSetBits(masque)] 1) {
le masque;
}
}
retour n;
}
}
«» "

**Pourquoi il s'agit de la solution Java *

- Utilise *bit de déplacement* au lieu de `Math.pow` pour la vitesse.
- Coure en temps constant : **O(1)**.
- Utilise seulement O(1) espace supplémentaire.

---

Mise en œuvre de Python

'`python
"""
LeetCode 3064 – Devine le nombre en utilisant des questions bitwise
"""

solution de classe (problème):
def findNumber(self) -> Int:
n = 0
pour i dans la plage(30): # bits 0,29
masque = 1 << i
i self.commonSetBits(masque) == 1 :
n.= masque
retour n
«» "

**Notes de python**

- `Problem` est la classe de base qui fournit `commonSetBits`.
- `self.commonSetBits` est utilisé dans la méthode.
- Toujours **O(1)** temps et espace.

---

Mise en œuvre du C++

'`cpp
***
* LeetCode 3064 – Devinez le nombre en utilisant des questions bitwise
* Auteur: Votre nom
* Complexité: O(1) temps, O(1) espace
*/
class Solution : public Problème {
public:
int findNumber() remplace {
la valeur n = 0;
pour (int i = 0; i < 30; ++i) {
masque int = 1 << i;
si [commonSetBits(masque)] 1 )
le masque;
}
retour n;
}
};
«» "

*Pourquoi C++ fonctionne de même*

- Utilise le décalage bit (`1 << i`) tout comme Java/Python.
- `commonSetBits` est une méthode virtuelle définie dans la classe de base.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Loop sur 30 bits **O(1)** (constante 30 itérations)
Chaque appel API est négligeable (fourni par LeetCode)

**Total :**
- **Heure:** O(1) – 30 appels API quel que soit le numéro caché.
- **Espace:** O(1) – seulement quelques variables entières.

---

## --Pièges communs et cas de bord

Pourquoi ça arrive
- Oui.
**L'utilisation de `1 << 30`**" dépasse un entier de 32 bits signé. = Stick à `1 << 29` pour le bit le plus élevé dans un nombre de 30 bits, ou utiliser `1L << i` si 64 bits. Autres
**Utilisation incorrecte de l'API**= Certaines solutions appellent par erreur `commonSetBits(1 << i)` plusieurs fois ou mélangent des indices de bits. Gardez l'appel à l'intérieur de la boucle; assurez-vous que chaque masque a exactement un jeu de bits. Autres
**Les erreurs hors-par-un peuvent sauter un peu ou dépasser la limite. Loop de `i = 0` à `i < 30`. Autres
**En supposant une limite entière de 32 bits**.Le nombre caché peut être jusqu'à "230-1", donc seulement 30 bits sont pertinents. Ne pas tester au-delà de 29. Autres

---

Stratégies alternatives

Stratégie Quand utiliser Complexité
C'est pas vrai.
**Binary Search sur les bits**= Si vous pouvez demander des numéros avec plusieurs bits définis et voulez moins de 30 appels. Environ `log2(30)` 5 appels si des masques habilement choisis. Autres
**Echantillonnage aléatoire**= Lorsque l'API est bruyante ou coûteuse; utile pour des problèmes de longueur de bits plus grands. En fonction de l'échantillonnage; non garanti O(1). Autres
**Comptage par le biais du débit** O(30) appelle toujours, mais avec une logique plus complexe. Autres

> **Pourquoi la méthode simple de 30 appels est généralement la meilleure**
> Les contraintes de problèmes garantissent que 30 appels sont à la fois suffisants et minimes. Ajouter la complexité rend le code plus difficile à lire et augmente le risque de bugs.

---

Conclusion et conseils professionnels

Vous venez de maîtriser **LeetCode 3064 – Devinez le nombre en utilisant des questions bitwise**.

- **Ce que cherchent les employeurs**:
* Compréhension claire des opérations bitwise.
* Capacité de traduire un problème en une solution optimale à temps constant.
* Code propre, langue-agnostique (Java, Python, C++).

- ** Prochaines étapes** :
* Pratiquer d'autres * manipulation de bits * problèmes: Numéro unique, série Bitwise et & Or, Kth le plus petit dans l'arbre de recherche binaire, etc.
* Construisez une repo GitHub avec vos solutions – présente des compétences de résolution de problèmes aux recruteurs.
* Écrire un blog (comme celui-ci) pour expliquer votre processus de pensée – idéal pour le CV et le portfolio.

**Rappelez-vous**: Dans les entrevues, *expliquez votre intuition*, * montrez la manipulation de cas de bord* et * parlez des compromis temps/espace*.
Bonne chance pour décrocher ce rôle technique ! C'est ce qu'il a dit.

---

Mots clés

- LeetCode 3064
- Devine le nombre en utilisant des questions bitwise
- solution bitwise ET API
- Python Java C++ Solutions LeetCode
- Entretien de manipulation de bits O(1)
- fonction commonSetBits
- entretien prép bitwise tours
- LeetCode 3064 discussion
- coder la stratégie d'entretien bitwise

---

Bon codage, et que vos interviews soient plus douces !