---
Titre: LeetCode 556. Suivant Élément III -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Suivant Élément III – Un bon, mauvais et mauvais – Plongée (Java-Python-C++)
*LeetCode 556 – Medium – ..Trouver le prochain entier plus grand avec les mêmes chiffres.

---

Pourquoi ce problème te fait penser

- **LeetCode Haut de la page-10 Questions d'entrevue** – Les recruteurs sur LinkedIn, Indeed & Loading l'énumèrent fréquemment.
- **Shows Core Algorithm Skills** – Permutations, cupidité et raisonnement de pile.
- **Langue Agnostique** – Démontrer la compétence en *Java, Python, C++* (et même Go, Rust, etc.).
- **Hands-On Complexity Analysis** – O(n) time & O(1) espace supplémentaire.

> **Mots-clés du référencement**: *Next Grand Élément III, LeetCode 556, problème d'entrevue, algorithme, entretien de codage, entretien de codage Java, entretien de codage Python, entretien de codage C++, entretien d'ingénieur logiciel. *

---

Récapitulation du problème

> **Input**: entier positif `n` (1 ≤ n < 231).
> **Objectif** : Trouvez le nombre entier le plus petit :
> 1. Utilise exactement les mêmes chiffres décimaux que `n`.
> 2. est supérieur à "n".
> 3. Convient à un entier de 32 bits signé; sinon retourner `-1`.

**Exemples**

Produit
- Oui.
Dénomination des marchandises
Dénomination des marchandises
Dénomination des marchandises
115
ANNEXE

---

## Stratégie de haut niveau – ♫Prochaine permutation de chiffres

La tâche est précisément la prochaine permutation lexicographique* de la séquence numérique.

1. **Trouver le pivot** – le premier chiffre (de droite) qui est **plus petit** que son voisin droit.
- Si aucun n'existe → les chiffres sont dans l'ordre décroissant → aucun plus grand nombre n'existe.
2. **Trouver le successeur** – le plus petit chiffre à droite du pivot qui est **plus grand** que le pivot.
3. **Swap** pivot et successeur.
4. **Revers** (ou trier en montant) le suffixe droit du pivot – cela donne le plus petit nombre plus grand.

Toute la routine est *O(L)* où `L` est le nombre de chiffres (=10 pour les ints 32 bits).
L'espace est *O(1)* – nous travaillons en place sur un tableau de caractères.

---

Surmonter Pièges d'affaires

Autres Décision Pourquoi il vous voyage
- Oui.
**Overflow**. Même si la prochaine permutation existe, le résultat peut dépasser `INT_MAX`. Parse dans une variable 64 bits (`long` en Java/C++ ou `int64` en Python) et comparer avec `231‐1`. Autres
**Tous les mêmes chiffres** Autres
**Trainer des zéros**= `120` → suivant est `201` (notez l'ordre d'échange). Suffix inversion gère les zéros automatiquement. Autres
** Nombres négatifs** ► Le problème garantit un code positif, mais défensif. Vérifier `n < 0` et retourner `-1`. Autres
**Les plus grands nombres**=2147483647= → le suivant existe mais déborde.=Utilisez 64 bits temporaires et rejetez si > `INT_MAX`. Autres

---

## Mise en œuvre du code

- Oui. 1. Java (bibliothèque standard, `int`)

"Java
solution de classe publique {
Int public nextGreaterElement(int n) {
char[] chiffres = entier.àString(n).àCharArray();

// Étape 1: Trouver le pivot
i = chiffres.longueur - 2;
pendant que (i >= 0 && chiffres[i] >= chiffres[i + 1]) i--;
si (i < 0) retour -1; // déjà permutation maximale

// Étape 2: Trouver un successeur
int j = chiffres.longueur - 1;
pendant que (j >= 0 && chiffres[j] <= chiffres[i]) J--;

// Étape 3: Échanger
swap(chiffres, i, j);

// Étape 4: suffixe inverse
inverse(chiffres, i + 1);

// Contrôle du dépassement
long résultat = Long.parseLong(nouvelle chaîne(chiffres));
retour du résultat > Integer.MAX_VALUE ? -1 : (int) résultat;
}

Swap privé à vide(char[]a, int i, int j) {
char t = a[i]; a[i] = a[j]; a[j] = t;
}

vide privé inverse(char[] a, int démarrage) {
int l = début, r = longueur - 1;
pendant le swap (a, l++, r--);
}
}
«» "

