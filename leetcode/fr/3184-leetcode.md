---
titre: LeetCode 3184. Nombre de paires qui forment une journée complète Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3184 – Nombre de paires qui forment une journée complète (facile)

Lien vers le code
- C'est quoi ?
*Java * O(n) Autres
*Python * O(n)* `solution.py'
*C++**= O(n)= `solution.cpp`=

Une journée complète est une durée de temps qui est un multiple exact de 24 heures.

Le problème est un casse-tête classique. Ci-dessous, vous trouverez une implémentation propre et prête à la production dans **Java**, **Python** et **C++**, suivie d'un parcours de style blog qui met en évidence les aspects *bon*, *mauvais* et *ugly* de la résolution de ce problème d'interview.

---

Récapitulation des problèmes

Compter le nombre de paires "(i, j)" avec "i < j"

«» "
(heures[i] + heures[j]) % 24 == 0
«» "

En d'autres termes, la somme est un multiple de 24.

---

Idée de solution – HashMap + Compte du reste

Au lieu de vérifier chaque paire (`O(n2)`), nous pouvons le résoudre en temps linéaire:

1. **Dénombrement des restes* *
Pour chaque heure, calculer `rem = heure % 24`.
Le reste nécessaire pour atteindre un multiple de 24
«comp = (24 - rem) % 24».

2. **Couvercle de paires valides à la volée**
Alors qu'il est itératif, le nombre de paires impliquant l'élément courant est égal au nombre courant de "comp" déjà vu.

3. **Mise à jour de la carte des fréquences**
Incrémenter le compteur pour "rem".

Cette technique est la même que l'astuce classique à deux somme, mais nous travaillons modulo 24.

---

Mise en œuvre des références

### Java

"Java
// Solution.java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
Compte d'entrée publicPairs de jour complets(int[] heures) {
Carte<integer, integer> freq = nouveau HashMap<>();
nombre int = 0;

pendant (int h : heures) {
int rem = h % 24;
complément int = (24 - rem) % 24; // 0 cartes à 0
count += freq.getOrDefault(complément, 0);

freq.merge(rem, 1, entier::sum);
}
le nombre de retours;
}
}
«» "

Python

'`python
# solution. py
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def countCompleteDayPairs(self, hours: List[int]) -> Int:
freq = defaultdict(int)
ans = 0
pendant h en heures:
m = h % 24
Comp = (24 - rem) % 24
ans += freq[comp]
[rem] += 1
retour et
«» "

C++

'`cpp
// solution.cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre de jours completsPairs(vecteur <int>& heures) {
unordered_map<int, int> freq;
long an = 0;
pendant (int h : heures) {
int rem = h % 24;
Int comp = (24 - rem) % 24;
as += freq[comp];
freq[rem]++;
}
retourner static_cast<int>(ans);
}
};
«» "

---

Article du blog – Le bon, le mauvais, et le mauvais de résoudre le LeetCode 3184

- Oui. 1. Présentation

Si vous regardez un rôle d'ingénierie de logiciel, vous rencontrerez probablement LeetCode 3184 dans votre prép d'entrevue. Il est marqué *Easy*, mais la gymnastique mentale nécessaire pour éviter le piège quadratique est non-triviale. Ce post brise le problème en ses éléments de base, explique pourquoi une approche linéaire brille, et touche même comment les intervieweurs peuvent évaluer votre solution.

- Oui. 2. Le problème en anglais clair

On vous donne une liste d'heures. Deux d'entre eux qui se résument à un multiple exact de 24 forment un jour complet. Comptez combien de paires existent. Pour les petits tableaux, une double boucle fonctionne; pour les tableaux avec 105 éléments, elle exploserait.

- Oui. 3. Le bon* – une solution linéaire

La solution élégante utilise une carte **fréquence des restes**. Pensez à chaque heure comme un seau dans un cycle de 24 heures. Si un nombre est `r`, vous avez besoin d'un autre nombre avec le reste `24 – r` (ou `0` si `r` est `0`) pour atteindre un multiple de 24. En gardant un compteur pour chaque reste que vous itérer, vous pouvez instantanément savoir combien de partenaires valides le nombre actuel a déjà vu. L'algorithme fonctionne dans le temps O(n) et l'espace supplémentaire O(1) (les 24 seaux constants).

