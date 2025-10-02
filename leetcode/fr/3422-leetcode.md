---
titre: LeetCode 3422. Opérations minimales pour assurer l'égalité des éléments subarray
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La maîtrise du LeetCode 3422
### Opérations minimales pour assurer l'égalité des éléments subarray
**Le bon, le mauvais et le mauvais** – Un guide complet (Java / Python / C++)

---

Récapitulation des problèmes

> **Grâce à un nombre entier et à un k entier.
> Vous pouvez incrémenter ou diminuer tout élément de `nums` par `1` n'importe quel nombre de fois.
> **Objectif:** Trouver le nombre minimum d'opérations requis de sorte que *au moins un* sous-ensemble de taille `k` contient **tous les éléments égaux**.

«» "
Entrée: nombres = [4,-3,2,1,-4,6], k = 3
Produit: 5
«» "

---

Pourquoi ce problème se trouve-t-il

* **Véritable étoile de l'interview** – apparaît sur de nombreuses playlists.
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
* **Pièges d'arrêt** – manipulation des duplicatas, nombres négatifs et maintien efficace de la médiane.

---

- Oui. 1. L'approche naïve – Que ne pas faire

Texte
Pour chaque fenêtre de taille k
Pour chaque valeur x de -10^6 à 10^6
Compter les opérations pour faire la fenêtre tous x
«» "

* **Heure:** O(n * (étendue)) → impossible.
* **Espace:** O(1).

**Leçon:** Vous avez besoin d'une médiane *dynamique*, pas d'une analyse de force brute.

---

- Oui. 2. La stratégie gagnante – Sliding-Window Median

1. **Choisir la valeur cible** – la médiane de la fenêtre actuelle donne la somme minimale des différences absolues.
2. **Maintenir deux tas**
* `faible` (pape maximale) – moitié inférieure de la fenêtre
* `haute` (minimum-pap) – moitié supérieure
3. **Continuer à courir les sommes**
* `sumLow` – somme des éléments dans `faible`
* "sumHigh" – somme des éléments en "high" "
4. **Coulissant**
* Insérez le nouvel élément dans l'un des tas.
* Supprimer l'élément sortant (effacement ou multiset paresseux).
* Re-équilibrer ainsi `= faible=="haut=".
* Calculer le coût actuel :
```coût = médiane * bas.size() - sumLow + sumHaut - médiane * haut.size()` "
5. **Tirez le coût minimum** sur toutes les fenêtres.

**Complexités* *

Temps Espace
C'est pas vrai.
Chaque opération O(log k)=O(k) (pavillons + ensembles paresseux)=
Tout au long du passage

---

- Oui. 3. Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
Tous partagent la même logique, mais utilisent des structures de données spécifiques au langage.

> **Astuce:** Si vous êtes sur LeetCode, collez simplement la classe `Solution` dans l'éditeur.
> Si vous préparez un travail, copiez le fichier complet, ajoutez un `main()` pour les tests locaux et poussez vers votre GitHub.

---

#### 3.1 Java – `TreeSet` + Deux Heaps

"Java
Importation de java.util.*;

solution de classe publique {
(a) (b) (b) (b) (b) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (c) (d) (c) (c) (c) (c) (c) (d) (c) (d) (c) (c) (d) (c) (d) (c) (d) (c) (c) (d)) (c) (c) (c)
// Deux files d'attente prioritaires: max-heap (faible), min-heap (haut)
Priorité Queue<Integer> low = new PriorityQueue<>(Collections.reverseOrder());
PrioritéQuue<entier> élevée = nouvelle prioritéQuue<>();

// Pour la suppression paresseuse : occurrences de comptage
Carte<entier,entier> àDelete = nouvelle HashMap<>();

longue sommeLow = 0, sommeHaut = 0;
long ans = long. MAX_VALEUR;

// Aide lambdas
java.util.fonction.IntConsommateur ajouter = (x) -> {
i (faible.isEmpty()) x <= low.peek()) {
low.add(x); sumLow += x;
} autre {
haut.add(x); sommeHaut += x;
}
solde();
};

java.util.fonction.IntConsommateur supprimer = (x) -> {
// Marque à supprimer
Delete.put(x, Delete.getOrDefault(x, 0) + 1);
// Retirez logiquement du tas approprié
si (x <= low.peek()) sumLow -= x;
autre somme Élevée -= x;
// Nettoyer les éléments supérieurs si nécessaire
cleanTop(low, toDelete);
cleanTop(high, toDelete);
solde();
};

java.util.fonction.VoidÉquilibre des fonctions = () -> {
// Tailles d'équilibre: low.size() >= high.size()
pendant que (bas.size() > high.size() + 1) {
Int val = low.poll(); sommeLow -= val;
haut.add(val); sommeHaut += valeur;
cleanTop(low, toDelete);
cleanTop(high, toDelete);
}
pendant que (high.size() > low.size()) {
Int val = high.poll(); sommeHigh -= val;
low.add(val); sumLow += val;
cleanTop(low, toDelete);
cleanTop(high, toDelete);
}
};

java.util.fonction.LongFournisseur getMedien = () -> low.peek();

java.util.fonction.LongFournisseur courantCoût = () -> {
long médian = getMedian.getAsLong();
retour médian * bas.size() - sumLow + sumHaut - médian * haut.size();
};

// Construire la fenêtre initiale
pour (int i = 0; i < k; i++) add.accept(nums[i]);
ans = Math.min(ans, courantCost.getAsLong());

// Fenêtre de diapositives
pour (int i = k; i < nombres.longueur; i++) {
Add.accept(nums[i]);
supprimer.accept(nums[i - k]);
ans = Math.min(ans, courantCost.getAsLong());
}

le retour des an;
}

// Éléments supérieurs propres qui sont marqués pour la suppression
vide privé propre Haut (Priorité) Queue<integer> tas, carte<integer, entier> àSupprimer) {
pendant que (!heap.isEmpty() && toDelete.getOrDefault(heap.peek(), 0) > 0) {
Int val = heap.poll();
àDelete.put(val, àDelete.get(val) - 1);
}
}
}
«» "

> **Pourquoi ça marche* *
> * `faible` garde la moitié *inférieure, donc son maximum (en haut) est la médiane.
> * Suppression paresseuse évite les opérations coûteuses `supprimer` sur `PriorityQueue`.
> * Chaque étape coûte `O(log k)`.

---

### 3.2 Python – `heapq` + `Counter "

