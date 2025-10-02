---
Titre: LeetCode 3659. Répartition dans les groupes K-Distinct -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3659. Répartition dans les groupes K‐Distinct – Solution, Code et Blog

> **Problème (Code de débit 3659)**
> Compte tenu d'un tableau entier `nums` et d'un entier `k`, déterminer si tous les éléments de `nums` peuvent être séparés en un ou plusieurs groupes de telle sorte que:
> 1. Chaque groupe contient **exactement des éléments k**.
> 2. Tous les éléments d'un groupe sont **distinct**.
> 3. Chaque élément de «nums» est utilisé **exactement une fois**.
> Retourner `true` si une telle partition existe, sinon `faux`.

La solution ci-dessous est écrite en **Java**, **Python** et **C++**.
L'article qui suit explique l'intuition, les pièges communs et les cas de bord délicats.
L'article est optimisé par SEO pour le succès de l'entrevue (mots clés: *LeetCode 3659*, *partition array k separate groups*, *hashmap solution*, *Java/Python/C++ interview problem).

---

L'idée de base – la bonne

1. **Nombre de groupes**
*Si nous avons `n = nombres.longueur` items et chaque groupe doit avoir exactement `k` items, puis nous avons besoin `n % k == 0 ' groupes. *
Si cette condition échoue, la réponse est instantanément "faux".

2. **Fréquence liée**
*Chaque valeur distincte peut apparaître au plus une fois dans un seul groupe. *
Par conséquent, si une valeur se produit temps `cnt`, nous avons besoin au moins groupes `cnt` pour les placer tous.
Le nombre de groupes disponibles est `n / k`.
Par conséquent, **`cnt` ne doit pas dépasser `n / k`** pour toute valeur.

3. ** Décision finale**
Si la taille du tableau est un multiple de `k` **et** aucune fréquence ne dépasse `n/k`, la partition est toujours possible – nous pouvons simplement distribuer chaque copie d'une valeur dans un groupe différent.

Cette logique est à la fois **O(n)** temps et **O(n)** espace (hash map).

---

Code

- Oui. 1. Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe {
partition publique booléenneArray(int[] nums, int k) {
int n = longueur nums;
si (n % k != 0) retourner faux; // les groupes doivent faire partie intégrante

groupes int = n / k;
Carte<integer, integer> freq = nouveau HashMap<>();

pour (int v : nombres) {
freq.put(v, freq.getOrDefault(v, 0) + 1);
si (freq.get(v) > groupes) { //
retourner faux;
}
}
retour vrai;
}
}
«» "

- Oui. 2. Python

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def partition Array(self, nombres: List[int], k: int) -> C'est vrai.
n = len(nums)
si n % k:
retour Faux # ne peut pas se diviser en groupes complets

groupes = n // k
freq = compteur(s)

retourner tous(c <= groupes pour c dans freq.values())
«» "

- Oui. 3. C++

'`cpp
#inclut <non-ordonné_map>
#incluez <vecteur>