Pourquoi c'est bon

- **Speed** – Le temps linéaire est le seul moyen de répondre aux contraintes si le tableau grandit.
- **Simplicité** – Un passage, une carte, pas de boucles imbriquées.
- **Évoluabilité** – Fonctionne pour des durées allant jusqu'à 105 heures ou plus, sans dépasser les limites de temps.

- Oui. 4. Le *Bad* – L'approche Brute-Force

Une double boucle naïve :

"Java
nombre int = 0;
pour (int i = 0; i < n; i++)
pour (int j = i + 1; j < n; j++)
si ((heures[i] + heures[j]) % 24 == 0) nombre++;
«» "

Cet algorithme O(n2) est parfait pour le problème des contraintes originales (n ≤ 100), mais c'est un choix *mauvais* si vous parlez interview prep parce que:

- **Performance** – C'est facile de dire que je vais juste le faire dans l'interview ; les intervieweurs s'attendent à ce que vous optimisiez.
- **Clarity** – Montre un manque de compréhension du problème de la nature modulaire.
- **Échelle** – Pas une solution à l'épreuve de l'avenir pour les ensembles de données plus importants.

- Oui. 5. Les pièges communs

Pourquoi ça arrive ?
- Oui.
**Utiliser `% 24` sur des nombres énormes**= Oublier que la somme peut déborder `int`=Utilisez `long` pour la somme si la langue le permet; cependant, pour Java, vous pouvez garder `% 24` sûr parce que `int` reste dans les 32 bits, mais utilisez `long` si vous prévoyez de résumer explicitement. Autres
**Reste manquante La pensée `comp = 24 - rem` donne 24 au lieu de 0= Utiliser `(24 - rem) % 24` de sorte que `rem = 0` donne `comp = 0`. Autres
**Mutable map pendant l'itération**.Réinitialisation accidentelle des comptes dans la boucle. Autres
**Overflow in counter**=Pairs de comptage pour des entrées énormes=Utilisez `long` pour la réponse. Autres

- Oui. 6. Conseils d'entrevue

1. **Exposer l'idée O(n) avant le codage** – Les intervieweurs aiment vous voir penser à la complexité du temps.
2. **Cas de bord de Mention** – Zéro reste, grand nombre, duplicata.
3. **Test sur petits échantillons** – Montrez que vous comprenez la sortie attendue.
4. **Parlez de l'espace** – Clarifiez que vous utilisez seulement 24 compteurs, peu importe la taille de l'entrée.
5. **Optionnel** – Afficher une version à un passage qui évite une deuxième recherche de carte en incrémentant d'abord un compteur.

"Java
// Astuce unique
nombre int = 0;
pour (int h : heures) {
int rem = h % 24;
nombre += freq.getOrDefault( (24 - rem) % 24, 0 );
freq.put(rem, freq.getOrDefault(rem, 0) + 1);
}
«» "

- Oui. 7. Résumé

- **Bien**: Compte du reste d'un passage, temps O(n), espace O(1).
- **Bad**: boucles imbriquées de Brute-force; facile mais pas de niveau d'entrevue.
- **Ugly**: Erreurs communes concernant le module et le débordement entier.

Si vous pouvez coder la solution dans **Java**, **Python** et **C++** – comme indiqué ci-dessus – et expliquer clairement le raisonnement, vous serez bien placé pour répondre à cette question lors d'une entrevue de codage.

- Oui. 8. Takeaway optimisé SEO

- **Mots-clés**: LeetCode 3184, Count Pairs that form a Complete Day, interview coding, algorithme, hashmap, deux-sum modulo 24, solution Java, solution Python, solution C++, entretien d'emploi, entretien d'ingénierie logicielle.
- **Meta Description**: LeetCode 3184 avec une solution de hashmap linéaire. Obtenez un code Java, Python et C++ ainsi qu'un guide d'entrevue convivial pour le référencement qui couvre les bonnes, les mauvaises et les laides de résoudre les paires de comtes qui forment une journée complète. (en milliers de dollars)

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit