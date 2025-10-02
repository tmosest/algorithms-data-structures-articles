---
titre: LeetCode 1067. Nombre de chiffres dans la gamme -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 1067 – **Compte de Digit à portée* *
**Problème** Nombre(int d, int bas, int haut) "
C'est difficile.

> **Objectif** – Pour un seul chiffre `d (0‐9)` et une plage inclusive `[faible, élevée]`, retourner le nombre total de fois `d` apparaît dans les représentations décimales de chaque entier dans cette plage.
> **Constraints** – «1 ≤ faible ≤ élevé ≤ 2·108» (= 200 millions).

Comme la plage d'entrée peut être énorme, une boucle naïve (`pour (int i=low;i<=high;i++)...) serait beaucoup trop lente. La solution standard utilise **digital‐DP** – une technique de programmation dynamique qui traite les chiffres décimaux d'un nombre du plus significatif au moins significatif tout en gardant la trace des états « étanches » et « leader-zéro ».

Vous trouverez ci-dessous des implémentations de travail, annotées dans **Java, Python et C++** qui fonctionnent dans le temps `O(log N)` et la mémoire `O(log N)`.

---

- Oui. 2. Mise en œuvre Java (Digit-DP)

"Java
***
* LeetCode 1067 – Nombre de chiffres dans la gamme
*
* Java 17, temps O(log N), mémoire O(log N)
*/
solution de classe {
// Tableau de mémorisation : pos x count
mémo privé int[];
cible privée int; // chiffre que nous comptons
char privé[] chiffres; // représentation en chaîne du nombre courant

Nombres d'entrées publiques Nombre(int d, int bas, int haut) {
Ça. cible = d;
le compte de retour à (élevé) - compte à (faible - 1);
}

*** Nombre d'occurrences de la cible dans [0, n] */
Int privé countUpTo(int n) {
si (n < 0) retour 0; // garde pour le bas-1
chiffres = entier.àString(n).àCharArray();
int len = chiffres. longueur;
mémo = nouvelle int[len][len]; // occurrences maximales <= len
pour (int[] ligne : mémo) Arrays.fill(row, -1);
retour dp(0, 0, vrai, faux);
}

***
* @param pos indice actuel en chiffres[]
* @param cnt nombre de chiffres cibles vus à ce jour
* @param étroitement si les chiffres précédents correspondaient au préfixe de n
* @param a commencé si nous avons placé un chiffre zéro non leader
* @retour total des occurrences à chiffres cibles de cet état vers l'avant
*/
Int privé dp(int pos, int cnt, booléen serré, booléen commencé) {
si (pos == chiffres.longueur) retourne cnt; // fin du nombre
si (!tight && started && memo[pos][cnt] != -1) // bouton cache
retourner mémo[pos][cnt];

int limite = serré ? chiffres [pos] - '0' : 9;
= 0;

// Option 1: sauter cette position (toujours en tête des zéros)
si (!started) total += dp(pos + 1, cnt, false, false);

début int Chiffre = commencé ? 0 : 1; // aucun zéro de début autorisé après le début
pour (int d = startDigit; d <= limite; d++) {
Int nouveau Cnt = cnt + (d == cible ? 1 : 0);
boolean newTight = serré && (d == limite);
total += dp(pos + 1, newCnt, newTight, true);
}

si (!tight && started) mémo[pos][cnt] = total;
le total des retours;
}
}
«» "

- Oui. Comment ça marche

Étape Que se passe-t-il ?
C'est pas vrai.
`digetsCount`= Calls helper for `high` and `low-1`, puis soustrait. Autres
"countUpTo" Convertit `n` en tableau de caractères, prépare le mémo, appelle `dp`. Autres
"dp" explore récursivement tous les chiffres possibles à la position "pos". Autres
"(pos, cnt, serré, commencé)" Autres
Mémorisation Obtenir des résultats pour les états *non étanches* afin d'éviter la recomputation. Autres

Les visites de l'algorithme à tout le plus des états `len * len` (`len ≤ 10` pour 2·108), donc il est pratiquement constant temps.

---

- Oui. 3. Mise en œuvre de Python (PDD d'une seule ligne)

'`python
Code Leet 1067 – Nombre de chiffres dans la gamme
# Python 3.11, temps O(log N), mémoire O(1) (en utilisant explicitement les limites de récursion)
Solution de classe:
chiffres Compte(s), d: int, faible: int, élevé: int) -> Int:
retour self.f(high, d) - self.f(low - 1, d)

