---
titre: LeetCode 1405. La plus longue chaîne heureuse -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1405. Longest Happy String – Solution 3 langues + SEO-optimized Blog

Ci-dessous vous trouverez une implémentation complète et prête à la production du problème **Longest Happy String** dans **Java, Python et C++**.
Après le code, un article de blog de plongée profonde explique l'algorithme, les avantages/cons, les pièges, et pourquoi maîtriser ce problème fera briller votre profil LeetCode aux recruteurs.

---

Code

> **Signature**
> `public String le plus long DiversString(int a, int b, int c)»

Java (JDK 17+)

"Java
Importation de java.util.*;

solution de classe publique {
public Chaîne plus longue DiversString(int a, int b, int c) {
// Max-heap ( file d'attente prioritaire) ordonnée par le nombre restant
PrioritéQueue<int[]> pq = nouveau PrioritéQueue<>(
(x, y) -> Compare entier(y[0], x[0]); // descendant

si (a > 0) pq.offre(nouvelle int[]{a, 'a'});
si (b > 0) pq.offre(nouvelle int[]{b, 'b'});
si (c > 0) pq.offre(nouvelle int[]{c, 'c'});

StringBuilder sb = nouveau StringBuilder();

pendant que (!pq.isEmpty()) {
int[] premier = pq.poll(); // le plus fréquent
le nombre d'int1 = premier[0];
char ch1 = (char) première[1];

// Si nous avons déjà deux ch1 consécutifs, utilisez la deuxième plus fréquente
si (longueur() >= 2 &&
sb.charAt(sb.longueur() - 1) == ch1 &&
sb.charAt(sb.longueur() - 2) == ch1) {

si (pq.isEmpty()) casse; // rien d'autre à utiliser

int[] deuxième = pq.poll();
char ch2 = (char) seconde[1];

sb.annexe(ch2);
si (--seconde[0] > 0) pq.offre(seconde); // recul si disponible

pq.offre(premier); // remise en premier
} autre {
sb.annexe(ch1);
si (--compte1 > 0) pq.offre(nouvelle int[]{count1, ch1});
}
}
retour sb.toString();
}

// Pour des tests rapides
public statique vide principal(String[] args) {
System.out.println(nouvelle solution().longestDiverseString(1, 1, 7));
System.out.println(nouvelle solution().longestDiverseString(7, 1, 0));
}
}
«» "

Python 3

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
plus longtemps DiversString(self, a: int, b: int, c: int) -> str:
# Le heapq de Python est un heap min; les comptes négatifs de magasin pour le heap max
pq: Liste[tuple[int, str]] = []
pour le nombre, l'omble en (a, a), b, b), c, c):
si compter > 0:
(-compte, char)

res = []

alors que pq:
count1, ch1 = heapq.heappop(pq)
count1 = -count1 # retour à positif

# Si les deux derniers caractères sont ch1, utilisez le suivant le plus fréquent
si len(res) >= 2 et res[-1] == ch1 == res[-2]:
si non pq:
Break # rien d'autre à utiliser

count2, ch2 = heapq.heappop(pq)
nombre2 = -nombre2

res.append(ch2)
si nombre2 - 1:
heapq.heappush(pq, (-(compte2 - 1), ch2))

# remettre en premier
(-compte 1, ch1)
Sinon:
res.append(ch1)
si nombre1 - 1:
heapq.heappush(pq, (-(compte1 - 1), ch1))

retour ''.join(res)

# Démo rapide
si __nom__ == "__main__" :
s = Solution()
print(s.longestDiverseString(1, 1, 7))
print(s.longestDiverseString(7, 1, 0))
«» "

C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne plus longue DiversString(int a, int b, int c) {
Nombre maximal de paires {compte, char}
priorité_queue<pair<int, char>> pq;
si a) pq.push({a, 'a'});
si b) pq.push({b, 'b'});
si c) pq.push({c, 'c'});

la chaîne rés;

pendant que (!pq.vide()) {
auto [cnt1, ch1] = pq.top(); pq.pop();

// Vérifiez trois caractères consécutifs
si (res.size() >= 2 && res[res.size()-1) == ch1 && res[res.size()-2) == ch1) {
si (pq.vide()) casse; // rien d'autre à utiliser

auto [cnt2, ch2] = pq.top(); pq.pop();
résolution += ch2;
si (--cnt2) pq.push({cnt2, ch2});

pq.push({cnt1, ch1}); // remettre en premier
} autre {
res += ch1;
si (--cnt1) pq.push({cnt1, ch1});
}
}
retour rés;
}
};

Int main() {
Solution sol;
Cout << sol.longestDiverseString(1, 1, 7) << endl;
cout << sol.longestDiverseString(7, 1, 0) << endl;
retour 0;
}
«» "

> Les trois implémentations fonctionnent dans **O(a + b + c)** temps et **O(1)** espace supplémentaire (au-delà du tas d'au plus trois éléments).

---

Article du blog – Le bon, le mauvais, et l'atroce du LeetCode

> **Concentré des mots clés** : *La plus longue chaîne heureuse*, *LeetCode*, *Greedy Algorithm*, *Priority Queue*, *Interview Prep*, *La chasse à l'emploi*.

---

Introduction

LeetCodes **1405 – Longest Happy String** est un problème classique d'avidité qui teste votre capacité à équilibrer *fréquence* et *contraintes*. Bien qu'il puisse sembler simple à première vue, la maîtrise de ce problème révèle des idées profondes sur:

- ** Prise de décisions concernant la liberté* *
- **Structures de données** (Max-Heap / Priority Queue)
- **Traitement des affaires** (lorsque deux ou trois lettres sont sur le point d'apparaître)

Obtenir ce problème bien peut faire un recruteur d'yeux pop dans une pile de CV, surtout quand vous en parlez dans une interview technique.

---

Rétablissement du problème

> **Objectif**: Construisez la plus longue chaîne possible composée de «a», «b» et «c» de telle sorte que:
> 1. Pas de "aaaa", "bbb" ou "ccc" apparaît comme une sous-chaîne.
> 2. La chaîne utilise au plus `a` ‘a=s, `b` ‘b=s et `c` ‘c=s.
> 3. Retournez *toute* chaîne la plus longue (vide si impossible).

**Contrôles* *
`0 <= a, b, c <= 100`, `a + b + c > 0`.

---

C'est vrai. Le bien – Pourquoi une graisse + Heap fonctionne

Raison
C'est pas vrai.
**Sous-structure optimale**= À chaque étape, choisir le personnage le plus fréquent est toujours sûr – tout autre choix ne ferait que réduire la longueur restante. Autres
Autres **Simple État**. Seulement le compte courant et les deux derniers caractères comptent. Autres
**Complexité linéaire**= Chaque insertion de caractères est O(log 3) = O(1); temps total O(n). Autres
Autres **Efficacité de l'espace**Le tas contient au plus trois éléments; la chaîne de sortie est la seule grande structure. Autres
**Mise en œuvre claire**= Les cartes logiques naturellement à la prise, vérifier, remettre avec une file d'attente prioritaire. Autres

> **A emporter**: Greedy with a max-heap donne une solution **O(n)** qui est banale à raisonner et rapide dans la pratique.

---

C'est pas vrai. Les pièges communs

"Piège" "Ce qui ne va pas"
C'est-à-dire
Autres **Ne pas vérifier deux mêmes chars consécutifs. Après chaque appendice, vérifiez les deux derniers caractères; s'ils sont égaux au candidat actuel, passez au deuxième plus fréquent. Autres
**Ignorer les autres comptes** Après avoir décrémenté, réinsérer dans le tas seulement si le nouveau nombre est toujours positif. Autres
Pour `(a=0, b=1, c=2)`, vous devez gérer avec grâce le scénario "Une seule lettre gauche". L'algorithme sort naturellement lorsque le tas est vide; veillez à ce que l'état de la boucle vérifie le vide après un échange forcé. Autres
**L'utilisation d'un « heap » sans négation est un « heap » de type python; oublier de stocker des négatifs conduit à une mauvaise commande. Entreposez des nombres négatifs ou utilisez `heapq.nmest`. Autres
En supposant qu'O(n2) en raison de scans répétés pour la lettre la plus fréquente. Éviter les scans linéaires; toujours utiliser les opérations "poll()"/`offer()". Autres

