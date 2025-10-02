---
titre: LeetCode 3144. Partition minimale de sous-chaîne d'égale fréquence de caractères -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3144 – Partition de sous-chaîne minimale d'égal caractère Fréquence
> **Programmation dynamique de LeetCode *

---

TL;DR
Compte tenu d'une chaîne inférieure `s`, la diviser en les plus rares sous-chaînes possibles de sorte que *chaque sous-chaîne est --équilibrée* – chaque caractère de la sous-chaîne apparaît le même nombre de fois.
Nous résolvons le problème avec un DP classique qui fonctionne dans **O(n2·26)** temps et **O(n)** espace.

Langue Heure Espace
- C'est quoi ?
* C++** , O(n2·26) , O(n)
*Java * O(n2·26)
**Python**

---

- Oui. 1. Remise en état des problèmes

> ** Sous-chaîne minimale de la fréquence de caractères égaux**
>
> **Input:** `s` – une chaîne de longueur `1 ... 1000` ne contenant que des lettres minuscules.
> ** Sortie :** le nombre minimum de sous-chaînes dans une partition de `s` où chaque sous-chaîne est *équilibrée*.
> Une sous-chaîne est **équilibrée** si tous les caractères qui y apparaissent apparaissent le même nombre de fois.

Exemple
«» "
s = "ababcc"
partitions valides: ("ab", "c", "c") , ("ab", "abc", "c") , ("abcc")
partitions invalides: ("a", "bab", "cc") , ("aba", "bc", "c") , ("ab", "abcc")
«» "

---

- Oui. 2. Intuition et stratégie

* Nous considérons la corde de gauche à droite.
* Laissez `dp[i]` être le nombre minimal de sous-chaînes équilibrées nécessaires pour couvrir le préfixe `s[0 ... i]`.
* Pour chaque `i` nous regardons en arrière et essayons de mettre fin à une sous-chaîne équilibrée `i`.
* En déplaçant le pointeur de départ `j` de `i` vers le bas à `0`, nous maintenons la fréquence de chaque caractère dans `s[j ... i]`.
* Si la fenêtre actuelle est équilibrée, nous pouvons terminer la partition à `i` comme `dp[j-1] + 1`.
* La réponse est «dp[n-1]».

La fenêtre coulissante qui vérifie *équilibre* est **O(26)** par étape (seulement 26 lettres).
La complexité globale est donc **O(n2·26)**.

---

- Oui. 3. Preuve d'exactitude

Nous prouvons que le DP décrit ci-dessus donne la partition optimale.

Lemma 1
Pour tout indice `i`, `dp[i]` est égal au nombre minimum de sous-chaînes équilibrées nécessaires pour couvrir le préfixe `s[0...i]`.

*Proof. *
Nous montrons par induction sur "i".

*Base:* `i = 0`.
La seule sous-chaîne est `s[0]`.
S'il est équilibré (toujours vrai parce qu'un caractère se produit une fois) `dp[0] = 1`.
Sinon, aucune partition n'existe, mais le problème garantit qu'au moins une partition existe, de sorte que le lemma détient.

*Étape d'introduction:*
Supposons que le lemma détient tous les indices `< i`.
Lorsque vous calculez `dp[i]` nous examinons chaque début possible `j` de la dernière sous-chaîne: `j ↓ [0, i]`.
Si `s[j...i]` est équilibré, alors le reste de la chaîne `s[0...j-1]` peut être partitionnée de façon optimale en sous-chaînes `dp[j-1]` par l'hypothèse d'induction.
Par conséquent, `dp[j-1] + 1` est une taille de partition réalisable pour le préfixe `i`.
Prendre le minimum sur tous les "j" possibles donne la taille optimale pour "i".
Ainsi "dp[i]" est optimal. *



Lemma 2
La procédure qui maintient les fréquences des caractères tout en scannant à l'envers identifie correctement si `s[j...i]` est équilibré.

*Proof. *
Nous conservons un tableau `freq[26]` où `freq[c]` compte les occurrences de la lettre `c` dans la fenêtre actuelle.
Après avoir ajouté `s[j]`, nous recalculons `minFreq` et `maxFreq` parmi tous `freq[c] > 0`.
`minFreq== maxFreq` iff chaque fréquence non nulle est égale à la même valeur, qui est précisément la définition d'une sous-chaîne équilibrée. *



- Oui. Théorème
L'algorithme renvoie le nombre minimal possible de sous-chaînes équilibrées couvrant l'ensemble de la chaîne `s`.

