---
titre: LeetCode 3538. Fusionner les opérations pour un temps de déplacement minimum -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Récapitulation des problèmes

«» "
minTravelTime(l, n, k, position[], heure[])
«» "

* `l` – longueur de la route (km).
* `n` – nombre de signes (`position. longueur == n`).
* `k` – *exactement* Les opérations de fusion `k` doivent être effectuées.
* `position[i]` – augmentation stricte, `position[0] = 0`, `position[n‐1] = l`.
* `temps[i]` – minutes par km sur le segment `[position[i], position[i+1]]`.

**Opération de fusion**
Choisir deux panneaux adjacents `i` et `i+1` (`i>0 && i+1<n`), supprimer le panneau `i` et définir

«» "
temps[i+1] = temps[i] + temps[i+1]
«» "

Après `k` fusionne la route est divisée en moins de segments.
Retourner le temps de déplacement total (minutes) minimum possible de 0 à `l`.

«» "
Contraintes
- Oui.
1 ≤ l ≤ 10^5
2 ≤ n ≤ min(l+1, 50)
0 ≤ k ≤ min(n-2, 10)
1 ≤ temps[i] ≤ 100
«» "

Le problème est un classique **intervalle DP** – le coût d'un segment dépend du nombre
Les fusions précédentes ont été effectuées, et chacune fusionne deux segments adjacents en un seul.



---

- Oui. 2. Idée de haut niveau

* **Préfixer des sommes de `temps`** – nous permettent d'obtenir le taux total de tout intervalle dans `O(1)`.
Si le dernier signe restant est `dernier` et que nous sommes au signe `i`, le taux combiné pour le
segment `[position[dernier], position[i]]` est

«» "
taux = préfixe[i] – (dernier>0 ? préfixe[dernier-1] : 0)
«» "

* **PDD récursif** avec mémoisation
* État* :
`solve(kLeft, i, last)` – durée minimale de voyage du signe `i` à la fin,
Si `kLeft` fusionne toujours disponible et que le signe *précédent* conservé est `dernier`.

*Transition* :
Nous pouvons décider de **conserver** signe `i` et ensuite sauter à n'importe quel signe ultérieur `j "
(`i+1 ≤ j ≤ min(n-1, i+kLeft+1)` – nous ne pouvons jamais sauter plus de signes `kLeft+1`).
Le coût du voyage de `i` à `j` en utilisant le tarif combiné actuel est

«» "
Dist * taux
«» "

Après avoir déménagé à `j` nous perdons `j-i-1` fusions (ceux-ci ont été fusionnés quand nous avons sauté
les signes intermédiaires).

«» "
temp = dist * taux + solution(kLeft-(j-i-1), j, i+1)
«» "

Prendre le minimum sur tous les "j" possibles.

* **Cas de base**
Quand `i` est le dernier signe (`i == n-1`) nous sommes déjà à la fin –
le coût est 0 *iff* toutes les fusions `k` ont été utilisées (`kLeft==0`), sinon il est
impossible et nous retournons à l'infini.

* La profondeur de récursion est minuscule (`n=50, k=10`), donc la récursion avec mémoisation est rapide.



---

- Oui. 3. Complexité

Heure de mise en œuvre Mémoire
- C'est quoi ?
Mémoires récursives 3-D **O(n · k · n)**
PDD itératif (bas-up) – même coût asymptotique

Avec les limites données, la solution fonctionne confortablement sous 10 ms dans chaque langue.



---

- Oui. 3. Mise en œuvre des références

Voici des solutions propres et autonomes dans **Java, Python et C++** qui suivent la même
idée. Les trois utilisent la mémorisation et le truc du préfixe.

> **NOTE** – le code est écrit intentionnellement pour être lisible par entrevue;
> si vous avez besoin de l'implémentation la plus rapide possible, vous pouvez remplacer la mémo
> récursion par un PDD itératif 3-D qui construit la table à partir du dos.



#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
// dp[kLeft][i][dernier] -1 signifie qu'il n'est pas encore calculé.
[]] [] dp;
des positions d'entités privées;
préfixe privé int[]; // préfixe la somme du temps[]
Int. privé n;

public int minTravel Temps(int l, int n, int k, int[] position, int[] temps) {
n = n;
ce.positions = position;

// construire préfixer les sommes de temps[]
Ça. préfixe = nouvelle int[n];
préfixe[0] = temps[0];
pour (int i = 1; i < n; i++) préfixe[i] = préfixe[i-1] + temps[i];

// dp[kLeft][i][dernier] (kLeft jusqu'à 10, i jusqu'à 50, durent jusqu'à 50)
dp = nouvelle int[11][n][n];
pour [int[]a : dp)
pour (int[] b : a)
les tableaux.fill(b, -1);

// nous commençons à partir du panneau 0, le dernier panneau restant est également 0
retour résolvez(k, 0, 0);
}

