---
titre: LeetCode 2652. Somme multiple - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 2652 – **Sum Multiples**
**Votre guide go‐to pour les solutions Java, Python & C++ + un article de blog optimisé pour le référencement* *

> *Sum tous les entiers de 1 à n qui sont divisibles par 3, 5 ou 7.
> **Difficulté:** Facile

---

TL;DR

Langue O(1) Formule mathématique O(n) Boucle
- C'est quoi ?
**Java** – utilise les séries arithmétiques
**Python** – utilise les séries arithmétiques
*C++** .Sum Of Multiples(n) – utilise les séries arithmétiques

> **Choisir la solution Math** pour passer de grands tests en *< 1 ms* et impressionner les intervieweurs.

---

## Article de blog – Le bon, le mauvais, et le lamentable de somme multiples

> ** Mots-clés de référence**: *LeetCode Somme Multiples, La somme Java des multiples, la somme Python des multiples, la somme C++ des multiples, le défi de codage d'entretien, la solution O(1), les séries arithmétiques, l'algorithme interview prep*

Aperçu du problème

LeetCode 2652 vous demande de calculer la somme de chaque entier entre 1 et n (inclus) qui est un multiple de 3, 5, ou 7.
Les contraintes sont minuscules ('1 ≤ n ≤ 10^3') – mais un *pass unique* sur la plage vous montre encore une approche efficace O(n). La vraie question de style interview est: pouvez-vous le faire *O(1)* avec un tour mathématique?

> **Pourquoi c'est important**: Les intervieweurs aiment vous voir utiliser *inclusion-exclusion* et *série arithmétique* – cela vous montre que vous êtes à l'aise avec l'analyse mathématique et la complexité.

---

C'est vrai. L'approche naïve – O(n) Loop

"Java
= 0;
pour (int i = 1; i <= n; i++) {
Si (i % 3 == 0=1 i % 5 == 0=1 i % 7 == 0) {
Montant i);
}
}
«» "

**Pour**
- Simple à comprendre
- Travaux pour n'importe quel n

**Cons**
- Temps linéaire → inutile pour n minuscule dans les scénarios d'entretien réel
- Ne démontre pas une pensée algorithmique plus profonde

> **Ligne de bottom** : bonne pour une solution rapide, mauvaise pour un entretien de codage *réel*.

---

La solution élégante O(1) Math

Nous utilisons la formule pour la somme d'une série arithmétique:

\[
S_k = k + 2k + 3k + \dots + mk = k \times \frac{m(m+1)}{2}
\]
où `m = ..

**Inclusion – Principe d'exclusion* *

- Somme de multiples de 3 + multiples de 5 + multiples de 7
- Soustraire les multiples de 15 (3×5), 21 (3×7), 35 (5×7) (depuis compté deux fois)
- Ajouter des multiples de 105 (3×5×7) dos (depuis soustrait trois fois)

**Formule* *

«» "
S = sommeMultiples(3) + sommeMultiples(5) + sommeMultiples(7)
- sommeMultiples(15) - sommeMultiples(21) - sommeMultiples(35)
+ sommeMultiples(105)
«» "

où "sumMultiples(k)" est calculé en O(1) comme suit:

«» "
m = n / k
retour k * m * (m + 1) / 2
«» "

**Avantages**

- **Heure**: O(1) – aucune boucle
- **Espace**: O(1)
- **Readability**: montre la maîtrise de la conception mathématique et de l'algorithme
- **Performance**: passe des millions de cas d'essai instantanément

---

######=4=" Extraits de code – prêts à être copiés

##### 4.1 Java (O(1) Math)

"Java
solution de classe {
Int sumOfMultiples(int n) {
retour (int) (somme(n, 3) + somme(n, 5) + somme(n, 7)
- somme(n, 15) - somme(n, 21) - somme(n, 35)
+ somme(n, 105);
}

somme privée longue (int n, int k) {
long m = n / k;
retour (long) k * m * (m + 1) / 2;
}
}
«» "

##### 4.2 Python (O(1) Mathématiques)

'`python
Solution de classe:
def sumOfMultiples(self, n: int) -> Int:
def s(k: int) -> Int:
m = n // k
retour k * m * (m + 1) // 2

