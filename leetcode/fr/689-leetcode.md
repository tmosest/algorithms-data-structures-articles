---
Titre: LeetCode 689. Somme maximale de 3 sous-tribus sans recouvrement -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
C'est pas vrai. La somme maximale de 3 subarrases sans recouvrement – LeetCode 689
*(Hard – 73 % des soumissions ont battu ça – une question d'interview parfaite pour un rôle d'ingénierie logicielle)*

Code de la langue
C'est quoi, ça ?
**Java** Afficher </résumé> ... </détails>
*Python *Détails *<résumé > Afficher </résumé> ... </détails>
**C++** Afficher </résumé> ... </détails>

> *Vous voulez décrocher votre prochain emploi? Écrivez la solution, expliquez le truc et partagez-la sur LinkedIn ou votre portfolio. C'est exactement ce qu'il s'agit de ce billet – une plongée profonde, une solution prête à la copie, et un article de blog poli qui est convivial pour le référencement et prêt à l'entrevue. *

---

Récapitulation des problèmes

> **Input**
> `nums`: `int[]` – 1 ≤ longueur nominale ≤ 2 × 104
> `k`: longueur de chaque sous-aire (1 ≤ k ≤ plancher(nums.longueur/3))
> ** Sortie**
> `int[3]` – les indices de départ des trois subdivisions *non-overlaping* de longueur `k` qui donnent la somme totale maximale.
> Si plusieurs triples donnent la même somme, retournez le **lexicographiquement le plus petit**.

> **Exemple**
> `nums = [1,2,1,2,6,7,5,1], k = 2 → [0,3]`

> Explication: sous-ensembles `[1,2]`, `[2,6]`, `[7,5]` somme à 18, le maximum possible.

---

- Oui. Stratégie de haut niveau (le «bien»)

1. **Fenêtre coulissante** – calculez la somme de chaque sous-aire de longueur `k`.
*`subSum[i]` = somme de `nums[i .. i+k-1]»
Temps O(n), espace O(n).

2. **Précalculer les meilleurs indices de gauche/droite**
* `bestLeft[i]` – indice de la sous-somme *maximum* du préfixe `[0 .. i]`.
* `bestRight[i]` – indice du sous-somme *maximum* dans le suffixe «[i .. n-k]».
Pour les liens, nous conservons l'indice le plus précoce (lexicographiquement le plus petit).

3. **Essayez chaque sous-cours moyen possible**
Pour le début intermédiaire `m` (doit satisfaire `k ≤ m ≤ n-2k`):
«» "
gauche = bestLeft[m - k]
droite = meilleur Droite[m + k]
total = subSum[gauche] + subSum[m] + subSum[droite]
«» "
Gardez le triple avec le plus grand "total".
Si les liens `total`, l'ordre lexicographique est automatiquement géré par la construction de `bestLeft/right`.

L'algorithme entier est **O(n) temps, O(n) espace** – le meilleur possible pour ce problème.

---

## 4--D'une promenade détaillée (le "Bad" & "Ugly")

Pourquoi ça va mal
- C'est quoi ?
**Naïve O(n3)**=Énumérer tous les triples → trop lents (n jusqu'à 20 000). Autres Utilisez la fenêtre coulissante + les meilleurs indices précalculés. Autres
**Le double comptage se chevauche**=Le milieu `m` doit laisser des fentes `k` de chaque côté. Iterate `m` de `k` à `n-2k`. Autres
**Cravates cassées incorrectement** Dans `BestLeft`, lorsque les sommes sont liées, conservez l'indice *plus petit*; de même dans `BestRight`. Autres
**La longueur « subSum » est « n-k+1 ». Repères d'index soigneusement: `subSum[i]` correspond au début `i`. Autres
**Les cas d'Edge**="nums.longueur== 3k` – un seul triple possible. Les boucles s'en occupent naturellement; assurez-vous que les indices sont dans les limites. Autres
**Grands nombres**= Somme allant jusqu'à 2 × 104 éléments, chacun < 216 → correspond à int.= Utiliser `int` en Java/C++, `int` en Python (précision arbitraire). Autres
**Déchets de mémoire**=L'entreposage complet du sous-sum est nécessaire pour les recherches O(1). Accepter l'espace O(n) ; les contraintes le permettent. Autres

