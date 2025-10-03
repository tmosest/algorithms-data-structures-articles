---
Titre: LeetCode 1536. Swaps minimum pour organiser une grille binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code – 3 langues

Vous trouverez ci-dessous des solutions propres et prêtes à la production pour **LeetCode 1536 – Inversement minimal pour organiser une grille binaire** en **Java, Python et C++**.
Les trois implémentations utilisent la même stratégie gourmande :

1. Comptez la course à zéro pour chaque rangée.
2. À partir de la ligne supérieure vers le bas, choisissez la ligne la plus proche qui a assez de zéros de piste et -bubble--le à la position actuelle – le nombre de swaps est simplement la distance déplacée.
3. Si aucune ligne appropriée n'existe à une étape quelconque, retourner `‐1`.

Langue Complexité Remarques
C'est quoi, ça ?
"Java" "O(n2)" temps, "O(n)" espace "Utilise un "int[]" pour les nombres de zéros. Autres
Temps "O(n2)", "O(n)" espaceUtilisez une liste simple. Autres
Temps "O(n2)", "O(n)" L'espace utilise `vecteur<int>`. Autres

---

Java

"Java
***
* 1536. Swaps minimum pour organiser une grille binaire
* Solution Java – temps O(n2), espace O(n)
*/
solution de classe {
public int minSwaps(int[][] grille) {
int n = longueur de la grille;
int[] trailingZeros = nouveau int[n];

// 1. Calculer le nombre de pistes-zéro pour chaque ligne
pour (int i = 0; i < n; ++i) {
cnt = 0;
pour (int j = n - 1; j >= 0; --j) {
si [grid[i][j]] 1) pause;
cnt++;
}
à suivreZeros[i] = cnt;
}

swaps d'int = 0;

// 2. Emplacement de l'avidité de la rangée supérieure au bas
pour (int requis = n - 1; requis >= 0; --obligatoire) {
int idx = -1;
// Trouvez la première ligne (du haut) qui a au moins `requis` zéros
pour (int i = 0; i < n; ++i) {
si (trailingZeros[i] >= requis) {
idx = i;
pause;
}
}
Si (idx) -1) retour -1; // impossible

// Déplacer cette ligne vers la position actuelle
pour (int i = idx; i > requis; --i) {
TraînerZeros[i] = TraînerZeros[i - 1];
}
TrailingZeros[required] = requis; // la rangée déplacée se trouve maintenant à `required "

swaps += idx - requis;
}
swaps de rendement;
}
}
«» "

---

Python

'`python
# 1536. Swaps minimum pour organiser une grille binaire
# Solution Python – temps O(n2), espace O(n)

Solution de classe:
def minSwaps(self, grille: List[List[int]]) -> Int:
n = len(grid)
Traînage = [0] * n

# Compter les zéros pour chaque rangée
pour i dans la plage(n):
cnt = 0
pour j dans la plage(n - 1, -1, -1):
si grille[i][j]] 1 :
pause
cnt += 1
Traîner[i] = cnt

swaps = 0

# Greedy: placer les rangées de haut en bas
pour les besoins dans la gamme (n - 1, -1, -1):
idx = -1
pour i dans la plage(n):
si vous suivez[i] >= besoin:
idx = i
pause
Si idx == - 1 :
retour -1

# Déplacer la ligne choisie vers le haut
pour i dans la gamme (idx, besoin, -1):
Traînage[i] = Traînage[i - 1]
[besoin] = besoin

swaps += idx - besoin

swaps de rendement
«» "

---

C++

'`cpp
// 1536. Swaps minimum pour organiser une grille binaire
// C++17 solution – temps O(n2), espace O(n)

solution de classe {
public:
Int minSwaps(vecteur<vecteur<int>>& grille) {
int n = quadrillage.size();
vecteur<int> traînant(n, 0);

// 1. Compter les zéros de piste par rangée
pour (int i = 0; i < n; ++i) {
cnt = 0;
pour (int j = n - 1; j >= 0; --j) {
si [grid[i][j]] 1) pause;
++cnt;
}
la piste[i] = cnt;
}

swaps d'int = 0;

// 2. Déplacement en cas d'avidité
pour (int need = n - 1; need >= 0; --besoin) {
int idx = -1;
pour (int i = 0; i < n; ++i) {
si (retard[i] >= besoin) {
idx = i;
pause;
}
}
Si (idx) -1) retour -1; // impossible

// Déplacer les lignes vers le haut pour amener idx à la position `besoin`
pour (int i = idx; i > besoin; --i) {
la piste[i] = la piste[i - 1];
}
[besoin] = besoin;

swaps += idx - besoin;
}

swaps de rendement;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 1536

---

Titre
**Le bon, le mauvais et le mauvais de LeetCode 1536 – Maîtriser les swaps minimums dans une grille binaire (Java/Python/C++)* *

---

