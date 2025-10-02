---
titre: LeetCode 1554. Les chaînes diffèrent par un seul caractère - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1554 – Différenciation des lignes par un seul personnage

> **TL;DR**
> Utilisez un hash *polynomial pour réduire chaque mot en un seul entier.
> Pour chaque position `i` supprimer la contribution du caractère `i` et vérifier si deux mots deviennent égaux.
> Temps = O(N·M), Espace = O(N).

---

Récapitulation des problèmes

«» "
Entrée : Chaîne[] dic (tous les mots de même longueur, unique, minuscule)
Sortie : true si deux mots diffèrent par exactement un caractère au même indice
faux sinon
«» "

Échantillon Sortie Explication
C'est quoi ?
["abcd", "aacd", "aacd"]]
["ab", "cd", "yz"]="false=" Aucune paire ne diffère par un caractère="
["abcd", "cccc", "abyd", "abab"]

Contraintes
* "Dictée ≤ 10^5"
* `len(word) = M ≤ 10` (parce que tous les mots sont de longueur égale)
* Chaque mot est unique et se compose uniquement de `a‐z`.

---

Algorithme – Hash polynomial + Set

1. **Pouvoirs précalculés**
`pow[i] = BASE^i mod MOD` pour `i = 0 ... M-1'.
`BASE = 257` (première prime > 256, fonctionne pour tous les ASCII)
`MOD = 1 000 000 007` (primaire large pour éviter les débordements)

2. **Cacher chaque mot**
`hash(w) = ↓ (w[j] * pow[j]) mod MOD`

3. **Pour chaque indice «i»**
*Créer un jeu de hachage frais* `seen`.
*Pour chaque mot* calculer `hashWithoutChar = (hash[w] – w[i]*pow[i]) mod MOD`
*Si `hashWithoutChar` déjà dans `seen` → deux mots diffèrent seulement à `i`* → retour `true`.
Sinon, ajoutez-le à "seen".

4. **Retour `faux`** si aucune paire n'a été trouvée.

> **Pourquoi ça marche* *
> Enlever la contribution d'un seul caractère du hachage polynôme donne le hachage de la sous-chaîne *remaining*.
> Si deux mots diffèrent seulement à la position `i`, leurs hachages « removed-char» sont identiques – nous le prenons dans le jeu.
> Les collisions sont astronomiquement improbables avec un entier 64 bits et un module 1e9+7.

---

Preuve d'exactitude

*Que `w1` et `w2` soient deux mots qui diffèrent uniquement à l'index `k`. *

- Oui. Leurs haches complètes ne diffèrent que par `Δ = (w1[k] - w2[k]) * pow[k]`.
- Enlever `k` des deux hachages donne `h1' = h1 - w1[k]*pow[k]` et `h2' = h2 - w2[k]*pow[k]`.
- Depuis `h2 = h1 + Δ`, nous avons
`h2' = h1 + Δ - w2[k]*pow[k] = h1 + (w1[k]-w2[k]*pow[k] - w2[k]*pow[k] = h1 - w1[k]*pow[k] = h1''.
Ainsi `h1' = h2'`.

À l'inverse, si deux mots « k » sont égaux à un indice, la seule différence entre les mots peut être à « k », car tous les autres caractères contribuent les mêmes montants aux deux hachages. Par conséquent, ils diffèrent par au plus un caractère; un caractère unique des mots lui garantit exactement un. *

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Pouvoirs précalculateurs
Calculer tous les hachages
Loop principal O(N·M) O(N) par itération (série)
**Total******

Avec `N ≤ 10^5` et `M ≤ 10`, cela fonctionne confortablement sous 1 seconde dans les trois langues.

---

Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
Chacun suit la même idée algorithmique et inclut des commentaires pour plus de clarté.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
public booléen diffèrentByOne(String[] dic) {
si (dicte) null dict.longueur < 2) retourner faux;
base finale = 257; // > 255
durée finale MOD = 1_000_000_007L; // 1e9+7
L = dict[0].longueur();

