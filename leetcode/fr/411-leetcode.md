---
titre: LeetCode 411. Abréviation de mot unique minimum - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 411. Abréviation de mot unique minimum
*Problème de LeetCode à 1 an*
<https://leetcode.com/problèmes/minimum-unique-word-abréviation/>

> **Objectif** – Avec une chaîne `target` et une liste de mots `dictionary`, trouvez l'abréviation *short* de `target` qui ** ne peut** être une abréviation de **any** mot dans le dictionnaire.
> Une abréviation peut remplacer *toute* sous-chaîne non adjacente par leur longueur.

---

### TL;DR
Le problème se résume à un ensemble classique de *hitting* sur au plus 21 positions (parce que `cible.longueur ≤ 21`).
Nous énumérons tous les masques possibles, le testons contre tous les mots du dictionnaire, et choisissons celui avec la plus petite longueur d'abréviation.

- **Java** – ~140 lignes
- **Python** – ~100 lignes
- **C++** – ~120 lignes

Les trois solutions fonctionnent confortablement sous 10 ms pour les limites de LeetCode.

---

- Oui. 1. L ' Algorithme (en anglais)

Étape Ce qu'il fait Pourquoi il importe
-- -- -- -- -- -- -- -- -- -- -- --
Autres **1. Filtrer le dictionnaire**. Seuls ces mots peuvent partager la même abréviation. Autres
**2. Calculer les masques de différence**. Pour chaque mot de ce genre, un bitmask `diff` où bit `i` est défini si `target[i] "diff" nous dit *où* le mot diffère de la cible. Autres
Chaque masque `m` (0 bits à base de) représente l'ensemble des positions que nous *maintenons* (c'est-à-dire non abrégées). Autres Le nombre de masques possibles est de <2^len(cible)>, ≤2^21,2 millions. Autres
Pour chaque mot du dictionnaire, vérifiez `m & diff != 0 '.. ► Garantie qu'au moins une position maintenue diffère, de sorte que l'abréviation ne peut correspondre à ce mot. Autres
**5. Calculer la longueur de l'abréviation**. La fonction objective. Autres
**6. Construisez la chaîne d'abréviations**. Transforme le meilleur masque en la corde requise. Autres

Parce que l'espace de recherche est minuscule (2 millions de dollars), un dénombrement de force brute est à la fois simple ** et** rapide.

---

- Oui. 2. Code

#### 2.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
public Chaîne minAbréviation(Cible de String, dictionnaire String[]) {
int m = longueur cible();
// 1. ne garder que des mots de même longueur
Liste <Integer> diffs = nouvelle liste de distribution<>();
pour (String w : dictionnaire) {
si (w.longueur() != m) poursuivre;
masque int = 0;
pour (int i = 0; i < m; i++) {
si (cible.charAt(i) != w.charAt(i))
masque= 1 << i;
}
diffs.add(masque);
}
// Si aucun mot concurrent → remplacer tout simplement
si (diffs.isEmpty()) retourne String.valueOf(m);

Int bestMask = 0;
int mieux Len = entier.MAX_VALUE;

// 3. énumérer tous les masques
= 1 << m;
pour (int masque = 0; masque < total; masque++) {
// 4. doit frapper chaque diff
booléen ok = vrai;
pour (int diff : diffs) {
si ((mask & diff)) == 0) { ok = faux; casse; }
}
Si (!ok) continue;

// 5. calcul de la longueur de l'abréviation
Int len = 0;
i = 0;
pendant que (i < m) {
si ((masque & (1 << i)) != 0) { // conserver cet omble
len++;
i++;
} autre { // commencer une série d'abréviations
j = i;
pendant que (j < m && (masque & (1 < < j))) == 0) j++;
len++; // un numéro pour l'exécution
i = j;
}
}
si (len < bestLen) {
bestLen = len;
le meilleur Masque = masque;
}
}

// 6. construire la chaîne à partir du meilleur Masque
StringBuilder sb = nouveau StringBuilder();
i = 0;
pendant que (i < m) {
si ((meilleurMask & (1 << i)) != 0) {
sb.append(target.charAt(i));
i++;
} autre {
j = i;
pendant que (j < m && (meilleure tâche & (1 << j))) == 0) j++;
sb.append(j - i);
i = j;
}
}
retour sb.toString();
}
}
«» "

---

2.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def minAbréviation(self, cible: str, dictionnaire: List[str]) -> str:
m = len(cible)
# Gardez seulement des mots de même longueur
diffs = []
pour w dans le dictionnaire:
si len(w) != m:
poursuivre
masque = 0
pour i, c, d) dans le dénombrement(zip(cible, w)):
si c != d:
masque = 1 << i
diffs.append(masque)

si non diffs:
retour str(m) # tout remplacé

best_mask, best_len = 0, flotteur('inf')
Total = 1 << m

pour masque à portée(total):
# frappe tous les diffs
if any((mask & diff)) == 0 pour diff dans diffs:
poursuivre

# longueur de l'abréviation
La valeur de la valeur de référence est égale à la valeur de référence.
alors que i < m:
si masque & (1 << i):
cur_len += 1
i += 1
Sinon:
j = i
alors que j < m et non (masque et (1 < < j)):
j += 1
cur_len += 1 # un nombre pour l'exécution
i = j
si cur_len < best_len:
best_len, best_mask = cur_len, masque

# résultat de construction
res = []
i = 0
alors que i < m:
si best_mask & (1 << i):
res.append(cible[i])
i += 1
Sinon:
j = i
alors que j < m et non (meilleure_masque & (1 << j)):
j += 1
Annexe(str(j - i))
i = j
retour ''.join(res)
«» "

