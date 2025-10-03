---
titre: LeetCode 2564. Sous-chaînes de requêtes XOR -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Sous-chaînes de questions XOR – LeetCode 2564
*Maîtrisez l'astuce bit-wise, écrivez du code propre en Java, Python et C++, et obtenez le blog prêt à écrire qui est SEO-friendly pour les recruteurs. *

---

- Oui. 1. Récapitulation des problèmes

Autres Quoi ? Pourquoi ?
- Oui.
*Input**= Chaîne binaire `s` (= 104) et `queries[i] = [firsti, secondi]` (= 105)=
Autres Pour chaque requête, trouvez la sous-chaîne *short* de `s` dont la valeur décimale `val` satisfait `val ^ firsti== secondi`.
**Extrait**= `[lefti, righti]` (0-based) ou `[-1,-1]` si aucune sous-chaîne n'existe. Si plusieurs réponses, choisissez celle avec la plus petite `lefti`. Autres

> **Pourquoi est-ce dur pour les recruteurs ? **
> Il teste l'algèbre bit-wise, préfixe des astuces, et une bonne compréhension des compromis entre l'espace et l'espace.

---

- Oui. 2. Le point de vue fondamental

1. `val ^ premier] seconde → val = première ^ seconde "
Chaque requête se résume donc à *=find une sous-chaîne avec la valeur décimale `target = first ^second`.

2. La chaîne binaire a au maximum **30** bits qui peuvent être représentés par un entier 32 bits.
→ Pour chaque position de départ, il suffit d'examiner au maximum les 30 caractères suivants.
Ceci maintient le prétraitement O(n · 30).

3. Nous n'avons besoin que de l'occurrence *premier* (le plus gauche) de chaque valeur.
→ Conservez une seule paire `[start, fin]` par valeur dans une carte de hachage.

4. **Leading zéros** – une sous-chaîne qui commence par `0` et est plus longue que 1 a une valeur de 0.
Nous le traitons comme un seul cas spécial: nous stockons `[i,i]` pour la valeur 0 une fois, puis sautons plus longtemps sous-chaînes de 0...0.

---

- Oui. 3. Algorithme

«» "
préprocessus:
carte = {}
pour l dans 0 ... n-1:
si s[l] == «0»:
map.setdefault(0, (l,l))
poursuivre
Valeur = 0
pour r dans l ... min(n-1, l+29):
val = (val << 1)) (s[r] - '0')
carte.setdefault(val, (l,r))

réponse(demandes):
res = []
pour la première, la deuxième dans les requêtes:
objectif = premier ^ deuxième
si cible dans la carte:
res.append(map[target])
Sinon:
res.appendice((-1,-1))
retour res
«» "

*Temps* = O(n · 30 + q)*Espace* = O(n · 30) (c'est-à-dire dans le pire des cas, 3 × 105 entrées).

---

- Oui. 4. Mise en œuvre des références

#### 4.1 Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe {
public int[][] substringXorQueries(String s, int[][] requêtes) {
Carte<entier, int[]> mp = nouveau HashMap<>();
int n = s.longueur();

pour (int l = 0; l < n; l++) {
si (s.charAt(l) == '0') { // seule la valeur 0 est valide
mp.putIfAbsent(0, nouvelle int[]{l, l});
poursuivre;
}
Int val = 0;
pour (int r = l; r < n && r - l < 30; r++) {
val = (val << 1)) (s.charAt(r) - '0');
mp.putIfAbsent(val, nouvelle int[]{l, r});
}
}

int[] [] ans = nouvelle int[queries.longueur][2];
pour (int i = 0; i < requêtes.longueur; i++) {
la cible int = requêtes[i][0] ^ requêtes[i][1];
int[] paire = mp.getOrDefault(cible, nouvelle int[]{-1, -1});
ans[i][0] = paire[0];
ans[i][1] = paire[1];
}
le retour des an;
}
}
«» "

4.2 Python 3

'`python
Solution de classe:
def substring XorQueries(self, s: str, requêtes: List[List[int]]) -> Liste[Liste[int]]:
mp = {}
n = len(s)

