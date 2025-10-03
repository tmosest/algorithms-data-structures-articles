---
titre: LeetCode 3146. Différence de permutation entre deux cordes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Différence de permutation entre deux cordes – LeetCode 3146
**A Plongée profonde (Java / Python / C++) + SEO-Optimized Blog Post**

> **Tags:** #LeetCode #Java #Python #C++ #HashMap #StringAlgorithmes #Préparation de l'entrevue

---

- Oui. 1. Aperçu du problème

**LeetCode 3146 – Différence de permutation entre deux cordes**

> On vous donne deux cordes `s` et `t` telles que:
> * Chaque caractère dans `s` apparaît ** au plus une fois**.
> * `t` est une permutation de `s`.
>
> La différence de permutation** entre `s` et `t` est définie comme suit:
> \[
- \text{index}_t(c)\,
> \]
>
> Rends cette somme.

**Exemple**

Résultat
C'est pas vrai.
"abc"""bac""""""2" ("0-1" +"1-0" +"2-2")"
"abcde"

**Contrôles* *

* `1 ≤ s.longueur ≤ 26`
* Chaque caractère dans `s` apparaît une fois.
* `t` est une permutation de `s`.

---

- Oui. 2. Approche optimale de Brute-Force

2.1 Brute- Forcer
Itérer sur chaque caractère dans `s`, trouver son index dans `t` en scannant toute la chaîne, et résumer les différences absolues.

*Time:* `O(n2)` – chaque recherche scanne jusqu'à `n` caractères.
*Espace:* "O(1)" – seulement quelques compteurs.

Ceci est très bien pour `n ≤ 26`, mais pour la pratique de l'entrevue, vous devriez viser une solution `O(n)`.

2.2 Approche optimale – HashMap / Array

Parce que chaque caractère est unique, nous pouvons cartographier un caractère → sa position en **O(1)** temps.

1. **Construisez une carte pour `s`**: `posInS[char] = index`.
2. **Traverse `t`**: pour chaque `char` à l'index `i`, recherchez `posInS[char]` et ajoutez `abs(i -posInS[char])` à la réponse.

*Heure:* `O(n) "
*Espace: * `O(n)` (la carte / tableau de hachage)

Comme l'alphabet n'est que des lettres anglaises minuscules (« a–z »), un simple tableau entier de longueur 26 fonctionne tout autant qu'un HashMap, ce qui nous donne la recherche la plus rapide à temps constant.

---

- Oui. 3. Mise en œuvre du code

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**. Chacun comprend:

* Effacer les noms des variables
* Commentaires en ligne
* Sécurité des caisses (bien que les contraintes garantissent la validité)

#### 3.1 Java

"Java
Importer java.util. HashMap;

solution de classe publique {
public int findPermutation Différence(String s, chaîne t) {
// Carte de chaque caractère à son index en 's'
HashMap<Caractère, entier> indexInS = nouveau HashMap<>();
pour (int i = 0; i < s.longueur(); i++) {
l'indexInS.put(s.charAt(i), i);
}

Int diffSum = 0;
// Traverse 't', calcul des différences absolues
pour (int i = 0; i < t.longueur(); i++) {
ch = t.charAt(i);
int posInS = indexInS.get(ch);
diffSum += Math.abs(i - posInS);
}
retour diffSum;
}
}
«» "

> **Pourquoi HashMap?**
> Pour une solution générale; si vous savez que l'alphabet est petit, vous pouvez remplacer `HashMap` par `int[26]`.

3.2 Python

'`python
Solution de classe:
def findPermutation Différence (self, s: str, t: str) -> Int:
# Construisez le dictionnaire : char -> index en s
pos_in_s = {ch: i for i, ch in énumérate(s)}

diff_sum = 0
pour i, ch dans l'énumération(t):
diff_sum += abs(i - pos_in_s[ch])

retourner diff_sum
«» "

> ** Touches pyroniques* *
> La compréhension de la liste et le dictionnaire rendent le code concis.
> `abs` est intégré, donc pas d'importations supplémentaires nécessaires.

### 3.3 C++

'`cpp
#incluez <string>
#inclut <non-ordonné_map>
#incluez <cmath>

solution de classe {
public:
Int findPermutation Différence(std::chaîne s, md::chaîne t) {
std::unordered_map<char, int> posInS;
pour (int i = 0; i < s.size(); ++i)
PosInS[s[i]] = i;

Int diffSum = 0;
pour (int i = 0; i < t.size(); ++i)
diffSum += md::abs(i - posInS[t[i]]);

retour diffSum;
}
};
«» "

