---
titre: LeetCode 2950. Nombre de sous-chaînes divisibles
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2950 – Nombre de sous-chaînes divisibles
**Type de problème:** Moyenne
**Délai:** 2 s
**Limite de l'espace:** 256 Mo

---

- Oui. 1. Exposé des problèmes

> Chaque lettre anglaise minuscule est cartographiée à un chiffre (voir le tableau ci-dessous).
> Un **substring** d'une chaîne est toute séquence contiguë et non vide de caractères.
> Une sous-chaîne est **divisible** si la somme des valeurs cartographiées de ses caractères est divisible par sa longueur.
> Compte tenu d'une chaîne `word` (1 ≤="word ≤ 2000), retourner le nombre de sous-chaînes divisibles de `word`.

Valeur de la lettre
C'est pas vrai.
A, b, 1
C, d, e
F, g, h
I, J, K
L, m, n
o, p, q
R, s, t
U, v, w
x, y, z

*Exemples*

"Mot" réponse
C'est quoi ?
Voir la table de l'échantillon dans l'énoncé du problème.
"bdh" , "d" , "h" , "bdh"
"abcd" 6" "a"`, "b"`, "c"`, "d"`, "ab"`, "cd"

---

- Oui. 2. Intuition – Moyenne = entier

Pour une sous-chaîne de longueur `p`, ses valeurs mapées sont `f(c1)...f(cp)`.
La sous-chaîne est divisible iff

«» "
F(c1)+f(c2)+...+f(cp)
C'est un entier
p
«» "

La valeur moyenne ** de la sous-chaîne doit donc être un entier compris entre 1 et 9.

Si nous fixons une moyenne `a` (1 ≤ a ≤ 9) nous pouvons demander: *Combien de sous-chaînes ont la moyenne exactement `a`? *

Pour une "a" donnée

«» "
f(c1)+...+f(cp) = p · a
(f(c1)-a) + ... + (f(cp)-a) = 0
«» "

Le problème se réduit donc à compter les sous-groupes dont la somme **transformée est zéro**.
Cela peut être fait en temps linéaire avec un truc préfixe + hash-map.

Parce qu'il n'y a que 9 moyennes possibles, nous répétons simplement le scan linéaire 9 fois – **O(9 · n)** globalement.

---

- Oui. 3. Algorithme (étapes précises)

1. **Précalculer la cartographie**
`int val[26] = {1,1,2,2,2,3,3,4,4,5,5,5,6,6,6,7,7,8,8,8,9,9};`

2. **Réponse = 0**

