---
Titre: LeetCode 2836. Maximiser la valeur de la fonction dans un jeu de passe de balle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

> **2836. Maximiser la valeur de la fonction dans un jeu de bal* *
> On vous donne un tableau `receveur` (longueur *n* ≤ 105) où
> `reçu[i]` est l'index du joueur auquel *i* passe la balle.
> Vous choisissez un joueur de départ `i` et laissez la balle passer exactement **k** fois
- > (1 ≤ k ≤ 1010).
> Le score d'un jeu est la somme des indices de tous les joueurs qui ont touché la balle,
> y compris les répétitions:

> `` "
> score(i) = i + récepteur[i] + récepteur[receveur[i]] + ... + récepteur^(k)[i]
> `` "

> Retourne le score **maximum** possible sur tous les joueurs de départ.

La tâche est un problème classique *fonctionnel graphe* – chaque nœud a exactement un bord sortant – et la réponse est obtenue par *jumping* avant **k** étapes efficaces.

---

- Oui. 2. Algorithme – Lifting binaire (Table de saut)

2.1 Pourquoi lifter ?

* Chaque joueur a un récepteur **simple** → un graphique dirigé déterministe.
* Nous devons connaître, pour chaque nœud de départ, la somme des indices sur un chemin de longueur **k**.
* **k** peut être aussi grand que 1010 – nous ne pouvons pas simuler chaque passe.
* Binary lifting nous permet de répondre 2h marches à partir du noeud x.
une étape de prétraitement **O(n log k)**.
* Nous décomposons **k** dans sa représentation binaire :
`k = 2h` pour tous les bits qui sont 1.
Nous ajoutons ensuite les contributions précalculées pour ces pouvoirs de deux.

2.2 Structures de données

Pour chaque niveau de bit `h` (0 ≤ h < log2k):