> **Pourquoi `unordered_map`?**
> Fournit une recherche moyenne dans le cas O(1).
> Pour un facteur constant encore plus rapide, vous pouvez utiliser `int[26]` et indexer par `c - 'a'.

---

- Oui. 4. Analyse de la complexité

L'approche Temps Espace
- C'est quoi ?
Brute-Force Autres
HashMap/Array** Autres

Avec `n ≤ 26`, l'une ou l'autre approche fonctionne, mais les intervieweurs attendent la solution linéaire et discuteront de votre choix.

---

- Oui. 5. Bien, mal, mal – Leçons apprises

Catégorie
C'est pas vrai.
**Le choix algorithmique**=L'utilisation d'une carte de hachage donne un temps linéaire – le spot doux de l'intervieweur. Sauter la carte et utiliser des boucles imbriquées est facile mais perd du temps. Suringénierie : construction d'un arbre équilibré (« TreeMap »), triage ou récursion. Autres
**Code Clarity**= Dictionnaire monoligne en Python, boucles courtes en Java/C++. Les noms de variables lourds (`map1`, `map2`) ou les commentaires trop verbeux peuvent encombrer la solution. Mélanger des langages ou des constructions spécifiques à la plate-forme (par exemple, Java=s `TreeMap` quand `HashMap` suffit). Autres
**Edge Cases**. Aucune – les contraintes garantissent l'entrée valide. Oublier de manipuler des chaînes vides (mais non autorisées). Des contrôles nuls inutiles qui rendent le code plus long sans bénéfice. Autres
**Readability**="Inline `abs(i - posInS[ch]' montre clairement l'intention. Découper la logique en plusieurs fonctions d'aide inutilement. En utilisant des chiffres magiques ou des indices peu clairs (par exemple, `s.charAt(i)`, `t.charAt(i)`). Autres
**Performance**= L'utilisation d'un tableau de taille 26 donne une recherche constante – plus rapide dans la pratique. En utilisant `HashMap` en Java encore très bien, mais plus lent que le tableau. L'utilisation de `TreeMap` conduit à `O(n log n)` même si la taille des entrées est minuscule. Autres

**À emporter :**
Gardez la solution *simple*, *fast* et *claire*. Évitez la surcomplication lorsque les contraintes sont serrées et simples.

---

- Oui. 6. Résumé du blog optimisé du SEO

- **Titre:** 3146 – Différence de permutation entre deux cordes: HashMap & Array Solutions (Java, Python, C++)
- **Meta Description:** Apprendre à résoudre le LeetCode 3146 – Différence de permutation entre deux cordes – avec des approches efficaces de HashMap et de tableau. Compléter des exemples de code Java, Python et C++ ainsi qu'une analyse de performance. (en milliers de dollars)
- **Mots clés:** LeetCode 3146, différence de permutation, algorithme de chaîne, solution de hash map, problème de chaîne de Java, défi de chaîne de Python, question d'entrevue C++, complexité de l'algorithme, prép d'entrevue.
- ** Structure de l'en-tête :**
- H1 : Code de leet 3146 – Différence de permutation entre deux cordes
- H2 : Déclaration de problème
- H2 : Approche de Brute-Force contre approche optimale
- H2 : Mise en œuvre du code (Java, Python, C++)
- H2 : Analyse de complexité
- H2 : Bon, mauvais, mauvais – Leçons apprises
- H2 : pensées finales et conseils d'entrevue

L'ajout d'une introduction intéressante, d'exemples illustratifs et d'une conclusion concise permettra de garder les lecteurs branchés et d'aider le grade de poste pour les recherches liées à l'emploi. Inclure une section « Prochaines étapes » pour encourager les lecteurs à explorer les problèmes liés au LeetCode ou à partager l'article sur LinkedIn, en stimulant ses signaux sociaux.

---

- Oui. 7. Liste de contrôle finale pour une entrevue gagnante

1. **Comprendre les contraintes** – caractères uniques → alphabet de taille constante.
2. **Choisir la bonne structure de données** – `HashMap` ou `int[26]`.
3. **Conservez le code concis** – une boucle pour la cartographie, une pour la somme.
4. ** Expliquez votre processus de réflexion** – parlez de compromis temps/espace.
5. **Test edge cases** – petites chaînes, ordre inverse, chaînes identiques.

Avec les extraits de code ci-dessus et les leçons de l'analyse *Good, Bad, Ugly*, vous êtes prêt à ace ce problème LeetCode – et atterrissez cette interview! C'est ce qu'il a dit.

---