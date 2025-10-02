---
titre: LeetCode 354. Enveloppes de poupées russes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La maîtrise du LeetCode 354 – Enveloppes de poupées russes

Code de la langue
C'est quoi, ça ?
**Java**
**Python**
**C++**

> ** Pourquoi lire ça ? * *
> Si vous vous préparez à une interview d'ingénierie logicielle, les Enveloppes de poupées russes sont un problème classique de niveau dur qui teste les astuces de tri, la programmation dynamique et la recherche binaire.
> Ce post vous donne une solution **complète, prête à la production** en Java, Python et C++, plus une plongée profonde dans le *bon, le mauvais, et le laid* de la résoudre.

---

# Aperçu du problème

**LeetCode 354 – Enveloppes de poupées russes**

> Vous avez une liste d'enveloppes où `enveloppes[i] = [wi, hi]`.
> Une enveloppe peut être placée à l'intérieur d'un autre *iff* ** à la fois** sa largeur *et* sa hauteur sont strictement plus petites.
> Retournez le nombre maximum d'enveloppes que vous pouvez nicher.

*exemple*
[[5,4],[6,4],[6,7],[2,3]» ([2,3] → [5,4] → [6,7])

**Contrôles* *

- `1 ≤ enveloppes longueur ≤ 105 "
- `1 ≤ wi, hi ≤ 105 "

---

Les bons, les mauvais et les méchants

Qu'est-ce qui est bon Qu'est-ce qui est mauvais Quoi ?
- C'est quoi ?
**Approach**= Réduisez à la plus longue séquence croissante (LIS) → `O(n log n)="Le DP naïf (`O(n2)`) échoue sur 105 entrées=" Oublier l'astuce *hauteur-descendant* pour des largeurs égales → mauvaise réponse="
**Traitement**=Traitement par largeur asc, hauteur desc=Traitement par les deux asc peut conduire à traiter les enveloppes de la même largeur de façon incorrecte=Traitement des erreurs cause TLE ou WA si non prudent=
**Recherche binaire**= Réutiliser `Arrays.binarySearch` ou des indices négatifs personnalisés à faible limite.=Le mauvais traitement des indices négatifs conduit à des valeurs hors limite.=Mise en œuvre incorrecte de la recherche binaire (moyen-overflow)==
**Space**= O(n) pour le tableau DP= Mémoire supplémentaire pour les tableaux de copie= Ne libère pas de mémoire sur les grandes entrées=
**Readability**= Aide claire pour LIS==Responsabilités mixtes en une seule fonction==Lambdas en ligne trop compliqués ou classes anonymes==

---

La solution optimale: `O(n log n)` Approche

1. **Enveloppes sèches**
- Largeur **ascendant**.
- Si les largeurs sont égales, trier la hauteur **descendant**.
- Pourquoi descendre ?
- Les enveloppes de la même largeur ne peuvent pas nier.
- En mettant le plus grand d'abord, on évite de le compter deux fois en LIS.

2. ** Hauteurs d'extraction**
Après tri, nous avons une séquence de hauteurs où chaque enveloppe de largeur augmente déjà.

3. ** Calculer le LIS sur les hauteurs* *
- Utilisez une méthode classique de tri de patience (recherche binaire sur un tableau `dp`).
- `dp[i]` stocke la plus petite queue possible d'un subséquence croissant de longueur `i+1`.
- La longueur de la plus longue subséquence croissante est la réponse.

> **Pourquoi LIS?**
> Après tri, toute séquence imbriquée valide doit avoir des hauteurs en augmentation stricte. Ainsi, le problème se réduit à trouver la plus longue subséquence croissante de hauteurs.

---

# Détails de la mise en œuvre

Vous trouverez ci-dessous des implémentations propres et prêtes à la copie pour **Java, Python et C++**.
Les trois utilisent le même noyau algorithmique : trier + LIS avec recherche binaire.

---

Mise en œuvre de Java

"Java
Importer java.util. Les tableaux;
Importer java.util. Comparateur;

solution de classe publique {

// Helper : l'augmentation la plus longue Subséquence en utilisant la recherche binaire
longueur d'inte privée Dénomination des marchandises
int[] dp = nouvelle int[nums.longueur];
Int len = 0;

pour (int num : nombres) {
i = Recherche de tableaux.binary(dp, 0, len, num);
i (i < 0) i = -(i + 1); // point d ' insertion
dp[i] = nombre;
Si (i == len) len++;
}
retour len;
}

Int public maxEnveloppes[[]] {
Classer par largeur asc, hauteur desc pour des largeurs égales
Arrays.sort(enveloppes, nouveau Comparateur<int[]>() {
@Override
public int compare(int[] a, int[] b) {
si (a[0] == b[0]) retour b[1] - a[1]; // hauteur descendante
retour a[0] - b[0]; // largeur ascendante
}
});

Hauteurs d'extraction
int[] hauteurs = nouvelle int[envelopes.longueur];
pour (int i = 0; i < enveloppes.longueur; i++) {
hauteurs[i] = enveloppes[i][1];
}

// 3.
longueur de retourOfLIS(hauteurs);
}
}
«» "

**Complexités* *

- Temps: "O(n log n)" (triage + LIS)
- Espace: "O(n)" (variante de hauteur + DP)

---

Mise en œuvre de Python

'`python
de bisect importer bisect_left
de taper l'importation Liste

Solution de classe:
def maxEnveloppes(même, enveloppes: Liste[Liste[int]]) -> Int:
N° 1 Tri: largeur asc, hauteur desc
enveloppes.sort(key=lambda x: (x[0], -x[1]))

N° 2 Hauteurs d'extraction
hauteurs = [h pour _, h dans les enveloppes]

LIS par tri de patience
dp = [] # dp[i] = plus petite queue de longueur i+ 1
pour h en hauteur:
idx = bisect_left(dp, h)
Si idx == len(dp):
dp.annexe(h)
Sinon:
dp[idx] = h
retour len(dp)
«» "

**Complexités* *

- Temps: 'O(n log n) "
- Espace: "O(n)"

---

Mise en œuvre du C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxEnveloppes(vecteur<vecteur<int>&enveloppes) {
Classer: largeur ascendante, hauteur descendante
sort(enveloppes.degin(), enveloppes.end(),
[](const auto& a, const auto& b) {
si (a[0] == b[0]) retourne a[1] > b[1]; // hauteur
retour a[0] < b[0]; // largeur asc
});

Hauteurs d'extraction
vecteur<int> hauteurs;
hauteurs.reserve(enveloppes.size());
pour (auto& e : enveloppes) hauteurs.push_back(e[1]);

// LIS en utilisant lower_bound
vector<int> dp; // dp[i] = plus petite queue de longueur i+ 1
pour (int h : hauteurs) {
auto it = lower_bound(dp.begin(), dp.end(), h);
si (it == dp.end()) dp.push_back(h);
sinon *it = h;
}
retourner static_cast<int>(dp.size());
}
};
«» "