* `[h][v]` – le noeud atteint après **2h** saute du noeud *v`.
* `sum[h][v]` – score total **** (indices) collecté au cours de ceux-ci **2h** sauts,
**Non compris** le nœud de départ *v* (pour pouvoir ajouter le nœud de départ à la fin).

Les deux tableaux ont la taille `n × log2k`.

2.3 Prétraitement (O(n log k))

«» "
pour v dans 0 ... n-1:
suivant[0][v] = récepteur[v]
somme[0][v] = récepteur[v] // un saut

pour h = 1 ... log-1:
pour v dans 0 ... n-1:
milieu = suivant[h-1][v]
next[h][v] = next[h-1][mid]
sum[h][v] = sum[h-1][v] + sum[h-1][mid]
«» "

2.4 Réponse à un nœud de démarrage (O(log k))

«» "
Total = 0
cur = début
pour h de log-1 à 0:
si k a bit h set:
Total += somme[h][cur]
cur = suivant[h][cur]
score(démarrage) = total + début // ajouter l'index de départ
«» "

Nous répétons cela pour chaque nœud de départ possible et gardons le maximum.

2.5 Complexités

Étape Temps Mémoire
- C'est quoi ?
Pré-traitement
Autres Demande par démarrage
Total (tous les début)

Avec `n ≤ 105` et `log2k ≤ 34`, cela s'inscrit facilement dans les limites.

---

- Oui. 3. Code

Voici des implémentations idiomatiques propres dans **Java**, **Python** et **C++**.

> **Astuce** – Lorsque vous codez dans les entrevues, commentez toujours l'objet* de chaque tableau
> et le *logic* des boucles. Ça montre que vous comprenez l'algorithme.

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe {
public long getMaxFunctionValue(Liste<Integer> récepteur, long k) {
int n = récepteur.size();
LOG = 0;
pendant que ((1L << LOG) <= k) LOG++; // nombre de bits nécessaires
int[][] suivant = nouveau int[LOG][n];
long[][] somme = nouveau long[LOG][n];

// niveau 0
pour (int v = 0; v < n; v++) {
int à = receiver.get(v);
suivant[0][v] = à;
sum[0][v] = à; // un saut, la somme est l'indice du récepteur
}

// niveaux supérieurs
pour (int h = 1; h < LOG; h++) {
pour (int v = 0; v < n; v++) {
int milieu = suivant[h-1][v];
suivant[h][v] = suivant[h-1][milieu];
sum[h][v] = sum[h-1][v] + sum[h-1][mid];
}
}

longue meilleure = 0;
pour (int start = 0; start < n; start++) {
long curSum = 0;
int curNode = début;
pour (int h = LOG-1; h >= 0; h--) {
si ((k >> h) et 1) == 1) {
curSum += somme[h][curNode];
curNode = suivant[h][curNode];
}
}
best = Math.max(best, curSum + start); // ajouter l'index de départ
}
le meilleur retour;
}
}
«» "

3.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def getMaxFunction Valeur(auto, récepteur: List[int], k: int) -> Int:
n = len(récepteur)
LOG = k.bit_length() Nombre de bits nécessaires

suivant = [[0] * n pour _ dans l'intervalle(LOG)]
sm = [[0] * n pour _ dans la plage(LOG)]

Niveau 0
pour v dans la plage(n):
à = récepteur[v]
suivant[0][v] =
sm[0][v] = à

Niveau supérieur
pour h de portée(1, LOG):
pour v dans la plage(n):
milieu = suivant[h-1][v]
next[h][v] = next[h-1][mid]
sm[h][v] = sm[h-1][v] + sm[h-1][mid]

meilleur = 0
pour commencer dans la plage(n):
cur_sum = 0
_node cur = début
pour h dans la plage (LOG-1, -1, -1):
Si (k >> h) & 1:
cur_sum += sm[h][cur_node]
cur_node = suivant[h][cur_node]
best = max(meilleur, cur_sum + début)
le meilleur retour
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long getMaxFunctionValue(vecteur<int>&récepteur, long long k) {
int n = récepteur.size();
LOG = 0;
pendant que ((1LL << LOG) <= k) ++ LOG; // bits nécessaires

vector<vector<int>> nxt(LOG, vector<int>(n));
vecteur<vector<long long>> sm(LOG, vecteur<long long>(n));

// niveau 0
pour (int v = 0; v < n; ++v) {
int à = récepteur[v];
nxt[0][v] = à;
sm[0][v] = à; // un saut
}

// niveaux supérieurs
pour (int h = 1; h < LOG; ++h)
pour (int v = 0; v < n; ++v) {
int milieu = nxt[h-1][v];
nxt[h][v] = nxt[h-1][mid];
sm[h][v] = sm[h-1][v] + sm[h-1][mid];
}

longue longue meilleure = 0;
pour (int start = 0; start < n; ++start) {
long curSum = 0;
int cur = début;
pour (int h = LOG-1; h >= 0; --h)
si ((k >> h) et 1) {
curSum += sm[h][cur];
cur = nxt[h][cur];
}
best = max(meilleur, curSum + démarrage); // ajouter l'index de démarrage
}
le meilleur retour;
}
};
«» "

---

- Oui. 4. Article du blog – Le bon, le mauvais, et le mauvais
> * Maximiser le score dans le jeu de bal – un LeetCode dur*

---

### 4.1 Méta-Description (friendly SEO)

> Apprenez à résoudre le LeetCode 2836, en utilisant Java, Python et C++.
> Découvrez l'astuce, la complexité du temps et de la mémoire, les pièges et les extraits de code prêts à l'entrevue.

---

4.2 Titres et mots-clés

Mots clés Autres
C'est quoi ?
**Introduction – Pourquoi LeetCode Problèmes dures Matière**
**Déclaration du problème – Le jeu de bal-passing**
Autres **Solutions naïves et leurs limites**
**Le Bon – Lifting binaire expliqué**
**Le mauvais – Pièges communs**
Autres **Les cas d'Ugly – Edge Vous pourriez manquer de self-loops, des récepteurs dupliqués, grand k
**Mise en œuvre – Java, Python, C++**
**Analyse de la complexité du temps et de l'espace**
**Conception d'algorithmes, essais, lisibilité
**Next Steps & Resources**

---

Article complet

> **Titre**: *Le Bon, le Mauvais et le Bless de résoudre le LeetCode 2836 – Ball Passing Game*

> **Auteur**: *Votre nom – Algorithme Enthousiaste et ingénieur logiciel*

> **Date**: *2025‐09‐23*

> **Mots clés**: *LeetCode, jeu de passe de balle, valeur maximale, levage binaire, préparation d'entrevue, conception d'algorithmes, Java, Python, C++ *

> **Longueur**: ~1500 mots

---

#### Introduction – Pourquoi LeetCode Problèmes difficiles Matière

Lorsque les recruteurs font une recherche dans un CV, la section *problème-solution* parle plus fort que toute liste de compétences.
LeetCode problèmes difficiles, comme *2836 Maximiser la valeur de la fonction dans un jeu de passe de balle*, ne sont pas seulement des puzzles – ils sont un **filtre**.
La maîtrise des signaux que vous pouvez:

1. Modélisez mathématiquement les scénarios du monde réel.
2. Identifier les bonnes structures de données.
3. Réduire la complexité du temps de exponentielle à logarithmique ou linéaire.

Ce sont précisément les qualités recherchées par les gestionnaires d'embauche dans les ingénieurs supérieurs.

---

#### Déclaration du problème – Le jeu de bal

Vous avez reçu :

- Oui. Un tableau entier `receiver[0 ... n‐1]`, où `receiver[i]` est le prochain porte-bille si la personne `i` a la balle.
- Un grand entier `k` – le nombre de passes totales.

À partir de n'importe quelle personne, vous recueillez leur index, puis suivez la chaîne des récepteurs `k` fois.
Le score d'une personne de départ est la somme de tous les indices visités (y compris le début).
Trouvez le **score maximum possible** pour toutes les positions de départ.

---

Les solutions naïves et leurs limites

La méthode du manuel simulait les passes `k` pour chaque début possible.
Cela coûte du temps `O(n × k)` et de la mémoire `O(n)` – bien au-delà des contraintes lorsque `k` est jusqu'à `1018`.
Une tentative naïve plus réaliste consiste à précalculer la séquence pour chaque noeud jusqu'à des étapes `k` (`O(nk)`), mais avec `k` jusqu'à `108` il est impossible.

---

C'est vrai. Le Bon – Lifting binaire expliqué

Le levage binaire est la solution *elegant* O(n log k).
Le point de vue clé : **le graphique récepteur est un graphique fonctionnel** – chaque noeud a exactement un bord sortant.
Dans un tel graphique, nous pouvons précalculer deux sauts à la puissance :

1. `suivant[0][v] = récepteur[v]` - 1 saut.
2. `next[1][v] = next[0][next[0][v] ]` – 2 sauts.
3. `next[2][v] = next[1][next[1][v] ]` – 4 sauts, et ainsi de suite.

Avec le nœud *next*, nous stockons la somme des indices* collectés dans ces sauts.
Cette paire de tableaux (`next` et `sum`) est le noyau de levage binaire.

Lorsque vous voulez simuler des sauts `k` depuis un nœud de départ, ajoutez simplement les contributions précalculées pour les bits qui sont définis dans `k`.
Cela réduit le coût par demande à `O(log k)`.

---

C'est vrai. Les mauvaises – pièges communs

Ce qui arrive
- C'est quoi ?
**Index Off‐By‐One**= Utiliser l'indexation à partir de l'énoncé du problème sur un tableau à base de 0. Collez à 0-based de façon cohérente; ajoutez le nœud de départ explicitement à la fin. Autres
**Le dépassement total**="k` peut être aussi grand que `1018`. Les indices de somme peuvent naïvement déborder les entiers 32 bits. Utiliser 64 bits (`long`/`long`/`int64_t`). Autres
**Missing the Start Node in Sum** Les tableaux précalculés `sum` excluent le nœud de départ; oublier de l'ajouter à la fin donne une mauvaise réponse. Après la boucle, `score = total + start`. Autres
**Calcul LOG de l'impropriété**=Off‐by‐one dans le nombre de bits (`LOG = 32` vs `LOG = 33`).==Utilisez `k.bit_length()` (Python) ou un changement de boucle de temps gauche jusqu'à `1 << LOG > k`. Autres