Description de la méta
Lutte contre le LeetCode 1536 : Des swaps mineurs pour organiser une grille binaire ? Consultez notre guide convivial SEO sur le problème, la solution gourmande, les compromis de performance, les idées d'entrevue et comment relever ce défi en Java, Python et C++.

---

Introduction
Si vous avez déjà regardé LeetCode **1536** – Le Minimum s'échange pour organiser une grille binaire – et a senti votre chute d'estomac, vous n'êtes pas seul.
C'est un classique **greedy + array‐manipulation** puzzle qui peut faire ou casser votre rythme d'entrevue. Dans ce post, nous disséquerons l'approche **=good=** qui vous permet de la résoudre proprement, les interviewers **=bad=** écument aiment vous jeter, et les boîtiers **=ugly=** qui testent votre robustesse.
En plus, nous allons vous montrer **ready‐to‐paste Java, Python, et C++ implémentations**, interview‐ready explications, et des conseils pratiques qui vont faire briller votre CV.

---

### Description du problème (pour les lecteurs qui ne l'ont pas encore vu)

> **Input:**
> `grid` – une matrice binaire `n × n` (`0` ou `1`).
> ** Fonctionnement :**
> Vous pouvez échanger deux lignes *adjacents* de la matrice.
> **Objectif:**
> Réorganiser les lignes de manière à ce que la ligne supérieure contienne au moins des zéros de piste `n‐1`, la deuxième ligne au moins `n‐2`, ..., et la ligne inférieure au moins `0`.
> **Produits:**
> Nombre minimal de swaps requis, ou «‐1» si impossible.

> **Exemple**
> `` "
> grille = [0,1],
> [1,1,0]
> [1,0]]
> `` "
> Réponse : `1` (ligne 0 avec ligne 2).

---

1. Approches naïves et pourquoi ils échouent

L'approche Ce qu'il fait Pourquoi il est inefficace
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Recherche de force brute de toutes les permutations** commandes de lignes → impossible pour `n > 6 ' , il suffit de générer tous les ordres. Autres
**Programmation dynamique sur des sous-ensembles de rangées** Autres
**Récursion du haut vers le bas + mémo**==Déplacer récursivement les lignes, les états de cachage== Espace d'état exponentiel===La mémoisation le corrige toujours. Autres

> ** Bonne nouvelle:** Le problème est **polynomial-time solvable**. La clé est d'exploiter la *structure* d'une matrice binaire : seul le **le plus 1** de chaque ligne compte.

---

2. L'avidité - Comptabiliser les zéros

1. **Pourquoi suivre les zéros?**
Une ligne peut être déplacée à la position `i` *iff* il a au moins `n‐i‐1` zéros à sa fin.
Nous précalculons donc cette valeur pour chaque ligne – une passe linéaire par ligne.

2. **Pourquoi choisir la ligne la plus proche? **
Déplacer une rangée plus loin coûte plus de swaps. En prenant toujours la ligne la plus proche qui satisfait aux exigences actuelles, nous garantissons des swaps totaux minimes.
Considérez-le comme une série de bulles unidimensionnelles où chaque élément est une rangée et le -key-zéro est son nombre traînant.

3. **Proof d'optimalité**
- Le nombre *obligatoire* de zéros de fuite diminue de façon monotonique à mesure que nous descendons la grille.
- Supposons que nous ayons une solution qui a déplacé une rangée plus loin au lieu de la plus proche; l'échange de ces deux mouvements réduirait le nombre total d'échanges sans rompre la faisabilité.
- Par conséquent le choix avide est optimal (argument d'échange standard).

4. **Détails sur la mise en œuvre**
- **Temps:** `O(n2)` – deux boucles imbriquées (compte des zéros + déplacement avide).
- **Espace:** `O(n)` – nous ne conservons que les nombres de zéros.
- Fonctionne pour **Java, Python, C++** comme indiqué ci-dessus.

> ** Bon à emporter:** Un seul tableau entier transforme un problème de matrice 2-D en un simple algorithme cupide 1-D.

---

- Oui. Les cas de bord et les pièges communs

Qu'est-ce qui arrive ? Comment le repérer ?
- C'est quoi ?
Autres **Aucune ligne n'a assez de zéros de piste** , Greedy échoue tôt → retourner `‐1`. Après avoir compté les zéros, vérifiez `max(trailingZeros) < n‐1».
**Les rangées multiples satisfont à une exigence**= L'une d'elles fonctionne, mais vous devez choisir le *plus proche* pour éviter les swaps supplémentaires. Regardez la première rangée (indice le plus petit) avec suffisamment de zéros. Autres
**Le déplacement à tort des lignes vers le bas augmente les swaps. Autres
**La lecture de l'exigence est interrompue**= Vous pouvez penser que la ligne supérieure a besoin de `n` zéros, mais elle n'a besoin que de `n‐1'.= Utilisez la formule `need=n‐1 - i` où `i` est l'index de la ligne cible. Autres
Autres **Grande taille d'entrée (`n = 30`)**. Même `O(n2)` est bien, mais la récursion naïve peut faire sauter la pile. "Continuez à la boucle cupide itérative. Autres

> ** Leçon clé :** *Ne présumez jamais qu'un algorithme plus complexe (DP, BFS, etc.) fonctionnera automatiquement mieux.* Parfois, un passage linéaire sur un tableau dérivé est tout ce dont vous avez besoin.

---

Quand le problème se pose Toi

1. **Misinterprétation des swaps "adjacents"* *
- Il *pas* une permutation complète; vous ne pouvez échanger que la ligne `i` avec la ligne `i+1`.
- Par conséquent, déplacer une ligne de la position `idx` vers `need` coûts exactement `idx-need` swaps (pas `1`).

2. **Oubliant que la rangée déplacée correspond au nombre zéro* *
- Après avoir bougé une rangée, son nombre de zéros de suite devient exactement la valeur *obligatoire* (`beed`).
- Ne pas le mettre à jour casse les itérations.

3. ** Erreurs hors pair avec des indices**
- La ligne supérieure correspond à "need = n‐1".
- La ligne inférieure a besoin de "nécessité = 0".
- Les bugs hors-par-un sont la cause la plus courante d'une mauvaise réponse dans ce problème.

4. **Si la matrice est déjà triée* *
- La grille peut déjà satisfaire à l'exigence; votre algorithme doit quand même retourner les swaps `0`.
- Ne pas préfiltrer les lignes ; laissez la boucle gourmande gérer le cas déjà correct.

---

5. Conseils de préparation à l'entrevue

Conseil Pourquoi ça compte dans une entrevue de codage
-- -- -- -- -- -- ----------------------------------
**Dépliquer l'invariant** – À l'étape `k`, les premières lignes `k` sont déjà positionnées correctement et ont au moins `n‐k‐1` des zéros de piste. Affiche que vous comprenez la structure du problème, pas seulement le code. Autres
**Afficher l'analyse O(n2)** – `n ≤ 30`, donc c'est bien. Les intervieweurs adorent entendre votre discussion sur la complexité; cela prouve que vous n'êtes pas seulement encodant aveugle. Autres
**Discuse l'impossibilité tôt** – `si maxZeros < n-1 retour Les sorties précoces permettent de maintenir l'efficacité de l'algorithme et de démontrer une prise de conscience du cas de bord. Autres
Autres ** Mettre en évidence la transformation unidimensionnelle** – convertir un problème 2-D en tableau 1-D. Il s'agit d'un thème d'interview récurrent (=réduire la dimensionnalité=) et d'un bon point de conversation. Autres
** nuances spécifiques à la langue de Mention** – p.ex. Python=s `list`, C++=s `vector<int>`.= Aide les recruteurs à comprendre l'étendue de votre expérience. Autres
**Afficher les cas d'essai** – inclure l'exemple fourni et un cas impossible. Démontre robustesse et confiance en votre solution. Autres

