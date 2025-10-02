---
titre: LeetCode 466. Compter les Répétitions -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution

Ci-dessous sont trois solutions complètes et autonomes qui compilent sur les derniers JDK, Python 3.11 et GCC 14.

---

### 1.1 Java (Code Leet 466)

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
Int public getMaxRepetitions(String s1, int n1, String s2, int n2) {
si (n1 == 0) retourner 0;
// clé : indice en s2, valeur : (indice de bloc, nombre de s2 vu)
Carte<entier, int[]> enregistrement = nouvelle HashMap<>();

indice int = 0; // position à l'intérieur de s2
nombre d'int = 0; // combien de s2 nous avons terminé
block int = 0; // combien de blocs s1 traités

pendant que (bloc < n1) {
// traiter un bloc de s1
pour (int i = 0; i < s1.longueur(); i++) {
si (s1.charAt(i) == s2.charAt(index)) {
l'index++;
si (index == s2.longueur()) { // un autre s2 fini
indice = 0;
count++;
}
}
}

block++;

// Détection du cycle
Clé entière = indice;
si (enregistrer.contientKey(key)) {
int[] prev = record.get(key);
int prevBlock = prev[0];
int prevCount = prev[1];

// nombres avant cycle
préfixe intBlocks = prevBlock;
préfixe intCount = prevCount;

// nombres dans le cycle
cycle intBlocks = bloc - prevBlock;
cycle int Nombre = nombre - prevCount;

// blocs restants après cycles complets
restant Blocs = n1 - bloc;
Int pleine Cycles = restantsBlocs/cycleBlocs;
Int tallBlocks = restantBlocks % cycleBlocks;

Total Nombre = préfixe
+ pleinCycles * cycle
+ getTailCount(s1, s2, index, tailBlocks, compte, prevCount);

total de retourCoût / n2;
}

// Souvenez-vous de l'état actuel
record.put(index, nouvelle int[]{bloc, nombre});
}

// aucun cycle détecté
nombre de retours / n2;
}

/** compte combien de s2 nous pouvons obtenir dans la partie arrière. */
Int privé getTailCount(String s1, String s2, int startIndex,
Couvercles, coupe, coupe) {
indice int = début Index;
nombre int = curCount;
pour (int i = 0; i < tailBlocks; i++) {
pour (int j = 0; j < s1.longueur(); J++) {
si (s1.charAt(j) == s2.charAt(index)) {
l'index++;
si (index == s2.longueur()) {
indice = 0;
count++;
}
}
}
}
compte de retour - prevCount;
}
}
«» "

*Temps*: **O(=1=1 +=2=)**
* Espace*: **O(=2=)** – la carte peut contenir au plus des indices "=2=" différents.

---

#### 1.2 Python (Code Leet 466)

'`python
de taper l'importation Dict, Tuple

Solution de classe:
def getMaxRepetitions(self, s1: str, n1: int, s2: str, n2: int) -> Int:
si n1 == 0:
retour 0

# clé : position dans s2, valeur : (block_index, count_of_s2)
enregistrement: Dict[int, Tuple[int, int]] = {}

idx_s2 = 0 # position actuelle dans s2
nombre = 0 nombre de s2 finis
bloc = 0 nombre de blocs s1 traités

pendant que le bloc < n1:
pour ch en s1:
si ch == s2[idx_s2]:
idx_s2 += 1
Si idx_s2 == len(s2) :
idx_s2 = 0
nombre += 1
bloc += 1

# détection du cycle
si idx_s2 dans l'enregistrement :
prev_block, prev_count = enregistrement[idx_s2]

# préfixe
prefix_blocks = prev_block
prefix_count = prev_count

# cycle
cycle_blocks = bloc - prev_block
cycle_count = count - prev_count

_blocs restants = n1 - bloc
full_cycles = autres_blocs // cycles_blocs
tail_blocks = reste_blocks % cycle_blocks

total = (
_compte préfixe
+ cycles complets * nombre de cycles
+ compte_de_tail(
s1, s2, idx_s2, queue_blocs, nombre, prev_count
)
)
total de retour // n2

enregistrement[idx_s2] = (bloc, nombre)

# Aucun cycle trouvé
Nombre de retours // n2

