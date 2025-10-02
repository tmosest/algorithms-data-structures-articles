---
titre: LeetCode 3597. Chaîne de cloisonnement -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Mastering LeetCode 3597 – ** Chaîne de partition**
*Java • Python • Solutions C++ – Le Bon, le Mauvais et le Ugly (SEO-Optimized)*

---

- Oui. Pourquoi ce problème vous fait penser

- **Hard-er qu'il ne semble** – un trick cupide classique déguisé en un puzzle sous-string unique.
- **LeetCode #3597** – apparaît dans de nombreux ensembles d'entrevues de niveau intermédiaire (Google, Amazon, Microsoft).
- **Langues** – vous verrez la même logique implémentée en Java, Python et C++ – parfaite pour mettre en valeur la maîtrise multiplateforme.
- **Time & Space** – O(n) time & O(n) space – propre, évolutif et prêt à la production.

Si vous clouez ceci, vous allez démontrer:

1. ** Stratégie de grêle** – choisir le segment unique le plus court possible.
2. **Intusion de la structure des données** – ensembles de hachages par rapport aux cartes.
3. **Clean code** – concis, lisible et sans bug.

---

Rétablissement du problème

> Avec une chaîne `s` de lettres minuscules, partition `s` dans **unique** sous-chaînes.
>
> À partir de l'index `0`, continuer à prolonger la sous-chaîne actuelle jusqu'à ce qu'elle devienne *nouvelle* (n'est jamais apparue dans son ensemble).
> Une fois que la sous-chaîne est unique, ajoutez-la à la liste de réponses, marquez-la en tant que « Seen » et commencez à construire la prochaine sous-chaîne à partir du personnage suivant.
>
> Retournez la liste des sous-chaînes dans l'ordre où elles ont été créées.

> **Constraints**
> `1 <= longueur <= 105`
> `s` ne contient que des lettres anglaises minuscules.

---

## Intuition – Principe de l'avidité la plus courte

Considérez la corde comme une courroie transporteuse de lettres.
Lorsque vous construisez un segment, vous ne devez jamais dépasser** le premier point où le segment devient *nouveau*.
Si vous allez au-delà de ce point, vous perdez du temps et créez une sous-chaîne plus longue qui aurait été divisée plus tôt.

L'algorithme optimal est donc :

1. Démarrer un segment à l'index actuel.
2. Continuez à ajouter des caractères jusqu'à ce que le segment ne soit pas dans le jeu `seen`.
3. Ajoutez ce segment au résultat, ajoutez-le à `seen`, et lancez un nouveau segment à l'index suivant.

Cela fonctionne dans le temps linéaire parce que chaque caractère est traité exactement une fois.

---

Surmonter Affaire Ugly

Pourquoi il rompt les approches naïves
-- -- -- -- --------------------------------------------------
Une boucle emboîtée naïve peut tester à plusieurs reprises le même préfixe, causant O(n2). Autres
"Abcabcabc..." La règle de l'avidité nous assure de ne jamais construire d'"abcabc"; cependant, certaines implémentations permettent à tort des répétitions qui se chevauchent. Autres
Autres Très longue entrée (105).L'utilisation d'un `StringBuilder` qui copie des sous-chaînes à chaque fois peut faire exploser la mémoire/temps. Autres

La clé est d'utiliser un *hash-set* qui vérifie l'existence des sous-chaînes en O(1) et de construire le segment actuel progressivement.

---

Solutions de code

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe {
liste publique<String> partitionString(String s) {
int n = s.longueur();
Liste <String> ans = nouvelle liste de distribution<>();
Set<String> vu = nouveau HashSet<>();

StringBuilder cur = nouveau StringBuilder();
pour (int i = 0; i < n; i++) {
cur.append(s.charAt(i));
si (!see.contient(cur.àString())) {
as.add(cur.toString());
voir.add(cur.toString());
cur.setLength(0); // réinitialiser pour le segment suivant
}
}
le retour des an;
}
}
«» "

- **Time**: `O(n)` – chaque caractère joint une fois.
- **Espace**: "O(n)" – résultat + jeu.

