---
titre: LeetCode 3396. Nombre minimum d'opérations pour faire des éléments dans la répartition Distinct -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
### Code en Java=Python=C++ + Un message de blog optimisé pour stimuler votre jeu d'entrevue

---

Récapitulatif du problème (de LeetCode)

> On vous donne un nombre entier.
> Dans une opération, vous pouvez **supprimer les trois premiers éléments** du tableau (si moins de 3 restent, supprimer tous).
> Un tableau est considéré comme "distinct" si tous ses éléments sont uniques.
> Retournez le nombre **minimum** d'opérations nécessaires pour distinguer le tableau.
> (Un tableau vide est toujours distinct.)

**Contrôles* *

Valeur des contraintes
C'est pas vrai.
1 ≤ longueur nums ≤ 100 '

---

- Oui. Aperçu de haut niveau

La seule façon d'enlever les duplicata est de couper le *front*.
Ainsi, le problème se réduit à:

> **Trouvez l'index le plus ancien (en regardant de l'arrière) où apparaît un duplicata. **
> Tous les éléments jusqu'à cet index doivent être supprimés, et chaque opération enlève 3 éléments de l'avant.
> Le nombre d'opérations est simplement «ceil(i+1)/3»)».

Parce que `nums[i] ≤ 100`, un simple tableau de fréquence (taille 101) est suffisant – pas de carte de hachage nécessaire.

---

Solutions de code

Voici trois implémentations :

Langue Approche Temps Espace
- C'est quoi ?
*Java** * Greedy (O(n)) * O(n) * O(1) *
*Python * Greedy (O(n))
(O(n))

N'hésitez pas à copier le code dans votre éditeur IDE ou LeetCode.

---

#### 2.1 Java (Optimal Greedy)

"Java
// Java 17
solution de classe {
Nombre minimum d'opérations (int[] nombres) {
// freq[0] est inutilisé parce que nombres[i] >= 1
int[] freq = nouvelle int[101];
// Scanner à partir du dos; premier duplicata force les retraits
pour (int i = longueur nominale - 1; i >= 0; --i) {
si (++freq[nums[i]] > 1) {
// (i + 3) / 3 == Ceil(i+1)/3)
retour (i + 3) / 3;
}
}
retour 0; // déjà distinct
}
}
«» "

> **Pourquoi ça marche* *
> Nous gardons un nombre de fréquence en se déplaçant de droite à gauche.
> La première fois que nous voyons une valeur déjà vue, tous les éléments jusqu'à cet indice doivent être supprimés.
> Chaque opération parcourt 3 éléments, de sorte que le nombre d'opérations est le plafond de `(i+1)/3`.

---

#### 2.2 Python (végétation optimale)

'`python
# Python 3.10+
Solution de classe:
def minimumOperations(self, nombres: List[int]) -> Int:
freq = [0] * 101 # 1 uniquement
pour i dans la plage (len(nums) - 1, -1, -1):
freq[nums[i]] += 1
si freq[nums[i]] > 1 :
# ceil((i+1)/3) => (i + 3) // 3
retour (i + 3) // 3
retour 0
«» "

---

#### 2.3 C++ (Célébration optimale)

'`cpp
// C++17
solution de classe {
public:
int minimumOperations(vecteur<int>& nums) {
vector<int> freq(101, 0); // valeurs 1..100
pour (int i = nombres.size() - 1; i >= 0; --i) {
si (++freq[nums[i]] > 1) {
// ceil(i+1)/3)
retour (i + 3) / 3;
}
}
retour 0;
}
};
«» "

---

2.4 Brute-Force (Simulation) – Pour apprendre

> **Utile pour comprendre le problème mais pas optimal. **

"Java
// Java – simulation O(n^2)
solution de classe {
Nombre minimum d'opérations (int[] nombres) {
Int ops = 0;
int[] arr = nums.clone();
alors que (vrai) {
en cas de rupture (allDistinct(arr));
int toRemove = Math.min(3, longueur d'arrondi);
arr = Arrays.copyOfRange(arr, toRemove, arr.longueur);
ops++;
}
les opérations de retour;
}

Booléen privé tousDistinct(int[] a) {
Définir<integer> vu = nouveau HashSet<>();
pour (int v : a) si (!seen.add(v)) retourner faux;
retour vrai;
}
}
«» "

---

Article sur le blog – Le bon, le mauvais et le mauvais de LeetCode 3396

> **Titre**: *LeetCode 3396 – Maîtriser le nombre minimum d'opérations pour distinguer les éléments d'array*
> **Méta-Description**: Découvrez comment résoudre LeetCode 3396 en Java, Python et C++. Comprendre la cupidité et la force brute, les compromis entre le temps et l'espace et les conseils d'entrevue. Augmentez votre score d'entrevue de codage maintenant. (en milliers de dollars)

---

Introduction

Si vous êtes en préparation pour une interview d'ingénierie logicielle, vous allez rencontrer des variations d'un tableau unique. LeetCode 3396 ajoute une torsion : vous ne pouvez couper que les trois premiers éléments de chaque opération. Le défi est de **minimiser** ces opérations.

Dans cet article, nous disséquerons le problème, nous passerons par une solution gourmande, et nous le comparerons à une approche de force brute. Nous allons également afficher le code en Java, Python et C++, et vous donner des explications prêtes à l'entretien.

---

#### 2-

- **Objectif** : Enlever les duplicatas avec le moins d'opérations de retrait.
- **Key Insight**: Le retrait du front nous force à penser en termes de *préfixes*.
- **Observation**: Si vous scannez le tableau de droite à gauche, la première fois que vous appuyez sur un duplicata vous indique exactement combien d'éléments vous devez supprimer.

