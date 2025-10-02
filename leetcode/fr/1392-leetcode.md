---
titre: LeetCode 1392. Le plus long préfixe heureux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le plus long préfixe heureux – LeetCode 1392
**Algorithme, code (Java / Python / C++), et référence Article de blog optimisé**

---

Récapitulation des problèmes

Point de détail
- C'est quoi ?
**LeetCode ID**
**Titre** Autres
Difficulté
Un préfixe *happy* est un préfixe **non-vide** de `s` qui est aussi un suffixe (mais pas toute la chaîne). Autres
Retourner le plus long préfixe heureux de la chaîne donnée `s`. Retourner `""` si aucune n'existe. Autres
**Constraints**= `1 ≤ s.longueur ≤ 105` <br> `s` ne contient que des lettres anglaises minuscules. Autres

> **Exemple**
> `s = "bab"` → le plus long préfixe heureux = `"bab"`

---

- Oui. Pourquoi la Naïve O(n2) Brute Force Fails

L'idée la plus simple est de vérifier chaque préfixe contre chaque suffixe, ce qui prend **O(n2)** temps.
Avec `n = 105`, cela signifie que les opérations de 1010 – bien au-delà des limites pour un juge en ligne ou un vrai entretien.

---

- Oui. L'approche gagnante – KMP / LPS Array

### ♫ Aperçu des clés
Le plus long préfixe qui est aussi un suffixe est exactement la dernière valeur du tableau **Longest Prefix‐Suffix (LPS)** de l'algorithme de correspondance des chaînes KMP.

- **LPS[i]** = longueur du plus long préfixe approprié de `s[0...i]` C'est aussi un suffixe de cette sous-chaîne.
- La réponse est simplement "s.substr(0, LPS[n‐1])".

Étapes de l'algorithme

1. **Construisez le tableau LPS** en un seul scan de gauche à droite.
- `len` garde la longueur actuelle du LPS.
- Quand `s[i] == s[len]` → `len++` et définir `lps[i] = len`.
- Sinon, réduire `len` à `lps[len-1]` jusqu'à ce qu'il y ait un match ou un match.
2. **Retour** la sous-chaîne `s[0: lps[n-1]]`.

