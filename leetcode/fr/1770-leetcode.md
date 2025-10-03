---
titre: LeetCode 1770. Score maximal des opérations de multiplication -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

LeetCode 1770 – Score maximal des opérations de multiplication
Temps O(m2), mémoire O(m2) *

Un problème qui semble simple à la surface mais est en fait une grande arme d'entretien. **M. Coder**

---

Table des matières
1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Pourquoi ce problème est une question d'entrevue *Must‐Know*](#Why-thi-problem-is-a-must‐know-interview-question)
3. [La bonne – l'approche claire et intuitive du PDD] (#la bonne approche claire et intuitive)
4. [Le mauvais – Que se passe-t-il si vous n'utilisez pas DP?](#le mauvais-qu'est-ce qu'il y a-si vous ne utilisez-dp)
5. [Les cas de bord et les pièges communs] (#les cas de bord et les pièges communs)
6. [Solution à travers](#solution à travers)
7. [Code Snippets](#code-snippets)
- [Java] (#Java)
- [Python] (#python)
- [C++](#c++)
8. [Comment l'expliquer dans une entrevue (et la terre qui travaille)] (#comment l'expliquer dans une entrevue)
9. [SEO checklist – Faites sortir votre blog](#seo-checklist)
10. [TL;DR](#tl-dr)

---

Récapitulation des problèmes

> **Don**
> * `nums[0 ... n-1]` – un tableau entier (1 ≤ n ≤ 105)
> * `multiplicateurs[0 ... m-1]` – un ensemble entier (1 ≤ m ≤ 300 et **m ≤ n**)

> **Action** – Exécuter **exactement des opérations « m »**.
> Dans l'opération *i-th*, vous pouvez **supprimer** soit l'élément **leftmost** soit l'élément **leftmost** de `nums`.
> L'élément supprimé est multiplié par `multipliers[i]` et ajouté à votre score total.

> **Objectif** – Maximiser le score total après toutes les opérations `m`.

---

Pourquoi ce problème est-il une question d'entrevue?

Pourquoi ça compte ?
-- -- -- -- -- --
Autres **Choisir le PDD**Démonstration *comment décider entre deux futurs états* – un thème d'entrevue de base. Autres
Autres **Greedy + DP**.Vous pourriez être tenté d'adopter une approche gourmande ; vous montrer savoir **quand l'avidité échoue** est impressionnant. Autres
**L'astuce de tailler le tableau aux premiers et derniers éléments `m` montre que vous pouvez raisonner sur *reachability* et *espace-sauver*. Autres
Avec `m ≤ 300`, une force brute `O(m3)` est invraisemblable – prouve que vous pouvez concevoir une solution *efficace*. Autres
**Numéros négatifs** Autres

> **Entretien d'embauche Hack:** Si vous pouvez placer cette question dans une fente de 45 minutes, vous obtiendrez l'insigne "DP" sur votre CV – un mot clé convoité pour de nombreux recruteurs technologiques.

---

Le bon – L'approche claire et intuitive du PDD

1. **Définition de l'État* *
- `dp[l][k]` – la note maximale que nous pouvons obtenir ** après avoir déjà pris des éléments `k` de la gauche** du tableau paré et sont actuellement en opération `k`.
- Le nombre d'éléments tirés de la droite est "k - l".
- L'index de l'élément le plus utilisable dans le tableau original est
"droite = n - 1 - (k - l)".

2. **Transition**
- Prendre à gauche: `nums[l] * multiplicateurs[k] + dp[l+1][k+1]`.
- Prendre à droite: `nums[right] * multiplicateurs[k] + dp[l][k+1]`.
- Choisissez le maximum.

3. **Dossier de base**
- Quand `k == m`, tous les multiplicateurs sont utilisés → score `0`.

4. **Optimisation**
- Seuls les premiers `m` et les derniers `m` éléments de `nums` peuvent être choisis.
- Si `n > 2*m`, nous pouvons *trim* `nums` en toute sécurité à un nouveau tableau de taille `2*m`.
- Oui. Cela réduit la taille de la table DP à au plus `m × m` (= 90 000 entrées lorsque `m = 300`).

L'algorithme fonctionne dans le temps `O(m2)` et la mémoire `O(m2)` – parfaitement adapté aux contraintes.

---

Qu'arrive-t-il si vous n'utilisez pas DP ?

Une mise en œuvre recursive directe qui tente tous les choix de gauche/droite produira **temps exponentiel** ('O(2^m)').
Avec `m = 300`, qui est astronomiquement énorme – vous allez frapper **Time‐Limit Exceed** en 0.01 s.

Même une récursion mémolisée qui ne **pas** taille le tableau utilise toujours `O(n2)` mémoire quand `n` est grand, qui va exploser jusqu'à > 2 Go.
C'est pourquoi la solution *naïve* est une fin ** morte**.

---

## -Le mauvais – Cas de bord et pièges communs

Piège Explication
- C'est quoi ?
**Produits négatifs**Les multiplicateurs et les "nums" peuvent être négatifs. Une simple prise de la plus grande valeur absolue de l'heure échoue. Utiliser la comparaison DP complète (`max(gauche, droite)`). Autres
**Overflow**=Score max =1000 *=1000 *=300 000 000 '= s'adapte à `int`, mais ajouter de nombreuses opérations peut dépasser 32 bits dans certaines langues.= Utilisez `long' (C++/Java) ou `int64` (Python=s `int` n'est pas lié). Autres
**Large `n`**" `n` peut être 105, mais vous n'avez besoin que d'éléments `2*m`. Trimez le tableau d'abord; sinon vous attribuez `n × n` DP table. Autres
**Dépassement de la pile récursive**= La profondeur récursive `m ≤ 300` est sûre dans la plupart des temps d'exécution, mais dans des environnements stricts, vous pouvez atteindre les limites de la pile. Fournir une implémentation itérative (bottom-up) ou utiliser `@lru_cache` dans Python. Autres
**Les calculs de l'indice Wong**Les erreurs hors-par-un lors du calcul de l'indice "n - 1 - (k - l)" sont fréquentes. Gardez un invariant clair : `l` indique toujours l'élément de gauche non utilisé suivant. Autres
**L'explosion de mémoire**="dp` taille `m × m` est bonne, mais `dp` de taille `n × n` ne l'est pas. Trim `nums` à `2*m` d`abord. Autres

---

# # # Solution Walk- Par

1. **Triez le tableau**
Texte
si n > 2*m :
nombres = nombres[:m] + nombres[-m:]
«» "
Maintenant "len(nums)". 2*m".

2. ** Tableau PD**
`dp[l][k]` – meilleur score après avoir utilisé des multiplicateurs `k` et déjà enlevé des éléments `l` de la gauche.
Le nombre du côté droit enlevé est `k - l`.

3. **Répétition**
Texte
gauche = nombres[l] * multiplicateurs[k] + dp[l+1][k+1]
droite = nombres[right_index] * multiplicateurs[k] + dp[l][k+1]
dp[l][k] = max(gauche, droite)
«» "

4. **Base** – `k == m` → 0.

5. **Réponse** – «dp[0][0]».

---

# # # C'est des extraits de code

> Les trois solutions utilisent **Memoused DP** (top-down).
> complexité temporelle : **O(m2)**, Mémoire : **O(m2)**.
> `m ≤ 300`, de sorte que le tableau DP est au plus 90 000 entrées.

---

### Java

"Java
Importer java.util. Les tableaux;

solution de classe {
/* 1. Conserver une référence au tableau paré */
Int privé[] les numéros;
multiplicateurs int privés;
Int m privé, n; // n == longueur nums., m == multiplicateurs.longueur
mémo privé long[]; // long pour éviter le débordement

Int maximum Score(int[] nombres, int[] multiplicateurs) {
ceci.multiplicateurs = multiplicateurs;
ce.m = multiplicateurs.longueur;
/* Trim seulement la partie nécessaire des nombres */
i (longueur maximale > 2 * m) {
int[] paré = nouvel int[2 * m];
Système.arraycopie(nums, 0, parés, 0, m);
Système.arraycopie(nums, nombres.longueur - m, paré, m, m);
ce.nums = paré;
} autre {
ce.nums = nombres;
}
ce.n = ce.nums.longueur;
mémo = nouveau long[m][m]; // indices: gauche, prise
pour (long[] ligne : mémo) Arrays.fill(row, Long.MIN_VALUE);
retour (int) dfs(0, 0); // début à partir de gauche=0, multiplicateurs utilisés=0
}

/* dp(left, k) → meilleur score après avoir utilisé des multiplicateurs de k et avoir enlevé les éléments de gauche du côté gauche */
privé long dfs(int gauche, int k) {
si k == m) retourne 0;
si (memo[gauche][k] != Long.MIN_VALUE) retour mémo[left][k];
int droite = n - 1 - (k - gauche); // indice correspondant à droite

longue durée Gauche = (long) nombres[gauche] * multiplicateurs[k] + dfs(gauche + 1, k + 1);
longue durée Droite = (long) nombres[droite] * multiplicateurs[k] + dfs(gauche, k + 1);

retour mémo[left][k] = Math.max(take À gauche, prendre à droite);
}
}
«» "

> **Pourquoi "long"?**
> Même si `int` correspond aux limites, l'utilisation de `long` garantit la sécurité si les contraintes sont assouplies.

---

Python

'`python
à partir de functools importer lru_cache

Solution de classe:
def maximum Score(même, nombres, multiplicateurs):
m = len(multiplicateurs)

# Seuls les premiers et derniers éléments m peuvent être utilisés
si len(nums) > 2 * m:
nombres = nombres[:m] + nombres[-m:]

n = len(nums)

@lru_cache(maxsize=Aucune)
def dfs(gauche, k):
""gauche – combien d'éléments de gauche déjà pris
k – combien de multiplicateurs déjà utilisés"""
Si k == m:
retour 0
droite = n - 1 - (k - gauche) # indice de l'élément droit actuel
take_left = nombres[left] * multiplicateurs[k] + dfs(left + 1, k + 1)
take_right = nombres[right] * multiplicateurs[k] + dfs(left, k + 1)
retour max(take_left, take_right)

retour dfs(0, 0)
«» "

> **`lru_cache`** remplace la table DP manuelle, en maintenant la pile de récursion minimale.

---

### C++ (Top-Down avec la mémoisation)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maximum Score(vecteur<int>& nombres, vecteur<int>& multiplicateurs) {
int m = multiplicateurs.size();

/* Trimez le tableau à 2*m si nécessaire */
si ((int)nums.size() > 2 * m) {
vecteur <int> paré(2 * m);
la copie(nums.degin(), nums.degin() + m, trimé.degin();
copie(nums.end() - m, nums.end(), trimmed.degin() + m);
nums.swap(trimmed);
}
int n = nombres.size();

vector<vector<long long>> memo(m, vector<long long>(m, LLONG_MIN));

fonction<long long(int,int)> dfs = [&](int gauche, int k) -> long {
si k == m) retourne 0;
si (memo[gauche][k] != LLONG_MIN) retourner mémo[left][k];
int droite = n - 1 - (k - gauche);
longue durée Gauche = 1LL * nombres[gauche] * multiplicateurs[k] + dfs(gauche + 1, k + 1);
longue duréeDroite = 1LL * nombres[droite] * multiplicateurs[k] + dfs(gauche, k + 1);
retour mémo[left][k] = max(take À gauche, prendre à droite);
};
retour (int)dfs(0, 0);
}
};
«» "

> Le lambda `dfs` capture les `nums` et les `multipliers` par référence, en gardant le code concis.

---

TL;DR

- **Trim `num` à `2*m`** pour éviter une mémoire énorme.
- Utilisez un DP mémorisé avec l'état "dp[left][utilisé]".
- Transition : comparer prendre à gauche contre prendre à droite.
- Complexité: temps "O(m2)", mémoire "O(m2)".
- Les trois implémentations fonctionnent en fraction de seconde pour les contraintes données.

---

- Oui. Liste de contrôle du référencement – Faites sortir votre blog

1. **Titre** – Inclure le mot-clé «DP» et mentionner les contraintes.
2. **Description détaillée** – 150–160 caractères: Maîtrisez le problème DP LeetCode en 45 min – les matrices, évitez les débordements et passez le filtre recruteur. (en milliers de dollars)
3. **En-têtes** – Utilisez H1, H2, H3 pour la lisibilité; les moteurs de recherche aiment le contenu structuré.
4. **Images/Diagrammes** – Diagramme de transition de l'état visuel (peut être un SVG).
5. **Code Highlighting** – Utilisez les balises `<pre><code class="language-java">...</code></pre>`.
6. ** Liens internes** – Lien vers vos autres billets de blog sur DP, cupidité, ou interview prep.
7. **Sources externes** – Citer la page de problème LeetCode.
8. **URL canonique** – Si vous repositionnez sur Medium, utilisez l'URL originale comme canonique.
9. **Alt Text** – Ajouter un texte alt descriptif pour toutes les images.
10. ** Partage social** – Ajouter des méta tags de carte Twitter pour afficher les extraits de code dans l'aperçu.

> **Résultat:** Votre article sera classé plus haut pour la solution de LeetCode de leet, et les recruteurs défilant les tableaux d'emploi le repéreront instantanément.

---

TL;DR

*Trim le tableau → mémorisé DP → `O(m2)` heure. *
Les trois langues sont prêtes à copier-coller dans votre prochain entretien ou blog.

Bonne chance ! C'est ce qu'il a dit.

---

Liens
- Problème de LeetCode 1770: [Score maximal des opérations de multiplication](https://leetcode.com/problèmes/maximum-score-from-performing-multiplication-operations/)

---

> J'ai aimé ce passage ? Ajouter un commentaire, partager sur LinkedIn, et faire savoir aux recruteurs que vous pouvez crack DP en quelques minutes! *

---

* * TL; RD

- Trim `num` aux premiers/derniers `m` éléments.
- État DP : "dp[left][k]".
- Transition: "max (à gauche, à droite)".
- Base: `k == m → 0`.
- Temps: "O(m2)", Mémoire: "O(m2)".
- Les trois extraits de langue ci-dessus illustrent l'approche.

> **Result:** Vous pouvez résoudre le problème LeetCode en moins d'une minute et ajouter "DP" à votre CV. Les

---

**Happy codage et interview hacking!**

---

*Cet article est sous licence CC BY-SA. N'hésitez pas à vous adapter et à partager! *

---

* * TL;DR

**Trim**, **DP**, **Memoise** – 90 000 états max.
Java/Python/C++ fonctionnent tous avec le temps `O(m2)`.
Évitez les récursions exponentielles et les explosions de mémoire.
Portez ceci sur votre CV et les recruteurs prendront note.