'`python
importation heapq
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def minOperations(self, nombres: List[int], k: int) -> Int:
low = [] # max-heap (valeurs inversées)
haute = [] # Min-heap
à_supprimer = Counter()
somme_faible = somme_élevée = 0
ans = flotteur('inf')

def clean:
pendant que le tas et le to_delete[heap[0]] > 0:
val = heapq.heappop(heap)
à_delete[val] -= 1

def solde():
# Assurez-vous que lent(faible) >= lent(élevé)
pendant que len(faible) > len(élevé) + 1:
val = -heapq.heappop(faible)
propre(faible)
heapq.heappush(haut, val)
propre(élevé)
pendant que len(haut) > len(bas):
val = heapq.heappop(élevé)
propre(élevé)

def add(x):
somme non locale faible, somme élevée
si elle n'est pas faible ou x <= -faible[0]:
heapq.heappush (faible, -x)
somme_faible += x
Sinon:
heapq.heappush(haut, x)
somme_élevée += x
solde()

def remove(x):
somme non locale faible, somme élevée
à_delete[x] += 1
si x <= -faible[0]:
somme_faible -= x
Sinon:
somme_élevée -= x
propre(faible)
propre(élevé)
solde()

def médiane():
retour - faible[0]

coût():
m = médiane()
retour m * len(low) - sum_low + sum_high - m * len(high)

Première fenêtre
pour i dans la plage(k):
ajouter(nums[i])
ans = min(ans, coût())

# Diapositive
pour i dans la plage(k, len(nums)):
ajouter(nums[i])
supprimer(nums[i - k])
ans = min(ans, coût())

retour et
«» "

> ** Faits saillants**
> * `low` est un *max-heap* en stockant des négatifs.
> * `Counter` trace les valeurs à ignorer (`to_delete`).
> * Toutes les opérations restent `O(log k)`.

---

### 3.3 C++ – `multiset` + Itérateurs

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long minOpérations(vecteur<int>& nums, int k) {
// multiset garde tout trié
la fenêtre multiset<int>;
somme longue = 0;
longue longue meilleure = LLONG_MAX;

ajouter automatiquement = [&](int x) {
window.insert(x);
somme += x;
};
supprimer automatiquement = [&](int x) {
auto it = window.find(x);
si (it != window.end()) {
-= *il;
window.erase(it);
}
};

médiane automatique = [&]() -> longue {
auto it = window.begin();
avance(it, window.size() / 2); // Indice de la médiane basé sur 0
retour *it;
};

Auto curCost = [&]() -> long {
long med = médiane();
longue gaucheSum = 0, droiteSum = 0;
pour (auto it = window.begin(); it != window.end(); ++it) {
si (*it <= med) gauche Montant *il;
à part juste Somme += *it;
}
longue gauche Cnt = distance (window.begin(), window.find(med));
longue droite Cnt = window.size() - gaucheCnt - 1;
// Coût = somme
retour med * gauche Cnt - gauche Somme + droite Sum - med * droite Cnt;
};

// Construire la première fenêtre
pour (int i = 0; i < k; ++i) ajouter(nums[i]);
best = min(meilleur, curCost());

// Diapositive
pour (int i = k; i < (int)nums.size(); ++i) {
ajouter(nums[i]);
supprimer(nums[i - k]);
best = min(meilleur, curCost());
}

le meilleur retour;
}
};
«» "

