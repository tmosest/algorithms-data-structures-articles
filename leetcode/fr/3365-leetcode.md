---
titre: LeetCode 3365. Réorganiser les sous-chaînes K pour former une chaîne cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3365 – Replacer les sous-chaînes K pour former une chaîne cible
## Solutions Java, Python & C++ + Post Blog In-Depth

> **TL;DR** –
> *Le problème demande si deux chaînes d'anagrammes peuvent être partitionnées en « k » pièces de longueur égale, puis les morceaux de « s » réaménagés pour former « t ». *
> *Un seul `O(n)` passer avec une carte de hachage est suffisant: il suffit de compter les morceaux de `s`, puis les consommer de `t`. *

Ci-dessous vous trouverez:

Langue Fichier Code
C'est quoi ?
*Java *Solution.java *[Lien] (#java) *
*Python *Python *solution.py *[Link](#python) Autres
*C++**=solution.cpp===[Lien](#cpp)==

Après cela, un article de blog plein-blown SEO-friendly qui explique l'algorithme, marche à travers le bon, mauvais, laid, et offre des idées de style interview.

---

Solution Java

"Java
// Solution.java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
le booléen public estpossibleàréorganiser(chaîne s, chaîne t, int k) {
int n = s.longueur(); // n == t.longueur()
blockSize = n / k; // garanti d'être entier

// Compter chaque bloc de k s
Carte<String, entier> freq = nouveau HashMap<>();
pour (int i = 0; i < n; i += blockSize) {
Bloc de chaîne = s.substring(i, i + blockSize);
freq.merge(bloc, 1, entier::sum);
}

// Consommer les blocs de t
pour (int i = 0; i < n; i += blockSize) {
Bloc de chaîne = t.substring(i, i + blockSize);
Nombre entier = freq.get(bloc);
si (compter) null. 0) retourner faux;
freq.put (bloc, nombre - 1);
}
retour vrai;
}
}
«» "

> **Pourquoi ça marche* *
> * `k` est fixe, de sorte que chaque longueur de bloc est `n/k`.
> * Parce que `s` et `t` sont des anagrammes, chaque bloc qui apparaît dans `t` doit également apparaître dans `s`.
> * La carte de hachage garantit la recherche `O(1)` pour chaque bloc.

---

Solution Python

'`python
# solution. py
def isPossibleToRearrange(s): str, t: str, k: int) -> C'est vrai.
n = len(s)
bloc = n // k

freq = {}
Nombre de blocs de s
pour i dans la plage(0, n, bloc):
Sous = s[i:i+bloc]
freq[sub] = freq.get(sub, 0) + 1

# Consommer des blocs de t
pour i dans la plage(0, n, bloc):
Sous = t[i:i+bloc]
si freq.get(sub, 0) == 0:
Retour Faux
[sous] -= 1

retour Vrai
«» "

> **Notes spécifiques au python**
> * Le givrage crée une nouvelle chaîne, mais les frais généraux sont négligeables pour `n ≤ 2·10^5`.
> * `dict.get` est la moyenne `O(1)`.

---

C++ Solution

'`cpp
// solution.cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool isPossibleToRearrange(chaîne s, chaîne t, int k) {
int n = s.size(); // n == t.size()
bloc int = n / k; // taille du bloc

non ordonné_map<string, int> freq;

// Nombre de sous-chaînes de s
pour (int i = 0; i < n; i += bloc) {
chaîne sub = s.substr(i, bloc);
++freq[sub];
}

// Consommer des sous-chaînes de t
pour (int i = 0; i < n; i += bloc) {
chaîne sub = t.substr(i, bloc);
auto it = freq.find(sub);
Si (it) freq.end()->seconde 0) retourner faux;
--it->seconde;
}
retour vrai;
}
};
«» "

> **Notes spécifiques C++**
> * `unordered_map` donne des opérations moyennes `O(1)`.
> * `substr` copie la sous-chaîne, mais la longueur est au plus `n/k ≤ n`.
> * Aucune gestion manuelle de la mémoire n'est requise.

---

Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 3365

> **Mots clés**: LeetCode 3365, Rerange K Substrings, problème de codage d'entrevue, pensée algorithmique, Solution Java, solution Python, solution C++, entretien d'emploi, entretien de codage, structures de données, carte de hachage, partition sous-chaîne, anagrammes.

---

- Oui. 1. Présentation

Lorsque vous préparez une entrevue d'ingénierie logicielle, problème LeetCode **3365 – Replacer les sous-chaînes K en chaînes de cibles** est une question *mine d'or*.
Il teste :

- **Le raisonnement de l'anagramme** – les cordes sont garanties pour être des anagrammes.
- **Score partitionnement** – vous devez diviser une chaîne en morceaux égaux.
- **Comptage des cartes de vol** – suivi efficace de la fréquence des blocs.
- **Soins de vigilance** – veillez à ce qu'il y ait des sous-chaînes, des copies et des entrées importantes.