@staticmethod
def _tail_count(s1: str, s2: str, début: int,
_blocs de queue: int, cur_count: int,
prev_count: int) -> Int:
idx = début
cnt = calcul
pour _ dans range(tail_blocks):
pour ch en s1:
si ch == s2[idx]:
idx += 1
Si idx == len(s2):
idx = 0
cnt += 1
retour cnt - prev_count
«» "

*Temps*: **O(=1=1 +=2=)**
* L'espace*: **O(=2)**

---

### 1.3 C++ (Code Leet 466)

'`cpp
#incluez <string>
#inclut <non-ordonné_map>
#incluez <vecteur>

solution de classe {
public:
Int getMaxRepetitions(std::string s1, int n1,
md::chaîne s2, int n2) {
si (n1 == 0) retourner 0;

// carte: index dans s2 -> paire(blocIndex, compteS2)
std::unordered_map<int, std::pair<int, int>> enregistrement;

int idxS2 = 0; // position en s2
= 0; // nombre de s2 finis
bloc int = 0; // nombre de blocs s1 traités

pendant que (bloc < n1) {
pour (char ch : s1) {
si (ch) s2[idxS2] {
++idxS2;
si (idxS2 == (int)s2.size()) {
idxS2 = 0;
+ nombre;
}
}
}
+ bloc;

// Détection du cycle
auto it = record.find(idxS2);
si (it != record.end()) {
int prevBlock = it->second.first;
int prevCount = it->seconde.seconde;

// pièce préfixée
préfixe intCount = prevCount;

// Partie du cycle
cycle intBlock = bloc - prevBlock;
cycle int Nombre = nombre - prevCount;

int restant = n1 - bloc;
Int pleine Cycles = restant / cycleBlock;
int tailBlocks = restant % cycleBlock;

Int total =
préfixe
+ pleinCycles * cycle
+ tailCount(s1), s2, idxS2, tailBlocks, nombre, prevCount);

total de retour / n2;
}
enregistrement[idxS2] = {bloc, nombre};
}

// aucun cycle détecté
nombre de retours / n2;
}

particulier:
/* combien de s2 supplémentaires peuvent être collectés dans la partie arrière */
(suite) s1, const st::string& s2,
début int Idx, queue d'inteBlocks,
d'un point de vue économique
int idx = début Idx;
int cnt = curCount;
pour (int i = 0; i < tailBlocks; ++i) {
pour (char ch : s1) {
si (ch == s2[idx]) {
++idx;
si (idx) == (int)s2.size() {
idx = 0;
++cnt;
}
}
}
}
retour cnt - prevCount;
}
};
«» "

*Temps*: **O(=1=1 +=2=)**
* L'espace*: **O(=2)**

> **Les trois implémentations utilisent la même idée** – traverser `s1` `n1` fois, garder l'index actuel à l'intérieur `s2`, compter combien de chaînes `s2` complètes nous pouvons extraire, et chercher un cycle pour sauter le travail répété.
> La détection du cycle garantit que l'algorithme n'excède jamais quelques centaines d'itérations (parce qu'il n'y a que des indices distincts de «S2»).

---

- Oui. 2. Article de blog – Code de Leet 466 : Compter les répétitions

Description de la méta
**LeetCode 466 – Compter Les Répétitions** – Maîtriser le problème de subséquence de chaîne le plus dur avec un algorithme basé sur le cycle. Lisez les solutions Java, Python et C++, l'analyse de la complexité, les conseils de préparation d'entretien et débarquez votre prochain travail d'ingénierie logicielle !

---

1. Aperçu du problème

Détails
C'est quoi ?
Numéro de code
**Nom**
Difficulté
*Tags *Tags *Tags *Tags *Tags *Tags

**État* *
Avec deux chaînes `s1` et `s2`, répéter `s1` exactement `n1` fois (formant `S1 = s1.repeat(n1)`) et répéter `s2` exactement `n2` fois (formant `S2 = s2.repeat(n2)`).
`S2` est une suite **** de `S1` si nous pouvons supprimer des caractères de `S1` pour obtenir `S2`.
Retourner le nombre maximal entier `k` de telle sorte que `S2` répété `k` times soit une séquence de `S1`.
En termes formels: `k = maxMatches / n2 =`.

---

- Oui. 2. Pourquoi ce problème est intéressant

