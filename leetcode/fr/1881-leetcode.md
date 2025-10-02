---
titre: LeetCode 1881. Maximum Valeur après insertion -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1881 – Maximum Valeur après insertion
C++** – Une solution propre pour chaque langue

> *Vous souhaitez décrocher ce rôle d'ingénierie logicielle? Maîtrisez ce problème LeetCode, montrez une implémentation polie, et vous vous démarquerez des intervieweurs.

Ci-dessous vous trouverez:

* Une étape par étape** de l'algorithme optimal.
* **Java, Python et code C++** – tout le temps O(n), O(1) espace supplémentaire.
* Un article de style **blog** qui explique le problème, le bon, le mauvais, le laid, et comment l'utiliser dans votre chasse au travail.

---

- Oui. 1. Récapitulation des problèmes

> *On vous donne un très grand nombre entier `n`, représenté comme une chaîne, et un nombre entier `x` (1‐9).
> `n` peut être négatif.
> Insérer `x` dans la représentation décimale de `n` (jamais à gauche du `-`) de telle sorte que l'entier résultant soit maximisé.
> Retourne le nouveau numéro comme une chaîne. *

«» "
Exemple
Entrée : n = "73", x = 6
Produit: "763"

Entrée : n = "-55", x = 2
Produit: "255"
«» "

"n.longueur ≤ 100 000", il faut donc éviter le temps quadratique.

---

- Oui. 2. Intuition – Pourquoi la règle de l'avidité fonctionne

Signe de l ' objectif stratégique
- C'est quoi ?
*Rendre le nombre plus grand *= Insérer `x` ** avant le premier chiffre qui est plus petit que `x`**. Le placer plus tôt donne plus de valeur. Autres
*Rendre le nombre moins négatif*. Insérer `x` ** avant le premier chiffre qui est plus grand que `x`**. Dans un nombre négatif, une plus petite valeur *absolue* est plus grande. Autres
Autres Pas de chiffre de ce genre.Appendient `x` à la fin (positif) / après tous les chiffres (négatif). Autres

La règle de l'avidité est optimale parce que chaque position est indépendante du reste – une fois que nous plaçons `x` à la première tache de "bonne" nous ne pouvons pas faire mieux.

---

- Oui. 3. Algorithme (temps O(n), espace O(1))

«» "
si n[0] == '-': // nombre négatif
pour i = 1 .. len-1:
si n[i] > x: // premier chiffre supérieur à x
insérer x avant n[i]
retour
// pas de tel chiffre -> annexe à la fin
retour n + x
Sinon: // nombre positif
pour i = 0 .. len-1:
si n[i] < x: // premier chiffre inférieur à x
insérer x avant n[i]
retour
// pas de tel chiffre -> annexe à la fin
retour n + x
«» "

*Nous travaillons uniquement avec la représentation des chaînes, donc aucun problème de débordement. *

---

- Oui. 4. Analyse de la complexité

Métrique Positif Négatif
C'est pas vrai.
Temps "O(len(n)") ""O(len(n)" Autres
Espace extra-atmosphérique `O(1)` (construction en place via le constructeur de cordes) Autres

`len(n)` ≤ 100 000, de sorte que la solution s'intègre facilement dans les délais.

---

- Oui. 5. Mise en oeuvre des références

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
chaîne publique maxValue(chaîne n, int x) {
StringBuilder sb = nouveau StringBuilder();
cx char = (char) ('0' + x);

si (n.charAt(0) == '-') { // négatif
sb.annexe('-');
booléen inséré = faux;
pour (int i = 1; i < n.longueur(); i++) {
si (!inserted && n.charAt(i) > cx) {
sb.appendice(cx);
inséré = vrai;
}
sb.append(n.charAt(i));
}
si (!insert) sb.append(cx); // appendice à la fin
} autre { // positif
booléen inséré = faux;
pour (int i = 0; i < n.longueur(); i++) {
si (!inserted && n.charAt(i) < cx) {
sb.appendice(cx);
inséré = vrai;
}
sb.append(n.charAt(i));
}
si (!insert) sb.append(cx); // appendice à la fin
}
retour sb.toString();
}
}
«» "

5.2 Python

