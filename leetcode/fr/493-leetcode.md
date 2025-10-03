---
titre: LeetCode 493. Paires inversées -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Paires inversées (Code Leet 493) – Guide du code et du blog

Vous trouverez ci-dessous des implémentations prêtes à travailler** dans **Java, Python et C++** pour le problème *Reverse Pairs*.
Après le code, vous lisez un article de style *blog* qui explique le problème, les aspects bons, mauvais et laids des solutions typiques, et pourquoi ce problème est un excellent point d'interview pour les rôles d'ingénierie logicielle.

> **SEO Mots-clés**: *LeetCode Pairs inversés, Solution de Pairs inversés, Fusionner Tri, diviser-et-conquer, question d'entrevue, Java, Python, C++ interview de codage, conseils d'entrevue d'emploi, interview d'algorithme*

---

- Oui. 1. Récapitulation des problèmes (Code de bord 493)

> **Pairs inversés* *
> *Avec un tableau entier `nums`, retournez le nombre de paires inversées dans le tableau. *
> Une paire inverse est une paire `(i, j)` où `0 ≤ i < j < nums.length` et `nums[i] > 2 * nums[j]`.

Exemple Entrée Sortie Explication
C'est pas vrai.
[1,3,2,3,1] Autres
"[2,4,3,5,1] "" "3" "(1,4) ", "(2,4) ", "(3,4) " Autres

**Contrôles* *

* `1 ≤ longueur nominale ≤ 5 × 104`
* `-231 ≤ nombres[i] ≤ 231 − 1`

---

- Oui. 2. Pourquoi l'approche naïve O(n2) fait défaut

La double boucle de force brute vérifie chaque paire:

Texte
pour i dans 0 .. n-1:
pour j en i+1 .. n-1:
si nombres[i] > 2 * nombres[j]:
nombre++
«» "

* **Temps**: < < O(n2) > > – inacceptable pour < < n = 50 000 > > (2,5 milliards d ' opérations).
* **Espace**: "O(1)" – Très bien, mais la vitesse tue.

---

- Oui. 3. Le bon – Diviser & Conquer avec Fusion Tri

La solution optimale utilise la même astuce de comptage qui sous-tend *compte d'inversion*.
Lors de l'exécution d'une fusion standard, nous ** comptabilisons** combien d'éléments de la moitié droite satisfont à l'état de paire inverse pour chaque élément de la moitié gauche.

3.1 Esquisse d'algorithme

«» "
fonction fusion SortAndCount(nums, gauche, droite):
si gauche >= droite: retourner 0

milieu = (gauche + droite) / 2
nombre = fusionSortAndCount(nombres, gauche, milieu)
+ fusionSortAndCount(nums, mi+1, droite)

// Nombre de paires inversées traversant les moitiés
j = milieu + 1
pour i de gauche à mi:
tandis que j <= droite et nombres[i] > 2 * nombres[j]:
j++
nombre += j - (milieu + 1)

// Fusionner les deux moitiés triées
fusion(nombres, gauche, milieu, droite)
Nombre de retours
«» "

* **Point de vue principal** :
*Alors que les deux moitiés sont triées, nous pouvons les parcourir linéairement pour compter toutes les paires croisées en O(n). *

3.2 Pourquoi ça marche

* Chaque appel récursif garantit que son segment est trié après le retour.
* La marche à deux points (`i` pour la gauche, `j` pour la droite) compte toutes les paires `(i, j)` avec `i` dans la moitié gauche et `j` dans la moitié droite.
* Fusionner l'étape maintient l'ordre trié pour le niveau suivant.

3.3 Complexité

* **Time**: `O(n log n)` – chaque niveau de récursion traite tous les éléments `n` une fois.
* **Espace**: `O(n)` – tableau auxiliaire pour la fusion (peut être fait en place avec des astuces supplémentaires mais `O(n)` est plus simple).

---

- Oui. 4. Les pièges communs

Pourquoi ça arrive ?
- Oui.
**Débordement entier** lors du calcul de "2 * nombres[j]" peut être aussi grande que `231−1`. Multiplier par 2 débordements int. 32-bit. Autres
**L'utilisation de `int` pour le compte**=Le nombre maximum peut être `n(n-1)/2`, jusqu'à ~1,25 milliards pour `n=50k`.=L'utilisation de `long` pour le compteur en Java/C++; `int` en Python est débordée. Autres
Autres **Les limites de fusion de Wrong**=Les erreurs hors-par-un (`mid` vs `mid-1`) brisent l'invariant trié. Testez soigneusement avec des tests unitaires; utilisez un squelette standard de fusion. Autres
**Re-alterner les tableaux à chaque fusion** Autres

---

- Oui. 5. Les approches alternatives

Démarche
C'est quoi ?
**Binary Indexed Tree (Fenwick)**=Poigne les mises à jour dynamiques, utiles dans les variations. Nécessite une compression de coordonnées, O((n+logV) log n). Autres
**Segment Tree** Plus de mémoire, plus de facteur constant. Autres
**Divide-et-Conquer (même que Merge Sort)** La complexité de la mise en œuvre pour les débutants. Autres

Pour ce problème précis, *Merge Sort* reste la solution la plus simple, la plus propre et la plus conviviale pour les interviews.

---

- Oui. 6. Mise en œuvre – 3 langues

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int inversePairs(int[] nums) {
si (nombres) null (longueur) num) 0) retour 0;
int[] temp = nouveau int[nums.longueur];
retour (int) fusion TriAndCount(nums, temp, 0, nombres.longueur - 1);
}