C'est bien, c'est mal.
C'est quoi ?
** Bon** Nécessite une compréhension profonde de la logique de subséquence. la solution est trop lente. Autres
Les contraintes (`n1, n2 ≤ 10000`) vous obligent à penser en termes de *cycles* plutôt que de force brute. Il est facile de se perdre dans l'arithmétique pointeur quand `s1` et `s2` sont de longueurs différentes. Autres
**Désormais** L'éditorial officiel est concis mais n'est pas convivial pour les débutants. Autres

---

- Oui. 3. Aperçu algorithmique

1. ** Passage simple**
Scanner `s1` bloc par bloc.
Conserver un indice `idxS2` dans `s2`.
Quand un caractère de `s1` correspond au caractère actuel de `s2`, avancez `idxS2`.
Lorsque `idxS2` atteint la fin de `s2`, nous avons extrait un `s2` complet et réinitialisé `idxS2` à `0`.
Incrément un `compte` qui suit combien `s2` nous avons extrait.

2. **Détection des cycles**
La seule chose qui compte après le traitement de chaque bloc de `s1` est le `idxS2` actuel.
Il n'y a que des valeurs possibles pour `idxS2`.
Si le même `idxS2` apparaît à nouveau, nous sommes entrés dans un *cycle* : le schéma des futures réalisations se répète.
Enregistrez l'index des blocs et le `compte` lorsque chaque `idxS2` unique apparaît en premier.
Une fois qu'un cycle est trouvé, décomposer les travaux restants en :

* **Préfixe** – partie avant le début du cycle.
* **Cycle** – le segment répétable.
* **Tail** – les blocs restants qui ne forment pas un cycle complet.

3. ** Calculer le nombre total de «s2»**
«» "
total = préfixe
+ pleinCycles * cycle
+ taille
«» "

`tailCount` est calculé en simulant les "tailBlocks" restants (au plus un cycle de longueur).

4. **Réponse** – diviser par `n2` (division entière).

L'algorithme fonctionne en temps linéaire par rapport aux longueurs de `s1` et `s2` plus une petite constante pour la recherche de cycle. La consommation de mémoire est limitée par «S2 ».

---

- Oui. 4. Extraits de code

Langue Fichier clé Complexité
C'est pas vrai.
**Java** Autres
**Python** Autres
**C++**= `Solution.cpp`= **Heure**=(=1=+=2=) **Espace** Autres

*Les blocs de codes complets sont indiqués ci-dessus. *

---

- Oui. 5. Conseils d'entrevue

Sujet Pourquoi ça compte
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Two-pointer technique**=Keep track of positions in `s2` while scanning `s1`.= Pense à `s1` comme la boucle =outer= et `s2` comme le pointeur =Inner=. Autres
Autres **Détection de cycle** , permet de sauter d'énormes répétitions (`n1` jusqu'à 10 000). Enregistrez le *state* (index dans `s2`) dans une carte ; une fois vu, vous connaissez la boucle. Autres
**Analyse de la complexité**=Les intervieweurs adorent la discussion Big-O propre.==Remarquer le temps linéaire et l'espace constant (O(=2=)). Autres
**Cas d'escroquerie** Testez-les avant de coder. Autres

> ** Conseil professionnel** – Lorsque vous expliquez votre solution, mentionnez qu'il s'agit d'un problème classique de la période* qui apparaît dans de nombreuses questions d'entrevues subséquentes. Il démontre une compréhension profonde de la façon d'optimiser au-delà de la force brute.

---

- Oui. 6. Pourquoi cette solution vous procure le travail