pour l dans la plage(n):
si s[l] == «0»:
mp.setdefault(0, (l, l))
poursuivre
Valeur = 0
pour r dans la plage(l, min(n, l + 30):
val = (val << 1)
mp.setdefault(val, (l, r))

res = []
pour la première, la deuxième dans les requêtes:
objectif = premier ^ deuxième
res.append(list(mp.get(target, (-1, -1)))
retour res
«» "

#### 4.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<vecteur<int>> sous-chaîne XorQueries(chaîne s, vecteur<vector<int>>&questions) {
sans ordre_map<int, paire<int,int>> mp;
int n = s.size();

pour (int l = 0; l < n; ++l) {
si (s[l] == '0') { // seule la valeur 0 est autorisée
mp.emplace(0, make_pair(l, l));
poursuivre;
}
Int val = 0;
pour (int r = l; r < n && r - l < 30; ++r) {
val = (val << 1)) (s[r] - '0');
mp.emplace(val, make_pair(l, r));
}
}

vecteur<vecteur<int>> ans;
as.reserve(queries.size());
pour (auto &q : requêtes) {
la cible int = q[0] ^ q[1];
auto it = mp.find(cible);
si (it != mp.end())
le nom et l'adresse de l'utilisateur;
Autre
le nom de l'entité ou de l'entité concernée;
}
le retour des an;
}
};
«» "

> **Note:** `emplace` avec `opérateur[]` se comporte comme `putIfAbsent` – il garde la paire *left-most*.

---

- Oui. 5. Écrire un blogue En haut

> **Description de la méta (= 155 caractères)* *
> *Solve LeetCode 2564 Substring XOR Queries in Java, Python & C++. Solution de hash-map 30 bits, conseils d'entrevue, trick bitwise & SEO-friendly guide pour les recruteurs. (en milliers de dollars)

---