---

Mise en œuvre du code

> **Note**: Les trois solutions utilisent l'idée algorithmique * même* – seulement des changements de syntaxe.

### 5.1 Java (style LeetCode)

"Java
// 689. Somme maximale de 3 sous-découpages
solution de classe {
Int[] maxSumOfThreeSubarrays(int[] nums, int k) {
int n = longueur nums;
si (n < 3 * k) retourne une nouvelle int[0];

// 1. Calculer les sommes de tous les sous-réseaux de longueur k
Int numSub = n - k + 1;
int[] subSum = nouveau int[numSub];
= 0;
pour (int i = 0; i < k; i++) somme += nombres[i];
subSum[0] = somme;
pour (int i = k; i < n; i++) {
somme += nombres[i] - les nombres [i - k];
sous-Sum[i - k + 1] = somme;
}

// 2. bestLeft[i] – indice avec la somme maximale en [0..i]
int[] bestLeft = nouveau int[numSub];
bestLeft[0] = 0;
pour (int i = 1; i < numSub; i++) {
si (sous-sum[i] > sous-sum[meilleur Gauche[i - 1]]) {
bestLeft[i] = i;
} autre {
bestLeft[i] = bestLeft[i - 1];
}
}

// 3. bestRight[i] – indice avec la somme maximale en [i..end]
int[] bestRight = nouveau int[numSub];
le meilleur Droite[num] Sous - 1] = nombre Sous-alinéa 1;
pour (int i = numSub - 2; i >= 0; i--) {
si (sous-Sum[i] >= sous-Sum[bestRight[i + 1]]) {
bestRight[i] = i;
} autre {
bestRight[i] = bestRight[i + 1];
}
}

// 4. Essayez chaque sous-cours du milieu
int[] best = nouveau int[3];
bestTotal = -1;
pour (int m = k; m <= numSub - k - 1; m++) {
int gauche = bestLeft[m - k];
int droite = meilleur Droite[m + k];
int total = subSum[gauche] + subSum[m] + subSum[droite];
si (total > le meilleurTotal) {
bestTotal = total;
best[0] = gauche;
meilleure[1] = m;
meilleure[2] = droite;
}
}
le meilleur retour;
}
}
«» "

#### 5.2 Python 3

'`python
# 689. Somme maximale de 3 sous-tribus sans recouvrement
Solution de classe:
def maxSumOfThreeSubarrays(self, nombres: list[int], k: int) -> list[int]:
n = len(nums)
si n < 3 * k:
retour []

1. Montants de la sous-tribu
num_sub = n - k + 1
sub_sum = [0] * num_sub
cr = somme(nums[:k])
sub_sum[0] = curr
pour i dans la plage (k, n):
pour += nombres[i] - les noms [i - k]
sub_sum[i - k + 1] = courbure

# 2. mieux à gauche
best_left = [0] * num_sub
pour i dans range(1, num_sub):
if sub_sum[i] > sub_sum[best_left[i - 1]]:
best_left[i] = i
Sinon:
best_left[i] = best_left[i - 1]

# 3. meilleur droit
best_right = [0] * num_sub
best_right[-1] = num_sub - 1
pour i dans l'intervalle (num_sub - 2, -1, -1):
si sub_sum[i] >= sub_sum[best_right[i + 1]]:
best_right[i] = i
Sinon:
best_right[i] = best_right[i + 1]

3. boucle du candidat moyen
meilleure = [0, 0, 0]
best_total = -1
pour m dans la plage(k, num_sub - k):
l = best_left[m - k]
r = best_right[m + k]
total = sous_sum[l] + sous_sum[m] + sous_sum[r]
si total > best_total:
best_total = total
best = [l, m, r]

le meilleur retour
«» "

#### 5.3 C++ (17)

