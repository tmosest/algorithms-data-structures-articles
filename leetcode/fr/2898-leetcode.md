---
titre: LeetCode 2898. Score maximal du stock linéaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2898 – Score maximal du stock linéaire
**Moyenne** – Code Leet

> **Objectif** – Choisir une séquence de jours telle que pour chaque paire consécutive
> `prix[i] – prix[j]== i – j`.
> Maximiser la somme des prix choisis.

Ci-dessous est une solution **ready-to-copy** dans **Java**, **Python** et **C++** (O(n) time, O(n) space) suivie d'un billet de blog **SEO-friendly** qui explique l'astuce, les compromis et pourquoi c'est un excellent point d'entrevue.

---

- Oui. 1. Aperçu de la solution

Langue idée clé complexité
C'est pas vrai.
*Java * Prix - indice ' (1-basé) → seau, somme par seau 'O(n)' temps, 'O(n)' espace
**Python**=Identique à Java – utiliser `defaultdict`=="O(n)` time, `O(n)` espace
**C++**============================================================================================================================================================================================================================================================ espace

*Pourquoi le `prix - indice' fonctionne-t-il? *
Pour une séquence linéaire, la différence entre deux prix consécutifs est égale à la différence entre les indices:

«» "
prix[i] – prix[j] = i – j (i > j)
«» "

Réarrangement:

«» "
prix[i] – i = prix[j] – j
«» "

Ainsi, tous les indices sélectionnés partagent le même **key** `prix – indice`.
Nous nous contentons de regrouper les prix par cette clé et de choisir le seau avec la plus grande somme.

---

- Oui. 2. Code de référence

### 2.1 Java

"Java
Importation de java.util.*;

solution de classe {
prix public long maxScore(int[]) {
Carte<entier, long> seau = nouveau HashMap<>();
réponse longue = 0L;

pour (int i = 0; i < prix.longueur; i++) { // 0
clé int = prix[i] - (i + 1);
long newSum = seau.getOrDefault(key, 0L) + prix[i];
seau.put(clé, nouveauSum);
réponse = Math.max(réponse, nouveauSum);
}
réponse de retour;
}
}
«» "

2.2 Python

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maxScore(self, prix: Liste[int]) -> Int:
seau = defaultdict(int)
meilleur = 0
pour i, prix en énuméré(prix): # i est basé sur 0
clé = prix - (i + 1)
Seau[clé] += prix
best = max(meilleur, seau[clé])
le meilleur retour
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long maxScore(vecteur<int>& prix) {
non ordonné_map<long long, long> seau;
long an = 0;
pour (size_t i = 0; i < prix.size(); ++i) {
longue clé longue = (long long)prix[i] - (long long)(i + 1);
benne[clé] += prix[i];
ans = max(ans, seau[key]);
}
le retour des an;
}
};
«» "

---

- Oui. 3. Billet de blog – Note de stock linéaire maximale : le bon, le mauvais, et le mauvais

> **Audience cible:** développeurs Java/Python/C++ se préparant pour des interviews techniques, recruteurs et amateurs d'algorithmes.
> ** Mots-clés principaux :** *Python solution*, *C++ solution*, *hashmap trick*, *problème d'interview*, *O(n) algorithme*.

---

3.1 Introduction

> Lorsque vous ouvrez LeetCode 2898 *Maxim Linear Stock Score*, la première chose qui peut vous mordre est l'état apparemment «odd» :
> `prix[i] – prix[j]== i – j`.
> Il ressemble à un puzzle de programmation dynamique ou à deux pointeurs, mais le vrai tour est un simple liner: **bucket par `prix - indice'**.

Cet article explique pourquoi ce seau fonctionne, ses avantages et ses inconvénients, et comment l'expliquer avec confiance dans une interview.

---

3.2 Restaurer le problème

Nous avons un tableau `prix[1...n]` (1-indexé).
Choisir une sous-séquence `index = [i1 < i2 < ... < ik]` telle que pour chaque paire adjacente

«» "
prix[ij] - prix[ij-1] = ij - ij-1 (1)
«» "

Le **score** est simplement la somme des prix sélectionnés.
Nous devons le maximiser.

---

3.3 Intuition et transformation

Réécrire (1) en déplaçant les termes :

«» "
prix[ij] - ij = prix[ij-1] - ij-1
«» "

Le côté gauche est **constant** pour tous les indices dans une séquence linéaire.
Donc tous les jours choisis partagent la même valeur de

«» "
clé = prix - indice
«» "

Si nous rassemblons tous les jours par cette clé et additionnons les prix à l'intérieur de chaque groupe, le groupe qui a la plus grande somme est la réponse.

