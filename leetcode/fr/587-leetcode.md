---
titre: LeetCode 587. Érigez la clôture -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 587. La clôture – Trois – Way Solution & a SEO-Optimized Blog Post

> **TL;DR**
> *Mettre en oeuvre une coque convexe (Manotonic-Chain) qui maintient des points collinéaires sur la frontière. *
> *Nous fournissons le code Java, Python et C++, ainsi qu'un article de blog complet qui explique le bon, le mauvais et le laid de ce problème, emballé avec des crochets SEO amis des interviews. *

---

- Oui. 1. Récapitulation des problèmes (Code de bord 587)

> **Objectif** – Compte tenu d'un éventail de coordonnées de l'arbre, retourner *chaque* arbre qui se trouve sur le périmètre de la clôture de longueur minimale qui entoure tous les arbres.
> ** Règle spéciale** – Si la clôture est une ligne droite (tous les arbres collinéaires) retourner tous les arbres.

Contraintes:
- 1 ≤ "longueur des arbres" ≤ 3000
- 0 ≤ `xi, yi` ≤ 100
- Toutes les coordonnées sont uniques.

---

- Oui. 2. Idée de haut niveau

La clôture qui couvre tous les points avec le plus petit périmètre est la coque **convexe** du jeu de points.
La seule nuance est que *les points collinéaires qui reposent sur les bords de la coque doivent également être retournés*.
C'est une variation classique du problème de la coque convexe.

Nous utiliserons l'algorithme **Monotonic Chain (Andrew)** – O(N log N) time, O(N) space – car il est court, rapide et facile à écrire dans les trois langues.

---

- Oui. 3. Détails de l'algorithme

1. **Trier** tous les points lexicographiquement par x, puis par y.
2. **Construire la coque inférieure**:
* Marchez à travers les points triés.
* Alors que les deux derniers points de la coque avec le point actuel font un ** virage droit** (`cross <= 0` pour *keep* points collinéaires) – pop le dernier point.
* Poussez le point actuel.
3. **Construire la coque supérieure** de la même façon, mais marcher à travers les points triés à l'envers.
4. **Combine** les coques inférieures et supérieures (laisser tomber le dernier point de chacune pour éviter la duplication).
5. **Supprimer les duplicata** (surtout lorsque tous les points sont collinéaires – les deux coques contiennent le même ensemble) – utiliser un `HashSet` (Java), `set` de tuples (Python), ou `unordered_set` avec un hash personnalisé (C++).

