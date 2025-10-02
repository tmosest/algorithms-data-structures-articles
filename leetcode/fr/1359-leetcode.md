---
titre: LeetCode 1359. Compter toutes les options de ramassage et de livraison valides -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1359. Compter toutes les options de ramassage et de livraison valides
### Hard – LeetCode, le favori des interviews, et une grande vitrine pour votre portfolio

> **Mots-clés** – *Codeleet 1359*, *comptez toutes les options de ramassage et de livraison valides*, *hard*, *DP*, *combinatoire*, *entrevue d'algorithme*, *entrevue de codage*, *conseils d'entrevue d'emploi*, *solution de Java*, *solution de Python*, *solution de C++*

---

- Oui. 1. Exposé des problèmes (reformulé)

Vous avez des ordres **n**.
Chaque commande `i` se compose d'un *pickup* (`Pi`) et d'un *livraison* (`Di`).
Vous devez créer une seule séquence qui contient tous les événements `2n`, avec la seule restriction que `Di` doit venir **après** "Pi".

> Exemple
> `n = 2` → séquences possibles (6 au total)
> `P1 P2 D1 D2`, `P1 P2 D2 D1`, `P1 D1 P2 D2`, `P2 P1 D1 D2`, `P2 P1 D2`, `P2 P1 D2`, `P2 D2 P1 D1`

Retourner le nombre de séquences valides modulo `10^9 + 7`.
«1 ≤ n ≤ 500».

---

- Oui. 2. Pourquoi ce problème est une grande question d'entrevue

C'est bien, c'est mal.
C'est pas vrai.
**Compbinatoire** – révèle combien d'intervieweurs aiment des solutions mathématiques propres. **Modulo arithmétique** – vous aurez besoin de se rappeler de garder tout à l'intérieur `int64`. Autres
**Le temps linéaire** – O(n) le résout instantanément même pour n = 500. **La programmation dynamique** peut être exagérée; les gens mettent souvent en place une table DP énorme au lieu d'un seul ligne. Autres
**Démonstration en langage brut** – un algorithme unique peut être codé en Java, Python et C++. Autres

---

- Oui. 3. Intuition et dérivation

1. **Vue faciale**
Le nombre total de façons d ' organiser des articles distincts est de " (2n) ! " .
Chaque livraison doit suivre son ramassage, de sorte que pour chaque commande, nous collapsons la paire `(Pi, Di)` dans une paire d'un ordre.

2. **Divisant la commande à l'intérieur de chaque paire* *
Pour chaque commande, la paire peut être en 2 ordres: `(Pi, Di)` ou `(Di, Pi)`.
Nous ne devons garder que le bon, donc nous nous divisons par `2` pour chaque ordre.
La réponse est donc:

\[
Le nombre d'heures de travail est le suivant:
\]

3. **Simplifier le produit**
Grouper les termes factoriels deux par deux :

\[
= \prod_{i=1}^{n} (2i-1)(2i)
\]

Diviser par «2» à l'intérieur de chaque produit:

\[
\frac{(2i-1)(2i)}{2} = (2i-1) \cdot i
\]

Alors

\[
\text{réponse} = \prod_{i=1}^{n} i \times (2i-1)
\]

Cette formule ne nécessite que des multiplications `O(n)` et seulement **une** variable pour garder le produit en cours d'exécution.

---

- Oui. 4. La formule finale

«» "
ans = 1
pour i = 1 ... n:
ans = ans * i (mod M)
ans = ans * (2*i - 1) (mod M)
retour et
«» "

«M = 1_000_000_007».

L'opération modulo est appliquée après **chaque** multiplication pour éviter le débordement (utiliser `long`/`long long`).

---

- Oui. 5. Mise en œuvre du code

#### 5.1 Java

"Java
solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

Commission européenne
long ans = 1;
pour (int i = 1; i <= n; i++) {
ans = (ans * i) % MOD; // multiplier par i
ans = (ans * (2L * i - 1)) % MOD; // multiplier par (2*i-1)
}
retour (int) ans;
}
}
«» "

