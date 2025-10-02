---
titre: LeetCode 2914. Nombre minimum de modifications pour rendre la chaîne binaire belle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – LeetCode 2914 Nombre minimum de modifications à faire Binary String Beautiful

Le problème se résume à **correspondant à la paire**.
Pour une chaîne binaire de longueur égale `s = s0 s1 ... s(n-1)` nous pouvons le diviser en
sous-chaînes de longueur 2:
«(s0,s1)» (s2,s3)...».
Chaque paire doit devenir tout-zéro ou tout-un.
Changer un caractère dans une paire corrige toute la paire, donc la stratégie optimale
est:

«» "
réponse = nombre de paires adjacentes (si,si+1) où si != Si+ 1
«» "

C'est le nombre minimal de tours requis.

Voici des solutions propres, O(N) dans **Java**, **Python** et **C++**.

---

### Java

"Java
// LeetCode 2914 – Nombre minimum de modifications pour rendre la chaîne binaire belle
solution de classe {
int public minChanges(String s) {
changements int = 0;
// itérer par étapes de 2 – regarder chaque paire
pour (int i = 0; i < s.longueur(); i += 2) {
// si les deux caractères diffèrent, nous avons besoin d'un flip
si (s.charAt(i) != s.charAt(i + 1)) {
modifications++;
}
}
les changements de retour;
}
}
«» "

---

Python

'`python
# LeetCode 2914 – Nombre minimum de modifications pour rendre la chaîne binaire belle
Solution de classe:
def minChanges(self, s: str) -> Int:
changements = 0
pour i dans la plage(0, len(s), 2):
si s[i] != [i + 1]:
changements += 1
changement de retour
«» "

---

C++

'`cpp
// LeetCode 2914 – Nombre minimum de modifications pour rendre la chaîne binaire belle
solution de classe {
public:
int minChangers(chaîne s) {
changements int = 0;
pour (int i = 0; i < (int)s.zize(); i += 2) {
si (s[i] != s[i + 1]) + + changements;
}
les changements de retour;
}
};
«» "

Les trois solutions fonctionnent dans **O(n)** temps, utiliser **O(1)** espace supplémentaire, et
conforme à la signature attendue de LeetCode.

---

- Oui. 2. Article de blog – Code de Leet 2914: La Belle Chaîne Binary – Bon, Mauvais, et Ugly

> **SEO Mots-clés**: *LeetCode 2914, changements minimums, belle chaîne binaire, interview de codage, interview d'algorithme, solution Java, solution Python, solution C++, algorithme gourmand, correction par paire, prep d'interview*

---

- Oui. Quel est le problème?

Sur le code de Leet
(Problème 2914) vous êtes donné une chaîne binaire de longueur pair `s`.
Une chaîne est **beau** si vous pouvez la diviser en sous-chaînes, chacune :

* Même longueur (ainsi la scission sera toujours en paires de deux caractères)
* Tous zéro ou tous un.

Vous pouvez retourner n'importe quel personnage.
Retournez les flips *minimum* nécessaires pour rendre toute la chaîne belle.

---

L'intuition – L'avidité de la paire

Parce que chaque sous-chaîne doit avoir une longueur égale, la division naturelle est en * paires adjacentes*:

«» "
(n-2) s(n-1)
«» "

Si une paire contient déjà deux bits égaux (00 ou 11), nous sommes bons.
Si non (01 ou 10), nous *must* flip **exactement un** des deux bits pour rendre la paire belle.
Les flips en différentes paires n'interfèrent pas entre eux, donc le meilleur
la stratégie est simplement:

> Compter combien de paires ont des bits mal appariés ; ce compte est la réponse.

Pas de DP, pas de rétro-tracking, pas de cupidité.
C'est pourquoi ce problème a une solution d'avidité pure**.

---

Analyse de complexité

Temps Espace
C'est pas vrai.
Solution **O(n)** – un passage sur la chaîne **O(1)** – un seul compteur
Autres où `n = s.longueur()` Autres

Avec `n ≤ 105`, cela fonctionne en microsecondes dans toutes les langues principales.

---

Mise en œuvre – Code Bon

Vous trouverez ci-dessous la mise en œuvre *propre, prête à la production* en trois langues.

*Java*

