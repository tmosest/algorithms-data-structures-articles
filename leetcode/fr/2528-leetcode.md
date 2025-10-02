---
titre: LeetCode 2528. Maximiser la ville minimale
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 2528 – ** Maximiser la ville à puissance minimale**

La tâche consiste à ajouter de nouvelles centrales électriques `k` (toutes ayant la même portée `r`) à une ligne de villes afin que la puissance *minimum* de toute ville devienne la plus grande possible.

Les contraintes sont grandes (`n` jusqu`à `105`, `k` jusqu`à `109`) – nous avons besoin d`un algorithme qui fonctionne dans `O(n log reply)` et utilise seulement `O(n)` mémoire supplémentaire.



-----------------------------------------------------------------------------------

- Oui. 2. Aperçu de l'algorithme

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
**1. Recherche binaire sur la réponse**. Si nous pouvons obtenir une puissance minimale de `mid` avec au plus `k` nouvelles stations, toute valeur plus petite est également réalisable; si nous ne pouvons pas, aucune plus grande valeur n'est possible. Autres
**2. Placement Greedy**.En balayant les villes de gauche à droite, si la ville `i` manque de puissance, placez les stations manquantes aussi loin que possible à droite (`pos = min(n-1, i+r)`). Autres
**3. Tenue de livres sur les fenêtres coulissantes** Utiliser un tableau auxiliaire `add[]` où `add[x]` est le changement net dans `cur` qui commence à la ville `x`. Quand une nouvelle station est placée à `pos`, nous faisons `add[pos] += need` et `add[pos+r+1] -= need` de sorte que la station cesse d'influencer après la fin de sa portée. Cela nous donne `O(1)` mise à jour par ville et garde la fenêtre coulissante dans le temps linéaire. Autres

La procédure de vérification est donc linéaire, et nous recherchons la réponse.



-----------------------------------------------------------------------------------

- Oui. 3. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie la puissance minimale maximale possible.

---

Lemma 1
Lors de la vérification d'une cible fixe `mid`, la règle cupide de placer les stations manquantes dans la ville la plus lointaine qui peut encore couvrir la ville actuelle.

**Prof.**
Que la ville `i` ait actuellement `p < mi` puissance.
Toute ville `j` qui peut être alimentée par une nouvelle station à `pos` satisfait
"pos -" [i, i+r]".
Si nous plaçons les nouvelles stations à une position *gauche* `pos' < pos`, les nouvelles stations couvrent toujours la ville `i` et couvrent également toutes les villes dans `[pos', pos'+r]`.
Puisque `pos` est la position la plus droite* qui couvre toujours `i`, l'intervalle `[pos', pos'+r]` est un sous-ensemble de `[pos, pos+r]`.
Par conséquent, toute ville qui peut être alimentée par une station à `pos' peut également être alimentée par une station à `pos`.
Ainsi, choisir `pos` ne peut pas réduire l'ensemble des villes futures qui peuvent être alimentées. *



Lemma 2
Pour un "mid" fixe, le placement gourmand utilise le nombre minimum possible de stations supplémentaires parmi tous les placements possibles.

**Prof.**
Considérez le moment où la ville `i` est traitée.
Comme toutes les villes précédentes sont déjà satisfaites (par induction), tout emplacement possible qui satisfait la ville `i` doit ajouter au moins `besoins = stations mi - cur` qui couvrent `i`.
L'algorithme cupide ajoute exactement des stations "besoins".
En raison de Lemma 1 ces stations sont placées aussi loin que possible, de sorte qu'elles ne rendent aucune ville auparavant satisfaite de devenir insatisfaite.
Ainsi, aucun placement ne peut utiliser moins de stations que l'avide. *



Lemma 3
Si la vérification cupide échoue (besoin de plus de "k" stations), alors aucun placement ne peut atteindre la cible "mid".

**Prof.**
Supposons qu'il y ait eu un placement qui permet d'utiliser "mid" dans la plupart des stations "k".
Considérez les villes dans l'ordre.
Chaque fois que l'algorithme gourmand décide d'ajouter des stations à la ville "i", tout autre placement doit ajouter ** au moins** le même nombre de stations à une position qui couvre également "i" (Lemma 2).
Par conséquent, l'autre placement ne peut pas utiliser moins de stations que l'avide pour tout préfixe de villes.
Si l'avidité dépasse le "k", il en est de même pour tout autre placement. *



- Oui. Théorème
La recherche binaire combinée à la vérification cupide renvoie la puissance minimale maximale possible.

**Prof.**
Laissez `opt` être la puissance minimale optimale.
Pour chaque `mid ≤ opt`, le contrôle avide réussit (par Lemma 3), de sorte que la recherche binaire déplacera la limite inférieure vers `mid`.
Pour chaque `mid > opt`, la vérification cupide échoue, donc la recherche binaire déplace la limite supérieure vers le bas.
Ainsi la recherche converge vers `opt`.



-----------------------------------------------------------------------------------

- Oui. 4. Analyse de la complexité

Étape Temps Mémoire
C'est pas vrai.
Recherche binaire (réponse au journal) Autres
Cochez par `mid`" `O(n)`" `O(n)` (le tableau auxiliaire `add[]`) Autres
Total **«O(n log reponse)»****«O(n)»** Autres

`réponse` ≤ `somme(stations) + k` ≤ `105·105 + 109` `1010`, donc `réponse log` ≤ 34.



-----------------------------------------------------------------------------------

- Oui. 5. Mise en oeuvre des références

Les trois implémentations sont identiques en logique – seule la syntaxe diffère.

> **NOTE** – Tous utilisent `long`/`long long` pour les sommes et le nombre de stations ajoutées pour éviter les débordements.
> La fonction helper `can(mid)` implémente le contrôle avide.

#### 5.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
public long maxPower(int[] stations, int r, int k) {
int n = stations. longueur;

// limite supérieure: somme de toutes les stations + k
somme longue = 0;
pour (int s : stations) somme += s;
longue gauche = 0, droite = somme + k;

pendant que (gauche <= droite) {
long milieu = (gauche + droite) >>> 1; // (gauche + droite)/2 sans débordement
si (peut (stations, r, n, milieu, k)) {
gauche = milieu + 1; // milieu est réalisable → essayer plus grand
} autre {
droite = milieu - 1; // milieu impossible → essayer plus petit
}
}
retour droit; // dernier succès milieu
}

Poudre de booléen privé(int[] stations, int r, int n, longue cible, long k) {
long[] add = nouveau long[n + 1]; // diff array, n+1 pour éviter les contrôles des limites
long cur = 0; // puissance courante couvrant la ville i
longue utilisation = 0; // stations que nous avons déjà ajoutées

pour (int i = 0; i < n; i++) {
cur += ajouter[i] + stations[i];

si (cur < cible) {
besoin long = cible - cur;
nécessaire +=;
si (utilisé > k) retourner faux; // ne peut pas rester dans le budget

cur += besoin; // ajouter la puissance maintenant

int pos = Math.min(n - 1, i + r); // ville la plus éloignée qui couvre encore i
add[pos] += besoin; // commencer à affecter à pos
si (pos + r + 1 < n) {
add[pos + r + 1] -= besoin; // stop affectant après la plage
}
}
}
retour vrai;
}
}
«» "

5.2 Python 3.10

'`python
Solution de classe:
def maxPower(self, stations: List[int], r: int, k: int) -> Int:
n = len(stations)