'`python
Solution de classe:
def maxValue(self, n: str, x: int) -> str:
cx = str(x)
# Numéro positif
si n[0] != '-':
pour i, ch dans l'énumération(n):
si ch < cx:
retour n[:i] + cx + n[i:]
retour n + cx # aucune position trouvée

# Numéro négatif
pour i dans la plage (1, len(n)):
si n[i] > cx:
retour n[:i] + cx + n[i:]
retourner n + cx # ajouter à la fin
«» "

C++

'`cpp
solution de classe {
public:
chaîne maxValue(chaîne n, int x) {
char cx = '0' + x;
// Nombre positif
Si (n[0] != '-') {
pour (size_t i = 0; i < n.size(); ++i) {
si (n[i] < cx) {
retour n.substr(0, i) + cx + n.substr(i);
}
}
retour n + cx;
}

// Nombre négatif
pour (size_t i = 1; i < n.size(); ++i) {
si (n[i] > cx) {
retour n.substr(0, i) + cx + n.substr(i);
}
}
retour n + cx;
}
};
«» "

Les trois solutions fonctionnent dans le temps linéaire et l'espace auxiliaire constant, répondant aux contraintes de problème.

---

- Oui. 6. Article de blog – Le Bien, le Mal, et le Ugly de LeetCode 1881

> **Titre:** Mastering LeetCode 1881: *Valeur maximale après insertion* – Une plongée profonde pour les demandeurs d'emploi
> **Meta Description:** Découvrez la solution cupide optimale pour LeetCode 1881, consultez le code Java/Python/C++ et découvrez les conseils d'entretien qui vous aident à décrocher un rôle d'ingénieur logiciel.

---

6.1 Introduction

LeetCode est un élément essentiel du parcours de préparation de l'entrevue. Parmi les milliers de problèmes, **1881 – Maximum Value after Insertion** est une manipulation classique de chaîne + puzzle gourmand qui teste à la fois votre pensée et votre style de codage.

Si vous vous préparez pour des rôles à Google, Amazon, Microsoft, ou toute start-up à croissance rapide, en clouant ce problème démontre:

* ** intuition algorithmique** – repérer la règle avide.
* **Manipulation des caisses** – nombres négatifs, pas de position appropriée.
* ** Implémentation propre** – code qui est facile à lire et à exécuter dans O(n).

Ci-dessous, nous disséquons le problème, nous traversons la solution optimale, nous fournissons du code prêt à la copie en Java, Python et C++, et nous vous donnons des informations conviviales.

---

#### 6.2 Énoncé du problème (reformulé)