## Sous-chaînes de questions XOR – Le guide de préparation à l'entrevue
*(Mots-clés du référencement: **Sous-chaîne de questions XOR**, **LeetCode 2564**, **chaîne binaire XOR**, **solution hashmap**, **problème d'entrevuebitwise***

Table des matières
1. Le problème
2. Le point de vue gagnant
3. Pourquoi c'est un recruteur préféré
4. Algorithme détaillé et complexité
5. Code de référence (Java / Python / C++)
6. Bonne, mauvaise et mauvaise – Un critique Prenez
7. Comment encadrer ce problème dans une reprise/une entrevue
8. FAQs et dossiers de bord

---

C'est vrai. 1. Quel est le problème

LeetCode 2564 vous demande de ** chercher une valeur décimale à l'intérieur d'une chaîne binaire** qui satisfait une simple équation XOR.
C'est un classique *bit-wise algebra* + *hash-map* problème que beaucoup d'intervieweurs aiment jeter sur les candidats.

> **Traitement des clés:**
> Convertissez chaque requête en une seule cible entière* (`first ^ second`) et demandez-lui ensuite: "Les `s` contiennent-ils une sous-chaîne avec cette valeur? (en milliers de dollars)

---

C'est vrai. 2. Le point de vue gagnant

Répercussions pratiques
Il n'y a pas de lien entre les deux.
Chaque requête est un **lookup** – pas besoin d'examiner la chaîne au moment de la requête. Autres
Autres La valeur de la chaîne binaire s'adapte en **30 bits** , nous n'examinerons qu'au plus 30 caractères par début → **O(n · 30)** prétraitement. Autres
Autres Seulement le **premier** (left-most) occurrence matters. Autres
**Les zéros de fuite** produisent la valeur Poignée comme un cas spécial → éviter les entrées exponentielles dupliquées. Autres

---

C'est vrai. 3. Pourquoi les recruteurs aiment ce problème

Compétence testée Pourquoi ça compte
C'est pas vrai.
Autres Beaucoup de rôles de bas niveau (encastrés, systèmes) nécessitent une bonne compréhension de XOR, ET, OU. Autres
Démonstration de la capacité de transformer un scan O(n2) naïf en O(n). Autres
Hash‐map space‐time trade‐off (en anglais seulement) Shows on peut penser dans *O(1) amortized* lookups, un concept CS de base. Autres
Nettoyez l'implémentation Java/Python/C++.Vous pouvez coder en plusieurs langues – un plus pour les positions complètes. Autres

---

C'est vrai. 4. La solution "Good" – Ce qui fait sortir cette solution

1. **Linear + Constante** – `O(n · 30 + q)` est essentiellement linéaire dans la taille de l'entrée, ce qui est le meilleur que vous pouvez espérer sur cette échelle.
2. **Simplicité** – L'idée centrale est un seul passage qui construit une carte; la phase de requête n'est qu'une recherche de dictionnaire.
3. **Réponse déterministe** – La carte stocke automatiquement l'événement le plus à gauche, satisfaisant à l'exigence de gauche la plus petite.
4. **Language-agnostique** – Fonctionne exactement comme en Java, Python, C++ – idéal pour montrer la polyvalence.

---

C'est vrai. 5. L'Énorme – Où la solution peut s'arrêter

Sujet Impact Atténuation
C'est quoi ?
**Taille de la carte** – Jusqu'à ~3 × 105 entrées. Autres
**30-char limit** – Hard-coded for 32-bit ints. Autres
**Leading zéro handling**= Nécessite une branche minuscule mais essentielle. Autres

---

C'est vrai. 6. L'Ugly – Les choses qui se sentent ridiculisées

1. **Valeur 0 vs. Il semble contre-intuitif qu'une plus longue chaîne de zéros égale encore 0.
2. **Dupliquer les valeurs** – Deux sous-chaînes différentes peuvent produire la même valeur entière ; vous devez garantir le *left‐most* un gagne.
3. **Off‐par‐un dans la fenêtre 30‐char** – La boucle utilise `r - l < 30`, qui est subtile mais cruciale pour rester dans les limites de 32 bits.
4. **Hash-map collision** – En C++ `unordered_map` peut être sensible au taux de frappe; réservez un grand nombre de godets (`reserv(n*30)`) pour conserver l'amortissement O(1).

---

C'est vrai. 7. Comment présenter Cela dans un CV / Interview

Section Que dire
C'est pas vrai.
**Déclaration du problème** 2564 – Sous-chaînes de requêtes XOR – chaîne binaire + requêtes 100k. Autres
**Approach**==Réduit chaque requête à une seule recherche entière via `cible = première ^ seconde`. Précalculé la sous-chaîne la plus courte pour chaque valeur possible à l'aide d'une carte de hachage et examiné seulement les 30 caractères suivants par début. Autres
**Complexité** Autres
**Profession linguistique** Autres
**Result**="Accepté sur LeetCode en < 0,2 s pour tous les cas de test; parfait pour les rôles critiques de performance. Autres

---

C'est vrai. 8. FAQ

C'est ce qu'il a dit.
-- -- -- -- -- --
*Pourquoi 30, pas 32?*= Parce qu'un int signé 32 bits peut représenter des valeurs allant jusqu'à 231-1. Le problème garantit "la première ^ seconde ≤ 109 < 230". Autres
*Qu'en est-il des zéros de tête? * Une sous-chaîne qui commence par `0` et a de la longueur > 1 est toujours 0. On ne stocke qu'une seule fois le caractère zéro. Autres
*Pouvons-nous utiliser un tableau préfixe-somme à la place?*= Oui, mais il faudrait encore une carte de toutes les valeurs de 30 bits possibles. Le laminage direct est plus simple et plus rapide. Autres
*Et si `s` est plus long que 104? * L'algorithme fonctionne encore, mais dépasserait les limites de temps/espace. Dans ce cas, vous auriez besoin d'un bit-set / tri plus sophistiqué. Autres

---

- Oui. 9. Réflexions finales

- **Bonne** – O(1) recherche amortie, mathématiques claires, prétraitement à temps constant.
- **Bad** – Environ 3 × 105 entrées de carte; mémoire-lourde pour les très grandes cordes.
- **Ugly** – La quirk leader-zéro , force une branche spéciale qui est facile à manquer.

En maîtrisant ce problème, vous impressionnerez les recruteurs qui s'intéressent aux opérations **bit-wise**, aux astuces **hash-map** et au code **clean** dans plusieurs langues.

Bon codage – et bonne chance d'obtenir cette entrevue!