---

- Oui. 2. Python 3

'`python
de taper l'importation Liste

Solution de classe:
def partitionString(self, s: str) -> Liste[str]:
vu = set()
ans = []
cur = []
pour ch en s:
cur.append(ch)
seg = ''.join(cur)
s'il n'est pas vu:
Annexe(seg)
voir.add(seg)
cur.clear()
retour et
«» "

Python"s `'.join()` sur une liste croissante est `O(len(cur)` mais globalement toujours linéaire parce que chaque char est joint exactement une fois.

---

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
partition vectorielle<string> Chaîne(s) {
unordered_set<string> vu;
vecteur <chaîne> ans;
chaîne de caractères cur;

pour (charc : s) {
cur.push_back(c);
si (!see.count(cur)) {
le nom et l'adresse de l'utilisateur;
voir.insérer(cur);
cur.clear();
}
}
le retour des an;
}
};
«» "

- **Unordered_set** donne "O(1)".
- "cur.clear()" garde la chaîne petite – pas de copies inutiles.

---

## Harnais d'essai complet (facultatif)

'`python
si __nom__ == "__main__" :
sol = Solution()
essais = [
("abbccd", "a", "b", "bc", "c", "cc", "d"]),
("abcabc", "a", "b", "c", "ab", "ca", "bc"]),
[(aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
"xyz", "x", "y", "z"]
- Oui.
pour inp, exp dans les essais:
out = sol.partitionString(inp)
s'il vous plaît.
print("Tous les tests sont passés!")
«» "

---

Ce que les intervieweurs recherchent

**Beau**
C'est quoi ?
**Liste pour suivre les sous-chaînes visibles → `O(n2)`. Autres
**Space‐efficace** – stocker uniquement les segments vus, pas tous les préfixes. Autres
**Cross‐lang limpidity** – algorithme identique en Java, Python, C++. ** Hypothèses implicites** – par exemple, que l'entrée ne contient que des lettres minuscules. **Pas de manipulation d'erreur** – échec silencieux sur les chaînes vides (bien que les contraintes l'interdisent). Autres

---

## Points d'entrevue

1. **Propreté grêle** – Montrez que vous pouvez expliquer pourquoi le segment unique le plus court est optimal.
2. **Le choix de la structure des données** – Hash-set vs. trie vs. map – discute des compromis temporels.
3. **Complexité** – Mettre l'accent sur "O(n)" – important pour les cordes de 105 longueurs.
4. **Test** – Cases limites de mention (toutes les mêmes lettres, motifs alternés).
5. **Pièges potentiels** – Si l'intervieweur mentionne que l'overlap est autorisé, préciser que les répétitions doivent être des sous-chaînes entières.

---

## SEO Meta (pour la plateforme de blog)

- **Titre**: Java, Python, C++ – Partition String LeetCode 3597 – Solution de préparation à l'entrevue
- **Description**: Guide étape par étape du LeetCode 3597 – Chaîne de partitions. Apprenez la stratégie gourmande, les cas de bord, et obtenez le code Java propre, Python et C++ pour les interviews. (en milliers de dollars)
- **Mots-clés**: *LeetCode Partition String*, *Java solution*, *Python solution*, *C++ solution*, *Greedy algorithme*, *Hash-set*, *Interview problem*, *Resume boost*, *Coding interview*.

---

Les pensées finales

Partition String est un bijou **tiny** dans la boîte à outils LeetCode.
Avec un seul passe gourmand et un seul hachage, vous pouvez le résoudre en temps linéaire, indépendamment de la taille des entrées.

**Bien** – logique avide propre, O(n) complexité.
**Bad** – suringénierie ou boucles imbriquées menant à O(n2).
**Ugly** – mauvaise utilisation de la mémoire ou mauvaise construction de la chaîne causant TLE sur de grandes données.

La maîtrise de ce problème démontre que vous pouvez *transférer un algorithme concis en plusieurs langues*, un trait que recherche chaque ingénieur senior. Bon codage – et bonne chance pour votre prochaine entrevue!