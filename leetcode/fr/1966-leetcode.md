---
titre: LeetCode 1966. Nombres binaires à rechercher dans un tableau non trié -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
En 1966. Nombres de recherche binaires dans un tableau non trié
### De la bonne à la mauvaise : une plongée profonde dans une entrevue Solution prête

> **Mots clés**: LeetCode 1966, nombres de recherche binaire, tableau non trié, préfixe-suffix, pile monotonique, préparation d'entrevue, conception d'algorithme, complexité temporelle, complexité spatiale, entretien d'emploi en génie logiciel.

---

- Oui. 1. Pourquoi ce problème importe

- **Analogie du monde réel**: Imaginez-vous chasser une clé cachée dans un tiroir en désordre. Vous saisissez aléatoirement un élément, et selon qu'il est gauche ou droite de la clé, vous jetez tout un côté du tiroir.
- **Aimant d'interview**: LeetCodeS__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
- **Career Boost** : Résoudre le problème montre avec élégance votre capacité à raisonner sur *les pires garanties* – exactement ce que les gestionnaires d'embauche aiment voir.

---

- Oui. 2. Déclaration de problème (version courte)

Compte tenu d'un tableau entier **unique** "nums", trouvez combien d'éléments sont **garantis** à trouver quelle que soit la façon dont le pivot est choisi au cours de la procédure de recherche aléatoire décrite ci-dessous.

**Procédure**:
1. Choisissez un pivot au hasard.
2. Si elle équivaut à la cible → succès.
3. Si pivot < cible → supprimer pivot et tout à sa gauche.
4. Si pivot > cible → supprimer pivot et tout à sa droite.
5. Répétez jusqu'à ce que le tableau soit vide → échec.

- **Objectif** : Compter les éléments qui *ne peuvent pas* être éliminés par un choix de pivot.

---

- Oui. 3. Intuition: Quand une cible se perd-elle?

Une cible `x` obtient *supprimée* seulement si un pivot est:

Position du pivot Valeur du pivot Effet sur `x` Autres
- C'est quoi ?
**Left of `x`**=Plus grand que `x`=Enlever `x` et tout ce qui reste du pivot. Autres
**Le droit de `x`**= Moins de `x`= Enlève `x` et tout le droit du pivot. Autres

Étant donné que *toute* élément peut devenir pivot, **pour `x` être garanti trouvé** aucune des situations ci-dessus ne peut jamais se produire.

Cela signifie :

1. **Tous les éléments à gauche de `x` sont inférieurs ou égaux à `x`**.
2. **Tous les éléments du droit de "x" sont supérieurs ou égaux à "x".**

Parce que tous les nombres sont uniques, le cas d'égalité n'apparaît jamais ; nous exigeons simplement une inégalité stricte.

---

### 4. La solution (O(n) temps, O(n) espace)

1. **Préfixe Max** – `leftMax[i]`: valeur maximale parmi les «nums[0...i]».
2. **Suffixe Min** – «rightMin[i]»: valeur minimale parmi les «nums[i...n-1]».

Un élément `nums[i]` est **safe** iff
"leftMax[i] == nums[i]" ** et** Il n'y a pas de quoi.
Parce que si le préfixe max est l'élément lui-même, chaque élément gauche est plus petit.
De même, si le suffixe min est l'élément lui-même, chaque élément droit est plus grand.

"Java
solution de classe {
public int binaireSearchableNumbers(int[] nums) {
int n = longueur nums;
si (n) 1) retour 1;

int[] leftMax = nouveau int[n];
Int curMax = entier.MIN_VALUE;
pour (int i = 0; i < n; i++) {
curMax = Math.max(curMax, nombres[i]);
gaucheMax[i] = curMax;
}

int[] rightMin = nouveau int[n];
Int curMin = Entier. MAX_VALEUR;
pour (int i = n - 1; i >= 0; i--) {
curMin = Math.min(curMin, nombres[i]);
droite Min[i] = curMin;
}

nombre int = 0;
pour (int i = 0; i < n; i++) {
si (leftMax[i] == nombres[i] && rightMin[i] == nombres[i]) count++;
}
le nombre de retours;
}
}
«» "

**Python**

'`python
Solution de classe:
def binaireSearchableNumbers(self, nombres: List[int]) -> Int:
n = len(nums)
si n] 1: retour 1

gauche_max = [0] * n
cur = flotteur('-inf')
pour i, val dans l'énumération(nombres):
cur = max(cur, val)
gauche_max[i] = cur

droite_min = [0] * n
cur = flotteur('inf')
pour i dans la plage(n-1, -1, -1):
cur = min(cur, nombres[i])
right_min[i] = cur

retour sum(1 pour i dans range(n) si left_max[i]==nums[i] et le right_min[i]==nums[i])
«» "

**C++**

'`cpp
solution de classe {
public:
int binaireSearchableNumbers(vector<int>& nums) {
int n = nombres.size();
si (n) 1) retour 1;
vecteur<int> gaucheMax(n), droiteMin(n);
Int curMax = INT_MIN;
pour (int i = 0; i < n; ++i) {
curMax = max(curMax, nombres[i]);
gaucheMax[i] = curMax;
}
Int curMin = INT_MAX;
pour (int i = n-1; i >= 0; --i) {
curMin = min(curMin, nombres[i]);
droite Min[i] = curMin;
}
cnt = 0;
pour (int i = 0; i < n; ++i)
si (leftMax[i] == nombres[i] && droiteMin[i]== nombres[i]) ++cnt;
retour cnt;
}
};
«» "

---

- Oui. 5. La Variante de l'O(n) temps, O(1) espace supplémentaire

