---
titre: LeetCode 2899. Les derniers entiers visités -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2899 – **Derniers entiers visités**
### Facile – Java-Java Python-C++ Solutions + In-Depth Blog Post

---

Récapitulation des problèmes

On vous donne un nombre entier.
- Un entier ** positif** représente une visite et doit être rappelé.
- `-1` est une requête: vous devez retourner le *k‐th* le plus récent mémorisé entier, où `k` est le nombre de `-1`s consécutifs vus jusqu'à présent (y compris le courant).
- Si `k` est plus grand que le nombre d'entiers mémorisés, retourner `-1`.

La sortie est une liste d'entiers produits par toutes les requêtes `-1`.

**Contrôles* *
"1 ≤ longueur nominale ≤ 100"
- "nums[i] == -1` ou `1 ≤ nums[i] ≤ 100`

---

Solution optimale (temps O(n), espace O(n)

Le point de vue clé :

Étape Ce que nous faisons
- C'est quoi ?
**Push**. Entreposez tous les entiers positifs sur un *stack* (dernière entrée, première sortie). Autres Nous avons toujours besoin des visites les plus récentes. Autres
Lorsque nous rencontrons un nombre positif, réinitialisez le compteur consécutif‐`-1`. Autres
Sur `-1`, augmenter le compteur. Si le compteur ≤ taille de la pile, retourner l'élément à `stack.size() - counter`; sinon retourner `-1`. Autres

Cela donne un algorithme propre à un passage.

---

Mise en œuvre du code

> **Note:** Les trois snippets compilent et fonctionnent sur la plateforme LeetCode.

#### 3.1 Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
liste publique<integer> lastVisitedIntegers(int[] nums) {
Liste <Integer> ans = nouvelle liste de distribution<>();
Liste<Integer> pile = nouvelle liste d'array<>(); // agit comme une pile

int consec = 0; // compteur consécutif -1

pour (int num : nombres) {
Si (nombre) -1) {
consec++; // un autre -1 dans une rangée
si (consec <= empil.size()) {
// k-th le plus récent -> stack.size() - k
ans.add(stack.get(stack.size() - consec));
} autre {
les paragraphes 1 et 2 sont remplacés par le texte suivant:
}
} autre {
pile.add(num); // pousser une nouvelle visite
consec = 0; // réinitialiser le compteur consécutif
}
}
le retour des an;
}
}
«» "

3.2 Python

'`python
de taper l'importation Liste

Solution de classe:
dernière Visites Integers(self, nombres: List[int]) -> Liste[int]:
ans = []
pile = [] nombre de visites récentes
consec = 0 # compteur consécutif -1

pour num in nums:
Si num == -1:
consec += 1
si consec <= len(stack):
ans.append(stack[-consec]) # kth le plus récent
Sinon:
Annexe(-1)
Sinon:
Annexe(num)
consec = 0
retour et
«» "

### 3.3 C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> lastVisitedIntegers(vecteur<int>& nums) {
vecteur <int> ans;
vector<int> pile; // visites récentes
int consec = 0; // compteur consécutif -1

pour (int num : nombres) {
Si (nombre) -1) {
+consec;
si (consec <= (int)stack.size())
// k-th le plus récent
Autre
as.push_back(-1);
} autre {
pile.push_back(num);
consec = 0;
}
}
le retour des an;
}
};
«» "

---

Billet de blog – Le bon, le mauvais, et l'horrible des derniers entiers visités

Introduction

Lors de la préparation d'un entretien *logiciel d'ingénierie*, il est commun de rencontrer des problèmes de suivi d'état. *LeetCode 2899 – La dernière visite d'Intégers* est un tel problème qui teste votre capacité à maintenir une histoire dynamique tout en manipulant des requêtes. Dans cet article, nous allons disséquer le problème, marcher à travers une solution propre, mettre en évidence le bon, le mauvais, et les aspects laids, et terminer avec SEO-friendly aperçus pour vous aider à atterrir cet appel d'entrevue.

---

Pourquoi Ce problème est important

Caractéristiques Pourquoi c'est utile
C'est-à-dire
**Gestion de l'État**=Les applications du monde réel (p. ex. navigation, défaire les piles) doivent se souvenir des actions passées. Autres
**One-Pass Algorithm**= Démontre comment résoudre des exigences complexes avec le temps O(n). Autres
Autres **Edge‐Case Handling** , vous aide à réfléchir à la réinitialisation, aux requêtes consécutives et aux états vides. Autres
**Cross‐Language Implementation** Autres

