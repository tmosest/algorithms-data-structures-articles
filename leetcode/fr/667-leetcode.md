---
titre: LeetCode 667. Beau arrangement II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 667 – Beau arrangement II
**Moyenne** – «constructArray(n, k)»

> **Problème**
> Compte tenu de deux entiers `n` et `k` (1 ≤ k < n ≤ 104), construire une permutation des premiers nombres `n` naturels de telle sorte que le tableau des différences absolues entre les éléments consécutifs contient **exactement des valeurs distinctes `k`**.
> Retourne toute permutation valide.

Ci-dessous vous trouverez **trois solutions complètes, prêtes à fonctionner** – une en **Java**, une en **Python**, et une en **C++** – plus un parcours *blog-style* qui explique l'algorithme, ses avantages et ses inconvénients, et pourquoi il est un excellent modèle prêt à l'entrevue.

---

L'arrangement magnifique

1. **Nous avons besoin de différences distinctes `k`. * *
La plus grande différence possible dans une permutation de 1...n est `n-1`.
Si nous voulons exactement des différences distinctes `k`, nous pouvons les garantir en construisant un modèle qui produit les différences `k, k-1, ..., 1` – qui `k` valeurs distinctes.

2. ** Stratégie de construction**
* Commencez par les premiers nombres `n-k-1` en ordre ascendant – ils produiront des différences de 1 seulement, aucune nouvelle valeur distincte.
* Pour les positions `k+1` restantes, nous *zig‐zag* entre les deux extrémités de la plage restante:
* côté bas = `n-k` (le premier nombre inutilisé),
* côté supérieur = `n`,
* puis décrémenter le côté supérieur, incrémenter le côté inférieur, etc.
* Ce zig‐zag produit des différences: `k, k-1, ..., 1` dans cet ordre – exactement `k` valeurs distinctes.

3. **Pourquoi ça marche**
* La première partie ne crée pas de nouvelles différences au-delà de `1`.
* La partie zig-zag donne une séquence de différences en baisse stricte, chaque nouvelle différence est plus petite que la précédente.
* Différences distinctes totales = `k`.
* Tous les nombres de 1...n sont utilisés exactement une fois – une permutation valide.

L'algorithme fonctionne dans **O(n)** temps et utilise **O(1)** espace supplémentaire (en dehors du tableau de sortie).

---

## Code Snippets

### Java

"Java
Importation de java.util.*;

solution de classe {
construction publique[]Array(int n, int k) {
int[] ans = nouvelle int[n];
Int idx = 0;

// 1. Préfixe avec 1 ... N-K- 1
pour (int v = 1; v < n - k; v++) {
[idx++] = v;
}

// 2. Zig‐zag pièce produisant k différences distinctes
pour (int i = 0; i <= k; i++) {
Si (i % 2 == 0) { // même i → prendre du côté inférieur
[idx++] = n - k + i / 2;
} autre { // impair i → prendre du haut
[idx++] = n - i / 2;
}
}
le retour des an;
}

// ---- Harnais d'essai simple (facultatif) ----
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(Arrays.toString(s.constructArray(3, 1)); // [1, 2, 3]
Système.out.println(Arrays.toString(s.constructArray(3, 2)); // [1, 3, 2]
}
}
«» "

Python

'`python
Solution de classe:
def construction Array(self, n: int, k: int) -> liste[int]:
ans = []
# Préfixe : 1 ... n-k- 1
(plage (1, n - k))

Le suffixe de Zig-zag
pour i dans la plage (k + 1):
i % 2 == 0 & #160;:
n - k + i // 2) # côté bas
Sinon:
Annexe(n - i // 2) # haut
retour et

♪ ---- Essai ----
si __nom__ == "__main__" :
s = Solution()
print(s.constructArray(3, 1)) # [1, 2, 3]
print(s.constructArray(3, 2)) # [1, 3, 2]
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> constructArray(int n, int k) {
vecteur <int> ans;
a. réserve(n);

// Préfixe: 1 ... n-k- 1
pour (int v = 1; v < n - k; ++v)
(v)

// Le suffixe de Zig‐zag
pour (int i = 0; i <= k; ++i) {
Si (i % 2 == 0) // pair -> côté bas
a. les données relatives à l'état de l'aéronef;
Autre // étrange -> côté supérieur
c) Le nom de l ' agent de contrôle (n - i/2);
}
le retour des an;
}
};

Int main() {
Solution s;
vecteur<int> a = s.constructArray(3, 1);
pour (int x : a) cout << x << '; // 1 2 3
Cout << '\n';
a = s.constructArray(3, 2);
pour (int x : a) cout << x << '; // 1 3 2
}
«» "

---

Article du blog – Le bon, le mauvais et le mauvais de la belle entente II

