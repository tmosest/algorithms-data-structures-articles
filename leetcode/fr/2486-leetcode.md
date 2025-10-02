---
titre: LeetCode 2486. Ajouter des caractères à la chaîne pour faire la séquence -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Ajouter des caractères à la chaîne pour faire la séquence – 2486 (LeetCode)

TL;DR
Trouvez le plus long préfixe de **t** qui apparaît déjà comme une subséquence dans **s**.
La réponse est simplement « len(t) – matched ».
Complexité: **O(n + m)** temps, **O(1)** espace.

---

## Déclaration du problème

On vous donne deux chaînes `s` et `t` contenant seulement des lettres anglaises minuscules.

Retourne le nombre minimum de caractères qui doit être ajouté à la *end* de `s` de sorte que `t` devienne un subséquence de la nouvelle chaîne.

> ** subséquence** – une chaîne qui peut être dérivée d'une autre en supprimant zéro ou plus de caractères sans changer l'ordre des caractères restants.

> **Exemples**

Explication
- C'est quoi ?
"Entraînement" "Codage" , 4 , Annexe "Codage". Autres
- "abcde" - "a" - "0" Déjà un subséquence. Autres
Ajouter "t" entier. Autres

**Contrôles* *

- `1 ≤ s. longueur, t. longueur ≤ 105 "
- Les mots `s` et `t` se composent uniquement de lettres anglaises minuscules.

---

Les bons, les mauvais et les méchants

Aspect Pourquoi ça compte Comment le gérer
C'est-à-dire
**Bon*** *L'approche à deux points* est linéaire et constante. "Itérer une fois sur les deux cordes, incrémenter des pointeurs seulement quand une correspondance est trouvée. Autres
Beaucoup de candidats confondent *subséquence* avec *sous-chaîne* ou *préfixe*. Gardez la définition à l'esprit; nous sommes des caractères correspondants dans l'ordre, mais ils peuvent être non contigus dans `s`. Autres
L'algorithme renvoie naturellement `len(t)` quand aucun caractère ne correspond. Pas besoin de manipulation spéciale. Autres

---

Algorithme – Deux pointeurs

1. **Initialiser deux indices**
`i` – indice dans `s` [0 ... "s.longueur-1"]
`j` – index dans `t` (... «t.longueur‐1»)

2. **Traverse ' s '**
Alors que `i < s.longueur` et `j < t.longueur`:
- Si `s[i] == t[j]`, déplacer **tous les deux** `i` et `j`.
- Sinon, ne bougez que "i".

3. **Résultat**
Le nombre de caractères laissés dans `t` est `t.length - j`.
C'est le nombre minimal de caractères qui doit être ajouté à `s`.

---

La preuve de l'exactitude

Laisser `k = j` après la boucle.
Tous les indices `0 ... k‐1` de `t` ont été appariés dans l'ordre `s`.
Par construction, aucun caractère ultérieur de `t` (`k ... t.length‐1`) n'a de caractère correspondant dans `s` après le préfixe assorti, sinon la boucle l'aurait assorti et augmenté `j`.

L'ajout du suffixe `t[k ...]` à la fin de `s` crée une nouvelle chaîne où les premiers caractères `k` de `t` sont déjà une subséquence (la partie correspondante) et le suffixe restant apparaît mot pour mot à la fin.
Ainsi `t` devient un subséquence de la nouvelle chaîne.

Aucun nombre plus petit de caractères ne peut suffire parce que chaque caractère de `t[k ...]` n'est pas présent dans la partie correspondante de «s».
Par conséquent, `t.longueur – k` est optimal.

---

Analyse de complexité

Calcul métrique
C'est pas vrai.
Chaque caractère de "s" est examiné au plus une fois.
* Espace * seulement deux indices entiers. Autres

---

Mise en œuvre

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.

- Oui. 1. Java

"Java
solution de classe {
Int annexe publique Caractères(String s, String t) {
i = 0, j = 0;
int n = longueur(), m = longueur();

(i < n& j < m) {
si (s.charAt(i) == t.charAt(j)) {
j++; // correspond à un caractère de t
}
i++; // toujours se déplacer dans s
}
retour m - j; // caractères à ajouter
}
}
«» "

> **Pourquoi cela fonctionne** – `i` scanne `s` linéairement. Chaque fois que nous touchons un caractère de `t`, nous déplaçons `j`. Après la boucle `j` est égal au plus long préfixe de `t` qui est un subséquence de `s`.

- Oui. 2. Python

'`python
Solution de classe:
def appendCaractéristiques(self, s: str, t: str) -> Int:
i = j = 0
alors que i < len(s) et j < len(t):
si s[i] == t[j]:
j += 1
i += 1
retour len(t) - j
«» "

