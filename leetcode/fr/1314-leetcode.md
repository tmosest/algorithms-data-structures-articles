---
titre: LeetCode 1314. Somme du bloc de matrice -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Voici des implémentations propres et prêtes à la production de **LeetCode 1314 – Matrix Block Sum** écrit en **Java, Python et C++**.
Tous les trois utilisent un préfixe **2-D sum** (également appelé image intégrale) pour calculer chaque somme de blocs en **O(m × n)** temps et **O(m × n)** mémoire auxiliaire – la solution optimale pour ce problème.

> **Astuce:** Les sommes de préfixe sont un modèle d'entrevue classique. La maîtrise de ces questions vous donne un coup de pouce instantané pour une grande variété de questions.

---

### Java – Préfixe-Sum + DP propre

"Java
Importer java.util. Les tableaux;

solution de classe publique {

matriceBlockSum(int[][] mat, int k) {
int m = longueur du tapis;
n = longueur mat[0];

// 1-based prefix sum array
int[][] pref = nouvelle int[m + 1][n + 1];

pour (int i = 1; i <= m; i++) {
pour (int j = 1; j <= n; j++) {
pref[i][j] = pref[i - 1][j] + pref[i][j - 1]
- pref[i - 1] [j - 1] + mat[i - 1] [j - 1];
}
}

int[]] ans = nouveau int[m][n];

pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
int r1 = Math.max(0, i - k) + 1; // inclusivement, basé sur 1
int c1 = Math.max(0, j - k) + 1;
int r2 = Math.min(m, i + k + 1); // exclusif
int c2 = Math.min(n, j + k + 1);

ANS[i][j] = pref[r2][c2] - pref[r1 - 1][c2]
- pref[r2][c1 - 1] + pref[r1 - 1][c1 - 1];
}
}

le retour des an;
}

// ---- pour des essais manuels rapides ----
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
[][] mat = {{12,3},{4,5,6},{7,8,9}};
[] [] res = s.matrixBlockSum(mat, 1);
Système.out.println(Arrays.deepToString(res));
}
}
«» "

---

### Python – Préfixe rapide-Sum (sans NumPy)

'`python
Solution de classe:
def matrixBlockSum(self, mat: List[List[int]], k: int) -> Liste[Liste[int]]:
m, n = len(mat), len(mat[0])

# 1 – somme du préfixe
pref = [[0] * (n + 1) pour _ dans la plage (m + 1)]
pour i à portée (1, m + 1):
ligne_sum = 0
pour j dans la plage(1, n + 1):
ligne_sum += mat[i-1][j-1]
pref[i][j] = pref[i-1][j] + range_sum

ans = [[0] * n pour _ dans l ' intervalle(m)]
pour i dans la plage (m):
pour j dans la plage(n):
r1 = max(0, i - k) + 1
c1 = max(0, j - k) + 1
r2 = min(m, i + k + 1)
c2 = min(n, j + k + 1)
[i] [j] = (
[r2][c2]
- pref[r1-1][c2]
- pref[r2][c1-1]
+ pref[r1-1][c1-1]
)
retour et
«» "

> **Note :** La boucle intérieure est délibérément écrite en Python clair pour plus de clarté. Si vous êtes sur Python 3.8+, vous pouvez utiliser `itertools.accumulate` ou `NumPy` pour un léger boost de vitesse.

---

### C++ – O(m·n) avec la somme du préfixe 2-D

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<vector<int>> matriceBlockSum(vector<vector<int>>& mat, int k) {
int m = mat.size(), n = mat[0].size();
vecteur<vector<int>> pref(m + 1, vecteur<int>(n + 1, 0)

// Calculer la somme du préfixe 1
pour (int i = 1; i <= m; ++i) {
dans la ligneSum = 0;
pour (int j = 1; j <= n; ++j) {
 rangSum += mat[i-1][j-1];
pref[i][j] = pref[i-1][j] + rangSum;
}
}

vector<vector<int>> ans(m, vector<int>(n, 0));

pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
int r1 = max(0, i - k) + 1;
c1 = max(0, j - k) + 1;
int r2 = min(m, i + k + 1);
int c2 = min(n, j + k + 1);
ANS[i][j] = pref[r2][c2] - pref[r1-1][c2]
- pref[r2][c1-1] + pref[r1-1][c1-1];
}
}
le retour des an;
}
};
«» "

