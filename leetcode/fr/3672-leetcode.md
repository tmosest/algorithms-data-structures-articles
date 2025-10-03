---
titre: LeetCode 3672. Somme des modes pondérés en Subarrays -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Somme des modes pondérés dans les sous-barrages – Un guide complet
*LeetCode 3672 – Medium.

---

- Oui. 1. Récapitulation des problèmes

On vous donne un nombre entier (taille ≤ 105) et un nombre entier `k`.
Pour chaque subarray contigu de longueur `k` nous devons:

Description des étapes Autres
- C'est quoi ?
Autres **1**= Compter la fréquence de chaque élément dans le sous-réseau. Autres
Autres ** 2** Le *mode* est l'élément avec la plus haute fréquence; si plusieurs éléments se lient, choisissez le **plus petit**. Autres
Autres **3**= Le *poids* du sous-réseau est "mode * fréquence(mode)". Autres
Autres **4**= Sommer les poids de tous les sous-barrages de longueur «k». Autres

Retourne cette somme comme une «long».

> **Exemple**
> `nums = [1,2,2,3], k = 3` → poids: `4` (pour `[1,2]`) + `4` (pour `[2,2]`) = **8**.

---

- Oui. 2. Pourquoi ce problème est une grande question d'entrevue

Aspect Pourquoi ça compte
-- -- -- -- -- --
**Fenêtre coulissante** Autres
**Fréquences de comptage** Autres
**Statuts de la commande**= Besoin de récupérer rapidement le mode → utiliser une BST* ou un "pap* équilibré avec comparaison personnalisée. Autres
**Tie-Breaking** Exclusivité de l'étui qui teste soigneusement la conception de comparaison. Autres
**Temps/Complexité de l'espace** Autres
**Agnosticisme de langue**= Solvable en Java, Python, C++ → montre que vous pouvez adapter les structures de données à la langue. Autres

---

- Oui. 3. Stratégie de haut niveau

1. **Maintenir une carte de fréquence** `freq[value] = count` pour la fenêtre actuelle.
2. **Gardez un conteneur trié** qui commande des paires par **fréquence descendante, valeur ascendante**.
* Le premier élément est toujours le mode courant.
3. **Coulez la fenêtre** une étape à la fois:
* Supprimer l'élément sortant – mettre à jour la carte de fréquence et le conteneur trié.
* Ajouter l'élément entrant – mettre à jour les mêmes structures.
* Si la fenêtre est pleine (`taille == k`), lisez le premier élément du conteneur trié et ajoutez son poids à la réponse.

Comme chaque élément est inséré et retiré au plus une fois du contenant trié, le coût total est `O(n log n)`.

---

- Oui. 4. Détails de mise en œuvre par langue

### 4.1 Java (TreeSet)

L'arbre "TreeSet" de Java est un arbre rouge-noir qui nous permet de stocker des paires et de maintenir l'ordre.
Nous stockons `int[] {freq, value}` et fournissons un comparateur personnalisé:

"Java
TreeSet<int[]> set = nouveau TreeSet<>(
(a, b) -> a[0] != b[0] ? Integer.compare(b[0], a[0]) : Integer.compare(a[1], b[1])
);
«» "

Nous utilisons également un `HashMap<Integer, Integer>` pour la table de fréquence.

Code complet ci-dessous (même que la solution éditoriale mais annotée pour plus de clarté).

"Java
Importation de java.util.*;

