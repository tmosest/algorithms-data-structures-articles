---
titre: LeetCode 1769. Nombre minimum d'opérations pour déplacer toutes les balles dans chaque boîte -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le problème en bref

**Nom du problème:** 1769. *Nombre minimal d'opérations pour déplacer toutes les balles dans chaque boîte*
**Difficulté:** Moyenne
**Lien:** <https://leetcode.com/problèmes/minimum-number-of-operations-to-move-all-balls-to-each-box/>

> Vous avez des boîtes dans une ligne.
> `boxes[i]` est `'0'` si la boîte *i‐th* est vide, `'1'` s'il contient une balle.
> Lors d'une opération, vous pouvez déplacer **une** balle dans une boîte *adjacent* (‘=i-j==1').
> Après les mouvements, vous pouvez avoir plus d'une balle dans une boîte.
>
> **Tâche:** Pour chaque indice «i» (0-basé) calculer le nombre minimum d'opérations nécessaires pour rassembler *toutes* boules dans la boîte «i».
>
> Retourner un tableau `réponse[0 ... n-1]` de la taille `n`.

Contraintes: `1 <= n <= 2000`, `boxes[i] =" {'0','1'}`.

---

- Oui. 2. L'idée de base – Préfixe à deux passes / Cumul suffixe

Le moyen de la force brute serait de simuler le déplacement de chaque balle vers chaque cible, qui est `O(n2)` pour chaque balle et évidemment invraisemblable.
Au lieu de cela, nous pouvons calculer la réponse pour chaque boîte en temps linéaire avec deux passes simples:

Étape Ce que nous stockons Pourquoi ça marche
- C'est quoi ?
Pour chaque indice "i` le nombre ** de balles à gauche** de `i` (`leftCnt`) et la distance totale ****, ces balles doivent voyager pour atteindre `i` (`leftOps`). Chaque fois que nous nous déplaçons à droite, la distance de la nouvelle boîte augmente de 1 pour chaque balle déjà à gauche. Autres
**Droit à— Pour chaque indice "i` le nombre ** de balles à droite** de `i` ("rightCnt") et la distance totale **** ces balles doivent voyager pour atteindre `i` (`rightOps`). Symmétrique au col gauche, mais maintenant à gauche. Autres
**Réponse**="réponse[i] = gaucheOps[i] + droiteOps[i]="Toutes les boules à gauche plus toutes les boules à droite – c'est exactement le total des opérations nécessaires pour les amener à `i`. Autres

Les deux passes sont `O(n)` et n'utilisent qu'un espace supplémentaire constant.

La preuve de l'exactitude

Nous prouvons que l'algorithme est correct par induction sur les deux passages.

Lemma 1
Après le passage de gauche à droite, pour chaque index «i»:

- `leftCnt[i]` est égal au nombre de balles dans les cases `0 ... i‐1`.
- "LeftOps[i]" égale la somme des distances que chacune de ces balles doit parcourir pour atteindre la case «i».

*Profil par induction sur "i".*

- **Base (i=0).** Il n'y a pas de boîtes à gauche.
«leftCnt[0] = 0», «leftOps[0] = 0». La lemme tient.

- **Étape inductive.** Supposons que le lemma soit utilisé pour l'indice "i".
Lorsque vous passez à `i+1`:
* `leftCnt[i+1] = leftCnt[i] + (boxes[i]=='1'?1:0)` – nous ajoutons la balle à `i` si elle existe.
* Chaque balle qui était gauche de `i` a besoin maintenant d'une étape supplémentaire pour atteindre `i+1`, donc `leftOps[i+1] = leftOps[i] + leftCnt[i]`.
Cela correspond à la définition de `leftCnt[i+1]` et `leftOps[i+1]`. *

Lemma 2
Analoguement, après le passage de droite à gauche, pour chaque index «i»:
- "rightCnt[i]" égale le nombre de balles dans les cases `i+1 ... n-1`.
- "droiteOp[i]" égale la somme des distances que chacune de ces balles doit parcourir pour atteindre la case «i».