retour (
paragraphe 3 + paragraphe 5 + paragraphe 7
- s(15) - s(21) - s(35)
+ s(105)
)
«» "

#### 4.3 C++ (O(1) Mathématiques)

'`cpp
solution de classe {
public:
nt sumOfMultiples(int n) {
somme automatique = [&](int k) -> long {
long m = n / k;
retour 1LL * k * m * (m + 1) / 2;
};
retourner static_cast<int>(
somme(3) + somme(5) + somme(7)
- somme(15) - somme(21) - somme(35)
+ somme(105)
);
}
};
«» "

> **Astuce**: Utilisez `long` pour les produits intermédiaires pour éviter les débordements, même si la réponse finale correspond à `int`.

---

#### 5.

Numéro
C'est quoi ?
Utiliser `long`/`long long` pour les calculs intermédiaires
En oubliant l'inclusion – Exclusion Vérifier que chaque ensemble multiple est ajouté/subtracté correctement
Utiliser `n / k` pour compter le nombre de multiples existant jusqu'à `n` Autres
Autres Essais de résistance jusqu'à 10^9 pour confirmer le fonctionnement de la formule

---

#### 6-

L'approche Temps Espace
- C'est quoi ?
O(n) Boucle **O(n)**
O 1) Mathématiques

> **Takeaway**: Dans les interviews, préférez la solution O(1) – elle montre que vous savez optimiser et utiliser les mathématiques pour réduire le temps d'exécution.

---

### # 7-

1. **Demandez toujours des contraintes** – elles vous guident vers la bonne complexité.
2. ** Expliquez votre processus de pensée** – parlez d'inclusion – exclusion, séries arithmétiques, et pourquoi vous avez choisi O(1).
3. **Cas de bord de Mention** – débordement, grand `n`, et comment vous gardez contre eux.
4. **Soyez prêt à mettre en œuvre** – donnez un code propre et bien commenté (voir les extraits ci-dessus).

---

Pratique, pratique, pratique

- **LeetCode**: 2652 – Somme multiple
- **GeeksforGeeks**: Série arithmétique Sum - rafraîchir la formule
- **HackerRank**: Problèmes pratiques d'inclusion

---

Mot final

Le problème Sum Multiples est un *classique* pour apprendre à transformer une simple boucle en une solution mathématiquement élégante. En maîtrisant les séries inclusion-exclusion et arithmétique, vous allez :

- Réduire la complexité du temps de linéaire à constant
- Montrer les intervieweurs que vous pensez au-delà de la force brute
- Renforcer la confiance pour les problèmes plus difficiles (p. ex., le comptage des coprimes, la fonction de mobius)

> **Conseil pro**: Lorsque vous terminez, écrivez une suite de test rapide (JUnit/pytest/GoogleTest) pour couvrir les cas de bord. Il montre professionnalisme et attention au détail.

---

Références et lectures supplémentaires

- LeetCode 2652 – [Sum Multiples](https://leetcode.com/problèmes/sum-multiples/)
- GeeksforGeeks – [Arithmetic Progression Sum] (https://www.geeksforgeeks.org/arithmetic-progressions/)
- Brilliant.org – [Inclusion – Principe d'exclusion] (https://brilliant.org/wiki/inclusion-exclusion-principe/)

---

Obtenez votre emploi

Vous voulez décrocher ce rôle d'ingénierie logicielle ?
- **Suivez** notre chaîne pour plus de passages LeetCode
- **Télécharger** la liste de contrôle gratuite de la préparation de l'entrevue
- **Reach out** pour un coaching personnalisé

Codage heureux 