Pouvoirs précalculateurs
long[] pow = nouveau long[L];
pow[0] = 1;
pour (int i = 1; i < L; i++) {
pow[i] = (pow[i - 1] * BASE) % MOD;
}

// 2.
long[] haches = nouveau long[dict.long];
pour (int i = 0; i < dic.longueur; i++) {
longue h = 0;
Chaîne s = dict[i];
pour (int j = 0; j < L; j++) {
h = (h + s.charAt(j) * pow[j]) % MOD;
}
hashes[i] = h;
}

// 3
pour (int pos = 0; pos < L; pos++) {
Set<Long> vu = nouveau HashSet<>();
pour (int i = 0; i < dic.longueur; i++) {
longue sans = (hases[i] - dic[i].charAt(pos) * pow[pos]) % MOD;
si (sans < 0) sans += MOD; // garder positif
si (!seen.add(out)) retourne true; // duplicata → diffèrent par un
}
}
retourner faux;
}
}
«» "

---

Python

'`python
de taper l'importation Liste

Solution de classe:
Def differentByOne(self, dic: List[str]) -> bool:
s'il ne s'agit pas d'un dicton ou d'un len( dicton) < 2:
Retour Faux

BASE = 257
MOD = 1 000 000 007
L = len(dict[0])

# pouvoirs précalculés
pow = [1] * L
pour i dans la plage (1, L):
pow[i] = (pow[i - 1] * BASE) % MOD

# Des hachages pleins
haches = []
pour s in dict:
h = 0
pour j, ch dans le(s) énumérateur(s):
h = (h + ord(ch) * pow[j]) % MOD
Annexe(h)

# enlever un char par position
pour pos dans la plage (L):
vu = set()
pour i, s en énumération(dicte):
Sans = (hases[i] - ord(s[pos]) * pow[pos]) % MOD
si non vu:
retour Vrai
voir.add(sans)
Retour Faux
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool differentByOne(vecteur<string>& dic) {
si (dict.size() < 2) retourner faux;
longue BASE = 257;
longue MOD = 1'000'000'007LL;
int L = dict[0].size();

// 1. pouvoirs précalculateurs
vecteur <long> pow(L);
pow[0] = 1;
pour (int i = 1; i < L; ++i)
pow[i] = (pow[i-1] * BASE) % MOD;

// 2. hachage complet
vecteur <long> h(dict.size());
pour (size_t i = 0; i < dic.size(); ++i) {
long vail = 0;
pour (int j = 0; j < L; ++j)
val = (val + dic[i][j] * pow[j]) % MOD;
h[i] = valeur;
}

// 3. essayez de supprimer chaque position
pour (int pos = 0; pos < L; ++pos) {
_set non ordonné<long long> vu;
pour (size_t i = 0; i < dic.size(); ++i) {
longue durée sans = (h[i] - dict[i][pos] * pow[pos]) % MOD;
si (sans < 0) sans += MOD;
si (!seen.insert(sans).second) retourne vrai;
}
}
retourner faux;
}
};
«» "

> **Astuce** – Utilisez `uint64_t` (2^64) au lieu d'un module si vous voulez abandonner complètement l'opération `%`; la probabilité de collision est essentiellement zéro pour les contraintes données.

---

Pourquoi cet algorithme est-il l'interview-Ready

Pourquoi ça compte ?
- Oui.
**O(N·M)**
Autres **Pas de boucles imbriquées
**La preuve mathématique**
**Poignées négatives** Autres

** Liste de contrôle des entretiens**

