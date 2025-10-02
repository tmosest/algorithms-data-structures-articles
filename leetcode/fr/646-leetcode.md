---
titre: LeetCode 646. Longueur maximale de la chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 646 – Longueur maximale de la chaîne de paires
**Langue:** C++
**Approach:** Greedy (sort par la deuxième valeur de chaque paire) – optimal et le plus rapide.
**Complexité temporelle :** **O(n log n)** (triage)
**Complexité spatiale:** **O(1)** (en place, à l'exception du tableau d'entrée)

---

1.1 Récapitulation du problème

> Compte tenu d'un tableau de la taille `n`, où `pairs[i] = [lefti , righti]` et `lefti < righti`.
> Une paire **p2 = [c, d]** suit la paire **p1 = [a, b]** si `b < c`.
> Trouvez la longueur maximale d'une chaîne qui peut être formée en utilisant n'importe quel sous-ensemble des paires dans n'importe quel ordre.

---

1.2 Regard sur l'avidité

Si nous choisissons toujours la paire qui se termine **earliest** (la plus petite valeur `droite`) parmi toutes les paires qui peuvent démarrer une nouvelle chaîne, nous laissons le plus grand espace libre possible pour les paires restantes.
Ainsi, la stratégie optimale est:

1. **Trier** les paires par leur valeur « droite » ascendante.
2. Scanner de gauche à droite, en choisissant une paire chaque fois que sa «gauche» est supérieure à la «droite» de la dernière paire choisie.

La règle avide est exactement la même que le problème classique de sélection d'activité.

---

- Oui. 2. Mise en œuvre des références

Vous trouverez ci-dessous un code propre et prêt à la production pour chacune des langues demandées.
Toutes les solutions ont la même complexité algorithmique, mais utilisent des idiomes spécifiques au langage et des appels de bibliothèques intégrés.

---

### 2.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public int findLongestChain(int[][] paires) {
// 1. Trier par le deuxième élément (à droite)
les tableaux.sort(pairs, a, b) -> Integer.compare(a[1], b[1]);

nombre int = 0;
int prevRight = entier.MIN_VALUE;

// 2. Numérisation de graisse
pour (int[] paire : paires) {
si (pair[0] > prevRight) { // peut être ajouté
count++;
prevRight = paire[1]; // mettre à jour la dernière paire choisie
}
}
le nombre de retours;
}
}
«» "

**Explication des lignes principales**

Ligne Pourquoi c'est important
-- -- -- -- -- --
"Arrays.sort(pairs, ...)" Trier par la deuxième valeur; garantit que la prochaine paire sélectionnable est celle avec la plus petite extrémité. Autres
`prevRight = Integer.MIN_VALUE`= Permet de sélectionner la première paire sans logique de cas particulier. Autres
`pair[0] > prevRight`= État cupide de base : le début de la paire actuelle doit être après la fin de la paire précédente. Autres

---

2.2 Python

'`python
Solution de classe:
def findLongest Chaîne(même, paires: Liste[Liste[int]]) -> Int:
# 1. Trier par le deuxième élément
paires.sort(key=lambda x: x[1])

nombre = 0
prev_end = flotteur('-inf')

2. Scannage d'avidité
pour gauche, droite par paire:
si gauche > prev_end :
nombre += 1
prev_end = droite

Nombre de retours
«» "

*`float('-inf')`* joue le même rôle que `Integer. MIN_VALUE' en Java.

---

C++

'`cpp
solution de classe {
public:
int findLongestChain(vecteur<vecteur<int>>& paires) {
// 1. Tri par deuxième élément
tri(pairs.begin(), paires.end(),
[](const vector<int>& a, const vector<int>& b) {
retour a[1] < b[1];
});

nombre int = 0;
int prevRight = INT_MIN;

// 2. Numérisation de graisse
pour (const auto & p : paires) {
si (p[0] > prevRight) {
+ nombre;
prevRight = p[1];
}
}
le nombre de retours;
}
};
«» "

---

- Oui. 3. Programmation dynamique alternative (O(n2))

Pour l'exhaustivité, la solution DP est utile quand vous voulez *également* récupérer la chaîne ou quand l'intuition gourmande n'est pas évidente.

'`python
def findLongestChainDP(paires):
n = len(paires)
paires.sort(key=lambda x: x[1])
dp = [1] * n # dp[i] = longueur se terminant à i
pour i dans la plage(n):
pour j dans la plage i:
si paires[j][1] < paires[i][0]:
dp[i] = max(dp[i], dp[j] + 1)
retour max(dp)
«» "

Complexité: **O(n2)** temps, **O(n)** espace – beaucoup plus lent pour `n <= 1000`, mais toujours parfaitement bon pour LeetCode.

---

- Oui. 4. Article du blog – Le bon, le mauvais, et l'acharnement de résoudre le leetCode 646

4.1 Pourquoi ce problème est-il important?
* LeetCode 646 est un problème classique de chaîne maximale qui mélange **algorithmes gredy** avec l'intuition de la sélection d'activité. (en milliers de dollars)
* C'est un favori sur les listes de prép d'entrevue de codage parce qu'il teste:
* Comprendre les fonctions de tri et de comparaison.
* Capacité d'identifier les sous-structures optimales.
* Nettoyer, code O(n log n) qui compile dans toutes les langues.