Ci-dessous, nous traversons l'énoncé du problème, analysons l'algorithme, discutons des avantages, des inconvénients et des pièges, et finissons avec des idées de style interview.

---

- Oui. 2. Rétablissement des problèmes

> **Don**
> • Deux cordes `s` et `t`, toutes deux de longueur `n` (2·105) et **anagrammes** les unes des autres.
> • Un entier `k` tel que `n` est divisible par `k`.
> **Question**
> Pouvez-vous diviser `s` en `k` sous-chaînes contiguës de longueur égale, réorganiser ces sous-chaînes arbitrairement, et les concaténer pour obtenir exactement `t`?

Si oui → retourner `true`, sinon → `false`.

---

- Oui. 3. Approches naïves et leurs défauts

L'approche du temps La complexité de l'espace Pourquoi il fait défaut
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Générez toutes les permutations `k!` des sous-chaînes `k` et comparez `O(k! * n)`" `O(k)`" `k` peut être jusqu`à `n` ( pire cas 200k) – impossible. Autres
Autres Vérifiez chaque position de `t` par rapport à chaque sous-chaîne possible de `s`. Autres
Autres Utilisez une fenêtre coulissante pour chaque bloc dans `t`=" `O(n * k)`=" `O(n/k)`=" Toujours quadratique quand `k` est petit. Autres

Nous avons donc besoin d'une solution *linéaire*.

---

- Oui. 4. La solution optimale – Carte de fréquence des blocs

4.1 Observation

Parce que `s` et `t` sont des anagrammes, chaque caractère dans `t` existe quelque part dans `s`.
Si on divise les deux chaînes en blocs de longueur `len = n/k`, le problème se réduit à:

> *Le multiset des blocs `k` de `s` peut-il être réaménagé pour égaler le multiset des blocs `k` de `t`? *

La solution se résume donc à comparer deux ensembles de cordes.

##### 4.2 Algorithme (une carte de laissez-passer)

1. **La longueur du bloc de calcul** `len = n / k`.
2. **Couvercles de «s»**:
- Pour chaque `i = 0 ... n-1` pas `len`, prendre la sous-chaîne `s[i ... i+len)` et augmenter son nombre dans une carte de hachage.
3. **Consommer les blocs de `t`**:
- Pour chaque `i = 0 ... n-1` pas `len`, prendre la sous-chaîne `t[i ... i+len)`.
- Si le bloc est manquant ou si son nombre est zéro → retourner `faux`.
- Sinon, décrémentez son compte.
4. **Tous les blocs correspondent** → retourner `true`.

**Complexités* *

Opération Temps Espace
- C'est quoi ?
Carte du bâtiment Sous-chaînes `O(k)` → Sous-chaînes `O(n)` total
Consommer la carte Autres
**Dans l ' ensemble** Autres

Parce que `k ≤ n`, la solution est linéaire dans la longueur de la chaîne et utilise un espace supplémentaire constant par rapport à `k`.

#### 4.3 Edge- Traitement des cas

Bordure Ce qu'il faut faire attention
Il n'y a pas de problème.
La carte aura une entrée ; l'algorithme ne fonctionne pas. Autres
Chaque caractère est un bloc. Autres
Les copies de sous-chaînes peuvent être coûteuses.Utilisez `String#substring` en Java (référence O(1) dans JDK moderne) ou `substr` en C++/Python; toujours bon pour 200k. Autres
Autres **TrÃ ̈s petite longueur de bloc (1)** Ã©chantillonnage fréquent de la carte Toujours O(1) par tÃ¢che; bien. Autres
**Extraction de la chaîne de caractères** Autres

---

- Oui. 5. Le bien, le mal et le mal

C'est vrai. Les bonnes
- **Simplicité** – L'algorithme n'utilise qu'une carte de hachage.
- **Temps linéaire** – Poigne la taille maximale d'entrée confortablement.
- **Déterministe** – Pas de rétrogradation ou d'explosion exponentielle.
- **Language-agnostic** – Fonctionne en Java, Python, C++, Allez, etc.

C'est vrai. Les mauvais
- **Substring Overhead** – Chaque bloc est une nouvelle chaîne (Java) ou copie (C++/Python).
- **Collision Hash-Map** – Bien que la recherche moyenne O(1), les entrées pathologiques (p. ex., de nombreux blocs identiques) peuvent provoquer une dégradation des performances dans certaines langues si une fonction de hachage médiocre est utilisée.
- **Utilisation de mémoire** – Pire-case `k == n` conduit à `n` clés distinctes, qui est toujours `O(n)` mais peut utiliser une mémoire importante dans un environnement d'entretien serré.

