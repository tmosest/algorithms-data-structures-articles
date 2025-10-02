---
titre: LeetCode 229. Élément de majorité II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Élément majoritaire 3-Way – 229. Élément majoritaire II
Référence rapide
Langage Temps Espace Complexité Lien vers LeetCode
-- -- -- -- -- -- -- -- -- -- -- -- -- --
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres
**Python**=O(n)=O(1)=O(n)=https://leetcode.com/problèmes/majority-element-ii/ Autres
*C++ * O(n) * O(1) * O(n) * https://leetcode.com/problèmes/majority-element-ii/ Autres

> **Objectif** – Retourner chaque nombre qui apparaît **plus que** *n* / 3 fois.

> **Pourquoi ça compte** – C'est le problème d'entrevue classique qui teste votre capacité à penser au vote *Boyer-Moore*, aux algorithmes *d'espace constant* et aux astuces *de temps linéaire*. C'est une vitrine parfaite pour un candidat qui peut écrire un code propre et efficace en plusieurs langues.

---

- Oui. 2. Code – Java / Python / C++

> *Les trois implémentations utilisent l'algorithme Boyer-Moore étendu (également appelé version "candidate" de la version "Candidate"). *

### 2.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<entier> majoritéÉlément(int[] nombres) {
int candidate1 = 0, candidate2 = 1; // valeurs arbitraires distinctes
nombre int1 = 0, nombre2 = 0;

// 1er passage – trouver des candidats possibles
pour (int num : nombres) {
si (nom du candidat) {
nombre1++;
} sinon si (num == candidat2) {
nombre2++;
} sinon si (compte 1 == 0) {
candidat1 = nombre;
nombre1 = 1;
} sinon si (compte 2 == 0) {
candidat2 = nombre;
nombre2 = 1;
} autre {
count1--;
nombre2--;
}
}

// 2ème passe – vérifier les candidats
nombre1 = 0; nombre2 = 0;
pour (int num : nombres) {
si (num == candidat1) count1++;
sinon si (num == candidat2) count2++;
}

Liste du résultat <entier> = nouvelle liste de distribution<>();
int n = longueur nums;
si (compte 1 > n / 3) résultat.add(candidate1);
si (compte2 > n / 3) résultat.add(candidate2);
le résultat du retour;
}
}
«» "

2.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def majorité Élément(même, nombres: Liste[int]) -> Liste[int]:
# 1er laissez-passer – recherche de candidat
cand1, cand2 = 0, 1 # valeurs de départ arbitraires distinctes
nombre1, nombre2 = 0, 0

pour num in nums:
si num == cand1:
nombre1 += 1
elif num == cand2:
nombre2 += 1
nombre d'élifs1 == 0:
cand1, count1 = nombre, 1
nombre d'élifs2== 0:
cand2, count2 = num, 1
Sinon:
nombre1 -= 1
nombre2 -= 1

# 2ème passe – vérification
nombre1 = nombre2 = 0
pour num in nums:
si num == cand1:
nombre1 += 1
elif num == cand2:
nombre2 += 1

res = []
n = len(nums)
si nombre1 > n // 3:
res.append(cand1)
si nombre2 > n // 3:
res.append(cand2)
retour res
«» "

C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
std::vector<int> majorityElement(std::vector<int>& nums) {
int cand1 = 0, cand2 = 1; //
nombre int1 = 0, nombre2 = 0;

// Premier passage : trouver des candidats potentiels
pour (int num : nombres) {
si (num == cand1) count1++;
sinon si (num == cand2) count2++;
Sinon, si (compte 1 == 0) { cand1 = num; nombre1 = 1; }
Sinon, si (compte 2) 0) { cand2 = num; nombre2 = 1; }
autres { nombre1--; nombre2--; }
}

// Deuxième passe : vérifier le nombre
nombre1 = nombre2 = 0;
pour (int num : nombres) {
si (num == cand1) count1++;
sinon si (num == cand2) count2++;
}

std::vector<int> résultat;
int n = nombres.size();
si (count1 > n / 3) result.push_back(cand1);
si (count2 > n / 3) result.push_back(cand2);
le résultat du retour;
}
};
«» "