> **Pourquoi cela ne manque-t-il pas une subséquence optimale? * *
> Toute subséquence optimale doit satisfaire (1), donc toutes ses clés sont égales.
> Inversement, le choix de tous les indices avec une clé particulière satisfait automatiquement (1).
> La meilleure réponse est donc la somme maximale du seau.

---

3.4 Le bien – Simplicité et vitesse

* **Time** – O(n) parce que nous numérisons le tableau une fois.
* ** Espace** – O(n) pire cas (chaque élément a une clé distincte).
* **Mise en œuvre** – Mise à jour de la carte de hash en ligne 5 dans Java/Python/C++.
* **Big-O Friendly** – Poignées `n = 10^5` confortablement; `prix ≤ 10^9`, donc nous utilisons `long`/`int64_t`.

> *Interview-Amiendly*: Vous pouvez l'expliquer en < 30 secondes – Groupe par différence d'indice de prix.

---

### 3.5 L'Éclate – Pièges cachés

Que se passe-t-il ?
- C'est quoi ?
En utilisant l'indice 0 incorrectement.
Autres Dépassement de la somme (le prix * n ' peut dépasser 32 bits) Autres
Autres Oublier la clé initiale La carte peut contenir des zéros pour les clés invisibles. poignées de clés manquantes

---

#### 3.6 La suringénierie

Certaines personnes interrogées tentent d'utiliser des arbres segmentés, des arbres Fenwick ou des tables DP.
Ces approches ajoutent une complexité inutile et des délais de risque ou des bogues.
S'en tenir au seau **hash-map** à moins que l'intervieweur ne veuille explicitement une solution plus élaborée.

---

### 3.7 Exemple de marche

«» "
prix = [1, 5, 3, 7, 8]
indices (1-basés): 1 2 3 4 5

clé = prix - indice:
1-1 = 0
5-2 = 3
3-3 = 0
7-4 = 3
8-5 = 3

Cercueils :
0 → [1, 3] somme = 4
3 → [5, 7, 8] somme = 20 <-- max

Réponse = 20
«» "

---

3.8 Tester votre mise en œuvre

Autres Essai prévu
C'est pas vrai.
[5, 6, 7, 8, 9]
[10]
[1, 2, 3, 4, 5]
[1, 1000000000]
1+2+4+8+16+32 = 63 (toutes les clés de partage 0)

Écrivez des tests unitaires dans votre langue ou utilisez le terrain de jeux LeetCode.

---

#### 3.9 Récapitulation de complexité

- **Heure**: `O(n)` – passage unique sur le tableau.
- **Espace**: `O(n)` – la taille de la carte correspond au nombre de clés distinctes.
- **Évoluabilité**: Poigne les contraintes maximales (`n = 10^5`, `prix ≤ 10^9`) en millisecondes.

---

3.10 Pourquoi c'est une bonne question d'entrevue

1. **Trick Revealed** – Démontre la reconnaissance des motifs : convertir une contrainte de différence en clé.
2. ** Langues multiples** – Afficher que vous pouvez le résoudre en Java, Python, C++ (et même JavaScript).
3. **Le temps est suffisant** – Vous pouvez le résoudre avec une seule boucle ; pas de tables DP ou de récursion.
4. **Edge Cases** – Encourage la discussion sur le débordement, l'indexation et les collisions de hachage.

---

3.11 Avis de clôture

- ** Expliquez clairement la transformation** avant d'écrire le code.
- **Afficher les mises à jour de la carte** étape par étape.
- **Débordement de Mention** en utilisant des langages avec des largeurs entières fixes.
- **Finir avec l'analyse de complexité** – les recruteurs adorent voir que vous pensez à la performance.

Codage heureux, et que la touche `prix - indice` vous mène toujours au score le plus élevé! C'est ce qu'il a dit.

---

#### 3.12 SEO Capture instantanée

Mots clés
C'est pas vrai.
Titre du stock linéaire maximal – LeetCode 2898 Solution Java Python C++
Description de la Meta de Solve LeetCode 2898 dans le temps O(n). Lire Java, Python, code C++ et guide de préparation d'entrevue. Autres
H1===================================================================================================================================================================================
Restatement des problèmes de H2, Intuition, Code Java, Code Python, Code C++, Complexité, Conseils d'entrevue
LeetCode 2898 exemple de diagramme, Java hashmap code snippet, Python par défaut exemple, C++ unordered_map code

Ajoutez l'article à votre blog, partagez-le sur LinkedIn et regardez le trafic de recherche d'emploi croître!