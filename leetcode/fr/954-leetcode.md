---
Titre: LeetCode 954. Tableau des paires doubles -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 954. Array des paires doubles – Les bons, les mauvais et les méchants

> **Objectif:**
> Compte tenu d'un tableau entier de longueur uniforme `arr`, déterminez s'il peut être réordonné de façon à ce que chaque élément `x` soit suivi de son double `2x`.
> Officiellement, nous avons besoin d'une permutation d'"arr" telle que
> `arr[2*i+1] == 2 * arr[2*i]` pour tous `0 <= i < arr.longueur/2`.

---

- Oui. Pourquoi ce problème compte pour une entrevue

- ** Concepts de base:** cartes de hachage, gourmandise, tri, manipulation de nombres négatifs, cas de bord (zéros).
- ** Modèle d'entrevue commune :** Peut-on coupler chaque élément avec son double/la moitié ? (en milliers de dollars)
- **Compétences prêtes à l'emploi:** conception d'algorithmes, analyse de complexité, mise en œuvre propre en plusieurs langues.

---

- Oui. 1. Les bonnes

Qu'est-ce que c'est ?
-- -- -- -- -- -- -- -- -- -- -- -- -- --
**Idée simple**=Utiliser les nombres de fréquences + l'ordre de valeur absolue=Poignées positives, négatives et zéros uniformément==
**Complexité du temps** Autres
Autres **Complexité spatiale**
**Déterministe**
**Réutilisable**

---

- Oui. 2. Les mauvais

Pourquoi il peut vous faire monter Comment éviter
- C'est quoi ?
**La manipulation des zéros**
**Nombres négatifs**= Si vous traitez d'abord les grands négatifs, vous pourriez consommer leur moitié prématurément.
**Les plus grands entiers**=2 * x` peuvent déborder de 32 bits lorsque `x = 105`=Utilisez 64 bits (`long`/`long long`) pour le contrôle de multiplication ou pour un type plus grand.
Dans certaines langues, la carte n'est pas ordonnée, ce qui peut conduire à des résultats incohérents.

---

- Oui. 3. L'Ugly

"Piège" Ce qui ne va pas
C'est-à-dire
**Mutable map pendant l'itération**
Autres **L'utilisation d'une liste de clés seulement**= Si vous sautez un élément qui a encore le compte, vous manquerez les futures appariements== Loop sur le tableau (ou la liste triée) et vérifier la fréquence actuelle avant de procéder==
**Int vs Long débordement**= `int` * 2 peut dépasser `int` Valeur max==Promouvoir `long` lors du calcul `2 * x`=
** Mi-pairs manquants pour des comptages impairs** L'algorithme détectera les partenaires insuffisants lorsqu'il tentera de coupler le deuxième 4

---

- Oui. 4. Solutions complètes

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.
Tous utilisent la même stratégie de haut niveau :

1. Comptez la fréquence de chaque entier.
2. Trier les nombres par leur valeur absolue.
3. Pour chaque nombre, essayez de le jumeler avec son double, la décrémentation compte au fur et à mesure.

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe {
public boolean canReorderDoubled(int[] arr) {
// 1. Carte des fréquences
Carte<integer, integer> freq = nouveau HashMap<>();
pour (int x : arr) {
freq.put(x, freq.getOrDefault(x, 0) + 1);
}

// 2. Tri par valeur absolue
Liste <Integer> triée = nouvelle liste d'array<>(freq.keySet());
trié.sort(Comparator.comparingInt(Math::abs));

// 3. L'appariement de l'avidité
pour (int x : trié) {
int countX = freq.getOrDefault(x, 0);
si (compteX) 0) continuer; // déjà utilisé

int doubleX = x * 2; // safe: x <= 1e5, donc double <= 2e5
int countDouble = freq.get OrDefault(doubleX, 0);

si (countDouble < countX) retourner faux; // pas assez de partenaires

// consommer les paires
freq.put(x, 0);
freq.put(doubleX, countDouble - countX);
}

retour vrai;
}
}
«» "

> **Astuce:** Utilisez `long` pour le calcul `doubleX` si vous vous attendez à des valeurs proches de `Integer. MAX_VALUE'.

