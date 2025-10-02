---
titre: LeetCode 1974. Temps minimum pour taper un mot en utilisant une machine à écrire spéciale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Vous trouverez ci-dessous les implémentations **complètes** pour LeetCode **1974 – Temps minimum pour taper un mot en utilisant une machine à écrire spéciale** dans **Java, Python 3, et C++**.
Toutes les solutions partagent la même logique :
*Gardez la trace de la position actuelle du pointeur (initialement `'a''), calculez la distance dans le sens des aiguilles d'une montre et dans le sens des aiguilles d'une montre jusqu'au caractère suivant, prenez la plus petite, ajoutez-la au total en cours d'exécution, puis ajoutez 1 seconde pour l'opération de type. *

Langue Fichier Code
C'est quoi ?
*Java**
**Python**
*C++**

---

- Oui. Java – `Solution.java "

"Java
solution de classe publique {
***
* Renvoie le nombre minimum de secondes pour saisir le mot donné
* sur la machine à écrire circulaire.
*
* @param word une chaîne composée uniquement de lettres anglaises minuscules
* @retour temps total en secondes
*/
public int minTimeToType(mot de frappe) {
temps int = 0; // temps total passé
char current = 'a'; // pointeur commence à 'a'

pour (int i = 0; i < word.longueur(); i++) {
cible char = mot.charAt(i);
int diff = Math.abs(cible - courant); // distance dans le sens des aiguilles d'une montre
int move = Math.min(diff, 26 - diff); // chemin le plus court
temps += déplacement + 1; // déplacement + type
courant = cible; // pointeur de mise à jour
}
le temps de retour;
}
}
«» "

---

### Python – `solution.py "

'`python
Solution de classe:
def minTimeToType(self, mot: str) -> Int:
"""
Calcule le nombre minimum de secondes nécessaires pour taper
le mot donné sur un clavier circulaire.

Paramètres
- Oui.
mot : str
Des lettres anglaises minuscules seulement.

Retourne
- Oui.
Int
Temps total en secondes.
"""
durée = 0
courant = 'a '

pour cible en mot:
diff = abs(ord(target) - ord(current))
mouvement = min(diff, 26 - diff)
temps += mouvement + 1 # mouvement + type
courant = cible

temps de retour
«» "

---

### C++ – `solution.cpp "

'`cpp
solution de classe {
public:
int minTimeToType(mot chaîne) {
temps int = 0;
courant char = 'a';

pour (char cible : mot) {
int diff = abs(cible - courant); // distance dans le sens des aiguilles d'une montre
mouvement int = min(diff, 26 - diff); // distance la plus courte
temps += déplacement + 1; // déplacement + type
courant = cible; // pointeur de mise à jour
}
le temps de retour;
}
};
«» "

---

> **Pourquoi c'est optimal* *
> Chaque caractère est traité une fois → **O(n)** temps, **O(1)** espace auxiliaire.
> L'algorithme utilise la propriété que l'alphabet est circulaire, de sorte que la distance entre deux lettres est le minimum des étapes dans le sens des aiguilles d'une montre et dans le sens des aiguilles d'une montre.

---

2. Article du blog – Le bon, le mauvais et le mauvais de LeetCode 1974

> **SEO Mots-clés**: *LeetCode 1974*, *Minimum Time to Type Word*, *machine à écrire spéciale*, *solution Java*, *solution Python*, *solution C++*, *codage interview*, *entretien avec un ingénieur logiciel*, *problème algorithmique*, *préparation à l'entrevue d'emploi*, *codage challenge*, *complexité du temps*, *complexité de l'espace*.

---

Récapitulation des problèmes

> **LeetCode 1974 – Temps minimum pour taper un mot en utilisant une machine à écrire spéciale* *
> *On vous donne une machine à écrire circulaire avec les 26 lettres minuscules (`a`–`z`).
> Au départ, le pointeur indique "a". Dans une seconde, vous pouvez :*
> 1. *Déplacez le pointeur dans le sens des aiguilles d'une montre ou dans le sens des aiguilles d'une montre. *
> 2. *Tapez la lettre que le pointeur indique actuellement. *
> *Avec un mot, calculez le minimum de secondes nécessaires pour le taper. *

---

Contraintes rapides

Valeur des contraintes
C'est pas vrai.
Durée de la phrase 1 ... 100
Alphabet seulement lettres anglaises minuscules

---

Pourquoi Ce problème est génial pour les entrevues

1. **Simplicité + profondeur**
- À première vue, il ressemble à un problème trivial de distance, mais caché à l'intérieur sont des leçons sur les structures de données circulaires, les choix avides, et la sous-structure optimale.

2. **Parallèle réelle au monde* *
- Pensez à une machine à écrire mécanique ou à un cadran rotatif sur un coffre. Comprendre le mouvement le plus court dans une disposition circulaire est commun dans la robotique, l'UI/UX (cadrans circulaires) et les systèmes embarqués.

3. **Substructure optimale claire* *
- Pour chaque nouveau caractère, nous n'avons besoin que de la position précédente pour décider du meilleur mouvement. Pas d'explosion d'état → *programmation dynamique* n'est pas nécessaire; une approche *greedy* fonctionne parfaitement.

4. **Peu de temps**
- Temps `O(n)` avec mémoire constante: un modèle incontournable pour le codage des entretiens où les contraintes de temps sont serrées.

5. ** Facile à étendre**
- Une fois que vous maîtrisez cela, vous pouvez gérer des variations: différents alphabets, mouvements pondérés, ou même des mises en page non linéaires.

---

Les mauvaises – Pièges communs

Pourquoi il fait défaut
- C'est quoi ?
**Obligation de la valeur de la valeur de la valeur de la valeur de la valeur de la valeur de la valeur de la valeur de référence Autres
**Distances variables**= Utiliser `abs(cur - prev)` seulement== Ignore l'enveloppe circulaire; par exemple `a` à `z` devrait être 1, et non 25==
**Codage à main Écrire `26` partout sans commentaires Œuvre uniquement pour l'anglais minuscule; échoue sur Unicode ou d'autres alphabets
**Utilisation de `Math.abs` avec des caractères en Java** C'est exact, mais beaucoup de nouveaux codeurs oublient d'utiliser `abs` sur `int` différences
**Itérer avec des indices et appeler `charAt` en Java**="word.charAt(i)` à l'intérieur de la boucle="Toujours bien, mais l'utilisation d'un for-loop amélioré ("pour (char ch : word.toCharArray())") est plus propre et évite les erreurs off-by-one="
**Ne pas réinitialiser le pointeur**

---

## Les cas les plus horribles – les cas de bord que vous devriez tester

Autres Tester la sortie attendue Pourquoi il est Tricky
-- -- -- -- -- -- --
"Mot = "a"" "1" "Une seule action de type; aucun mouvement. Autres
Déplacer dans le sens contraire des aiguilles d'une montre 1 étape + type. Autres
Déplacer 1 pas (dans le sens des aiguilles d'une montre) + type, puis taper `z`. Autres
"Mot = "abcdefghijklmnopqrstuvwxyz""""""51"" 25 mouvements + 26 types (chaque mouvement minimal). Autres
Il n'y a pas de mouvement après la première `z`; chaque `z` suivante ne coûte qu'une seconde. Autres
Mot = "qwerty" "27" Déplacements mixtes; garantit que l'algorithme choisit la bonne direction à chaque fois. Autres
"Mot = "abcdefghijklmnopqrstuvwxyza"""""27"" Enveloppe circulaire de `z` retour à `a` coûts 1, pas 25. Autres

> **Astuce:** Écrire un script rapide pour forcer tous les mots de longueur 1–3 et comparer avec votre implémentation. Il garantit que la logique de distance est sans bug.

---

Solution étape par étape

- Oui. 1. Initialiser

Texte
pointeur = 'a' // position de départ
durée = 0
«» "

- Oui. 2. Pour chaque caractère `c` en `mot`

1. **Distance de calcul absolue**
""diff
- pointeur
«» "
2. **Distance de sortie**
""diff
wrap = 26 - diff
«» "
3. **Choisissez le mouvement le plus court* *
""diff
mouvement = min(diff, enveloppe)
«» "
4. **Ajouter du temps**
""diff
temps += déplacer + 1 // +1 pour taper le caractère
«» "
5. **Mettre à jour le pointeur**
""diff
pointeur = c
«» "

- Oui. 3. Temps de retour "

---

Analyse de complexité

Mesure Résultat
C'est pas vrai.
**Heure**="O(n)` où `n = mot.length()` (passe unique)
**Espace** – seulement quelques variables entières/char Autres

---

Les variations que vous pourriez rencontrer

Variation Comment s'ajuster
C'est quoi ?
**Differente taille de l'alphabet** Autres
**Moyens pondérés**= Précalculer une matrice de coûts de 26×26; utiliser `move = min(diff, wrap, heightedCost)'. Autres
**Mise en page non circulaire** Autres
**Fastest Type d'action seulement**= Supprimer le `+1` et rapporter juste mouvement. Autres

---

À emporter

> **LeetCode 1974** est un exemple de manuel de la façon dont un puzzle apparemment simple cache un motif avide, renforce l'importance de la manipulation des structures circulaires, et vous prépare à des questions d'entrevue réelles qui exigent à la fois la justesse et l'efficacité.
> Les extraits Java, Python et C++ ci-dessus sont prêts à être collés dans l'éditeur LeetCode ou dans tout environnement local.
> **Codage heureux – et que votre pointeur se déplace toujours dans la direction la plus rapide!**

---

> **Si vous avez trouvé cet article utile, déposez un """ sur la repo ou partagez-le avec un ami qui se prépare à des entretiens techniques. * *