Complexité
- **Time**: `O(n)` – un passage sur la chaîne.
- **Espace**: `O(n)` – le tableau LPS.
(Une version à espace constant est possible mais inutile pour `n ≤ 105'.)

---

Code en trois langues

Voici les implémentations prêtes à être lancées.
Tous suivent la même logique – build LPS, return prefix.

### Java

"Java
solution de classe publique {
public Chaîne plus longue Préfixe(String s) {
int n = s.longueur();
int[] lps = nouvelle int[n];
int len = 0; // longueur du suffixe préfixe précédent le plus long
i = 1;

pendant que (i < n) {
si (s.charAt(i) == s.charAt(len) {
len++;
lps[i] = len;
i++;
} autre {
Si (len != 0) {
len = lps[len - 1];
} autre {
lps[i] = 0;
i++;
}
}
}
// le plus long préfixe heureux est les premiers caractères lps[n-1]
retourner s.substring(0, lps[n - 1]);
}
}
«» "

Python

'`python
Solution de classe:
def leastPrefix(self, s: str) -> str:
n = len(s)
lps = [0] * n
longueur = 0 # longueur du suffixe préfixe précédent le plus long
i = 1

alors que i < n:
si s[i] == s[longueur]:
longueur += 1
lps[i] = longueur
i += 1
Sinon:
si longueur != 0:
longueur = lps[longueur - 1]
Sinon:
lps[i] = 0
i += 1

# le plus long préfixe heureux
retour s[:lps[n - 1]]
«» "

C++

'`cpp
solution de classe {
public:
chaîne plus longue Préfixe(chaîne s) {
int n = s.size();
vecteur<int> lps(n, 0);
int len = 0; // longueur du suffixe préfixe précédent le plus long
i = 1;

pendant que (i < n) {
si (s[i] == s[len] {
++len;
lps[i] = len;
++i;
} autre {
Si (len != 0) {
len = lps[len - 1];
} autre {
lps[i] = 0;
++i;
}
}
}
retour s.substr(0, lps[n - 1]);
}
};
«» "

> **Test**
> ``java
> Solution sol = nouvelle solution();
> System.out.println(sol.longestPrefix("ababa")); // imprime "ab"
> `` "

---

C'est pas vrai. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**L'élégance algorithmique**=KMP donne une solution *O(n*) – le facteur ultime de l'interview. L'approche brute-force O(n2) est élégante dans sa simplicité mais pratiquement inutilisable pour les grandes cordes. Une mauvaise mise en œuvre de la mise à jour LPS (erreurs hors-par-un) peut donner des résultats erronés en silence, surtout lorsque la chaîne entière est une répétition d'un motif plus petit. Autres
**Lisibilité du code**= Effacer les noms de variables (`len`, `lps`, `i`) pour aider les futurs responsables. Des macros trop compliquées ou un état global caché peuvent cacher des bugs. L'utilisation d'un « lps[i] = s.substr(...) » à l'intérieur de la boucle crée des sous-chaînes inutiles, ce qui nuit aux performances. Autres
**Edge-case safety**=Poigne les chaînes de longueur 1 → retourne `""`.=En oubliant de manipuler `len== 0` dans l'autre branche conduit à des boucles infinies. Ne pas vérifier que le préfixe retourné est *strictement* plus petit que la chaîne originale peut mal classifier la chaîne entière comme un préfixe heureux (invalide par problème). Autres
**L'utilisation de la mémoire**=Le tableau `O(n)` est négligeable pour `n ≤ 105`. En stockant une table complète de 2-D DP, vous seriez surqualifié. Il est possible de tenter de réduire la mémoire à « O(1) » en rejetant le tableau LPS, mais cela ajoute une complexité qui en vaut rarement la peine. Autres
La fonction LPS est une sous-routine classique utilisée dans de nombreux problèmes d'appariement de motifs. Il est redondant d'écrire un chèque de force pour chaque entrevue. La suringénierie d'une bibliothèque LPS super-générique qui gère des modèles de différents jeux de caractères peut masquer la logique de base. Autres

---

Article sur le blog optimisé du SEO

> **Titre**: *Le plus long préfixe heureux (LeetCode 1392) – KMP en Java, Python, C++

> **Meta Description**: Maîtrisez le problème de "Longest Happy Prefix" avec une solution KMP propre. Préparez-vous à coder des interviews avec des extraits de code Java, Python et C++, en plus d'un guide convivial SEO.

---

Comprendre le plus long préfixe heureux

Lorsque les intervieweurs demandent le plus long préfixe qui est aussi un suffixe (à l'exclusion de la chaîne entière), ils testent essentiellement votre familiarité avec les algorithmes de chaînes, en particulier l'algorithme Knuth‐Morris‐Pratt (KMP). La maîtrise de KMP déverrouille toute une classe de problèmes, depuis l'appariement des motifs jusqu'à l'établissement de la longueur des bordures dans les séquences d'ADN.

Pourquoi KMP bat Brute Forcer

- **Temps linéaire**: «O(n)» versus «O(n2)» pour les vérifications naïves.
- **Performance prévisible**: gère efficacement le pire cas (par exemple, "aaaa...a").
- **Widely Reconnu**: Démontre que vous comprenez les fondamentaux algorithmiques.

La mise en œuvre de LPS dans votre langue préférée

Code rapide Remarques
C'est quoi, ça ?
* Voir l'extrait de Java ci-dessus * Utiliser `String.charAt()` pour l'accès O(1) char. Autres
* Voir l'extrait de Python ci-dessus. * La compréhension de la liste pour `lps` est bonne, mais la boucle maintient l'utilisation de la mémoire faible. Autres
* Voir l'extrait de code C++ ci-dessus. Autres

Étape par étape

1. **Initialiser** `lps[0] = 0`, `len = 0`, `i = 1`.
2. **Loop** tandis que `i < n`:
- **Match** → `len++`, set `lps[i] = len`, `i++`.
- **Mismatch** → si `len > 0` → `len = lps[len-1]`; sinon `lps[i] = 0`, `i++`.
3. **Résultat**: "s.substr(0, lps[n-1)]".

Les cas d'Edge à regarder

- Cordes à caractères simples → pas de préfixe heureux.
- Chaîne entière est un motif répété → la réponse est le plus grand préfixe / suffixe approprié.
- L'entrée vide de la chaîne est refusée par les contraintes, mais mérite toujours d'être protégée dans le code de production.

Résumé du rendement

Complexité
C'est pas vrai.
**Heure**="O(n)" – chaque caractère est examiné au plus deux fois. Autres
**L'espace**=O(n)= – le tableau LPS. Autres

Comment résoudre ce problème dans une entrevue

1. ** Expliquez l'intuition**: "Le problème est une requête LPS classique."
2. **Afficher l ' algorithme**: Décrivez la construction du KMP et la tranche finale.
3. **Code dans la langue de l'intervieweur**: Fournir une mise en œuvre propre et testée.
4. ** Validation des cas de bordure**: Demandez des caractères simples ou des motifs répétés.
5. **Discuss extensions**: Mentionnez comment la même logique LPS résout les requêtes à la frontière dans d'autres problèmes.

Mots clés amis

- Le plus long préfixe heureux
- Solution LeetCode 1392
- Algorithme KMP
- tableau LPS
- Entretien par algorithme de chaîne
- Correspondance de la chaîne Java
- Entretien de codage Python
- Problèmes d'interview C++
- Préparation de l'entrevue algorithmique
- Des solutions de chaînes efficaces

Utilisez ces mots clés naturellement dans les titres, les points de puce et la méta description pour attirer les recruteurs à la recherche de talents algorithmiques.

---

C'est pas vrai. Dernier départ

Le problème **Longest Happy Prefix** est une application de manuel du tableau **KMP LPS**. Avec un seul balayage linéaire, vous pouvez retourner le plus long préfixe approprié qui est également un suffixe. Les solutions Java, Python et C++ propres ci-dessus devraient vous aider à aser l'interview et à délimiter ce rôle technologique.

Bon codage ! C'est ce qu'il a dit