---

C'est vrai. L'Ugly – Variations et Extensions avancées

1. **Nombreuses épreuves* *
- LeetCode=2 s'assure que vous réinitialisez le tas pour chaque test.

2. **Comptes importants (1 000 000)**
- Même si les contraintes disent ≤ 100, une interview réelle peut présenter des nombres plus importants.
- L'algorithme fonctionne toujours parce que les opérations de tas sont indépendantes de la magnitude du compte; seule la longueur de chaîne finale change.

3. **Nuances linguistiques particulières**
- **Java**: Rappelez-vous que `char` est 16-bit; le stocker comme `int` dans le tas pour maintenir la commande.
- **Python**: Utilisez `heapq.heappush`/`heappop` avec des nombres négatifs; évitez les conversions `int`‐to‐`char`.
- **C++**: Utilisez `std::priority_queue` de `pair<int, char>`.

---

C'est vrai. Discussion sur la préparation à l'entrevue

Lors d'un entretien technique, vous pouvez parcourir ce problème dans le style suivant:

1. ** Clarifier les contraintes* *
- On peut utiliser les trois lettres ? Et quand un compte est 0 ? (en milliers de dollars)

2. ** Expliquer le choix de l'avidité**
- Il choisit toujours le personnage avec la plus haute fréquence restante. (en milliers de dollars)

