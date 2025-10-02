---
titre: LeetCode 3499. Maximiser la section active avec le commerce Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
C'est pas vrai. Le problème de type LeetCode

> **Problème**
> On vous donne une chaîne binaire **s** (`'0'` = inactif, `'1'` = actif).
> Un *commerce* comprend:
> 1. Choisir un bloc contigu de `'1'`s qui est **arrondi** par `'0'`s sur les deux côtés.
> 2. Remplacer ce bloc de `'1's par un bloc plus long de `'1's par le remplissage d'inondations dans les `'0'`s environnants – le nouveau bloc s'étend jusqu'au bloc suivant de `'1'` (ou jusqu'à ce que la chaîne se termine).
>
> Vous pouvez effectuer ** au plus un** trade.
> Retourner le nombre maximum de «1»** qui peut être présent après le commerce (ou après n'avoir rien fait si un commerce est impossible).

> **Constraints**
* 1 ≤ ≤ 105
> * s se compose uniquement de `'0'` et `'1'`

Le problème apparaît sur LeetCode sous la forme de *Sections actives maximales après un échange* (ID 1690 – renommez-le .

> **Pourquoi est-ce important? * *
> Lors d'un entretien de qualité de production, on demande à un candidat d'optimiser une opération à chaîne. L'astuce est de réaliser que le seul avantage vient de transformer un bloc de `'1`s entouré de zéros en un bloc plus long de `'1`s qui absorbent les zéros sur **deux** côtés.
> Cette prestation correspond à la somme des deux zéros adjacents qui se trouvent de chaque côté du bloc «1» choisi.

---

Vite Regardez l'Algorithme

1. **Couvez les «1» d'origine** – «ones».
2. **Scannez la chaîne** tout en gardant :
* `curZero` – longueur de la séquence actuelle de `'0'`.
* `prevZero` – longueur de la série précédente de `'0'` qui est *arrondie* par `'1`s.
3. Chaque fois que nous voyons un `'1'` après quelques zéros, nous déplaçons `curZero` dans `prevZero` et réinitialisons `curZero`.
4. Si nous rencontrons plus tard une autre série de zéros suivie d'un `'1'`, nous pouvons **trader** ce milieu `'1'`-bloc et gagner `prevZero + curZero` new `'1`s.
5. Gardez le maximum de tous ces gains (« bestGain »).
*S'il n'y a pas de commerce possible ('bestGain == 0') la réponse est simplement 'ones'.*

Le scan entier est **O(n)** temps et **O(1)** espace.

---

- Oui. Mise en œuvre des références

Ci-dessous sont trois implémentations *complètes* – Java, Python 3 et C++ – qui suivent la même logique. Ils sont tous compilés sur l'environnement LeetCode standard (`class Solution { ... }`).

> **NOTE**
> Les trois codes assument la signature de la fonction :

"Java
solution de classe {
public int maxActiveSections Après le commerce (String s) { ... }
}
«» "

'`python
Solution de classe:
def maxSections actives Après le commerce (s'il s'agit d'une entreprise) -> Int: ...
«» "

'`cpp
solution de classe {
public:
int maxActiveSectionsAfterTrade(chaîne s) { ... }
};
«» "

---

#### 3.1 Java

"Java
solution de classe {
public int maxActiveSections Après le commerce(String s) {
// Nombre total de sections actives initialement
= 0;
pour (char ch : s.toCharArray()) {
si (ch == '1') ceux++;
}

// Scanner pour les zéros adjacents
int bestGain = 0; // best sum de deux essais de zéro adjacents
int curZero = 0; // longueur de l'exécution de zéro en cours
int prevZero = 0; // longueur du zéro précédent

pour (int i = 0; i < s.longueur(); ++i) {
c = s.charAt(i);
si (c) '0') {
curZero++; // continuer à compter les zéros
} autre { // nous avons frappé un '1 '
si (prevZero > 0 && curZero > 0) {
bestGain = Math.max(bestGain, prevZero + curZero);
}
// Le nombre de zéros que nous venons de terminer devient le « précédent »
prevZero = cur Zéro;
curZero = 0; // réinitialiser pour l'exécution suivante
}
}

// Si la chaîne se termine par des zéros – ils ne peuvent pas être utilisés pour un trade,
// donc on ignore le dernier curZero en ne l'ajoutant pas à bestGain.

retour + bestGain; // trade est optionnel
}
}
«» "

---

3.2 Python 3

'`python
Solution de classe:
def maxSections actives Après le commerce (s'il s'agit d'une entreprise) -> Int:
# Compter les sections actives existantes
les = s.count('1')

best_gain = 0
_zéro = 0
prev_zero = 0

pour ch en s:
si ch == '0':
_zéro 1
Sinon : # ch == '1'
si prev_zero > 0 et cur_zero > 0:
best_gain = max(best_gain, prev_zero + cur_zero)
prev_zero = cur_zero
_zéro = 0

retour + best_gain
«» "

---

### 3.3 C++

'`cpp
solution de classe {
public:
int maxSections actives après le commerce(chaîne s) {
= 0;
pour (char ch : s) si (ch == '1') ++ones;

int bestGain = 0;
l'ent curZero = 0, prevZero = 0;

pour (charte : s) {
si (ch == '0')
++curZero;
Autre { // ch == '1 '
si (prevZero > 0 && curZero > 0)
bestGain = max (bestGain, prevZero + curZero);
prevZero = cur Zéro;
curZero = 0;
}
}

retour + bestGain; // si bestGain est 0, nous retournons simplement ceux
}
};
«» "

Les trois solutions fonctionnent en **O(n)** temps, utilisez **O(1)** espace auxiliaire, et passez la contrainte 105-longueur.

---

- Oui. L'article du blog – Maîtriser le problème des sections actives (bon, mauvais et mauvais)

> **Titre**:
> ** Maximiser les sections actives après un échange – une plongée profonde dans un problème difficile de LeetCode* *
> **Méta-Description**:
> Déverrouillez les secrets du problème de Sections actives maximum. Apprenez l'astuce O(n) intelligente, comprenez les cas de bord, et voyez pourquoi il est un must-solve pour les entrevues d'ingénierie logicielle.

- Oui. 1. Présentation

Le problème **Maximise Active Sections After One Trade** est un favori sur les plateformes d'entretien comme LeetCode et HackerRank. L'histoire sonne simple: vous avez une chaîne binaire, vous êtes autorisé à effectuer un seul -trade, et vous voulez finir avec le plus `'1'' possible. Dans la pratique, le problème est un bel exercice dans l'analyse de la longueur d'exécution**, la manipulation des cas de référence** et l'état d'esprit d'optimisation**.

> *Pourquoi cela apparaît-il souvent dans les entrevues? *
> Parce qu'il cache une subtilité : la seule façon d'obtenir un avantage d'un trade est de remplacer un bloc de `'1'`s qui est *arrondi* par `'0'`s avec un bloc plus long qui -absorbe - ces zéros. Il enseigne aux candidats comment transformer un problème verbal en algorithme concret.

- Oui. 2. Réévaluation des problèmes (en français)

- **Input**: Une chaîne binaire `s` (`'0'` = inactive, `'1'` = active).
**Règles commerciales**:
1. Choisissez un bloc contigu de `'1'`s **flanked** par `'0'`s sur les deux côtés.
2. Remplacer ce bloc par un nouveau bloc de `'1's qui s'étend jusqu'au prochain bloc `'1'` (ou la chaîne se termine).
- **Objectif**: Après avoir effectué au plus un trade, retournez le nombre maximum de `'1''s** qui peut apparaître dans la chaîne.

La longueur des cordes peut atteindre 100 000, donc une simulation naïve est hors de question.

- Oui. 3. Bien – Le point de vue intelligent O(n)

L'observation clé :
> **Le bénéfice du trade est égal à la longueur des deux zéros de chaque côté du bloc «1» choisi. **
> En d'autres termes, nous recherchons un motif `0...0 1...1 0...0` et nous pouvons "squeeze" le milieu `'1'`-bloc dans les zéros gauche et droit.
> La prestation est `leftZeroRun + rightZeroRun`.

De ce point de vue, le problème se réduit à:

1. Comptez les `'1`s existantes – c'est la valeur de base.
2. Trouvez la somme maximale de deux zéros consécutifs** qui sont *sandwiched* entre `'1's.
3. Ajouter cette somme maximale à la valeur de base.
4. Si aucune paire n'existe, la réponse n'est que la valeur de base (ne rien faire est toujours permis).

3.1 Traitement des cas de bord

Bordure Pourquoi c'est difficile Comment notre algorithme fonctionne
Il y a un problème.
Zero-runs au début ou à la fin de la chaîne. Le scan n'ajoute jamais le tout premier ou dernier zéro à « bestGain ». Autres
Les blocs consécutifs `'1'` sans zéros entre eux. L'algorithme ne met tout simplement jamais à jour `bestGain` – il reste `0`. Autres
Autres Très long zéro-run qui relie toute la chaîne Le trade serait un non-op, car il n'y a rien de l'autre côté à remplacer. Le premier zéro-run ne devient jamais `prevZero` (son char précédent n'est pas `'1''). Autres

- Oui. 4. Pourquoi l'approche naïve est une mauvaise idée

Une première tentative pourrait être :

1. Énumérer tous les blocs du milieu `'1'`.
2. Pour chacun, simuler le trade en balançant vers l'avant et vers l'arrière jusqu'à la prochaine `'1''.
3. Comptez les nouveaux `'1', gardez le meilleur.

C'est une solution **O(n2)** : pour une chaîne de 105 caractères, elle serait chronométrée. C'est parce que :

- Oui. Il ignore la nature du problème.
- Oui. Il utilise le travail quadratique lorsque le travail linéaire suffit.
- Oui. Il oblige le candidat à penser à une simulation coûteuse plutôt qu'à un simple scan.

- Oui. 5. La mise en œuvre laborieuse

Beaucoup de personnes interrogées ou d'étudiants rédigent une solution de force brute qui :

'`python
pour i dans la plage(len(s)):
pour j dans la plage(i, len(s):
i s[i:j+1] == '1'*k et s[i-1] == '0' et s[j+1] == «0»:
# ... simulation de remplissage d'inondation ...
«» "

La boucle interne relise des parties de la chaîne à plusieurs reprises, conduisant à une complexité **temps qui explose**. C'est aussi *peu* parce que:

- Oui. Le code est difficile à lire – boucles imbriquées, de nombreuses vérifications d'index.
- Oui. Il est fragile – de petites erreurs d'index provoquent `IndexError` ou de mauvais résultats.
- Oui. Il s'agit d'une surcompétence – le problème ne **pas** nécessite une simulation de remplissage d'inondation.

L'éditorial de LeetCode souligne cependant l'élégante solution de course à deux points, transformant le laid en un algorithme propre, lisible et efficace.

- Oui. 6. La ligne linéaire expliquée

Au cœur de la solution O(n) se trouve la technique de course à deux points**:

1. **Current Zero Run (`curZero`)** – alors que nous voyons `'0'' nous les comptons simplement.
2. **Précédent Zero Run (`prevZero`)** – quand nous avons frappé un `'1'', nous traitons la course de zéros que nous venons de terminer comme le voisin gauche de la prochaine transaction potentielle.
3. Chaque fois que la prochaine série de zéros suit ce bloc `'1'`, nous pouvons **trader** et gagner `prevZero + curZero`.
4. Nous n'avons jamais besoin d'aller au-delà de la prochaine étape zéro, c'est-à-dire de toutes les informations requises.

Cette approche s'apparente au problème classique du sous-arrayum maximal : vous gardez une fenêtre roulante, mettez à jour une valeur optimale et ne revoyez jamais les pièces traitées.

- Oui. 7. À emporter dans le monde réel

> *Si vous pouvez réduire une opération apparemment compliquée de "trade" à un simple "picker deux zéros voisins et remplacer les zéros intermédiaires, vous serez prêt pour les questions sur*:
> * Encodage de longueur d'exécution (commun dans les algorithmes de compression).
> * Manipulation de chaînes dans les problèmes d'entrevue.
> * Optimisation des opérations dans les structures de données (p. ex. arbres segmentés, arbres Fenwick).
> * Prise de conscience des bords – surtout lorsqu'il s'agit d'un problème de fond.

8. TL;DR – La solution 3 lignes

Texte
les = nombre('1')
prevZero = curZero = 0
pour c en s:
si c == '0': curZero += 1
Sinon:
best = max (meilleur, prevZero + curZero)
prevZero, curZero = curZero, 0
retour + meilleur
«» "

C'est le cœur de chaque solution acceptée. Une fois que vous le comprenez, le problème est une brise.

- Oui. 9. Exercices de pratique

Tâche Pourquoi il est utile
- Oui.
Autres Implémenter la solution dans **Rust** – pratique à vie & emprunt-vérificateur. Construire des compétences de manipulation de cordes de bas niveau. Autres
Autres Modifier la fonction pour retourner les indices* du bloc commercial optimal. Il revient de l'algorithme au problème original. Autres
Autres Généraliser une version **k-trade** – vous pouvez effectuer jusqu'à des métiers `k`. Il vous défie de penser aux solutions DP ou segment-tree. Autres

10 ans. Réflexions finales

Le problème **Sections actives maximales** est un petit défi autonome qui enseigne les plus grandes leçons :

- **Transformer les mots pour courir** – toujours chercher des groupes contigus.
- **Les caisses sont le véritable test** – rappelez-vous que les première et dernière séries de zéros ne peuvent pas être utilisées pour un trade.
- **Optimiser tôt** – une simulation O(n2) vous fera toujours coller ; pensez aux passes linéaires.

Maîtrisez ce problème, et vous constaterez que beaucoup d'autres questions d'entrevue deviennent beaucoup plus faciles. Bon codage !



> **Mots-clés** – *LeetCode, interview, défi de codage, chaîne binaire, encodage de longueur d'exécution, algorithme O(n), un commerce, sections actives, inondation, analyse d'exécution, entretien d'ingénierie logicielle*
> **Tags** – *LeetCode, Interview, Algorithmes, Chaîne, Fenêtre coulissante, Programmation dynamique*



---

Bonne résolution, et que votre `'1'' soit toujours dans la majorité!