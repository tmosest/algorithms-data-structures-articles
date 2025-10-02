---
titre: LeetCode 484. Trouver la permutation - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Leetcode 484 – Trouver la permutation
Le bon, le mauvais et le mauvais de résoudre un problème d'entrevue classique
*Python C++ – temps O(n), espace auxiliaire O(1)*

---

### TL;DR
* **Problème** – Construisez la permutation lexicographiquement la plus petite de `[1 ... n]` qui satisfait à un modèle de "I" (augmentation) et "D" (diminution).
* **Solution** – Scanner la chaîne une fois, et chaque fois qu'on trouve une série de -D-s consécutifs, inverser ce segment de l'ordre naturel `[1, 2, ...]`.
* **Pourquoi ça compte** – La technique de la cupidité ou de la glissade est un modèle fréquent dans les entrevues (arras, piles, cupidité). La maîtrise montre que vous pouvez traduire une chaîne de contraintes en une commande optimale dans le temps linéaire.

---

- Oui. 1. Récapitulation des problèmes

> **Input**: `s` – une chaîne de longueur *n‐1*, chaque caractère est soit `'I'` ou `'D'`.
> **Output**: la permutation lexicographiquement la plus faible `perm` de `[1 ... n]` qui satisfait
> `` "
* S[i] == 'I' φ perm[i] < perm[i+1]
> s[i] == 'D' φ perm[i] > perm[i+1]
> `` "

> **Constraints**
1 ≤ longueur ≤ 105
> * contient uniquement `'I'` ou `'D'`

> **Exemple**
> `s = "DI"` → `[2, 1, 3]` (la plus petite parmi `[2,1,3]` et `[3,1,2]`)

---

- Oui. 2. Le point de vue sur l'avidité

*Si nous ignorons les contraintes pendant un moment, l'ordre naturel `[1,2,3,...]` est la permutation lexicographiquement la plus petite. *

Une série de forces ''D '' a une sous-séquence ** de diminution**.
Dans une subséquence décroissante, la plus petite permutation lexicographique est obtenue par **réversation** qui se déroule.

**Pourquoi l'inversion fonctionne* *
* Supposons que nous ayons une exécution `DI...I` de la longueur `k+1` commençant par l'index `i`.
* Les numéros qui occuperont des positions `i ... i+k` sont les numéros naturels `k+1` suivants: `i+1, i+2, ..., i+k+1`.
* Reversing donne `i+k+1, ..., i+2, i+1`, qui est le plus petit arrangement qui est strictement décroissant.

Ainsi, l'algorithme entier se réduit à:

«» "
perm = [1, 2, ..., n]
pour chaque bloc maximum consécutif «D» [l ... r] en s:
vers l'arrière[l ... R+1]
retour permanent
«» "

L'astuce est d'effectuer l'inversion **en place** tout en scannant la chaîne, en évitant une pile explicite ou un tableau supplémentaire.

---

- Oui. 3. Les trois applications idiomatiques

Voici des solutions propres et prêtes à la production en Java, Python et C++.
Tous exécutés dans le temps `O(n)`, utilisez seulement le tableau de sortie comme espace auxiliaire (`O(1)` extra).

---

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int[] findPermutation(String s) {
int n = s.longueur() + 1;
int[] perm = nouvelle int[n];

// Remplir d'ordre naturel 1..n
pour (int i = 0; i < n; ++i) perm[i] = i + 1;

i = 0; // indice courant en s
pendant que (i < s.longueur()) {
si (s.charAt(i) == 'I') { // rien à faire
i++;
poursuivre;
}

// nous avons fait une course "D". Trouver sa fin
début int = i;
alors que (i < s.leng() && s.charAt(i) == 'D') i++;

// Perm inverse[démarrer ... i] (inclus)
int gauche = début, droite = i;
pendant que (à gauche < à droite) {
int tmp = perm[gauche];
perm[gauche] = perm[droite];
perm[right] = tmp;
gauche++;
droit...
}
}

retour permanent;
}

