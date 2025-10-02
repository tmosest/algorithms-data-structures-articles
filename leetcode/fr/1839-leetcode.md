---
titre: LeetCode 1839. La plus longue sous-chaîne de tous les Vowels dans l'ordre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1839 – La plus longue Substring
### Bonne, mauvaise et laid: Une plongée profonde dans Vowel Sous-chaînes de commande (Java / Python / C++)

> **TL;DR** – Scannez la chaîne une fois avec une stratégie *greedy bi-pointer*.
> Heure: **O(N)**, Espace: **O(1)**.
> Trois solutions prêtes à passer (Java, Python, C++) sont fournies.

---

Récapitulation des problèmes

> **Input** – Une chaîne `word` qui ne contient que les cinq voyelles: `a, e, i, o, u`.
> **Objectif** – Retourne la longueur de la plus longue substrante contiguë
> 1. Contient **tous** cinq voyelles ** au moins une fois**.
> 2. Apparaît dans **ordre alphabétique strict** (`a...e...i...o...u`).

Si aucune sous-chaîne n'existe, retourner `0`.

> **Exemples**
> *aeiaaioaaaaaeiiiiouuuooaauuaeiu '* → **13** (aaaaeiiiiouuu')
> *'aeeiiiioooauuaeiou`* → **5** (`aeiou`)
*'a'* → **0**

---

C'est vrai. La Brute Approche de la force

La solution la plus intuitive est de générer *chaque* sous-chaîne, de vérifier les deux conditions et de garder la plus longue.
Texte
pour i en [0..n-1]:
pour j en [i+1..n]:
Sous = mot[i:j]
i est Beautiful(sub): best = max(best, len(sub))
«» "
**Pourquoi c'est mauvais**

Sujet Impact
C'est quoi ?
Sous-chaînes O(N2) Autres
O(N) par contrôle
Autres Frais généraux de mémoire élevée

Même avec les optimisations, il n'a pas passé les limites de temps de LeetCode.

---

C'est vrai. La stratégie optimale

#### # Points de vue fondamentaux
Pendant l' itération, nous pouvons *réinitialiser* chaque fois que l'ordre voyelle rompt.
Une sous-chaîne est valide **seulement** si elle avance dans la séquence voyelle.
D'où un seul balayage linéaire suffit.

#### Sliding-Window + Greedy

Sens de la variable
C'est pas vrai.
Indice de départ de la sous-chaîne actuelle du candidat
Combien de voyelles distinctes nous avons vues dans l'ordre (1...5)
La plus longue longueur de sous-chaîne trouvée jusqu'à présent

**Algorithme**

«» "
ans = 0
gauche = 0
étape = 1 // nous avons vu au moins un 'a' à la position 0

pour i de 1 à n-1:
if word[i] < word[i-1]: // commander cassé → nouvelle fenêtre
étape = 1
gauche = i
Sinon si mot[i] > mot[i-1]: // nous avons marché vers la prochaine voyelle
étape += 1

Si étape == 5: // nous avons vu a-e-i-o-u
ans = max(ans, i - gauche + 1)

retour et
«» "

**Pourquoi ça marche* *

- **Vérification de la commande**: Si la voyelle actuelle est *moins* que la précédente, la sous-chaîne ne peut pas continuer; nous devons commencer à nouveau à `i`.
- **Progression**: Si c'est *plus grand*, nous passerons à la prochaine voyelle.
- **Répétition**: Les caractères égaux (`'a'` → `'a`) ne changent pas `stage`; ils allongent simplement la fenêtre actuelle.
- ** Ensemble complet**: Quand `stage` atteint 5 nous savons que la fenêtre contient les cinq voyelles dans l'ordre, donc nous comparons sa longueur.

---

Mise en œuvre du code

> **Astuce** – Toutes les solutions fonctionnent dans *O(N)* temps, *O(1)* espace supplémentaire, et gérer la taille d'entrée maximale sans effort.

##### 4.1 Java (Readable, Constante-Espace)

"Java
solution de classe publique {
Int public le plus longtempsBeautifulSubstring(String word) {
int ans = 0, gauche = 0, étape = 1; // étape 1 signifie que nous avons déjà un 'a'

pour (int i = 1; i < word.longueur(); i++) {
char prev = word.charAt(i - 1);
char curr = mot.charAt(i);

si (curr < prev) { // ordre cassé
étape = 1;
gauche = i;
} sinon si (curr > prev) { // voyelle suivante
étape++;
}
si (étape) 5) {
ans = Math.max(ans, i - gauche + 1);
}
}
le retour des an;
}
}
«» "

4.2 Python (légant et rapide)

'`python
Solution de classe:
def leastBeautifulSubstring(self, word: str) -> Int:
ans = gauche = 0
étape = 1 # 1 -> 'a', 2 -> 'e', ... 5 -> 'u'

