---
titre: LeetCode 1944. Nombre de personnes visibles en attente -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de la solution

Ci-dessous sont trois implémentations complètement indépendantes de la solution `O(n)` optimale pour le LeetCode 1944.
Les trois utilisent l'idée **next-taller** (une pile monotonique sous le capot) et ont une logique identique.

---

## 1.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {

***
* Retourne le nombre de personnes que chaque personne peut voir à droite.
* @param hauteurs tableau de hauteurs distinctes
Tableau de nombres @retour
*/
public int[] canSeePersonnesCount(int[] hauteurs) {
si (hauteurs) = null== hauteurs.longueur <= 1) {
retourner une nouvelle int[]{0};
}

int n = hauteurs. longueur;
int[] nextTaller = nouveau int[n]; // index de la première personne à droite qui est plus grand (ou n)
résultat int[] = nouveau résultat int[n];

nextTaller[n - 1] = n; // personne à droite de la dernière personne
résultat[n - 1] = 0;

pour (int i = n - 2; i >= 0; --i) {
int j = i + 1; // commencer par le voisin immédiat
int cnt = 1; // i peut toujours voir j

// Alors que j est plus court que moi, saute le bloc entier que j peut voir
pendant que (j < n& hauteurs[j] < hauteurs[i]) {
j = nextTaller[j]; // sauter à la personne suivante plus grande de j
cnt++; // j elle-même est visible
}

// Si nous avons terminé parce que nous avons atteint la fin du tableau, nous avons compté un extra
si j == n) cnt--;

nextTaller[i] = j; // stocker pour les futures requêtes
résultat[i] = cnt;
}

le résultat du retour;
}

// harnais d'essai simple
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
int[] h1 = {10,6,8,5,11,9};
Système.out.println(Arrays.toString(sol.canSeePersonsCount(h1))); // [3, 1, 2, 1, 1, 0]

Int[] h2 = {5,1,2,3,10};
Système.out.println(Arrays.toString(sol.canSeePersonsCount(h2))); // [4, 1, 1, 1, 0]
}
}
«» "

---

## 1.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def canSeePerson(self, hauteurs: List[int]) -> Liste[int]:
si non hauteurs ou len(hauteurs) <= 1:
retour [0]

n = len(hauteurs)
next_taller = [n] * n # index de la première personne plus grande à droite
résultat = [0] * n

La dernière personne ne voit personne
next_taller[n-1] = n
résultat[n-1] = 0

pour i dans la plage(n-2, -1, -1):
j = i + 1
cnt = 1 # peut toujours voir le voisin immédiat

tandis que j < n et hauteurs[j] < hauteurs[i]:
j = next_taller[j] # sauter le bloc entier que j peut voir
cnt += 1

si j == n:
cnt = 1

suivant_taller[i] = j
résultat[i] = cnt

résultat du retour

Essai rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.canSeePersonnesCount([10,6,8,5,11,9])) # [3, 1, 2, 1, 1, 0]
print(sol.canSeePersonnesCount([5,1,2,3,10]) # [4, 1, 1, 1, 0]
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> canSeePersonsCount(vecteur<int>& hauteurs) {
int n = hauteurs.size();
si (n <= 1) retourner {0};

vector<int> nextTaller(n, n); // index de la première personne plus grande à droite
vecteur<int> résultat(n, 0);

// la dernière personne ne voit personne
nextTaller[n-1] = n;
résultat[n-1] = 0;

pour (int i = n-2; i >= 0; --i) {
i + 1;
int cnt = 1; // peut toujours voir le voisin

pendant que (j < n& hauteurs[j] < hauteurs[i]) {
j = nextTaller[j]; // sauter le bloc que j peut voir
cnt++;
}

i (j == n) cnt--; // nous en avons compté un trop

nextTaller[i] = j;
résultat[i] = cnt;
}
le résultat du retour;
}
};

// Essai simple
Int main() {
Solution s;
vecteur<int> h1 = {10,6,8,5,11,9};
auto r1 = s.canSeePersonsCount(h1);
pour (int x : r1) cout << x << '; // 3 1 2 1 1 0
Cout << '\n';

vecteur<int> h2 = {5,1,2,3,10};
auto r2 = s.canSeePersonsCount(h2);
pour (int x : r2) cout << x << '; // 4 1 1 0
Cout << '\n';
}
«» "

---

♪ 2. Article du blog

> **Titre** – Mastering LeetCode 1944 : *Nombre de personnes visibles en file d'attente* – Stack monotonique & Next‐ Technique Taller
> **Tags** – #LeetCode #InterviewPrep #AlgorithmDesign #Java #Python #C++ #MonotonicStack #CodingInterview

---

2.1 Pourquoi ce problème se pose dans les entrevues