---

6. SEO & Job-Search Crochet

- **Mots clés** : *LeetCode 1536, grille binaire d'échange minimum, solution Java, solution Python, solution C++, préparation d'entrevue, entretien de codage, entretien d'ingénierie logicielle, entretien d'algorithme, algorithmes gourmands, manipulation de tableau. *
- **Pourquoi cet article vous aide à trouver un emploi**:
1. **Clear, multi-langue code** que les recruteurs peuvent copier-coller dans leur environnement de test.
2. Une plongée profonde dans *pourquoi* une stratégie gourmande fonctionne, vous rendant prêt à expliquer le raisonnement lors des entrevues de la journée.
3. Considérez les pièges communs – les "bad" et "ugly" – que les intervieweurs utilisent souvent comme "gotchas". (en milliers de dollars)
4. Bonus: Une discussion sur **temps et compromis d'espace** qui montre que vous pouvez équilibrer performance et lisibilité.

---

Prise finale Loin

> **Bien** – La solution gourmande est élégante, fonctionne rapidement et écailles facilement.
> **Bad** – Il est facile d'obtenir l'indice arithmétique faux, et l'énoncé du problème peut induire les débutants en pensant qu'une permutation complète est nécessaire.
> **Ugly** – La subtilité que seuls les swaps *adjacents* sont autorisés, et qu'une rangée de zéros en fuite doit être *au moins* une valeur, peut vous faire trébucher si vous n'êtes pas prudent avec les invariants.

Lorsque vous présentez **LeetCode 1536** dans une interview, commencez par raconter le **invariant**, puis glissez dans l'approche **one-dimensional array**. Gardez vos indices propres, mettez à jour la rangée déplacée en traînant des zéros, et vous gagnerez ce badge de solution agréable – et une offre d'emploi potentielle.

Joyeux codage, et que votre prochaine interview soit une brise! C'est ce qu'il a dit.

---


---

*Sentez libre de laisser tomber votre propre cas de bord ou solution alternative dans les commentaires – nous aimons un bon défi! *