---
titre: LeetCode 3398. La plus petite sous-chaîne avec des caractères identiques Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3398 – La plus petite sous-chaîne avec des caractères identiques I
*Hard – Recherche binaire sur la réponse*

Langue Complexité Référence
C'est quoi ?
**Java**"O(n log n)" heure, "O(1)" espace supplémentaire (https://leetcode.com/problèmes/smallest-substring-with-identique-caracters-i/) Autres
**Python** espace supplémentaire
Temps "O(n log n)", "O(1)" espace supplémentaire

---

- Oui. 1. Remise en état des problèmes

On vous donne une chaîne binaire `s` (`'0'` et `'1'`) et un entier `numOps`.
Vous pouvez retourner n'importe quel peu au plus `num Le temps des opérations.
Après les retournements, trouvez la longueur **minimum possible** du plus long bloc contigu de caractères identiques.

---

- Oui. 2. Intuition

Si on vous demande de faire le bloc le plus long ≤ L, la réponse dépend uniquement des *runs* de caractères égaux qui sont plus longs que `L`.
Un tour de longueur `R > L` peut être divisé en morceaux de longueur au plus `L` en retournant quelques bits à l'intérieur de ce tour.
Le moyen le moins cher de le faire est de casser la course toutes les positions `L+1`:

«» "
R = q·(L+1) + r (0 ≤ r ≤ L)
«» "

Vous devez exactement `q` flips pour créer les séparateurs requis.
Somme `q` sur tous les tirages → qui est le nombre d'opérations nécessaires pour le candidat `L`.
Si ce nombre ≤ `numOps`, `L` est faisable, sinon il n'est pas.

La seule subtilité est quand `L == 1`.
Avec "L". 1' nous voulons une corde parfaitement alternée.
Pour cela, nous devons vérifier les deux modèles (`0101...` et `1010...`) et choisir celui qui a besoin de moins de flips.

Parce que le test de faisabilité est monotone (si `L` est réalisable alors toute `L` plus grande est également réalisable), nous pouvons binaire-rechercher le minimum possible `L`.

---

- Oui. 3. Algorithme (Pseudocode)

«» "
longueurs de chars égaux consécutifs en s
maxRun = élément maximal d'exécution

coût de la fonction(L):
Si L == 1 :
flips StartWith0 = nombre d'anomalies avec le motif 0101...
flips StartWith1 = nombre d'anomalies avec le motif 1010...
retour min(flipsStartWith0, flipsStartWith1)

Total = 0
pour chaque r en course:
Total += r // (L + 1)
retour total

recherche binaire sur L dans [1, maxRun]
milieu = (faible + élevé) // 2
si coût(mid) <= num Opérations:
réponse = milieu
élevé = milieu - 1
Sinon:
faible = milieu + 1

réponse de retour
«» "

---

- Oui. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie la longueur minimale de bloc la plus longue possible.

---

Lemma 1
Pour un tour de longueur `R > L`, le nombre minimum de tours nécessaires pour réduire chaque bloc à l`intérieur de ce tour à la longueur ≤ `L` est égal `=R / (L+1)=".

**Prof.**
Placez un séparateur (dépliez un peu) tous les caractères `L+1`.
Après les séparateurs `q="R/(L+1)=", l`exécution est divisée en blocs `q+1`, chacun de la longueur au plus `L` (le dernier bloc peut être plus court).
Toute solution qui utilise moins de « q » flips laisserait un bloc plus long que « L », ce qui contredit la faisabilité. *



Lemma 2
Pour un «L» fixe, le nombre total de tours calculés par «coût(L)» est le nombre *minimum* de flips requis pour obtenir une chaîne dont la plus longue longueur de bloc est ≤ `L`.

**Prof.**
`cost(L)` est la somme des valeurs de Lemma 1 sur tous les parcours plus longs que `L`.
Tous les parcours plus courts ou égaux à `L` sont déjà très bien et n'ont pas besoin de bascules.
Les embouts de pliage dans des parcours distincts sont indépendants, de sorte que la somme des coûts optimaux par parcours est globalement optimale. *



Lemma 3
Si `cost(L) ≤ numOps` il existe alors une séquence de < < numOps ' flips > > qui permet d ' obtenir la plus longue longueur de bloc ≤ `L`.

**Prof.**
`cost(L)` donne une façon constructive de retourner des bits à chaque long terme comme décrit dans Lemma 1.
Appliquer ces flips donne une chaîne avec la plus longue longueur de bloc ≤ `L`.
Étant donné que le nombre total de flips est égal à `cost(L)` et `cost(L) ≤ numOps`, l'exigence est satisfaite. *



Lemma 4
Si `cost(L) > numOps` il est impossible d'obtenir une chaîne avec la plus longue longueur de bloc ≤ `L` en utilisant seulement `numOps` flips.

**Prof.**
Par Lemma 2, toute solution réalisable doit effectuer au moins des retournements "cost(L)".
Si le coût (L) dépasse le budget, il n'existe pas de solution réalisable. *



C'est vrai. Théorème
L'algorithme de recherche binaire produit la longueur minimale de bloc la plus longue possible.

**Prof.**
Définir le prédicat `P(L): coût(L) ≤ numOps`.
Par Lemma 3, `P(L)` est vrai si le `L` est réalisable.
Par Lemma 4, si `P(L)` est faux, pas plus grand `L` ne peut être faux? En fait monotonique: si `L` n'est pas réalisable, toute plus petite `L` pourrait aussi ne pas être réalisable. L'ensemble de faisabilité est fermé à la baisse.
Ainsi, `P(L)` est monotone diminuant par rapport à `L`.
La recherche binaire sur un prédicat monotone trouve toujours le plus petit `L` avec `P(L)` true.
L'algorithme retourne que `L`.



---

- Oui. 5. Analyse de la complexité

Étape Coût
- Oui.
Construction de pistes (`O(n)`) Autres
"Coût(L)" pour un candidat "O(m)" où `m ≤ n` est le nombre de runs → "O(n)" (les runs sont traités une fois). Autres
Recherche binaire "O(log maxRun)" itérations, "maxRun ≤ n". Autres
**Total**="O(n log n)` temps, "O(1)` mémoire supplémentaire. Autres

---

- Oui. 5. Mise en oeuvre des références

Voici des solutions propres et prêtes à la production dans les trois langues demandées.

---

#### 5.1 Java (compatible avec le code leet)

"Java
Importation de java.util.*;

solution de classe {
Int minLength public(String s, int numOps) {
int n = s.longueur();
si (n == 1) retourner 1; // un seul bloc peut jamais exister

// Construction de longueurs d'exécution
Liste <Integer> runList = nouvelle liste d'array<>();
nombre int = 1;
pour (int i = 1; i < n; i++) {
si (s.charAt(i) == s.charAt(i - 1)) {
count++;
} autre {
runList.add(compte);
nombre = 1;
}
}
runList.add(compte);

Int maxRun = 0;
pour (int r : runList) maxRun = Math.max(maxRun, r);

// Test de faisabilité pour un candidat L
java.util.fonction.IntUnaireCoût de l'exploitant = L -> {
si (L) 1) {
Int mism0 = 0; // modèle 0101...
int mism1 = 0; // modèle 1010...
pour (int i = 0; i < n; i++) {
char attendu0 = (i % 2 == 0) ? '0' : '1';
char attendu1 = (i % 2 == 0) ? '1' : '0';
si (s.charAt(i) != attendu0) mism0++;
si (s.charAt(i) != attendu1) mism1++;
}
retour Math.min(mism0, mism1);
} autre {
Int flips = 0;
pour (int r : runList) {
flips += r / (L + 1);
}
flips de retour;
}
};

// Recherche binaire
int low = 1, high = maxRun, ans = maxRun;
alors que (faible <= haut) {
int milieu = (faible + élevé) >>> 1;
si (coût.applicationAsInt(mid) <= numOps) {
ans = milieu;
élevé = milieu - 1;
} autre {
faible = milieu + 1;
}
}
le retour des an;
}
}
«» "

---

#### 5.2 Python (3.10+)

'`python
de taper l'importation Liste

Solution de classe:
def minLength(s: str, numOps: int) -> Int:
n = len(s)
si n] 1 :
retour 1