- ** Logique de visibilité** – Capture une condition non-triviale de « ligne de vue » qui n'est pas un problème classique de fenêtre coulissante ou de deux points.
- **Échelle** – Les contraintes (`n ≤ 105`) en font un terrain de jeu parfait pour les structures de données avancées: *pile monotonique*.
- **Signaux de recrutement** – Résoudre ceci en O(n) avec un raisonnement clair montre votre capacité à transformer une force brute naïve en algorithme prêt à la production – exactement ce que les rôles supérieurs exigent.

---

## 2.2 Récapitulation des problèmes

> Compte tenu d'un tableau « hauteurs » de ** hauteurs entières distinctes**, chaque élément représente la hauteur d'une personne debout dans une file d'attente de gauche à droite.
> Une personne peut voir une autre personne à droite si *tous* les gens entre eux sont ** strictement plus courts** que *plus courts* des deux.
> Return a array `answer` where `answer[i]` correspond au nombre de personnes que la i-th personne peut voir à droite.

---

## 2.3 Naïve O(n2) Brute-Force

Texte
pour i = 0 ... n-1:
pour j = i+1 ... n-1:
si chacun entre i et j est plus court que min(hauteur[i], hauteur[j]):
réponse[i] += 1
«» "

Pièges

Pourquoi ça fait mal ?
C'est quoi ?
Pour `n = 100 000`, ~1010 opérations → time-out. Autres
**O(1) espace**= Acceptable, mais l'algorithme est opaque pour les intervieweurs. Autres
**Difficile d'expliquer pourquoi il fonctionne; les recruteurs préfèrent un récit clair de la structure des données. Autres

---

## 2.4 Insight: Stack monotonique

> L'observation clé :
> *En marchant de droite à gauche, une personne peut voir toutes les personnes dans un bloc **non-augmentation** jusqu'à ce que la première personne plus grande bloque la vue. *

Ceci se prête naturellement à une pile décroissante **monotonique**:
- Chaque entrée de pile stocke l'index* d'une personne dont la hauteur est ** supérieure à** la prochaine entrée de la pile.
- Oui. Pendant le traitement d'une nouvelle personne `i`, nous pouvons **jump** sur des blocs entiers qui sont plus courts que `i`, parce que chaque personne à l'intérieur d'un tel bloc est déjà connu pour être visible à `i`.

---

## 2.5 Approche de la prochaine stratégie (O(n) amortie)

L'idée est de pré-calculer, pour chaque indice «i», l'indice * de la première personne plus grande à sa droite* («nextTaller[i]».
Si nous connaissons déjà `nextTaller[j]` pour un voisin plus court `j`, nous pouvons sauter toute la sous-tribu `[j+1 ... nextTaller[j]-1]` en une seule étape.

Étapes de l'algorithme

1. **Initialiser**
- `nextTaller[n-1] = n` (personne à droite).
- "réponse[n-1] = 0".

2. **Traverse de droite à gauche**
- Que `j = i + 1` (le voisin immédiat).
- `cnt = 1` (la personne `i` voit toujours `j`).
- Pendant que `hauteurs[j] < hauteurs[i]`:
- `j = nextTaller[j]` (jump à la personne suivante plus grande de `j`).
- "cnt++".
- Si nous nous sommes arrêtés parce que `j == n`, nous avons compté un trop de → `cnt--`.
- Stocker `nextTaller[i] = j` et `answer[i] = cnt`.

3. **Retour** le tableau de réponses.

> **Pourquoi c'est correct** – Chaque `cnt` compte chaque personne qui est soit *directement* visible (`j`) ou fait partie d'un **bloc** de personnes strictement plus courtes que `j` peut voir.
> Parce que `nextTaller[j]` est toujours la première personne plus grande au-delà de ce bloc, on ne double jamais ni ne manque personne.

---

2.6 Exemple de passage

On exécute l'algorithme sur `hauteurs = [10, 6, 8, 5, 11, 9]'.

Tailles [i] Autres
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
(n)
1 9)
1 (11)
1 (5) → sauter à 4 (11) → +1 = 2
# 1= 6= 2= 1 (8) → sauter à 4 (11) → +1 = 2= 4=
1 (6) → sauter à 2 (8) → +1 = 2 → sauter à 4 (11) → +1 = 3

Résultat: `[3, 1, 2, 1, 1, 0]`.

---

2.7 Analyse de la complexité

Complexe métrique
C'est pas vrai.
Temps amorti (chaque indice est poussé/poché au plus une fois)
L'espace `O(n)` pour `nextTaller` et le tableau de réponses (pas de pile explicite dans le code final)

> **Pourquoi amortir?**
> Même si la boucle intérieure `While` peut fonctionner plusieurs fois, chaque indice est au plus une fois car il est retiré de la pile quand une personne plus grande est rencontrée. Par conséquent, le nombre total d'itérations de boucle sur toute la passe est ≤ 2 n.