// Les retours comptent aussi longtemps pour éviter les débordements
fusion privée longueSortAndCount(int[] nombres, int[] temps,
int gauche, int droite) {
si (gauche >= droite) retourner 0;
int milieu = gauche + (droite - gauche) / 2;
longue numération = fusionSortAndCount(nombres, temp, gauche, milieu)
+ fusionSortAndCount(nombres, temp, milieu + 1, droite);

// Nombre de paires croisées
int j = milieu + 1;
pour (int i = gauche; i <= milieu; i++) {
pendant que (j <= droite && (long) nombres[i] > 2L * nombres[j]) {
j++;
}
nombre += j - (milieu + 1);
}

// Fusionner l'étape
int i = gauche, k = gauche;
alors que (i <= mi && j <= droite) {
si (nums[i] <= nums[j]) temp[k++] = nombres[i++];
autres temp[k++] = nombres[j++];
}
pendant que (i <= milieu) temp[k++] = nombres[i++];
pendant que (j <= droite) temp[k++] = nombres[j++];
Système.arraycopy(temp, gauche, nombres, gauche, droite - gauche + 1);
le nombre de retours;
}
}
«» "

6.2 Python

'`python
def inversePairs(nums):
si non des nombres:
retour 0

def merge_sort_and_count(arr, gauche, droite) :
si gauche >= à droite :
retour 0
milieu = (gauche + droite) // 2
count = fusion_sort_and_count(arr, gauche, mi) + \
fusionner_sort_and_count(arr, milieu + 1, droite)

Nombre des paires inversées
j = milieu + 1
pour i dans la plage (gauche, milieu + 1):
alors que j <= droite et arr[i] > 2 * arr[j]:
j += 1
nombre += j - (milieu + 1)

# Fusionner les moitiés triées
fusionné = []
i, j = gauche, milieu + 1
alors que i <= mi et j <= droite:
fusionne.append(arr[i] si arr[i] <= arr[j] autre arr[j])
si arr[i] <= arr[j]:
i += 1
Sinon:
j += 1
alors que i <= mi:
l'annexe; i += 1
alors que j <= droite:
fusionned.append(arr[j]); j += 1
arr[left:right+1] = fusionné
Nombre de retours

retourner merge_sort_and_count(nums, 0, len(nums) - 1)
«» "

*### 6.3 C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
int inversePairs(std::vector<int>& nums) {
si (nums.vide()) retourne 0;
point::vecteur<int> temp(nums.size());
longue longue res = fusionSortAndCount(nums, temp, 0, nums.size() - 1);
return static_cast<int>(res); // count correspond à 32 bits pour ce problème
}

particulier:
longue longue fusionSortAndCount(std::vector<int>& nums,
std::vector<int>& temp,
int gauche, int droite) {
si (gauche >= droite) retourner 0;
int milieu = gauche + (droite - gauche) / 2;
long compte long = fusionSortAndCount(nombres, temp, gauche, milieu) +
fusionnerSortAndCount(nombres, temp, milieu + 1, droite);

// Nombre de paires croisées
int j = milieu + 1;
pour (int i = gauche; i <= milieu; ++i) {
pendant que (j <= droite && static_cast<long long>(nums[i]) > 2LL * nums[j]) {
++j;
}
nombre += j - (milieu + 1);
}

// Fusionner
int i = gauche, k = gauche;
alors que (i <= mi && j <= droite) {
si (nums[i] <= nums[j]) temp[k++] = nombres[i++];
autres temp[k++] = nombres[j++];
}
pendant que (i <= milieu) temp[k++] = nombres[i++];
pendant que (j <= droite) temp[k++] = nombres[j++];
md::copie(temp.begin() + gauche, temp.begin() + droite + 1,
nums.degin() + gauche);
le nombre de retours;
}
};
«» "

> **Note sur C++**
> *Le type `long` est obligatoire pour `2 * nums[j]`.
> La solution finale est sûre car la réponse est toujours ≤ 1 250 000 000 pour `n ≤ 50 000`. *

---

- Oui. 7. Article sur le blog – Pairs inversés

> **Titre**: Pairs inversés (LeetCode 493) – Le défi ultime du codage de l'entrevue
> **Auteur**: *Votre amoureux de l'algorithme

---

7.1 Introduction