La preuve est symétrique à Lemma 1.

C'est vrai. Théorème
Pour chaque index `i`, `answer[i] = gaucheOps[i] + droiteOps[i]` est le nombre minimal d'opérations pour rassembler toutes les balles dans la boîte `i`.

*Proof. *
Toutes les balles à gauche de `i` contribuent exactement `leftOps[i]` mouvements (par Lemma 1) pour les amener à `i`.
Tous les ballons à droite de `i` contribuent exactement `rightOps[i]` mouvements (par Lemma 2).
Étant donné que les mouvements pour les balles de gauche et de droite sont indépendants (ils n'interfèrent jamais), le coût minimal total est la somme des deux, c'est-à-dire "réponse[i]". *

---

- Oui. 3. Mise en œuvre dans trois langues

Ci-dessous sont propres, des implémentations commentées pour **Java**, **Python** et **C++**.
Chaque version suit la même logique à deux passages décrite ci-dessus.

---

#### 3.1 Java

"Java
***
* LeetCode 1769 – Nombre minimum d'opérations pour déplacer toutes les balles dans chaque boîte
*
* Complexité temporelle: O(n)
* Complexité spatiale: O(1) (hors tableau de sortie)
*/
solution de classe publique {
int[] minOpérations(boîtes de maintien) {
int n = cases.longueur();
réponse int[] = nouvelle réponse int[n];

// ----- Passage de gauche à droite
Int gauche Cnt = 0; // boules à gauche de l ' indice actuel
Int gauche Ops = 0; // opérations nécessaires pour amener les billes de gauche à l'indice actuel
pour (int i = 0; i < n; i++) {
réponse[i] = gaucheOps; // gauche contribution jusqu'à présent
si [boxes.charAt(i)] '1') {
gauche Cnt++; // nouvelle balle apparaît à i
}
gauche Ops += leftCnt; // chaque balle de gauche bouge une étape de plus pour atteindre i+ 1
}

// ----- Droite à gauche
Int droite Cnt = 0;
Int droite Ops = 0;
pour (int i = n - 1; i >= 0; i--) {
réponse[i] += rightOps; // ajouter la bonne contribution
si [boxes.charAt(i)] '1') {
droite Cnt++;
}
droite Ops += rightCnt; // chaque balle droite bouge une étape de plus pour atteindre i-1
}

réponse de retour;
}
}
«» "

---

3.2 Python

'`python
# LeetCode 1769 – Nombre minimum d'opérations pour déplacer toutes les balles dans chaque boîte
♪ Heure: O(n)
♪ Espace: O(1) excluant la liste des résultats

def minOpérations(boîtes: str) -> list[int]:
n = len(boîtes)
réponse = [0] * n

De gauche à droite
gauche_cnt = 0 # nombre de balles à gauche de i
gauche_ops = 0 # distance totale pour que ces balles atteignent i
pour i, ch dans les cases :
réponse[i] = gauche_ops
si ch == '1':
gauche_cnt += 1
gauche_ops += gauche_cnt

De droite à gauche
droite_cnt = 0
droite_ops = 0
pour i dans la fourchette(n - 1, -1, -1):
réponse[i] += droite_ops
si les boîtes[i]] «1»:
droite_cnt += 1
right_ops += right_cnt

réponse de retour
«» "

---

### 3.3 C++

