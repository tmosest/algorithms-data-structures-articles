---
Titre: LeetCode 2869. Opérations minimales pour collecter des éléments -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solution en trois langues

Ci-dessous vous trouverez des implémentations propres et prêtes à la production des **Opérations Minimum pour Collecter des Elements** (LeetCode 2869) dans **Java**, **Python** et **C++**.
Tous les trois suivent la même logique O(n) : itérer le tableau à partir du dos, conserver un ensemble des nombres collectés qui sont ≤ k, et s'arrêter dès que la taille de l'ensemble est égale à k.

"Java
// Java (Java 17)
Importation de java.util.*;

solution de classe publique {
Int min. d'opérations (liste <entier> nombres, int k) {
Total des opérations nécessaires
Int ops = 0;
// conserver les éléments uniques que nous avons recueillis (seulement ceux ≤ k)
Définir<integer> vu = nouveau HashSet<>();

// itérer de la fin – qui est le seul ordre que nous pouvons supprimer
pour (int i = nombres.size() - 1; i >= 0; i--) {
ops++; // une opération de suppression
val int = nums.get(i);
si (val <= k) {
voir.add(val); // nous ne nous soucions que de 1...k
}
si (seen.size() == k) pause; // tous les nombres nécessaires sont collectés
}
les opérations de retour;
}
}
«» "

'`python
# Python (Python 3,11)
de taper l'importation Liste

Solution de classe:
def minOperations(self, nombres: List[int], k: int) -> Int:
ops = 0
vu = set()
# itération inverse – même logique que la version Java
pour v en sens inverse(nombres):
Opérations += 1
si v <= k:
Voir.add(v)
si len(see) == k:
pause
retour ops
«» "

'`cpp
// C++17
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minOpérations(vecteur <int>& nums, int k) {
Int ops = 0;
unordered_set<int> vu; // O(1) moyenne insert/lookup
pour (int i = nombres.size() - 1; i >= 0; --i) {
++ops;
si (nums[i] <= k) vu.insert(nums[i]);
Si (int)seen.size() == k) pause;
}
les opérations de retour;
}
};
«» "

Les trois extraits ont la même complexité temporelle **O(n)** (n = `nums.size()`) et complexité spatiale **O(k)** (au plus k numéros uniques sont stockés).

---

- Oui. 2. Billet de blog – Le bon, le mauvais et le mauvais de LeetCode 2869

> **Titre:** *LeetCode 2869 – Opérations minimales pour collecter des éléments: Une plongée profonde (Java, Python, C++)*
> **Mots clés:** Minimum des opérations pour collecter des éléments, LeetCode 2869, solution Java, solution Python, solution C++, interview de codage, algorithme, complexité temporelle, complexité spatiale

---

Introduction

Lorsque vous vous préparez à une entrevue d'ingénierie logicielle, les problèmes qui se sentent *trivial* mais cachent une touche subtile donnent souvent le plus grand bénéfice. **LeetCode 2869 – Opérations minimales pour collecter des éléments** est un tel problème. Au premier coup d'oeil, vous pourriez penser que vous êtes juste compter des éléments. En réalité, vous devez comprendre l'ordre *retirement* et utiliser un *set* pour suivre ce que vous avez déjà collecté.

Dans cet article, nous disséquons le problème, nous traversons trois solutions propres (Java, Python, C++) et nous discutons des compromis, des pièges et des modèles du monde réel que les intervieweurs aiment sonder.

---

### Déclaration de problème

> Vous êtes donné un tableau `nums` d'entiers positifs et un entier `k`.
> Dans une opération vous **supprimer** le dernier élément du tableau et l'ajouter à votre *collection*.
> Retourner le nombre minimum d'opérations nécessaires pour avoir recueilli chaque entier de `1` à `k` inclusivement.

*Contrôles*

"1 ≤ longueur nominale ≤ 50"
- `1 ≤ nombres[i] ≤ longueur nominale "
- `1 ≤ k ≤ longueur nums "
- Oui. Il est garanti que vous pouvez collecter tous les numéros `1...k`.

---

### L'idée droite vers l'avant

La seule façon de recueillir des éléments est de retirer le tableau de la fin.
Si nous regardons le tableau de droite à gauche, la *première fois* nous rencontrons un nombre `= k` nous l'ajoutons à notre collection.
Une fois que nous avons vu **k nombres distincts** dans la plage `[1, k]`, nous avons terminé.

Le point de vue clé :
- **Pas besoin de garder tout le tableau** après qu'il ait été scanné.
- **Un ensemble** (ou un ensemble de hachage) donne l'insertion et la recherche O(1).

D'où un simple balayage linéaire à partir du dos, en comptant les opérations et en ajoutant à un ensemble jusqu'à ce que sa taille égale `k`, résout le problème.

---

