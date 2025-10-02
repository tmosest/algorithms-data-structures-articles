---
titre: LeetCode 3273. Montant minimum des dommages accordés à Bob -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Montant minimum des dommages accordés à Bob – LeetCode 3273
**Une visite complète (Java / Python / C++ + Blog Post)**

---

Table des matières
1. [Énoncé du problème] (#Énoncé du problème)
2. [Pourquoi ce problème compte] (#pourquoi-ce-problème-matières)
3. [Insight de base : temps d'achèvement pondéré](#temps d'achèvement pondéré de base)
4. [Greedy Solution (Règle Smith)] (#Greedy-solution-smiths-Règle)
5. [Analyse de la complexité] (#analyse de la complexité)
6. [Edge-Case & Pièges](#edge-Case--Pièges)
7. [Code Snippets](#code-snippets)
* Java
* Python
* C++
7. [Le Bon, le Mal et le Malheur]
8. [Alterner les approches et les variantes] (# alterner les approches--variantes)
9. [Take-away pour les entrevues et votre chasse à l'emploi] (#take-away pour les entrevues - votre chasse à l'emploi)
10. [Conclusion] (#conclusion)

---

- Oui. 1. Énoncé du problème <un nom="problème-statement"></a>

> ** Montant minimal des dommages accordés à Bob**
> *Difficulté: moyenne*

Vous recevez:
- "pouvoir" – le nombre de points de santé Bob peut enlever par seconde avec une attaque.
- Arriérages "dommages [i]" et "santé [i]" (taille **n**, «1 ≤ n ≤ 105»).

Chaque seconde Bob peut attaquer **un** ennemi et enlever les points de santé " puissance " de cet ennemi.
Après chaque seconde, chaque ennemi *vivant* inflige des dommages égaux à son «dommage[i]» à Bob.

**Objectif** : Trouver le nombre minimum de dégâts** Bob peut prendre si vous jouez de façon optimale.

**Type de retour**: `long` / `long` / Python `int` (parce que la réponse peut être jusqu'à 1013).

---

- Oui. 2. Pourquoi ce problème est-il important?

C'est pas vrai.
C'est le cas.
**Question d'interview commune** – LeetCode 3273 est devenu un problème populaire de l'interview-prép. La solution est une application de manuel de **Smith-S rule** pour planifier, un pont élégant entre les algorithmes et les problèmes du monde réel. Autres
Autres Vous aide à pratiquer **comparateurs / tri personnalisé** (Java, C++), **functools.cmp_to_key** (Python) et **int arithmétique** (Python) ints non liés. Vous donne confiance dans le raisonnement sur **temps d'achèvement pondéré** – un modèle qui apparaît dans de nombreuses questions d'entrevue. Les attaques entrelacées (p. ex., le changement d'ennemis au milieu de l'attaque) ne sont jamais meilleures – beaucoup de débutants essaient cela et se coincent. Autres

**Mots clés pour le référencement**
- LeetCode 3273
- Montant minimum des dommages accordés à Bob
- Algorithme du temps de réalisation pondéré
- Smiths Règle calendrier avide
- algorithme d'entretien de codage
- Solution Java Python C++
- défi de codage des entretiens
- conseils d'entretien d'emploi

---

- Oui. 3. Aperçu de base: Temps d'achèvement pondéré <un nom="temps d'achèvement pondéré par le cœur-inspective"></a>

Laissez-nous formaliser la situation :

Ennemy `i`. Santé `hi`.. Dommages par seconde `di`.. Temps d'attaque nécessaire (secondes) `ti`.
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
"hi" / "pouvoir" (ceil)

**Observation* *
Bob peut terminer un ennemi avant de passer au suivant sans perte d'optimalité.
Si vous retardez la fin de l'ennemi `x`, son *temps d'achèvement* `Cx` augmente, augmentant le dommage total `dx · Cx`.
Tous les ennemis qui viendront plus tard seront également retardés, de sorte qu'il n'est jamais bénéfique de changer.

Ainsi, le problème se réduit à:
> **Séquencier les ennemis dans un seul ordre. **
> Chaque ennemi `i` est attaqué consécutivement pendant `ti` secondes, puis il meurt.
> Le dommage total est

\[
\text{Total} = \sum_{i} d_i \times _Ci
\]

où `C_i` est l'heure d'achèvement (lorsque l'ennemi `i` meurt).

---

- Oui. 4. Solution d'avidité (Règle de Smith) <un nom (Règle de Smith)</a>

Le problème est exactement le ** temps d'achèvement pondéré** problème de programmation sur une seule machine:

- **Temps de traitement** = `ti` (secondes nécessaires pour terminer l'ennemi `i`).
- **Poids** = "di" (dommage par seconde).

La règle de Smith (également connue sous le nom de règle de ratio*) stipule :

> *Commander les emplois en diminuant `poids / temps de traitement'.*

Pour nos variables :

\[
\text{Ratio}_i = \frac{d_i}{t_i}
\]

Si nous trions les ennemis par ce rapport **descendant**, nous obtenons un calendrier optimal.
En cas de liens, toute commande est bonne (la comparaison du produit sera égale).

- Oui. Pourquoi la règle fonctionne
- Si l'emploi `A` a un rapport plus élevé que l'emploi `B`, terminer `A` plus tôt permet d'économiser plus de temps que terminer `B` en premier.
- L'échange de toute paire adjacente qui viole l'ordre de ratio augmente strictement l'objectif.
- Oui. Par conséquent, l'ordre trié est globalement optimal.

---

- Oui. 5. Analyse de complexité <un nom="analyse de complexité"></a>

Étape Opération Temps Espace
- C'est quoi ?
Calculer "ti` (division du ciel)
Autres Indices de tri par rapport à l'année
Calculer la réponse

**Dans l ' ensemble**
- **Heure**: **O(n log n)**
- **Espace** : **O(n)** (pour stocker `ti` et un tableau d'index)

Les limites numériques sont minuscules (`dommage`, `santé`, `puissance` ≤ 104), mais le temps cumulé `t` peut atteindre `109`.
Utilisez des entiers 64 bits (`long long` / `long` / Python's `int`) pour éviter le débordement.

---

- Oui. 6. Edge‐Case & Pièges <un nom="edge-case--pièges"></a>

Piège
- Oui.
**Débordement entier en comparaison**= Utilisez 64 bits (`long long`/`long`) pour calculer `d[a] * t[b]` et `d[b] * t[a]`. Autres
**La division de conseil**="(h + puissance - 1) / puissance" est l'astuce standard. Autres
**Tendance par rapport en Python**=Éviter la comparaison en points flottants; utiliser `functools. cmp_to_key`. Autres
**Tients en rapport**=Tout ordre fonctionne; si une sortie déterministe est nécessaire, briser les liens par index. Autres
**Large n**=Conserver l'utilisation de la mémoire faible; ne pas stocker plus d'entiers O(n). Autres

---

- Oui. 7. Extraits de code (Java / Python / C++) <a name="code-extraits"></a>

- Oui. Java (Java 17)

"Java
Importation de java.util.*;

solution de classe {
publique longue minDamage(int puissance, dommages int[], int[] santé) {
int n = longueur des dommages;
temps int[] = nouveau temps int[n];
pour (int i = 0; i < n; i++) {
temps[i] = (santé[i] + puissance - 1) / puissance; // ceil
}

Integer[] idx = nouveau Integer[n];
pour (int i = 0; i < n; i++) idx[i] = i;

Tableaux.sort(idx, a, b) -> {
longue gauche = (long) dommage[a] * temps[b];
long droit = (long) dommage[b] * temps[a];
si (à gauche) 0;
retour gauche > droite ? -1 : 1; // ordre décroissant
});

long total = 0;
longue durée de temps = 0;
pour (int id : idx) {
curTime += heure[id];
total += (long) dommage[id] * curTime;
}
le total des retours;
}
}
«» "

---

### Python (Python 3)

'`python
à partir de functools importer cmp_to_key

def minDamage(puissance, dommages, santé):
n = len(dommage)
temps = [(h + puissance - 1) // puissance pour h en santé] # ceil

def cmp(a, b):
gauche = dommages[a] * fois[b]
droite = dommage[b] * fois[a]
si gauche == à droite:
retour 0
retour -1 si gauche > droite autre 1 # rapport descendant

ordre = trié(range(n), key=cmp_to_key(cmp))

total, durée = 0, 0
pour i en ordre:
_temps += heures[i]
Total += endommagement[i] *
retour total
«» "

---

### C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue minDamage(pouvoir int, vecteur<int>&dommage, vecteur<int>&santé) {
int n = endommagement.size();
vecteur<int> t(n);
pour (int i = 0; i < n; ++i)
t[i] = (santé[i] + puissance - 1) / puissance; // ceil

vecteur<int> idx(n);
(idx.begin(), idx.end(), 0);

Tri(idx.begin(), idx.end(), [&](int a, int b) {
longue gauche = 1LL * dommages[a] * t[b];
long droit = 1LL * dommage[b] * t[a];
retour gauche > droite; // rapport descendant
});

long an = 0, cur = 0;
pour (int id : idx) {
cur += t[id];
ans += 1LL * dommages[id] * cur;
}
le retour des an;
}
};
«» "

---

- Oui. 8. Le Bon, le Mauvais et le Méchant <un nom, le bon, le mauvais et le mauvais></a>

Les bons
- **Simplicité**: Une fois que vous le reconnaissez est un problème de planification pondéré, la solution est un seul tri `O(n log n)`.
- **Réutilisabilité**: Des comparateurs personnalisés apparaissent dans de nombreux problèmes d'entrevue.
- **Déterministe**: La réponse est garantie optimale; aucun retour en arrière nécessaire.

- Oui. Les mauvais
- **Coût gâtant**: Pour l'énorme `n`, l'étape `O(n log n)` domine, mais il n'y a aucun moyen de l'entourer (sauf si vous utilisez des seau-sorts, qui sont rarement attendus).
- **Potentiel confusion**: Les débutants pourraient penser qu'ils peuvent finir leurs ennemis plus rapidement en les commutant, ce qui conduirait à une complexité exponentielle.

- Oui. L'Ugly
- **Tentes de suroptimisation**:
*Échanger des ennemis mi-attaque* → vous finissez par écrire un énorme DP qui ne paie jamais.
*L'utilisation des files d'attente prioritaires* → complique la solution.

La clé est de **verrouiller l'ordre** une fois que la règle de ratio est appliquée et puis juste simuler les attaques.

---

- Oui. 9. Autres approches et variantes <un nom="autres approches-variantes"></a>

Quand il est utile
-- -- -- -- -- -- -- -- --
Si les contraintes étaient petites (n ≤ 20), vous pourriez blesser la force ou utiliser DP sur les permutations. Autres
**Greedy with min-heap**= Quand les ennemis peuvent avoir la variable `puissance` ou la santé dynamique; vous avez besoin de réévaluer le rapport après chaque attaque. Autres
**Traitement de la peau**= Si le rapport "dommage / t" est limité par un petit entier (par exemple, ≤ 10), vous pouvez trier le seau en O(n). Autres
**Attaques paralléliennes**= Ne s'applique pas ici; mais si Bob pouvait attaquer plusieurs ennemis par seconde, le modèle change pour *processeur multiple*. Autres

---

- Oui. 10. Take-away pour les entrevues et votre chasse à l'emploi <a name="take-away-for-interviews--votre-chasse à l'emploi"></a>

1. **Identifiez le modèle** – Le temps d'achèvement pondéré apparaît dans l'horaire, l'horaire d'emploi, et de nombreux problèmes de coût minimum.
2. ** Expliquez votre raisonnement** – Parlez à travers pourquoi terminer un ennemi avant l'autre est toujours optimal.
3. **Afficher le comparateur** – Écrire une comparaison personnalisée en Java/C++ ou utiliser `cmp_to_key` en Python.
4. **Poignez de grands nombres** – Posez toujours des questions claires sur les types de données; faites preuve de sensibilisation au débordement.
5. **Complexité temporelle et spatiale** – Gardez la discussion précise ; les intervieweurs adorent vous voir quantifier.

Lorsque vous résolvez ce problème, vous n'écrivez pas seulement du code – vous montrez l'intervieweur que vous pouvez:

- Reconnaître un modèle algorithmique classique.
- Appliquer avec soin les contraintes.
- Fournir une solution propre et efficace en plusieurs langues.

---

## 11. Conclusion <un nom="conclusion"></a>

LeetCode 3273 est un brillant exemple d'élégance algorithmique** : un scénario simple et réel distillé dans le problème classique du temps d'achèvement pondéré*.
Par:

1. Calcul du temps d'attaque `ti` pour chaque ennemi.
2. Tri des ennemis par le rapport `di / ti`.
3. Accumuler les dommages avec une seule passe,

vous obtenez la réponse optimale en **O(n log n)** temps.

N'oubliez pas d'utiliser des entiers 64 bits, d'éviter le travail inutile en point flottant et de ne jamais interférer les attaques, à moins que vous ne fassiez quelque chose de faux*.

Avec cette compréhension, vous allez répondre à la question sur **LeetCode**, impressionner vos gestionnaires d'embauche, et déplacer un pas plus loin pour obtenir votre emploi de rêve! C'est ce qu'il a dit.

---

Codage heureux ! (en milliers de dollars)