Les paires inversées semblent trompeusement simples : *=Combien de fois un élément est plus de deux fois un autre qui apparaît plus tard dans le tableau.
En réalité, c'est un exemple de manuel d'un algorithme **diviser-conquer** qui teste la capacité d'un candidat à

* Raison des sous-cours triés
* Utilisez une traversée à deux points
* Prévenir les débordements entiers
* Écrire un code propre et réutilisable

Autres **Pourquoi les recruteurs l'adorent** – Il couvre **la pensée de complexité du temps**, **la manipulation dearray** et **la manipulation de cas de référence** – toutes les choses qu'ils recherchent dans un ingénieur logiciel.

---

#### 7.2 Énoncé du problème (réécrit)

> **Don** une liste d'entiers signés 32 bits,
> **Trouver** le nombre de paires d'index `(i, j)` de telle sorte que `i < j` et `nums[i] > 2 × nums[j]`.

> **Constraints**
> *Longueur du tableau ≤ 50 000*
> *Les numéros sont dans la gamme complète signée 32 bits. *

---

Le bien

**Le comptage de la matrice** est la solution canonique:

1. **Trier le tableau par récursion (diviser la plage en deux).
2. **Tout en fusionnant**, marcher une fois à travers les moitiés gauche et droite et compter combien de paires transversales satisfont à l'état.
3. **Retour** la somme des chiffres de tous les niveaux récursifs.

> Pourquoi c'est bon
> *Runs in O(n log n)*, qui est le meilleur que vous pouvez faire pour un tableau statique.
> *La mise en œuvre est courte (de 70 lignes dans la plupart des langues) et facile à raisonner. *

---

Le mal

Erreurs courantes qui transforment la solution élégante en une implémentation buggy:

* **Excédent**: "2 * nombres[j]" doit être évalué comme 64 bits.
* **Données erronées pour le compteur**: La réponse peut être ~1,25 milliards.
* ** Erreurs limites dans l'étape de fusion** : Les bugs hors-par-un détruisent le triage.
* **Distribution répétée de tampons temporaires**: Ça fait perdre du temps.

---

#### 7.5 Le Ugly - Quand vous devez penser en dehors de la boîte

1. **Binary Indexed Tree (Fenwick)** – Coordonnée – compresser les valeurs, puis itérer de droite à gauche en insérant dans le BIT et en demandant combien de nombres antérieurs sont > 2×current.
2. **Segment Tree** – Similaire au BIT mais plus flexible pour les requêtes de gamme.
3. **Divisez et conquérez (comme Merge‐Sort)** – Légèrement plus propre mais plus verbeux.

Tous atteignent *O(n log n)* ou *O(n log n + n log V)* le temps, mais **merge-sort** est toujours le plus *interview-ready* car il suffit de se souvenir du motif classique *inversion-count*.

---

7.6 Pourquoi ce problème est un grand sujet d'entrevue

Objectif de l'entrevue
- C'est quoi ?
**La pensée algorithmique**Le candidat peut repérer le tour de comptage croisé. Autres
**Coding Skills**= Aptitude à écrire une routine récursive correcte et une fusion en place. Autres
Autres **Connaissance des cas** Autres
**Maîtrise de la langue** Autres
**Temps/Espace Échanges**= Discussion sur le tableau temporaire `O(n)` par rapport aux fusions réellement en place. Autres

---

###7.7 Rapide- Tests de contrôle unitaire (pour les trois langues)

Texte
[1, 3, 2, 3, 1] → 2
[2, 4, 3, 5, 1] → 3
[0, 0, 0] → 0
[2147483647, -2147483648] → 1 (contrôle de la manipulation des débordements)
«» "

> **Conseil pour les intervieweurs**: Demandez au candidat de parcourir la partie *comptage de la paire* avec un petit tableau tiré à la main; il expose son modèle mental.

---

7.8 Conclusion et emploi Entretien à emporter

* **Pairs inversés** est un classique *O(n log n)* problème de partage-et-conquer qui mélange le tri de tableau avec une torsion de comptage.
* La mise en oeuvre démontre correctement la maîtrise de la pensée algorithmique, le traitement minutieux des types de données et le style de code propre – exactement ce que les gestionnaires d'embauche recherchent.
* Maîtrisez ce modèle, écrivez les extraits de trois langues ci-dessus, et vous serez prêt à accepter l'étape de l'entrevue de codage de votre prochaine recherche d'emploi en génie logiciel.

---

> **Note pro‐recruteur** – J'ai remarqué que vous avez résolu *Pairs inversés* efficacement. →
> *Réponse*: J'ai utilisé une approche de comptage basée sur la fusion, évitant soigneusement les débordements en utilisant des entiers 64 bits. Il fonctionne dans le temps `O(n log n)`, qui est essentiel pour les grandes entrées. (en milliers de dollars)
> Cela indique au recruteur que vous comprenez à la fois l'optimalité algorithmique et les cas pratiques.

Bon codage, et bonne chance pour votre prochaine interview!