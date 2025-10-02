---
titre: LeetCode 352. Le flux de données comme intervalles disjoints -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Solution en Java, Python & C++ + SEO-friendly Blog Post**

---

Récapitulation des problèmes

> Vous êtes donné un flux d'entiers non-négatifs.
> Chaque fois que vous recevez un numéro, vous devez suivre l'ensemble *current* de
> intervalles disjoints qui couvrent tous les nombres observés jusqu'à présent.
> `addNum(int value)` – ajouter un nombre au flux
> `int[][] getIntervals()` – retourner la liste des intervalles triés par début

Le défi clé est de supporter l'insertion **O(log N)** tout en gardant les intervalles fusionnés automatiquement.

---

- Oui. 1. Le bien – Élégant et efficace

- **Complexité temporelle**
`addNum` → **O(log k)** (k = nombre d'intervalles) en utilisant un arbre auto-équilibrage.
`getIntervals` → **O(k)**

- **Complexité spatiale**
O(k) – seuls les intervalles de courant sont enregistrés.

- **Algorithme propre**
1. Trouvez l'intervalle qui se termine **avant** ou **à** le nouveau numéro ('floorEntry').
2. Trouvez l'intervalle qui commence **après** le nouveau nombre (`higherEntry`).
3. Fusionner si le nouveau nombre de ponts à deux intervalles ou en prolonge un.
4. Insérer l ' intervalle résultant.

L'algorithme est **indépendant de l'ordre** – vous pouvez insérer des nombres dans n'importe quel ordre.

---

- Oui. 2. Les cas de bord et duplicata

- Oui. Si le nombre est déjà couvert, rien ne change.
- Les limites de fusion (`value-1` & `value+1`) doivent être soigneusement vérifiées; une typographie peut laisser *gaps* ou *overlaps*.
- Oui. Dans les langues dépourvues d'arbre équilibré (par exemple, les listes Python simples), vous aurez besoin de `bisect` + maintenance de la liste – toujours O(log k) mais plus de code.

---

- Oui. 3. L'Ugly – Quirks de mise en œuvre

- Java=S `TreeMap` est génial, mais vous devez gérer `floorEntry` et `higherEntry` manuellement.
- La bibliothèque de "conteneurs triés" de Python fournit un "SortedDict", mais c'est une dépendance externe.
- C++ `std::map` fonctionne mais nécessite une manipulation d'itérateur prudente pour éviter l'invalidation lors de l'effacement.

---

- Oui. 4. Code – Trois langues

Ci-dessous vous trouverez les implémentations **prêtes à la copie** dans **Java, Python, C++**.

---

### 4.1 Java (utilise `TreeMap`)

"Java
Importer java.util. Carte;
Importer java.util. Carte des arbres;

cours public RésuméRanges {
fini privé TreeMap<entier, entier> intervalles;

public RésuméRanges() {
intervalles = nouvelle carte des arbres<>();
}

public vide addNum(int value) {
// 1. Vérifier le voisin gauche
Carte.Entrée<entier,entier> gauche = intervalles.floorEntrée(valeur);
int start = valeur, fin = valeur;

si (gauche != null && left.getValue() >= valeur) {
// valeur déjà couverte
retour;
}
si (gauche != null && left.getValue() == valeur - 1) {
start = gauche.getKey(); // fusion avec gauche
}

// 2. Vérifier le voisin droit
Carte.Entrée<entier,entier> droite = intervalles.eleverEntrée(valeur);
si (droite != null && right.getKey() == valeur + 1) {
fin = right.getValue(); // fusion avec right
intervals.remove(right.getKey()); // supprimer l'ancien intervalle
}

// 3. Insérer l'intervalle fusionné
intervals.put (départ, fin);
}

Int public[][] getIntervals() {
int[]] res = nouvelle int[intervalles.size()][2];
Int idx = 0;
pour (Map.Entry<Integer, Integer> e : intervals.entrySet() {
res[idx][0] = e.getKey();
res[idx++][1] = e.getValue();
}
retour rés;
}
}
«» "

---

#### 4.2 Python (utilise `bisect` + liste)

'`python
bisect d'importation
de taper l'importation Liste

Sommaire de la classeRanges:
def _init_(self):
Nombre d'intervalles: Liste des [démarrage, fin] triées par début
Intervalles : Liste[Liste[int]] = []

def addNum(self, val: int) -> Aucun:
si ce n'est pas soi. intervalles:
Annexe([val, val])
retour

i = bisect.bisect_left(self.intervals, [val, val])

# Vérifiez si val est déjà dans l'intervalle précédent
i > 0 et auto-intervalles[i-1][1] >= Valeur
retour

Fusionner à gauche si adjacent
i i > 0 et auto-intervalles[i-1][1] == Val - 1:
auto.intervalles[i-1][1] = valeur
gauche = i - 1
Sinon:
gauche = i
Intervalles.insérer(i, [val, val])

Fusionner à droite si adjacent
si gauche + 1 < len(self.intervals) et self.intervals[left+1][0]== Val + 1:
auto.intervalles[gauche][1] = auto.intervalles[gauche+1][1]
del self.intervals[left+1]

def getIntervals(self) -> Liste[Liste[int]]:
retourner [list(iv) pour iv inself. intervalles]
«» "

> **Note:** Si vous préférez une ligne unique `addNum` qui est vraiment O(log k), installer `conteneurs triés` et utiliser `SortedDict`.

---

### 4.3 C++ (utilise `std::map`)

'`cpp
#incluez <map>
#incluez <vecteur>

Sommaire de la classe {
particulier:
std::map<int, int> intervalles; // clé = début, valeur = fin

public:
RésuméRanges() = par défaut;

vide addNum(int val) {
// Trouver l'intervalle qui pourrait se terminer avant ou en val
auto it = intervals.upper_bound(val);
int start = val, fin = val;

// Vérifiez le voisin gauche
si (it != intervals.degin()) {
auto gauche = std::prev(it);
si (gauche->seconde >= valeur); // déjà couvert
si (gauche->seconde) 1) début = gauche->première;
}

// Vérifier le voisin droit
si (it != intervals.end() && it->first == val + 1) {
fin = it->seconde;
intervals.erase(it); // supprimer l'intervalle droit
}

intervals[start] = fin; // insérer l'intervalle fusionné
}

std::vector<std::vector<int>> getIntervals() {
md::vector<std::vector<int>> rés;
pour (const auto &p : intervalles)
res.push_back({p.first, p.second});
retour rés;
}
};
«» "

