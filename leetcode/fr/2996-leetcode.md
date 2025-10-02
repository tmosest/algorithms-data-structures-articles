---
titre: LeetCode 2996. Le plus petit entier manquant plus grand que le préfixe séquentiel -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2996 – Le plus petit entier manquant plus grand que la somme de préfixe séquentiel
*Facile de 50 éléments

---

- Oui. 1. Remise en état des problèmes

On vous donne un tableau entier indexé 0 «nums» (1 ≤ nombres[i] ≤ 50).
Un préfixe **sequentiel** est un préfixe qui commence par `nums[0]` et chaque élément ultérieur augmente de 1, c'est-à-dire

«» "
nombres[0], nombres[0]+1, nombres[0]+2, ..., nombres[i]
«» "

Le préfixe ** le plus long** est le préfixe qui satisfait à cette règle pour le maximum possible "i".
Laissez `S` être la somme de tous les éléments dans ce plus long préfixe.

**Objectif**: Retourner le plus petit entier `x`

* `x` est **non** présent en `nums "
* `x` ≥ `S`

La longueur du tableau est minuscule (= 50), mais nous allons toujours viser une solution O(N log N) qui fonctionne dans les trois langues.

---

- Oui. 2. Intuition

1. **Trouver le plus long préfixe séquentiel**
À partir de `nums[0]`, continuez à ajouter des nombres alors que chaque élément suivant est exactement un plus grand.
Accumuler la somme tout en faisant ça.

2. **Déterminer le plus petit entier manquant ≥ S**
La façon naturelle est de regarder tous les nombres qui sont présents dans "nums".
Si un nombre correspond au candidat actuel `x`, nous devons le sauter – augmenter `x` de 1.
Parce que `nums[i]` est au plus 50 et la longueur du tableau est ≤ 50, nous pouvons simplement stocker les nombres dans un `HashSet` (ou `unordered_set`) et itérer vers le haut de `S`.

Cela donne un algorithme O(N) après avoir construit le jeu.
Le tri dans la solution originale LeetCode est inutile mais inoffensif; l'approche de l'ensemble est plus propre.

---

- Oui. 3. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le plus petit entier manquant requis.

Lemma 1
Après l'étape 1, la variable `S` correspond à la somme du plus long préfixe séquentiel.

*Proof. *
Nous commençons par `S = nombres[0]`.
Pour chaque `i ≥ 1` nous testons si `nums[i]== nombres[i‐1] + 1`.
Si vrai, `nums[0..i]` est séquentiel, donc nous ajoutons `nums[i]` à `S`.
Si faux, le plus long préfixe séquentiel se termine à `i‐1`, alors nous arrêtons.
Ainsi, la boucle s'arrête exactement au dernier élément du plus long préfixe séquentiel, et `S` contient sa somme. *

Lemma 2
Lorsque l'algorithme scanne des entiers candidats `x = S, S+1, S+2, ...` et s'arrête à la première `x` non dans l'ensemble des valeurs de tableau, ce `x` est absent de `nums`.

*Proof. *
L'ensemble contient exactement les entiers qui apparaissent dans `nums`.
Si l'algorithme atteint une valeur `x` qui est *not* dans l'ensemble, alors aucun élément de `nums` égale `x`.

Lemma 3
Le `x` retourné est le plus petit entier `≥ S` qui manque à `nums`.

*Proof. *
L'algorithme vérifie les nombres entiers consécutifs à partir de `S`.
Par Lemma 2, il s'arrête au premier entier manquant.
Par conséquent, aucun entier dans `[S, x‐1]` n'est manquant, et `x` est le plus petit entier manquant ≥ S.

C'est vrai. Théorème
L'algorithme renvoie la réponse requise.

*Proof. *
Par Lemma 1, `S` est la somme du plus long préfixe séquentiel.
Par Lemma 3, le `x` retourné est le plus petit entier ≥ S non présent dans `nums`.
Ainsi, l'algorithme satisfait la définition du problème. *

---

- Oui. 4. Analyse de la complexité

Étape d'opération de temps d'opération d'espace supplémentaire
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Autres Analyser le plus long préfixe séquentielle **O(N)**
Autres 2= Ensemble de valeurs de construction **O(N)**=
Autres 3= Analyse vers le haut de `S` (mauvaise affaire O(51‐S) ≤ O(50))= **O(N)**= O(1)=

Total : **O(N)** temps, **O(N)** espace.
Avec `N ≤ 50` c'est trivial.

---

- Oui. 5. Cas de bord

Motif
C'est quoi ?
Autres Tous les nombres sont les mêmes ('[5,5]') Le préfixe le plus long = 1 → `S = 5`. L'entier manquant ≥ 5 est `6'. Autres
Autres Le tableau est déjà un préfixe séquentielle parfait (`[1,2,3,4]`) Autres
Le tableau contient tous les nombres de 1 à 50, mais `S` est déjà présent. L'algorithme va sauter `S` et retourner `S+1`. Autres
Le tableau contient des duplicata, par exemple `[1,2,2,3]`.Les duplicata n'affectent pas la somme du préfixe; le jeu gère automatiquement les duplicata. Autres