* Pourquoi ça marche : *
Tous les résultats intermédiaires restent dans la 'long' (')
Le modulo maintient les valeurs limites, et le casting final à `int` est sûr parce que le résultat est toujours < `MOD`.

---

5.2 Python

'`python
Solution de classe:
MOD = 1 000 000 007

def countOrders(self, n: int) -> Int:
ans = 1
pour i dans la plage(1, n + 1):
ans = (ans * i) % de soi. MOD
ans = (ans * (2 * i - 1)) MOD
retour et
«» "

Python="int` est non consolidé, mais nous appliquons toujours le modulo pour la cohérence et pour imiter l'environnement LeetCode.

---

C++

'`cpp
solution de classe {
public:
int countOrders(int n) {
longue MOD = 1'000'000'007LL;
long an = 1;
pour (long long i = 1; i <= n; ++i) {
ans = (ans * i) % MOD; // multiplier par i
ans = (ans * (2 * i - 1)) % MOD; // multiplier par (2*i-1)
}
retourner static_cast<int>(ans);
}
};
«» "

"long" (64-bit) suffit parce que le produit intermédiaire ne dépasse jamais "9.22·10^18".

---

- Oui. 6. Analyse de la complexité

Java / Python / C++
-- -- -- -- -- -- -- --
**Heure** (une seule boucle)
**Espace** (constante mémoire supplémentaire)

Pour `n = 500` le programme effectue seulement 500 multiplications, finissant en microsecondes.

---

- Oui. 7. Erreurs courantes et comment les éviter

Erreur de vérification
C'est pas vrai.
Utiliser `int` pour le produit en Java ou en C++.Le résultat peut déborder `int` avant d'appliquer modulo. Autres
Autres Le produit peut dépasser la limite de 64 bits. Autres
Calcul "(2n)!" directement. Utilisez la formule dérivée qui n'a jamais besoin d'un facteur complet. Autres
En utilisant `pow(2, n)` pour la division. Soit éviter toute division (utiliser le produit `i * (2i-1)`) soit précalculer les facteurs et utiliser des inverses modulaires. Autres

---

- Oui. 7. Essai de cas de bord

Texte
Entrée: n = 1
Produit : 1

Entrée: n = 2
Produit : 6

Entrée: n = 3
Produit : 90

Entrée: n = 4
Produit : 1 260
«» "

Ce sont les valeurs obtenues de la formule et correspondent à la suite de test officielle LeetCode.

---

- Oui. 7. Bonus – Une alternative rapide avec des facteurs précalculés

Si vous préférez une approche inverse *factorielle + modulaire :

"Java
fait long = 1;
pour (int i = 2; i <= 2*n; i++) fait = fait * i % MOD;
longueur inv2n = modPow(2, n, MOD); // précalcul 2^n
ans = fait * modInverse(inv2n, MOD) % MOD;
«» "

Mais le monoligne dérivé ci-dessus est ** beaucoup plus propre** et plus rapide.

---

- Oui. 7. Stratégie d ' essai

Autres Essai Pourquoi c'est important
-- -- -- -- -- --
`n=1`=Caisse de base – la formule ne doit pas être trop divisée. Autres
"n = 2"" Petit, peut énumérer à la main. Autres
"n = 10"" Vérifie une multiplication plus grande mais assez petite pour vérifier manuellement. Autres
"n = 500" – test de stress – confirme aucun débordement et l'algorithme fonctionne instantanément. Autres
= valeurs aléatoires de `n` = Vérifier si la force brute est mise en œuvre pour `n ≤ 6` (lorsque le dénombrement est possible). Autres

---

- Oui. 8. À emporter pour votre curriculum vitae et votre entrevue

1. ** Mettre en valeur la perspicacité combinatoire** – dites que vous avez découvert la formule élégante du produit.
2. **Afficher les compétences en langues croisées** – télécharger les trois implémentations dans une repo GitHub et les lier dans votre portfolio.
3. **Discuses pièges** – comment vous avez géré modulo arithmétique et évité le débordement.
4. **Scalabilité de la Mention** – expliquer que même pour la plus grande `n`, l'algorithme est toujours O(n).

Ces points démontrent que vous *re *pas* seulement le codage; vous êtes le raisonnement, l'optimisation et la présentation professionnelle.

---

- Oui. 9. Conclusion

LeetCode 1359 est plus qu'un problème dur – c'est une leçon pour transformer un problème de comptage apparemment compliqué en une solution propre et linéaire.

- **Bien**: Un seul liner, O(n) temps, O(1) espace.
- **Bad**: Il faut manipuler soigneusement les modules.
- **Ugly**: L'approche factorielle naïve est une impasse.

En maîtrisant ce problème, vous pourrez l'aser dans n'importe quelle interview qui demande le comptage combinatoire, la programmation dynamique ou simplement un algorithme bien structuré.

Bonne chance, et continuez à coder !