---

C'est vrai. L'Agréable – L'optimalité

Étape Ce qu'il faut faire Pourquoi il est efficace
C'est un problème.
Autres **1**=Scan depuis l'arrière. Chaque élément qui a déjà été vu signifie que *doit* être dans le préfixe que nous supprimons. Autres
Autres Nombre de fréquences dans un tableau de taille 101. Aucune carte de hachage – espace constant en raison de contraintes. Autres
Autres Sur le premier duplicata, calculer "ceil((i+1)/3)". Parce que chaque opération supprime 3 éléments de l'avant. Autres

3.1 Complexité temporelle et spatiale

- **Heure** : "O(n)" – laissez-passer unique.
- **Espace**: `O(1)` – seulement un tableau de 101 éléments.

Ces complexités sont parfaites pour l'entrevue : rapide à expliquer et rapide à courir.

---

C'est vrai. La simulation "Bad" – Brute-Force

L'approche de simulation reflète ce qu'un candidat naïf pourrait coder en premier.

- **Algorithme** : Alors que le tableau contient des duplicatas, supprimez les 3 premiers éléments.
- **Complexité**: pire cas de `O(n^2)` parce que nous reconstruisons le tableau à chaque fois.
- **Drawback**: Ne pas évoluer au-delà des petites contraintes; obtiendra une limite de temps dépassée d'avertissement si la suite de test est plus grande.

**Pourquoi l'apprendre?**
Comprendre pourquoi la simulation échoue vous aide à repérer le modèle d'avidité optimal lors des entrevues.

---

C'est pas vrai. Les erreurs courantes

Comment corriger
- C'est quoi ?
Autres Oubliant que la première opération **** supprime *exactement* 3 éléments. Autres
Autres En utilisant une carte de hachage, mais en oubliant la gamme 1-basée...... .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . Autres
Revenir `i / 3 + 1` directement. Autres

---

C'est vrai. Explication de l'entrevue-réalisé

> Pourquoi la solution avide fonctionne-t-elle ? *
> Nous traitons de l'arrière. Le premier duplicata que nous rencontrons * nous force à tout supprimer jusqu'à ce point. Chaque opération supprime 3 éléments avant, de sorte que les opérations minimales sont le *ceil* de la longueur du préfixe divisé par 3.
> Parce que `nums[i] ≤ 100`, nous pouvons garder un petit tableau de fréquences, rendant la solution à la fois rapide et mémoire-lumière.

> **Questions de suivi possibles* *
> - *Et si l'opération supprimait 2 éléments au lieu de 3? *
> → Remplacer `ceil(i+1)/2)` par `(i + 2) / 2`.
> - *Et si nous pouvions enlever tout bloc contigu? *
> → Le problème devient un DPP classique, qui est un défi différent.

---

- Oui. Développement d'essais

Assurez-vous de valider votre solution dans les cas suivants :

Nombres prévus
C'est pas vrai.
[3,2,1,2,3]
[3,1,5,3,1,4,5]
[1,2,3]
[1,1,1,1]
[5,5,5,5,5]

Ajoutez des tests unitaires dans votre cadre préféré. Par exemple, en Java:

"Java
@Test
Essai de vide() {
affermEquals(1, nouvelle solution().minimumOpérations(nouvelle int[]{3,2,1,2,3});
}
«» "

---

#### 7-

- **Soyez simple**: Un seul passage de l'arrière suffit.
- ** Expliquez votre intuition**: Nous sommes forcés de couper les préfixes, donc nous avons seulement besoin de savoir où le premier duplicata apparaît de la fin. (en milliers de dollars)
- **Parler des contraintes**: Comme les valeurs sont ≤ 100, un tableau de 101 compteurs suffit, ce qui maintient l'espace de la solution O(1). (en milliers de dollars)
- **Complexité temporelle**: Souligner le temps linéaire – critique pour les grandes entrées.
- **Edge Cases**: Un tableau déjà distinct → 0 ops. Tableau vide → 0 ops.

---

Faits saillants du SEO

- **Mots-clés**: LeetCode 3396, Nombre minimum d'opérations, Faire Array Unique, Codage Interview, Java, Python, C++ Solution, Greedy Algorithm, Préparation d'entrevues, Structures de données, complexité temporelle, complexité spatiale.
- **Étiquettes d'en-tête**: Utilisez `<h1>` pour le titre, `<h2>` pour les sections principales, `<h3>` pour les sous-sections.
- **Liens internes**: Lien vers des problèmes liés au LeetCode comme -Supprimer les duplicatas d'un tableau ou -Supprimer les parties dans les sous-arrays. (en milliers de dollars)
- ** Liens externes** : référencez la page de problème officielle de LeetCode, un tutoriel sur les algorithmes gourmands, ou un blog sur la préparation des interviews.

---

Clôture

LeetCode 3396 peut sembler simple, mais il s'agit d'un excellent test de *observation*, de *raisonnage agréable* et de *codage propre*. En maîtrisant ce problème en trois langues et en comprenant les compromis, vous serez prêt à impressionner n'importe quel intervieweur.

> **À emporter**:
> *Lorsque les duplicatas ne peuvent être retirés que de l'avant, le premier duplicata de l'arrière dicte le nombre d'opérations. *
> Implémentez la solution gourmande, expliquez l'intuition, et regardez votre confiance en interview monter en flèche.

Bon codage – et bonne chance pour votre prochaine entrevue! Les

---