---

- Oui. 2. Article du blog – Le Block Sum de Matrix: Le Bon, Le Mauvais, et le Ugly

> **SEO Mots-clés**: Matrix Block Sum, LeetCode 1314, 2-D prefix sum, programmation dynamique, codage d'entrevue, Java, Python, solution C++, codage interview, entretien d'emploi, algorithme.

---

- Oui. H1 – Matrix Block Sum: Maîtriser un problème classique de LeetCode

> *=Avec une matrice `m × n` et un entier `k`, calculer la somme de chaque bloc `k`-radius autour de chaque cellule.
> Cette tâche apparemment simple est essentielle dans le codage des entrevues. Il teste votre capacité à transformer une boucle de force brute en solution mathématiquement intelligente.

### H2 – Le problème, en anglais clair

- **Input**: `mat` – `m × n` matrice entière; `k` – entier non négatif.
- **Output**: `ans` – matrice de même taille où chaque `ans[i][j]` équivaut à la somme de tous les éléments `mat[r][c]` satisfaisant
"r - i.I ≤ k" et "c - j.I ≤ k".
Les frontières sont tronquées – vous ne lisez jamais en dehors de la matrice.

> Pourquoi est-ce important ? *
> Les intervieweurs demandent souvent une solution « O(m × n) », ce qui signifie que vous ne pouvez pas vous permettre une boucle nichée naïve pour chaque cellule.

### H2 – Bonne : l'approche préfixe-sum

Ce qui arrive Pourquoi ça marche
- C'est quoi ?
Autres 1. **Construire une somme de préfixe 2-D.**="pref[i][j]` = somme de toutes les cellules dans le rectangle `(0,0)` à `(i-1,j-1)". Permet des requêtes de somme rectangle à temps constant. Autres
Autres 2. **Convertissez chaque requête dans un rectangle de préfixe.**= Le bloc autour de `(i,j)` est un rectangle `[r1,r2] × [c1,c2]`.== La somme = `pref[r2][c2] - pref[r1-1][c2] - pref[r2][c1-1] + pref[r1-1][c1-1]`. Autres
Autres 3. ** Calculer l ' an en O(1) par cellule**= Pour toutes les cellules `m × n`. Temps total = "O(m × n)". Autres
Autres 4. **Mémorie**= `pref` est `(m+1)×(n+1)`; `ans` est `m×n`.= Acceptable pour les contraintes jusqu'à 100. Autres

> *Résultat*: 100% correcteur, vitesse optimale et code propre.

### H2 – Mauvais : La Force Brute `O(m × n × k2)` Solution