solution de classe {
public:
Partition boolArray(std::vector<int>& nums, int k) {
int n = nombres.size();
si (n % k != 0) retourner faux; // les groupes doivent être entiers

groupes int = n / k;
std::unordered_map<int, int> freq;

pour (int v : nombres) {
si (++freq[v] > groupes) retourner faux; // violation du casier
}
retour vrai;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et l'acharnement de partager une représentation dans des groupes K-Distinct

Introduction

Si vous préparez une entrevue d'ingénierie logicielle, le problème **LeetCode 3659** est un bon point : il teste votre capacité à combiner des structures de données de base avec un raisonnement combinatoire. Dans cet article, nous allons disséquer le problème, marcher à travers une solution propre en Java, Python, et C++, et explorer les erreurs communes (-) et les pièges subtils (-) . Nous finirons avec des étiquettes SEO-friendly qui vous aideront à atterrir ce prochain appel d'entrevue.

---

- Oui. 1. Récapitulation des problèmes (bon)

> *Given `nums` et `k`, pouvons-nous partitionner `nums` dans des groupes de taille `k` avec des éléments distincts dans chaque groupe? *

Points clés à retenir :

- **Les groupes complets seulement** – vous ne pouvez pas laisser n'importe quel élément inutilisé.
- ** Distinct** – au sein d'un groupe, chaque valeur doit être unique.
- **Aucune contrainte de taille du groupe** – les groupes peuvent être n'importe quel nombre tant qu'ils contiennent chacun des éléments « k ».

---

- Oui. 2. Observations – Le principe du trou de Pigeon

- **Compte de groupes**: Si `n` n'est pas divisible par `k`, il n'y a aucun moyen de diviser en groupes de taille égale.
**→ Vérification rapide** : `n % k != 0` → `faux`.

- **Cap de fréquence**: Supposons que le nombre `5` apparaît 4 fois et que vous n'ayez que 3 groupes (`n/k = 3`). Au moins un groupe devrait contenir deux « 5 » – violant la distinction.
**→ Vérification**: Pour chaque valeur `x`, `freq[x]` doit être ≤ `n/k`.

La combinaison de ces deux contrôles est à la fois nécessaire et suffisante.

---

- Oui. 3. Algorithme et complexité (bon)

Texte
1. n ← longueur(s)
2. si n % k != 0 → retourner faux
3. groupes ← n / k
4. Compter les fréquences avec une carte de hachage
5. Si une fréquence > groupes → retourner faux
6. retour vrai
«» "

- **Heure**: `O(n)` – un seul passage pour compter.
- **Espace**: `O(n)` – la carte de hachage contient au plus `n` les clés distinctes.

---

- Oui. 4. Pièges communs – La mauvaise

Pourquoi il échoue
- C'est quoi ?
Le tri ne respecte pas la règle *distinct* entre les groupes. Utilisez plutôt le compte de fréquence. Autres
**Ignorer `n % k`**= Vous pouvez retourner `true` pour `[1,1,2]`, `k=2` (parce que les nombres correspondent), mais vous ne pouvez pas former de groupes complets. Toujours effectuer le contrôle de divisibilité d'abord. Autres
Autres **Utiliser `maxFrequence > k`**=_________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________ Autres
**Les compteurs mobiles en récursion** Une approche itérative avec un hashmap est plus propre. Autres

---

- Oui. 5. Les causes de bord – Le

- **Tous les éléments sont égaux** (`nums = [1,1,1,1]`, `k=2`) → `n/k = 2`, `freq[1] = 4` > 2 → `false`.
- **Valeurs maximales autorisées** ('nums.longueur = 10^5', chaque valeur jusqu'à `10^5') → Assurez-vous que votre hashmap/Counter peut gérer cette taille.
- **k = 1** → trivial; juste besoin `n % 1 == 0` (toujours vrai) et `max freq <= n`. Toujours `true`.
- **k = n** → un groupe; condition réduit à tous les éléments distincts → vérifier `max freq == 1`.

---

- Oui. 6. Pensées finales

L'élégance de ce problème réside dans deux simples observations mathématiques. Une fois que vous les voyez, la solution est une seule passe sur le tableau. Le vrai défi de l'entrevue est de se rappeler la distinction *fréquence cap* par rapport à *nombre de groupes* et d'éviter les hacks cupides ou récursifs trop compliqués.

---

- Oui. 7. Liste de contrôle du référencement (Boom de l'entrevue)

- **Titre**: Code de cap 3659 – Partition dans K‐Distinct Groupes : Java, Python, C++ Solutions & Conseils d'entrevue
- **Meta Description**: LeetCode Master 3659 en minutes! Lisez notre parcours détaillé, obtenez le code Java/Python/C++ et apprenez à aser l'interview. (en milliers de dollars)
- **En-têtes**: H1 (problème), H2 (Observations, Algorithme, Pièges, Cas d'Edge), H3 (Code Snippets)
- **Mots-clés**: *Code Leet 3659*, *Tableau de partitions*, *K groupes distincts*, *solution de plan de vol*, *Codage de l'entrevue de Java*, *Codage de l'entrevue de python*, *C++
- ** Liens internes**: Lien vers d'autres messages de solution LeetCode si une partie d'une série de blogs.
- ** Liens externes** : référencez la page de problème officielle LeetCode et les fils de solution les mieux notés.

---

- Oui. 8. A emporter

- **Rappel**: `n % k == 0` et `maxFreq <= n / k`.
- **Mise en oeuvre**: Un compteur de fréquence de passage unique – c'est tout ce dont vous avez besoin.
- **Pratique**: Essayez des variations comme la partition en groupes de taille `k` avec au moins un duplicata pour approfondir votre compréhension.

Bonne chance pour votre voyage d'entrevue – et un codage heureux! C'est ce qu'il a dit.

---

*Préparé par [Votre nom], ingénieur logiciel et coach d'entrevue*