1. **Claire, code idiomatique** – Pas de tableaux inutiles, chaque variable a un seul but.
2. **Algorithme évolutif** – Fonctionne confortablement pour les limites les plus défavorables (`n1, n2 ≤ 10 000').
3. **Préparé pour les suivis** – Si l'intervieweur demande : Que faire si `s1` ou `s2` est extrêmement long ?
4. ** Versatile** – Démontre votre capacité à traduire la même logique à travers Java, Python et C++ – un drapeau rouge pour les entreprises qui utilisent plusieurs piles technologiques.

---

- Oui. 2. SEO-Optimized Blog Post

> **Titre**: *Master LeetCode 466 – Compte Les Répétitions: Java, Python, C++ & Interview Préparation*

> **Description détaillée**: Découvrez la solution optimale pour LeetCode 466 – Comptez les Répétitions. Plongez dans le problème de subséquence de la chaîne dure, explorez la détection de cycle et voyez les implémentations Java, Python et C++ qui vous aident à accéder à votre prochaine interview technique.

```markdown
# Master LeetCode 466 – Compter les répétitions (Hard)

**LeetCode 466** est un favori parmi les ingénieurs de logiciels seniors et les amateurs de data-structure.
Ce post vous permet de parcourir une solution rapide basée sur le cycle dans **Java**, **Python** et **C++**.
Nous disséquons pourquoi le problème est difficile, mettons en évidence les concepts clés de l'entrevue, et vous donner l'avantage de poser votre rôle de rêve.

---

Capture de problème

> **Objectif**:
> - Répéter `s1` `n1` fois → `S1`.
> - Répéter `s2` `n2` fois → `S2`.
> - Trouver le maximum `k` de telle sorte que `S2` répété `k` times est un subséquence de `S1`.

Pourquoi c'est dur

- Oui. Il ne s'agit pas seulement de concaténation ; vous devez **supprimer** caractères de `S1` pour correspondre à `S2`.
- La force de Brute `O(n1·=1·=2·=2" est inacceptable pour `n1, n2 ≤ 10 000`.
- Mauvaise compréhension de "repeat" versus "concaténate" conduit à des bugs.

---

Une percée algorithmique

1. ** Scannage linéaire de `s1`** – Technique à deux points.
2. **Remplir la case `s2`** – Utiliser un index `idxS2` et un compteur `count`.
3. **Modèles** – Seuls les états "idxS2" possibles; utiliser une carte.
4. **Redoublements de mouvements** – Calculer le préfixe, le cycle et la queue pour obtenir le total Des allumettes.
5. **Résultat** – Division entière par `n2`.

L'algorithme s'exécute dans l'espace **O(=1=2=)** et **O(=2=)**.

---

Code en trois langues

Langue Complexité
C'est pas vrai.
**Java** **Time** O(=1=2=), **Espace** O(=2=) Autres
**Python** **Time** O(=1=+=2=), **Espace** O(=2=) Autres
**C++******Temps** Autres

> * Le code source complet est fourni dans l'article ci-dessus. *

---

Liste de contrôle de la préparation de l'entrevue

- Stratégie à deux points pour l'appariement de subséquences.
- Détection de cycles par l'État pour éviter les TLE.
- Manipulation de cas de bord (`n1==0`, chaînes vides).
- Discussion de complexité : temps linéaire, espace supplémentaire constant.

---

# # # Obtenez un emploi

Montrez aux recruteurs que vous pouvez résoudre un problème de LeetCode dur avec un code propre et efficace dans plusieurs langues.
Cela démontre :

1. **Profondeur algorithmique** – La détection du cycle est une technique éprouvée.
2. **La polyvalence des langues** – capacité d'écrire Java idiomatique, Python et C++.
3. **L'état d'esprit de résolution des problèmes** – vous vous concentrez sur l'optimisation, pas sur la force brute.

---

** Bon codage !**
«» "

---

Référence Mots clés

- LeetCode 466
- Compte les Répétitions
- Problème de subséquence de chaîne dure
- Algorithme de chaîne Java
- Technique à deux points Python
- Détection de cycle C++ sans ordre_map
- Préparation de l'entrevue pour les problèmes de chaîne
- Structures de données et algorithmes
- Solutions d'entretien d'ingénierie logicielle

---

- Oui. 3. Pensée finale

LeetCode 466 vous apprend à transformer un défi apparemment inextricable en une solution élégante et efficace.
Que vous codez dans **Java**, **Python** ou **C++**, l'idée centrale reste la même : scanner une fois, se souvenir de votre état, trouver le cycle et sauter le reste.

Utilisez les extraits de code et les idées d'entrevue ci-dessus pour **expliquer avec confiance** le problème dans votre prochaine entrevue et pour **montrer votre maîtrise** des techniques de manipulation de chaînes avancées. Bonne chance ! C'est ce qu'il a dit.

---

*Fin du blog. *

---

Ce guide complet, combinant code prêt à la production et explications prêtes à l'entrevue, devrait vous permettre de dominer LeetCode 466 et d'impressionner les recruteurs dans toute entreprise de haute technologie. Bonne solution !