1. ** Commencez par l'idée de force brute** – c'est facile à expliquer et généralement accepté au premier tour.
2. **Afficher que vous pouvez améliorer** – introduire le hachage polynôme, expliquant pourquoi il réduit une chaîne à un seul nombre.
3. **Risque de collision** – soyez honnête; personne ne peut garantir un hachage parfait, mais vous pouvez choisir un grand module ou un débordement de 64 bits pour le rendre négligeable.
4. **Découvrez le temps et l'espace** – les intervieweurs adorent voir les grands O découlant des contraintes.
5. **Parler de cas de bord** – liste vide, mots à une lettre, lettres toutes identiques, etc.

---

Bonne, mauvaise, mauvaise de la solution

Aspect du bien
- C'est quoi ?
**Bon*** *Temps linéaire*, fonctionne pour jusqu'à 105 mots, constante `M` garde la mémoire basse.
**Contrôles de hachage rares peuvent mal rapporter `false` → `true`.
La gestion de l'arithmétique modulaire en Java/C++ ('%' et valeurs négatives) peut être sujette à erreur. Éviter d'utiliser un arithmétique 64 bits non signé ou un langage qui s'enroule automatiquement ("long non signé" en C++).

> ** Conseil professionnel :** Si vous vous inquiétez des collisions dans un cadre de production, gardez une paire de hachages* (p. ex. deux modules différents) ou revenez à une étape de vérification lorsqu'un hachage en double est trouvé.

---

Essais et validation

Autres Test d'entrée prévu Résultat
C'est pas vrai.
Tableau vide
Autres Un seul mot "["a"] ""faux"
Autres Tous les mots identiques sauf un char : "["abcde", "abfde", "abgde"] ""true"
Autres Tous les mots diffèrent par 2 chars.
Taille maximale ('10^5') mots aléatoires

Générer des cas de test avec `random.sample` ou un générateur personnalisé pour être confiant.

---

Conseils d'entrevue

Sujet Que mentionner Pourquoi ça aide
- C'est quoi ?
**Conception de l'algorithme**= Commencez par une approche de force brute, puis identifiez la contrainte de caractère de l'algorithme → mène naturellement à l'idée de hachage. Affiche l'état d'esprit de résolution de problèmes. Autres
**Structures de données**= Utiliser un jeu de hachage pour détecter les duplicatas dans O(1). L'espace reste optimal. Autres
**Complexité** Quantifie l'efficacité. Autres
**Cas d'Edge**= Entrée vide, mot unique, longueur identique de tous les mots. Démontre la rigueur. Autres
**Manipulation de la collision** Montre la conscience des pièges du monde réel. Autres

---

Questions fréquemment posées

C'est ce qu'il a dit.
-- -- -- -- -- --
Autres **Puis-je utiliser une comparaison `String` après avoir retiré un char?** , mais ce serait O(N2·M) dans le pire des cas – inacceptable pour 105 mots. Autres
Autres **Et si M était plus grand (disons 1000)?**L'algorithme serait toujours O(N·M), mais 105·1000 est 108 opérations – limite. Une approche différente (en bit-masking ou en rolling hash) pourrait être nécessaire. Autres
En Java/Python/C++, nous utilisons 64 bits (`long`/`int64`) plus un module pour conserver les valeurs < MOD.
Autres **Pourquoi ne pas utiliser `unordered_set<string>` directement? Cela stockerait les chaînes complètes – la mémoire O(N·M) et les recherches plus lentes. Hashing compresse chaque corde à un entier, économisant de l'espace et du temps. Autres

---

Conclusion

Le tour de hachage polynôme transforme un problème apparemment lourd en une poignée d'opérations entières.
Avec seulement quelques lignes de code, vous satisfaire les contraintes, garder l'algorithme rapidement, et sont prêts à impressionner les intervieweurs.

> **Takeaway** – Quand on vous a demandé : Y a-t-il une paire qui diffère par un seul caractère ?
> Cet état d'esprit est exactement ce que de nombreuses entreprises technologiques recherchent : *les solutions intelligentes, efficaces et bien justifiées*.

Bon codage, et bonne chance pour votre prochaine interview! *