**Produit brut**
Pour les points `A(x1,y1)`, `B(x2,y2)`, `C(x3,y3)`:
«» "
croix = (x2-x1)*(y3-y1) - (y2-y1)*(x3-x1)
«» "
* `> 0` → virage à gauche
* `< 0` → à droite
- Oui. 0` → collinéaire

---

- Oui. 4. Code

#### 4.1 Java (Java 17+)

"Java
Importation de java.util.*;

solution de classe publique {

// Produit croisé de AB et AC
longue croix privée(int[] A, int[] B, int[] C) {
Déclaration (long)(B[0] - A[0]) * (C[1] - A[1]) - Oui.
(long)(B[1] - A[1]) * (C[0] - A[0]);
}

Int[]][][][][][][][][][][][][][][][]][][][][][]][][][][][]][][][][][]][][][]][][][][][][][][][][]][][][][][]][][]][][][][][]][][][]][][][]][][][]][][][][][][][][][][][][][][][][][][]][][][]][][][]][]][][][]][][][][][]][][][][][][]][][][][][]][][][][][][][][]
i (arbres) 0) retourner une nouvelle int[0][0];
Tableaux.sort(arbres, (p, q) -> {
si (p[0] != q[0]) retourne Integer.compare(p[0], q[0]);
retour Integer.compare(p[1], q[1]);
});

Liste<int[]> plus basse = nouvelle liste de distribution<>();
pour (int[] pt : arbres) {
pendant que (bas.size() >= 2 &&
cross(lower.get(lower.size() - 2),
< 0) {
d'une taille inférieure à 1;
}
b) inférieur.add(pt);
}

Liste<int[]> supérieure = nouvelle liste de distribution<>();
pour (int i = arbres.longueur - 1; i >= 0; --i) {
int[] pt = arbres[i];
pendant que (upper.size() >= 2 &&
cross(upper.get(upper.size() - 2),
upper.get(upper.size() - 1), pt) < 0) {
supérieur.supprimer(upper.size() - 1);
}
supérieur.add(pt);
}

// Fusionner les valeurs inférieures et supérieures, éviter les doubles paramètres
Set<List<Integer>> set = nouveau HashSet<>();
pour (int[] p : plus bas) set.add(Arrays.asList(p[0], p[1]);
pour (int[] p : supérieur) set.add(Arrays.asList(p[0], p[1]);

int[]] res = nouveau int[set.size()][2];
i = 0;
pour (Liste <entier> lst : set) {
res[i][0] = lst.get(0);
res[i][1] = lst.get(1);
i++;
}
retour rés;
}
}
«» "

> **Pourquoi utiliser `Liste<entier>` dans l'ensemble? **
> Les tableaux primaires ne peuvent pas être hashés correctement en Java; l'emballage dans une "Liste" nous donne un `egals`/`hashCode` stable.

---

4.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
extérieur Arbres(même, arbres: Liste[Liste[int]]) -> Liste[Liste[int]]:
si non des arbres:
retour []

trees.sort() # lexicographie: x puis y

def cross(o, a, b):
retour (a[0]-o[0]) * (b[1]-o[1]) - (a[1]-o[1]) * (b[0]-o[0])

inférieur = []
pour p dans les arbres:
pendant que lent(inférieur) >= 2 et croisé(inférieur[-2), inférieur[-1], p) < 0:
moins.pop()
annexe(p) inférieure

supérieur = []
pour p en marche arrière:
pendant que len(upper) >= 2 et croisé(upper[-2], supérieur[-1], p) < 0:
supérieur.pop()
supérieur.appendice(p)

# Combiner et défaire
coque = ensemble(tuple(pt) pour pt dans la partie inférieure[:-1] + supérieure[:-1])
retour [liste(pt) pour pt dans la coque]
«» "

> **Note** – Nous laissons tomber le dernier point de chaque demi-coque pour éviter la duplication des paramètres ('inférieur[-1] == supérieur[-1]').

---

### 4.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue croix longue (tableau de const<int,2>& A,
tableau de const<int,2>& B,
tableau de const<int,2>&C) {
retour 1LL*(B[0]-A[0]*(C[1]-A[1]) - Oui.
1LL*(B[1]-A[1])*(C[0]-A[0]);
}

vectorielle<vector<int>>externeTérées(vecteur<vector<int>&arbres) {
si (trees.vide()) retourne {};

tri(arbres.degin(), arbres.end(),
[](vecteur Const<int>& p, vecteur Const<int>& q){
si (p[0] != q[0]) retourne p[0] < q[0];
retour p[1] < q[1];
});

vecteur<array<int,2>> inférieur, supérieur;
pour (auto &p : arbres) {
tableau <int,2> pt{p[0], p[1]};
pendant que (bas.size() >= 2 &&
cross(lower[lower.size()-2), lower.back(), pt) < 0)
plus bas.pop_back();
lower.push_back(pt);
}

pour (auto it = arbres.rbegin(); il != arbres.rend(); ++it) {
tableau <int,2> pt{(*it)[0], (*it)[1]};
pendant que (upper.size() >= 2 &&
cross(upper[upper.size()-2%), upper.back(), pt) < 0)
upper.pop_back();
upper.push_back(pt);
}

// Supprimer le dernier élément de chaque pour éviter les duplicatas
plus bas.pop_back();
upper.pop_back();

_set non ordonné<long long> vu;
vecteur<vecteur<int>> rés;

ajouter automatiquement = [&](tableau Const<int,2>& pt){
longue clé longue = 1LL*pt[0]*101 + pt[1]; // 0<=x,y<=100 -> unique
si (see.insert(key).second) {
le nom et l'adresse de l'utilisateur;
}
};

pour (auto &pt : plus bas) add(pt);
pour (auto &pt : upper) add(pt);

retour rés;
}
};
«» "

> ** Astuce clé** – Comprimez chaque point en une seule touche longue (x*101 + y") parce que `x` et `y` sont ≤ 100. Cela nous permet d'utiliser `unordered_set<long>` pour la déduplication O(1).

---

- Oui. 5. Billet de blog – Le bon, le mauvais, et le mauvais de LeetCode 587

Titre
> **Erect the Fence (LeetCode 587) – Le guide complet (Java / Python / C++)**
> *Pourquoi la coque convexe est un incontournable pour les entrevues sur la structure des données, plus un tutoriel étape par étape. *

*(Ajouter une image en vedette d'une coque convexe en 2-D, le logo LeetCode et les extraits de code surlignés.) *

---

- Oui. 1. Présentation

> J'interviewe pour un poste d'ingénieur logiciel, mais je ne peux pas passer les questions de géométrie. (en milliers de dollars)
> Cette phrase est aussi courante qu'un crayon cassé dans un panneau d'embauche.
> Le problème Erect the Fence est un billet d'or* – il teste deux concepts simultanément :
> - **Trier** (pour linéariser les données)
> - **Invariants géométriques** (produit croisé, orientation).

Nous allons vous montrer la solution ** la plus rapide, la plus propre et la plus conviviale** en trois langues.

---

- Oui. 2. Pourquoi Convex Hull? (Les bons)

- **Concept universel** – Apparaît dans le graphisme informatique, la robotique, le SIG, même le jeu AI.
- **Linear-time ou quasi-linéaire** – L'algorithme Andrews fonctionne dans le log N O(N), battant le contrôle du périmètre de la force brute O(N2).
- **Couverture d'essai Rich** – Poignée tous les cas d'angle (tous les points collinéaires, un seul point, convexe vs concave arrangements).

> **Hook d'interview** – Décrivez une situation où vous deviez optimiser le chemin d'un robot vide qui devait couvrir toutes les pièces d'une maison. (en milliers de dollars)
> Le recruteur s'attend à ce que vous mentionniez presque immédiatement la coque convexe.

---

- Oui. 3. Déroulement de la mise en oeuvre (le bien)

1. **Trier les points** – La première étape O(N log N).
2. **Utilisez une pile (ou un vecteur)** pour maintenir la coque pendant que vous itérez.
3. **Test du produit brut** – Une seule ligne de code détermine si un point doit rester ou être enlevé.
4. ** Gardez des points collinéaires** – Il suffit de changer `cross < 0` en `cross <= 0`.
5. **Dupliquer** – En Java, utilisez une `Set<List<Integer>>`; en Python, `set(tuple(pt))`; en C++, une touche entière hashée.

*Pourquoi cet algorithme bat-il le classique Graham Scan? *
- Moins de code, moins de bogues, plus facile à expliquer verbalement.

---

- Oui. 4. Pièges communs (les mauvais)

Pourquoi c'est mauvais
- C'est quoi ?
En utilisant `< 0` pour l'état pop. Utiliser `<= 0` seulement si vous * devez* les conserver, sinon `>= 0 '.
Autres Oubliant de défaire quand tous les points sont collinéaires. Autres
En utilisant le trop-plein entier dans le produit croisé. Autres
En mélangeant la logique de virage gauche/droite, on vole l'orientation de la coque, ce qui entraîne une forme incorrecte. Se tenir à la convention: `cross > 0` = gauche, `< 0` = droite. Autres