// harnais d'essai simple
public statique vide principal(String[] args) {
Système.out.println(Arrays.toString(
nouvelle solution().findPermutation("DI")); // [2,1,3]
Système.out.println(Arrays.toString(
nouvelle solution().findPermutation("I")); // [1,2]
}
}
«» "

**Pourquoi il s'agit de l'implémentation Java d'Offre* *

Fonctionnalité
- Oui.
Autres Temps de passage simple
Autres Pas de pile auxiliaire ou de liste espace
Autres intention claire: remplissage naturel + renversement sélectif

---

3.2 Python

'`python
def find_permutation(s): str -> list[int]:
n = len(s) + 1
perm = liste (1, n + 1) # ordre naturel

i = 0
alors que i < len(s):
si s[i] == "Je":
i += 1
poursuivre

début = i
alors que i < len(s) et s[i]== "D":
i += 1

# inverse perm[départ : i+1] en place
perm[start:i+1] = inversé(perm[start:i+1])

retour permanent

♪ Démo
si __nom__ == "__main__" :
print(find_permutation("DI")) # [2, 1, 3]
print(find_permutation("I") # [1, 2]
«» "

L'attribution de la tranche de Python avec `reversed()` donne un renversement d'un liner – la manière *Pythonic*.

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findPermutation(chaîne s) {
int n = s.size() + 1;
vecteur <int> perm(n);
iota(perm.begin(), perm.end(), 1); // 1, 2, ..., n

i = 0;
pendant que [i < (int)s.s.ize()) {
si (s[i] == 'I') { ++i; continuer; }

début int = i;
pendant que (i < (int)s.size() && s[i] == 'D') ++i;

// inversement perm[démarrer .. i]
inverse(perm.degin() + début, perm.degin() + i + 1);
}
retour permanent;
}
};

Int main() {
Solution sol;
auto res = sol.findPermutation("DI");
pour (int x : res) cout << x << '; // 2 1 3
Cout << '\n';
}
«» "

C++ `iota` et `reverse` maintiennent le code terse et efficace.

---

- Oui. 4. Les bons, les mauvais et les méchants

Étape Ce qui arrive Comment éviter la douleur
Il y a un problème.
**Le Bon**=Une seule passe linéaire, seulement des opérations entières, pas de conteneurs supplémentaires. Utilisez des helpers intégrés (`iota`, `revers`, assignation de tranches) pour garder le code lisible. Autres
**Le mauvais**=Essai de construire une pile manuellement conduit à des bogues **off‐by‐one** et des facteurs constants plus élevés. Si vous avez besoin d'une pile, utilisez un `deque` ou `vector<int>` et pop/push soigneusement. Autres
**L'Ugly**=Le mélange de la logique de "reverse" à l'intérieur d'une boucle intérieure qui modifie également le tableau peut créer des boucles imbriquées déroutantes. Séparer la logique : 1) identifier le bloc `'D``, 2) effectuer un seul renversement. 3) Continuez à scanner. Autres

> **Conseil d'entrevue** – Si vous êtes déjà demandé de *expliquer* cette solution, commencez par écrire l'ordre naturel, alors montrez comment un `D` exécute force un renversement. Afficher un diagramme rapide d'une chaîne d'échantillons: `D D I I D` → `[1 2 3 4 5 6]` → inverser les positions 0-2 → `[3 2 1 4 5 6]` → continuer.

---

- Oui. 5. Cas de bord et complexité

Résultat
C'est quoi ?
« s » = « I » « [1, 2] » Autres
"s` = "D" """ "[2, 1]" Autres
Tous les "I`s" "[1, 2, ..., n] "
Tous les "D`s" `[n, n-1, ..., 1]` Autres

**Complexité* *

Métrique
- C'est quoi ?
Heure Autres
Espace "O(1)" (réseau de sortie) Autres

La contrainte de taille d'entrée (105) est manipulée confortablement dans les trois langues.

---

- Oui. 6. Bonus – Une pile– Variante fondée (pour examen)

Une solution classique de "stack" pousse les indices sur une pile chaque fois qu'un `'I'` ou fin de chaîne est vu, puis les pop pour définir des valeurs.
Bien que toujours `O(n)`, il utilise une pile supplémentaire de taille `O(n)` et peut être légèrement plus lent dans la pratique en raison des frais de mémoire.

"Java
Stack<integer> m = nouveau Stack<>();
valeur int = 1;
pour (int i = 0; i <= s.longueur(); i++) {
le point i) est remplacé par le texte suivant:
Si (i) s.longueur()S.charAt(i)== 'I') {
pendant que (!st.isEmpty()) perm[st.pop()] = val++;
}
}
«» "

Utilisez ceci seulement si vous êtes explicitement demandé de démontrer l'utilisation de la pile, sinon l'inversion de la fenêtre coulissante est plus propre.

---

- Oui. 7. SEO & Career‐Boosting Takeaway

1. **Mots clés** – *Leetcode 484, Trouver la permutation, pile gourmande, temps linéaire, problème d'entrevue, solution Java Python C++, algorithme O(n), codage d'entrevue d'emploi*
2. **Titre** –**Master Leetcode 484: Trouver la permutation – Greedy en Java, Python & C++*
3. **Description de la Meta** – *Apprendre le moyen le plus rapide de résoudre le Leetcode 484, Voir les implémentations Java, Python et C++, l'analyse de complexité et les explications prêtes à l'entretien. *

> **Pourquoi cela importe pour les recruteurs** – Le modèle de traduction d'une contrainte de chaîne en un ordre de tableau est une question d'entrevue fréquente pour les rôles d'ingénierie logicielle. Démontrer une solution O(n) claire dans plusieurs langues montre la polyvalence et la fluidité algorithmique.

---

- Oui. 8. Pensées finales

* Gardez le code **simple**: ordre naturel + retournements ciblés.
* Testez avec quelques exemples faits à la main, en particulier les cas de bord.
* Lorsque vous discutez dans une entrevue, passez à travers l'exemple sur un tableau blanc, montrant comment chaque `'D` fonctionne retourne un segment.

Bon codage – et bonne chance pour ce prochain travail! C'est ce qu'il a dit