"Java
solution de classe {
int public minChanges(String s) {
changements int = 0;
pour (int i = 0; i < s.longueur(); i += 2) {
si (s.charAt(i) != s.charAt(i + 1) change++;
}
les changements de retour;
}
}
«» "

*Python*

'`python
Solution de classe:
def minChanges(self, s: str) -> Int:
changements = 0
pour i dans la plage(0, len(s), 2):
si s[i] != [i+1]:
changements += 1
changement de retour
«» "

*C++*

'`cpp
solution de classe {
public:
int minChangers(chaîne s) {
changements int = 0;
pour (int i = 0; i < (int)s.zize(); i += 2)
si (s[i] != s[i+1]) ++ change;
les changements de retour;
}
};
«» "

Chaque version:

* Gérez la garantie d'une longueur uniforme en toute sécurité
* Utilise une simple boucle "pour" qui marche par deux
* Effectue une seule vérification `si` par paire

---

Les pièges à éviter

Pourquoi c'est mauvais
C'est le cas.
**Itération sur chaque caractère** (`i++` au lieu de `i+=2`) Utiliser `i += Chaque paire n'est inspectée qu'une seule fois. Autres
**Flipping the wrong bit** (p. ex., toujours changer le premier bit) Un seul "si" chèque suffit; pas besoin de décider *qui* bit à basculer. Autres
**En supposant que la chaîne peut être d'une longueur impair**.LeetCode garantit une longueur égale, mais un contrôle supplémentaire pourrait coûter du temps supplémentaire O(1) sans aucun avantage. Autres Faites confiance aux contraintes du problème; évitez toute validation supplémentaire. Autres
**L'utilisation d'une chaîne ou d'un tableau mutable ne serait pas nécessaire**. Travailler avec `charAt` / l'indexation de tableau; garder l'empreinte de mémoire constante. Autres

---

Les anti-patterns

L'anti-pattern Pourquoi il est laid
C'est le cas.
Une solution récursive naïve pourrait frapper le débordement de la pile pour `n = 105`. Rec(String s, int idx)` qui s'appelle pour chaque paire. Autres
**Utiliser le regex ou la chaîne scinde**=La division de la chaîne en paires puis la vérification de chaque paire est surkill. "s.split("(..)")" ou "Pattern.compile("(?<=..)(?=..)" etc. Autres
Autres **Copier la chaîne sur chaque itération**="s = s.remplace(...)` dans une boucle crée de nouvelles chaînes à chaque fois. Gardez la corde originale intacte; comptez seulement les erreurs. Autres
**Indicateurs de codage à l'arrêt**= si (s[0] != s[1]) ...` puis répéter pour toutes les paires manuellement. Utilisez une boucle pour généraliser. Autres

---

### ♫ A emporter pour les intervieweurs et les personnes interviewées

1. **Reconnaissez le motif** – La longueur même → divisée en paires suggère immédiatement un balayage linéaire.
2. **Correctivité de la graisse** – Chaque paire est indépendante; une solution locale est globalement optimale.
3. ** Temps/Espace** – O(n)/O(1) est plus que suffisant; pas besoin de structures de données de fantaisie.
4. **Cas d'Edge** – La chaîne est toujours uniforme ; l'algorithme gère naturellement tous les zéros ou tous les zéros avec aucun changement.
5. **Test** – Couverture :
* Toutes les paires sont égales à → 0 changements
* Toutes les paires différentes → n/2 changements
* Alternant 0101... → n/2 changements
* Mélanges aléatoires → calculer manuellement

---

Lire plus

* **Greedy Algorithms** – Comprendre quand les choix locaux conduisent à un optimum global.
* ** Programmation dynamique** – Pour des problèmes de partition plus complexes ; ici DP serait surkill.
* **LeetCode Discuter – Problème 2914** – De nombreux contributeurs partagent des variations et des preuves alternatives.

---

Verdict final

*Bonne* : Un compteur à un passage et à deux est la solution optimale.
*Bad*: La suringénierie, les boucles inutiles ou les copies mutables perdent du temps et de l'espace.
*Ugly* : Les indices de récursion, de régex ou de code dur rendent le code difficile à lire et à maintenir.

Avec les extraits de code ci-dessus, vous pouvez soumettre avec confiance à LeetCode, as l'entrevue, et mettre en valeur votre capacité à repérer la solution avide élégante. Bon codage !