**Astuce** – Écrire un petit aide `cross` avec des commentaires clairs; un seul typo brisera toute la solution.

---

- Oui. 5. Le "Ugly" – Quand les intervieweurs vous poussent plus loin

1. **Tous les Points Collinéaire** – Votre algorithme doit gérer ce cas bord gracieusement.
*Solution:* Après avoir construit les deux coques, convertir en un ensemble; pas besoin de logique séparée.

2. **Grande plage d'entrée** – Certains intervieweurs demandent : Et si `xi, yi` pouvait être jusqu'à 109 ? (en milliers de dollars)
*Solution:* Utilisez `long long` pour le produit croisé, évitez le débordement entier et changez la clé de duplication en une paire de hachage.

3. ** Contraintes de mémoire** – Lorsque la mémoire est limitée, vous pouvez construire la coque en place et réutiliser le tableau d'entrée.
*Python/C++:* Ajoute les indices de coque à une nouvelle liste, puis map back.
*Java:* Utilisez un résultat `int[]` et remplissez-le pendant l' itération.

4. ** Limites de temps** – L'algorithme O(N log N) passe facilement avec N = 3000.
Si vous avez besoin d'optimiser davantage, vous pouvez pré- trier par entier des valeurs et utiliser le tri de comptage (O(N)) parce que les coordonnées sont petites.