'`cpp
// 689. Somme maximale de 3 sous-découpages
solution de classe {
public:
vector<int> maxSumOfThreeSubarrays(vecteur<int>& nums, int k) {
int n = nombres.size();
si (n < 3 * k) retourner {};

// 1. sommes accessoires
Int numSub = n - k + 1;
vecteur<int> subSum(numSub);
= 0;
pour (int i = 0; i < k; ++i) somme += nombres[i];
subSum[0] = somme;
pour (int i = k; i < n; ++i) {
somme += nombres[i] - les nombres [i - k];
sous-Sum[i - k + 1] = somme;
}

// 2. mieux à gauche
vector<int> bestLeft(numSub);
bestLeft[0] = 0;
pour (int i = 1; i < numSub; ++i)
bestLeft[i] = sous-Sum[i] > sous-Sum[meilleur Gauche[i - 1] ? i : bestLeft[i - 1];

// 3. meilleur droit
vector<int> bestRight(numSub);
le meilleur Droite[num] Sous - 1] = nombre Sous-alinéa 1;
pour (int i = numSub - 2; i >= 0; --i)
bestRight[i] = subSum[i] >= subSum[bestRight[i + 1]] ? i : bestRight[i + 1];

// 4. boucle intermédiaire
vecteur <int> ans(3);
bestTotal = -1;
pour (int m = k; m <= numSub - k - 1; ++m) {
int l = bestLeft[m - k];
int r = meilleurdroit[m + k];
int total = subSum[l] + subSum[m] + subSum[r];
si (total > le meilleurTotal) {
bestTotal = total;
as = {l, m, r};
}
}
le retour des an;
}
};
«» "

---

## 6--Écrire un billet de blog gagnant – SEO & Interview Ready

Vous trouverez ci-dessous un article prêt à publier qui utilise des rubriques riches, des sections de mots clés, des captures d'écran de code et des conseils pratiques d'entrevue. Copiez-le dans Medium, Dev.to ou votre propre blog technologique. Étiquetez-la avec *LeetCode 689*, *interview d'emploi*, *ingénierie logicielle*, *codage défi* et regardez le trafic croître.

> **Pro‐Tip**: Ajouter un *Essayez-le vous-même** extrait interactif (par exemple, intégrer sur GitHub Gist ou CodePen) afin que les recruteurs puissent exécuter la solution instantanément.

---

6.1 Aperçu du blog

Section Objet
C'est pas vrai.
**Headline**=Prenez attention & incluez le numéro de problème LeetCode. Autres
**Récapitulatif du problème** Autres
Autres **Take-aways clés**= Énumérez le *pourquoi* ce problème est important dans les entrevues. Autres
**Algorithme Explication étape par étape (y compris un diagramme de flux). Autres
**Code**= Mettre en évidence la logique fondamentale dans une langue de choix. Autres
**Analyse de la complexité**= Montrez pourquoi O(n) bat toutes les autres approches. Autres
**Pièges communs**= Montrez ce que les intervieweurs aiment vous entendre éviter. Autres
Autres **Edge-Case Checklist**= Réassurer les recruteurs que vous comprenez les contraintes. Autres
**Conseils sur le rendement**= Discutez des facteurs constants, comment optimiser les 'Arrays.fill' de Java, etc. Autres
**La pensée finale**=Encourager la pratique sur LeetCode, le partage sur LinkedIn, la construction d'un portefeuille. Autres
**Call‐to‐Action**=Téléchargez le code=, #Appliquer maintenant=, #Partager vos propres solutions=. Autres

---

Article complet

> (Copier-coller dans Medium ou votre propre blog – vous pouvez même ajouter une image de héros d'un arbre binaire ou d'animation de fenêtre coulissante.)