- Oui. 3. C++

'`cpp
solution de classe {
public:
int appendiceCaractéristiques(chaîne s, chaîne t) {
i = 0, j = 0;
pendant que (i < (int)s.size() && j < (int)t.size()) {
si (s[i] == t[j]) ++j;
++i;
}
retour t.size() - j;
}
};
«» "

Les trois extraits suivent le même schéma de deux points.

---

## Essais unitaires (exemple de python)

'`python
def test():
sol = Solution()
affirme sol.appendCaractéristiques("coaching", "codage") == 4
affirme sol.appendCaractéristiques("abcde", "a") == 0
affirme sol.appendCaractéristiques("z", "abcde") == 5
affirme sol.appendCaractéristiques("", "abc") == 3
affirme sol.appendCaractéristiques("abc", "") == 0
affirme sol.appendCaractéristiques("aaa", "aaab") 1
print("Tous les tests ont réussi.")
«» "

Exécuter `python -m unittest` pour valider l'implémentation.

---

## SEO-Optimized Blog Post

> **Titre:** *Appendissez des caractères à la chaîne pour faire une séquence ultérieure – 2486.
> **Meta Description:** Master LeetCode #2486 avec une solution à deux points propre en Java, Python et C++. Comprendre les sous-séquences, les cas de bord et le temps d'exécution optimal.

Introduction

LeetCode 2486, Ajouter des caractères à la chaîne pour faire une séquence subséquente, est un favori pour les entretiens de manipulation de chaînes. Dans ce post, nous décrivons le problème, présentons une solution **fast** et **memory-friendly**, et livrons le code prêt à la copie en Java, Python et C++.

- Oui. Le problème en une seule ligne

> Trouvez le nombre minimal de caractères que vous devez ajouter à `s` afin que `t` devienne un subséquence de la nouvelle chaîne.

Pourquoi c'est une question d'entrevue classique

- Teste votre compréhension de **subséquence vs. substring**.
- Nécessite une solution **O(n+m)** ; de nombreuses solutions naïves fonctionnent dans un temps quadratique.
- Montrez votre compétence avec des techniques de **deux-pointeurs**, un élément essentiel dans les entrevues de codage.

### Aperçu de l'approche

1. Scan `s` avec un pointeur `i`.
2. Gardez un second pointeur `j` pour `t`.
3. Chaque fois `s[i]` est égal `t[j]`, incrément `j`.
4. Après l'analyse, `j` indique combien de caractères `t` ont été appariés.
5. La réponse est «len(t) – j».

C'est **temps linéaire** et **espace constant** – le meilleur que vous pouvez espérer.

Traitement des cas de bord

- `s` vide → response = `len(t)`.
- `t` plus longtemps que `s` → la même formule fonctionne.
- Dupliquer les lettres – le scan à deux points fonctionne toujours parce que nous ne nous soucions que de l'ordre, pas de la contiguïté.

Extraits de code

*(Insérer des blocs de code Java, Python, C++ d'en haut.) *

Suite de test de démarrage rapide

*(Insérer le code d'essai.) *

Résumé

La solution à deux points est la partie **bonne** : rapide, simple et facile à raisonner. La partie **bad** est la confusion entre la subséquence et la sous-chaîne ; rappelez-vous la définition ! La partie **ugly** apparaît souvent dans les cas de bord (chaînes vides, très longues `t`), mais l'algorithme les gère avec grâce sans branches supplémentaires.

**Vous voulez passer votre prochaine entrevue de codage?** Pratiquez ce problème, modifiez le code pour différentes langues, et expliquez clairement l'idée de deux points à votre intervieweur.

---

Les pensées finales

- ** Gardez à l'esprit la définition de la subséquence. **
- Oui. La solution à deux points est l'étalon or.
- Oui. L'implémentation est identique entre les langues – il suffit d'adapter la syntaxe.

Bonne chance avec votre pratique LeetCode et vos prochaines interviews ! Si vous avez aimé cet article, n'hésitez pas à le partager sur LinkedIn ou Twitter. Bon codage !