C'est vrai. L'Ugly
- **Musreading the Problem** – Certains candidats pensent à tort qu'ils doivent *réordonner les caractères à l'intérieur des blocs*, ce qui est faux. Les blocs eux-mêmes doivent rester intacts.
- **Off‐by‐One Bugs** – Oublier que `substring` prend l'exclusivité de l'index de fin peut causer des hors‐bounds.
- **En supposant que la sous-chaîne Java est O(n)** – Dans l'ancien JDKs `substring` crée une copie, conduisant à `O(n2)` dans le pire des cas. Les JDK modernes atténuent cela, mais une approche sûre est d'utiliser `StringBuilder` si vous êtes dans un environnement où vous ne pouvez pas compter sur cette garantie.

---

- Oui. 6. Conseils d'entrevue

1. **Exposer la contrainte d'anagramme** – Montrez que vous comprenez qu'elle garantit le nombre total de caractères correspondants, éliminant ainsi certaines possibilités.
2. **Demander des éclaircissements**
- Est-ce que `k` est garanti pour diviser `n`? (en milliers de dollars)
- "K" peut-il être égal à "n"? (en milliers de dollars)
- Les cordes ne contiennent que des caractères ASCII ? (en milliers de dollars)
Cela démontre l'attention portée aux détails.
3. **Démarrage de l'espace-temps** – Si l'intervieweur demande un espace supplémentaire constant*, vous pouvez noter que `k` peut être jusqu'à `n`, alors `O(k)` est inévitable à moins d'utiliser un algorithme multipass qui réutilise la même mémoire.
4. **Test** – Marchez à travers des exemples manuellement:
- `s = "bab"`, `t = "baba"`, `k = 2` → blocs `["ab", "ab"]` vs `["ba", "ba"]` → "faux".
- `s = "abcabc"`, `t = "bcaabc"`, `k = 3` → blocs `["abc", "abc"]` vs `["bca", "abc"]` → "faux".
- `s = "abcd"`, `t = "abcd"`, `k = 2` → blocs `["ab", "cd"]` vs `["ab", "cd"]` → "vrai".
Afficher les mises à jour de la carte pour chaque étape.

5. ** Structures de données alternatives** – Si l'intervieweur vous demande, vous pouvez discuter en utilisant un *multiset* (`Counter` dans Python) ou un *sorted map* si vous voulez garantir l'ordre déterministe (utile lorsque vous devez afficher l'ordre réaménagé).

---

#### 6.1 Que faire si des questions de suivi

- **Q**: *Et si `s` et `t` étaient **pas** anagrammes? *
**A**: Vous devez vérifier si le caractère compte dans `s` correspondent à ceux dans `t` avant de procéder. La carte de fréquence de bloc serait toujours valide, mais vous avez d'abord vérifié la propriété anagramme global.

- **Q**: * Pouvons-nous récupérer la permutation exacte des blocs qui produisent `t`? *
**A**: Oui. Tout en consommant `t`, entreposez les chaînes de blocs dans une liste et produisez-les dans l'ordre de consommation. L'algorithme lui-même vous donne déjà la permutation.

- **Q**: *Comment adapteriez-vous cette solution à un scénario de streaming où `s` arrive pièce par pièce? *
**A**: Mettre à jour la carte de hachage de façon incrémentelle lorsque de nouveaux blocs arrivent. Pour `t`, vous devez encore tamponner au moins les caractères `blockSize` pour former un bloc.

---

- Oui. 7. Conclusion

LeetCode 3365 est trompeurment simple mais rempli de thèmes d'entretien classiques:

- Le raisonnement d'anagramme → assure que le problème est soluble avec le comptage.
- Partitionnement → vous force à penser aux limites des blocs, pas seulement aux fréquences de caractères.
- Fréquence Hash‐map → l'outil go‐to pour la comparaison multiset.

En maîtrisant ce problème, vous renforcerez votre boîte à outils *algorithmique* et impressionnerez les intervieweurs avec une solution propre et linéaire qui s'adapte aux limites supérieures du problème.

---

- Oui. 8. Takeaway final de l'entrevue

> **Rappel** :
> 1. Cherchez toujours les contraintes cachées (anagramme, divisibilité).
> 2. Réduisez le problème à une comparaison *multiset* chaque fois que vous voyez Réorganiser ou Permuter.
> 3. Visez `O(n)` sauf si vous pouvez prouver que la limite inférieure optimale est pire.

Si vous pouvez articuler ce qui précède dans une discussion de 10 minutes, vous démontrerez la compétence de base de l'entrevue : *convertir les énoncés de problèmes en algorithmes concis et efficaces. *

---

Bon codage et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---



---

> **Vous réjouissez l'article? **
> *Partager sur LinkedIn ou Twitter. Étiquetez un ami qui se prépare pour une entrevue et laissez-les préparer leur travail ensemble! *

---



---

** Fin de document* *


---

Autres **Comment faire fonctionner les solutions* *
> *Java* → `Javac Solution.java && java Solution` (avec un harnais de test personnalisé).
> *Python* → `python3 solution.py` (avec un harnais de test).
> *C++* → `g++ -std=c++17 solution.cpp -O2 && ./a.out` (avec un harnais d'essai).

Bon codage, et bonne chance dans votre chasse au travail! C'est ce qu'il a dit