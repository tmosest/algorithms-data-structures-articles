---
titre: LeetCode 3318. Trouver X-Sum de tous les K-Long Subarrays I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Solution – Trouver X-Sum of All K‐Long Subarrays
**LeetCode 3318 ** **Facile** ≤ 50'

---

Récapitulation des problèmes
Compte tenu d'un tableau entier `nums`, de la taille de la fenêtre `k` et d'une valeur `x`, nous devons:

1. Comptez combien de fois chaque élément apparaît.
2. Gardez seulement les éléments les plus fréquents.
* Si deux nombres ont la même fréquence, la plus grande valeur gagne.
3. Sommer les éléments conservés (multiplier chaque nombre par sa fréquence).
4. Retournez un tableau de ces sommes pour chaque fenêtre coulissante.

Si une fenêtre a moins de valeurs distinctes `x`, le résultat est simplement la somme de la fenêtre entière.

---

Aperçu de l'algorithme

1. **Fenêtre coulissante** – déplacer une fenêtre de taille `k` dans le tableau une fois.
2. **Carte de fréquence** – maintenir une `Carte<entier, entier>` pour la fenêtre actuelle.
3. **Priorité file d'attente / tas** – créer un max-heap clé par
* fréquence supérieure → priorité supérieure
* fréquence égale → plus grande valeur → priorité plus élevée.
4. **Pop top x** éléments du tas, ajouter `valeur * fréquence` à la réponse.
5. Répétez jusqu'à ce que la fenêtre atteigne la fin.

Parce que `n ≤ 50`, nous reconstruisons le tas pour chaque fenêtre – encore assez rapide
('O((n‐k+1) * k log k)' - quelques microsecondes) et beaucoup plus simple à raisonner.

---

La complexité

Mesure Temps Espace
- C'est quoi ?
"O(k log k)" (bâtir un tas)
"O((n-k+1) * k log k)""

Avec les contraintes données, l'algorithme est facilement sous-seconde dans n'importe quelle langue.

---

## 3--Cas de bord et pièges

Numéro
C'est quoi ?
`x` correspond au nombre de valeurs distinctes Le tas contiendra simplement toutes les valeurs – correcte. Autres
Autres Fenêtre a moins de `x` nombres distincts. Autres
Dupliquer les nombres avec la même fréquence. Autres
Nombres négatifs (pas dans les contraintes) Autres

---

- Oui. Mise en œuvre des références

Ci-dessous vous trouverez trois solutions complètes et compilables – **Java, Python, C++** – chacun suivant la même logique.

Autres **Conseil:**
> Dans les entrevues, discutez de la façon dont vous pourriez garder le tas *incrémentalement* pour atteindre `O(n log k)` au lieu de `O(n‐k+1) * k log k)`.
> Avec une telle taille d'entrée, l'approche simple de reconstruction par fenêtre est généralement préférée.

---

### 4.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe {
public int[] findXSum(int[] nums, int k, int x) {
int n = longueur nums;
int[] ans = nouvelle int[n - k + 1];
pour (int i = 0; i <= n - k; i++) {
ans[i] = calcul(nums, i, i + k, x);
}
le retour des an;
}

calcul(int[] nombres, int l, int r, int x) {
// l inclusive, r exclusive
Carte<integer, integer> freq = nouveau HashMap<>();
Int brutSum = 0;
pour (int i = l; i < r; i++) {
brut Somme += nombres[i];
freq.merge(nums[i], 1, entier::sum);
}

si (freq.size() <= x) {
retour brutSum; // tous les éléments restent
}

// Max-heap par fréquence, puis par valeur
PrioritéQueue<Map.Entry<entier, entier> pq =
nouvelle priorité <>(a, b) -> {
int cmp = Integer.compare(b.getValue(), a.getValue());
retour cmp != 0 ? cmp : Integer.compare(b.getKey(), a.getKey());
});

pq.addAll(freq.entrySet());

= 0;
pour (int i = 0; i < x; i++) {
Carte.Entrée<entier,entier> e = pq.poll();
sum += e.getKey() * e.getValue();
}
la somme de retour;
}
}
«» "

---

#### 4.2 Python 3 (Python 3.10+)

'`python
Importations provenant des collections Compteur
importation heapq
de taper l'importation Liste

Solution de classe:
def findXSum(self, nombres: List[int], k: int, x: int) -> Liste[int]:
n = len(nums)
res = []
pour i dans la plage (n - k + 1):
fenêtre = nombres[i:i + k]
res.append(self._top_x_sum(window, x))
retour res

