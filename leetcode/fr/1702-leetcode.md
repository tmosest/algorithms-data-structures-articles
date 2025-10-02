---
titre: LeetCode 1702. Chaîne binaire maximale après le changement -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1702 – ** Chaîne binaire maximale après changement* *
*Le bon, le mauvais, et le laid – une plongée profonde dans un problème de style avide d'entrevue qui peut vous gagner un emploi. *

---

### TL;DR
* **Problème:** Transformez une chaîne binaire avec deux swaps autorisés (=00 → 10,=10 → 01) pour obtenir la plus grande chaîne numérique possible.
* **Connaissance clé:** Toutes les opérations peuvent être simulées en déplaçant un seul `0` vers la gauche sur les `1` adjacentes.
* ** Solution optimale:**
1. Trouvez le premier `0`.
2. Comptez les «1» qui apparaissent **après** que zéro.
3. Construisez une chaîne de tous les `1`s, puis placez un `0` à l'index `n - cnt_ones_after_first_zero - 1`.
* **Complexité:** "O(n)" temps, "O(1)" espace supplémentaire.

---

- Oui. 1. Déclaration de problème (Code de bord 1702)

Vous recevez une chaîne binaire `binary` (`0`‐`1` seulement).
Vous pouvez appliquer les deux opérations suivantes à plusieurs reprises :

Opération en état Exemple
- C'est quoi ?
Sous-chaîne "00" "00010" → "10010"
Sous-chaîne ""10" ""00010" → "00001"

Retourne la chaîne binaire **maximum** que tu peux obtenir après n'importe quel nombre d'opérations.
La valeur décimale de la chaîne binaire est la plus grande possible.

**Contrôles* *

* `1 ≤ longueur binaire ≤ 105 "
* `binary[i] ↓ {'0', '1'}`

---

- Oui. 2. Pourquoi l'avidité fonctionne – L'observation de Pattern

Laissez-les expérimenter avec quelques cordes :

Après beaucoup d'opérations Résultat
- C'est quoi ?
"000110"
"01"
"00110"

Vous remarquerez :

1. **Un seul `0` peut rester dans la chaîne finale** – tout le reste se transforme en `1`.
Tout `00` peut être remplacé par `10`, en déplaçant un `0` vers la droite.
Tout `10` peut être remplacé par `01`, en déplaçant un `0` vers la gauche.
Appliquant à maintes reprises ces valeurs, les zéros seront « clump » dans un seul zéro qui peut être déplacé vers n'importe quelle position que nous voulons, sauf le début même si la chaîne a commencé par « 1 ».

2. **Lorsque les terres zéro dépendent du nombre de `1`s qui suivent le premier zéro dans la chaîne d'origine**.
Chaque `1` après le premier zéro peut être à gauche du zéro par l'opération 2.
Ainsi le zéro sera finalement positionné de sorte que exactement que beaucoup `1`s sont à sa droite.

3. **La chaîne restante est tous `1`s sauf pour ce zéro unique** – c'est la valeur binaire maximale possible.

Donc la règle cupide est:

> *Gardez tous les `1`s de tête comme ils sont, déposez tous les `0` sauf un, et poussez celui `0` aussi loin que possible à droite étant donné le nombre de `1`s qui étaient après le premier `0`. *

---

- Oui. 3. L'algorithme – Étape par étape

1. **Scan de gauche à droite jusqu'au premier `0`**
*Si vous ne rencontrez jamais un `0`, la chaîne est déjà maximale – retournez-la. *

2. **Count `1`s qui apparaissent après ce premier `0`** (`cnt`).

3. **Construire le résultat**
* Créez une chaîne de longueur `n` remplie de `1`.
* Placer un seul `0` à l'index `n - cnt - 1`.

Pourquoi `n - cnt - 1`?
Parce que `cnt` est le nombre de `1`s qui doit rester à droite du zéro.
Dans une chaîne tout-one, le zéro occuperait naturellement le point le plus à gauche (index `0`).
Pour le déplacer à droite par des positions « cnt », nous le déplaçons simplement à des endroits « cnt » de la gauche, qui est « n - cnt - 1 » de la droite.

---

- Oui. 4. Code – Trois langues

Ci-dessous sont les implémentations propres et prêtes à la production qui fonctionnent dans **O(n)** temps et **O(1)** espace supplémentaire (à part la chaîne de sortie).

> **Note :** Les trois codes sont identiques en logique ; seule la syntaxe diffère.

---

#### 4.1 Java

"Java
solution de classe {
public String maximumBinaryString(String binaire) {
int n = binaire.longueur();
Int premier Zéro = binaire.indexOf('0');

// Pas du tout – déjà maximum
si (premier Zéro) -1) retour binaire;

// Compte 1 après le premier zéro
les Après Zero = 0;
pour (int i = firstZero + 1; i < n; i++) {
si (binary.charAt(i) == '1') Après Zero++;
}

// Construisez le résultat: tous les 1's avec un 0 placé correctement
StringBuilder sb = nouveau StringBuilder();
sb.append("1".repeat(n));
Int 0 Pos = n - un Après Zero - 1;
sb.setCharAt(zeroPos, '0');
retour sb.toString();
}
}
«» "

---

4.2 Python

'`python
Solution de classe:
def maximumBinaryString(self, binaire: str) -> str:
n = len(binaire)
first_zero = binaire.find('0')
si premier_zero == - 1 :
retour binaire

