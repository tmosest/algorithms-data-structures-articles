---
titre: LeetCode 3488. Questions sur les éléments les plus proches -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution

Ci-dessous sont **trois implémentations propres et prêtes à la production** – une pour chacune des langues d'entrevue les plus populaires.

> Les trois utilisent le même temps d'O(n), l'espace d'O(n) « two-pass » sur une technique de tableau doublé.
> Ils sont courts, pleinement commentés et ont fait l'objet de tests unitaires par rapport aux cas échantillonnés.

Langue Fonction Signature Code
- C'est quoi ?
**Java**= Liste publique<Intégrée> résoudreQueries(int[] nombres, requêtes int[]="<details><sommaire> Cliquez pour agrandir</résumé>

"Java
Importation de java.util.*;

solution de classe publique {

***
* Trouver la distance circulaire minimale à un autre élément égal pour chaque requête.
*
* @param nums Le tableau circulaire des entiers.
* Questions @param Indices dont nous avons besoin.
* @retour Une liste de distances minimales (ou -1 si aucun duplicata n'existe).
*/
liste publique<integer> resolveQueries(int[] nums, int[] requêtes) {
int n = longueur nums;
// distance[i] = distance circulaire minimale de i à un autre élément égal
int[] dist = nouvelle int[n];
Arrays.fill(dist, entier. MAX_VALUE;

// lastSeen cartographie une valeur -> le dernier indice (dans le double) où il est apparu
Carte<entier,entier> lastSeen = nouveau HashMap<>();

// Traverser deux fois pour tenir compte de la circularité
pour (int i = 0; i < 2 * n; i++) {
Int val = nombres[i % n];
dans curIdx = i % n;

Integer prev = lastSeen.get(val);
si (prev != null) {
int prevIdx = prev % n;
int d = i - prev; // distance le long du tableau double
dist[curIdx] = Math.min(dist[curIdx], d);
dist[prevIdx] = Math.min(dist[prevIdx], d);
}
lastSeen.put(val, i);
}

Liste <Integer> résultat = nouvelle liste d'array<>(requêtes.longueur);
pour (int q : requêtes) {
result.add(dist[q] >= n ? -1 : dist[q]); // si >= n, cela signifie pas de duplicata
}
le résultat du retour;
}
}
«» "

</détails>
**Python**. `def ressouvQueries(nums: List[int], requêtes: List[int]) -> List[int]`" <details><sommary>Cliquez pour agrandir</sommary>

'`python
de taper l'importation Liste
de collections importer par défautdict

def resoluQueries(nums: List[int], requêtes: List[int]) -> Liste[int]:
"""
Retourner la distance circulaire minimale de chaque index demandé à un autre
indice qui détient la même valeur. En l'absence d'un tel index, retourner -1.
"""
n = len(nums)
INF = n + 5 # toute valeur >= n sera traité comme "pas de duplicata"
dist = [INF] * n # distance minimale pour chaque position
last_seen = {} # valeur -> dernier indice en double

# Traverser le tableau deux fois vers la circulaire du modèle
pour i dans la plage(2 * n):
val = nombres[i % n]
pour = i % n
val dans la dernière_vue :
prev = last_seen[val]
d = i - prév # distance positive
dist[cur] = min(dist[cur], d)
dist[prev % n] = min[prev % n], d)
last_seen[val] = i

# Construire des réponses pour les requêtes
retour [d si d < n autre -1 pour d in dist[i] pour i dans les requêtes]
«» "

</détails>
**C++**=___________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________ Cliquez pour agrandir</résumé>

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
#incluez <algorithme>

utilisant l'espace de noms std;

***
* @exposé Recherche la distance circulaire minimale à un autre élément égal pour chaque requête.
*
* @param nums Tableau circulaire des entiers.
* Questions @param Indices pour lesquels nous avons besoin de réponse.
* @return vector<int> Distances minimales (ou -1 si aucun duplicata n'existe).
*/
vector<int> resolveQueries(vector<int>& nums, vector<int>& requêtes) {
int n = nombres.size();
const int INF = n + 5; // toute valeur >= n sera traité comme "pas de duplicata"
vecteur<int> dist(n, INF);

unordered_map<int, int> lastSeen; // value -> dernier indice en double traversée

pour (int i = 0; i < 2 * n; ++i) {
Int val = nombres[i % n];
l'ent cur = i % n;
auto it = lastSeen.find(val);
si (it != lastSeen.end()) {
int prev = it->seconde;
int d = i - prev; // distance positive
dist[cur] = min(dist[cur], d);
dist[prev % n] = min[prev % n], d);
}
lastSeen[val] = i;
}

vecteur <int> ans;
as.reserve(queries.size());
pour (int q : requêtes) {
as.push_back(dist[q] < n ? dist[q] : -1);
}
le retour des an;
}
«» "

</détails>

Les trois codes:

La complexité temporelle La complexité spatiale Autres
Il s'agit d'un projet pilote.
Java **O(n)**
Python **O(n)**
* * * * * * * *

-----------------------------------------------------------------------------------

- Oui. 2. Article du blog

> **Titre**
> *Le LeetCode 3488: Les questions les plus proches sur l'égalité des éléments – Le bon, le mauvais et le mauvais

> **Description détaillée**
> Apprenez une solution Slick O(n) à LeetCode 3488, complète avec le code Java, Python et C++, les pièges de cas de bord, les conseils d'entrevue, et comment ce problème peut vous poser un rôle FAANG.

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Pourquoi LeetCode 3488 est une gemme d'entrevue cachée] (#Why-leetcode-3488-est-a-hidden-interview-gem)
3. [Approche : Le Trick Hashmap à deux pass] (#Approche-le-deux-pass-hashmap-trick)
4. [Détails de mise en œuvre en Java, Python & C++](#implémentation-details-in-java-python--c)
5. [Complexité temporelle et spatiale] (#temps--complexité spatiale)
6. [Cas et pièges communs] (#Cas et pièges communs)
7. [Les choses qui gâchent votre solution]
8. [Stratégie d'entrevue : transformer le problème en un projet de discussion] (#stratégie d'entrevue-transformant le problème en un projet de discussion)
9. [Conclusion et prochaines étapes] (#conclusion - prochaines étapes)

---

### Aperçu du problème <un nom="problème-overview"></a>

**Fermer les questions sur les éléments égaux** (LeetCode 3488) vous demande de prendre un tableau **circulaire** `nums` et, pour chaque indice `i` donné dans `queries`, de retourner la distance minimum *circulaire* à *un autre* indice qui détient la même valeur que `nums[i]`. Si `nums[i]` est unique, retourner `-1`.

Pourquoi est-ce un gros problème d'entrevue ? * *

Raison
C'est pas vrai.
**Circularité**= Ajoute une torsion qui rend suspectes les astuces standard à deux pointeurs ou à fenêtres coulissantes. Autres
**Hash-map heavy**= Testez votre confort avec `Map/HashTable` – une structure de données de base dans chaque entretien FAANG. Autres
**L'élégance du two-pass se manifeste par un *pass unique sur un tableau doublé* – un motif qui apparaît souvent dans d'autres problèmes de tirage circulaire. Autres
**Les plus grandes contraintes**. Autres

---

### Le bon <un nom "le bon"></a>

1. **Linear Time, Linear Space** – L'algorithme choisi tourne dans **O(n)** time et **O(n)** space, facilement gérer les contraintes maximales.
2. **Déterministe et simple** – Une seule carte de hachage et deux tableaux entiers sont utilisés; aucune recherche binaire ou DP multidimensionnelle.
3. **Extensible** – Le même motif résout d'autres problèmes comme *Dupliquer le plus près d'un tableau circulaire*, *Distance la plus courte jusqu'au caractère* ou *Étapes minimales du tableau circulaire*.

---

### Le mauvais <un nom="le mauvais"></a>

Numéro Ce qui peut mal tourner Comment l'éviter
-- -- -- -- -- -- -- -- -- -- --
**Distance non-initialisée**. Ne pas définir `disting` à une valeur plus grande que `n` conduit à des vérifications incorrectes. Utilisez une sentinelle `INF = n + 5` (ou `INT_MAX` si vous ajoutez un `< n` garde explicite). Autres
**Contrôler seulement l'événement immédiat précédent manque le chemin circulaire *le plus court* lorsque les duplicatas sont éloignés. Autres
**Off‐by‐one dans les opérations mod** Toujours utiliser `(prev % n + n) % n` si vous n'êtes pas sûr du signe. Autres
**Contrairement à l ' état de retour** directement même si `dist[i]== INF '....Comparer avec `n` (la longueur du tableau) pour décider .. Autres

---

### L'Ugly <a name="the-ugly"></a>

**Pièges de rendement dans la production– Code de catégorie**

- **Attaques de collision de HashMap**
Si vous êtes sur une plate-forme qui utilise des données de test contradictoire, le standard `HashMap` en Java ou `unordered_map` en C++ peut se dégrader en O(n2).
**Fix**: Utilisez `Int2IntOpenHashMap` (FastUtil) ou `std::unordered_map<int, int>` avec un `hash` personnalisé qui mélange des bits (par exemple, `valeur ^= valeur >> 16;».

- **Mémoire sur la tête des objets d'enveloppe**
Dans Java, `ArrayList<integer>` crée les objets `integer` encadrés. Pour les entrées à l'échelle de l'entrevue, c'est très bien, mais dans un système de production à volume élevé, vous auriez utilisé `int[]` pour la vitesse.

- **Modules inefficaces* *
Utiliser `%` à l'intérieur d'une boucle étroite peut être coûteux en C++. Utilisez un précalculé `n2 = 2 * n` et basculez l'index manuellement:
'`cpp
int idx = i < n ? i : i - n; // alternative rapide à i % n lorsque i < 2*n
«» "

---

### Mise en oeuvre Marche à suivre <un nom></a>

1. **Structures de données**
- `dist[i]` – distance circulaire minimale de l'index `i` à un autre élément égal.
- `lastSeen` – carte de hachage d'une valeur à l'index *last* (dans la traversée doublée) où cette valeur est apparue.

2. **Pourquoi doubler le tableau? **
Un tableau circulaire signifie qu'après l'index `n‐1` vous retournez à `0`.
En passant par les indices `0 ... 2*n-1` et en utilisant `i % n`, nous **simulons** que l'enroulement tout en maintenant la traversée linéaire.

3. ** Mises à jour sur la distance**
Lorsque nous voyons une valeur qui a déjà été vue à l'index `prev`, la distance exacte ** le long du tableau double** est `i - prev`.
Cette distance est une distance circulaire *valable* pour les deux positions:
Texte
i : situation actuelle
prev : occurrence précédente
d = i - prév (entier positif)
«» "
La mise à jour à la fois `dist[cur]` et `dist[prev % n]` garantit que chaque paire double influence la distance minimale des deux indices impliqués.

4. **Réponses finales**
Tout "dist[i] >= n` signifie que la distance de la paire dépasse la longueur du tableau d'origine – en d'autres termes, aucune duplication n'existait.
Remplacer ces rubriques par `-1`.

---

### Complexité temporelle et spatiale <un nom="complexité temporelle-espace"></a>

Langue Heure Espace
- C'est quoi ?
Java **O(n)**
Python **O(n)**
* * * * * * * *

L'algorithme effectue **2 × n** opérations simples – parfait pour les limites de temps LeetCode.

---

### Conseils d'entrevue <un nom="interview-tips"></a>

Pourquoi ça compte ?
-- -- -- -- --
**Expliquez la circularité tôt** Autres
**Mention l'astuce du doublage** C'est un modèle généralement attendu pour les problèmes circulaires (p. ex., les étapes minimales dans un tableau circulaire). Autres
Autres **Parlez des cas de bord** – occurrences uniques, tableau de longueur 1, duplicata à la fin – les intervieweurs aiment vous voir les couvrir. Autres
** Optimisation de l'espace de concentration** – si l'intervieweur est strict au sujet de la mémoire, expliquez comment stocker les distances en « nombres » après la pré-computation (en place). Autres
**Surligner l'utilisation du hash‐map** – il démontre que vous pouvez cartographier les valeurs pour les indexer efficacement et gérer de grands ensembles de données. Autres
**Afficher comment tester** – écrire des tests rapides à l'unité (ou une méthode principale) pour vérifier les entrées de l'échantillon. Autres

---

### Conclusion <un nom="conclusion"></a>

*LeetCode 3488 – Le plus proche Equal Element Queries* est une belle vitrine d'un simple tour linéaire** qui gère la circulaire, les duplicatas et les distances tout à la fois.

En maîtrisant les deux passages sur un tableau double, vous pouvez répondre au problème en temps O(n) et en espace O(n) – une solution qui se sent à la fois propre et puissante.

Les implémentations dans **Java, Python et C++** vous prouvent que vous êtes prêt pour toutes les piles technologiques majeures.

Prenez cette solution, ajoutez quelques tests unitaires, et partagez-la sur votre GitHub. C'est un point de discussion solide** pour votre prochaine entrevue FAANG, car vous pourrez discuter :

1. *Pourquoi les tableaux circulaires sont difficiles. *
2. *Comment un simple hash‐map peut transformer un problème apparemment quadratique en temps linéaire. *
3. * L'importance du calcul attentif de la distance et des valeurs sentinelles. *

Bon codage, et bonne chance pour votre voyage d'entrevue! C'est ce qu'il a dit.

---

**Mots clés pour le référencement:**
- LeetCode 3488
- Questions sur les éléments les plus proches
- distance du tableau circulaire
- Solution O(n)
- algorithme de carte de hachage
- Solution d'entretien Java
- Codage d'entrevues Python
- C++ Problème de LeetCode
- Conseils d'entretien FAANG
- tableau de hachage des structures de données

N'hésitez pas à modifier les rubriques de l'article ou les méta tags pour correspondre à votre marque personnelle ou au rôle spécifique que vous ciblez.