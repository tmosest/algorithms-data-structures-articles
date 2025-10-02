---
titre: LeetCode 418. Fixation de l'écran de la peine -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Fixation de l'écran de la peine – LeetCode 418
o 1) Optimisation**
*Un article complet, multilingue et convivial, qui vous aidera à décrocher votre prochaine entrevue de codage. *

---

Aperçu du problème

Sujet Détails
C'est quoi ?
**Problème *************************************************************************************************************************************************************************************************************************************************************
**Input** Autres
**Output**= `int` – le nombre de fois que la phrase peut être installée sur un écran de `rows × cols` Autres
**Constraints**

Vous devez préserver l'ordre des mots. Un mot ne peut pas être divisé ; les mots sont séparés par un seul espace. Les cellules vides à l'écran sont remplies de `-` dans les exemples.

---

# # # , , Intuition

L'écran est scanné ligne par ligne. Chaque ligne peut contenir autant de mots *toute* que la largeur le permet. Une fois qu'une ligne est pleine, le mot suivant commence sur la ligne suivante.
La simulation naïve est facile mais **O(rows × len(sentence)** – beaucoup trop lente quand `rows` est 20 000 et la phrase est longue.

L'observation clé : l'état* de l'écran après chaque ligne n'est que l'index ** du mot** qui sera imprimé ensuite.
Si nous savons comment l'indice change après une ligne, nous pouvons -jump-de nombreuses lignes à la fois.

---

Algorithme – O(lignes) Greedy + Mémorisation

1. **Pré-calculer** l'index des mots suivant pour chaque mot de la phrase.
"NextIdx[i]" vous dit: *si le mot suivant à imprimer est `sentence[i]`, quel mot sera le suivant après la fin de la ligne actuelle? *
2. **Itérer sur les lignes** tout en maintenant un pointeur `curIdx` à l'index courant des mots.
Sur chaque itération:
`curIdx = nextIdx[curIdx]` – sautez au mot de départ suivant.
Gardez un compteur `fits` qui augmente de 1 chaque fois que nous terminons un cycle complet de la phrase (c.-à-d. quand `curIdx` retourne à 0).
3. **Retour** le compteur « fits ».

**Pourquoi ça marche* *
Parce que chaque ligne ne dépend que du mot de départ. Une fois que nous savons comment une ligne transforme le mot de départ, le processus est déterministe et peut être répété ligne par ligne.

**Complexité* *
- Heure: **O(lignes + n)**, où *n* = "sentence.longueur".
- Espace : **O(n)** pour le tableau `nextIdx`.

---

## 4-

Autres Décision Pourquoi c'est important Comment gérer
- C'est quoi ?
Autres Mot plus long que "cols" , impossible à adapter, mais les contraintes l'interdisent , Pas nécessaire ,
La sentence a exactement un mot "nextIdx[0]" sera `0` après chaque ligne
# # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #

---

Code – trois langues

> **Tip**: La version Java utilise `int[] nextIdx`, la version Python utilise une liste, et la version C++ utilise un `vecteur<int>`. Tous partagent la même logique.

#### 5.1 Java

"Java
solution de classe publique {
mots int publics Typing(String[] phrase, int lignes, int cols) {
int n = phrase. longueur;
int[] nextIdx = nouveau int[n];
Int curIdx = 0;

// Pré-calculer l'index suivant pour chaque mot
pour (int i = 0; i < n; i++) {
longueur int = 0;
j = i;
alors que (vrai) {
wordLen = phrase[j].longueur();
en cas de rupture (longueur + motLen > cols);
longueur += mot Len;
j = (j + 1) % n;
// Ajouter un espace après chaque mot sauf le dernier sur la ligne
si (longueur < cols) longueur++; // espace
}
nextIdx[i] = j;
}

= 0;
pour (int r = 0; r < lignes; r++) {
curIdx = nextIdx[curIdx];
Si (curIdx) 0) fits++;
}
les retours;
}
}
«» "

5.2 Python