def f(self, n: int, cible: int) -> Int:
si n < 0: retourner 0
s = str(n)
m = len(s)
mémo = [[-1] * (m + 1) pour _ dans l'intervalle(m)]

def dp(i: int, cnt: int, serré: bool, commencé: bool) -> Int:
Si i == m:
retour cnt
si pas serré et commencé et mémo[i][cnt] != - 1 :
retour de mémo[i][cnt]
up = int(s[i]) si elle est serrée 9
Res = 0
si non démarré:
res += dp(i + 1, cnt, false, false)
pour creuser dans range(0 si commencé ailleurs 1, jusqu'à + 1):
res += dp(i + 1, cnt + (dig= cible), serré et dig=up, Vrai)
si pas serré et commencé:
mémo[i][cnt] = res
retour res

retour dp(0, 0, vrai, faux)
«» "

> **Pourquoi Python fonctionne** – La profondeur de récursion de Python peut gérer 10 niveaux (maximum des chiffres).
> **Espace** – "memo" est au plus `10 × 10`.
> **Heure** – Toujours "O(log N)".

---

- Oui. 4. Mise en œuvre C++ (Bottom-Up Digit DP)

'`cpp
// Code Leet 1067 – Nombre de chiffres dans la gamme
// C++17, temps O(log N), mémoire O(log N)
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombres int Nombre(int d, int bas, int haut) {
cible = d;
le compte de retour à (élevé) - compte à (faible - 1);
}

particulier:
cible int;
les chiffres du vecteur<int>;
vecteur<vector<int>> mémo; // mémo[pos][cnt]

Int countUpTo(int n) {
si (n < 0) retourner 0;
chiffres.clair();
pendant que (n) { nombres.push_back(n % 10); n /= 10; }
inverse(digets.begin(), digets.end()); // la plus importante en premier
int len = chiffres.size();
mémo.assign(len, vector<int>(len + 1, -1));
retour dfs(0, 0, vrai, faux);
}

int dfs(int pos, int cnt, bool serré, bool commencé) {
si (pos) nombres.size() retourne cnt;
si (!tight && started && memo[pos][cnt] != -1) retourner mémo[pos][cnt];

int limite = serré ? chiffres[pos] : 9;
int res = 0;

si (!started) res += dfs(pos + 1, cnt, false, false); // sauter en tête zéro

début int Chiffre = commencé ? 0 : 1;
pour (int dig = début) Chiffre; creuser <= limite; ++dig) {
res += dfs(pos + 1, cnt + (dig == cible), limite serrée && dig ==, true);
}

si (!tight && started) mémo[pos][cnt] = res;
retour rés;
}
};
«» "

> **Différences clés** – Utilise un vecteur explicite pour les chiffres, la récursion ascendante (pas de lambdas).
> **Complexité** – Identique à Java/Python: temps `O(log N)`, mémoire `O(log N)`.

---

- Oui. 5. Article de blog – Le bon, le mauvais, le lamentable de Digit‐DP sur LeetCode 1067

> **Mots-clés**: LeetCode 1067, Chiffre Count in Range, chiffres DP, questions d'entretien de programmation dynamique, entretien d'emploi, ingénieur logiciel, solution Java, solution Python, solution C++, entretien de codage, conception d'algorithmes

5.1 Le problème dans une coquille de noix

LeetCode 1067 vous demande de compter combien de fois un seul chiffre apparaît dans un énorme intervalle entier. L'entrée peut atteindre 200 millions, mais vous devez terminer en moins d'un milliseconde. À première vue, une boucle de force brute semble être la réponse naturelle : il suffit d'itérer et de convertir chaque entier en chaîne, mais cela nécessiterait *des centaines de millions de conversions de chaînes*, impossibles dans une entrevue ou un défi de codage.

Il s'agit des chiffres de comptage classiques dans une plage de problème. La solution élégante est *digit‐DP* – une approche de programmation dynamique qui traite le problème comme une traversée des chiffres décimaux des nombres limites.

5.2 Les bonnes – Pourquoi les chiffres DP est la norme or

Autres Pourquoi il brille
C'est quoi ?
**Temps optimum**= Exécute en `O(log N)` par requête (=10 chiffres pour `2·108`). Autres
**Simplicité avec récursion**= Chaque étape de récursion gère un seul chiffre; l'état est minuscule: position, compter jusqu'à présent, drapeau serré, drapeau leader-zéro. Autres
**Réutilisable à travers les problèmes** DP, vous pouvez résoudre une foule de problèmes: nombres de nombres avec une somme donnée de chiffres, nombres divisibles par K, palindromes de nombre dans la gamme, etc. Autres
La taille de la table de mémorisation est « chiffres × chiffres » (= 100 entiers). Autres