'`python
pour i dans la plage (m):
pour j dans la plage(n):
Total = 0
pour r dans la plage (max(0, i-k), min(m, i+k+1):
pour c dans la plage (max(0, j-k), min(n, j+k+1):
Total += mat[r][c]
ans[i][j] = total
«» "

- **Time**: "O(m × n × k2)" → 106 × k2 opérations.
Avec `k` jusqu'à 100, cela peut exploser jusqu'à 1010 – bien trop lent.
- **Espace** : Même chose que l'optimum, mais l'effort perdu.

> *Pourquoi est-ce mauvais? *
> Les intervieweurs s'attendent à ce que vous pensiez au-delà des boucles imbriquées évidentes. La force brute est un drapeau rouge classique.

### H2 – Ugly: Edge‐ Défaut de traitement et de non-traitement des affaires Un seul piège

1. **Off‐par‐un dans les indices préfixes**
- `pref` est 1-based, mais beaucoup de nouveaux oublient le +1 offset, produisant de mauvais résultats.
2. **Bonne fixation**
- Le fait d'oublier `max(0, ...)` ou `min(m, ...)` conduit à des erreurs de tableau-out-of-bounds.
3. **Débordement entier**
- Dans des langues comme Java ou C++, les sommes cumulées peuvent dépasser `int`. Utilisez `long` ou `long` si «mat[i][j]» peut être grand.
4. **Nom de variable non conforme**
- Le mélange `r1`/`c1` pour les limites inclusives et exclusives confond les lecteurs.

> *Éviter d'être vexé*:
> 1. Ecrire les fonctions d'aide `int clamp(int val, int low, int low)';
> 2. Gardez à l'esprit la matrice préfixe 1-basée;
> 3. Essai sur les petites matrices en premier (`[[1]]`, `[[1,2],[3,4]`).

### H2 – Algorithme Plongée profonde : 2-D Préfixe Sum Mécanique

Un préfixe 2-D est défini comme suit:

«» "
[j] = < i, c < j} mat[r]
«» "

La somme de toute sous-matrice `[r1, r2] × [c1, c2]` (inclus) est:

«» "
S = pref[r2+1][c2+1]
- préf[r1][c2+1]
- pref[r2+1][c1]
+ pref[r1][c1]
«» "

Parce que chaque terme ajoute ou soustrait des régions qui se chevauchent exactement une fois.

> *Pourquoi 1-basé? *
> Les décalages +1 permettent à la ligne/colonne «vide» («pref[0][*] = 0») d'agir en tant que cas de bord zéro, simplifiant.

- Oui. H2 – Conseils de mise en oeuvre pour l'entrevue d'embauche

Titre Justification
- Oui.
Utiliser `long` pour préfixer les sommes; lancer à la sortie `int` si le problème ne garantit pas de débordement. Autres
**Python**= Écrire la boucle de préfixe en une seule ligne, mais garder `row_sum` pour plus de clarté. Afficher la formule de requête `O(1)`. Autres
*C++ ** , Préférez `vecteur<vecteur<int>> sur les tableaux bruts; évitez les variables globales à moins d'être spécifiées. Autres
**Tout******Exposer votre idée d'abord**: Expliquez le concept de préfixe-somme verbalement avant de le coder. Cela démontre une pensée algorithmique. Autres

- Oui. H2 – Résumé de la complexité (tabulé)

L'approche du temps L'espace convient pour
- C'est quoi ?
Brute-Force: "O(m × n × k2)" "O(m × n)" Seulement si `k` est minuscule (`k < 5`). Autres
"O(m × n)". Autres
Fenêtre coulissante (alternative) (deux passes) (O(m × n)) (deux passes) (O(m × n))(=) Fonctionne si vous pouvez maintenir une somme de roulement par ligne. Autres

> * Conseil pro* :
> Afficher à la fois le code et un diagramme **mental** de la requête rectangle. Les aides visuelles impressionnent les intervieweurs.

- Oui. H2 – Réflexions finales : du problème au portefeuille

*Matrix Block Sum* est plus qu'un casse-tête de codage, c'est un micro-écosystème pour la programmation **dynamique**, **préfixe des sommes** et **comportement transfrontalier**.
La maîtrise vous donne :

- Confiance dans la transformation des boucles imbriquées en formules mathématiques.
- Un schéma réutilisable pour les futurs problèmes d'entrevue impliquant des sommes cumulatives 2-D.
- Un badge d'honneur : -Je peux résoudre les problèmes O(m × n) en quelques secondes. (en milliers de dollars)

> * Prêt à accepter votre prochaine entrevue de codage? *
> Pratiquez la solution préfixe-sum en Java, Python et C++. Déployez-le dans un entretien simulé chronométré, et regardez les recruteurs prendre note.

- Oui. H3 – Appel à l'action

> **Partager** votre mise en œuvre préférée dans les commentaires.
> **Télécharger** les extraits de code ci-dessus.
> **Abonnez-vous** pour plus de détails.

---

- Oui. H3 – À propos de l'auteur

> Un ingénieur logiciel expérimenté qui a autorisé des entretiens techniques à Google, Amazon et Microsoft.
> Passionné par les algorithmes propres et le mentorat de la prochaine génération de codeurs.
> Suivez sur LinkedIn: [@YourName](#)- Blog: [yourblog.com](#)

---

* Fin de l'article. *