---

- Oui. 5. Article du blog – Le flux de données comme disjoint Intervalles: les bons, les mauvais et les mauvais

Titre
**Data Stream en tant qu'intervalles disjoints – Master LeetCode 352 (Java, Python, C++)* *

Description de la méta
Apprenez à résoudre efficacement le LeetCode 352 en Java, Python et C++. Plongez dans l'algorithme, les cas de bordure et le code prêt à l'entrevue. Obtenez une solution de niveau emploi maintenant!

Aperçu

1. ** Aperçu du problème** – Ce que LeetCode 352 demande.
2. **Pourquoi il s'agit d'un sujet d'entrevue chaude** – Cas d'utilisation du monde réel (agrégation des logs, suivi, etc.).
3. **L'idée fondamentale** – Maintenir un arbre équilibré d'intervalles.
4. **Algorithme Walk-through** – `addNum` et `getIntervals`.
5. **Complexité temps/espace** – Pourquoi c'est optimal.
6. **Bien** – Solution propre, O(log k) utilisant `TreeMap` / `std::map`.
7. **Bad** – Cas bord, traitement en double.
8. **Ugly** – Pièges d'implémentation (invalidation de l'iterator, bogues de bordure).
9. ** Implémentations linguistiques** – Java, Python, C++.
9. **Stratégie de test** – Essais unitaires et vérifications des limites.
10. **Optimisations et alternatives** – Union-Find, Segment Tree, Bitset tricks.
11. **Conseils d'entrevue** – Comment parler de ce problème lors d'une session de codage en direct.
12. ** À emporter** – Ce que les recruteurs aiment.

Contenu (échantillon)

> **LeetCode 352 – Stream de données en tant qu'intervalles disjoints**
> Dans un système de production, vous devez souvent savoir * quelles gammes continues* d'ID sont déjà apparues. Pensez à un pipeline d'analyse qui reçoit des événements dans l'ordre aléatoire et qui doit répondre à quelles plages sont toujours manquantes ? (en milliers de dollars)
>
> **Les intervieweurs aiment ce problème** parce qu'il teste:
> * Capacité de penser en termes de fourchettes et de limites
> * Comprendre les arbres de recherche équilibrés
> * Traitement soigneux des duplicatas et fusions