- Oui. 1. Titre & Meta (prêt à l'emploi)

**Titre**:
*Beau arrangement II – Une solution de LeetCode 667 étape par étape (Java, Python, C++)

**Description détaillée**:
Vous voulez ace LeetCode 667 ? Apprenez la construction gourmande «zig‐zag» pour Beautiful Arrangement II. Solutions Full Java, Python & C++, algorithme, cas de bord et conseils d'entretien. Parfait pour les entretiens d'ingénierie logicielle. (en milliers de dollars)

- Oui. 2. Présentation

Le problème *Beau arrangement II* est un favori parmi les intervieweurs d'algorithmes parce qu'il mélange un tour de permutation classique avec une nouvelle torsion sur le calcul des différences. Si vous cherchez à renforcer votre arsenal d'entrevues de codage, ce post vous donne:

* Un algorithme cupide (pourquoi ça marche).
* **Code source complet** en Java, Python et C++.
* Une plongée profonde dans **la complexité temps/espace**.
* Pièges communs, manipulation de cas de bord et conseils d'entrevue dans le monde réel.

Laissez plonger !

- Oui. 3. Récapitulation des problèmes

- Entrée: `n` (taille de la permutation) et `k` (nombre désiré de différences distinctes).
- Sortie : Toute permutation de `1 ... n` où le tableau des différences absolues entre les éléments adjacents contient **exactement des valeurs distinctes `k`**.

- Oui. 4. La perspective de l'avidité – Zig-Zag

> **Pourquoi zig-zag? **
> La plus grande différence que nous pouvons créer est `n-1`. En alternant entre le plus petit nombre non utilisé et le plus grand nombre non utilisé, on peut forcer la différence à diminuer de 1 à chaque fois :
> `n-k`, `n`, `n-k+1`, `n-1`, ...

Le modèle produit des différences: `k, k-1, ..., 1`. C'est `k` chiffres distincts – exactement ce que le problème exige.

- Oui. 5. Construction étape par étape

1. **Préfixe avec des nombres ascendants**
Utilisez les numéros `1` à `n-k-1`.
Pourquoi ? Ils génèrent une différence unique de "1", sans introduire de nouvelles différences distinctes.

2. ** Zig-zag les autres positions «k+1»* *
Texte
faible = n - k
élevé = n
résultat = []
pour i = 0 ... k:
i est égal: result.append(low + i/2)
sinon: result.append(high - i/2)
«» "
*La division entière `i/2` s'occupe de l'étape alternée de déplacement vers l'intérieur. *

3. **Combine**
Le tableau final est la concaténation du préfixe et de la partie zig‐zag.

- Oui. 6. Pourquoi l'algorithme est juste

*Toutes les différences produites par le préfixe sont `1`. *
*La partie zig-zag produit des différences qui diminuent strictement de `k` à `1`. *
Par conséquent, l'ensemble de différences distinctes est exactement « {1, 2, ..., k} » – « k » valeurs distinctes.

L'algorithme visite chaque entier de `1` à `n` exactement une fois, garantissant une permutation valide.

- Oui. 7. Analyse de la complexité

Étape Opérations Complexité
- C'est quoi ?
Loop "n-k-1" **O(n)**
Loop "k+1" **O(k)** Autres
Total –** Autres
* Espace: O(1)** auxiliaire (sortie d'éclairage)

La solution est optimale – nous ne pouvons pas battre le temps linéaire parce que nous devons toucher chaque élément au moins une fois.

- Oui. 8. Cas de bord et erreurs courantes

Édition Réparer
- C'est quoi ?
La boucle du préfixe devient vide (`n-k-1` = 0). Le code s'en occupe gracieusement; il suffit de démarrer zig‐zag dès le début. Autres
Le zig-zag utilise le motif correctement. Autres
L'utilisation de la division flottante au lieu de la division entier conduit à de mauvais indices. Utiliser `i/2` en Java, `i // 2` en Python, `i / 2` en C++ (depuis que la division `int` tronque). Autres
Autres Décommandement des pics bas/élevés.Le choix des deux côtés sur la même parité peut sauter les nombres. C'est la règle "Even → low, impair → high". Autres
Autres La soustraction de «élevé» ou l'ajout de «faible» peut dépasser «[1, n]».

- Oui. 9. Conseils d'entrevue

1. ** Expliquez l'intuition d'abord** – les intervieweurs aiment voir *pourquoi* vous choisissez une approche.
2. **Passer la permutation** sur papier. Écrivez le préfixe et zig‐zag côte à côte; montrez les différences qui en résultent.
3. **Parler de la complexité** – dire temps linéaire, espace supplémentaire constant.
4. **Demander des éclaircissements** si l'intervieweur est vague sur le fait que `k` est `0` (bien que les contraintes l'interdisent) ou sur l'ordre des différences.
5. **Afficher le code** dans la langue avec laquelle vous êtes le plus à l'aise, mais être prêt à traduire vers une autre langue sur place.

10 ans. Réflexions finales

Beau arrangement II présente un modèle puissant : *utilisez un préfixe contrôlé pour éviter un travail supplémentaire, puis un zig‐zag délibéré pour frapper exactement les valeurs distinctes requises*. C'est un excellent exemple de mélange d'une construction gourmande avec un raisonnement combinatoire – parfait pour les interviews par algorithme.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---

- Oui. 9. Conclusion

Vous avez maintenant :

* Trois solutions de code prêtes à la production.
* Un algorithme entièrement documenté qui est à la fois **simple** et **optimal**.
* Un article de blog qui est poli pour **moteurs de recherche** et **apprentissage**.

Que vous soyez en train de vous préparer à une entrevue avec un ingénieur logiciel senior, d'affiner vos compétences d'entrevue ou simplement de chercher à approfondir votre compréhension des astuces de permutation, le modèle *Beautiful Arrangement II* est incontournable. Utilisez-le, expliquez-le, et regardez-le impressionner les intervieweurs !

---

**P.S.** Essayez des tests aléatoires avec `n` jusqu'à `10^5` et confirmez le nombre de différences distinctes. N'hésitez pas à étendre le harnais de test dans n'importe quelle langue – l'algorithme est robuste et assez rapide pour toutes les contraintes.

Bonne chance, et le codage heureux!