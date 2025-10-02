---
titre: LeetCode 3210. Trouvez la chaîne chiffrée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 3210 – Trouver la chaîne chiffrée
**Difficulté:** Facile **Tags:** Chaîne, Math, Deux Pointeurs

> On vous donne une chaîne `s` et un entier `k`.
> Chiffrer la chaîne en utilisant l'algorithme suivant :
> Pour chaque caractère `c` dans `s`, remplacer `c` par le caractère *k*-th **après** `c` dans la chaîne (cycliquement).
> Retourne la chaîne chiffrée.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
Chaque personnage saute 3 positions en avant. Autres
`s = "aaa"`, `k = 1`""aaa"`" Tous les caractères sont identiques, donc la chaîne reste la même. Autres

**Contrôles* *

- Oui.
-- -- -- -- -- --
1 <= longueur <= 100 '
"1 <= k <= 10^4"
"s" se compose uniquement de lettres anglaises minuscules

---

- Oui. 2. Intuition et observation

La règle de chiffrement est *exactement* un déplacement circulaire de la chaîne par des positions `k` à gauche.
Si `k` est plus grand que la longueur de la chaîne (`n`), le déplacement par `n` ramène chaque caractère à sa place originale. Par conséquent, nous n'avons qu'à changer

«» "
efficace Maj = k % n
«» "

Le problème se réduit à produire une nouvelle chaîne où le caractère à index `i` dans la chaîne d'origine se déplace vers index `(i -effectiveShift) mod n`.
Équivalentement, nous pouvons construire le résultat en choisissant le personnage qui finira à chaque nouvelle position:

«» "
pour i dans 0 .. n-1:
résultat[i] = s[(i + effectiveShift) % n]
«» "

Cela donne une solution spatiale **O(n)** et **O(n)**.

---

- Oui. 3. Mise en œuvre des références

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.

> **Note:** Les trois versions gèrent le cas `k > n` en calculant `k % n` et produisent la même sortie pour les exemples.

#### 3.1 Java

"Java
solution de classe publique {
chaîne publique getEncryptedString(String s, int k) {
int n = s.longueur();
// Réduire le passage à la quantité minimale nécessaire
k %= n;

Résultat StringBuilder = nouveau StringBuilder(n);
pour (int i = 0; i < n; i++) {
result.append(s.charAt(i + k) % n)
}
retour résultat.àString();
}
}
«» "

**Pourquoi c'est bon? **
- `StringBuilder` évite la concaténation de cordes répétées.
- `k %= n` élimine les boucles inutiles lorsque `k` est énorme.
- Boucle lisible avec indices explicites.

---

3.2 Python