pour i dans la plage(1, len(mot)):
Prév, cur = mot[i-1], mot[i]
Si cur < prev: # rupture de commande
étape, gauche = 1, i
elif cur > prev: # passer à la prochaine voyelle
étape += 1

Si étape == 5: # toutes les voyelles vues
ans = max(ans, i - gauche + 1)

retour et
«» "

*### 4.3 C++ (Fat & Memory-Efficace)

'`cpp
solution de classe {
public:
int le plus longBeautifulSubstring(mot chaîne) {
int ans = 0, gauche = 0, étape = 1; // étape compte les voyelles dans l'ordre

pour (int i = 1; i < word.size(); ++i) {
char prev = mot[i-1];
char cur = mot[i];

si (cur < prev) { // réinitialiser
étape = 1;
gauche = i;
} sinon si (cur > prev) { // passer à la voyelle suivante
+ étape;
}

si (étape) 5) {
ans = max(ans, i - gauche + 1);
}
}
le retour des an;
}
};
«» "

---

C'est vrai. Edge Cases & Gotchas

Autres Décision Pourquoi ça compte ?
Il n'y a pas de lien entre les deux.
**Single voyelle** (par exemple, `"a"` ou `"uuu"`) )
**Re-démarrage de la fenêtre au milieu**
*Dupliquer les voyelles *Dupliquer les voyelles *Dupliquer les voyelles *Dupliquer les voyelles *Dupliquer les voyelles
Utiliser des indices, non des objets sous-chaînes

---

Résumé de la complexité

Langue Heure Espace
- C'est quoi ?
*Java*
Python **O(N)**
* * * * * * * * * * *

"N" = "mot.longueur()"

---

### # 7-

1. **En supposant qu'il contient toutes les voyelles.
Soyez explicite que chaque voyelle doit apparaître et l'ordre compte.

2. **Utilisation de `set` ou `HashMap` pour chaque fenêtre* *
Ce serait O(N2) dans le pire des cas. Le scan gourmand est la solution prévue.

3. **Sur-optimisation avec le régex**
Les expressions régulières peuvent être élégantes mais sont difficiles à justifier dans une entrevue.

4. **Négligence du cas de réinitialisation**
Oublier de réinitialiser `stage` lorsque l'ordre casse conduit à de mauvaises réponses.

---

### # 8-

- **Commencez avec un plan de force brute** – il clarifie les contraintes.
- **Choisissez des scans linéaires** – la plupart des problèmes de chaînes avec des contraintes d'ordre se résument à un seul passage.
- **Les machines d'état sont importantes** – `stage` est essentiellement une petite machine à état fini qui suit les progrès dans la séquence de voyelles.
- **La lisibilité du code est la clé** – même un seul liner dans Python devrait avoir des commentaires clairs pour les intervieweurs.
- **Les compromis entre le temps et l'espace** – ici, nous avons délibérément gardé la mémoire minimale parce que la taille des entrées est énorme.

---

Autres ressources

Lien Ce qu'il offre
-- -- -- -- -- --
[LeetCode 1839](https://leetcode.com/problèmes/longest-substring-of-all-vowels-in-order/) Une page de problème avec des cas de test
Autres [Solution Java – Constante Space](https://leetcode.com/problèmes/longest-substring-of-all-vowels-in-order/solutions/1175715/java-readable-code-constant-space-by-him-eip2/) Solution originale de Himanshu Chhikara Autres
(https://leetcode.com/problems/longest-substring-of-all-vowels-in-order/solutions/6798204/sliding-window-easy-by-vivek011299-jv7q/) Code Python propre
Autres [C++ Version – O(N) Two-Pointer](https://leetcode.com/problems/longest-substring-of-all-vowels-in-order/solutions/6622943/longest-beautiful-substring-c-solution-t/) Rapide et concis

---

Dernier verdict

Le problème de la sous-chaîne est un parfait exemple de la façon dont un *simple scan avide* transforme un cauchemar O(N2) en une brise O(N).

Copiez l'un des trois extraits de code, soumettez-le, et vous obtiendrez **AC** sur LeetCode 1839 en millisecondes.

Bonne chance – et que votre entrevue soit aussi ordonnée qu'une séquence de voyelles -beautiful--! C'est ce qu'il a dit.

---

> **Auteur** – *Favoris Stack-Overflow & LeetCode, transformant constamment les problèmes déconcertants en code propre et efficace. *
> **Contact** – GitHub: `@codingwizard`- LinkedIn: `linkedin.com/in/codingwizard "

---

> *Si vous avez aimé ce post, star le repo, partager avec des amis, et laisser un commentaire si vous l'avez trouvé utile! *
---

""diff
♪ Fin du blog
«» "