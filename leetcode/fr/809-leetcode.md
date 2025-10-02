---
titre: LeetCode 809. Mots expressifs -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
809. Mots expressifs – Solution à pile complète (Java / Python / C++)

Ci-dessous vous trouverez une implémentation propre et entièrement commentée pour **Java**, **Python** et **C++**.
Tous les trois résolvent le même problème LeetCode :

> Compte tenu d'une chaîne `s` et d'un éventail de mots de requête, retourner combien de ces mots peuvent être étendus en `s` en étendant à plusieurs reprises tout groupe de lettres identiques à **longueur ≥ 3**.

La solution utilise une technique classique à deux points qui fonctionne dans le temps **O(=S +=Sword=)** et **O(1)** espace supplémentaire.

---

### Java

"Java
// 809. Mots expressifs
// Heure : O(=S) +=word=)
// Espace : O(1)
solution de classe publique {
public int expressif Mots(String s, String[] mots) {
résultat int = 0;
pour (Pièce w : mots) {
si (estStretchable(s, w)) result++;
}
le résultat du retour;
}

booléen privé estStretchable(String s, String w) {
// Si w est plus long que s il ne peut jamais correspondre
si (w.length() > s.length()) retourne faux;

int i = 0, j = 0; // i → s, j → w
pendant que (i < s.length() && j < w.length()) {
si (s.charAt(i) != w.charAt(j)) retourne faux;

char cur = s.charAt(i);

// Longueur du compte en s
La valeur de l'unité de mesure est égale à la valeur de l'unité de mesure.
(i < s.length() && s.charAt(i) == cur) {
sCount++; i++;
}

// Nombre longueur de course en w
= 0;
pendant que (j < w.leng() && w.charAt(j) == cur) {
wCount++; j++;
}

// L'exécution ne doit pas dépasser l'exécution
si (wCount > sCount) retourner faux;

// Si la course est petite en s, elle doit correspondre exactement
si (sCount < 3 & sCount != wCount) retourner faux;
}

// Les deux cordes doivent être entièrement consommées
retour i == s.length() && j == w.length();
}
}
«» "

---

Python