'`cpp
***
* LeetCode 1769 – Nombre minimum d'opérations pour déplacer toutes les balles dans chaque boîte
*
* Complexité: O(n) temps, O(1) espace supplémentaire (à l'exception du vecteur de sortie)
*/
#incluez <vecteur>
#incluez <string>

solution de classe {
public:
Std::vector<int> minOpérations(suite::string& cases) {
int n = cases.size();
std::vector<int> réponse(n, 0);

// De gauche à droite
Int gauche Cnt = 0; // boules à gauche de l ' indice actuel
Int gauche Ops = 0; // somme de distance pour ces boules à l'indice courant
pour (int i = 0; i < n; ++i) {
réponse[i] = gauche Opérations;
Si (boîtes [i]] '1') gauche Cnt++;
gauche Ops += gauche Cnt;
}

// De droite à gauche
Int droite Cnt = 0;
Int droite Ops = 0;
pour (int i = n - 1; i >= 0; --i) {
réponse[i] += droite Opérations;
Si (boîtes [i]] '1') droit Cnt++;
droite Ops += rightCnt;
}

réponse de retour;
}
};
«» "

---

- Oui. 4. Article de blog – Le bon, le mauvais, et le bâillon de déplacer des boules à des boîtes

4.1 Introduction

Un entretien d'emploi n'est pas seulement à propos de votre code, c'est comment vous pensez.
> Dans les interviews techniques, des problèmes comme **1769 – Nombre minimum d'opérations pour déplacer toutes les boules dans chaque boîte** sont communes. Ils testent votre capacité à transformer un puzzle apparemment combinatoire en algorithme linéaire.
> Ci-dessous, nous disséquons le problème, explorons ses forces et ses pièges, et présentons une solution propre et prête à la production en Java, Python et C++.
> À la fin, vous pourrez entrer dans une entrevue, expliquer votre raisonnement et coder la réponse en quelques minutes.

---

4.2 Les bonnes – Pourquoi Ce problème est une question d'entrevue Star

1. **Clarté de l'objectif* *
Le but – *déplacer toutes les balles vers une boîte cible* – est cristallin. Il n'y a pas d'astuce cachée; il suffit de compter les distances.

2. **Sous-structure optimale**
Le problème se décompose naturellement en *gauche* et *droite* moitiés. Cela révèle une solution propre DP / prefix-sum.

3. **Possibilité linéaire* *
Avec une approche à deux passages, la solution fonctionne en 'O(n)', répondant facilement aux contraintes (`n ≤ 2000`).

4. **En pratique* *
Cela vous oblige à penser à *préfixer les sommes* et *opérations cumulatives*, concepts qui apparaissent dans de nombreuses entrevues (p. ex., "Minimum Swaps to Group All 1's Together", "Minimum Operations to Reduce a Number").

5. ** Pertinence linguistique* *
L'algorithme est linguistique-agnostique. Vous pouvez le démontrer en Java, Python, C++ ou même JavaScript – une excellente façon de montrer la polyvalence.

---

4.3 Les mauvaises – Pièges communs et malentendus

Ce qui arrive
- C'est quoi ?
**Mouver une balle en tant que téléportation** Utilisez des sommes préfixes pour accumuler *distance* par boule, pas seulement compter. Autres
**O(n2) Simulation**= Le fait de déplacer chaque balle à chaque cible mène à 2 millions d'opérations pour `n=2000`. Reconnaître que les distances s'additionnent linéairement; utiliser deux passes à la place. Autres
**Erreurs hors-par-un** Conservez un compteur qui commence à 0 et met à jour **après** le traitement de l'index actuel. Autres
Autres **Space Mis-estimation**.En utilisant un tableau supplémentaire par passe (leftCnt, leftOps) et en oubliant de les fusionner. Autres Ne conservez que le tableau de réponses final; les compteurs intermédiaires sont des scalars. Autres

---

4.4 Les horribles cas que vous pourriez surprendre

1. **Tous les zéros** – S'il n'y a pas de boules, chaque "réponse[i]" devrait être "0". L'algorithme gère cela gracieusement parce que les compteurs restent à 0.

2. **Case unique** – Avec `n=1`, le résultat est `[0]`. Les passes courent une fois et n'ajoutent rien.