---

- Oui. 6. Comment expliquer Sur un tableau blanc

1. **Draw** la liste triée des points horizontalement.
2. **Show** la coque inférieure en cours de construction – chaque pop représente un "corner" en cours de lissage.
3. **Mirreur** pour la coque supérieure.
4. **Combine** – Visualisez la version de la version inférieure.
5. **Remarquez** pourquoi les points collinéaires sur les bords restent – insistez sur l'état du produit croisé.

* Pratique*: Essayez d'expliquer cela en 3 minutes – vous trouverez que vous pouvez le faire naturellement après avoir écrit le code plusieurs fois.

---

- Oui. 7. Feuille de chaleur à emporter

Langue Trier Produit Cross
- C'est quoi ?
Java "Arrays.sort(arbres, cmp)"" "ArrayList<int[]>" Autres
Def cross(o,a,b)"""list" pour les moitiés" "set(tuple)" Autres
C++="sort(debut,end,cmp)="long long cross(array)=" "vector<array<int,2>>"""unordered_set<long>" (clé = x*101+y)"

> **Key:** Utilisez la formule *même* de produit croisé dans toutes les langues. Conservez la condition `cross < 0` pour le virage à droite et gardez les points collinéaires.

---

- Oui. 8. Mots définitifs

> Des questions de géométrie comme Erect the Fence sont *pas* à propos d'être un mathématicien; ils sont à propos de prouver que vous pouvez gérer **ensembles de données en deux dimensions**, appliquer un algorithme robuste, et écrire un code propre, sans bug.
> Maîtrisez la coque convexe une fois et vous gagnerez non seulement ce problème, mais une *classe entière* de questions d'entrevue.

*Ajouter un "Vous voulez plus? Consultez mon répertoire complet de solutions d'entretien de structure de données et un formulaire de courriel ou de contact. *

---

- Oui. 9. Méta-données SEO (pour les robots recruteurs)

Valeur du champ
C'est pas vrai.
Mots-clés LeetCode 587, Érect la solution de Fence, Entretien de la coque de Convexe, Entretien de la coque de Convexe, Entretien de la coque de Convexe de Java, Problème de géométrie de Python, Problème de géométrie de Convexe de C++, Questions d'entretien de structure de données, Préparation de l'entretien d'algorithme
Description du produit Découvrez la solution Java/Python/C++ la plus rapide pour LeetCode 587 – Erect the Fence. Apprenez les fondamentaux de la coque convexe et obtenez un passage complet avec le code. Autres
Titre Éliminer le code de clôture 587 – Terminé Guide Java/Python/C++
OG Image OG `https://exemple.com/assets/convex-hull.png` Autres
Carte Twitter Autres

---

- Oui. 6. Comment utiliser ce blogue dans votre portefeuille

- **Pin it on LinkedIn** avec le titre "Solved Erect the Fence en 4 langues – Convex Hull 101.
- **Embed** les extraits de code sur votre GitHub README.
- **Créez une courte vidéo** (3 minutes) de vous résolvant le problème en direct, puis téléchargez sur YouTube avec le même titre – l'algorithme de YouTubes aime comment résoudre les vidéos.
- **Ajoutez un quiz** à la fin de l'article (=Given points X, Y, Z, qui est sur la coque?=) – encourage l'engagement.

---

- Oui. 7. Pensée de clôture

> La géométrie peut être intimidante, mais les motifs sous-jacents sont simples.
> En maîtrisant l'algorithme de la chaîne monotonique une fois, vous pouvez résoudre avec confiance Erectez la Fence, ses variations, et une multitude d'autres énigmes géométriques d'interview.

Bon codage, et que vos clôtures soient toujours *fermes* et *efficaces*! C'est ce qu'il a dit.

---

** Fin de poste**