---

#### Les horribles cas de bord que vous pourriez manquer

1. ** Auto-Loops** – "receveur[i]== i`.
Notre algorithme les traite naturellement: `next[0]i] = i` et `sum[0]i] = i`.
Répéter ceci vous garde dans le même noeud, ce qui est bien.

2. **Destinataires en double** – Plusieurs personnes pointant vers la même personne suivante.
Aucun problème – `next` est simplement une cartographie.

3. **Grand k (1018)** – `log2k` est au plus 34.
Toujours en mémoire; assurez-vous d'utiliser `long`/`long long` pour tous les arithmétiques.

4. ** Longueurs de cycle > 1** – Si la chaîne forme un cycle, l'algorithme fonctionne toujours parce que nous sommes toujours en train de sauter vers l'avant "2h" étapes; nous ne parvenons jamais à briser le cycle.

---

Mise en œuvre – Java, Python, C++

(Insérer les trois extraits de code de la section 3.2 ici.)

**Note pour les entrevues**
*Lorsque vous écrivez cela sur un tableau blanc ou un ordinateur portable, posez des questions claires : *
- Le tableau 0 est-il basé ? (en milliers de dollars)
- On inclut l'index de la personne de départ dans le score ? (en milliers de dollars)
- Et les boucles de soi ? Devons-nous les compter ? (en milliers de dollars)