---

- Oui. 3. Article du blog – Élément II majeur : le bon, le mauvais et le mauvais

> **Méta-Description**: Master LeetCode 229 – Élément majoritaire II. Apprenez l'algorithme optimal O(n) / O(1), voyez les implémentations Java, Python et C++, et comprenez les pièges qui peuvent faire monter les intervieweurs. Parfait pour les chercheurs d'emploi en ingénierie logicielle.

3.1 Introduction

Si vous avez frappé LeetCode 229 dans votre prép d'interview, vous avez probablement regardé l'énoncé de problème, a imaginé une solution *hash map*, et s'est demandé pourquoi l'intervieweur continue de demander le temps linéaire et l'espace constant. (en milliers de dollars)
Majorité L'élément II n'est pas juste un autre problème de comptage – c'est un test de votre intuition algorithmique. Dans cet article, nous disséquerons l'algorithme optimal, l'algorithme naïf, et l'algorithme des cas. En chemin, vous verrez le code Java, Python et C++ prêt à copier que vous pouvez coller dans votre carnet d'entretien.

> **Pourquoi est-ce important pour votre carrière? **
> – Les intervieweurs aiment des solutions concises et efficaces dans l'espace.
> – Démontre la maîtrise des algorithmes classiques (Boyer-Moore).
> – Montrez que vous pouvez traduire des idées en plusieurs langues, une compétence essentielle pour les ingénieurs à fond.

3.2 Récapitulation du problème

> **Don** un tableau entier "nums" de taille "n".
> **Retour** tous les éléments qui apparaissent plus de 3 fois.
> **Contrairements**: 1 ≤ *n* ≤ 5 × 104,..

> **Observations**:
> * Au plus **deux** nombres peuvent satisfaire à la valeur de 3 parce que 3 × (n/3) = n.
> * Il s'agit d'une extension naturelle du problème classique de l'élément Majorité (n/2).

3.3 L'approche naïve – Hash Map