solution de classe publique {
mode public longPoids(int[] nombres, int k) {
int n = longueur nums;
long ans = 0L;

// Carte de fréquence : valeur -> Nombre
Carte<integer, integer> freq = nouveau HashMap<>();

// Ensemble trié de paires {compte, valeur}
TreeSet<int[]> set = nouveau TreeSet<>(
(a, b) -> a[0] != b[0] ? Integer.compare(b[0], a[0]) : Integer.compare(a[1], b[1])
);

Int gauche = 0;
pour (int right = 0; right < n; right++) {

// Ajouter un nouvel élément
int val = nombres[droite];
int cnt = freq.getOrDefault(val, 0);
si (cnt > 0) set.remove(new int[]{cnt, val});
cnt++;
freq.put(val, cnt);
set.add(new int[]{cnt, val});

// Supprimer l'ancien élément lorsque la fenêtre > k
Si (droite - gauche + 1 > k) {
int oldVal = nombres[gauche];
Int oldCnt = freq.get(oldVal);
set.remove(new int[]{oldCnt, oldVal});
oldCnt...
si (vieille Cnt) 0) {
freq.remove(oldVal);
} autre {
freq.put(oldVal, oldCnt);
set.add(new int[]{oldCnt, oldVal});
}
gauche++;
}

// Lorsque la fenêtre est exactement k, ajoutez son poids
si (droite - gauche + 1 == k) {
int[] modeInfo = set.first(); // freq le plus élevé, valeur la plus faible
ans += 1L * modeInfo[0] * modeInfo[1]; // poids = freq * valeur
}
}
le retour des an;
}
}
«» "

> **Complexités**
> Heure: `O(n log n)` (facteur log des opérations `TreeSet`)
> Espace: `O(n)` (carte de fréquence + jeu)

---

#### 4.2 Python (Contients Sortés + Compteur)

La bibliothèque standard de Python est dépourvue d'une BST équilibrée, mais le paquet de "conteneurs triés" de tiers nous donne une "SortedList" avec des opérations O(log n).
Si vous ne pouvez pas utiliser des libs externes, vous pouvez émuler la logique avec une suppression max-heap + paresseuse – le code ci-dessous utilise `SortedList` pour la brièveté.

'`python
Importations provenant des collections Compteur
de conteneurs triés importer TriéListe

Solution de classe:
def modeWeight(self, nums: list[int], k: int) -> Int:
n = len(nums)
freq = compteur()
# Trier par (-compte, valeur) → plus grand compte d'abord, plus petite valeur d'abord
ordre = TriéListe(key=lambda x: (-x[0], x[1]))

ans = 0
gauche = 0
pour droite, val in énumérate(nums):
# ajouter nouveau
c = freq.get(val, 0)
si c:
ordre.supprimer(c, val))
c += 1
freq[val] = c
ordre.add(c, val)

À gauche
Si droite - gauche + 1 > k:
old = nombres[gauche]
c_old = freq[old]
order.supprimer((c_old, old))
_Ancien -= 1
si c_old :
freq[old] = c_old
order.add((c_old, old))
Sinon:
del freq[old]
gauche += 1

Si droite - gauche + 1 == k:
mode_count, mode_val = ordre[0]
+= mode_count * mode_val

retour et
«» "

> **Complexités**
> Durée: `O(n log n) "
> Espace: 'O(n) "

---

### 4.3 C++ (carte_non ordonnée + multiset)

Les paires de magasins "{count, value}" et utiliser un comparateur personnalisé:

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long modePoids(vecteur<int>& nums, int k) {
int n = nombres.size();
long an = 0;

unordered_map<int,int> freq;
// multiset trié par freq desc, valeur asc
auto cmp = [](paire de const<int,int>& a, paire de const<int,int>& b) {
if(a.first != b.first) retourner a.first > b.first; // freq plus grand d'abord
retour a.seconde < b.seconde; // valeur plus petite d'abord
};
multiset<pair<int,int>, decltype(cmp)> order(cmp);

Int gauche = 0;
pour(int right=0; right<n; ++ right){
int val = nombres[droite];
int c = freq[val];
i c) order.erase(order.find({c,val}));
++c;
freq[val] = c;
ordre.insérer({c,val});

i (droite - gauche + 1 > k) {
int old = nombres[gauche];
int c_old = freq[old];
ordre.erase(order.find({c_old,old}));
_vieux;
si(c_old){
freq[old] = c_old;
order.insert({c_old,old});
} autre {
freq.erase(ancien);
}
+ + gauche;
}

if(droite - gauche + 1 == k){
auto it = order.begin();
ans += 1LL * it->premier * it->deuxième;
}
}
le retour des an;
}
};
«» "

> **Complexités**
> Durée: `O(n log n) "
> Espace: 'O(n) "