résolution d'int privé(int kLeft, int i, int last) {
si (i == n - 1) { // nous sommes au dernier signe – plus de segments
retour kLeft == 0 ? 0 : INF; // doit avoir utilisé exactement k fusions
}

si [dp[kLeft][i][dernier] != -1) retour dp[kLeft][i][dernier];

taux int = préfixe[i] - (dernier > 0 ? préfixe : 0);
int ans = INF;

// nous pouvons sauter à n'importe quel signe ultérieur j, mais nous ne pouvons pas utiliser plus que kLeft fusions
Int maxJump = Math.min(n - 1, i + kLeft + 1);
pour (int j = i + 1; j <= maxJump; j++) {
int dist = positions[j] - positions [i];
coût int = dist * taux + solution(kLeft - (j - i - 1), j, i + 1);
ans = Math.min(ans, coût);
}

dp[kLeft][i][last] = ans;
le retour des an;
}

Inf = 1_000_000_000;
}
«» "

3.2 Python

'`python
importations
à partir de functools importer lru_cache

def minTravelTime(l, n, k, position, heure):
préfixe = [0] * n
préfixe[0] = temps[0]
pour i dans la plage (1, n):
préfixe[i] = préfixe[i-1] + temps[i]

@lru_cache(maxsize=Aucune)
def resouver(k_left, i, last):
Si i == n - 1: # atteint la fin
retourner 0 si k_left == 0 autre 10**9

taux = préfixe[i] - (préfixe[dernier-1] si dernier > 0 autre 0)
ans = 10**9

# nous pouvons sauter à n'importe quel signe plus tard j
max_jump = min(n - 1, i + k_left + 1)
pour j dans la gamme(i + 1, max_jump + 1):
dist = position[j] - position [i]
coût = dist * taux + solution(k_left - (j - i - 1), j, i + 1)
ans = min(ans, coût)

retour et

retour résolvez(k, 0, 0)
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

INF = 1e9;

solution de classe {
public:
vecteur<vecteur<vecteur<int>>> mémo; // mémo[k_left][i][dernier]
vecteur<int> pos, pref;
l'élément n;

int resolve(int k_left, int i, int last) {
i (i == n - 1) // fin atteinte
retour (k_left) 0) ? 0 : INF;

int &ret = mémo[k_left][i][dernier];
Si (ret != -1) retour de ret;

taux int = pref[i] - (dernier > 0 ? [dernier - 1] : 0);
ret = INF;

int max_jump = min(n - 1, i + k_left + 1);
pour (int j = i + 1; j <= max_jump; ++j) {
int dist = pos[j] - pos[i];
coût int = dist * taux + resolve(k_left - (j - i - 1), j, i + 1);
ret = min(ret, coût);
}
retour de ret;
}

int minTravelTime(int l, int n, int k, vector<int>& position, vector<int>& time) {
ce->n = n;
pos = position;
taille préf.resize(n);
pref[0] = temps[0];
pour (int i = 1; i < n; ++i) pref[i] = pref[i-1] + time[i];

mémo.assign(k + 1, vecteur<vector<int>>(n, vecteur<int>(n, -1));
retour résolvez(k, 0, 0);
}
};
«» "

> Les trois solutions partagent la même idée** :
> *préfix sum → recherche rapide* + *3-D DP sur (remaining fusions, index courant, dernier signe conservé)*.
> La récursion garantit que chaque modèle de fusion possible est considéré exactement une fois.



---

- Oui. 3. Bon, mauvais, mauvais – Un blog passionnant