Pourquoi la solution est élégante

1. **Simplicité** – Une boucle, un ensemble, une condition de terminaison claire.
2. **Optimalité** – L'algorithme touche chaque élément au plus une fois → **O(n)** temps.
3. **Space‐efficace** – Seulement **O(k)** mémoire supplémentaire (le pire cas, l'ensemble contient tous les numéros 1...k).
4. **Language-agnostique** – La logique traduit presque mot à mot en Java, Python, C++ (comme indiqué ci-dessus).

Ces qualités font de la solution un exemple de manuel de faire une chose et le faire bien. (en milliers de dollars)

---

- Oui. Le "Bad" – où les choses peuvent aller mal

Pourquoi ça arrive Comment l'éviter
**--------------------------------------------------------------------------------
**Ignorer l'ordre** Rappelez-vous que vous devez *supprimer de la fin*. Autres
**L'utilisation d'un tableau pour l'adhésion** Utilisez un tableau hash-set ou booléen indexé par valeur. Autres
** Erreurs hors-par-un**= Opérations de décomptage (p. ex., boucle de démarrage de `i=0`). Augmentation du compteur *avant* vérification de la condition de résiliation. Autres
**Ne pas manipuler k=1**. Conserver le `si (seen.size() == k)` dans la boucle. Autres

Même si les contraintes sont minuscules (`n ≤ 50`), le code propre vous protège des bogues futurs ou des cas de test plus grands.

---

- Oui. Les choses qui peuvent rendre votre code mauvais

- **Structures de données inutiles** – par exemple, stocker l'ensemble du tableau inversé ou utiliser une liste pour les nombres vus au lieu d'un ensemble.
- **Limites codées en dur** – `int ops = 0;` sans commentaire sur la raison pour laquelle vous incrémentez d'abord.
- **Logique mixte et E/S** – Dans les paramètres d'entrevue, garder l'algorithme isolé de l'analyse d'entrée.
- **Aucun commentaire ou documentation** – Même un petit commentaire expliquant pourquoi nous rompons quand `seen.size() == k` aide à la lisibilité.

But pour *readable, auto-documenting code* – c'est ce que les intervieweurs évaluent.

---

### Cas de bord & Variations

Explication
C'est pas vrai.
Vous devrez supprimer chaque élément ; la réponse est `n`. Autres
La réponse est la position du premier `1` de la fin. Autres
La réponse est égale à `k` (il suffit de recueillir les premiers éléments `k`). Autres
Nombres dupliqués > k Ils sont ignorés – l'algorithme les saute naturellement. Autres

Si vous vouliez un problème de **generic, veuillez remplacer `v <= k` par `target.contient(v)`. Cela transforme la solution en une aide réutilisable.

---

Code – Édition Java

"Java
pour (int i = nombres.size() - 1; i >= 0; i--) {
ops++; // chaque suppression est une opération
val int = nums.get(i);
si (val <= k) { // nous ne nous soucions que de 1..k
voir.add(val); // définir des garanties unicité
}
si (seen.size() == k) pause; // tous les nombres nécessaires sont collectés
}
«» "

*Pourquoi nous incrémentons avant la vérification*:
Si le premier élément que vous pop est déjà `k`, vous devriez compter cette opération.
L'augmentation maintient d'abord le compteur précis.

---

Récapitulation de la complexité

- **Heure**: `O(n)` – un passage de droite à gauche.
- **Espace**: `O(k)` – au plus `k` numéros distincts stockés.

Ces limites linéaires sont l'endroit idéal pour les problèmes d'entrevue : rapide, minimal et clair.

---

Les pensées finales

LeetCode 2869 est un *micro-algorithme* qui teste si vous pouvez transformer une description de problème en une mise en œuvre minimale, correcte et efficace.

- **Bonne**: temps O(n), espace O(k), boucle concise.
- **Bad**: Pièges communs avec ordre, désuets et abus des structures de données.
- **Ugly**: Sur-ingénierie ou code messy qui cache l'intention.

**À emporter :**
Gardez la logique simple, utilisez la bonne structure de données (set), et commentez où vivent les invariants de l'algorithme. C'est ce que les recruteurs recherchent.

Bonne chance, et n'hésitez pas à laisser tomber vos propres solutions ou variations dans les commentaires!

---

** Lecture supplémentaire* *
- Fil de discussion LeetCode : [lien vers le problème]
- Articles sur *hash-set vs tableau pour les tests d'adhésion*
- Série d'entretiens sur LeetCode Problèmes difficiles

---

** méta description du référencement (155 caractères)* *
Code du leet 2869 – Opérations minimales de collecte d'éléments. Lire Solutions Java, Python & C++, analyse d'algorithme, cas de bord et conseils d'entretien. (en milliers de dollars)

---

Bon codage ! C'est ce qu'il a dit