---

- Oui. 6. Mise en œuvre du code

Voici des solutions propres, spécifiques à la langue, qui suivent l'algorithme défini décrit ci-dessus.

---

##### 6.1 Java

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe {
Integer(int[] nums) {
// 1. Trouver le plus long préfixe séquentiel et sa somme S
somme int = nombres[0];
pour (int i = 1; i < nombres de longueur; i++) {
si (nums[i] == nombres[i - 1] + 1) {
somme += nombres[i];
} autre {
pause;
}
}

// 2. Construisez ensemble de tous les nombres dans le tableau
Définir<entier> présent = nouveau HashSet<>();
pour (int v : nombres) {
présent.add(v);
}

// 3. Trouver le plus petit entier manquant >= Montant
int candidate = somme;
pendant que (présent.contient(candidat)) {
candidat++;
}
candidat au retour;
}
}
«» "

**Pourquoi c'est bon**
* Utilise `HashSet` pour les recherches O(1).
* Pas de tri inutile.
* Facile à lire et à entretenir.

---

##### 6.2 Python

'`python
Solution de classe:
def manquant Integer(self, nombres: list[int]) -> Int:
# La somme la plus longue du préfixe séquentiel
Total = nombres[0]
pour i dans la plage(1, len(nums)):
si des nombres [i] == nombres[i - 1] + 1:
Total += nombres[i]
Sinon:
pause

# Set pour les tests d'adhésion O(1)
présent = ensemble(s)

# Le plus petit entier manquant >= total
candidat = total
alors que le candidat actuel:
candidat += 1
candidat au retour
«» "

Les Python's intégrés `set` donnent les mêmes performances que les Java's `HashSet`.

---

*### 6.3 C++

'`cpp
#incluez <vecteur>
#inclut <unordered_set>

solution de classe {
public:
Int manquantInteger(std::vector<int>& nums) {
// Somme du préfixe le plus long
somme int = nombres[0];
pour (size_t i = 1; i < nums.size(); ++i) {
si (nums[i] == nombres[i - 1] + 1) {
somme += nombres[i];
} autre {
pause;
}
}

// Construire un_set désordonné pour la recherche O(1)
std::unordered_set<int> present(nums.begin(), nums.end());

// Le plus petit entier manquant >= Montant
int candidate = somme;
pendant que (présent.count(candidat)) {
+candidate;
}
candidat au retour;
}
};
«» "

La solution C++ reflète celle de Java mais utilise `unordered_set`.

---

- Oui. 7. Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
**Concept**
* Code * Nettoyez, pas de tri, temps O(N)
**Readability**
**Performance** N → négligeable
**Boîtes de corner**
**Piège potentiel**= Oublier d'ajouter `nums[0]` à `sum`=–=

> **Ligne de bottom:** La solution est élégante et efficace; il n'y a pas de pièces cachées.

---

- Oui. 8. Stratégie d ' essai

1. ** Essais de base**
* Exemple de cas de la déclaration.
* Tableau d'éléments uniques (`[1]` → répondre `2`).

2. **Préfixes séquentiels**
* `[4,5,6,10]` → le plus long préfixe somme `15`, réponse `15` (depuis 15 non présent).
* `[10,11,12,13]` → somme `46`, réponse `46`.

3. **Doublons**
* `[1,2,2,34]` → somme `10`, réponse `11`.

4. ** Portée complète**
* `[1,2,3,...,50]` → somme `1275`, réponse `1276`.

5. **Démarrage non séquentiel* *
* `[5,6,7]` → somme `18`, réponse `18`.

Exécutez chaque implémentation de langage sur le même ensemble de tests pour assurer la cohérence.

---

- Oui. 9. Pensées finales et conseils de carrière

* **Pourquoi cela importe:**
Ce problème teste la capacité d'un candidat à traduire une spécification apparemment simple en code efficace, et à raisonner sur les cas de bord. Les intervieweurs adorent parce que cela vous force à penser à *prefixes*, *sum* et *set membership* – tous les thèmes d'entrevue communs.

* ** Comment l'as sur une entrevue en direct : * *
* Dessinez rapidement l'algorithme sur papier.
* Discutez de la complexité à l'avant.
* Mentionnez l'approche définie pour éviter le tri.
* Valider avec quelques exemples faits à la main.