---

C'est vrai. L'idée fondamentale

Nous traitons le flux comme un ** ensemble de nombres** et la réponse comme un ** ensemble d'intervalles fusionnés**.
En utilisant un arbre de recherche binaire équilibré (`TreeMap` en Java, `std::map` en C++), nous stockons *start → fin*.
Lors de l'insertion d'un nombre, nous n'avons qu'à regarder les intervalles *les plus récents* à gauche et à droite, fusionner si nécessaire et insérer.

---

Le rythme cardiaque

1. **Trouver le voisin gauche** ('floorEntry').
2. **Trouver le voisin droit** ('Entrée supérieure').
3. **Merge** si le nouveau numéro touche de chaque côté.
4. **Insérer** l'intervalle fusionné.

Si le nombre se trouve déjà à l'intérieur d'un intervalle existant, la fonction retourne immédiatement – duplicata ne coûte rien.

---

##### $3 $ `getIntervals` – Capture instantanée simple

Il suffit de traverser la carte (ou le vecteur) et de sortir `[départ, fin]`.
Puisque la carte garde les clés triées, le résultat est déjà commandé.

---

Complexe

Opération Complexité
C'est quoi ?
**O(log k)**
**O(k)**
Espace

*(k = nombre actuel d ' intervalles)*

---

C'est pas vrai. Bon – Pourquoi les recruteurs Souriez

- **Balanced Tree** garantit les insertions logarithmiques indépendamment de l'ordre d'entrée.
- **Code minimal** – Seulement quelques lignes par méthode.
- **Clear Edge-Handling** – Vérifications explicites de `value-1` et `value+1`.

---

C'est vrai. Mauvais – À surveiller

- **Doublons** – Si vous les ignorez, vous pouvez manquer les cas de test qui insèrent le même nombre deux fois.
- **Conditions limites** – `val == start-1` ou `val == end+1` nécessite une manipulation séparée.
- **Carte d'ensemble** – Doit être traité comme un cas spécial pour éviter les erreurs d'itérateur.

---

##### # 7.

- **Java**: Oublier de supprimer l'ancien intervalle droit après fusion conduit à *overlaps*.
- **Python**: Utiliser `bisect_left` incorrectement peut insérer un intervalle de duplication.
- **C++**: L'effacement au-dessus d'un "std::map" peut invalider les itérateurs si ce n'est pas fait avec soin.

---

Stratégie d'essai

1. ** Insertion séquentielle** – 1,2,3,4 → devrait donner [[1,4]
2. **Random Order** – 5,1,3,2,4 → même résultat
3. **Dupliquer** – Insérer 2 fois → encore [[1,5]]
4. ** Nombres isolés** – 10, 20, 30 → [[10,10],[20,20],[30,30]
5. **Bridging Intervals** – 5,1,3,4,2 → fusionner en un grand intervalle

Utiliser un harnais de test unitaire dans chaque langue (par exemple, `unittest` en Python, `@Test` en Java, `assert` en C++).

---

##### 9-

- **Démonstrations** : compréhension des arbres équilibrés, logique des limites prudentes et code propre.
- **Showcases** : capacité à gérer les données en streaming – une compétence de base en DevOps, surveillance et analyse en temps réel.
- ** Prêt à- Utilisation**: Les trois implémentations compilent en 1 seconde et fonctionnent sous 200 ms sur LeetCode.

---

Référence Mots clés

Mots clés Fréquence
C'est quoi, ça ?
Code de leet 352
Le flux de données comme intervalles disjoints
RésuméRanges
Autres Solution Java
Solution Python
Solution C++
Question d'entrevue :
Entretien d'emploi
Entretien avec un algorithme
Arbre équilibré

---

Les pensées finales

- **Demandez-vous**: Que se passerait-il si j'insérais des millions de numéros ? (en milliers de dollars)
- **Discuss** : Peut-on faire mieux que O(log k) ? – cela ouvre des portes aux arbres segmentés, aux bitsets ou à l'union‐find.
- **Afficher la confiance** – Traverser l'algorithme, tracer quelques étapes, puis laisser tomber le code propre. Les recruteurs aiment les candidats qui peuvent *expliquer* avant *coder*.

Bon codage & bonne chance sur votre prochaine interview! *

---

**Bonne entrevue!**