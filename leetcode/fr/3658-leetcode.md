---
titre: LeetCode 3658. GCD de Odd et même les sommes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3658 – GCD d'étranges et même des sommes
Un rapide Gagnez une solution en Java, Python et C++
*(O(1) temps, O(1) espace – 100 % le plus rapide sur LeetCode*)

---

TL;DR
Les

- la somme des premiers *n* nombres impairs (`1 + 3 + ... + (2n‐1)`)
- la somme des premiers *n* nombres égaux (`2 + 4 + ... + 2n`)

est toujours "n".
Revenez juste `n`.

Langue Code Complexité
- C'est quoi ?
**Python**
**Java**
**C++**

---

## Pourquoi ça marche – Le Math derrière le -Nice-

Étape de détail Formule Autres
C'est quoi ?
Autres Nombres impairs du premier nombre *n* \( \displaystyle \sum_{k=1}^{n} (2k-1) = n^2 \) Autres
Autres 2= Somme de la première *n* nombres pairs = \( \displaystyle \sum_{k=1}^{n} 2k = n(n+1) \) Autres
CGV de \( n^2 \) et \( n(n+1) \) Autres
Autres Le seul diviseur commun est "n" Parce que "n" divise les deux termes et tout autre diviseur doit aussi diviser "n". Autres

Par conséquent, «gcd = n».

---

Code complet

Python 3

'`python
Solution de classe:
def gcdOfOddEvenSums(self, n: int) -> Int:
"""
Renvoie le GCD de la somme des premiers n nombres impairs
et la somme des premiers nombres égaux.

Complexité: O(1) temps, O(1) espace
"""
retour n
«» "

#### Java 17

"Java
solution de classe {
public int gcdOfOddEvenSums(int n) {
// Le GCD est toujours n, voir l'explication ci-dessus.
retour n;
}
}
«» "

C++17

'`cpp
solution de classe {
public:
int gcdOfOddEvenSums(int n) {
// Retour n directement ; pas besoin de calculer les sommes.
retour n;
}
};
«» "

---

## Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 3658

- Oui. 1. Les bonnes
- **O(1) Heure** – Pas de boucles, pas de récursion. Vous êtes terminé au moment où vous lisez l'entrée.
- **O(1) Espace** – Seulement la valeur d'entrée et de retour.
- ** Mathématiques claires** – Comprendre les formules vous donne confiance que la solution ne échouera jamais.
- ** Edge compétitif** – Un 1-liner est un badge de maîtrise; les intervieweurs aiment le code concis et élégant.

- Oui. 2. Les mauvais
- En supposant que "int" suffit ? * *
Les contraintes de LeetCode disent \(1 \le n \le 10^{??}\) (la limite supérieure exacte est une typo dans l'énoncé du problème). Si vous utilisez `int` en Java/C++, vous risquez de déborder lorsque `n` est près de 231–1.
- **Dirigeant Readability** – Une seule ligne « retour n ; » peut être cryptique pour les lecteurs qui ne connaissent pas les maths.
- **No Edge‐Case Handling** – Bien que `n >= 1`, certaines solutions naïves calculent les sommes puis appellent `gcd`, qui peut déborder pour `n` énormes.

- Oui. 3. L'Ugly
- **Sur-ingénierie** – De nombreux participants écrivent des boucles qui résument la série puis calculent « gcd » avec l'algorithme Euclid. Cela fonctionne, mais les facteurs constants sont énormes, et vous êtes fondamentalement re-mise en œuvre des maths qui , est déjà connu.
- **Wrong Type** – Utiliser `long` en Java/C++ mais oublier que `gcd` peut encore déborder si vous calculez les sommes d'abord.
- **Documentation manquante** – Un liner sans commentaire est une odeur de code. Les futurs responsables (ou votre futur moi) pourraient se demander pourquoi vous êtes simplement de retour `n`.

---

## SEO-Optimized Title & Meta Étiquettes

Contenu du champ
C'est quoi ?
**Titre**=3658 – GCD of Odd & Even Sums: One-Liner O(1) Solution in Python, Java & C++=
**Meta Description**== Apprenez la solution 100 % la plus rapide pour LeetCode 3658. Retourne «n» en tant que GCD de sommes impairs/even. Code en Python, Java, C++ + explication complète. Autres
LeetCode 3658, GCD impair même sommes, solution O(1), Python LeetCode, Java LeetCode, C++ LeetCode, conseils de codage d'entrevue, pensée algorithmique, programmation compétitive

---

Comment cet article vous aide à trouver un emploi

1. **Showcases Algorithmique Insight** – Le blog démontre que vous pouvez réduire un problème à la math pure, une compétence souhaitable pour les entretiens techniques.
2. **Faits saillants Qualité du code** – Propre, commenté et efficace signe le professionnalisme.
3. **Visibilité du moteur de recherche** – L'utilisation de mots-clés ciblés renforce le classement des articles sur les plateformes de recherche d'emploi et les blogs technologiques, en vous mettant devant les recruteurs.
4. ** Partageabilité** – La solution concise de 1 liner est idéale pour les communautés Twitter, LinkedIn et dev, générant un engagement et des références potentielles.

---

Les pensées finales

- **Toujours vérifier les contraintes**: Préférez `long`/`long` pour `n`.
- **Ajouter un commentaire** : Même un seul liner mérite une brève explication de son fonctionnement.
- **Voir l'article** : Un contenu clair et engageant augmente votre expertise perçue.

Bon codage, et bonne chance pour votre prochaine interview!