---

- Oui. 5. Bonne, mauvaise et laid de la solution

Catégorie: Ce qui fonctionne bien
Il n'y a pas de lien direct entre les deux.
**Bonne**) • La fenêtre coulissante maintient chaque élément traité deux fois (ajouter/supprimer). <br>• `TreeSet` / `multiset` maintient automatiquement le mode à l'avant. <br>• Pas besoin de recalculer les fréquences à partir de zéro.
**Bad**) • Coût des opérations `TreeSet` ou `multiset` `O(log n)` – acceptable mais peut être lourd si `k` est petit et `n` grand. Utilisez la suppression heap + paresseux si les libs externes ne sont pas autorisées. Autres
**Ugly**. • La suppression d'un élément d'une BST nécessite la paire exacte ; nous devons connaître le compte précédent pour le supprimer. <br>• Si nous oublions de supprimer l'ancienne paire, l'ensemble contiendra des entrées discontinues, corrompant le mode. Autres

---

- Oui. 6. Autres approches (lorsque " O(n log n) " est trop lent)

Démarche
C'est pas vrai.
Autres Si `nums[i] ≤ 105`, nous pouvons utiliser un tableau de taille `105 + 1` pour les fréquences et maintenir un second tableau pour les nombres → `O(1)` insertion/suppression. <br>Cependant, pour obtenir le mode, il faut toujours scanner le tableau des nombres (`O(maxValue)`), qui est `O(105)` par fenêtre → trop lent. Autres
Autres **Two Heaps + Lazy Deletion** .Utilisez un max-heap pour `(count, value)` et une carte de hachage pour les suppressions paresseuses. <br>Insertion O(log n), suppression O(1) (lazy). <br>Still `O(n log n)`, mais le facteur constant peut être inférieur à `multiset`. Autres
Autres **Segment Tree / Binary Indexed Tree**.Enregistrez les fréquences dans un arbre Fenwick et maintenez un arbre segmenté sur les valeurs pour demander la fréquence maximale. <br>Complexe à mettre en œuvre; pas nécessaire pour cette contrainte. Autres

---

- Oui. 7. Pourquoi ce blog vous aide à trouver un emploi

* **Title riche en mots clés** – Le sum de modes pondérés dans Subarrays – LeetCode 3672.
* **SEO-friendly** – Utilisation fréquente de termes tels que le code LeetMedium, le code Java/Python/C++, la fenêtre coulissante, le codeBalanced BST, le code Interview Question.
* **Explication claire, étape par étape** – Les recruteurs apprécient les ingénieurs qui peuvent articuler le processus de pensée.
* **Langues multiples** – Démontre la capacité d'adaptation.
* **Le code annoté** – montre non seulement la réponse, mais comment le construire.
* **Débat d'Edge** – Points saillants des pratiques de codage défensives.

Ajouter cet article à votre site Web personnel ou GitHub README indique que vous n'êtes pas seulement la solution de problèmes, vous êtes l'apprentissage, la documentation et le partage des connaissances. C'est exactement ce que cherchent les intervieweurs.

---

- Oui. 8. Dernier départ

La clé de ce problème est de reconnaître que le mode ** peut être conservé à l'avant d'un conteneur trié** pendant que nous mettons à jour les fréquences à la volée.
La solution `O(n log n)` résultante est à la fois propre et efficace à travers Java, Python et C++.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---

*Auteur: Votre nom – Ingénieur logiciel & Problème‐ Résoudre l'enthousiasme. *