> Vous êtes donné un grand entier `n` comme une chaîne (chiffres 1‐9, peut-être négatif) et un entier chiffre `x` (1‐9).
> Insérer `x` quelque part dans la représentation décimale de `n` (jamais à gauche d'un `-`) pour rendre le nombre résultant le plus grand possible.
> Retourne le nouveau numéro comme une chaîne.

---

6.3 Pourquoi la règle de l'avidité est intuitive

1. **Nombres positifs**
Placer un chiffre plus grand plus tôt donne une valeur de place plus élevée.
→ *Insérer `x` avant le premier chiffre plus petit que `x`. *

2. **Nombres négatifs**
Dans un nombre négatif, une valeur absolue plus petite est plus grande. (en milliers de dollars)
→ *Insérer `x` avant le premier chiffre plus grand que `x`. *

3. **Si aucun tel chiffre n'existe**
Tous les chiffres sont déjà optimaux par rapport à `x`.
→ *Appliquer `x` à la fin. *

Cette règle simple est au cœur de la solution – elle supprime le besoin de tout dénombrement de force brute.

---

#### 6.4 Algorithme pas à pas

Texte
Si n commence par '-': // nombre négatif
Boucle de l'indice 1 à len(n)-1
Si n[i] > x: // premier chiffre supérieur à x
Insérer x avant n[i] et retourner
Ajouter x à la fin et retourner

Autre: // nombre positif
Boucle de l'indice 0 à len(n)-1
Si n[i] < x: // premier chiffre inférieur à x
Insérer x avant n[i] et retourner
Ajouter x à la fin et retourner
«» "

*Toutes les opérations sont O(1) par caractère → total temps O(n). *

---

6.5 Code prêt à courir

> **Java**
> ``java
> solution de classe publique {
> public Chaîne maxValue(String n, int x) { ... }
> }
> `` "

> **Python**
> ``python
> solution de classe:
> def maxValue(self, n: str, x: int) -> str: ...
> `` "

> **C++**
> ``cpp
> solution de classe {
> public:
> chaîne maxValue(chaîne n, int x) { ... }
> };
> `` "

*(Voir les implémentations complètes dans la section précédente.) *

---

6.6 Pièges communs

Pourquoi il casse
- Oui.
**Utiliser `int` pour le nombre**=100 000 chiffres débordement== Traiter l'entrée comme une *chaîne*; ne jamais convertir en type numérique. Autres
**Ignorer le signe négatif**.Insérer avant `-` change le signe. Autres
**Appending at the wrong position**.Pour les nombres positifs, l'ajout avant le dernier chiffre peut réduire la valeur. Autres
**En supposant que `x` est un char**. Autres
Erreurs hors-par-un** Erreurs dans les limites de la boucle (p. ex., commencer par `0` pour négatif) Autres

---

6.7 Ce que recherchent les intervieweurs

1. **Compréhension des problèmes** – Pouvez-vous redire la tâche dans vos propres mots?
2. **Le choix de l'algorithme** – expliquez-vous pourquoi l'avidité fonctionne au lieu de la force brute?
3. **Cas d'Edge** – nombres négatifs, tous les chiffres sont déjà optimaux, nombres à un chiffre.
4. **Complexité** – temps O(n), espace O(1); discuter pourquoi il est efficace.
5. **La propreté du code** – noms de variables lisibles, commentaires appropriés, conception modulaire.
6. **Testing** – montrez quelques exemples, y compris les cas de bord.

---

#### 6.8 Auto-rapide Liste de contrôle

- [ ] La poignée de code `n = "1"` et `x = 9`? → `"91"`
- [ ] La poignée de code `n = "-9"` et `x = 1`? → `"-19"`
- [ ] La poignée de code `n = "987654321"` et `x = 5`? → `"9876543215"` (pas de point d'insertion)
- [ ] La poignée de code `n = "-123456"` et `x = 7`? → `"-1237456"` (insérer avant `7`)

Si toutes les boîtes sont cochées, vous êtes prêt à donner à ce problème un score parfait!

---

### 6.9 À emporter – transformer un problème en atout de carrière

LeetCode 1881 est plus qu'un puzzle à cordes ; il s'agit d'une étude *mini-case* dans la conception algorithmique. La maîtrise vous donne :

* Confiance dans les techniques gourmandes.
* Un portefeuille de solutions multilingues propres (Java, Python, C++).
* Un point de discussion qui peut conduire à des questions plus profondes sur la manipulation des cordes dans les entrevues.

**Étape suivante:** Pratiquez le problème par vous-même, lancez le code de référence sur les entrées aléatoires, et soyez prêt à expliquer votre solution dans une entrevue de programmation par paires. Bonne chance – votre prochaine offre d'emploi pourrait être juste une insertion loin!

---

6.9 Pensées finales

Problèmes de manipulation de chaînes comme la surface LeetCode 1881 dans de nombreuses interviews de codage du monde réel. En internalisant la règle de l'avidité, en évitant les pièges communs, et en présentant une solution propre et efficace, vous allez non seulement résoudre le problème, mais également impressionner les gestionnaires d'embauche qui apprécient la clarté et la performance.

Bon codage, et que votre insertion vous débarque toujours la valeur maximale – et l'offre maximale!

---

> **Auteur:** Jane Doe – Ingénieure principale en logiciels, Plateformes AI & Cloud
> **Contact:** jane.doe@exemple.com **Lien:** /in/janedoe

---

- Oui. 7. Conclusion

Vous possédez maintenant :

* Une bonne compréhension** de LeetCode 1881 est une solution gourmande.
* **Code de référence** dans les trois langues principales.
* **Aperçu d'interview** qui transforme un problème de manipulation de chaîne en une vitrine de votre acuité algorithmique.

Utilisez ces connaissances pour pratiquer, polir et briller dans votre prochain entretien technique. Bonne chance !