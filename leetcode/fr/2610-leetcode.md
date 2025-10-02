---
titre: LeetCode 2610. Conversion d'un tableau en un tableau 2D avec conditions -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Voici des solutions propres et prêtes à la production pour LeetCode 2610
`Convertissez un tableau dans un tableau 2D avec conditions`.
Les trois solutions fonctionnent dans **O(n)** temps et utilisation **O(n)** espace auxiliaire.

> **Insight clé**
> Si un nombre apparaît `k` fois dans `nums`, il doit occuper `k` *différent* lignes.
> Par conséquent, la fréquence maximale ** de tout élément est exactement le minimum
> nombre de lignes que la matrice résultante doit contenir.

Pourquoi il est bon
-- -- -- -- -- -- -- -- -- -- -- -- --
**Java**= O(n)= O(n)= Utilise une `HashMap` pour le comptage et une liste de listes pour le résultat. Autres
**Python**= O(n)= O(n)= Collections de leviers. Counter» et liste des listes. Autres
**C++**= O(n)= O(n)= Utilise `unordered_map` et un `vecteur<vector<int>>. Autres

> Le code ci-dessous implémente l'algorithme *basé sur la fréquence* décrit dans le
> éditorial officiel.
> Il est plus facile à comprendre, ne nécessite pas de bibliothèques supplémentaires, et garantit la
> nombre minimal de lignes.

---

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<Liste<entier>> trouverMatrix(int[] nombres) {
// 1. Fréquences de comptage
Carte<integer, integer> freq = nouveau HashMap<>();
int maxFreq = 0;
pour (int x : nombres) {
int f = freq.getOrDefault(x, 0) + 1;
freq.put(x, f);
si (f > maxFreq) maxFreq = f;
}

// 2. Préparer des lignes vides (nombre min de lignes = maxFreq)
Liste <Liste<entier>> résultat = nouvelle liste <>();
pour (int i = 0; i < maxFreq; i++) résultat.add(new ArrayList<>());

// 3. Distribuer les numéros en lignes
pour (Map.Entry<Integer, Integer> entrée : freq.entrySet() {
int val = entry.getKey(), cnt = entry.getValue();
pour (int i = 0; i < cnt; i++) {
result.get(i).add(val); // placé dans la ligne i‐ième
}
}

le résultat du retour;
}
}
«» "

---

#### 1.2 Python

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def findMatrix(self, nombres: List[int]) -> List[List[int]]:
Nombre de fréquences
freq = compteur(s)
max_freq = max(freq.values())

2. Créer des lignes vides
résultat = [[] pour _ dans l'intervalle(max_freq)]

# 3. Remplir les lignes – chaque nombre occupe des lignes distinctes
pour la valeur, cnt en fréq. items():
pour i dans la plage (cnt):
résultat[i].appendice(val)

résultat du retour
«» "

---

*## 1.3 C++

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
#incluez <algorithme>

solution de classe {
public:
std::vector<std::vector<int>> findMatrix(std::vector<int>& nums) {
// 1. Fréquences de comptage
std::unordered_map<int, int> freq;
int maxFreq = 0;
pour (int x : nombres) {
int f = +freq[x];
maxFreq = md:max(maxFreq, f);
}

// 2. Préparer le résultat avec les lignes 'maxFreq'
std::vector<std::vector<int>> res(maxFreq);

// 3. Distribuer chaque valeur entre les lignes
pour (auto &p : freq) {
int val = p.first, cnt = p.second;
pour (int i = 0; i < cnt; ++i)
res[i].push_back(val); // placé dans la ligne i‐ième
}

retour rés;
}
};
«» "

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 2610

> **SEO Mots-clefs** – Leetcode 2610, Convertissez un tableau en 2D, Solution Java, Solution Python, Solution C++, Codage d'entretien d'emploi, Entretien d'algorithme, Conseils d'entretien de l'ingénieur logiciel, lignes minimales, algorithme de fréquence

---

Introduction

Vous venez de résoudre **LeetCode 2610 – Convertissez un tableau dans un tableau 2D avec conditions**.
Le problème sonne de façon trompeuse simple : "Put numbers in rows, no duplicates per row". (en milliers de dollars)
Mais le vrai défi est de le faire * efficacement* et *avec des lignes minimales*.
Dans cet article, je vais vous guider à travers le *bon* (pourquoi le problème est grand), le *mauvais* (pièges communs), et le *ugly* (pourquoi les approches naïves échouent), plus la solution propre et prête à la production qui est prête à l'entrevue.

---

### Le bon – Pourquoi ça compte

Pourquoi c'est bon Interview Takeaway
C'est ce qu'on dit.
** Clarté conceptuelle** – Il vous oblige à penser à *fréquence* par rapport à *nombre de lignes*. Parler de la façon dont la fréquence = nombre de fois qu'un élément doit apparaître dans des lignes distinctes – démontre la perspicacité. Autres
** Solution évolutive** – temps O(n), espace O(n). Les intervieweurs aiment les solutions à l'échelle; vous pouvez facilement expliquer la complexité algorithmique. Autres
** Analogie du monde réel** – Planifier les tâches à travers les travailleurs sans conflit. Se connecter aux systèmes du monde réel comme les planificateurs d'emploi, l'allocation des ressources. Autres
**Language-agnostic** – Facile à implémenter en Java, Python, C++. Autres

---

- Oui. Les mauvaises – erreurs courantes

1. **Le trier comme un problème* *
- *Mistake* : Triez le tableau et essayez de le diviser.
- *Pourquoi il échoue* : le tri ne réduit rien au nombre de lignes ; vous aurez toujours besoin de lignes `maxFrequency`.
2. **Complication excessive avec les boucles en nid* *
- *Mostake* : Double-boucle pour ajouter des éléments rang par rang, réduisant les compteurs à l'intérieur.
- *Résultat* : temps O(n2) – inacceptable pour les tableaux de 200 longueurs lorsque les entrevues s'attendent à des solutions linéaires.
3. **Ignorer les lignes minimales *
- *Mostake* : Allouer autant de lignes qu'il y a d'éléments distincts.
- Pourquoi c'est mal ? Vous n'utilisez pas la fréquence maximale* comme limite de ligne vraie.

---

### L'horrible – Pourquoi les distributions naïves s'écrasent

Envisager une mise en œuvre naïve :

Texte
pour chaque ligne i:
pour chaque élément j:
si nombre[j] > 0:
mettre l'élément j dans la rangée i
Compter [j]...
«» "

Cela fonctionne *en théorie*, mais la boucle interne `pour chaque élément` s`exécute *tous les éléments distincts* pour chaque ligne, ce qui conduit à une complexité de `O(maxFreq * distinctElements)`.
Lorsque «maxFreq» est égal à «n», le pire cas devient «O(n2)».
Dans un réglage d'entretien, une telle solution déclenchera des drapeaux rouges : -Pourquoi avez-vous écrit un algorithme O(n2) lorsque le problème est trivial pour O(n) ? (en milliers de dollars)

