---
titre: LeetCode 2168. Sous-chaînes uniques avec une fréquence égale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Voici les solutions **prêtes à copier** pour LeetCode 2168 – *Unique Substrings with Equal Digit Fréquence* – écrit en **Java**, **Python** et **C++**.
Tous les trois suivent la même idée O(N2 · 10):
* énumérer toutes les sous-chaînes,
* maintenir un tableau de fréquences de 10 éléments tout en étendant la sous-chaîne,
* vérifier si chaque nombre non nul est égal,
* insérer la sous-chaîne dans un ensemble de hachage pour ne garder que des éléments uniques.

Texte
LeetCode 2168
Sous-chaînes uniques Avec une fréquence égale à un chiffre
Heure : O(N2 · 10)
Espace : O(N2) (ensemble de sous-chaînes uniques)
«» "

---

### Java – 100% Java 17

"Java
Importation de java.util.*;

solution de classe publique {
// Vérifier si tous les nombres non nuls sont les mêmes
booléen privé est Valid(int[] cnt) {
pivot int = -1;
pour (int i = 0; i < 10; i++) {
si (cnt[i]] 0) poursuivre;
si (pivot) -1) pivot = cnt[i];
sinon si (cnt[i] != pivot) retourner faux;
}
retour vrai;
}

État Fréquence numérique(String s) {
Set<String> unique = nouveau HashSet<>();
int n = s.longueur();

pour (int i = 0; i < n; i++) {
int[] cnt = nouvelle int[10];
StringBuilder cur = nouveau StringBuilder();

pour (int j = i; j < n; j++) {
int d = s.charAt(j) - '0';
cnt[d]++;

l'annexe(s.charAt(j));

si (isValid(cnt)) unique.add(cur.toString());
}
}
retour unique.size();
}
}
«» "

> **Conseil:** Le `StringBuilder` est réutilisé pour chaque `i`, donc nous évitons de construire une nouvelle chaîne pour chaque caractère.
> La méthode `isValid` ne scanne que 10 positions – des frais généraux négligeables.

---

### Python – 3.10+

'`python
de taper l'importation Liste, ensemble

Solution de classe:
def égal Fréquence des chiffres(self, s: str) -> Int:
n = len(s)
unique: Set[str] = set()

pour i dans la plage(n):
cnt = [0] * 10
cur = []

pour j dans la plage(i, n):
d = ord(s[j]) - 48
cnt[d] += 1
Annexe(s)

# Testez l'égalité de tous les nombres non nuls
pivot = Aucun
ok = Vrai
pour c en cnt:
si c == 0: continuer
si le pivot n'est pas:
pivot = c
elif c != pivot:
ok = Faux
pause
si oui:
unique.add('.join(cur))

retour len(unique)
«» "

> **Pourquoi une liste pour `cur`? **
> `''.join(cur)` est O(len(cur)), mais construire la liste une fois par `i` maintient la boucle intérieure linéaire.

---

### C++ – C++17 moderne

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool isValid(const array<int,10>& cnt) {
pivot int = -1;
pour (int c : cnt) {
si (c) 0) poursuivre;
si (pivot) -1) pivot = c;
sinon si (c != pivot) retourner faux;
}
retour vrai;
}

int égal Fréquence(chaîne s) {
unordered_set<string> uniq;
int n = s.size();

pour (int i = 0; i < n; ++i) {
tableau <int,10> cnt{}; // tous les zéros
chaîne de caractères cur;

pour (int j = i; j < n; ++j) {
int d = s[j] - '0';
++cnt[d];
cur.push_back(s[j]);

si (isValid(cnt)) uniq.insert(cur);
}
}
retourner static_cast<int>(uniq.size());
}
};
«» "

> **Pourquoi `unordered_set<string>`? * *
> Le hachage intégré est assez rapide pour ≤ 1 000 sous-chaînes.
> L'utilisation de `std::string` permet de lire le code; le coût de la copie est insignifiant pour les contraintes données.

---

- Oui. 2. Article de blog – Le bon, le mauvais, et l'indulgence de LeetCode 2168

> **Titre de la méta* *
> 2168 LeetCode: Des sous-chaînes uniques avec une fréquence égale – Java, Python & C++ Solutions
> **Description détaillée**
> Master LeetCode 2168 avec des solutions Java, Python et C++ propres. Apprenez l'algorithme, les pièges et comment impressionner les gestionnaires d'embauche avec votre style de codage.

---

Introduction

Lorsque les recruteurs vous demandent de résoudre *Unique Substrings with Equal Digit Fréquence* (LeetCode 2168), ils sont à la recherche de trois choses:

1. **Correctness** – l'algorithme trouve-t-il chaque sous-chaîne de qualification?
2. **Efficacité** – peut-elle gérer les entrées les plus mauvaises dans les délais?
3. **Clean code** – la solution est-elle lisible et durable?

Dans cet article, nous traversons le **good**, le **bad**, et les parties **ugly** des solutions typiques, nous montrons une mise en œuvre prête à la production en trois langues, et nous signalons des améliorations favorables à l'entrevue.

---

Récapitulation du problème

> **Input** – une chaîne `s` (longueur ≤ 1000) composée uniquement de chiffres décimaux.
> **Objectif** – compter **unique** sous-chaînes où *chaque chiffre qui apparaît* le fait **même nombre de fois**.

> **Exemples**
> **1212* → "{"1", "2", "12", "21", "1212"}" → réponse = 5
> *.12321* → 9 sous-chaînes uniques

La phrase clé est *= chaque chiffre qui apparaît. Les chiffres qui n'apparaissent pas du tout sont ignorés.

---

### Le bien – O(N2 · 10) Brute-Force avec validation précoce