4.2 Les bons
* **Simplicité** – Une fois que vous repèrez la règle de l'extrémité la plus petite, le code se résume à une seule boucle.
* **Performance** – Le tri domine, donnant du temps *O(n log n*) – rapide même pour la limite supérieure de 1000 paires.
* **Portabilité** – La même logique s'applique en Java, Python, C++ et même dans les langages fonctionnels.
* **Échelle** – La solution avide est toujours optimale pour les contraintes plus grandes (par exemple, `n = 106`), alors que DP serait invraisemblable.

Les mauvais
* ** Hypothèses lourdes** – La règle avide ne fonctionne que parce que les paires sont *non-overlaping* ('gauche < droite'). Si cet invariant se brise, l'algorithme échoue.
* **Readability for Beginners** – Tri avec un comparateur personnalisé ou lambda peut être source de confusion pour les nouveaux arrivants. Ajouter des commentaires est essentiel.
* **Edge Cases** – L'entrée vide ou les valeurs négatives sont traitées implicitement mais peuvent faire monter les gens pendant les entrevues si elles ne sont pas mentionnées.

#### 4.4 La moche
* **Tester des idées fausses** – Certains candidats comparent par erreur le « droit » de la paire actuelle avec le « droit » de la paire précédente sélectionnée *sans* s'assurer que la paire est effectivement sélectionnée.
* **Off‐by‐One Errors** – Dans Python, oublier `prev_end = float('-inf')` et initialiser avec `-1` pourrait rejeter incorrectement la première paire si sa `gauche` est `0`.
* ** Stabilité gustative** – Dans C++, `sort` n'est pas stable. Si deux paires partagent le même "droit", l'ordre de leurs valeurs de "gauche" n'affecte pas la justesse, mais un type instable peut rendre le débogage plus difficile.

4.5 Référencement Mots clés optimisés (Utilisez-les dans votre curriculum vitae, blog ou LinkedIn)

Mot-clé Pourquoi ça compte
C'est-à-dire
**Longueur maximale de la chaîne de paires**=Titre du problème principal – apparaît dans les entrevues et les résultats de recherche. Autres
**LeetCode Les gens cherchent souvent par numéro de problème. Autres
**Algorithme de grêle pour la chaîne de paires** Autres
**La solution Java pour la chaîne de paires**=Attire les recruteurs à la recherche de compétences Java. Autres
**Algorithme de cupidité Python** Autres
**C++ problème de l'entrevue** Autres
**Problème de sélection d'activité** Autres
**Préparation de l'entrevue d'embauche** Autres
**Résolution algorithmique des problèmes** Autres

> *Astuce:* Lors de l'affichage de l'article sur Medium, Dev.to, ou un blog personnel, utiliser des balises comme `#LeetCode`, `#Algorithm`, `#Java`, `#Python`, `#C++`, `#InterviewPrep`, `#JobSearch`.
> Les moteurs de recherche indexeront l'article, et les recruteurs utilisant des tableaux d'emploi (LinkedIn, Effective, etc.) filtreront souvent par ces balises.

4.6 Réflexions finales

*Si vous pouvez expliquer ce problème en moins de 30 secondes, vous avez montré la maîtrise du raisonnement avide et le codage propre. *
Gardez les extraits de code prêts dans votre repo personnel – les recruteurs aiment voir des solutions bien structurées dans toutes les langues.
Et, comme toujours, pratiquez la version DP. Même si vous n'allez pas l'utiliser dans la production, savoir *deux* solutions distinctes démontre de la profondeur – quelque chose que chaque embaucheur cherche.

---

- Oui. 5. Liste de contrôle à emporter pour votre entrevue

1. **Énoncer la règle de l'avidité**: Choisir la paire avec le plus petit paramètre droit qui ne se chevauche pas avec la paire précédemment choisie. (en milliers de dollars)
2. **Afficher le genre**: Dans Java utiliser `Arrays.sort(pairs, (a,b) -> a[1] - b[1])`; dans Python `pairs.sort(key=lambda x: x[1])`; dans C++ `sort(..., [](auto& a, auto& b){ retourner a[1] < b[1]; })`.
3. **Expliquer le scan**: Conservez `prevEnd`, incrément `count` lorsque `left > prevEnd`, mettez à jour `prevEnd`.
4. **Complexité**: temps `O(n log n)`, espace auxiliaire `O(1)`.
5. **Cas d'Edge**: tableau vide, toutes les paires qui se chevauchent, valeurs négatives – tous traités naturellement.
6. **PDD facultatif**: mention "O(n2)" PDD si l'intervieweur demande des approches alternatives.

---

- Oui. 6. Enveloppage

Vous avez maintenant :

* ** Trois solutions prêtes à la production** – Java, Python, C++.
* **Une explication claire et conviviale pour l'entrevue** – Bon, mauvais, mauvais.
* **SEO-friendly copy** qui atterrira votre post de blog dans les résultats de recherche pour la longueur maximale de la chaîne de paires et les requêtes connexes.

Mettez cela dans votre portfolio, postez l'article, et vous allez non seulement mettre en valeur vos compétences de codage, mais aussi votre capacité à les communiquer – exactement ce que les recruteurs chassent. Bon codage, et bonne chance pour votre prochaine interview!