---

2.8 Code en trois langues

*(Voir les extraits de code ci-dessus)*

Chaque mise en œuvre suit le même squelette logique:

Texte
pour i de n-2 à 0:
j = i + 1
cnt = 1 // voisin immédiat
tandis que j < n et hauteurs[j] < hauteurs[i]:
j = nextTaller[j] // sauter sur un bloc de personnes plus courtes
cnt += 1
if j == n: cnt -= 1 // nous en avons compté un trop
suivantTaller[i] = j
réponse[i] = cnt
«» "

Les codes Java, Python et C++ diffèrent uniquement en syntaxe, et non en substance algorithmique.

---

##2.9 Edge- Liste de contrôle des cas

Qu'est-ce qui arrive ?
C'est-à-dire
- Oui. Retours "[0]" Pas de gens, pas de visibilité. Autres
- Oui. 1 ''' Retourne `[0] '' La dernière personne ne voit personne. Autres
Autres Toutes les hauteurs augmentent (par exemple, `[1,2,3,4]`) Chaque personne ne voit que le voisin. Autres
Autres Toutes les hauteurs diminuent (par exemple, `[4,3,2,1]`) La première personne voit tous les autres. Autres

---

## 2.10 Bon, mauvais, mauvais – Ce que les intervieweurs À propos

Aspect du bien
- C'est quoi ?
**Heure**= O(n) passe tous les tests rapidement. O(n2) est *inacceptable* sur les limites données. Oublier de gérer le cas de la dernière personne peut donner silencieusement `0` au lieu de `1`. Autres
**L'espace** Autres Trop de structures auxiliaires peuvent faire exploser la mémoire sur des entrées extrêmement importantes. L'utilisation d'une récursion naïve (débordement de sacs) est un écueil laid. Autres
**Readability**La pile monotonique est un modèle de manuel, facile à expliquer. Des astuces obscures peuvent cacher la logique sous-jacente. Le sur-commentage des boucles intérieures peut devenir illisible; maigre mais le code explicatif est le meilleur. Autres
**Correctness**=Le fait de sauter sur les blocs visibles *entier* ne garantit pas un double comptage. La logique manuelle « while » peut accidentellement surestimer si le cas de fin de procès est oublié. Le fait de ne pas gérer le scénario de hauteur exactement égale (bien que le problème garantisse des hauteurs distinctes) peut briser d'autres problèmes similaires. Autres
**Interview Narratif**=Je me suis rendu compte qu'une fois que je connais la personne suivante plus grande, toutes les personnes entre les deux sont visibles; je peux donc les sauter en un seul saut. J'ai essayé une boucle imbriquée d'abord, mais c'était trop lent. Autres

---

## 2.11 Tendance des entrevues

1. **Comprenez la géométrie** – visualisez la file d'attente, imaginez une ligne de vue et pensez en termes de blocs de personnes.
2. **Traduisez le problème en une pile monotonique** – il s'agit d'un modèle commun pour les problèmes de vision ou de plus grand élément.
3. **Expliquer le *pourquoi* de chaque étape** – les recruteurs aiment une justification claire pour pourquoi un bloc peut être sauté.
4. **Cas de bord de Mention** – cela démontre une programmation défensive. Même si l'entrée garantit des hauteurs distinctes, il est bon de parler de variantes de hauteur égale.
5. **Ecrire un code propre et minimal** – vous pouvez résoudre en Python, Java ou C++ ; l'idée centrale reste la même.

---

2.12 Conclusion

> Le problème de la file d'attente de "Visibilité" est un microcosme de conception d'algorithmes modernes : il se situe à l'intersection du raisonnement combinatoire et de l'utilisation efficace de la structure des données.
> Résoudre proprement en O(n) met en valeur la maîtrise des piles monotoniques et l'élégance algorithmique – un combo gagnant pour les rôles logiciels seniors.

---

## 2.13 Lecture et pratique supplémentaires

- **Next Greater Element** – problème classique de LeetCode.
- **Stone Wall (Codilité)** – utilise une pile pour calculer les changements de hauteur de paroi.
- **Le plus grand rectangle en histogramme** – une torsion de programmation dynamique sur la logique de la pile.
- **Fenêtre coulissante Maximum** – repose également sur une file d'attente monotonique.

---

> **TL;DR:**
> 1. Reconnaissez les blocs visibles → pile décroissante monotonique.
> 2. Précalculer `nextTaller[i]` tout en traversant de droite à gauche.
> 3. Sautez sur les blocs, ajustez le compteur et manipulez le boîtier de fin de parcours.
> 4. Mettre en œuvre dans n'importe quelle langue; le noyau algorithmique reste le même.

---

*Bon code, et que votre ligne de vue soit toujours claire dans chaque entrevue! *