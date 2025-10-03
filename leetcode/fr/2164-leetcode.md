---
titre: LeetCode 2164. Classer les indices même et les indices bizarres Indépendamment -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2164 – Classer les indices du même ordre et du même ordre
### (solutions Java, Python & C++ + guide d'entrevue convivial pour le référencement)

---

Description de la méta
Master LeetCode 2164 avec des solutions claires et prêtes à la production en **Java, Python et C++**.
Apprenez l'algorithme, la manipulation des cas, l'analyse du temps et de la mémoire et les explications de style d'entrevue pour impressionner les gestionnaires d'embauche.

---

- Oui. 1. Le problème en coque
> **Indices du même ordre et du même ordre

> *Avec un tableau entier indexé 0 'nums', recommandez-le pour que : *
> - *Les valeurs des indices **odd** (1, 3, 5, ...) sont triées **non de plus en plus** (descendant). *
> - *Les valeurs à **even** les indices (0, 2, 4,...) sont triés **non-diminution** (croissant). *

> Retourne le tableau résultant.

> **Constraints**
> - 1 ≤ "longueur en nombre" ≤ 100
> - 1 ≤ "nums[i]` ≤ 100

> **Exemples**
En savoir plus Sortie Explication
> C'est pas vrai.
>--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- Même les indices triés asc → `[2,3,4,1]` Autres
Un seul élément impair et même – aucun changement nécessaire

---

- Oui. 2. Pourquoi ce problème est un sujet d'entrevue de bonne, de mauvaise et de mauvaise qualité

**Beau**
C'est quoi ?
Facile à comprendre – séparation claire d'indices impairs/même.Il faut deux sortes; pas vraiment O(n) – une subtilité pour l'optimisation.
Démonstration de la manipulation des sous-réseaux et du re-assemblage La petite taille d'entrée cache le potentiel d'une solution de comptage O(n)
Autres Fournit un terrain de jeu pour tester les cas de bord (élément unique, toutes les mêmes valeurs) ─ Tri des frais généraux est inutile pour 1 ≤ n ≤ 100 mais mérite toujours d'être mentionné ─ Les erreurs avec la division entière peuvent corrompre l'étape de reconstruction

> **À emporter :** Maîtriser la stratégie simple à deux passages, mais être prêt à justifier O(n log n) vs O(n) et discuter d'écueils de cas de bord.

---

- Oui. 3. L ' idée fondamentale

1. **Séparer** les éléments en deux tableaux auxiliaires:
- `even` détient des valeurs aux indices 0, 2, 4, ...
- "odd" détient des valeurs aux indices 1, 3, 5, ...

2. **Trier** indépendamment :
- `even` → ascendant (`Arrays.sort`)
- `odd` → descendant (`Arrays.sort` + comparateur inverse)

3. **Remplacez** dans le tableau original en utilisant le même motif d'index.

Parce que `nums.length` ≤ 100, le coût de tri `O(n log n)` est insignifiant et garde le code lisible.

---

- Oui. 4. Mise en œuvre Java (Fast & Clear)

"Java
Importer java.util. Les tableaux;
Importer java.util. Recouvrements;

solution de classe {
public int[] sortEvenOdd(int[] nums) {
int n = longueur nums;

// Stockage temporaire pour des positions paires et impaires
Integer[] even = nouveau Integer[(n + 1) / 2]; // ceil(n/2)
Nombre entier[] impair = nouveau nombre entier[n / 2]; // étage(n/2)

//
pour (int i = 0; i < n; i++) {
Si (i % 2 == 0) {
even[i / 2] = nombres[i];
} autre {
impair[i / 2] = nombres[i];
}
}

Trier séparément
Tableau 3.
Arrays.sort(odd, Collections.reverseOrdonnance()); // descendant

// 3
résultat int[] = nouveau résultat int[n];
pour (int i = 0; i < n; i++) {
résultat[i] = (i % 2 == 0) ? even[i / 2] : impair[i / 2];
}
le résultat du retour;
}
}
«» "

**Pourquoi c'est prêt pour la production* *

Étape Pourquoi c'est important
-- -- -- -- -- --
"entier[]" → permet le comparateur inverse , les tableaux primaires ne peuvent pas être inversés sans copie ,
`Arrays.sort(even)`==Traitement rapide intégré/Traitement de fusion – stable pour 100 éléments==
"Collections.reverserCommander()" Un seul liner – aucune logique de comparaison personnalisée

---

- Oui. 5. Mise en œuvre de Python (concise et pythonique)

'`python
Solution de classe:
def tri EvenOdd(self, nombres: list[int]) -> list[int]:
n = len(nums)