- Oui. 2. Python (élégant, 3 lignes dans la boucle)

'`python
Solution de classe:
def nextGreaterElement(self, n: int) -> Int:
s = liste(str(n))
i = len(s) - 2
alors que i >= 0 et s[i] >= [i+1]:
I -= 1
i < 0: retour -1

j = len(s) - 1
alors que s[j] <= s[i]:
J = 1

s[i], s[j] = s[j], s[i]
s[i+1:] = inversé(s[i+1:]) # suffixe inversé

val = int('.join(s))
retourner la valeur si la valeur <= 2**31-1 autre -1
«» "

- Oui. 3. C++ (Fast, STL)

'`cpp
solution de classe {
public:
Int nextGreaterElement(int n) {
chaîne s = to_string(n);
i = s.size() - 2;
(i >= 0 && s[i] >= s[i+1]) --i;
si (i < 0) retour -1;

int j = s.size() - 1;
pendant que (s[j] <= s[i]) --j;

swap(s)[i], s[j];
inverse(s.degin() + i + 1, s.end());

long vall = stoll(s);
retour (val > INT_MAX) ? -1 : static_cast<int>(val);
}
};
«» "

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Trouver le pivot O(L)
Trouver le successeur
Swap et inversement O(L)
Analyse finale et contrôle du débordement

Total: **O(L)** temps, **O(1)** espace auxiliaire.
Avec `L ≤ 10` l'algorithme est effectivement *constant* pour toutes les entrées.

---

## Entretien-Préparation Discussion

1. **Pourquoi la prochaine permutation? **
- Les chiffres sont une chaîne de caractères; générer toutes les permutations est factorial-time – impossible pour 10 chiffres.
- Greedy Find la première paire décroissante de l'ordre *next* lexicographique.

2. **Autres approches**
- **Stack** : poussez les chiffres, pop jusqu'à ce que vous trouviez un chiffre plus petit, etc. (essentiellement le même algorithme).
- **Trier le suffixe** : au lieu de renverser, trier le suffixe ascendant – même résultat mais O(L log L).
- **Énumération en bitmasques**: ne fonctionne que pour les très petits chiffres.

3. ** Erreurs communes* *
- Oublier de gérer le débordement.
- Échanger des indices erronés (off‐by‐one).
- Réverser la mauvaise partie (pivot inclus).

4. **Stratégie de test**
- Tous les chiffres descendant → -1.
- Tous les chiffres ascendant → trivial suivant.
- Un seul chiffre → -1.
- Bord de la limite 32 bits (`2147483638` → `2147483863`).
- Nombres comportant des doubles (`115` → `151`).

---

- Oui. Le bon, le mauvais et le mauvais

Aspect du bien
- C'est quoi ?
LeetCode agrafe, enseigne les permutations
**Mise en oeuvre**= Un seul passage, en place== Nécessite une gestion soigneuse de l'index== Dépassement de la manipulation conduisant à WA==
**Readability**
**Performance**= O(10) constante== Aucune= Allocation excessive de mémoire (p. ex. conversion en liste d'entrées)=

---

## À emporter pour la chasse au travail

- **Afficher le modèle**: *prochaine permutation* est une recette réutilisable (utilisée dans des problèmes comme la Permutation suivante ou le plus grand nombre).
- **Parler de cas de bord**: L'overflow est une question d'entrevue classique; la manipulation montre l'attention aux détails.
- **Discussion du temps et de l'espace**: Les recruteurs aiment quand les candidats articulent *O(n)* vs *O(n log n)* compromis.
- ** Démontrer la flexibilité linguistique** : Fournir la même logique en Java, Python, C++ – indique des compétences fortes en multiplateforme.

---

Les pensées finales

Solving LeetCode 556 se sent comme déverrouiller un niveau secret dans votre arsenal d'entretien. En maîtrisant la logique de la prochaine permutation et en anticipant les pièges, vous impressionnerez les recruteurs qui apprécient le code propre, efficace et sans bug.

Joyeux codage, et que les dieux de l'interview vous bénissent avec le prochain grand travail! C'est ce qu'il a dit.

---

**Mots clés pour SEO**: Next Greater Element III, LeetCode 556, algorithme d'entrevue, prochaine permutation, code d'entrevue d'emploi, entretien de codage de Java, interview de Python, interview de C++, entretien d'ingénieur logiciel, résolution de problèmes algorithmique.