> **Pourquoi le multiset est le plus propre en C++**
> * `multiset` donne l'insertion, la suppression et l'accès de l'itérateur à la médiane.
> * Pas besoin de suppression paresseuse – `erase(iterator)` supprime l'élément exact.

---

> **À emporter dans la langue de la crise* *
> *Toutes les trois solutions* conservent la fenêtre triée, conservent les sommes et recalculent le coût minimum en `O(log k)` par étape.

---

- Oui. 4. Débogage et affaires de bord

Pourquoi ça compte ?
- C'est quoi ?
**Numéros du duplicata**. Les Heaps/sets doivent stocker les événements *exacts*. Utiliser `Counter`/`Counter` ou `multiset` avec des itérateurs. Autres
**Valeurs négatives**=La logique médiane tient pour n'importe quel entier, mais méfiez-vous du dépassement en C++.=Utilisez 64-bit (`long') pour toutes les sommes. Autres
**Petit `k` (1)**. Toute fenêtre de taille 1 est déjà égale. Retour `0` tôt. Autres
**Large `k` (≥ n)**= Une seule fenêtre.=Construisez-la une fois, sautez la boucle. Autres

---

- Oui. 5. Tester votre solution

'`python
def test():
sol = Solution()
les opérations de sol.min([4, -3, 2, 1, -4, 6], 3) == 5
les opérations de sol.min([1, 2, 3, 4, 5], 2) == 0
affirme sol.minOpérations([5,5,5], 4) == 0
print("Tous les tests sont passés!")
«» "

Exécutez l'extrait localement. Sur LeetCode, le harnais de test LeetCodeS le fera pour vous.

---

- Oui. 6. Ce que les intervieweurs À propos

Qu'est-ce qu'ils cherchent ?
- C'est pas vrai.
**Clarté algorithmique**** Comprendre la formule médiane et les coûts. Explication ci-dessus + commentaires en ligne. Autres
**Manipulation de caisses d'Edge** Suppression lassime, utilisation `Counter`. Autres
**Complexité du temps**"O(n log k)". Autres
**Codage style** Les meilleures pratiques linguistiques (par exemple, "Collections.reverseOrder()" en Java). Autres

---

- Oui. 7. SEO-Optimized Blog – Comment il aide votre resume

* **Titre et étiquettes**
* `LeetCode 3422`, `Minimum Operations Subarray`, `Java solution`, `Python solution`, `C++ solution`, `sliding window médiane`, `algorithm interview`, `coding interview`, `software engineer`.

* **Description de la méta (=160 caractères)* *
> Solve LeetCode 3422 en Java, Python et C++. Apprenez la stratégie médiane de la fenêtre coulissante, obtenez une analyse de l'espace temporel et des conseils de carrière pour votre prochaine entrevue en génie logiciel. (en milliers de dollars)

* **Rich Snippets** – Ajouter un bloc JSON‐LD pour *Comment faire* du contenu.

html
<type de texte="application/ld+json">
{
"@context" : "https://schema.org",
"@type" : "HowTo",
"nom": "Maîtrise du LeetCode 3422: Opérations minimales pour rendre les éléments subarray égaux",
"description": "Un guide complet avec des solutions Java, Python et C++ et des interviews."
"étape": [
{"@type":"HowToStep","texte":"Comprendre le problème et pourquoi la médiane est optimale."},
{"@type":"HowToStep","texte":"Mise en œuvre d'une fenêtre coulissante médiane en utilisant deux tas."},
{"@type":"HowToStep","texte":"Optimisez pour les duplicata avec suppression paresseuse ou multiset."},
{"@type":"HowToStep","texte":"Validez contre les cas de bord et l'analyse temps/espace."}
- Oui.
}
</script>
«» "

* ** Liens internes** – lien vers d'autres articles de blogs comme "Two-Pointer Tricks for Interviews" ou "Heap Balancing Basics".

* **Backlinks** – mentionnez la repo GitHub et invitez les lecteurs à regarder le projet.

---

Les pensées finales – faire entrer le code dans un emploi

1. **Portfolio-ready code** – commit chaque fichier, ajoute des tests unitaires, pousse vers GitHub.
2. **Exposer l'algorithme** dans une vidéo d'une minute ou une diapositive.
3. **Cas de bord des pratiques** – nombres négatifs, duplicata, `k == 1`.
4. **Le temps de la solution** – une note rapide de complexité dans les commentaires montre que vous vous souciez de la performance.
5. **Afficher la pile entière** – être prêt à expliquer à la fois *algorithme* et *implémentation* sur Java, Python et C++.

> **Résultat:** Vous impressionnerez les gestionnaires d'embauche avec une solution *complète, prête à l'entrevue* et un blog poli qui est SEO-friendly, vous prouvant à la fois un codeur et un communicateur.

Bon codage et bonne chance d'atterrissage ce rôle d'ingénieur logiciel! C'est ce qu'il a dit