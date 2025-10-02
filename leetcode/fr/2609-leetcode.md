---
titre: LeetCode 2609. Trouvez la sous-chaîne la plus équilibrée d'une chaîne binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2609 – Trouver la sous-chaîne la plus équilibrée d'une chaîne binaire

> **Titre**
> 2609. Trouvez la sous-chaîne la plus équilibrée – Java / Python / C++ Implementation + SEO‐Optimized Blog Post

---

Récapitulation des problèmes

On vous donne une chaîne binaire **`s`** (`0`s et `1`s seulement).
Une sous-chaîne **équilibrée** est une tranche contiguë de «s» où:

* Tous les `0`s viennent *avant* aucun `1` (pas `0` après un `1`).
* Le nombre de `0`s correspond au nombre de `1`s.

La sous-chaîne vide est considérée comme équilibrée (longueur 0).
Retourne la longueur *maximum* de toute sous-chaîne équilibrée.

**Exemples**

La plus longue sous-chaîne équilibrée
- C'est quoi ?
Nombre d'unités
Télécopie:
111 (vide)

**Contrôles* *

* `1 <= longueur <= 50`
* `s[i] ─ {'0','1'} "

Autres Vous pouvez résoudre cela en **O(n)** temps avec deux compteurs simples – un grand tour convivial d'entrevue!

---

- Oui. Pourquoi une stratégie de contre-pointeur fonctionne-t-elle?

Parce que la chaîne équilibrée doit ressembler à "00...011...11"`, nous pouvons scanner de gauche à droite:

1. **Count menant `0`s** – laissez-le être `cnt0`.
2. **Après le premier `1` apparaît**, continuez à compter `1`s – laissez-le `cnt1`.
3. Chaque fois qu'un nouveau bloc de `0`s commence (après que nous ayons déjà compté quelques `1`s), nous **reset** `cnt0` et `cnt1` et recommencer.

La longueur d'une sous-chaîne équilibrée se terminant à n'importe quel indice est "2 * min(cnt0, cnt1)" parce que le plus petit des deux nombres limite le nombre de paires que nous pouvons former.

Cette seule passe nous donne la réponse en **O(n)** temps et **O(1)** espace supplémentaire.

---

- Oui. Mise en œuvre

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

#### 3.1 Java

"Java
solution de classe {
public int find La plus longue Solde Sous-chaîne(String s) {
Int maxLen = 0;
= 0;

pour (int i = 0; i < s.longueur(); i++) {
char ch = s.charAt(i);

si (ch == '0') {
// Si nous avons déjà vu des '1', nous devons réinitialiser.
si (one > 0) {
zéros = 1;
ceux = 0;
} autre {
zéros++;
}
} autres { // ch == '1 '
si (zéro > 0) {
les++;
} autre {
// Un '1' avant un '0' ne peut pas former une sous-chaîne équilibrée
zéros = 0;
ceux = 0;
}
}

maxLen = Math.max(maxLen, 2 * Math.min (zéros, ceux));
}

retour maxLen;
}
}
«» "

> **Bien**: Un passage, pas de tableaux auxiliaires, facile à lire.
> **Bad**: La logique de réinitialisation est un peu verbeuse – un petit bug peut s'infiltrer.
> **Ugly**: Si vous oubliez les `ones > 0` garde, vous autorisez incorrectement `0` après un bloc de `1`s.

---

3.2 Python

'`python
Solution de classe:
def findTheLongestBalancedSubstring(self, s: str) -> Int:
max_len = 0
zéros = 0

pour ch en s:
si ch == '0':
si:
# nouveau bloc de zéros après certains -> réinitialiser
zéros, ceux = 1, 0
Sinon:
zéros += 1
Sinon : # ch == '1'
si zéros:
+= 1
Sinon:
zéros = 0

max_len = max(max_len, 2 * min(zéros, ceux))

_retourner maxlen
«» "

> **Bien**: Pythonique, clair, aucune pénalité pour compte de ligne.
> **Bad**: Toujours en s'appuyant sur une réinitialisation manuelle, peut être moins évident pour les nouveaux arrivants.
> **Ugly**: Oublier de réinitialiser `ones` lors du démarrage d'un nouveau bloc `0` peut conduire à des résultats incorrects.

---

### 3.3 C++

'`cpp
solution de classe {
public:
int trouver La plus longue bataille Sous-chaîne(chaîne s) {
int maxLen = 0, zéros = 0, ceux = 0;

pour (charte : s) {
si (ch == '0') {
si (ones) { // nouveau bloc de zéros après ceux
zéros = 1;
ceux = 0;
} autre {
+ zéros;
}
} autres { // ch == '1 '
si (zéro) {
+ones;
} autre {
zéros = ceux = 0; // tête 1 ne peut pas démarrer un bloc équilibré
}
}
maxLen = max(maxLen, 2 * min(zéros, ceux));
}
retour maxLen;
}
};
«» "

