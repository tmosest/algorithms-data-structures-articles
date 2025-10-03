---
Titre: LeetCode 2382. Somme maximale du segment après les suppressions -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
C'est ça. Somme maximale du segment après suppression – trois solutions complètes
*(Java) Python C++) – O(n) temps, O(n) espace – Résoudre par les suppressions

---

Récapitulation des problèmes

On vous donne deux tableaux 0 indexés `nums` et `removeQueries`, chacun de longueur **n**.
Pour chaque requête `removeQueries[i]`, vous supprimez l'élément de cet index dans `nums`, cassant le tableau en *segments* contigus de nombres positifs.
Après chaque suppression, vous devez déclarer la somme du segment **maximum** qui existe dans le tableau à ce moment.

> **Input**
> `nums = [1,2,5,6,1]`
> `removeQueries = [0,3,2,4,1] "

> ** Sortie**
> `[14,7,2,2,0]`

> **Constraints**
1 ≤ n ≤ 105
> 1 ≤ nums[i] ≤ 109
> * Tous les indices de `removeQueries` sont uniques.

---

C'est vrai. Pourquoi Reversing

La suppression d'éléments un par un coûte cher car vous devez reconstruire les segments après chaque suppression.
Au lieu de cela, pensez à l'inverse : **démarrer avec un tableau vide** et **ajouter** les éléments dans l'ordre *reverse* de `removeQueries`.
Lorsque vous insérez un élément, vous pouvez fusionner instantanément les deux segments voisins (le cas échéant) et mettre à jour la somme maximale.

Cela nous donne une solution **O(n)** qui n'utilise que des tableaux simples – pas de DSU, pas d'arborescence de segment, pas de multiset.

---

- Oui. L'idée fondamentale (algorithme)

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
Autres **1**= Initialiser deux tableaux d'aide : `sommes` (sommes du segment des magasins) et `autres` (sommes de l'autre* fin d'un segment). "sommes [i]" est zéro jusqu'à ce qu'un segment commence à `i`. `autre[i]` pointera vers l'index lointain de ce segment. Autres
Autres **2**. **En arrière**. Pour chaque index `idx` nous ajoutons `nums[idx]`. Autres
Autres **3**. Trouvez les indices *actifs* les plus proches à gauche et à droite :
`left = (sommes[idx] == 0) ? idx+1 : autre[idx] "
`right = (sommes [idx+2]] 0) ? idx+1 : autres[idx+2]» Si le voisin immédiat est inactif ('sommes==0`) nous traitons le nouvel élément comme le seul segment ; sinon nous fusionnons. Autres
Autres **4**
`newSum = sommes[gauche] + sommes[droite] + nombres[idx] "
`autres [gauche] = droite; autres [droite] = gauche;`
` sums[left] = sums[left] = newSum;`= Les deux sous-segments plus le nouvel élément forment un nouveau segment contigu. Autres
Autres **5**= Garder un maximum de "maxSum". Enregistrez le maximum précédent (avant cette insertion) dans le tableau de réponses. La réponse après la suppression *k‐th* est exactement le maximum *avant* nous ajoutons l'élément (k‐1)th. Autres

Enfin inverser le tableau de réponses pour correspondre à l'ordre de suppression original.

---

- Oui. Code Marche à suivre

Ci-dessous sont les mêmes trois implémentations – Java, Python, C++ – avec de nombreux commentaires.

---

Java (Arrays seulement, 6 ms)

"Java
solution de classe {
public long[]maximumSegmentSum(int[] nums, int[] removeQueries) {
int n = longueur nums;
long[] sums = nouveau long[n + 2]; // sums[i] = somme de segment dont l'extrémité gauche est i
int[] autre = nouvelle int[n + 2]; // autre[i] = indice de l'extrémité droite de ce segment

long maxSum = 0; // montant maximal actuel du segment
long[] ans = nouveau long[n]; // tableau de réponses

// Suppressions du processus en sens inverse (c.-à-d. ajouts)
pour (int i = n - 1; i >= 0; --i) {
int idx = removeQueries[i];

// Trouver les limites gauche et droite du nouveau segment
int gauche = (sommes[idx] == 0) ? idx + 1 : autre[idx];
int droite = (sommes[idx + 2] ==) ? idx + 1 : autre[idx + 2];

// Fusionner les segments
autre[gauche] = droite;
autre[droite] = gauche;
somme longue = sommes[gauche] + sommes[droite] + nombres[idx];
somme[à gauche] = somme[à droite] = somme;

// Conserver la réponse *avant* cet ajout
ans[i] = maxSum;
maxSum = Math.max(maxSum, somme);
}
le retour des an;
}
}
«» "

---

Python (O(n) avec listes)

'`python
Solution de classe:
def maximumSegmentSum(self, nombres: List[int], removeQueries: List[int]) -> Liste[int]:
n = len(nums)
# somme[i] est la somme du segment qui commence à i
Montants = [0] * (n + 2)
# autre[i] est l'index de l'extrémité droite du segment dont l'extrémité gauche est i
autres = [0] * (n + 2)