**Complexités* *

- Temps: 'O(n log n) "
- Espace: "O(n)"

---

# Comment les éviter

Pourquoi ça arrive
- Oui.
Autres **Sortie par hauteur ascendante** pour des largeurs égales.
**L'utilisation incorrecte de `Arrays.binarySearch`** (Java) Autres
**Débordement de la recherche binaire** (`mid = l + (r-l)/2`)
**O(n2) DP sur 105 entrées**
**Off‐by‐one dans la mise en œuvre du SIL**=Longueur de subséquence incorrecte=Logique du point d'insertion à double contrôle==

---

# Analyse du rendement

Algorithme Temps Espace Remarques
C'est pas vrai.
**Naïve DP** ('O(n2)')=5 × 1010 ops (1052)="O(n)'=" Non faisable"
**Trier + LIS** [« O(n log n) »] Fonctionne confortablement sous la limite d'une seconde fois
**PDD optimisé avec recherche binaire** La seule différence est la clarté de la mise en œuvre.

**Pourquoi `O(n log n)` passe facilement* *

- Tri de 100 000 éléments, 100 000 × log2(100 000) .
- Recherche binaire LIS : une autre opération de 1.7 × 106.
- Total < 4 × 106 opérations primitives → ~0.01–0.02 s sur les juges modernes.

---

Entretien- Points de discussion prêts

1. ** Expliquez l'analogie de la poupée russe**: séquences imbriquées, qui augmentent strictement les paires.
2. **Pourquoi le tri est-il nécessaire**: réduit la comparaison en 2 dimensions au LIS en 1-dimension.
3. **L'astuce descendante en hauteur**: les poignées sont d'égales largeurs correctement.
4. **Détailler la méthode de tri de la patience**: tableau `dp`, recherche binaire, `lower_bound`.
5. **Complexité**: montrer grand— O et pourquoi il répond aux contraintes.
6. **Cas d'Edge**: enveloppe unique, toutes les enveloppes égales, entrée non triée.
7. **Extensions possibles**: si vous autorisez "bisect_right".

> *Astuce*: Gardez l'explication succincte mais soulignez l'astuce intelligente (hauteur descendante). C'est ce que les intervieweurs aiment.

---

Résumé

- **Objectif**: Max enveloppes imbriquées → LIS sur les hauteurs après un tri intelligent.
- **Algorithme**: "O(n log n)" (tri de tri + patience).
- **Mise en œuvre**: Java, Python, C++ – prêts pour les tests de codage de production ou d'entretien.
- ** Erreurs communes** : mauvaise direction de tri, DP naïf, recherche binaire mal gérée.

En maîtrisant ce problème, vous serez équipé pour aborder ** tout problème qui peut être réduit à LIS**, et vous aurez une belle histoire pour votre prochaine entrevue de codage.

Bon codage, et bonne chance pour votre voyage d'entrevue! C'est ce qu'il a dit.

---

*Sentez-vous libre de déposer des questions dans les commentaires ou de partager vos propres variations de la solution. *