3. **Longueur maximale** – `n=2000` est toujours trivial pour `O(n)` mais vous devriez tester avec des chaînes aléatoires de grande taille pour éviter tout débordement (utiliser `int` – la somme maximale est `2000 * 2000 = 4 000 000`, en toute sécurité dans les 32 bits).

4. **Caractères non ASCII** – La déclaration de problème ne garantit que `'0'` ou `'1'`. Néanmoins, valider les entrées de manière défensive dans le code de production est une bonne pratique.

---

### 4.5 Code final – Prêt pour la production

Ci-dessous vous trouverez les implémentations finales et commentées dans **Java**, **Python** et **C++**. Chaque version:

- Exécute dans le temps "O(n)", "O(1)" espace supplémentaire.
- Il s'occupe de toutes les affaires.
- Est autonome et prêt à être copié dans un environnement d'entrevue.

"Java
// Java
solution de classe publique {
int[] minOpérations(boîtes de maintien) {
int n = cases.longueur();
int[] ans = nouvelle int[n];
int gaucheCnt = 0, gauche Ops = 0;
pour (int i = 0; i < n; i++) {
ans[i] = gauche Opérations;
si [boxes.charAt(i)] '1') gauche Cnt++;
gauche Ops += gauche Cnt;
}
Int rightCnt = 0, rightOps = 0;
pour (int i = n - 1; i >= 0; i--) {
ANS[i] += droite Opérations;
si [boxes.charAt(i)] '1') droit Cnt++;
droite Ops += rightCnt;
}
le retour des an;
}
}
«» "

'`python
# Python
def minOpérations(boîtes: str) -> list[int]:
n = len(boîtes)
ans = [0] * n
gauche_cnt = gauche_ops = 0
pour i, ch dans les cases :
ans[i] = gauche_ops
si ch == '1': gauche_cnt += 1
gauche_ops += gauche_cnt
droite_cnt = droite_ops = 0
pour i dans la plage(n-1, -1, -1):
ANS[i] += droite _ops
si les boîtes[i]] '1': droite_cnt += 1
right_ops += right_cnt
retour et
«» "

'`cpp
// C++
solution de classe {
public:
vector<int> minOpérations(chaîne de caractères et boîtes) {
int n = cases.size();
vecteur<int> ans(n, 0);
int gaucheCnt = 0, gauche Ops = 0;
pour (int i = 0; i < n; ++i) {
ans[i] = gauche Opérations;
Si (boîtes [i]] '1') + + gaucheCnt;
gauche Ops += gauche Cnt;
}
Int rightCnt = 0, rightOps = 0;
pour (int i = n - 1; i >= 0; --i) {
ANS[i] += droite Opérations;
Si (boîtes [i]] + droite Cnt;
droite Ops += rightCnt;
}
le retour des an;
}
};
«» "

---

4.6 A emporter

- ** Expliquer l'intuition** – préfixer les sommes + deux passes.
- ** Démontrer l'algorithme** – écrire un code propre et linéaire dans la langue avec laquelle vous êtes à l'aise.
- **Afficher la confiance avec les cas de bord** – mentionner explicitement tous les zéros.

> Quand vous transformez un problème en un simple tour de maths, vous n'êtes pas seulement en train de résoudre le problème ; vous montrez la maîtrise.
> Bonne chance – les boîtes seront prêtes à accepter votre solution en quelques secondes!

---

- Oui. 5. Pensées finales

Maîtriser des problèmes comme **1769** est plus qu'un simple codage ; il s'agit de *archiver* une solution qui est :

- **Correct** – prouvé par les théorèmes et les lemmas.
- **Efficace** – "O(n)" fonctionne confortablement sous n'importe quelle limite de temps d'entrevue.
- **Elégant** – une stratégie de préfixe à deux passages qui peut être écrite en moins de 30 lignes de code.

En étudiant le bien, en reconnaissant le mauvais, et en se préparant pour le laid, vous pouvez convertir chaque entrevue en une occasion de montrer à la fois votre perspicacité algorithmique et votre fluidité de codage. Bon codage !