total = somme(stations)
lo, hi = 0, total + k # 64-bit entiers sont naturels en Python

def can(mid: int) -> C'est vrai.
ajouter = [0] * (n + 1) # tableau diff
cur = 0 # puissance couvrant actuellement cette ville
utilisé = 0

pour i dans la plage(n):
cur += ajouter[i] + stations[i]
si cur < mi:
besoin = milieu - cur
utilisé += besoin
si utilisé > k: # budget dépassé
Retour Faux
cur += besoin
pos = min(n - 1, i + r)
ajouter[pos] += besoin
si ps + r + 1 < n:
ajouter[pos + r + 1] -= besoin
retour Vrai

alors que lo <= bonjour:
milieu = (lo + hi) // 2
si possible (milieu):
lo = milieu + 1
Sinon:
Bonjour = milieu - 1
retour
«» "

Numéro 5.3 C++17

'`cpp
solution de classe {
public:
long maxPower(vecteur<int>& stations, int r, long long k) {
int n = stations.size();

somme longue = 0;
pour (int s : stations) somme += s;
long lo = 0, hi = somme + k; // 64-bit

auto can = [&](long cible longue) -> Bool {
vector<long long> add(n + 1, 0); // tableau diff
longue courbure = 0, utilisée = 0;

pour (int i = 0; i < n; ++i) {
cur += ajouter[i] + stations[i];
si (cur < cible) {
long besoin = cible - cur;
nécessaire +=;
si (utilisé > k) retourner faux;
besoin de cur +=;
Int pos = min(n - 1, i + r);
add[pos] += besoin; // commence à influencer à pos
Si (pos + r + 1 < n)
add[pos + r + 1] -= besoin; // s'arrête après sa portée
}
}
retour vrai;
};

pendant que (lo <= bonjour) {
long long milieu = (lo + hi) >> 1;
si (can(mid) lo = milieu + 1;
Autre salut = milieu - 1;
}
retour salut;
}
};
«» "

Les trois solutions fonctionnent dans le même temps `O(n log response)` et n'utilisent qu'un tableau auxiliaire `O(n)`.



-----------------------------------------------------------------------------------

- Oui. 6. Article de blog – De LeetCode 2528 à une solution de préparation au travail

> **Chercher les mots-clés**: *LeetCode 2528*, *Maximize the Minimum Powered City*, *binary search slide window*, *Java interview*, *Python interview*, *C++ interview*, *emploi interview*, *logiciel ingénieur*, *structures de données*.

---

### 6.1 Récapitulation des problèmes (TL;DR)

> Étant donné qu ' il n ' y a pas de villes dans une ligne, chacune d ' entre elles dispose d ' un nombre initial de stations électriques.
> Une station a une portée de couverture `r` (c'est-à-dire qu'elle alimente chaque ville de `pos-r` à `pos+r`).
> Nous pouvons construire `k` nouvelles stations du même type.
> **Objectif:** ajouter les nouvelles stations de sorte que la puissance **minimum** parmi toutes les villes soit aussi grande que possible.
> Retourne cette puissance minimale maximale.

---

6.2 Qu'est-ce qui rend le problème difficile?

1. ** Énorme < < k > > . **
Nous ne pouvons pas aller au-delà de toutes les possibilités; nous devons utiliser partout l'arithmétique 64 bits.

2. **Large `n` 105. **
Toute approche `O(n2)` sera dépassée.
Nous avons besoin d'une solution linéaire ou `n log n`.

3. **Objectif mondial (minute de toutes les villes). * *
L'optimisation n'est pas obtenue en maximisant localement chaque ville; nous devons penser globalement.



6.3 Aperçu 1 – Recherche binaire sur la réponse

Si nous pouvons obtenir une puissance minimale de `mid` en utilisant au plus `k` nouvelles stations, alors toute cible plus petite est également réalisable.
Inversement, si nous ne parvenons pas à atteindre un « milieu », aucun objectif plus large n'est possible.

*Pourquoi la recherche binaire? *
Il transforme une vérification de faisabilité globale en prédicat monotone :
`P(mid)` = = Pouvons-nous obtenir une puissance minimale ≥ milieu?

---

### 6.4 Insight 2 – Le placement en douceur est optimal

Quand nous rencontrons une ville qui manque de puissance, nous ** devons** ajouter quelques stations qui la couvrent.
Quelle ville devrait accueillir ces nouvelles stations ?
*Greedy Règle:* les mettre le plus à droite possible (`pos = min(n-1, i+r)`).

Pourquoi ça marche ?

* La station à la position la plus à droite a la plus longue *future portée* – elle peut aider le plus grand nombre de villes à sa droite.
* Le placement ne fait jamais de mal à des villes déjà satisfaites (ils sont tous laissés de 'pos').

Mathématiquement, la stratégie d'avidité est optimale (elle utilise les plus petites nouvelles stations) – voir la preuve d'exactitude ci-dessus.



#### 6.5 Insight 3 – O(1) Mise à jour de la fenêtre avec un tableau de partage

Tout en scannant de gauche à droite, nous maintenons une somme courante `cur` des centrales qui influencent actuellement la ville en cours de traitement.

«» "
stations existantes → constante
nouvelles stations → ajouté par gourmandise, laissez la fenêtre après les étapes r
«» "

Nous stockons le changement d'influence* qui commence à chaque ville dans un tableau auxiliaire `add[]`:

*Quand nous mettons `besoin` de nouvelles stations à `pos`
`add[pos] += besoin` (ils commencent à influencer chez `pos`)
`add[pos+r+1] -= need` (ils s'arrêtent après leur portée)

Pendant le scan, nous faisons `cur += add[i] + stations[i]`.
Toutes les opérations sont `O(1)` par ville → global `O(n)`.



6.6 Pseudocode complet

«» "
fonction can(mid):
pour = 0
utilisé = 0
ajouter = [0] * (n+1) // tableau diff

pour i en 0 ... n-1:
cur += ajouter[i] // appliquer diff qui commence ici
stations cur +=[i]

si cur < mi:
besoin = milieu - cur
utilisé += besoin
si utilisé > k: Retour Faux

cur += besoin
pos = min(n-1, i+r)
ajouter[pos] += besoin
add[pos+r+1] -= need // sera appliqué à la fin de l'intervalle

retour Vrai
«» "

Recherche binaire sur `mid` appels `can(mid)` jusqu'à ce que la réponse se stabilise.



### 6.7 Extraits de code

Mots clés Autres
C'est pas vrai.
**Java** 1' pour le point médian pour éviter le débordement. Autres
**Python**=Utilisez `list` de zéros; les ints de Python=s sont non liés, mais nous utilisons toujours la logique `long`-like. Autres
**C++**="long long" partout, `vecteur<long long>` pour `add`. Autres

> Consultez les implémentations de référence de la section précédente pour un code complet et prêt à copier.



-----------------------------------------------------------------------------------

- Oui. 7. Pièges courants et -Que ne pas faire

Piège Explication
- C'est quoi ?
**Utiliser `int` pour la réponse**= `k` peut être `109` et chaque ville peut déjà avoir `105` stations → sum ~ `1010`. Autres
**Omettre le `+ r + 1` dans la mise à jour du diff**=L'influence de la station se termine après les étapes `r`. Oublier le `+1` signifie qu'il continue d'influencer une ville trop, conduisant à un surcompte. Ajouter le mot `-beed` à `pos + r + 1`. Autres
**Binary search limits off by one**= Si nous retournons `lo` après la boucle, nous pouvons donner une cible inaccessible. Retour `hi` (dernier succès `mid`). Autres
**Ignorer les villes au-delà de la plage de `add`**= Quand `pos + r + 1 == n`, nous accédons `add[n]` qui est en dehors du vecteur. Attribuer `ajout` avec la taille `n+1` ou garde `si (pos + r + 1 < n)`.
** Ne pas ajouter de « stations[i] » Après le diff** , les stations existantes font toujours partie de la puissance de cette ville. Inclure `stations[i]` dans la même mise à jour `cur`. Autres
**Ne pas réinitialiser `cur` chaque test**.La somme courante persiste sur les appels de recherche binaire → mauvais résultats. Recréer `add` (ou le effacer) pour chaque appel de `can`. Autres



-----------------------------------------------------------------------------------

- Oui. 8. De l'algorithme à la réussite des entrevues

1. ** Expliquez la monotonicité**: pourquoi la recherche binaire fonctionne pour la faisabilité.
2. **Décrivez l'invariant gourmand**: le placement le plus lointain → portée le plus long, ne fait jamais mal à gauche.
3. **Afficher l'astuce de la fenêtre O(1)**: tableau diff → mise à jour de la fenêtre coulissante.
4. **Mettre l'accent sur l'arithmétique 64 bits**: soulignez que `k` est énorme, `n` grand → toutes les sommes doivent être `long'.
5. ** Démontrez votre code**: passez par un petit test mental, en passant par `cur`, `add`, `used`.
6. **Cas de bord de discussion**:
* `r` = 0 → chaque ville ne peut être alimentée que par sa propre station.
* `k` = 0 → la réponse est simplement `min(stations)`.
* Toutes les villes ont déjà un énorme pouvoir → la réponse est énorme mais toujours limitée par le budget.

Être capable d'articuler ces idées montre à l'intervieweur que vous pouvez gérer à la fois *algorithmique* et *pratique* contraintes.



-----------------------------------------------------------------------------------

7.1 Pensée finale

LeetCode 2528 est un exemple de manuel de la façon dont un problème apparemment simple « add‐up‐to‐k» cache des idées algorithmiques profondes.
En transformant l'objectif global en prédicat de recherche binaire, en démontrant l'optimalité gourmande, et en utilisant un tableau de diff pour les mises à jour linéaires, nous arrivons à une solution à la fois **efficace** et **propre**.

Partagez cette approche dans votre prochain entretien, et regardez les intervieweurs hocher la tête dans l'approbation!

---



### 6.8 Article – J'ai raté quelque chose ? (en milliers de dollars)

> Si vous avez écrémé l'article et que vous voyez des lacunes, voici une liste de contrôle rapide:

1. ** Avez-vous mentionné l'arithmétique 64 bits? * *
2. **Avez-vous expliqué pourquoi la cupidité est optimale? **
3. **Avez-vous montré comment le tableau diff maintient la fenêtre O(1)? * *
4. ** Avez-vous énuméré les erreurs les plus courantes? * *
5. **Avez-vous utilisé les mots clés dans le titre? **

> Sinon, n'hésitez pas à modifier l'article en conséquence.



---

** Félicitations!**
Vous comprenez maintenant le LeetCode 2528 à un niveau profond, avez un code prêt à la production en trois langues, et pouvez l'expliquer comme un ingénieur chevronné. Bonne chance dans votre prochain entretien !



-----------------------------------------------------------------------------------

- Oui. 7. À propos de cette rédaction

> Si vous avez trouvé cela utile, partagez-le sur GitHub, Stack Overflow, ou un blog personnel.
> Étiquette-la avec **logiciel-ingénierie**, **interview-prep**, **algorithmes** et **structures de données**.

---



---

- Oui. 8. Résumé de ce que vous apprenez

* La recherche binaire transforme une vérification de faisabilité globale en un simple prédicat monotone.
* La règle cupide "place aussi loin que possible à droite" est certainement optimale pour ce problème.
* Un tableau diff (différence) donne une mise à jour de la fenêtre coulissante `O(1)`, transformant un processus potentiel `O(n2)` en `O(n)`.
* Toutes les implémentations utilisent l'arithmétique 64 bits pour rester dans les limites budgétaires.
* Le même algorithme fonctionne en Java, Python et C++, prouvant l'élégance linguistique-agnostique.



-----------------------------------------------------------------------------------

**Codage heureux!**



-----------------------------------------------------------------------------------

- Oui. 9. FAQ rapide

**Q :** Pourquoi la réponse est toujours `hi` après la boucle de recherche binaire?
**A :** Parce que "lo" dépasse le dernier succès "mid". La boucle se termine lorsque `lo > hi`; `hi` détient alors la plus grande valeur possible.

**Q :** Et si `k = 0`?
**A :** La fonction `can` vérifie immédiatement si chaque ville satisfait déjà `mid`; si `mid` est plus grand que le minimum global, elle échoue.

**Q :** Avons-nous vraiment besoin de la taille de tableau `add` `n+1`?
**A :** C'est une petite marge de sécurité; nous pourrions utiliser la taille `n` avec des contrôles aux frontières, mais la fente supplémentaire supprime une peritération conditionnelle.



-----------------------------------------------------------------------------------

10 ans. A emporter

> *LeetCode 2528* montre qu'une combinaison intelligente de **binaire**, **greedy placement** et **diff array updates** peut transformer une optimisation globale redoutable en un algorithme linéaire élégant.
> La maîtrise de ces modèles vous servira dans les entrevues et les projets du monde réel.