def _top_x_sum(self, arr: List[int], x: int) -> Int:
cnt = contre(arrière)
si len(cnt) <= x:
retour sum(arr) # tous les éléments restent

# max-heap: (-freq, -valeur) -> pop plus grand freq, puis plus grande valeur
geap = [(-freq, -val) pour la val, freq en cnt.items()]
heapq.heapify

Total = 0
pour _ dans la plage(x):
freq_neg, val_neg = heapq.heappop(heap)
Total += -val_neg * -freq_neg
retour total
«» "

---

### 4.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findXSum(vector<int>& nums, int k, int x) {
int n = nombres.size();
vecteur <int> ans;
pour (int i = 0; i <= n - k; ++i) {
les données relatives à l'utilisation d'un système de gestion de l'information, y compris les données relatives à l'utilisation d'un système de gestion de l'information.
}
le retour des an;
}

particulier:
int calcule(vecteur const<int>& nombres, int l, int r, int x) {
unordered_map<int,int> freq;
Int brutSum = 0;
pour (int i = l; i < r; ++i) {
brut Somme += nombres[i];
++freq[nums[i]];
}

si ((int)freq.size() <= x)
retour brutSum; // garder tout

// max-heap: paire<freq, valeur> avec comparateur personnalisé
en utilisant P = paire<int,int>;
Auto cmp = [](const P& a, Const P& b) {
si (a.first != b.first) retourner a.first < b.first; // freq plus grand d'abord
retour a.seconde < b.seconde; // plus grande valeur d'abord
};
priority_queue<P, vector<P>, decltype(cmp)> pq(cmp);
pour (auto &kv : freq) pq.emplace(kv.second, kv.first);

= 0;
pour (int i = 0; i < x & & !pq.vide(); ++i) {
auto [f, v] = pq.top(); pq.pop();
la somme += v * f;
}
la somme de retour;
}
};
«» "

---

Article du blog – *Les bons, les mauvais et les méchants*
### Comment un problème de LeetCode 1 minuté peut vous poser un travail d'ingénierie logicielle

> **Objectif :** Rédigez un article concis et convivial sur le référencement qui vous aide à vous faire remarquer par les recruteurs.
> **Audience:** Ingénieurs de front, de back-end ou de stack complet à l'attaque **LeetCode 3318**.
> **Tone:** Amiable, dicté par les données et un peu d'humour.

---

5 idées d'orientation (chercheurs amis)

1. **=LeetCode 3318 Solution en Java, Python, & C++ – Un parcours complet* *
2. **=Trouver X‐Sum de K‐Long Subarrays – 3 versions de code + Conseils pratiques**=
3. Pourquoi maîtriser un petit problème de LeetCode peut stimuler votre score recruteur *

> *Conseil:* Utilisez le titre qui inclut le numéro exact de LeetCode – les recruteurs cherchent souvent par nom de problème ou ID.

---

Article complet

> **Titre:**
> **Le bon, le mauvais et le mauvais de LeetCode 3318: Un guide de l'emploi et de la lutte**

---

Introduction

À première vue, LeetCode 3318 *=Trouver X‐Sum of All K‐Long Subarrays I=2 semble être un casse-tête trivial.
Mais dans la salle d'entrevue, la profondeur de la conversation compte beaucoup plus que la vitesse du code.

Pourquoi ? Les recruteurs et les gestionnaires d'embauche ne sont pas seulement à la recherche de solutions *correctes* – ils chassent pour :

* **L'état d'esprit de résolution des problèmes** – capacité de décomposer une tâche et d'identifier les cas bord.
* ** Compétences en communication** – expliquer l'approche, les compromis et les pièges.
* ** Style de codage** – propre, durable et prêt à la production.
* **Passion pour apprendre** – curiosité pour optimiser et améliorer la solution.

Ci-dessous, nous déballons les aspects *Good*, *Bad* et *Ugly* de ce problème et comment vous pouvez transformer chacun en avantage d'embauche.

---

- Oui. Le bon – ce que vous faites

Autres Ce que vous faites Pourquoi ça compte
-- -- -- -- -- -- -- --
**Restatation claire du problème**= Affiche que vous pouvez saisir les exigences – la première étape à n'importe quel travail d'ingénierie. Autres
**Démontrer l'idée de la fenêtre coulissante** Autres
**Afficher les trois versions linguistiques**= Faits saillants de la fluidité des plateformes; les recruteurs aiment les candidats qui peuvent se déplacer entre les piles technologiques. Autres
Autres **Ajouter une analogie avec le monde réel** (p. ex., des articles fréquents de haut en haut = les produits les plus populaires dans un magasin) Autres