3. Pour chaque `a` de 1 à 9
* `diff[i] = val[word[i]-'a'] - a` (valeur transformée)
* Calculer la somme du préfixe de `diff` et stocker chaque préfixe dans une carte de hachage
(«préfixe[sum]» = combien de fois cette somme est apparue jusqu'à présent).
* Chaque fois que le préfixe actuel `s` est revu, tous les sous-tarifs entre les deux positions ont la somme 0 → ils ont tous la moyenne `a`.
* Augmentation de la réponse par le nombre de paires de sommes préfixes égales.

4. Retourne la réponse.

---

- Oui. 3. Pseudocode

«» "
ans = 0
pour a au 1..9:
carte = carte de hachage vide // clé = somme préfixe, valeur = fréquence
carte[0] = 1 // préfixe vide
pour = 0
pour chaque caractère ch en mot:
cur += valeur[ch] - a
ans += map.getOrDefault(cur, 0)
map[cur] = map.getOrDefault(cur, 0) + 1
retour et
«» "

---

- Oui. 4. Analyse de la complexité

Commentaire Expression Résultat
C'est pas vrai.
Durée: 9 ·=mot: **O(9 · n)** (=18 000 opérations pour le pire des cas `n = 2000') Autres
Mémoire Taille de la carte de l'hash (la carte est recréée 9 fois, mais chaque copie est immédiatement supprimée)

Les deux limites sont facilement respectées pour les contraintes données.

---

- Oui. 5. Mise en œuvre des références

> Les solutions suivantes suivent exactement la même logique et peuvent être collées directement dans l'onglet LeetCode.

---

##### 5.1 Java

"Java
solution de classe {
// 1-based mapping for 'a'..'z '
finale statique privée MAP = {
1, 1, 2, 2, 3, 3, 3, 4, 4, 4,
5, 5, 5, 6, 6, 7, 7, 7, 8, 8, 9, 9, 9
};

public long divisible Sous-chaînes (mot d'ordre) {
long ans = 0;
int n = mot.longueur();

pour (int avg = 1; avg <= 9; avg++) {
// préfixe sum hash map
HashMap<entier, entier> prefCnt = nouveau HashMap<>();
prefCnt.put(0, 1); // préfixe vide

Int cur = 0;
pour (int i = 0; i < n; i++) {
Int val = MAP[word.charAt(i) - 'a'];
cur += val - avg; // transformer en valeur - avg
ans += prefCnt.getOrDefault(cur, 0);
prefCnt.put(cur, prefCnt.getOrDefault(cur, 0) + 1);
}
}
le retour des an;
}
}
«» "

---

5.2 Python

'`python
Solution de classe:
# table de correspondance: 0 → a, 1 → b, 2 → c, etc.
_MAP = [
1, 1, 2, 2, 3, 3, 3, 4, 4, 4,
5, 5, 5, 6, 6, 7, 7, 7, 8, 8, 9, 9, 9
- Oui.

def divisible Sous-chaînes (même, mot: str) -> Int:
ans = 0
n = len(mot)

pour avg dans la gamme(1, 10):
pref = {0: 1}
pour = 0
pour ch en mot:
cur += self._MAP[ord(ch) - 97] - avg
ans += pref.get(cur, 0)
pref[cur] = pref.get(cur, 0) + 1
retour et
«» "

---

C++

'`cpp
solution de classe {
public:
long divisibleSous-chaînes(mot chaîne) {
statique const int MAP[26] = {
1, 1, 2, 2, 3, 3, 3, 4, 4, 4,
5, 5, 5, 6, 6, 7, 7, 7, 8, 8, 9, 9, 9
};

long an = 0;
int n = mot.size();

pour (int avg = 1; avg <= 9; ++avg) {
unordered_map<int, int> prefCnt;
préfCnt.reserve(n + 1);
prefCnt[0] = 1; // préfixe vide
Int cur = 0;
pour (char ch : mot) {
cur += MAP[ch - 'a'] - avg;
as += prefCnt[cur];
++préfCnt[cur];
}
}
le retour des an;
}
};
«» "

---

## Comment résoudre le Leetcode 2950: Nombre de sous-chaînes divisibles

> **Cible auprès du public:** LeetCode passionnés, intervieweurs, data-structure et étudiants en algorithme
> * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

---

- Oui. 1. Pourquoi le nombre de sous-chaînes divisibles

Le nom lui-même suggère que nous devons penser à **divisibilité** et **sous-chaînes**.
Si vous ignorez la correspondance lettre-à-chiffre et que vous forcez simplement toutes les sous-chaînes `O(n2)`, vous atteindrez la limite de temps.
La vraie astuce est de reconnaître que la *moyenne* des valeurs cartographiées doit être un **entier** (1–9).

---

- Oui. 2. La moyenne = entier

1. **Moyenne = entier** – pour une sous-chaîne de longueur `p`

«» "
(somme des valeurs cartographiées) / p doit être un entier
«» "

2. **Fixer une moyenne «a»** (1-9) et demander
Combien de sous-chaînes ont cette moyenne exacte ?

3. **Transformer le tableau**
Pour chaque position `i` calcule `value[i] - a`.
Maintenant une sous-chaîne a la moyenne `a` **iff** la somme transformée sur cette sous-chaîne est **zero**.

4. **Couvercle de la somme zéro**
Un préfixe classique + un plan de hachage :
Texte
pref[0] = 0
pour chaque i:
pref[i+1] = pref[i] + diff[i]
n'importe quelle paire (l,r) avec pref[l] == pref[r] = somme de diff[l.r-1] == 0
«» "

5. ** Repose les 9 moyennes** – complexité totale "O(9 · n)".

---

- Oui. 3. Pourquoi cela bat la solution O(n2) naïve

Démarche Temps Raison
- C'est quoi ?
Brute-force (O(n2)) 20002 4 millions de contrôles – toujours bien, mais la constante est élevée. Autres
"Préfixe-somme + tour moyen" O(9 · n)" 9 × 2000 = 18 000 opérations – presque négligeable. Autres
Un seul hash-map par moyenne. Autres

Le test-suite LeetCode est généreux, mais les intervieweurs aiment les solutions qui fonctionnent dans le temps linéaire après un petit facteur constant.

---

- Oui. 4. Détails de la mise en œuvre

Tableau de cartographie

Le problème définit une cartographie non alphabétique:

«» "
A,b → 1
c,d,e → 2
f,g,h → 3
i,j,k → 4
L,m,n → 5
o,p,q → 6
r,s,t → 7
Nombre d'unités
x,y,z → 9
«» "

La plupart des solutions précréent un tableau de longueur 26 de sorte que `value[ch - 'a']` fonctionne en O(1).

4.2 Extraits de code

Voici des implémentations propres et prêtes à la production dans les trois langues les plus courantes.

---

###### 4.2.1 Java

> Utilise un `HashMap<Integer, Integer>` pour les fréquences préfixes.

"Java
solution de classe {
finale statique privée MAP = { /* 26 éléments;

public long divisible Sous-chaînes (mot d'ordre) {
long ans = 0;
int n = mot.longueur();

pour (int avg = 1; avg <= 9; avg++) {
HashMap<entier, entier> prefCnt = nouveau HashMap<>();
cfCnt.put(0, 1);
Int cur = 0;
pour (int i = 0; i < n; i++) {
cur += MAP[word.charAt(i) - 'a'] - avg;
ans += prefCnt.getOrDefault(cur, 0);
prefCnt.put(cur, prefCnt.getOrDefault(cur, 0) + 1);
}
}
le retour des an;
}
}
«» "

4.2.2 Python

> Utilise un dictionnaire pour les fréquences préfixes.

'`python
Solution de classe:
_MAP = [1,1,2,2,3,3,3,4,4,5,5,5,6,6,6,7,8,8,9,9]

def divisible Sous-chaînes (même, mot: str) -> Int:
ans = 0
pour avg dans la gamme(1, 10):
pref = {0: 1}
pour = 0
pour ch en mot:
cur += self._MAP[ord(ch)-97] - avg
ans += pref.get(cur, 0)
pref[cur] = pref.get(cur, 0) + 1
retour et
«» "

* ##### 4.2.3 C++

> Utilise `unordered_map` avec `reserve` pour éviter le rechapage.

'`cpp
solution de classe {
public:
long divisibleSous-chaînes(mot chaîne) {
MAP de const. statique[26] = { /* 26-élément mapping */ };
long an = 0;
int n = mot.size();

pour (int avg = 1; avg <= 9; ++avg) {
unordered_map<int,int> prefCnt;
préfCnt.reserve(n+1);
1 = 1;
Int cur = 0;
pour (char ch : mot) {
pour += MAP[ch-'a'] - avg;
as += prefCnt[cur];
++préfCnt[cur];
}
}
le retour des an;
}
};
«» "

---

- Oui. 5. Tester votre solution

1. **Cas d'Edge**: `"aaaa"` - toutes les valeurs sont 1, donc chaque sous-chaîne a une moyenne 1 → réponse = `n*(n+1)/2`.
2. ** Chaînes de random** – générer `mot' de longueur 2000, vérifier la justesse du solveur de la force brute O(n2).
3. **Test de résistance** – exécuter de nombreux cas aléatoires pour éviter tout débordement (la réponse correspond à "long long`/`long`).

---

- Oui. 6. A emporter

- Reconnaître les contraintes cachées : la moyenne des chiffres cartographiés doit être un entier.
- Transformez le problème en comptage **subarrays de somme zéro** – une technique classique.
- Gardez la cartographie comme tableau pour les recherches O(1).
- Répéter pour chacune des 9 moyennes possibles – globale linéaire.

Avec cet état d'esprit, vous allez résoudre LeetCode 2950 dans un flash et impressionner les intervieweurs avec un algorithme propre et efficace.

---

> *Bon code, et que votre prochaine interview soit une brise!* C'est ce qu'il a dit.

---



**Fin du guide. **