3. **Afficher la logique du tas**
- Il faut maintenir un maximum de « {compte, lettre} » et réinsérer après chaque décrément. (en milliers de dollars)

4. ** Mettre en évidence la vérification à deux caractères* *
- Si les deux derniers caractères sont les mêmes que mon candidat, je vais temporairement pop le second le plus fréquent et l'utiliser. (en milliers de dollars)

5. **Fournir des exemples de cas de bord**
- Pour l'entrée (7, 1, 0), l'algorithme produira «aabaaa» comme la plus longue chaîne valide. (en milliers de dollars)

6. **Analyse du temps et de l'espace**
- temps O(a + b + c), espace supplémentaire O(1). (en milliers de dollars)

Les recruteurs aiment quand les candidats peuvent discuter *pourquoi* la solution est optimale, pas seulement *comment* elle fonctionne.

---

- Oui. Pourquoi ce problème vous aide à trouver un emploi

Compétences Comment le problème s'entraîne
C'est ce que j'ai dit.
**La pensée algorithmique** Autres
**Structure de données Compétence**= Affiche le confort avec les files d'attente prioritaires, qui sont communes dans la conception système et le codage réel. Autres
Votre solution est propre, durable et bien documentée – caractère la valeur des recruteurs dans le code de production. Autres
Autres **La gestion du temps** Autres

> *Lorsque vous clouez 1405, vous montrez que vous pouvez gérer *contraintes* et *maximisation* en un seul passage – une combinaison rare qui se distingue sur un CV technique. *

---

- Oui. Bonus : Extension à 5 caractères

Si vous êtes curieux, la même logique cupide balance à **n-lettre heureux cordes** (`n <= 26`). La seule différence est:

- Le tas deviendra de plus en plus grand.
- La règle des "deux-consécutifs" reste identique.
- La complexité reste **O(longueur totale)**.

---

- Oui. Verdict final

- **Le Bon** – Rapide, optimal et conceptuelment élégant.
- **Le mauvais** – Nécessite une manipulation soigneuse de la règle de "deux consécutifs" et de la réinsertion.
- **Les Ugly** – Aucune ! (Lorsque la logique est correcte, l'implémentation est simple.)

**Maîtrisez ce problème, et vous n'aurez pas seulement ace LeetCode=s échelle de difficulté, mais aussi donner aux intervieweurs un exemple *déjà-fait* de **le raisonnement d'accord + file d'attente de priorité**—une recette que les recruteurs aiment.

---

Enveloppe

- Oui.
- C'est quoi ?
Solutions Java, Python, & C++ avec **O(n)** temps

N'hésitez pas à copier, courir et modifier les extraits de code.
Bon codage, et que votre prochaine interview soit -Happy - pour toutes les bonnes raisons!