> **Conseil d'entrevue** – Présentez d'abord le diagramme d'état. Montrez qu'il n'y a que 4 états logiques: `standard` (préfixe égal à la limite) et `started` (si nous avons placé un chiffre non zéro). Cela rend la récursion évidente.

5.3 Les mauvaises – Pièges communs et comment les éviter

1. **Leading Zeros** – Le fait d'oublier de traiter les zéros de tête provoque particulièrement une surestimation des chiffres en nombres comme `0013`.
*Solution*: Ajouter un drapeau `démarré`; compter `cible` seulement si `démarré` est vrai, sinon sauter.

2. **Off‐by‐One sur Gammes** – De nombreuses solutions soustractent `count(low-1)` mais oublient que `low-1` peut être `0`.
*Solution*: Ajouter garde `si (n < 0) retourner 0;` dans l'aide.

3. **Conditions de mémorisation** – Stocker les résultats pour les états *tight* est erroné parce que la limite supérieure change par appel.
*Solution*: Mémo seulement pour `!tight && started`.

4. **Profondeur de récursion** – Dans les langues avec des limites de récursion peu profondes (p. ex. Python 2), `sys.setrecursionlimit` peut être nécessaire.
*Solution*: Dans Python, la profondeur de récursion n'est que de 10 pour ce problème, mais définissez la limite de toute façon si vous généralisez.

5. **Wrong Digit Order** – La conversion d'un nombre en une chaîne de caractères par rapport à la construction d'un tableau de chiffres du plus petit au plus petit peut retourner la signification de `pos`.
*Solution*: Standardiser sur **la plus importante d'abord**; il simplifie la logique du drapeau `tanche`.

#### 5.4 Les horribles – les cas de bord qui voyagent même les experts

Pourquoi il est méchant
- Oui.
**d = 0**.Les zéros de tête ne sont jamais comptés, donc 0 apparaît seulement en nombres comme 10, 20... mais *pas* comme le chiffre de tête de 100. Autres Conserver le drapeau `démarré`; compter `cible` seulement lorsque `démarré`. Autres
Autres **La marge comprend 1**=1 `low = 1` donne `high-low+1=1` entier, mais l'aide fonctionne toujours parce que `countUpTo(0)` est 0.=1 Pas de changement – le `countUpTo(low-1)` garde le gère. Autres
**high = 2·108**. Les chiffres à 9 chiffres, mais certaines langues traitent 200 000 000 comme 9 chiffres. Convertir en chaîne ou utiliser la boucle de division; ils donnent tous deux la bonne longueur. Autres
**cible = 0 et nombre = 0** Certaines solutions sautent à tort le compte en raison du drapeau `started`. 0', retour 1.

#### 5.5 SEO— Résumé optimisé pour les demandeurs d'emploi

> **Si vous vous préparez à une entrevue de génie logiciel, maîtrisez le chiffre DP ne résout pas seulement LeetCode 1067 en millisecondes, mais démontre aussi une pensée algorithmique profonde. **
> **Affichage d'une implémentation propre de Java, Python ou C++ DP** impressionnera les intervieweurs qui s'attendent à ce que vous traitiez efficacement les problèmes de gros intrants.
> **Au-delà du LeetCode, les concepts numériques-DP apparaissent dans les scénarios réels** – algorithmes de cotation, comptage combinatoire dans l'analyse et même dans la construction d'index de recherche efficaces.

**Traitements clés pour le CV:**

- * Programmation Dynamique :* Expertise éprouvée dans les modèles DP.
- * Optimisation de la complexité du temps :* Solutions fournies dans la rubrique "O(log N)".
- *Langue de la croix Compétence* Java, Python, solutions C++ avec la même logique.
- *Résoudre les problèmes:* Répondez rapidement à des questions d'entrevue difficiles comme le compte Digit dans Range.

Utilisez l'expression « conception d'algorithme Digit‐DP »** dans la section compétences; les recruteurs l'utilisent souvent comme un filtre à mots clés.

---

- Oui. 6. Clôture

Les solutions ci-dessus sont prêtes à copier-coller dans votre IDE ou votre plateforme de codage. Lorsque vous les présentez dans un entretien, marchez à travers la machine d'état, expliquez la manipulation des zéros de tête, et soulignez le drapeau `étanchéité`. Cette narration, couplée à l'élégant code récursif, laissera les intervieweurs convaincus que vous êtes un candidat fort pour n'importe quel rôle d'ingénierie logiciel. C'est ce qu'il a dit.

---

*Bon code ! *