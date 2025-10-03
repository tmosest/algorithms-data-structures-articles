---
titre: LeetCode 3334. Trouvez le score maximum de facteur de la représentation -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3334 – ♫Trouver la note maximale du facteur de la représentation
*Un problème LeetCode Medium s'est transformé en une étoile d'entrevue. *

---

Table des matières
1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Pourquoi cela compte pour les entrevues] (#pourquoi-il-matières)
3. [Intuition et cas de bord] (#intuition)
4. [Approche de la force brute par rapport à l'approche optimale] (#approches)
* 4.1. Force brute (O(n2))
4.2 Préfixe/suffixe GCD & LCM (O(n))
5. [Complexité temporelle et spatiale](#complexité)
6. [Mise en œuvre en trois langues] (#mise en œuvre)
* Java
* Python
* C++
7. [Test de la solution] (#test)
8. [Bon, mauvais, et laide du problème] (#bon-mauvais)
9. [Conseils d'écriture et de préparation à l'emploi] (#wrap-up)
10. [Référencement et mots-clés](#seo)

---

## Problème Recap <un nom="problème-recap"></a>

> **Donné d'un nombre entier (1 ≤ nombre de longueur ≤ 100, 1 ≤ nombres[i] ≤ 30),**
> **supprimer au plus un élément pour maximiser le score de facteur de la matrice restante,**
> où
> **Note du facteur = GCD (tous les éléments restants) × LCM (tous les éléments restants). **
>
> Retourne ce score maximum de facteur.
> Note : GCD & LCM d'un seul élément sont l'élément lui-même ; un tableau vide donne la note 0.

---

- Oui. Pourquoi ça compte pour les entrevues <un nom=why-it-matters></a>

LeetCode 3334 est une question d'entrevue classique** parce qu'il teste:

Pourquoi ça compte ?
- Oui.
**La théorie des nombres**= Comprendre les propriétés GCD & LCM, la protection contre les débordements
**Programmation dynamique/préfixe-suffixe**
**Analyse de la complexité**
**Codage style**

Si vous réussissez ce problème, vous allez montrer recruteurs vous pouvez:

- Traduire une définition mathématique en code
- Optimiser la force brute jusqu'au temps linéaire
- Cas de bord de poignée gracieusement

---

## Intuition & Edge Cases <a name="intuition"></a>

* Le score du facteur de l'ensemble du tableau est notre référence.
* L'élimination d'un élément peut changer à la fois le GCD et le LCM, parfois drastiquement.
* Étant donné que le nombre de LCM ≤ 30 n'excède jamais 230 (~1 B) lorsqu'il est combiné avec le GCD (au plus 30), un entier de 64 bits (`long`/`long`) est sûr.
* Cas de bord :
* Longueur du tableau = 1 → enlevant rien n'est optimal; score = `x2`.
* Le tableau contient tous les 1=1 → GCD = 1, LCM = 1 → score = 1.
* Enlever n'importe quel élément lorsque tous les nombres sont égaux laisse le même GCD/LCM.

---

## Brute-Force vs. Approche optimale <un nom></a>

#### 4.1 Force brute (O(n2))

Calculez GCD/LCM pour chaque sous-ensemble qui exclut au plus un élément.

```pseudo
maxScore = 0
pour i en [-1 ... n-1]: // -1 signifie "ne rien supprimer"
courant GCD = 0
courantLCM = 1
pour j dans [0 ... n-1]:
si j == i: continuer
courantGCD = gcd(courant GCD, nombres[j])
currentLCM = lcm(currentLCM, nombres[j])
maxScore = max(maxScore, courantGCD * courantLCM)
«» "

**Pour:** Simple, pas de structures de données supplémentaires.
**Cons:** O(n2) temps; pas idéal si `n` étaient grands.

4.2 Préfixe / suffixe GCD & LCM (O(n))

L'observation clé: GCD/LCM du tableau sans élément `i` est égale au préfixe ** jusqu'à `i‐1` combiné avec le suffixe après `i`**.

1. Précalculer
* `prefGCD[k]` = GCD de `nums[0 ... k] "
* `prefLCM[k]` = LCM de `nums[0 ... k] "
* `sufGCD[k]` = GCD de `nums[k ... n‐1] "
* `sufLCM[k]` = LCM de `nums[k ... n‐1] "

2. Pour chaque indice «i»:
* `gcdSansI = gcd(prefGCD[i-1], sufGCD[i+1])` (border les mains)
* `lcmSansI = lcm(prefLCM[i-1], sufLCM[i+1])`
* `score = gcdSansI * lcmSansI "

3. Considérez aussi le cas de l'enlèvement de l'ensemble de la matrice.

**Pourquoi ça marche* *
GCD et LCM sont associatifs et commutatifs:
`gcd(a,b,c) = gcd(gcd(a,b),c)` et de la même façon pour le ML.
Ainsi, le tableau sans un élément peut être construit en combinant les deux moitiés.

**Complexités* *
* Heure: O(n)
* Espace: O(n) (quatre tableaux auxiliaires)

---

## Complexité temporelle et spatiale <un nom=complexité></a>

L'approche Temps Espace
- C'est quoi ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
Préfixe/suffixe **O(n)**

Compte tenu des contraintes (`n ≤ 100`), les deux passent confortablement.
Cependant, les intervieweurs attendent souvent la solution linéaire.

---

## Mise en oeuvre dans trois langues <un nom></a>

Voici des solutions propres et autonomes pour Java, Python et C++.

> **Astuce:** La fonction GCD est intégrée dans Java (`java.math.BigInteger.gcd`) et Python (`math.gcd`). Dans C++, nous utilisons `std::gcd` de `<numérique>`.

---

- Oui. 1. Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
statique privé long gcd (long a, long b) {
pendant que (b != 0) {
long t = a % b;
a = b;
b = t;
}
retour a;
}

intérieur statique long lcm(long a, long b) {
Si (a) : 0) retour 0;
retourner a / gcd(a, b) * b; // diviser d'abord pour éviter le débordement
}

public long maxScore(int[] nums) {
int n = longueur nums;
si (n == 1) retour (long) nombres[0] * nombres[0];

long[] prefGcd = nouveau long[n];
long[] prefLcm = nouveau long[n];
long[] sufGcd = nouveau long[n];
long[] sufLcm = nouveau long[n];

prefGcd[0] = nombres[0];
prefLcm[0] = nombres[0];
pour (int i = 1; i < n; i++) {
prefGcd[i] = gcd(prefGcd[i - 1], nombres[i]);
b) PréfLcm[i] = lcm[i - 1], nombres[i];
}

sufGcd[n - 1] = nombres[n - 1];
sufLcm[n - 1] = nombres[n - 1];
pour (int i = n - 2; i >= 0; i--) {
sufGcd[i] = gcd(sufGcd[i + 1], nombres[i];
sufLcm[i] = lcm(sufLcm[i + 1], nombres[i];
}

long best = prefGcd[n - 1] * prefLcm[n - 1]; // aucun retrait

pour (int i = 0; i < n; i++) {
long g = (i == 0) ? sufGcd[1] : (i == n - 1) ? b) PrefGcd[n - 2] : gcd(prefGcd[i - 1], sufGcd[i + 1]);
long l = (i == 0) ? sufLcm[1] : (i == n - 1) ? b) PréfLcm[n - 2] : lcm(préfLcm[i - 1], sufLcm[i + 1];
best = Math.max(best, g * l);
}
le meilleur retour;
}

// ------------------- pilote pour un contrôle rapide de la santé mentale -------------------
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.maxScore(nouvelle int[]{2,4,8,16}); // 64
Système.out.println(s.maxScore(nouvelle int[]{1,1,1}); // 1
System.out.println(s.maxScore(new int[]{5}); // 25
}
}
«» "

---

- Oui. 2. Python (Python 3.10)

'`python
importer des maths
de taper l'importation Liste

Solution de classe:
def maxScore(self, nombres: List[int]) -> Int:
n = len(nums)
si n] 1 :
nombres de retour[0] * nombres[0]

pref_gcd = [0] * n
pf_lcm = [0] * n
suf_gcd = [0] * n
suf_lcm = [0] * n

pref_gcd[0] = pref_lcm[0] = nombres[0]
pour i dans la plage (1, n):
pref_gcd[i] = maths.gcd(pref_gcd[i - 1], nombres[i])
pref_lcm[i] = pref_lcm[i - 1] // math.gcd(pref_lcm[i - 1], nombres[i]) * nombres[i]

suf_gcd[-1] = suf_lcm[-1] = nombres[-1]
pour i dans la plage (n - 2, -1, -1):
suf_gcd[i] = math.gcd(suf_gcd[i + 1], nombres[i])
_1cm[i] = suf_lcm[i + 1] // math.gcd(suf_lcm[i + 1], nombres[i]) * nombres[i]

best = pref_gcd[-1] * pref_lcm[-1] # aucune suppression

pour i dans la plage(n):
g = suf_gcd[1] si i == 0 autre pref_gcd[n - 2] si i == n - 1 autre math.gcd(pref_gcd[i - 1], suf_gcd[i + 1])
l = suf_lcm[1] si i == 0 autre pref_lcm[n - 2] si i == n - 1 autre (pref_lcm[i - 1] // math.gcd(pref_lcm[i - 1], suf_lcm[i + 1]) * suf_lcm[i + 1])
best = max (meilleur, g * l)

le meilleur retour

# tests manuels rapides
si __nom__ == "__main__" :
s = Solution()
print(s.maxScore([2,4,8,16])) # 64
print(s.maxScore([1,1.1))) # 1
print(s.maxScore([5])) # 25
«» "

---

- Oui. 3. C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long gcdll(long long a, long b) {
b) { long t = a % b; a = b; b = t; }
retour a;
}

long long (long long a, long b) {
Si (a) : 0) retour 0;
retourner a / gcdll(a, b) * b; // diviser d'abord
}

long maxScore(vecteur<int>& nums) {
int n = nombres.size();
si (n == 1) retourner 1LL * nombres[0] * nombres[0];

vecteur <long long> prefGcd(n), prefLcm(n), sufGcd(n), sufLcm(n);

prefGcd[0] = prefLcm[0] = nombres[0];
pour (int i = 1; i < n; ++i) {
prefGcd[i] = gcdll(prefGcd[i-1], nombres[i]);
l'alinéa suivant est ajouté:
}

sufGcd[n-1] = sufLcm[n-1] = nombres[n-1];
pour (int i = n-2; i >= 0; --i) {
sufGcd[i] = gcdll(sufGcd[i+1], nombres[i];
sufLcm[i] = lcmll(sufLcm[i+1], nombres[i];
}

long long best = prefGcd.back() * prefLcm.back(); // aucune suppression

pour (int i = 0; i < n; ++i) {
long g = (i == 0) ? sufGcd[1] : (i == n-1) ? prefGcd[n-2] : gcdll(prefGcd[i-1], sufGcd[i+1];
long l = (i == 0) ? sufLcm[1] : (i == n-1) ? prefLcm[n-2] : lcmll(prefLcm[i-1], sufLcm[i+1];
best = max (meilleur, g * l);
}
le meilleur retour;
}
};
«» "

---

## Tester la solution <un nom="test"></a>

"""
♪ Java
Javac Solution.java
java Solution
# Python
solution python3. py
Numéro C++
g++ -std=c++17 -O2 solution.cpp -O Sol
./sol
«» "

Entrées d'échantillons (vous pouvez copier-coller dans un harnais de test):

Produit escompté
-- -- -- -- -- -- -- --
[2,4,8,16]
[1,1]
[5]
[4,4]
"[3,6,9]"""18" (supprimer 9 → GCD = 3, LCM = 6, score = 18)"

---

## Bon, mauvais, et laideur du problème <un nom</a>

Aspect du bien
- C'est quoi ?
La définition est *propre* et auto-explication. Le GCD/LCM peut être source de confusion pour les candidats qui ne sont pas lourds. Sur-ingénierie : essayer de pré-calculer toutes les sous-ententes possibles. Autres
**Pathure d'optimisation**= Préfixe/suffixe droit. Beaucoup d'intervieweurs s'attendent à ce que vous vous rendiez compte de l'association rapidement. Une mauvaise compréhension du fait que le LCM n'est pas linéaire peut conduire à l'acceptation de l'O(n2). Autres
**Les entiers 64 bits sont en sécurité ici. Certaines solutions oublient de diviser avant de se multiplier en LCM. Oublier que `a*b` peut déborder *même pour les petits a,b* dans les langues sans support intégré 128-bit. Autres
**Tests** Les cas d'Edge avec un seul élément ou tous sont souvent manqués. L'absence d'un renvoi conduit à une mauvaise réponse pour «[1]» ou «[30]». Autres

---

## Wrap‐Up & Job‐ready Conseils <a name="wrap-up"></a>

1. **Commencez avec le croquis de la force brute** – il clarifie l'espace de problème.
2. **Pensez à "supprimer un" comme "préfix + suffixe"** – un modèle qui apparaît dans de nombreux problèmes de tableau (par exemple, "Maximum Subarray" après la suppression d'un élément).
3. **Écrire les aides réutilisables GCD/LCM**; utiliser des fonctions intégrées lorsque c'est possible.
4. **Test sur les caisses de bord** (longueur = 1, toutes les 1s, toutes mêmes, mélangées petites/grandes).
5. ** Expliquez votre intuition à haute voix** lors d'une entrevue; les recruteurs s'intéressent à votre processus de pensée autant que le code final.

> *Si vous pouvez implémenter 3334 en moins de 30 secondes, vous êtes probablement prêt à attaquer d'autres Mediums LeetCode (par exemple, 1646, 1461, 1519) avec confiance. *

---

## SEO & Mots-clés <a name="seo"></a>

- **LeetCode 3334**
- Trouvez le score maximum de facteur de la représentation
- problème de suppression de tableau GCD LCM
- Manipulation du tableau linéaire
- Problème d'entretien de la théorie du nombre
- Java/Python/C++ Solutions LeetCode
- Problèmes mathématiques de préparation des entretiens
- Questions sur l'algorithme d'entretien d'emploi

Ajouter les tags ci-dessus à votre blog, GitHub repo, ou portefeuille pour augmenter la visibilité parmi les recruteurs à la recherche de défis de "LeetCode Medium," ou "Array manipulation".

Bon codage – et bonne chance pour votre prochaine interview! C'est ce qu'il a dit