---

#### 2.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne minAbréviation(cible de chaîne, dictionnaire vector<string>) {
int m = cible.size();
vecteur<int> diffs;
pour (auto &w : dictionnaire) {
si ((int)w.size() != m) poursuivre;
masque int = 0;
pour (int i = 0; i < m; ++i)
si (cible[i] != w[i]) masque=1 << i;
diffs.push_back(masque);
}
si (diffs.vide()) retourne à_string(m);

bestMask = 0, bestLen = INT_MAX;
= 1 << m;
pour (int masque = 0; masque < total; ++masque) {
bool ok = true;
pour (int diff : diffs) {
si ((mask & diff)) == 0) { ok = faux; casse; }
}
Si (!ok) continue;

i = 0;
pendant que (i < m) {
Si (masque & (1 << i)) { len++; ++i; }
autres {
j = i;
pendant que (j < m & & ! (masque & (1 < < j))) ++j;
len++; // un numéro
i = j;
}
}
si (len < bestLen) { bestLen = len; best Masque = masque; }
}

la chaîne rés;
i = 0;
pendant que (i < m) {
si (meilleurMask & (1 << i)) { res.push_back(target[i]); ++i; }
autres {
j = i;
pendant que (j < m & & ! (meilleure tâche & (1 << j))) ++j;
res += to_string(j - i);
i = j;
}
}
retour rés;
}
};
«» "

---

- Oui. 3. Billet de blog – Le bon, le mauvais, et l'acharnement du mot minimum unique Abréviation

> **SEO Mots-clés:** LeetCode 411, Abréviation de mot minimum Unique, algorithme d'entretien, Java, Python, C++, bitmask, frapper ensemble, abréviation la plus courte, conseils d'entretien d'emploi, entretien d'ingénieur logiciel.

---

3.1 Ce qui fait Ce problème
**Bien:**

1. **Small Search Space** – `target.longueur ≤ 21`.
Même une force brute complète sur tous les masques de 2^m court en millisecondes.

2. **Codage élégant de bitmask** –
Un entier capture l'ensemble du choix d'entretien/abbreviate, permettant des essais d'intersection O(1).

3. ** Saveur combinatoire pure** –
La solution est essentiellement un problème *hitting set*, un classique qui interviewe l'amour.

4. **Language‐Indépendant** –
La même logique fonctionne en Java, Python ou C++; idéal pour les interviews en plusieurs langues.

---

### 3.2 Où il obtient Tricky
**Balance:**

1. **Comprendre la longueur des abréviations** –
Le coût n'est pas seulement `#kept`.
Vous devez aussi compter des groupes de caractères omis consécutifs.
Beaucoup de candidats ont mal calculé cela et produisent une mauvaise réponse.

2. **Cas d'urgence** –
* Pas de mots de dictionnaire → réponse est simplement `m`.
* Mots de dictionnaire de différentes longueurs → ils sont hors de propos.

3. **Pièges de rendement** –
L'utilisation d'un constructeur naïf `String` à l'intérieur du dénombrement peut faire des ballons.
S'en tenir aux contrôles bitwise et aux boucles entières.

4. **Bruit de mise en œuvre** –
La conversion d'un masque en une chaîne de caractères nécessite un comptage attentif.

---

3.3 L'Ugly – Sur-Ingénierie?
Certaines solutions plongent dans le *backtracking avec taille*, *branche-et-bound* ou *bit DP*.
Tout en étant élégants, ils :

- Ajouter ~200 lignes de code pour seulement un gain de vitesse de 1 %.
- C'est plus difficile à vérifier dans un cadre d'entrevue.
- Peut masquer le simple noyau de force brute qui satisfait réellement les contraintes.

**Ligne de bottom:** * Restez simple. *
Afficher l'idée bitmask, calculer les masques `diff`, énumérer, choisir le meilleur, et construire la chaîne.

---

3.4 Comment agir Ceci dans une interview

1. **Exposer l'analogie de l'ensemble de frappe** –
Nous devons choisir des positions qui diffèrent de chaque mauvais mot. (en milliers de dollars)

2. **Afficher le code du masque** –
Un bit par personnage – idéal pour les opérations rapides ET. (en milliers de dollars)

3. **Dériver la formule de longueur** –
`len = #kept + #runs_of_zero`.
Écrivez-le ou dessinez-le.

4. ** Liste de contrôle des dossiers d'urgence** –
* Dictionnaire vide.
* Mots de différentes longueurs.
* Longueur cible 1 ou 21.

5. **Parler de la complexité** –
`O( 2^m * n )` pour les contrôles de masque + `O( 2^m * m )` pour les calculs de longueur.
Avec `m ≤ 21`, il s'agit d'environ 2 millions d'opérations – trivial.

6. **Envelopper avec une mise en œuvre courte** –
Choisissez la langue de votre choix; montrez un squelette de fonction succinct.

---

3.5 Mot final – Pourquoi cela compte pour votre prochain travail

LeetCode 411 teste votre vitesse de codage* et votre clarté conceptuelle*.
Résoudre cela démontre clairement:

- **La pensée algorithmique** – l'abstraction aux bitmasks.
- **Codage Discipline** – boucles efficaces sur la concaténation des cordes.
- **Communication** – expliquant une fonction de coût non évidente.

Lorsque vous vous retirez d'une entrevue avec ce problème résolu, vous aurez gagné *les deux* le coche vert sur le tableau et quelques points supplémentaires pour la clarté. Bonne chance pour votre prochain entretien !

---


---

**Profitez du codage dans les langues et rock que LeetCode 411!**