# Le compte 1 est après le premier zéro
after_zero = binaire[first_zero+1:].count('1')

# Construire le résultat
res = ['1'] * n
0_pos = n - ones_after_zero - 1
res[zero_pos] = '0'
retour ''.join(res)
«» "

---

### 4.3 C++

'`cpp
solution de classe {
public:
chaîne maximumBinaryString(chaîne binaire) {
int n = binaire.size();
Int premier Zéro = binaire.find('0');
si (firstZero == chaîne::npos) retourne binaire; // pas de zéro

// Compte 1 après le premier zéro
les Après Zero = 0;
pour (int i = firstZero + 1; i < n; ++i)
si (binary[i]] '1') +onesAfterZero;

// Construire le résultat
chaîne res(n, '1');
Int 0 Pos = n - un Après Zero - 1;
res[zeroPos] = '0';
retour rés;
}
};
«» "

---

- Oui. 5. Les bons, les mauvais et les méchants

**Aspect**
C'est pas vrai.
**Idées algorithmiques** Aucun. Autres
**Complexité**= Temps `O(n)`, espace `O(1)`.= O(n2) si vous simulez chaque échange. O(2n) force brute. Autres
**Readability**= Clean, one-pass.= Difficile à suivre si vous mélangez la logique. Confusion de solutions récursives ou de piles. Autres
**Cas d'Edge**=Poignée tous les uns, tous les zéros, mélangés. Effacement si la position zéro n'est pas calculée correctement. Défile sur de très longues cordes (débordement de la pile). Autres
**Interview Verdict** ★★★★★ – simple, déterministe, couvre les contraintes. – trop lent, complexité inutile. – risqué, échoue sur les tests. Autres

**Pourquoi la cupidité fonctionne :**
Parce que les opérations sont locales et affectent seulement un `0` et un `1` adjacent, vous pouvez penser à la chaîne comme un lot de stationnement de la chaîne où chaque `0` peut conduire à travers `1`s mais ne peut pas sauter sur un autre `0`. Ainsi, au plus un `0` peut survivre et sa position finale est pleinement déterminée par le nombre de `1` qui étaient à sa droite au départ. C'est le cœur mathématique de la solution.

---

- Oui. 6. Pourquoi ce blog aide votre recherche d'emploi

1. ** Mots clés du référencement** – L'article est poivré avec des termes recruteurs rechercher pour: *Maximum Binary String After Change*, *LeetCode 1702*, *transformation de cordes binaires*, *solution de Java*, *solution de Python*, *solution de C++*, *algorithme de corde*, *O(n) time*.

2. **Deuxième de l'explication** – Les recruteurs apprécient les candidats qui, non seulement écrivent du code, mais peuvent articuler *pourquoi* une solution fonctionne.

3. **Samples de code en plusieurs langues** – Démontre la polyvalence et la capacité de travailler dans la langue utilisée par votre équipe.

4. **Structured Sections & Headings** – Rendre facile l'embauche des gestionnaires pour skim et trouver ce dont ils ont besoin.

5. **Contexte du problème** – montre que vous pouvez aborder de vrais problèmes d'entretien LeetCode, une exigence commune pour les rôles d'ingénierie logicielle.

---

- Oui. 7. Chaleur à emporter Feuille

Étape Que faire? Pourquoi?
- C'est quoi ?
Rechercher en premier `0`. Autres
Autres Le nombre `1` est après `0`. Ce sont ceux qui finiront à droite du zéro final. Autres
Autres Construire une chaîne all‐`1` et insérer un `0` à `n - cnt - 1`. Positionne le zéro exactement là où les opérations le permettent. Autres
Autres Retournez la chaîne. Autres

---

- Oui. 8. Pensées finales

Le problème *Maximum Binary String After Change* est un exemple classique de la façon dont une série apparemment compliquée d'échanges locaux peut s'effondrer en une seule solution cupidité linéaire. La maîtrise de ce problème met en évidence :

* ** intuition algorithmique** – repérer l'invariant que tous les zéros s'effondrent en un seul.
* **Codage élégance** – mise en œuvre propre et lisible.
* **Préparation à l'entrevue** – capacité d'expliquer à la fois le comment et le pourquoi.

Gardez ce modèle dans votre boîte à outils : chaque fois que vous voyez des opérations locales qui déplacent seulement un élément à gauche ou à droite, vérifiez si l'ensemble de la séquence se réduit à un seul choix global.

Bonne chance – votre prochaine interview de codage ne saura pas ce qui l'a frappé! C'est ce qu'il a dit.

---

> *Préparé pour vous par ChatGPT, l'assistant AI qui aime le code propre et de bonnes explications. *