# Séparer en listes paires et impaires
même = [nums[i] pour i dans la plage(0, n, 2)]
impair = [nums[i] pour i dans l'intervalle(1, n, 2)]

# Trier chaque liste
même.sort() # ascendant
impair.sort(reverse=True) # descendant

Remplacement
res = [0] * n
pour i dans la plage(n):
res[i] = even[i // 2] si i % 2 == 0 autre impair[i // 2]
retour res
«» "

**Python en bref**

- `range(0, n, 2)` / `range(1, n, 2)` gère l'extraction de l'indice.
- `list.sort()` est en place et utilise déjà Timsort (`O(n log n)`).
- L'opérateur `//` garantit la division entière.

---

- Oui. 6. Mise en œuvre C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> trierEvenOdd(vector<int>& nums) {
int n = nombres.size();
vecteur<int> même(n + 1) / 2);
vecteur<int> impair(n / 2);

// Séparer
pour (int i = 0; i < n; ++i) {
Si (i % 2 == 0) égale[i / 2] = nombre[i];
autres étranges[i / 2] = nombres[i];
}

// Tri
tri(even.begin(), even.end()); // ascendant
tri(odd.begin(), impair.end(), plus grand<int>(); // descendant

// Fusionner
vecteur<int> res(n);
pour (int i = 0; i < n; ++i) {
Res[i] = (i % 2 == 0) ? even[i / 2] : impair[i / 2];
}
retour rés;
}
};
«» "

**Pourquoi STL? **

- `sort` utilise l'introsort (O(n log n)) – parfaitement bon pour `n ≤ 100`.
- `plus grand<int>()` est un comparateur léger pour l'ordre décroissant.

---

- Oui. 5. Analyse de la complexité

Métrique
- C'est quoi ?
**Heure**="O(n log n)" – deux sortes indépendantes="O(n log n)" – même raison="O(n log n)" – même raison
**L'espace**=O(n)` auxiliaire (`even` + `odd`)=O(n)` auxiliaire==O(n)` auxiliaire==
**En place?** Non (utilise des tableaux d'aide)

> ** Pouvons-nous faire mieux? **
> Étant donné que `nums[i]` ≤ 100 et `n` ≤ 100, une matrice de comptage (table de fréquence de la taille 101) donnerait `O(n)` temps et `O(1)` espace supplémentaire.
> Cependant, l'approche triée est plus simple, plus facile à raisonner et parfaitement acceptable dans les contextes d'entrevue.

---

- Oui. 6. Erreurs et bords communs Liste de contrôle des cas

Erreurs Comment éviter
C'est quoi ?
**Swapping impair/even valeurs au lieu d'indices**. Autres
**L'utilisation de la division entière est incorrecte**. Dans Python, utilisez `i // 2`. Autres
**Négligence d'inverser la liste impaire** Autres
**Ne pas manipuler des tableaux de longueurs impaires**. Cela couvre à la fois et étrange `n`. Autres
**En supposant que les valeurs sont distinctes**=Le tri fonctionne avec des duplicatas; assurez-vous que l'ordre reste stable au besoin. Autres

---

- Oui. 7. Variations que vous pourriez rencontrer

Variation de la réponse
Ce n'est pas le cas.
**Tous les indices sont triés en ascension** Autres
**Trier les indices dans l'ordre inverse (même en descendant, impair en montant)** Autres
**Les plus grandes contraintes (n 105, valeurs 109)**= Remplacer le tri par le tri de tri ou de seau si la plage de valeurs est petite ou utiliser une file d'attente de priorité stable. Autres
**Besoin d'indices de sortie au lieu de valeurs**= Après fusion, afficher les positions originales stockées pendant la phase de fractionnement. Autres

---

- Oui. 8. Conseils d'entrevue prêts

1. ** Expliquez votre plan avant de coder** – montrez-vous en pensant aux compromis temps/espace.
2. **Mention l'alternative de comptage-sort** – montre la conscience des possibilités O(n).
3. **Test cas bord** dans votre explication:
- Élément unique (`[42]`)
- Toutes les valeurs sont égales ('[5,5,5]')
- Longueur maximale (`n=100`)
4. **Discussion de la lisibilité par rapport au rendement** – Les compromis sont importants pour les gestionnaires embaucheurs.

---

- Oui. 9. Pourquoi ce problème est un must-Know pour les entrevues d'emploi

- **Array manipulation fondamentaux** – sépare les préoccupations (split → tri → fusion).
- **Index arithmétique** – crucial pour de nombreux problèmes de structure des données.
- **Tarifs irritantes** – démontre la compréhension de l'ordre ascendant et descendant.
- **Conversation de complexité** – peut conduire à des discussions plus approfondies sur les optimisations algorithmiques.

Ajoutez ce problème à votre liste de pratique d'entrevue et vous serez prêt à en discuter avec les recruteurs et les gestionnaires d'embauche.

---

Mots clés (utilisés dans l'article)
- LeetCode 2164
- Trier les indices et les indices bizarres
- Solution Java LeetCode 2164
- Solution Python LeetCode 2164
- Solution C++ LeetCode 2164
- algorithme d'entretien
- entretien de génie logiciel
- entretien sur la structure des données
- manipulation du tableau
- compter tri vs tri rapide
- préparation d'un entretien d'emploi

---

Mot final
Maîtriser l'approche **split-sort-merge**, connaître les cas de bord, et être prêt à discuter pourquoi une solution `O(n log n)` est acceptable ici et comment vous l'optimiser pour les entrées plus grandes.
Avec les extraits de code et les idées d'entrevue ci-dessus, vous êtes entièrement équipé pour ace LeetCode 2164 – et impressionnez l'équipe d'embauche qui est à la recherche de solutions de problèmes propres et efficaces. C'est ce qu'il a dit.

Bon codage et bonne chance avec votre prochaine interview!