'`python
Solution de classe:
Mots Dactylographie(self, phrase: list[str], lignes: int, cols: int) -> Int:
n = len(sentence)
suivant_idx = [0] * n

# Précalculer l'index suivant pour chaque mot
pour i dans la plage(n):
longueur = 0
j = i
alors que Vrai:
mot_len = len(sentence[j])
si longueur + word_len > cols:
pause
longueur += mot_len
j = (j + 1) % n
# espace après un mot, à moins qu'il dépasse la ligne
si longueur < cols:
longueur += 1
next_idx[i] = j

cur_idx, correspond = 0, 0
pour _ dans l'intervalle(s) :
cur_idx = next_idx[cur_idx]
si cur_idx == 0:
ajustement += 1
retour
«» "

C++

'`cpp
solution de classe {
public:
Int mots Dactylographie(vecteur<string>& phrase, lignes int, int cols) {
int n = phrase.size();
vecteur<int> suivantIdx(n);

// Pré-calculer l'index suivant pour chaque mot
pour (int i = 0; i < n; ++i) {
Int len = 0;
j = i;
alors que (vrai) {
int wlen = phrase[j].size();
en cas de rupture (len + wlen > cols);
LEN += WLEN;
j = (j + 1) % n;
Si (lent < cols) ++len; // ajouter de l ' espace
}
nextIdx[i] = j;
}

int curIdx = 0, correspond à 0;
pour (int r = 0; r < lignes; ++r) {
curIdx = nextIdx[curIdx];
Si (curIdx) 0) + ajustements;
}
les retours;
}
};
«» "

---

C'est pas vrai. Discussion sur le blogue : Bon, mauvais et affreux

> **SEO Mots-clés**: *sensence screen fitting, leetcode 418 solution, interview de codage, entretien d'emploi, conception d'algorithme, cupidité, optimisation, Java, Python, C++ *

### 6.1 La Force brute

> ``python
> # O(rows * words_in_sentence) – trop lent pour les lignes 20k
> pour la ligne de range(s):
> pour mot dans la phrase:
> ...
> `` "
>
> *Pourquoi il échoue :*
> Chaque ligne est en boucle sur toute la phrase, même lorsque la phrase est longue, mais la plupart des mots ne correspondent jamais à une seule ligne. La complexité souffle à des millions d'opérations.

#### 6.2 La bonne humeur + mémorisation

*Idée clé:* *Rappelez-vous où vous finissez après chaque ligne. *
- Pré-calculer la transition "nextIdx".
- Pour chaque ligne juste sauter: `curIdx = nextIdx[curIdx]`.
- La complexité est linéaire dans le nombre de lignes – *optimal pour le codage des entrevues*.

### 6.3 La variante du DP (d'après un éditorial)

Certaines solutions utilisent une programmation dynamique avec un tableau 2-D pour enregistrer l'état de chaque paire ligne-colonne.
Alors que techniquement correct, il utilise **O(rows·cols)** mémoire et le temps, ce qui le rend * inutile* et * plus difficile à comprendre*.
Pour une interview, gardez la solution simple et lisible – ** l'approche gourmande gagne**.

6.4 Entretien— Conseils prêts

Motif
- Oui.
**Expliquer la transition d'état** (index des mots suivant)
**Cas de bord des phrases** (mot unique, longueur de phrase 1, etc.) Démontrer la rigueur
**Donner une analyse de la complexité**
**Afficher le code en deux langues** Autres

---

C'est pas vrai. A emporter

- **Problème**: Comptez combien de fois une phrase correspond à un écran donné.
- **Best Solution**: Greedy + mémorisation ('O(rows + n)').
- **Key Insight**: L'état de l'écran après chaque ligne est entièrement déterminé par l'index du mot suivant à imprimer.
- **Langues**: Java, Python, C++ – tous utilisent le même algorithme.

> La maîtrise de ce modèle vous aidera non seulement à as *LeetCode 418* mais aussi à toute question d'entrevue impliquant *string packing*, *cycle patterns* ou *greedy simulation*. Bonne chance pour ce prochain travail !