```markdown
Code de Leet 689 : Somme maximale de 3 substituts sans recouvrement – un guide complet
*Problème d'entretien difficile, 73 % des solutions l'ont battu, parfait pour votre prochain entretien d'ingénierie logicielle. *

---

Déclaration du problème

> **Objectif**: Trouver trois sous-partages de longueur égale `k` dans un tableau `nums` qui maximisent la somme totale.
> **Retour** : Les trois indices de départ, lexicographiquement plus petits sur les liens.

> Contraintes:
> 1 ≤ longueur nominale ≤ 20 000
> 1 ≤ k ≤ plancher(longueur en chiffres/3)
> * Chaque élément < 216

> **Pourquoi c'est important**:
> * Nécessite une fenêtre coulissante + une programmation dynamique en un seul passage.
> * Démontre une compréhension profonde des compromis temps/espace – un must-know pour le codage des entrevues à Google, Amazon, Microsoft, Stripe, etc.

---

## Đ Aperçu de haut niveau – L'approche « Bonne »

1. **Fenêtre coulissante**
* Calculez chaque somme de sous-tarifs en temps linéaire. *
«» "
subSum[i] = somme(nums[i ... i+k-1])
«» "
Complexité: **O(n)**.

2. **Préfixe / suffixe Indices Max**
* `bestLeft[i]` – l'indice du "subSum` maximal dans `[0 ... i]` (le plus avancé sur les liens).
* `bestRight[i]` – l'indice du maximum `subSum` dans `[i ... fin]` (derniers sur les liens – mais nous choisissons le plus tôt* quand nous construisons).

Ces tableaux nous font connaître instantanément *le meilleur candidat de gauche* et *le meilleur candidat de droite* pour toute sous-audience du milieu.

3. **Énumérer le sous-réseau moyen**
*Le début intermédiaire `m` doit laisser des fentes `k` de chaque côté → `k ≤ m ≤ n-2k`. *
Calculer la somme totale pour `left = bestLeft[m-k]`, `right = best Oui.
Gardez le triple avec le plus grand total; les liens sont automatiquement résolus parce que nous utilisons toujours les premiers indices.

> Résultat : **O(n)** temps, **O(n)** espace – le meilleur pour ce problème.

---

Code – Java / Python / C++

> *Sentez libre de copier les extraits ci-dessous dans votre propre IDE ou LeetCode test runner. *

"Java
// 689. Somme maximale de 3 sous-découpages
solution de classe {
Int[] maxSumOfThreeSubarrays(int[] nums, int k) {
int n = longueur nums;
si (n < 3 * k) retourne une nouvelle int[0];

Int numSub = n - k + 1;
int[] subSum = nouveau int[numSub];
= 0;
pour (int i = 0; i < k; i++) somme += nombres[i];
subSum[0] = somme;
pour (int i = k; i < n; i++) {
somme += nombres[i] - les nombres [i - k];
sous-Sum[i - k + 1] = somme;
}

int[] bestLeft = nouveau int[numSub];
bestLeft[0] = 0;
pour (int i = 1; i < numSub; i++)
bestLeft[i] = subSum[i] > subSum[bestLeft[i-1]] ? i : bestLeft[i-1];

int[] bestRight = nouveau int[numSub];
bestRight[numSub-1] = numSub-1;
pour (int i = numSub-2; i >= 0; i--)
bestRight[i] = subSum[i] >= subSum[bestRight[i+1]] ? i : bestRight[i+1];

int[] ans = nouveau int[3];
bestTotal = -1;
pour (int m = k; m <= numSub - k - 1; m++) {
int l = bestLeft[m - k];
int r = meilleurdroit[m + k];
int total = subSum[l] + subSum[m] + subSum[r];
si (total > le meilleurTotal) {
bestTotal = total;
ans = nouvelle int[]{l, m, r};
}
}
le retour des an;
}
}
«» "

'`python
# 689. Somme maximale de 3 sous-tribus sans recouvrement
Solution de classe:
def maxSumOfThreeSubarrays(self, nombres: List[int], k: int) -> Liste[int]:
n = len(nums)
si n < 3 * k: retour []

num_sub = n - k + 1
sub_sum = [0] * num_sub
cur = somme(nombres[:k])
sub_sum[0] = cur
pour i dans la plage (k, n):
Nombres d'unités - les noms
sub_sum[i-k+1] = cur

best_left = [0] * num_sub
pour i dans range(1, num_sub):
best_left[i] = i si sub_sum[i] > sub_sum[best_left[i-1]] autre best_left[i-1]

best_right = [0] * num_sub
best_right[-1] = num_sub-1
pour i dans range(num_sub-2, -1, -1):
best_right[i] = i si sub_sum[i] >= sub_sum[best_right[i+1]]

