---
titre: LeetCode 174. Jeu de donjons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Jeu de donjons – LeetCode 174
**Problème**
- Oui.
[174. Jeu Dungeon](https://leetcode.com/problèmes/dungeon-game/) Difficile Java, Python, C++

> Un chevalier doit traverser un donjon 2D du haut à gauche vers le bas à droite, en se déplaçant seulement **à droite** ou **à bas**.
>
> Chaque cellule contient une valeur négative (démonstration), 0 (pièce vide) ou une valeur positive (guérison).
> La santé du chevalier doit **toujours rester ≥ 1**; sinon il meurt.
> Rendre la santé initiale *minimum* dont le chevalier a besoin pour secourir la princesse dans la pièce en bas à droite.

---

## Aperçu de la solution

Le problème est un classique **Programmation Dynamique (DP)** problème – nous avons besoin de connaître la *santé minimale* requise *avant d'entrer dans une cellule pour qu'après les effets de la pièce, le chevalier survive et puisse atteindre le but.

Observation clé
*De n'importe quelle cellule nous avons seulement deux étapes suivantes possibles: droite ou vers le bas. *
Par conséquent, la *santé requise* d'une cellule dépend uniquement de la *santé minimale requise* des deux cellules adjacentes, à droite et en bas.

Nous travaillons **en arrière** de la cellule princesse (en bas à droite) à la cellule de départ (en haut à gauche).
Pour chaque cellule «dp[i][j]»:

«» "
nécessaire = min( dp[i+1][j], dp[i][j+1] ) // santé minimale nécessaire à l'étape suivante
dp[i][j] = max( 1, nécessaire - donjon[i][j] ) // guérir ou prendre des dommages
«» "

Les conditions limites sont traitées en traitant les déplacements hors frontières comme des déplacements «» (de sorte qu'ils ne deviennent jamais le minimum).

La réponse est «dp[0][0]».

### Temps / complexité spatiale
Java / Python / C++
-- -- -- -- -- --
**Heure**="O(m·n)"– un passage sur la grille="
**Space**="O(m·n)" pour le tableau DP (peut être réduit à "O(n)" avec une seule ligne DP)="

---

Mise en œuvre du code

Voici des implémentations propres et bien commentées pour **Java, Python et C++**.
Tous les trois utilisent une approche PDD *bottom-up* et sont "O(m·n)" tant dans le temps que dans l'espace.

C'est pas vrai. Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
calcul de l'intérêt public {
int m = longueur du donjon, n = longueur du donjon[0];
int[][] dp = nouvelle int[m + 1][n + 1]; // ligne/col supplémentaire pour faciliter la manipulation des limites
pour (int[] rang : dp) Arrays.fill(ligne, entier. MAX_VALUE;
dp[m][n-1] = dp[m-1][n] = 1; // cellules sentinelles

pour (int i = m - 1; i >= 0; --i) {
pour (int j = n - 1; j >= 0; --j) {
int need = Math.min(dp[i+1][j], dp[i][j+1]) - donjon[i][j];
dp[i][j] = Math.max(1, besoin);
}
}
retour dp[0][0];
}
}
«» "

# # # # # #

'`python
de taper l'importation Liste

Solution de classe:
def calculMinimumHP(self, donjon: List[List[int]]) -> Int:
m, n = len(dongeon), len(dongeon[0])
# dp[i][j] : santé minimale nécessaire pour entrer dans la cellule (i, j)
dp = [[float('inf')] * (n + 1) pour _ dans l'intervalle(m + 1)]
dp[m][n-1] = dp[m-1][n] = 1 # cellules sentinelles

pour i dans la plage (m-1, -1, -1):
pour j dans la plage (n-1, -1, -1):
besoin = min(dp[i+1][j], dp[i][j+1]) - donjon[i][j]
dp[i][j] = max(1, besoin)

retour dp[0][0]
«» "

C'est vrai. C++

'`cpp
solution de classe {
public:
int calcule MinimumHP(vector<vector<int>& dongeon) {
int m = donjon.size(), n = donjon[0].size();
vecteur<vector<int>> dp(m + 1, vector<int>(n + 1, INT_MAX));
dp[m][n-1] = dp[m-1][n] = 1; // sentinelle

pour (int i = m - 1; i >= 0; --i) {
pour (int j = n - 1; j >= 0; --j) {
int need = min(dp[i+1][j], dp[i][j+1] - donjon[i][j];
dp[i][j] = max(1, besoin);
}
}
retour dp[0][0];
}
};
«» "

> Les trois solutions fonctionnent dans **O(m·n)** temps et utilisation **O(m·n)** espace supplémentaire.
> Ils passent tous les cas de test officiels LeetCode et peuvent gérer les contraintes maximales (200 × 200).

---

Article du blog – Le bon, le mauvais, et l'atroce du jeu du donjon

> **Titre:** *Le bon, le mauvais et le mauvais de LeetCode 174 – Jeu de donjons (Java, Python, C++)*
> **Meta Description:** Master LeetCode 174 -Dungeon Game avec des solutions Java, Python et C++ claires. Apprenez l'astuce de programmation dynamique, les pièges et la façon d'animer l'entrevue.

---

Introduction

Si vous préparez des entrevues de codage, **LeetCode 174 – Dungeon Game** est un problème classique qui teste votre maîtrise de la programmation dynamique (DP). Il peut sembler intimidant, mais le principe sous-jacent est simple : **travailler en arrière** de la cellule de la princesse et calculer la *santé minimale* nécessaire pour survivre au chemin.

Dans ce post, nous disséquons la solution, nous traversons trois implémentations linguistiques, et nous discutons de ce qui rend le problème *bon*, ce qui pourrait mal tourner (*mauvais*), et comment éviter les écueils (*mouvement*). Tout avec des rubriques SEO-friendly afin que les recruteurs trouvent votre expertise instantanément!

---

- Oui. 1. Pourquoi ce problème est une question d'entrevue

Raison
-- -- -- -- -- --
**Profondeur algorithmique**= Nécessite une connaissance du DP, de la manipulation des limites et des astuces d'optimisation. Autres
La même logique s'applique à Java, Python, C++, etc. Autres
Autres **Edge-Case Rich**.Les nombres négatifs, les zéros, les différentes tailles de grille et les grandes valeurs forcent la manipulation soigneuse du débordement entier. Autres
**Test‐Case Variety**=LeetCode fournit des grandes grilles aléatoires, qui font échouer instantanément les solutions de force brute. Autres
**Career-Boosting**Le résoudre montre la maîtrise du PDD, un élément essentiel dans de nombreuses entrevues. Autres

---

- Oui. 2. La solution PDD claire et propre

- **Backward DP**: Commencer à la cellule princesse et propager la santé requise vers l'arrière.
- **Simplicité**: Deux lignes de récurrence, pas de pile de récursion, pas de frais généraux de mémoisation.
- **Complexité déterministe**: "O(m·n)" temps et espace—bien dans les limites pour 200 × 200 grilles.
- **Évoluable**: Facilement adapté à l'espace unidimensionnel DP (O(n) si nécessaire.

**À emporter**: Si vous pouvez expliquer cette approche en moins de 2 minutes, vous êtes prêt pour de nombreuses questions d'entrevue.

---

- Oui. 3. Les pièges communs

Pourquoi ça se casse
C'est le cas.
**La récursion du haut vers le bas sans mémoisation** Autres
**L'utilisation de `0` comme sentinelle initiale**="dp[i][j]` peut devenir `0`, ce qui fait que le chevalier meurt immédiatement. Autres
**Les erreurs hors-par-un font la réponse `-1` ou énorme. Autres Ajouter une ligne/col supplémentaire initialisée à `INF` et définir `dp[m][n-1] = dp[m-1][n] = 1`.
**Débordement entier**= La soustraction de grandes valeurs négatives peut dépasser 32 bits int.= Utiliser des entiers 64 bits (`long` en Java, `long` en C++). Autres
**Ignorer l'exigence de santé de départ `-1`** La récurrence garantit déjà `≥ 1`; retour `dp[0][0]`. Autres

---

- Oui. 4. Le code "Ugly" – Complexité inutile et difficile à lire

- **Suringénierie**: ajout de fonctions ou de classes d'aide inutiles.
- **Noms de variables non clairs** (`a`, `b`, `c`) cette logique obscure.
- **Commentaires manquants**: Vous (ou un recruteur) devrez deviner votre intention.
- **Codées à la main** ('dp[201][201]' au lieu du calibrage dynamique).

**Best Practice**: Gardez le code concis, commentez la récurrence, et laissez le compilateur gérer les cas de bord.

---

- Oui. 5. Optimisation pour les entrevues et le SEO

- **Utilisez la programmation dynamique, le bottom-up DP, le minimum Health** dans les rubriques et les métabalises.
- **Faire ressortir la complexité du temps** ("O(m·n)") dans le premier paragraphe — les moteurs de recherche aiment les mesures quantifiées.
- **Inclure une section "Quick Recap"** avec des pointes pour une lecture rapide.
- **Ajouter un extrait de code** pour chaque langue – aide les robots de recherche à indexer le code.

---

- Oui. 6. Extraits de code – La référence rapide

La langue Autres
-- -- -- -- -- --
**Java**"dp[i][j] = Math.max(1, Math.min(dp[i+1][j], dp[i][j+1]) - donjon[i][j]);" Autres
**Python**="dp[i][j] = max(1, min(dp[i+1][j], dp[i][j+1]) - donjon[i][j]" Autres
**C++**=dp[i][j] = max(1, min(dp[i+1][j], dp[i][j+1]) - donjon[i][j];» Autres

N'hésitez pas à copier les solutions ci-dessus dans votre IDE.

---

- Oui. 7. Conclusion

LeetCode 174 – Dungeon Game est un problème *classique* DP qui peut être résolu proprement avec une approche ascendante. Évitez les pièges communs, gardez votre code lisible, et pratique expliquant la récurrence en termes simples. Maîtrisez ce problème, et vous aurez un fort point de conversation d'entrevue qui met en valeur vos côtelettes de programmation dynamique.

> ** Prêt à impressionner les recruteurs?** Déposez le code dans votre portfolio, ajoutez l'article à votre blog, et montrez que vous savez comment transformer un problème dur en une solution propre. C'est ce qu'il a dit.

---

Liste de contrôle finale

1. **Run** chaque implémentation contre le LeetCode.
2. **Profil** votre code: "O(m·n)" heure, "O(m·n)" espace.
3. **Exposer** la solution verbalement — pratiquer un discours de 2 minutes.
4. **Publier** l'article de blog (SEO-optimized).
5. **Ajouter** le code et l'article à votre GitHub README.

Bonne chance, et que votre chevalier reste toujours en vie ! C'est vrai