---

4.2 Python

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def canReorderDoubled(self, arr: List[int]) -> bool:
freq = contre(arr)

# Nombres de processus par valeur absolue ascendante
pour x dans trié(freq, key=abs):
Si freq[x] == 0:
poursuivre

double_x = x * 2
si freq[double_x] < freq[x]:
Retour Faux

freq[double_x] -= freq[x]
freq[x] = 0

retour Vrai
«» "

> **Pourquoi triés par `abs`?**
> S'assure que si `x` est la plus grande grandeur d'une paire (`-4` et `-8`), nous traitons `-4` d'abord, donc `-8` est toujours disponible.

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool canReorderDoubled(vector<int>& arr) {
unordered_map<long long, int> freq;
pour (int x : arr) freq[x]++;

// Tri par valeur absolue
Tri(arr.begin(), arr.end(), [](int a, int b) {
retourner llabs(a) < llabs(b);
});

pour (int x : arr) {
Si (freq[x]] 0) continuer; // déjà utilisé
longue longue doubleX = 2LL * x; // utiliser 64-bit pour éviter le débordement
si (freq[doubleX] < freq[x]) retourner faux; // pas assez de partenaires

freq[doubleX] -= freq[x];
freq[x] = 0;
}
retour vrai;
}
};
«» "

---

- Oui. 5. Analyse de la complexité

Métrique
- C'est quoi ?
(le tri domine) Autres
**Space**"O(n)" (hash map + tried list)""O(n)"""O(n)" Autres

---

- Oui. 6. SEO–Résumé amical

- **Titre:** Description des paires doubles – 954= Solution de LeetCode (Java, Python, C++)
- **Méta—Description:** Découvrez l'approche gourmande pour résoudre LeetCode 954 – Array of Doubled Pairs. Voir les exemples de code Java, Python et C++, l'analyse de complexité et les conseils d'entrevue. (en milliers de dollars)
- **Mots clés:** LeetCode 954, Tableau des paires doubles, carte de hachage, algorithme gourmand, préparation d'entrevue, interview de codage, solution Java, solution Python, solution C++
- ** Structure de l'en-tête :**
- H1: Tableau des paires doubles – 954
- H2 : Déclaration de problème
- H2: Points de vue clés (bon / mauvais / mauvais)
- H2: Code complet (Java / Python / C++)
- H2 : Analyse de complexité
- H2 : Conseils d'entrevue

> **Pourquoi ça vous aide à décrocher un emploi? * *
> En maîtrisant ce problème classique d'appariement des paires et en présentant une solution propre et multilingue, vous démontrez :
> * une forte compréhension des structures de données (cartes hash, compteurs),
> * capacité à raisonner sur les cas de bord (zéros, négatifs, débordement),
> * expérience en écriture claire, commenté code qui est facile à examiner.
> Tous sont très recherchés par les recruteurs de haute technologie.

---

- Oui. 7. Liste de contrôle à emporter

- [ ] Compter les fréquences avec une carte de hachage / compteur.
- [ ] Trier par valeur absolue, pas par valeur brute.
- [ ] L'appariement de l'avidité : consommer des comptes en un seul passage.
- [ ] Poignez zéro comme cas spécial (même nombre).
- [ ] Utilisez l'arithmétique 64 bits pour `2 * x` si nécessaire.
- [ ] Essai sur les cas bord:
- `[0, 0]` → `true "
- `[1, 2, 2, 4]` → `vrai "
- `[1, 2, 4, 8]` → `faux "
- `[-1, -2, -4, -8]` → `true "

---

La pensée finale

Le problème des paires doubles est un microcosme de nombreux défis d'entrevue : il faut penser en termes de *paires*, respecter *commander les contraintes* et se méfier des pièges comme **zéros** et **nombres négatifs**. La maîtrise de ce problème vous donnera confiance pour toute une classe de questions de pairing, qui apparaissent fréquemment sur les entrevues de codage.

Bonne chance, codage heureux, et que votre fonction `canReorderDoubled` retourne toujours `true` pour les bonnes entrées!