meilleure = [0,00]
best_total = -1
pour m dans la plage(k, num_sub - k):
l, r = best_left[m-k], best_right[m+k]
total = sous_sum[l] + sous_sum[m] + sous_sum[r]
si total > best_total:
best_total = total
best = [l, m, r]
le meilleur retour
«» "

'`cpp
// 689. Somme maximale de 3 sous-découpages
solution de classe {
public:
vector<int> maxSumOfThreeSubarrays(vecteur<int>& nums, int k) {
int n = nombres.size();
si (n < 3*k) retourne {};

int numSub = n-k+1;
vecteur<int> subSum(numSub);
int s=0; pour(int i=0;i<k;i++) s+=nums[i];
sous-sum[0]=s;
pour(int i=k;i<n;i++){
s+=nums[i]-nums[i-k];
sous-Sum[i-k+1]=s;
}

vector<int> bestLeft(numSub);
bestLeft[0]=0;
pour(int i=1;i<numSub;i++)
bestLeft[i]=subSum[i]>subSum[bestLeft[i-1]]?i:bestLeft[i-1];

vector<int> bestRight(numSub);
bestRight[numSub-1]=numSub-1;
pour(int i=numSub-2;i>=0;--i)
bestRight[i]=subSum[i]>=subSum[bestRight[i+1]]?i:bestRight[i+1];

vecteur <int> ans(3);
int mieux Total = 1;
Pour(int m=k;m<=numSub-k-1;m++){
int l=bestLeft[m-k], r=best Droite[m+k];
int total=subSum[l]+subSum[m]+subSum[r];
if(total>meilleurtotal){
le meilleur Total = total;
as={l,m,r};
}
}
le retour des an;
}
};
«» "

---

Décomposition

Étape Temps Espace
C'est pas vrai.
Fenêtre coulissante **O(n)** Autres
Préfixe / suffixe max. **O(n)** Autres
L'espace supplémentaire constant

Total : **Heure O(n)**, **Espace O(n)**.
Toutes les autres solutions naïves (double ou triple boucles imbriquées) seraient **O(n3)**, ce qui est *impossible* pour `n = 20 000`.

---

## Comment les éviter

Pourquoi les recruteurs s'occupent-ils?
- C'est quoi ?
Autres En utilisant deux boucles pour le préfixe et suffixe mais *recomptage* sub-array sums. Autres
Ne pas manipuler correctement la rupture de l'attache. Autres
(en milliers de francs suisses) Défauts sur les cas de bord court. Autres
À l'aide d'un trop-plein d'int 32 bits (dans des langues comme C++) Autres
Négligence `n < 3k` check. Autres

---

Liste de contrôle des cas de bord

- `nums` longueur exactement `3k` → un seul triple possible.
- `k = 1` → trivial, il suffit de choisir trois éléments maximum sans adjacence.
- `nums` tous les zéros → doivent retourner `[0, 1, 2]` (lexicographiquement plus petit).
- `k` égale `floor(n/3)` → seulement un ou deux placements possibles.

Testez-les avant de poster.

---

Conseils de performance

Langue
- Oui.
Utiliser `Arrays.fill` pour initialiser les tableaux si vous avez besoin de grandes valeurs par défaut. Évitez les requêtes `HashMap` – nous utilisons des tableaux simples. Autres
**Python**=Utilisez parcimonieusement la compréhension des listes; les boucles sont assez rapides. Autres
Utiliser `std::vector<int>` avec `reserve` pour éviter les réaffectations. Utiliser `std::max_element` si vous préférez la lisibilité, mais la boucle manuelle est légèrement plus rapide. Autres

---

La dernière pensée et appel à l'action

LeetCode 689 a été résolu en Java, Python et C++ et publié sur GitHub. J'ai également partagé ma solution sur LinkedIn et j'ai reçu des interviews de Google et Stripe.

> Si vous vous préparez à une entrevue de codage, pratiquez ce problème *par jour*. Ajoutez la solution à votre portfolio, écrivez un billet de blog ou créez une courte vidéo expliquant l'algorithme. Les recruteurs remarquent quand les candidats *prouvent* leurs compétences en résolution de problèmes, pas seulement *parlent* à leur sujet.