*Proof. *
Par Lemma 1, `dp[n-1]` est optimal pour toute la chaîne.
L'algorithme produit `dp[n-1]`.
Par conséquent, l'algorithme est correct. *



---

- Oui. 4. Analyse de la complexité

* **Heure:**
* Boucle extérieure sur `i` ('n` itérations).
* Boucle intérieure au-dessus de `j` (itérations n`).
* Pour chaque `j` nous mettons à jour les fréquences dans **O(1)** et vérifions l'équilibre dans **O(26)**.
→ `O(n2·26)` ↓ `O(n2)` pour `n ≤ 1000`.

* **Espace:**
* tableau `dp`: `O(n)`.
* Tableau de fréquences: `O(26)`.
→ Total `O(n)`.



---

- Oui. 5. Mise en oeuvre des références

Voici des solutions propres, commentées et prêtes à coller dans **C++**, **Java** et **Python**.
Tous les trois suivent la même stratégie de PDD.

---

### 5.1 C++ (GNU C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// Aide à tester si une fenêtre est équilibrée
bool statique estBalanced(tableau de const<int, 26>& freq) {
Int mn = INT_MAX, mx = 0;
pour (int f : freq) {
si (f) 0) poursuivre;
mn = min(mn, f);
mx = max(mx, f);
}
retour mn == mx; // mn== mx iff toutes les fréquences non-zéro sont égales
}

int minimumSubstringsInPartition(string s) {
int n = s.size();
vector<int> dp(n, n); // dp[i] = sous-chaînes minimales pour le préfixe [0,i]
pour (int fin = 0; fin < n; ++ fin) {
tableau <int, 26> freq{}; // initialisé à zéro
pour (int start = fin; start >= 0; --démarrer) {
freq[s[start] - 'a']++; // étendre la fenêtre vers la gauche
si (isBalanced(freq)) { // window [start,end] est équilibré
le candidat int = (début == 0) ? 1 : dp[début - 1] + 1;
dp[end] = min(dp[end], candidat);
}
}
}
retour dp.back();
}
};
«» "

---

#### 5.2 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
// Vérifiez si le tableau de fréquence actuel représente une sous-chaîne équilibrée
booléen statique privé estBalanced(int[] freq) {
int min = entier.MAX_VALUE, max = 0;
pour (int f : freq) {
si (f) 0) poursuivre;
min = Math.min (min, f);
max = Math.max (max, f);
}
retour min == max;
}

Int minimum public Sous-chaînesInPartition(String s) {
int n = s.longueur();
int[] dp = nouvelle int[n];
Arrays.fill(dp, n); // grande valeur initiale

pour (int end = 0; fin < n; fin++) {
int[] freq = nouveau int[26];
pour (int start = fin; start >= 0; début--) {
freq[s.charAt(start) - 'a']++;
si (estBalanced(freq)) {
int cand = (démarrage) 0) ? 1 : dp[start - 1] + 1;
dp[end] = Math.min(dp[end], cand);
}
}
}
retour dp[n - 1];
}
}
«» "

---

5.3 Python 3 (3.11)

'`python
de taper l'importation Liste

Solution de classe:
@staticmethod
def is_equilibred(freq: List[int]) -> bool:
"""Retourne Vrai si toutes les fréquences non nulles sont égales."""
mn, mx = Aucune, Aucune
pour f en freq:
si f == 0:
poursuivre
si mn n ' est pas ou f < mn:
mn = f
si mx n'est pas ou f > mx:
mx = f
retour mn == mx

def minimumSubstringsInPartition(self, s: str) -> Int:
n = len(s)
dp = [n] * n # dp[i] = sous-chaînes min pour le préfixe [0,i]

pour la fin dans l'intervalle(n):
freq = [0] * 26
pour commencer dans la plage (fin, -1, -1):
freq[ord(s[start]) - 97] += 1
si self.is_balanced(freq):
cand = 1 si début == 0 autre dp[départ - 1] + 1
dp[end] = min(dp[end], cand)

retour dp[-1]
«» "

---

- Oui. 6. Billet de blog – Le bon, le mauvais, et l'acharnement de la partitionnement équilibré

6.1 Introduction

Si vous êtes un candidat à l'ingénierie logicielle en regardant des entrevues de haute technologie, vous avez probablement vu LeetCode **3144 – Sous-chaîne minimale de fréquence de caractères égaux**.
Il s'agit d'un puzzle *moyen-difficulté* DP qui est une excellente vitrine des compétences en résolution de problèmes.
Laissez-vous disséquer pourquoi ce problème est une mine d'or d'entrevue, explorez l'élégant DP qui le résout, et parlez des pièges qui peuvent vous faire trébucher.

> **Mots clés**: LeetCode, questions d'entrevue, programmation dynamique, sous-chaînes équilibrées, entretien d'emploi, ingénieur logiciel, C++, Java, Python, pensée algorithmique.

---

6.2 Le bien – ce qui en fait une bonne question d'entrevue

Aspect Pourquoi il est précieux
-- -- -- -- -- -- -- ------------------ -- --
**Contraintes claires**= Longueur ≤ 1000, seulement lettres minuscules – permet des solutions O(n2) sans s'inquiéter des délais. Autres
La propriété de partition optimale conduit naturellement à un DP unidimensionnel. Autres
**Langues multiples**= Solvable en C++, Java ou Python – démontre la polyvalence du langage. Autres
**Décomposition logique**=Vous le cassez en = est-ce que cette fenêtre est équilibrée?== et peut-on terminer une partition ici?== – bon pour tester la communication. Autres
Autres **Edge‐Case Rich** . Les chaînes de lettres simples ou toutes les mêmes lettres sont triviales, mais des motifs mixtes (p. ex., « ababcc ») vous poussent à tester correctement l'équilibre. Autres

Les intervieweurs aiment les problèmes lorsqu'il existe un PDD ** propre et prouvable**, car il vous permet d'expliquer votre raisonnement étape par étape et de recevoir une rétroaction immédiate sur l'exactitude.

---

6.3 Les mauvaises – pièges communs et malentendus

1. **Mise à l'écart* *
*Vous pourriez penser qu'une sous-chaîne est équilibrée si *certains* caractères sont égaux, pas *tous* qui apparaissent. *
La condition correcte est ** toutes les fréquences non nulles sont identiques**.

2. ** Utilisation de structures de données supplémentaires* *
*De nombreux candidats construisent un `Map<Caracter, Integer>` à l'intérieur de la boucle intérieure. *
Bien que fonctionnel, cela ajoute des frais généraux; une gamme de taille 26 est plus rapide et plus facile à raisonner.

3. **Oubliant la transition DP préfixe**
La récurrence `dp[end] = min(dp[end], dp[start-1] + 1)` est essentielle.
Sauter la partie `dp[start-1]` donne de mauvaises réponses pour les préfixes qui contiennent déjà plusieurs sous-chaînes équilibrées.

4. **Boundaire hors‐un**
Quand "démarrer". 0' il n'y a pas de préfixe gauche.
Oublier de gérer correctement cela conduit à des indices négatifs ou de mauvais résultats.

5. ** Sous-estimation du rendement**
On peut penser que `O(n2·26)` est rapide, mais l'écrire incorrectement (par exemple, recalculer les fréquences à partir de zéro dans la boucle intérieure) le poussera vers `O(n3)` et le temps mort.

---

6.4 Le lamentable – Que regarder dans votre propre code

* **Re-Computation inutile* *
Certaines solutions naïves recalculent tout le tableau de fréquence pour chaque paire `(start, fin)`.
Le contrôle O(26) est bon marché, mais la reconstruction du tableau à chaque fois coûte O(n) et rompt le budget de temps.

* **Vérification de l'équilibre des erreurs* *
Un bogue fréquent consiste à comparer `freq.min()` et `freq.max()` sur *toutes* 26 lettres, y compris les zéros.
Puisque zéros plus bas `min`, vous allez faussement marquer fenêtres comme déséquilibré.
La clé est de sauter les fréquences zéro.

* ** Initialisation du PD* *
La configuration `dp[i]` à `i+1` (le pire cas) est sûre, mais l'initialisation à `n` (longueur de chaîne) est plus intuitive.
Ne pas le remplir correctement peut laisser des valeurs élevées qui ne sont jamais mises à jour.

* **Mémoire en C++**
Oublier `array<int, 26> freq{};` ou utiliser un `int freq[26]` cru qui n'est pas réinitialiser chaque `fin` contaminera les fenêtres ultérieures.

---

#### 6.5 Passage – Le PDD propre vous dira à votre intervieweur

> *=Nous allons maintenir un DP 1-D pour les préfixes et faire glisser une fenêtre arrière, mettant à jour un tableau de fréquences de 26 dimensions. Lorsque cette fenêtre est équilibrée, nous mettons à jour l'entrée DP.

1. **Définition PD**
`dp[i] = nombre min de sous-chaînes équilibrées pour préfixer jusqu'à i`.
*Pourquoi 1-D?* Parce que nous n'avons besoin que de la partition optimale pour le préfixe précédent – aucune table 2-D requise.

2. **Scan en arrière**
Pour chaque `fin`, déplacer `start` vers la gauche, mettre à jour `freq[s[start]]`.
Vérifier l'équilibre dans O(26).

3. **Essais de balance**
Utiliser `min` et `max` de fréquences non nulles.
`min=max` → équilibré.

4. **Transition**
`candidate = dp[start-1] + 1` (ou `1` si le début est 0).
Gardez le minimum sur tous les départs possibles.

5. **Résultat**
`dp[n-1]` est la réponse optimale.

---

6.6 Conseils pratiques

Conseil Comment maîtriser
C'est quoi ?
**Mise en œuvre de toutes les trois langues**Shows vous pouvez traduire la logique en C++, Java et Python. Autres
**Ecrire les tests d'unité**= Valider sur les cordes triviales, les mêmes cordes, les mêmes motifs alternés et les cordes aléatoires. Autres
Autres **Explain While Coding**.Promenez-vous dans les mises à jour dp', l'entretien de la fréquence et le contrôle équilibré – les intervieweurs aiment le raisonnement verbal. Autres
Autres **Temps de vos courses**= Sur LeetCode, exécutez 5 cas de test aléatoires et notez l'épreuve – assurez-vous que votre solution est efficace. Autres

---

6.7 Conclusion

LeetCode 3144 est plus qu'un simple problème de PDD : il s'agit d'une vitrine **compacte des compétences clés en interview** : analyse de contrainte propre, programmation dynamique, manipulation soignée des cas et mise en œuvre efficace.

En maîtrisant le PDD montré ci-dessus et en comprenant les pièges communs, vous serez prêt non seulement à répondre à la question, mais à impressionner vos intervieweurs avec une logique claire et un code robuste.

**Codage heureux, et que vos entretiens d'emploi soient aussi équilibrés que les sous-chaînes de partitions vousll!**

---

6.8 Mot final

Si vous préparez une entrevue d'ingénierie logicielle, incluez LeetCode **3144** dans votre liste de pratique.
La solution DP est assez simple pour coder en 30 minutes, mais le raisonnement qui la sous-tend est assez profond pour mériter les éloges des intervieweurs seniors.

Bonne chance, et rappelez-vous : * les solutions équilibrées sont souvent les meilleures ! *

---

- Oui. 7. Liste de contrôle à emporter

1. **DP sur les préfixes** – `dp[i] = min(dp[j-1] + 1)` sur toutes les fenêtres équilibrées `[j ... i]`.
2. **O(26) vérification équilibrée** – comparer min et max de fréquences non nulles.
3. ** Attention aux zéros** – ils doivent être ignorés lors de la détermination de l'équilibre.
4. **Traitement des cas** – "démarrage" 0 ' → candidat = 1.
5. **Meilleures pratiques linguistiques** – initialisation zéro, vérification des limites et fonctions d'aide claires.

Utilisez les implémentations de référence ci-dessus comme point de départ, modifiez-les pour s'adapter à votre style, et pratiquez l'explication de l'algorithme à haute voix – ce qui fait de vous un candidat exceptionnel. C'est ce qu'il a dit.

---



> **Auteur:** *Votre ami Algorithme Mentor*
> **Date:** *2024‐10‐15*
> **Tags:** LeetCode, interview prep, programmation dynamique, C++, Java, Python, sous-chaînes équilibrées, questions d'entretien algorithmiques.

---



- Oui. 8. Remarques finales

Qu'il s'agisse du codage en C++, Java ou Python, la solution DP ci-dessus est une façon *canonique* de s'attaquer au LeetCode 3144.
N'hésitez pas à l'adapter, à ajouter des mémos ou à expérimenter des fenêtres coulissantes.
Bonne chance, et que vos sous-chaînes équilibrées soient toujours parfaitement équilibrées ! C'est ce qu'il a dit.



---



*Préparé pour : Ingénieurs prêts à l'entrevue. *
*Sentez libre de déposer ce code dans votre dépôt ou GitHub Gist et référez-le dans votre portfolio. *



---



♪



---



[Fin de la note technique]