# Construire des longueurs d'exécution
résultats: Liste[int] = []
cnt = 1
pour i dans la plage (1, n):
si s[i] == [i - 1]:
cnt += 1
Sinon:
runs.append(cnt)
cnt = 1
runs.append(cnt)

max_run = max(runs)

coût(L: int) -> Int:
Si L == 1 :
# malencontreux avec deux motifs alternés possibles
mism0 = mism1 = 0
pour i, ch dans le(s) énuméré(s):
prévu0 = '0' si i % 2 == 0 autre '1'
attendu1 = '1' si i % 2 == 0 autre '0'
Si ch != prévu0:
msm0 += 1
Si ch != attendu1:
Misem1 += 1
retour min(mism0, mism1)
flips = 0
pour r en course:
flips += r // (L + 1)
retour flips

# Recherche binaire
lo, hi = 1, max_run
ans = max_run
alors que lo <= bonjour:
milieu = (lo + hi) // 2
si coût(mid) <= num Opérations:
ans = milieu
Bonjour = milieu - 1
Sinon:
lo = milieu + 1
retour et
«» "

---

#### 5.3 C++ (GNU C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minLength(chaîne, int numOps) {
n = (int)s.size();
si (n) 1) retour 1;

// Construction de longueurs d'exécution
vecteur<int> les parcours;
cnt = 1;
pour (int i = 1; i < n; ++i) {
Si (s[i]] cnt++;
autres {
runs.push_back(cnt);
cnt = 1;
}
}
runs.push_back(cnt);