'`python
# 809. Mots expressifs
♪ Temps: O(len(s) + somme(len(w) pour w en mots)
♪ Espace: O(1)

Solution de classe:
d ' expression Mots(self, s: str, mots: list[str]) -> Int:
retour sum(self._stretchable(s, w) pour w en mots)

def _stretchable(self, s: str, w: str) -> C'est vrai.
si len(w) > len(s):
Retour Faux

i = j = 0
alors que i < len(s) et j < len(w):
si s[i] != [j]:
Retour Faux

ch = s[i]
s_cnt = 0
alors que i < len(s) et s[i]== Ch:
_cnt += 1
i += 1

w_cnt = 0
alors que j < len(w) et w[j] == Ch:
w_cnt += 1
j += 1

si w_cnt > s_cnt: # w a plus de lettres dans ce groupe
Retour Faux
si s_cnt < 3 et s_cnt != w_cnt : # ne peut pas étirer un groupe court
Retour Faux

retour i == len(s) et j == len(w)
«» "

---

C++

'`cpp
// 809. Mots expressifs
// Heure : O(=S) +=word=)
// Espace : O(1)

solution de classe {
public:
int expressive Mots(chaîne s, vecteur<chaîne> &mots) {
Int ans = 0;
pour (auto & w : mots)
si (stretchable(s, w)) ++ans;
le retour des an;
}

particulier:
bool isStretchable (chaîne &s Const, chaîne &w Const) {
si (w.size() > s.size()) retourne faux;

taille_t i = 0, j = 0; // i -> s, j -> w
pendant que (i < s.size() && j < w.size()) {
si (s[i] != w[j]) retourner faux;

char cur = s[i];
taille_t sCnt = 0;
alors que (i < s.size() && s[i] == cur) {
++sCnt; ++i;
}

taille_t wCnt = 0;
pendant que (j < w.size() && w[j] == cur) {
++w cnt; ++j;
}

si (wCnt > sCnt) retourne faux; // w plus long que s
si (sCnt < 3 && sCnt != wCnt) retourner false; // ne peut pas s'étirer
}
retour i == s.size() && j == w.size();
}
};
«» "

---

Article du blog – Mots expressifs : le bon, le mauvais et le mauvais

> **SEO Mots-clés**: *Expressive Words Leetcode, solution Leetcode 809, entretien d'algorithme Java Python C++, comment résoudre des mots expressifs, algorithme d'entretien d'emploi, problème de mots extensibles, questions d'entretien d'algorithme*

---

Introduction

Si vous préparez une interview d'ingénierie logicielle, vous rencontrerez rapidement **LeetCode 809 – Expressive Words**. Il est trompeurment simple, mais voyage souvent les candidats parce qu'il mélange la manipulation de la chaîne avec une règle de "Stretch" qui est facile à mal interpréter.

Dans cet article, nous allons décomposer les aspects **good**, **bad**, et **ugly** du problème, marcher à travers une solution robuste dans **Java**, **Python** et **C++**, et mettre en évidence des takeaways prêts à l'interview.

> *Pourquoi le titre? *
> Le bon, le mauvais et le mauvais est une référence classique de *Le Parrain*. Il indique que nous plongeons profondément dans ce qui *travaille*, ce qui *fail* et ce qui *est facile de se tromper*.

---

Récapitulation des problèmes (bon)

Vous avez reçu :
- Une chaîne "s" (la chaîne "stretchy").
- Un tableau `words[]` de mots de requête candidats.

Une opération **Stretch** est:
1. Choisissez un groupe de caractères identiques en un mot.
2. Ajoutez des copies supplémentaires de ce caractère afin que la longueur du groupe soit **≥ 3**.

L'objectif : Compter le nombre de mots en mots [] peut être étendu en "s".

Pourquoi est-ce bon ?
- ** Contraintes claires**: "1 ≤ s.longueur, mots.longueur ≤ 100". Donc un scan linéaire est parfait.
- **Déterministe**: Pas de hasard ou de recul; l'approche avide fonctionne.

---

C'est vrai. Où se trouve le problème (mal)

1. ** La règle de l'étirement
Vous *ne pouvez pas* étirer un groupe dans `s` qui est déjà plus petit que 3. Seuls les groupes **≥ 3** peuvent être la cible de l'étirement.
* Piège commun* : Pensant que vous pouvez rétrécir `s`=" groupe pour correspondre `w`, ce qui est faux.

2. **Bogues hors-par-un dans le comptage de la longueur d'exécution**
En comptant des lettres identiques contiguës, oublier d'augmenter les deux pointeurs conduit à des boucles infinies ou à des vérifications mal alignées.

3. **Incompatibilité des dossiers d'Edge**
- « s » est plus court que « w ».
- `s` contient des groupes supplémentaires que `w` n`a pas.
- "w" a un groupe plus long que le groupe équivalent.

La partie "bad" est qu'une seule règle off-by-one ou mal comprise peut tuer votre solution.

---

C'est pas vrai. La réparation classique à deux points (Ugly → Beau)

La solution complexe implique souvent des boucles imbriquées, des cartes de fréquence de construction ou des passes multiples. La façon la plus propre est l'approche **deux points, longueur d'exécution**:

1. Traverse `s` et `w` simultanément.
2. Lorsque les caractères actuels correspondent, compter combien de fois chaque apparaît consécutivement (longueur de la course).
3. Appliquer les règles d'étirement :
- La longueur de l ' essai ne peut pas dépasser la longueur de l ' essai.
- Si la longueur d'exécution est ** < 3**, elle doit être égale à la longueur d'exécution exacte.
4. En cas d'inadéquation, avorter.

La beauté se trouve dans **O(1)** mémoire supplémentaire et une seule passe sur chaque mot.

---

C'est vrai. Code Marche à suivre (Java)

"Java
solution de classe publique {
public int expressif Mots(String s, String[] mots) {
cnt = 0;
pour (String w : mots) si (estStretchable(s, w)) cnt++;
retour cnt;
}

booléen privé estStretchable(String s, String w) {
si (w.length() > s.length()) retourne faux;
i = 0, j = 0;
pendant que (i < s.length() && j < w.length()) {
si (s.charAt(i) != w.charAt(j)) retourne faux;
char cur = s.charAt(i);
int sCnt = 0, wCnt = 0;
alors que (i < s.leng() && s.charAt(i) == cur) { sCnt++; i++; }
pendant que (j < w.leng() && w.charAt(j) == cur) { wCnt++; j++; }
si (wCnt > sCnt) retourner faux;
si (sCnt < 3 && sCnt != wCnt) retourner faux;
}
retour i == s.length() && j == w.length();
}
}
«» "

> **Pourquoi c'est bien* *
> *variables claires*, *points de sortie uniques*, *pas de nombres magiques*.

---

#### 6=2 Python & C++ – Comparaisons rapides

- **Python**: Utilise les boucles `while` et `len()` pour les limites.
- **C++**: Utilise `size_t` pour les indices, `string` et `vector<string>`.

Tous partagent le même flux logique, ce qui facilite la traduction entre les langues.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Mots-clés:
"est stretchable" ()

Avec les limites données (= 100 caractères), la performance est insignifiante, mais l'algorithme s'échelle linéairement si les chaînes grandissent.

---

- Oui. Que montrer sur votre CV

- **Problème**: LeetCode 809 – Mots expressifs
- **Skills**: manipulation de chaînes, encodage de longueur d'exécution, algorithmes gourmands, technique à deux points
- **Langues**: Java, Python, C++
- **Résultat**: solution propre O(n) avec couverture complète des essais

Mentionnez que vous **évitez** les pièges communs d'erreurs hors-par-un et de mauvaises interprétations des conditions d'étirement, démontrant l'attention aux détails – un trait clé de l'entrevue.

---

Liste de contrôle des essais

Autres Essai Description
- C'est quoi ?
"s = "heeellooo", mots = ["hello", "hi", "hélio"]` Produit escompté : 1
"s = "zzzzyyyyy", mots = ["zzyy", "zy", "zyy"]` Produit escompté : 3
"s = "abcd", mots = ["abc", "abcd", "ab"] Tous les retours
"s = "aabbcc", mots = ["aabbcc", "aabbcc"] L'étreinte n'est pas autorisée sur les groupes < 3
"s = "aaa", mots = ["aa"] Il faut retourner 0 (groupe trop court)

Ajoutez des cas de bord pour les groupes à lettre unique, les tableaux vides et les chaînes de longueur maximale.

---

#### 10) Dernier départ (Le méchant devient beau)

> Si vous êtes coincé, rappelez-vous que le problème est essentiellement une comparaison de longueur d'exécution. La méthode à deux points élimine la complexité et protège contre les bugs subtils. *

Au cours des entretiens, l'intervieweur vous demandera d'expliquer la règle 3. Lorsque vous pouvez l'articuler clairement et présenter la solution à deux points, vous allez non seulement résoudre le problème, mais aussi présenter l'élégance algorithmique**.

---

Conclusion

LeetCode 809 est plus qu'un puzzle à cordes, c'est un **test de précision**. En maîtrisant l'approche à deux points dans **Java, Python et C++**, vous êtes prêt à impressionner les gestionnaires d'embauche et à démontrer l'état d'esprit **de préparation** qu'ils ont après.

Bon codage, et bonne chance d'obtenir cette prochaine entrevue de travail! C'est ce qu'il a dit.

---

* Fin de l'article. *

---

> *Sentez-vous libre pour modifier la liste de contrôle --Testing et ajouter plus de cases bord. La clé est de démontrer la rigueur, la clarté et un algorithme poli. *