> *Recruter-friendly note:* *=Je peux résoudre un problème en Java, Python, et C++ – Je suis à l'aise avec plusieurs langues.

---

C'est vrai. Les mauvais – Des erreurs communes

Erreur Ce qui ne va pas Comment le réparer
- C'est quoi ?
**Seuils de codage à chaud** (par exemple, toujours `x == 1`) Paramètrez la logique, expliquez pourquoi `x` peut varier. Autres
**Manipulation de cas de bord d'émission** (tableau vide, `k==0`) Valider les entrées et gérer les cas d'angle explicitement. Autres
**En utilisant seulement une carte de hachage** Utilisez un comparateur qui tient compte des liens. Autres
Autres **Reconstruire le tas de toutes les itérations** Mentionnez une amélioration `O(n log k)` comme un bonus. Autres

> **Pro-tip:** Dans une vraie interview, dites *=I=d garder le tas à jour avec chaque quart de fenêtre, ce qui nous amène à O(n log k)=* et dessine l'idée sur un tableau blanc.

---

C'est pas vrai. L'horrible – Ce qu'il faut éviter (et comment récupérer)

Autres Scénario ulcéreux Pourquoi ça fait mal
- C'est quoi ?
**Code Spaghetti** (mélangeant des compteurs, des tas et des boucles sans fonctions claires) Refacteur en petites fonctions d'aide. Autres
**Commentaires manquants**=Ce qui rend votre code cryptique, particulièrement pour un recruteur qui pourrait skim. Ajouter de brèves explications en ligne. Autres
**Utilisation de langage non idiomatique** (par exemple, en utilisant `map` au lieu de `unordered_map` en C++ pour les petites entrées) Utilisez les conteneurs STL les plus courants pour la langue. Autres
** Nombres magiques de codage dur** (`-1`, `-5`) Prévient la réutilisation dans d'autres contextes. Utilisez des constantes nommées ou expliquez la logique. Autres

---

C'est vrai. Bonus : Comment transformer la discussion en question d'entrevue STAR

> **Situation:** On m'a présenté un problème de fenêtre coulissante où nous devions garder les éléments les plus fréquents. (en milliers de dollars)
> **Tâche :** J'avais besoin de produire une solution propre et prête à la production en plusieurs langues. (en milliers de dollars)
> **Action:** J'ai implémenté une carte de fréquence, reconstruit un lourd max pour chaque fenêtre et manipulé les liens par valeur. J'ai également esquissé comment garder l'accroissement du tas pour les performances O(n log k). (en milliers de dollars)
> **Résultat:** La solution fonctionne dans < 5 ms en Java, < 1 ms en Python et < 2 ms en C++. J'ai fait preuve de fluidité et de pensée algorithmique croisée, ce qui m'a fait appeler d'une entreprise technologique de premier plan. (en milliers de dollars)

---

Liste de contrôle du référencement (pour que les recruteurs puissent vous trouver)

Mots-clés Pourquoi ça compte Comment l'intégrer
-- -- -- -- -- -- -- --
*LeetCode 3318*= ID du problème exact – les recruteurs cherchent par numéro. Titre, premier alinéa, titres de code. Autres
*findXSum *= Nom de la fonction – correspond au nom de la solution LeetCode. Dans la section des explications de code. Autres
*Solution de Java*, *Solution de Python*, *Solution de C++* Des blocs de code séparés avec ces rubriques. Autres
*Fenêtre coulissante*, * file d'attente prioritaire*, *pape* Mentionnez-les dans la section "Bien". Autres
*Entretien de l'ingénieur logiciel*, *Entretien de codage*, *Conseils d'entrevue d'emploi* Parsemer naturellement dans l'introduction et la conclusion du blog. Autres

---

À emporter

*LeetCode 3318* peut sembler trivial, mais la façon dont vous **explore** il – identifier des compromis, manipuler des cas de bord, écrire un code multi-langue propre, et articuler votre processus de pensée – fait un jour recruteur.

Donnez le bon, mauvais, ugly, une explication claire et amicale, saupoudrer dans les mots-clés SEO ci-dessus, et vous aurez une vitrine convaincante pour votre prochaine interview. C'est ce qu'il a dit.

---

Bon codage, et que votre nombre d'offres d'emploi soit bientôt trop élevé!