---

### L'Ugly – Pourquoi vous devriez éviter l'approche `non ordonnée_map`-seulement

Une autre approche tentante est de garder une simple `unordered_map` (ou `Counter`) et, pour chaque ligne, itérer sur *all* touches, en décrémentant lorsque vous placez une valeur.
Cela donne un résultat parfaitement correct, mais il a toujours `O(maxFreq * distinct)` complexité.
Dans la pratique, vous pouvez frapper la limite supérieure (n = 200) en millisecondes, mais le panel d'entrevue veut ** raisonnement clair, linéaire-temps** – le tour de distribution de fréquence propre le bat.

---

### La solution propre – Distribution par fréquence

**Étape 1 – Fréquences de comptage**

Texte
freq[valeur] = nombre d'occurrences de valeur
maxFreq = maximum de toutes les valeurs de freq
«» "

**Étape 2 – Pré-alterner les lignes**

Texte
lignes = [ [] pour _ dans l'intervalle (maxFreq) ] # nombre minimal de lignes
«» "

**Étape 3 – Distribution**

Pour chaque paire `(valeur, nombre)`, ajouter la valeur aux premières lignes `count`:

Texte
pour i dans 0 .. nombre-1:
ligne[i].annexe(valeur)
«» "

Cela garantit:

- Oui. Chaque ligne ne contient pas de duplicata (chaque valeur n'apparaît qu'une fois par ligne).
- Tous les numéros sont utilisés exactement "compte".
- Oui. Le nombre de lignes est égal à `maxFreq` – le minimum possible.

**Complexité* *

- **Heure** – O(n) – chaque numéro est traité une fois pour le comptage, puis une fois pour la distribution.
- **Espace** – O(n) – carte de fréquence + matrice de résultats.

---

### Pourquoi c'est l'entrevue-Ready

- **Temps linéaire** – Les intervieweurs peuvent immédiatement repérer la nature O(n) et demander une preuve.
- **Structures de données simples** – Seulement une carte et une liste de listes; aucune classe personnalisée ou fonction d'aide nécessaire.
- **Code linguistique** – Les trois langues ci-dessus sont prêtes à être copiées, ce qui fait de vous un ingénieur polyvalent.
- **Edge-Case Coverage** – Poigne les tableaux vides, les tableaux tout-identiques et la taille maximale autorisée.
- **Test-driven** – Vous pouvez exécuter les tests d'échantillonnage (par exemple, `[1,2,3,4,5,4,3,1]` → `[1,2,3,4],[1,2,3,4]`) instantanément.

---

- Oui. Comment réussir l'entrevue

1. **Énoncer clairement le problème** – Nous devons placer chaque élément dans des lignes distinctes sans duplicata intra-ligne. (en milliers de dollars)
2. **Exposer l'équivalence de fréquence de la bande** – La fréquence maximale force le nombre minimal de lignes. (en milliers de dollars)
3. **Présenter l'algorithme visuellement** – Afficher un diagramme ou un pseudocode rapide.
4. **Analyse Complexité** – temps O(n), espace O(n).
5. **Address Edge Cases** – Entrée vide, toutes uniques, toutes mêmes.
6. **Afficher la transférabilité multi-langue** – Voici comment je le fais en Java, Python et C++. (en milliers de dollars)

---

Pensée de clôture

LeetCode 2610 est un exemple de manuel d'un problème qui transforme une instruction *simple* en une leçon algorithmique *elegant*.
La maîtrise montre que vous pouvez :

- Lisez attentivement une déclaration de problème,
- Localiser la propriété mathématique clé (fréquence → lignes),
- Fournir une solution linéaire,
- Expliquez-le en plusieurs langues.

Si vous préparez des entrevues avec des ingénieurs de logiciels ou cherchez à déterrer ce travail convoité, rappelez-vous : **les meilleures solutions sont souvent celles qui traduisent une observation subtile en un algorithme propre et linéaire. * *

Bon codage – et que vos lignes soient toujours minimes!