'`python
Solution de classe:
def getEncryptedString(self, s: str, k: int) -> str:
n = len(s)
k %= n # changement effectif
retourner ''.join(s[(i + k) % n] pour i dans l'intervalle(n))
«» "

** Pierres de touches pyroniques**

- Compréhension de la liste + "join" rendements O(n) temps.
- Oui. Pas de constructeur de chaînes explicites; les chaînes de Python sont immuables mais `join` est efficace.

---

### 3.3 C++

'`cpp
solution de classe {
public:
chaîne getEncryptedString(chaîne s, int k) {
int n = s.size();
k %= n; // poste effectif
chaîne res(n, '\0'); // résultat préalloté
pour (int i = 0; i < n; ++i) {
res[i] = s[(i + k) % n];
}
retour rés;
}
};
«» "

**C++ faits saillants* *

- `string res(n, '\0')' préalloue la mémoire, empêchant les réaffectations répétées.
- Utilise l'indexation zéro comme les trois langues.

---

- Oui. 4. Analyse

Temps Espace
C'est le cas.
**Toutes les trois solutions Autres

- `n` est la longueur de `s` (= 100).
- Oui. L'algorithme est optimal; nous ne pouvons pas faire mieux que de lire chaque personnage une fois.

---

- Oui. 5. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Readability**= Loop avec index explicite + commentaires; tout le code s'explique. Certaines solutions naïves utilisent des boucles imbriquées ou des concaténations de cordes (`+` en Java/Python), menant au temps O(n2). Autres
**Performance** Aucun.
**Cas d'Edge**=Poignées `k == n`, `k > n` et caractères identiques gracieusement. Aucun. Autres
**Mémoire**= chaîne de résultats préalignée/`StringBuilder`.= Aucune.= Concaténation dynamique de la chaîne dans une boucle en Java/Python peut attribuer de nombreuses chaînes intermédiaires, conduisant à des ballonnements de mémoire. Autres

- Oui. Comment éviter les vilains pièges

- **Réduire toujours `k` modulo `n`** avant de procéder.
- **Éviter la concaténation des cordes en boucles** – utiliser un constructeur ou préalloter.
- **Tenir l'indice arithmétique simple**: `(i + shift) % n` est la formulation la plus naturelle pour la rotation gauche.
- **Valeurs limites de test**: `k == 1`, `k == n`, `k > n` et `s` de longueur 1.

---

- Oui. 6. SEO-Optimized Blog Post: ♫Mastering LeetCode 3210 – Trouver la chaîne chiffrée

> **Titre:**
> *LeetCode 3210 – Trouver la chaîne chiffrée: Java, Python & C++ Solutions + Conseils d'entrevue*

> **Méta—Description:**
> Solve LeetCode 3210 Trouvez la chaîne chiffrée avec le code Java, Python et C++ propre. Apprenez l'algorithme, l'analyse de l'espace temporel et les stratégies prêtes à l'entrevue.

> **Mots clés:**
> LeetCode 3210, Trouver la chaîne chiffrée, solution Java, solution Python, solution C++, cryptage de chaîne, déplacement cyclique, codage d'entrevue, analyse d'algorithme, complexité de temps, complexité de l'espace, codage interview prep

---

Introduction

Si vous êtes en train de vous préparer pour les interviews de codage, LeetCodeS *Easy* problèmes sont un excellent endroit pour polir vos fondamentaux. Un tel problème, **3210 – Trouver la chaîne chiffrée**, teste votre compréhension de la manipulation des chaînes et de l'arithmétique modulaire. Dans ce post, nous allons parcourir le problème, dériver une solution optimale, présenter un code propre dans trois langues principales, et discuter des meilleures pratiques qui vous feront briller dans une entrevue.

---

Récapitulation du problème

> Compte tenu d'une chaîne `s` et d'un entier `k`, remplacer chaque caractère par le caractère `k`-th qui vient après dans la chaîne (circulairement). Retourne la chaîne chiffrée résultante.

---

Intuition

L'opération est simplement une rotation **circulaire gauche** par des positions `k`. Parce que la rotation par la longueur de la chaîne ramène la chaîne à son état d'origine, nous n'avons besoin de tourner que par `k % n`, où `n = s.length()`. Ce point de vue réduit le problème à une traversée "O(n)".

---

- Oui. Pourquoi cette solution est-elle une entrevue? Amiable

1. **Time-Space Optimisation:** `O(n)` temps et `O(n)` espace, le meilleur possible pour un problème de chaîne.
2. ** Logique claire :** Une seule boucle avec arithmétique simple.
3. **agnostique de la langue:** L'algorithme est directement sur Java, Python et C++.

---

Code de référence

C'est vrai. Java

"Java
solution de classe publique {
chaîne publique getEncryptedString(String s, int k) {
int n = s.longueur();
k %= n;
Résultat StringBuilder = nouveau StringBuilder(n);
pour (int i = 0; i < n; i++) {
result.append(s.charAt(i + k) % n)
}
retour résultat.àString();
}
}
«» "

Python

'`python
Solution de classe:
def getEncryptedString(self, s: str, k: int) -> str:
n = len(s)
k %= n
retourner ''.join(s[(i + k) % n] pour i dans l'intervalle(n))
«» "

C++

'`cpp
solution de classe {
public:
chaîne getEncryptedString(chaîne s, int k) {
int n = s.size();
k %= n;
chaîne res(n, '\0');
pour (int i = 0; i < n; ++i) {
res[i] = s[(i + k) % n];
}
retour rés;
}
};
«» "

---

Répartition de la complexité

- **Heure:** `O(n)` – un passage sur la chaîne.
- **Espace:** `O(n)` – la chaîne de sortie.

---

Cas et pièges de bord

Pourquoi ça compte Comment faire
- C'est quoi ?
Le déplacement plus que la longueur de la chaîne augmente inutilement le temps d'exécution. Réduire `k` de `k %= n`.
- Oui. 0 '' Pas de changement; doit retourner la chaîne originale. L'algorithme s'en occupe naturellement après modulo. Autres
"s" de longueur 1" Un seul caractère; le décalage ne fait rien. 1' donne 0; la boucle produit le même caractère. Autres
Autres Tous les caractères identiques Le résultat reste inchangé. Pas besoin de manipulation spéciale. Autres

---

Bien, mal, mal – une perspective de codage

- **Good**: Utilisation d'une seule boucle avec arithmétique modulaire; mémoire de sortie préalternative.
- **Bad**: Performing string concatenation inside a loop in Java/Python, qui cause du temps quadratique.
- **Ugly**: Oublier de réduire `k` quand il est plus grand que la longueur de la chaîne, conduisant à des calculs inutiles.

---

### Conseils d'entrevue

1. **Clarifier le problème** – Demandez si `k` peut être zéro ou négatif (dans ce problème il peut't).
2. **Exposer le Trick Modulo** – Démontrer la compréhension du comportement cyclique.
3. **Discuss Complexité** – Montrez que vous pouvez raisonner sur le temps et l'espace.
4. **Afficher le code Propreté** – Gardez-le lisible, commentez si nécessaire.
5. **Edge Cases** – Exécutez-en quelques-uns mentalement, ce qui surprend souvent les intervieweurs.

---

À emporter

LeetCode 3210 est trompeur mais encapsule un motif d'entretien classique : reconnaître une rotation, réduire avec le modulo, et construire une nouvelle chaîne efficacement. Maîtriser ce modèle non seulement résout le problème, mais également vous équipe avec un outil pour beaucoup d'autres problèmes de chaîne et de tableau que vous allez rencontrer dans de vraies interviews.

Bon codage, et la meilleure chance d'atterrir ce travail de rêve!