Parce que `s.longueur ≤ 1000`, un algorithme quadratique est acceptable. L'astuce est d'éviter de scanner** la sous-chaîne sur chaque extension :

1. Pour chaque index de démarrage `i`, initialisez un tableau de fréquences de 10 éléments `cnt` et un fichier vide `StringBuilder` (Java) / list (Python) / string (C++).
2. Développez la sous-chaîne un caractère à la fois (`j` de `i` à `n-1`), mettant à jour `cnt` et la chaîne actuelle.
3. Après chaque extension, lancez `isValid(cnt)` – un seul passage sur 10 éléments – pour vérifier que toutes les fréquences non nulles sont égales.
4. Si valide, insérer la sous-chaîne dans un ensemble de hachage pour conserver l'unicité.

**Pourquoi est-ce bon? **

- **Linéaire par sous-chaîne** – la boucle interne fonctionne O(1) (10 étapes).
- **Pas de copie de chaîne lourde** – nous conservons une chaîne en cours d'exécution et matérialisons seulement la clé pour le jeu au besoin.
- **Simple, code idiomatique** – facile pour les recruteurs à lire et à raisonner.

---

- Oui. L'Éclat – Structures de hachage, de trie ou de données supplémentaires

Certaines solutions sur LeetCode ajoutent de la complexité pour peu de gain:

Pourquoi ? Autres
- C'est quoi ?
Whash à roulettes + file d'attente à double extrémité Le hachage devrait représenter 10 compteurs, pas seulement une sous-chaîne. Autres
Autres Trie des sous-chaînes : Oui. N2 nœuds est inutile pour N = 1000. Autres
Autres Pré-calculer toutes les fréquences de paires. Autres

**À emporter :** Dans les interviews, une solution *clear* O(N2) bat une optimisation intelligente mais illisible. Les recruteurs accordent une grande importance ** à la compréhension** plutôt qu'à la célérité*.

---

- Oui. L'Ugly – Reconstruction fréquente substrante

Une erreur courante est de reconstruire la sous-chaîne sur chaque itération:

"Java
pour (int j = i; j < n; j++) {
// ...
Chaîne sub = s.substring(i, j + 1); // O(longueur)
si (isValid(cnt)) set.add(sub);
}
«» "

Cela ajoute un facteur supplémentaire `O(L)` (où `L` est la longueur de la sous-chaîne). Pour une corde de 1000 caractères, elle peut vous pousser vers la limite de 10 secondes pour certains juges.

**Fix:** Gardez une chaîne mutable (`StringBuilder`, `String`, ou liste) et *only* la matérialiser lorsque vous la connaissez valide.

---

### Code étape par étape

Laissez-nous illustrer la version Java, qui est la plus verbeuse encore claire.

"Java
État Fréquence numérique(String s) {
Set<String> unique = nouveau HashSet<>();
int n = s.longueur();

pour (int i = 0; i < n; i++) {
int[] cnt = nouvelle int[10];
StringBuilder cur = nouveau StringBuilder();

pour (int j = i; j < n; j++) {
int d = s.charAt(j) - '0';
cnt[d]++;

l'annexe(s.charAt(j));

si (isValid(cnt)) unique.add(cur.toString());
}
}
retour unique.size();
}
«» "

* **Outer loop** – corrige l'index de départ `i`.
* **La boucle intérieure** – étend la sous-chaîne vers la droite.
* **`cnt`** – met à jour les fréquences en O(1).
* ** `isValid`** – seulement 10 étapes, donc le temps global est `O(N2)`.

Les variantes Python et C++ suivent la même logique ; il suffit d'ajuster la syntaxe et les types de données.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Récapitulatif des sous-chaînes
Actualisation des fréquences
Contrôle de validité
Autres Set Hash jusqu`à `O(n2)` sous-chaînes uniques
**Total** Autres

Avec `n ≤ 1000`, les opérations les plus mauvaises sont environ `106` – confortablement dans la limite de 2 secondes sur la plupart des plates-formes.

---

### Entretien–Conseils amis

Numéro
C'est quoi ?
** Copies inutiles de la chaîne**= Utiliser un constructeur/liste mutable; seulement `join`/`toString` sur les sous-chaînes valides. Autres
Dans `isValid`, sautez les entrées où `cnt[i]=0`.
**Téléchargez la commande en utilisant `HashSet` (Java), `unordered_set` (C++) ou `set` (Python). Autres
**Readability**=Tenir des noms de fonction descriptifs (`equalDigitFrequencecy`, `isValid`). Autres
**Cas d'Edge**= Testez les chaînes à caractères simples, tous les mêmes chiffres, en alternant les chiffres. Autres

---

Ce que les recruteurs recherchent

1. **Correctness** – gérer tous les cas de bord, pas d'off‐by‐one.
2. **L'échange d'espaces horaires** – expliquer pourquoi `O(n2)` est en sécurité ici.
3. **Codage propre** – éviter les abstractions inutiles.
4. **Optionnel** – mentionner les améliorations possibles (par exemple, en utilisant des bitmasks pour 10 chiffres) mais expliquer pourquoi elles sont inutiles pour les contraintes.

---

Pensées de clôture

LeetCode 2168 est un grand problème pour présenter une approche **équilibrée** : un algorithme rectiligne à la fois **efficace** pour les limites données et **facilement compréhensible**.
En maîtrisant les implémentations Java, Python et C++ ci-dessus, vous serez prêt à :

* Discutez de l'algorithme sur un tableau blanc.
* Écrivez un code propre et sans bug dans une entrevue.
* Montrez aux recruteurs que vous priorisez **la clarté sur l'intelligence** – un trait clé pour les développeurs seniors.

Bon codage, et bonne chance d'atterrir ce prochain rôle!

---