> **Bien**: boucles serrées, frais généraux variables minimes.
> **Bad**: La syntaxe C++=s `pour (char ch: s)` est moderne, mais peut faire monter les gens utilisés pour les boucles basées sur l'index.
> **Ugly**: Mélanger `++zeros` et `zeros = 1` peut être source de confusion – un commentaire aide.

---

Analyse de complexité

Heure de mise en œuvre
- Oui.
Java/Python/C++
La force brute (boucles neutralisées)

Avec `n ≤ 50`, toutes les solutions fonctionnent en microsecondes, mais l'approche linéaire est un modèle de meilleure pratique pour les intervieweurs.

---

C'est pas vrai. Tranche Liste de contrôle des cas

Qu'est-ce qu'il faut regarder
-- -- -- -- -- -- -- -- --
La chaîne commence par `1`. Autres
Plusieurs blocs de `0`s après un bloc de `1`s. Autres
Le résultat `0`s ou `1`s" est `0`. Autres
Empty substring (pas de paire → 0). Autres

---

# # # 6 Le bien, le mal, le mal de ce problème

Aspect du bien
- C'est quoi ?
**Limpidité conceptuelle**=La sous-chaîne équilibrée est une simple ligne de zéros, puis tous les motifs. L'exigence «comptes égaux» peut confondre certains. Une interprétation erronée de la sous-chaîne vide conduit à des cas de base erronés. Autres
**Une seule analyse linéaire, pas de structures de données supplémentaires. Autres La logique de réinitialisation peut paraître maladroite. Erreurs hors-par-un lors de la réinitialisation du compteur. Autres
**Difficulté de codage** Requiert une manipulation soigneuse des cas de bord. L'écriture de la réinitialisation dans un langage différent peut briser la logique. Autres
**L'appel à l'entrevue**= montre la compréhension de la technique à deux points.=Les intervieweurs peuvent demander pourquoi pas deux boucles imbriquées?= Impossible d'expliquer l'astuce de "min". Autres

---

Article de blog optimisé du SEO

> **Titre**
> 2609. Trouvez la sous-chaîne la plus équilibrée – Java, Python, C++ Solution + Conseils d'entrevue

> **Description détaillée**
> Maître LeetCode #2609 en quelques minutes. Apprenez une solution linéaire, comparez les implémentations Java/Python/C++ et obtenez des conseils pour l'entretien.

Aperçu du blog

1. **Intro** – Qu'est-ce qu'une sous-chaîne binaire équilibrée?
2. **Énoncé de problème** – Récapitulation rapide et exemples.
3. ** Force brute contre linéaire** – Pourquoi O(n) est préférable.
4. **L'algorithme O(n)** – Deux compteurs, réinitialisez la logique.
5. **Code complet en Java, Python, C++** – Extraits annotés.
6. ** Analyse de complexité** – Pourquoi ça compte dans les interviews.
7. **Pièges communs** – Cas de bord et réinitialiser les bogues.
8. **Bien, mal, mal** – Feuille de triche rapide pour les intervieweurs.
9. **À emporter** – Pourquoi ce problème met en évidence la conception d'algorithmes propres.
10. **Appel à l'action** – Essayez-le, commentez vos pensées, partagez sur LinkedIn.

### -Exemple de référencement amical

> **Trouver la sous-chaîne la plus équilibrée en O(n)* *
> Dans un monde où les intervieweurs aiment les solutions linéaires, le LeetCodeS 2609 vous défie de trouver la plus longue sous-chaîne où tous les zéros précèdent les unes, et les nombres correspondent. Une seule passe en utilisant deux compteurs résout cela en **O(n)** temps – parfait pour une entrevue de 30 minutes.
>
> **Java, Python, C++**
> L'algorithme est identique entre les langues; seulement les changements de syntaxe. Voir nos trois implémentations propres ci-dessous.
>
> **Pourquoi c'est une grande question d'entrevue* *
> 1. **Clarté conceptuelle** – Le motif de « bloc 0 » → 1 bloc est intuitif.
> 2. **Élégance algorithmique** – Pas de tableaux auxiliaires, juste deux int.
> 3. **Manipulation de cas d'Edge** – La logique de remise à zéro teste votre attention aux détails.
>
> **Prêt à passer la prochaine entrevue de codage? * *
> Implémentez la solution, testez les cas de bord et expliquez la logique du compte min à votre intervieweur. C'est un petit problème qui démontre la maîtrise des scans linéaires – un must-know pour toute entrevue d'ingénierie logicielle.

---

- Oui. Réflexions finales

* **Efficace du temps** – O(n) est optimal pour ce problème.
* **Efficacité spatiale** – Seulement deux compteurs entiers.
* **Portabilité** – La même logique fonctionne entre les langues.
* **Valeur d'entrevue** – Montre votre capacité à réduire un problème apparemment équilibré à un simple balayage.

• Pratiquez le code, ajoutez des tests unitaires pour les cas de bord (`"1"`, `"0"`, `"111000"`, etc.), et vous serez prêt à impressionner les recruteurs avec une solution propre et efficace!

---

Joyeux codage !
N'hésitez pas à laisser un commentaire ou à partager votre propre tour sur ce problème.