Au lieu de stocker des tableaux préfixes/suffix, nous pouvons traverser une fois et maintenir *deux* propriétés monotoniques :

- Oui. En scannant de gauche à droite, suivre le maximum **current**.
- Oui. En scannant de droite à gauche, suivre le minimum ** actuel**.

Aucun tableau auxiliaire n'est nécessaire — seulement les deux valeurs d'exécution. Cela donne **O(1) espace** mais la logique reste la même. Le code ci-dessus capture déjà cela, de sorte que les tableaux préfixe-suffix peuvent être omis si l'espace est serré.

---

- Oui. 6. Cas de bord et essais

Autres Test d'entrée d'entrée d'entrée d'entrée d'entrée d'entrée d'entrée
- C'est quoi ?
Un seul élément, toujours trouvé. Autres
"[-1,52] "" "1"" "1"" "1"" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1" "1"" "1" "1" "1" "1"" "1"" "1"" "1"" "1" """" "1" "1" """" "1" "1" """ "1" """" "1" "" """"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" Autres
Seulement les plus petits ('1') restent en sécurité. Autres
[4] `[1,2,3,4,5]`= `5`= Trié ascendant → tous sont sûrs. Autres
= 5=5 `[5,4,3,2,1] `=5`= Trié en descendant → tous sont sûrs (mirrored). Autres
Les éléments `10`, `20`, `25` sont sûrs. Autres

Toujours tester avec:

- Des séquences qui augmentent et diminuent strictement (les pires garanties).
- Permutations aléatoires pour confirmer la logique.
- De grands tableaux (éléments `10^5`) pour valider les contraintes de temps.

---

- Oui. 7. Suivi: Et si les duplicatas étaient autorisés?

Avec des duplicatas, les inégalités *strict* se décomposent. L'algorithme devrait considérer le **rank** d'un élément, pas seulement sa valeur. Une approche :

1. **Comprimez le tableau dans une liste de (valeur, index le plus à gauche, index le plus à droite). **
2. Pour chaque groupe, assurez-vous qu'aucun élément de son groupe de gauche* n'est plus grand que la valeur du groupe ** et** aucun élément de son groupe de droite n'est plus petit.
3. Compter le nombre de valeurs uniques qui satisfont à la condition.

Une façon plus efficace est de garder un ensemble *trié* de valeurs vues tout en scannant et en vérifiant les limites en conséquence. Cela augmente légèrement la complexité mais reste linéaire si vous utilisez un arbre de statistiques d'ordre (par exemple, `TreeSet` en Java ou `bisect` en Python).

---

- Oui. 8. Une évaluation rapide

Aspect du bien
- C'est quoi ?
**Clarté conceptuelle**= Simple préfixe/suffixe raisonnement== Nécessite une manipulation soigneuse des indices== La logique d'élimination peut conduire à des bogues hors-par-un
Autres **Complexité temporelle** Aucun écueil significatif
Autres **Complexité de l'espace**= O(n) (peut se réduire à O(1))== Des tableaux supplémentaires peuvent être surtubés== Aucune=
Autres **Edge-Case Handling** , Fonctionne pour toutes les valeurs uniques. 1'. Oublier que `int` min/max peut déborder
**Évoluabilité**=Poignées 105 éléments confortablement Autres

**Bottom Line**: La solution préfixe-suffixe est *bonne* – propre, simple et conviviale. Éviter les réseaux auxiliaires (pile monotonique) est *bien* mais inutile sauf si la mémoire est serrée. La seule partie *ugly* est de vous assurer d'interpréter correctement la logique de gauche/droite ; un glissement là va s'enfoncer dans de mauvaises réponses.

---

- Oui. 9. Conseils d'entrevue

1. **Énoncer clairement le problème** – Résumer la règle de l'éloignement.
2. **Exposer la sécurité** – Souligner qu'une cible est sûre si elle est le maximum de son préfixe gauche *et* le minimum de son suffixe droit.
3. **Walk Through an Example** – Choisissez un petit tableau et montrez visuellement les tableaux préfixe/suffixe.
4. **Complexité** – Mention O(n) temps et espace O(n), plus la variante optionnelle O(1) espace.
5. **Cas d'Edge** – Notez rapidement le cas d'élément unique et l'hypothèse de valeur unique.
6. **Suivi** – Décrivez brièvement comment les duplications changeraient la logique.

---

- Oui. 10. Les pensées finales

- **Pourquoi c'est Interview-Ready** : La solution est un scan *linéaire* avec une condition mathématique claire.
- **Pourquoi c'est efficace**: Poigne la contrainte maximale de LeetCode (éléments `105`) confortablement.
- **Pourquoi c'est élégant**: L'astuce préfixe/suffixe transforme un processus aléatoire apparemment complexe en un contrôle déterministe de la valeur maximale/min.

En maîtrisant ce problème, vous démontrerez de solides compétences de manipulation de réseau et une bonne compréhension du raisonnement du pire cas** – exactement ce que les entreprises de haute technologie recherchent.

---

Appel à l'action

- **Pratique**: Implémenter la solution dans les trois langues (Java, Python, C++) et exécuter des tests aléatoires.
- **Showcase**: Ajouter la solution à votre repo GitHub et le bloger (comme ce post).
- **Interview**: Apportez ceci dans votre prochain tour de codage; c'est un début de conversation parfait.

Bon codage, et bonne chance pour votre voyage d'entrevue! C'est ce qu'il a dit.

---

**Mots clés**: #Codeleet #Interview Prép #PrefixSuffix #Problèmes d'Array #O(n) #CodageInterview #AlgorithmDesign #Logiciel Génie #Java #Python #C++

---