int maxRun = *max_element(runs.begin(), runs.end());

coût automatique = [&](int L)->int{
si (L) 1) {
la valeur de l'unité de mesure est égale à la valeur de l'unité de mesure.
pour (int i = 0; i < n; ++i) {
char expect0 = (i % 2 == 0) ? '0' : '1';
char expect1 = (i % 2 == 0) ? '1' : '0';
si (s[i] != expect0) mism0++;
si (s[i] != s'attend1) mism1++;
}
retour min(mism0, mism1);
} autre {
Int flips = 0;
pour (int r : runs)
flips += r / (L + 1);
flips de retour;
}
};

int low = 1, high = maxRun, ans = maxRun;
alors que (faible <= haut) {
int milieu = faible + (élevé - faible) / 2;
si (coût(mid) <= numOps) {
ans = milieu;
élevé = milieu - 1;
} autre {
faible = milieu + 1;
}
}
le retour des an;
}
};
«» "

---

5.4 Cas de bord traités

Autres Décision Pourquoi ça compte ?
- Oui.
- Oui. 1'.. La seule longueur du bloc est 1.. Retourner 1 immédiatement.
"numOps". 0`- Pas de flips autorisés → la réponse est la plus longue course actuelle.La recherche binaire fonctionnera toujours, mais nous pouvons sauter les contrôles de coûts coûteux.
"L" 1`-= Le modèle alternant ne peut pas être géré par la formule générique d`exécution. Autres

---

- Oui. 6. Article de blog
*(SEO-optimized copy-paste ready for Medium, Dev.to, ou un blog personnel)*

> **Titre**
> Des chaînes binaires aux entrevues de préparation à l'emploi – Mastering LeetCode 3398 avec la recherche binaire

---

6.1 Introduction

> *=Hard=* est un label LeetCode qui signifie que vous n'êtes pas seulement la pratique; vous êtes *montrer* votre pensée algorithmique.
> Problème 3398 – *Petite sous-chaîne avec des caractères identiques I* – teste exactement cela: vous devez trouver un bloc minimum plus long après des retournements de bits limités.
> Dans ce post, je vais passer par l'intuition, la solution formelle, pourquoi elle fonctionne, et comment vous pouvez l'expliquer dans une interview.
> Si vous chassez un rôle d'ingénierie logicielle, c'est le genre de question que vous allez voir dans le codage des rondes, et la maîtriser vous donne du matériel digne de se vanter pour votre CV.

---

6.2 Ce qui fait Ce problème

Autres Pourquoi dur Ce que ça signifie pour vous.
C'est ce que j'ai dit.
**Monotone Feasibility + Binary Search**=Vous apprendrez à =binary-search sur la réponse=– un modèle qui apparaît dans de nombreuses questions d'entrevue. Autres
Autres **Délai L = 1**.Les petits hors-par-on peuvent briser votre logique. Vous devez penser aux deux modèles alternatifs. Autres
**Les plus grandes contraintes** Une solution O(n2) ou O(n × numOps) naïve TLE. Autres

---

### 6.3 La bonne idée de base

*Répartir chaque long trajet en blocs de longueur ≤ L en tournant un séparateur toutes les positions L+1. *
Pourquoi ça marche ?
Parce que le fait de retourner le plus tôt possible** à l'intérieur d'un long terme vous donne toujours le maximum d'avantages pour les plus petits.
Les maths fonctionnent à `=R/(L+1)=== retourne par course – simple, rapide et optimal.