---

Télécharger la solution complète (toutes langues confondues) → [GitHub Gist](https://gist.github.com/votre nom d'utilisateur/leetcode-689)

Vous voulez discuter d'autres défis LeetCode ? Laissez un commentaire ou DM moi sur LinkedIn.

> * Prêt à casser votre prochain entretien ? Laissez-nous coder, partager et être embauchés ! *
«» "

---

6.3 Améliorations visuelles

Comment ajouter
C'est pas vrai.
**Diagramme de fenêtre coulissante**= Utiliser un SVG ou PNG qui montre une fenêtre mobile sur le tableau. Autres
**Surlignement syntaxique du code**= Utiliser des blocs de code balisage; Surlignement automatique moyen. Autres
Autres **Edge‐Case Table**=Utilisez un tableau à balisage pour une référence rapide. Autres
**Lien avec la repo de GitHub**= Fournissez un lien avec une repo avec les trois implémentations linguistiques. Autres

---

Prochaines étapes pour vous

1. **Run le code** – collez les extraits dans votre IDE préféré.
2. **Champs d'essai** – par exemple, «nums=[1,2,3,3,4,5,6,7,8,9], k=3».
3. **Publier** – copier l'article dans Medium/Dev.to avec les étiquettes pertinentes.
4. **Partager** – poste sur Linked Dans avec un commentaire: LeetCode 689 en Java, se sentent prêts pour la prochaine interview de codage!
5. **Appliquer** – utilisez la conversation comme point de discussion dans votre prochaine entrevue.

---

> **Codage heureux & bonne chance lors de votre prochaine interview!**
«» "

---

C'est tout ! Vous avez maintenant la solution complète*, l'analyse de l'espace-temps*, les pièges communs*, et un article riche en référencement. Déposez ceci dans votre portfolio, continuez à pratiquer, et vous atterrissez ce rôle d'ingénierie logicielle plus rapidement que vous pouvez le dire.

Bon codage ! (en milliers de dollars)
«» "

---

> **Meta‐Note**: Si vous utilisez l'article sur Medium, définissez le temps de lecture** à environ 7–8 minutes pour correspondre aux messages de solution LeetCode typiques, et ajoutez une section **.

---

- Oui. Comment partager sur LinkedIn

Texte
( ) Problème : LeetCode 689 – Somme maximale de 3 substituts non-overlaping
Solution : passe linéaire O(n) + indices de préfixe/suffixe max
( ) Langues: Java, Python, C++
( ) Consultez le code complet et le chemin parcouru : https://github.com/votre nom d'utilisateur/leetcode-689
C'est vrai. Laissez-nous discuter comment cela démontre la fenêtre coulissante + la maîtrise DP! #leetcode #interviewprep #logicielingénierie
«» "

Déposer le lien vers votre GitHub ou le blog. Les recruteurs adorent voir le code réel, et le hashtag de discussion fera apparaître votre profil aux gestionnaires d'embauche.

---

routine de pratique hebdomadaire

1. **Jour 1** – Lisez le problème et écrivez l'algorithme sur papier.
2. **Jour 2** – Mettre en œuvre dans une langue, sur des exemples de cas.
3. **Jour 3** – Ajouter les essais de cas de bord (`n = 3k`, tous les zéros, grand `k`).
4. **Jour 4** – Écrire un billet de blog ou une vidéo expliquant la solution.
5. **Jour 5** – Partagez sur les réseaux sociaux, engagez-vous avec les commentaires.
6. **Jour 6** – Examiner d'autres solutions ou soumettre au juge en ligne.
7. **Jour 7** – Réfléchir aux erreurs et affiner votre code.

Répétez avec un nouveau problème LeetCode.

---

**Et c'est un guide complet** de l'algorithme à l'affichage, vous assurant de bénéficier pleinement de la solution et de l'exposition aux recruteurs.

Bonne chance et profitez de votre préparation d'entrevue! C'est ce qu'il a dit.

---

* Sentez-vous libre d'adapter l'article, le code et les messages de médias sociaux pour s'adapter à votre propre style et marque. *