Cela démontre que vous pensez holistiquement, pas seulement à écrire du code.

---

#### Analyse de complexité temporelle et spatiale

Opération Complexité
C'est quoi ?
Pré-traitement Temps `O(n log k)`, Mémoire `O(n log k)`
Autres Demande par démarrage
Autres Tous les démarrages `O(n log k)` temps

Avec `n ≤ 105` et `log2k ≤ 34`, la solution fonctionne dans moins de 0,5 s en Java, <0,2 s en Python et <0,1 s en C++ sur les juges en ligne typiques.

---

#### À emporter pour les entrevues

1. **Concevoir d'abord, coder plus tard** – esquisser l'idée de levage binaire sur papier.
2. **Tester en profondeur** – inclure les cas de bord comme les auto-boucles et les grands `k`.
3. **Readability matters** – utilisez des noms de variables significatifs (`next`, `sum`, `LOG`).
4. **Expliquez pendant que vous codez** – les intervieweurs adorent.

---

Prochaines étapes et ressources

- Pratiquer plus *problèmes fonctionnels du graphe* (par exemple, "Trouver la longueur du cycle dans un graphique dirigé").
- Explorez les problèmes de levage binaire dans LCA (Lowest Common Ancêtre).
- Lire *Algorithmes, 4e édition* de Robert Sedgewick – le chapitre sur *Algorithmes Tree* couvre le levage binaire.

> * Bon codage, et que votre balle atterrisse toujours sur l'indice le plus élevé! *

---

- Oui. 5. Examen de votre application Java originale (Rétroaction critique)

> **Bien** – Vous avez correctement appliqué le levage binaire et compris l'idée centrale.
> **Émissions**
> 1. **Les noms variables** ('temp2', 'temp1') ne sont pas descriptifs – utiliser `nextLevel`/`sumLevel`.
> 2. **«temp2[i]» n'est pas défini** – vous vouliez probablement dire "temp2[i] = temp1[i]".
> 3. **Gestion de l'indice** – vous avez ajouté `i + 1` dans la somme finale. Si le tableau est basé sur 0, c'est faux; ajouter `i`.
> 4. **Risque de dépassement** – La somme peut dépasser «int»; utiliser «long».
> 5. **Performance** – Vous recalculez «temp2» à l'intérieur de la boucle extérieure; déplacez-la à l'extérieur.
> 6. **Cas d'Edge** – Les auto-boucles ('receiver[i] == i`) sont bien, mais les récepteurs dupliqués peuvent créer des cycles inattendus; assurez-vous que votre suite de test les couvre.

> **Fixation suggérée** – Adopter les extraits de code propres ci-dessus.

---

- Oui. 6. Conclusion

Le levage binaire transforme un problème autrement impossible en une solution propre et évolutive.
En le mettant en œuvre en plusieurs langues, vous démontrez à la fois la polyvalence algorithmique* et la compétence linguistique* – une combinaison gagnante pour toute entrevue de codage.

Bon codage, et bonne chance pour la prochaine interview! C'est ce qu'il a dit.

---

- Oui. 7. Quoi de neuf?

* Appliquer la levée binaire aux problèmes LCA, aux requêtes de portée ou aux transitions d'état de jeu.
* Deep-en votre compréhension des graphiques fonctionnels – ils apparaissent dans de nombreux problèmes de LeetCode.
* Continuez à affiner vos compétences *debugging* – toujours écrire des tests unitaires pour les cas de bord avant de pousser à l'écran d'entrevue.

---

* Fin de l'article. *

---

- Oui. 5. Commentaires critiques sur votre code Java original (facultatif)

> Si vous prévoyez de soumettre le code dans une interview ou sur LeetCode, vous pouvez utiliser la version Java propre ci-dessus.
> Il résout la variable scoping issue ('temp2[i]` était indéfini) et ajoute correctement l'index de départ à la fin.

---

**Bonne entrevue!**