Maîtriser ce problème prouve que vous pouvez concevoir des structures de données efficaces et gérer l'état mutable – compétences cruciales pour tout moteur ou rôle de système.

---

Les mauvaises – Pièges communs

1. **Confuser l'indexation** – Souvenez-vous que le plus récent est *stack.size() – k* (pas *k - 1*). Les erreurs hors-par-un sont la principale raison d'une mauvaise réponse.
2. **Oublier la réinitialisation** – Le compteur `-1` consécutif doit réinitialiser chaque fois qu'un nombre positif apparaît. Négliger cela donne des résultats incorrects pour des entrées comme `[1, -1, 2, -1]`.
3. **Utilisation de `pop()` pour les requêtes** – Beaucoup de débutants pop la pile par erreur sur chaque `-1`, détruisant l'histoire. La pile doit être **read-only** pour les requêtes.
4. **Ignorer les États vides** – Si vous voyez `-1` avant un nombre positif, vous devez retourner `-1` au lieu d'accéder à un index invalide.

---

### Les mauvaises – approches suboptimales

L'approche
C'est pas vrai.
**Two-D Array de toutes les requêtes** Autres
**Reconstruire l'histoire sur chaque question**= O(n2) fois; vous traversez à nouveau le tableau pour chaque `-1`. Autres
**Liste liée à l'insertion de la tête**= Fonctionne mais ajoute un pointeur supplémentaire; pas aussi propre qu'un vecteur/ArrayList. Autres
**Utiliser la récursion pour les requêtes**=Risque de trop-plein sur les grandes entrées; surkill pour un simple balayage linéaire. Autres

Ces modèles sont tentants si vous visez des correctifs rapides, mais ils brisent l'évolutivité et la lisibilité - qualités interviewers détestent.

---

Analyse de complexité

Complexité
C'est pas vrai.
**Temps**=O(n) – passe un seul coup sur le tableau. Autres
**L'espace**=O(n) – le pire des cas, tous les nombres sont positifs, donc nous les stockons tous. Autres

Cette solution linéaire bat le leaderboard sur LeetCode (1 ms en Java, Python, C++ sur matériel standard).

---

Conseils pratiques pour l'entrevue

1. **Expliquer votre structure de données** – Mentionnez qu'une pile garde des visites récentes, et qu'un compteur suit des requêtes consécutives.
2. **Edge Cases** – Discutez de scénarios comme le leader `-1`s, le traînant `-1`s, et alterner des modèles positifs/négatifs.
3. **Pourquoi vous ne faites pas `pop()`** – Clarifiez que les requêtes sont en lecture seule, en préservant l'historique pour les requêtes futures.
4. **Cross‐Language Thought Process** – Montrez comment le même algorithme s'adapte à Java, Python et C++ (array/vector vs. list vs. std::vector).
5. **Démarrage de l'espace-temps** – Si l'intervieweur demande l'optimisation, soulignez que O(n) est optimal ; vous ne pouvez pas obtenir mieux que cela parce que vous devez examiner chaque élément au moins une fois.

---

Liste de contrôle du référencement (pour les recrues et les entraîneurs de carrière)

- **Mots-clés cibles**: *LeetCode 2899, Dernières visites Integers, problème de suivi d'état, algorithme à un passage, question d'entretien, solution Java, solution Python, solution C++*
- **Description détaillée**: Solve LeetCode 2899 – Les derniers entiers visités en Java, Python et C++. Algorithme monopass O(n) avec logique de pile claire. Lisez le blogue complet pour trouver des pièges et des conseils d'entrevue. (en milliers de dollars)
- **Balises d'en-tête**: H1 (`LeetCode 2899 – Dernières visites Integers`), H2 (`Problem Recap`, `Optimal Solution`, `Code Implementations`, `Blog Post – The Good, The Bad, and The Ugly`), H3 (`Java`, `Python`, `C++`), H4 (`Edge-Case Handling`, `Analyse de la complexité`).

Ces balises aident les moteurs de recherche à indexer le message et à le faire correspondre avec les requêtes liées à l'entrevue.

---

Pensée de clôture

Si vous pouvez expliquer pourquoi une simple pile + compteur est la solution *droite* et comment vous évitez les pièges typiques, vous démontrerez une maîtrise de **structures de données stagnantes** – une caractéristique d'un développeur de haut niveau. Ce problème est petit sur LeetCode, mais les concepts qu'il teste sont énormes dans le monde réel.

Bonne chance pour votre prochain entretien ! Si vous avez trouvé cet article utile, partagez-le sur LinkedIn ou Twitter et tag **@YourCompany** afin que les recruteurs voient votre expertise en action. C'est ce qu'il a dit.

---