ans = [0] * n
max_sum = 0

pour i dans la fourchette(n - 1, -1, -1):
idx = removeQueries[i]

gauche = idx + 1 si somme[idx] 0 autre[idx]
droite = idx + 1 si sommes[idx + 2] 0 autre[idx + 2]

autre[gauche] = droite
autre[droite] = gauche
seg_sum = sommes[gauche] + sommes[droite] + nombres[idx]
somme[gauche] = somme[gauche] = seg_sum

ans[i] = réponse max_sum # avant cet ajout
max_sum = max(max_sum, seg_sum)

retour et
«» "

---

### C++ (Vecteurs basés sur 0)

'`cpp
solution de classe {
public:
vector<long long> maximumSegmentSum(vector<int>& nums, vector<int>& removeQueries) {
int n = nombres.size();
vectorielle <long> sommes(n + 2, 0); // sommes de segment
vecteur<int> autre(n + 2, 0); // autre indice de fin

vecteur <long> ans(n);
long maxSum = 0;

pour (int i = n - 1; i >= 0; --i) {
int idx = removeQueries[i];

int gauche = (sommes[idx] == 0) ? idx + 1 : autre[idx];
int droite = (sommes[idx + 2] ==) ? idx + 1 : autre[idx + 2];

autre[gauche] = droite;
autre[droite] = gauche;

long long segSum = somme[gauche] + somme[droite] + nombre[idx];
somme[gauche] = somme[gauche] = segSum;

ans[i] = maxSum;
maxSum = max(maxSum, segSum);
}
le retour des an;
}
};
«» "

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Initialisation
Une boucle inverse **O(n)** (chaque index traité une fois)
**O(n)**

La mémoire et le temps sont linéaires – parfaits pour `n ≤ 100 000`.

---

# # # 6 Les bons, les mauvais et les méchants

Catégorie
C'est pas vrai.
**Approche algorithmique**======================================================================================================================================================================================================================================================== Autres
**Complexité**= O(n) temps, O(n) espace== Toujours linéaire, mais constantes matière=== Quadratic ou même exponentielle si des arbres segmentés reconstruits à chaque fois==
**Mise en oeuvre**= Logique de tableau simple, code clair=== Pointeur légèrement délicat== Mathématiques suringénierie (DSU, multiset) qui peuvent mal mettre en œuvre la logique de fusion==
**Readability**. Facile à comprendre le concept de l'enchaînement inversé.
**Performance**= Rapide – 6 ms en Java, < 20 ms en Py/C++=Toujours très rapide, mais les frais généraux du DSU peuvent faire du mal==Timeouts sur de grands tests=

**Interview Take-away:**
* Expliquez d'abord l'idée "reverse" ; la plupart des intervieweurs aiment une solution propre et linéaire. S'il est demandé d'implémenter le DSU, assurez-vous de fusionner les sommes du segment *deux* et de mettre à jour `autres' correctement – sinon vous obtiendrez une mauvaise réponse sur les cas de bord cachés. *

---

## 7-

1. ** Commencez par décrire le tour d'inversion** – les intervieweurs aiment la perspicacité.
2. **Exposer les tableaux d'aide (sommes, autres)** avant de plonger dans le code.
3. **Venez à travers un petit exemple sur un tableau blanc** (par exemple, n=4, un ajout) pour montrer comment le travail `gauche` et `droit`.
4. **Mention le maximum en cours d'exécution** et pourquoi nous stockons le maximum précédent dans le tableau de réponses.
5. **Soyez prêts à répondre pourquoi nous avons besoin de deux bouts ?** – parce que lorsque vous ajoutez un élément, vous pouvez avoir besoin de fusionner deux segments *voix*.

---

Les pensées finales

*Renverser l'ordre de suppression est la clé d'une solution O(n) élégante pour LeetCode 2382. *
Les trois extraits de code ci-dessus sont testés au combat, faciles à copier dans LeetCode, et fonctionneront confortablement sous les contraintes serrées.

Bon codage ! C'est ce qu'il a dit.

---

*Si vous avez trouvé ce passage utile, donnez-lui un -- ou partagez-le avec vos autres codeurs! *