Étape Opération Complexité
- C'est quoi ?
Autres Fréquences de comptage `Map<entier, Integer>''O(n) temps, O(n) espace
Rechercher une carte itérer O(n) time

"Java
Carte<integer, integer> freq = nouveau HashMap<>();
pour (int num : nums) freq.put(num, freq.getOrDefault(num, 0) + 1);
Liste <Integer> res = nouvelle liste de distribution<>();
pour (Map.Entry<Integer, Integer> e : freq.entrySet())
si (e.getValue() > n / 3) res.add(e.getKey());
«» "

**Pourquoi c'est mauvais pour les interviews* *
* Utilise une mémoire supplémentaire – *O(n)*.
* LeetCode=1 demande explicitement de l'espace O(1).
* Il ne présente pas une pensée algorithmique plus profonde.

3.4 Le bon – le plus grand – vote libre (prorogé)

3.4.1 Intuition

1. ** Sélection des candidats** – Nous pouvons suivre au plus deux candidats (`cand1`, `cand2`) et leurs 'votes' (`cnt1`, `cnt2`).
2. **Élimination du vote** – Chaque fois qu'un nouveau nombre ne correspond pas à l'un ou l'autre candidat et que les deux compteurs sont positifs, nous décrémentons les deux.
3. **Proof** – Si un nombre se produit > n/3 fois, il ne peut pas être complètement éliminé parce que chaque élimination supprime deux nombres, et la majorité doit survivre.

3.4.2 Deux passes

* **Pass 1** – Trouver les deux candidats majoritaires potentiels.
* **Pass 2** – Comptez leurs vrais événements pour confirmer s'ils franchissent effectivement le seuil.

Pourquoi O(1) Espace ?

On ne garde jamais toute la carte de fréquence. Seulement deux variables candidates et deux compteurs – quatre entiers. La mémoire reste constante quelle que soit la taille de l'entrée.

3.4.4 Cas de bord & Gotchas

Cas de bord Ce qu'il faut faire attention
Ce n'est pas le cas.
La longueur de l'array peut être la même que pour le seul élément. Initialiser les candidats à des valeurs distinctes (`0`, `1`) avant la boucle. Autres
Autres Tous les éléments mêmes.Les compteurs ne décrémenteront pas, toujours correct. Autres
Nombres négatifs Aucune différence – juste des comparaisons. Autres

3.4.5 Extraits de mise en œuvre

> **Java** – voir le code ci-dessus.
> **Python** – voir le code ci-dessus.
> **C++** – voir le code ci-dessus.

Tous les trois suivent la même logique, de sorte que vous pouvez facilement changer les langues sur place.

#### 3.5 L'horrible – Erreurs courantes

1. **En supposant que l'algorithme fonctionne pour n/2** – Pour `n/3`, vous avez seulement besoin de **deux** candidats, pas un.
2. **Passer la deuxième carte de validation** – La première passe ne garantit que *les candidats possibles* ; vous devez les vérifier.
3. **Utilisation `>` au lieu de `>=`** – Le problème dit explicitement plus de n/3.
4. **Initialiser les deux candidats à la même valeur** – Si vous commencez par `cand1 = cand2 = 0`, l'algorithme peut se tromper lorsque le tableau ne contient que des zéros.
5. **Omettre la chaîne "else if"** – Le mélange des conditions peut conduire à des mises à jour incorrectes du compteur.

3.6 Essais et cas de bord

Autres Test d'entrée prévu Pourquoi
C'est pas vrai.
Élément unique
Autres Deux "[1,2]`[1,2]` Tous les deux 1 > 2/3? Non → les deux 1/2 > 2/3? En fait, 1 > 0. Les deux apparaissent > n/3 ( )
Autres Aucun élément > 4/3
Autres Grande entrée: 5 × 104 nombres aléatoires: O(n) runtime, mémoire constante: Test de stress:

3.7 Variations et extensions

* **k-majority** – Généraliser jusqu'à <> n/k= en utilisant des candidats `k-1`.
* **Streaming data** – Le même algorithme fonctionne sur un flux de données: garder les compteurs, jeter au fur et à mesure que vous allez.
* **Parallélisme** – Split tableau, exécuter Boyer-Moore localement, fusionner les candidats.

3.8 Conclusion – Ce que les intervieweurs recherchent vraiment

Trait de preuve dans votre solution
- C'est quoi ?
**Profondeur algorithmique**
Autres **Efficacité de l'espace**
**Robustness**
**Qualité du code**
**La communication peut expliquer le raisonnement en 30 secondes

** Conseil professionnel :** Après le codage, répéter une explication de 30 secondes : Nous gardons deux candidats, décrément quand un nouvel élément entre en jeu, puis vérifions les comptes. (en milliers de dollars)

###3.9 Appel à l'action

> ** Prêt à accepter votre prochaine entrevue de codage? * *
> Copiez les extraits de Java/Python/C++ ci-dessus, pratiquez sur LeetCode et soyez confiant dans l'explication de la magie de Boyer-Moore.
> **Suivez pour plus d'articles prêts à l'entrevue** – nous nous attaquerons au tri, DP, théorie des graphiques, et plus encore.

---

- Oui. 4. Liste de contrôle du référencement (pour l'article du blog)

1. **Titre** – Élement Majorité II – LeetCode 229 Python, Solutions C++
2. **Description détaillée** – Résumé abrégé et riche en mots clés (voir ci-dessus).
3. **En-têtes** – H1, H2, H3 avec les mots-clés de la cible (=LeetCode 229,=Majority Element II,==Boyer–Moore,==O(n) time==).
4. **Liens internes** – Lien vers des articles connexes ou votre page de démonstration de code-pen.
5. **Liens externes** – Page de problème Reference LeetCode, explication officielle.
5. **Alt text** – Pour les captures d'écran ou les diagrammes de code, utilisez des balises alt descriptives.
6. ** Densité de mots clés** – ~1–2 % pour les mots clés principaux; utilisation naturelle.
7. **Partage social** – Inclure les boutons d'action ; mentionner « Partager sur LinkedIn, Twitter ».

Avec cet article, non seulement vous résolvez le problème, mais vous vous positionnez aussi comme un candidat capable d'offrir un code multiplateforme optimisé, un incontournable pour les rôles d'ingénierie logicielle actuels. Joyeux entretien !