**Pourquoi c'est génial pour votre CV**

* Vous pouvez expliquer une solution *run-based* en 30 secondes.
* Il démontre *l'état d'esprit d'optimisation*: vous réduisez un problème complexe à une poignée d'opérations arithmétiques.
* Vous montrerez que vous pouvez gérer des cas de bord non triviaux** (L = 1).

---

### 6.4 The Nice - Recherche binaire sur la faisabilité

Vous ne pouvez pas vérifier toutes les valeurs possibles `L` un par un (il y a jusqu'à n).
Au lieu de cela, vous observez que si un certain `L` est possible (vous pouvez faire tous les blocs ≤ L), alors tout *large* `L` est aussi possible, mais tout *plus petite* `L` peut ne pas l'être.
Cette propriété *monotone* vous permet de faire une recherche binaire `L` dans les étapes `O(log n)`.

**Explication conviviale* *

> Je détermine d'abord si un `L` donné est possible en comptant les flips requis; puis j'effectue une recherche binaire sur `L`.
> Chaque essai de faisabilité est linéaire dans le nombre de parcours, de sorte que la complexité globale est `O(n log n)` – assez rapide pour les contraintes. (en milliers de dollars)

---

### 6.5 Le "Bad" – Ce qui pourrait mal tourner

1. **Miss-counting runs** – par exemple, oublier de pousser le dernier run.
2. **Utiliser la formule générique pour L = 1** – cela échoue parce qu'un motif alternatif n'a pas de séparateur de la chaîne.
3. **Les limites inférieures/upper incorrectes dans la recherche binaire** – par exemple, utiliser `maxRun` comme limite supérieure mais ne pas gérer le cas où `maxRun` est 1.

** Comment vous protéger**

* Essai avec des chaînes minuscules (`n = 1`, `n = 2`, `numOps = 0`).
* Vérifier la fonction de coût pour une `L` connue (par exemple, L = courant max run → flips = 0).
* Marchez dans un exemple tiré à la main dans l'entrevue; montrez-vous que *mismatch* compte pour les deux modèles lorsque L = 1.

---

### 6.6 L'erreur – Pièges d'entrevue potentiels

Piège
- Oui.
J'ai écrit une solution qui passe l'échantillon mais pas des tests cachés. Autres
J'ai utilisé la récursion et j'ai obtenu le trop-plein de la pile. Autres
Autres L'intervieweur veut voir la complexité du temps. Autres

---

### 6.7 Le "Nice" – Que dire à l'intervieweur

1. **Énoncez le problème dans vos propres mots** – Nous sommes autorisés jusqu'à `numOps` bit flips; nous voulons minimiser la longueur du plus long bloc contigu. (en milliers de dollars)
2. **Expliquez le modèle basé sur l'exécution** – Nous pouvons comprimer la chaîne en longueurs d'exécution; chaque course de longueur `R` aura besoin de "=R/(L+1)=" flips pour faire tous les blocs ≤ L.
3. **Afficher le test de faisabilité** – ─Given `L`, nous pouvons calculer le total des retournements en temps linéaire. (en milliers de dollars)
4. **Décrivez la recherche binaire** – Nous la recherche binaire `L` de 1 à l'exécution maximale actuelle.
5. **Mention l'étui de bord** – Quand L = 1, nous devons considérer les deux modèles en alternance ; nous comptons simplement les erreurs par rapport à 0101... et 1010.... (en milliers de dollars)

Soyez prêt à écrire du code sur le tableau blanc: le squelette est court; la partie délicate est de gérer `L==1`.

---

### 6.8 Comment cette connaissance se traduit par le codage du monde réel

* **Traitement par lots** – Le fractionnement d'une chaîne dans des runs est analogue au traitement des logs en morceaux.
* ** Sélections de sperme** – Choisir le premier séparateur est une stratégie gourmande qui apparaît souvent dans les problèmes de programmation.
* **Modèles algorithmiques** – Une recherche binaire sur la réponse apparaît dans les questions minimum/maximum (par exemple, énergie initiale minimale pour les problèmes de chemin).

Si vous pouvez facilement expliquer ces modèles, vous signalez aux intervieweurs que vous pouvez *reconnaître* une classe de problèmes et *appliquer* une technique éprouvée.

---

### 6.9 Dernier départ

LeetCode 3398 n'est pas qu'une question ; c'est un moment de micro-enseignement.
*Bonne* pour votre CV : une cupidité soignée basée sur la course, une mise en œuvre propre « O(n log n) » et une preuve solide d'exactitude.
*Bon* pour la préparation de l'entrevue: pratique expliquant *binaire-recherche sur la réponse* et traitant des cas de bord subtils.

** Prochaines étapes**
1. Communiquez cette solution à votre dépôt GitHub (y compris les trois variantes linguistiques).
2. Ajoutez un blog avec les extraits de code et quelques exemples.
3. Dans votre CV, notez *=Solved LeetCode 3398 – optimisation des chaînes binaires en utilisant la décomposition et la recherche binaire sur la réponse.

Tu viens de transformer un puzzle algorithmique en or d'entretien. C'est ce qu'il a dit.

---

### 6.10 Clôture

Si vous avez apprécié cette plongée profonde dans LeetCode 3398, faites-le moi savoir!
Laissez un commentaire ou un DM sur LinkedIn, et je partagerai plus de questions prêtes à l'entrevue qui s'appuient sur les mêmes concepts.

Bon codage, et que vos rondes d'entrevue soient aussi serrées que le bloc le plus long minimum que vous venez d'optimiser!

---


**Fin du blog**

*(Sentez libre de modifier les rubriques ou ajoutez vos propres anecdotes personnelles. La structure est prête à être publiée et contient tous les points clés que l'intervieweur appréciera.) * *


---


- Oui. 7. Remarques finales

Nous avons couvert :

* Preuve algorithmique formelle que l'avidité basée sur l'exécution est optimale.
* Une mise en œuvre de référence approfondie en Java, Python et C++.
* Un article de blog prêt à publier de style interview qui relie la solution à la croissance de carrière.

Vous êtes maintenant entièrement équipé pour répondre à cette question, écrire un code propre, et expliquer le raisonnement dans une entrevue d'emploi. Bonne chance !