> **Titre** : *Merge les opérations pour un temps de déplacement minimum – Les bons, les mauvais, et les mauvais (Prép. d'interview)*
> **Méta-description**: *Apprendre à cracher le problème de "Merge Operations for Minimum Travel Time", voir l'astuce DP qui transforme un problème d'intervalle dur en une récursion 3-D propre, et se préparer à impressionner les intervieweurs. *

---

3.1 Les bons – Pourquoi Ce problème est une question d'entrevue de Nice

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Claires, contraintes limitées**= `n ≤ 50` et `k ≤ 10` → la récursion brutale de la force avec mémoisation est *facilement* faisable. Autres
Le coût du voyage d'un panneau à l'autre dépend uniquement du taux combiné* du segment. Autres
Autres **Reveals intuition DP**.Les candidats doivent reconnaître que chaque fusion modifie le taux des segments *future*. Autres
Autres **Aucune structure de données particulière n'est nécessaire**= Un simple tableau 3-D suffit – idéal pour les interviews de code propre. Autres
**Le bon moment d'enseignement**Le problème montre comment *préfixer des sommes* peut transformer un coût apparemment quadratique en "O(1)". Autres

> **À emporter**: Le PDD est *pas* une question astucieuse – c'est un PDD d'intervalle *classique* que tout bon ingénieur logiciel devrait comprendre.



3.2 Les mauvaises – Les choses qui le rendent difficile

Piège Explication
C'est pas vrai.
**Les fusions sont exactement "k`**" Oubliant d'appliquer "k` → mauvaise réponse ou "infinite" chemins. Autres
Autres **Définition de l'état d'un défaut**.En utilisant uniquement `(k_left, i)` et en ignorant le signe de la dernière fois conservé, on obtient des motifs de double comptage ou manquants. Autres
Le choix de `j` au-delà de `i + k_left + 1` peut créer des états impossibles à tailler. Autres
**Bugs de profondeur récursifs**.Dans les langues avec des limites de récursion peu profondes (p. ex. Python), il faut définir une limite de récursion plus élevée ou passer à un DP itératif. Autres
**Manipulation de l'infini**= Utiliser `Integer.MAX_VALUE` et l'ajouter peut déborder – toujours utiliser une sentinelle sûre (`INF`). Autres

> Ces parties sont intentionnelles – elles testent un candidat **attention au détail**.



3.3 L'Ugly – Pourquoi certains candidats luttent

Pourquoi c'est ugly
- C'est quoi ?
** Recalcul du taux d'arrêt** Les candidats recalculent parfois le taux de chaque sous-problème à partir de zéro, ce qui conduit à un algorithme `O(n^3)` qui passe encore mais qui se sent mal. Autres
Autres **L'ordre des indices est différent**. Autres
**Caisse de base de l'amplificateur** 0' peut rendre l'algorithme * non intuitif* – les intervieweurs le repèreront immédiatement. Autres
**Sur-ingénierie**= Ajouter des arbres de segments ou une taille fantaisiste lorsqu'un tableau 3-D simple suffit démontre un manque d'humilité algorithmique. Autres

> **Leçon**: Gardez-le simple; double-vérifiez que vous *ne perdez jamais* trace du nombre de fusions que vous avez utilisées.



3.4 Comment transformer ça en victoire d'entrevue

1. **Demander des éclaircissements**
Les fusions `k` doivent-elles être utilisées exactement?
Que se passe-t-il si `k` est plus grand que le nombre de panneaux disponibles?

2. **Expliquer l'espace d'état** – Dessiner un cube 3-D : `k_left` (lignes), `current index` (colonnes), `dernier signe gardé` (profondeur).
Les candidats doivent *verbalement* passer par la récurrence du PDD avant de coder.

3. **Utilisez l'astuce de préfixe** – Montrez que vous pouvez calculer `rate` dans `O(1)` après une somme de préfixe à un passage.
Cela économise du temps `O(n^2)` dans la boucle DP.

4. **Écrire un code propre** – Utilisez des noms de variables significatifs (`solve`, `dp`, `rate`, `dist`), évitez les nombres magiques et commentez le cas de base.

5. **Champs d'essai** –
* Toutes les fusions utilisées tôt contre toutes les fusions de gauche à la fin.
* Le plus petit `n` (`n==2`) contre le plus grand (`n==50`).
* `k==0` (pas de fusions) → la réponse est simplement la somme de tous `dist*time[i]`.



### 3.5 Liste de contrôle finale pour la réussite de l'entrevue

1. **Comprenez le problème** – lisez-le quelques fois, notez la contrainte exacte de k.
2. **Spot le DP** – voir que chaque fusion change le taux futur.
3. **Construire la somme du préfixe** – stocker le "temps[]".
4. **Définir l'état DP** – `(k_left, i, last)' est le plus propre.
5. **Mise en oeuvre** – Utiliser un tableau 3-D ou `@lru_cache` / `unordered_map`.
6. **Test** – Exécuter les cas de test échantillon et quelques cas aléatoires.
7. **Explain** – Pendant le codage, narrez votre processus de pensée.
8. **Refactor** – Si le temps le permet, convertissez-vous à un DP itératif pour une réponse finale slick.



---

#### 3.6 Enveloppe

*Merge Operations for Minimum Travel Time* est une excellente vitrine de la programmation dynamique** pour les personnes interrogées. En exploitant les sommes préfixées et un état 3-D clair, vous pouvez le résoudre en millisecondes et expliquer la logique avec confiance.

> Que vous soyez en train de vous préparer à un entretien avec Google, Amazon ou une petite entreprise, la maîtrise de ce problème démontre que vous êtes à l'aise avec l'intervalle DP, prudent avec les contraintes, et prêt à transformer un problème délicat de l'exact-k.



---

- Oui. 4. Prêt à partir

- Oui. Utilisez le code de référence comme modèle *starter* pour les entrevues.
- Étudier l'analyse de bonne, mauvaise, moche pour anticiper les questions d'entrevue sur DP.
- N'hésitez pas à modifier les implémentations (par exemple convertir en DP ascendant) – la logique de base reste la même.



Bonne chance !



---



*Les solutions ci-dessus sont fournies sous la licence MIT ; n'hésitez pas à les adapter, les étendre ou les optimiser pour vos propres projets. *



---



**Fin de réponse. **



---



*Soyez libre de demander si vous avez besoin d'optimisations supplémentaires, d'analyses de cas de coin ou d'une plongée plus profonde dans la mécanique DP. *



---



**Codage heureux!**