* **Balises pour votre blog:**
`LeetCode 2996`, `Smallest Missing Integer`, `Sequential Prefix Sum`, `Java solution`, `Python solution`, `C++ solution`, `Algorithm Analysis`, `Interview Prep`, `Coding Interview`, `Data Structures`, `Set Operations`, `O(N) solution`.

---

10. Article de blog (optimisé par le référencement)

> **Titre:**
> *LeetCode 2996 – Le plus petit entier manquant plus que la somme de préfixe séquentiel: une solution pleine pile en Java, Python & C++ *
> *Plus une plongée profonde dans l'algorithme, la complexité et les conseils prêts à l'entrevue. *

---

Introduction

Si vous chassez pour un problème de LeetCode qui est encore frais sur le radar d'entrevue, ne cherchez pas plus loin que **LeetCode 2996**. La tâche combine une astuce préfixe classique à une recherche simple – un terrain d'entraînement parfait pour votre prochaine entrevue sur la structure des données.

---

Aperçu du problème

On nous donne un tableau "nums" (taille ≤ 50).
* Trouvez le plus long préfixe qui est *sequentiel* – chaque nombre est un plus grand que le précédent.
* Calculez la somme `S` de ce préfixe.
* Retourner le plus petit entier `x ≥ S` qui ne **pas** apparaissent dans `nums`.

---

Pourquoi ce problème est-il l'entrevue-or

1. **Clarté des spécifications** – pas de astuces cachées.
2. **Plusieurs approches valides** – tri, deux-pass, mise en page.
3. **Application directe des concepts de base** – boucles, conditions, ensembles de hachage.
4. ** Richesse de la caisse d'Edge** – duplicata, gammes complètes, démarrages non séquentiels.

---

L'algorithme basé sur l'ensemble

Nous traversons des "nums" une fois pour trouver le préfixe.
Ensuite, nous *construisons un ensemble de hachage* contenant toutes les valeurs uniques.
Enfin, nous partons de "S" vers le haut, nous arrêtant à la première valeur manquante.

Texte
O(N) temps
«» "

Pas de tri nécessaire – c'est la solution la plus propre et la plus rapide pour les petites entrées.

---

Échantillons de codes complets

(Voir rubrique 6.6 ci-dessus pour le code Java, Python et C++.)

---

Complexité et bord Analyse de cas

* **Time**: `O(N)` – un seul balayage + une boucle de taille constante.
* **Espace**: `O(N)` – l'ensemble contient au plus 50 entiers.
* **Longueur d'analyse de la pire affaire**: 50 – donc l'algorithme est pratiquement instantané.

---

#### Tester votre solution

1. Écrire un petit harnais d'essai dans chaque langue.
2. Inclure tous les exemples fournis et les cas exceptionnels.
3. Vérifier que chaque mise en œuvre produit la même production.

---

#### Liste de contrôle de la préparation de l'entrevue

Liste de contrôle Pourquoi ça aide
C'est quoi ?
Un algorithme de croquis montre que vous comprenez le problème. Autres
La complexité de l'État démontre la compétence analytique. Autres
Expliquez ensemble vs trier. Autres
Autres Marchez à travers des exemples. Autres
Autres Posez des questions claires. Autres

---

À emporter

LeetCode 2996 n'est pas juste un problème ; c'est un *mini-talk* sur la façon de penser algorithmiquement. Maîtrisez-le, postez votre solution sur GitHub, et vous aurez un point de discussion prêt à l'emploi qui présente un code propre, une logique efficace et des fondamentaux solides de la structure des données.

---

Appel à l'action

Vous avez votre propre idée de ce problème ? Vous voulez discuter d'autres approches ou des optimisations plus profondes? Laissez un commentaire ci-dessous, ou consultez le dépôt **full code** lié dans la description. Bon codage !

---

> **Tags**: `LeetCode 2996`, `Algorithm`, `Interview Prep`, `Java`, `Python`, `C++`, `Data Structures`, `Set`, `Sum`, `Prefix`, `Coding Interview`, `Coding Challenge`.

---

11 ans. Conclusion

- **Algorithme**: Somme le plus long préfixe séquentiel → Définir la recherche.
- **Complexité**: temps O(N), espace O(N).
- **Robustness**: Poignées des duplicatas, des petites portées, des séquences complètes.
- **Valeur de carrière**: Démontre la clarté, l'efficacité et la communication prête à l'entrevue.

Armé de ces implémentations et de ces idées, vous êtes prêt à affronter **LeetCode 2996** avec confiance et impressionnez votre prochain intervieweur. Bon codage !