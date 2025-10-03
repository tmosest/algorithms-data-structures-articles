---
titre: LeetCode 1784. Vérifiez si Binary String a au plus un segment de un -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1784 – Vérifiez si Binary String a au plus un segment de Ones

**Mots clés:** LeetCode 1784, chaîne binaire, un segment de ceux, question d'entrevue, algorithme, solution O(n), Java, Python, C++, entretien de codage, ingénieur logiciel, entretien d'emploi, conseils professionnels

---

### TL;DR

- **Problème** – Déterminer si une chaîne binaire (`s`) contient *au plus un* bloc contigu de `1`s.
- ** Solution optimale** – Scanner une fois et marquer la première transition de `1` à `0`. Si un second `1` apparaît après cette transition, retourner `faux`.
- **Heure** – O(n)
- **Espace** – O(1)

> ** Conseil professionnel :** Un seul liner fonctionne (`!s.contient("01")` en Java ou `return "01" pas dans s` en Python), mais un scan manuel est la réponse d'entrevue "real" qui montre que vous comprenez les transitions d'état.

---

- Oui. 1. Énoncé de problème (de LeetCode)

> Avec une chaîne binaire `s` **sans diriger des zéros** (c'est-à-dire `s[0] == '1'`), retourner `true` si `s` contient **au plus un segment contigu de ceux**; sinon, retourner `false`.

Exemples

Valeur de sortie Raison
C'est quoi, ça ?
"1001""""false"" Deux blocs séparés de "1". Autres
Un bloc de `1`s suivi de zéros. Autres
Un seul "1". Autres
Un bloc de `1`s, puis zéros. Autres
""111000111""""false"" Deux blocs de "1" séparés par des zéros. Autres

Obstacles

- `1 <= longueur <= 100`
- Chaque caractère est soit `'0'` ou `'1'`
- `s[0] == '1'' (aucun zéro de début)

---

- Oui. 2. Les bons, les mauvais et les méchants

Qu'est-ce que c'est ? Pourquoi ça compte ? Comment améliorer ?
- C'est pas vrai.
Autres **Bonne – Simplicité** (Java) or `"01" not in s` (Python)= Rapide à écrire, facile à lire= Fonctionne pour toutes les entrées valides parce que `s` commence par `1`=
**Bad – Hypothèses cachées**
En utilisant le regex (`re.search(r'01', s)`) ou en construisant une machine à état fini.

---

- Oui. 3. Démarche détaillée du balayage linéaire

Nous traiterons la chaîne comme une séquence de **states**:

1. **Avant le premier `0`** – toujours dans le premier bloc de `1`s.
2. **Après le premier `0`** – nous avons quitté le premier bloc.
3. **Si nous voyons un autre `1` après l'état 2** – invalide (plus d'un bloc).

**Code Pseudo* *

«» "
vu Zéro = Faux
pour ch en s:
si ch == '0':
vu Zéro = Vrai
Sinon : # ch == '1'
si vuZero: # 1 après le premier zéro
Retour Faux
retour Vrai
«» "

**Pourquoi ça marche* *

- Oui. La première fois que nous avons frappé un `0`, nous avons défini `seen Zéro = Vrai.
- Tout autre `1` doit venir **après** ce `0`; si c'est le cas, nous avons un deuxième bloc, donc nous retournons `faux`.
- Si la boucle se termine, chaque `1` est apparu avant un `0` (ou il n'y avait pas `0`s), ce qui signifie qu'il n'y a qu'un seul bloc.

---

- Oui. 4. Mise en œuvre du code

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++** que vous pouvez coller dans LeetCode ou n'importe quel IDE.

#### 4.1 Java

"Java
solution de classe {
contrôle public du booléen OnesSegment(String s) {
booléen vu Zéro = faux;
pour (int i = 0; i < s.longueur(); i++) {
char ch = s.charAt(i);
si (ch == '0') {
vu Zéro = vrai;
} autres { // ch == '1 '
si (seenZero) retourne faux;
}
}
retour vrai;
}
}
«» "

> **One-liner alternative** (conserve le guide de style LeetCode)

"Java
solution de classe {
contrôle public du booléen OnesSegment(String s) {
contient("01");
}
}
«» "

4.2 Python

'`python
Solution de classe:
Contrôle OnesSegment(self, s: str) -> C'est vrai.
Voir_zero = Faux
pour ch en s:
si ch == '0':
voir_zero = Vrai
Sinon : # ch == '1'
si vu_zéro & #160;:
Retour Faux
retour Vrai
«» "

> **Pythonique monoligne**

'`python
Solution de classe:
Contrôle OnesSegment(self, s: str) -> C'est vrai.
retourner "01" non en s
«» "

### 4.3 C++

'`cpp
solution de classe {
public:
Contrôle des bools OnesSegment(chaîne s) {
Bool vu Zéro = faux;
pour (charte : s) {
si (ch == '0') vuZero = vrai;
sinon si (seenZero) retourne false; // ch == '1' après un zéro
}
retour vrai;
}
};
«» "

> **C++11 monoligne**

'`cpp
solution de classe {
public:
Contrôle des bools OnesSegment(chaîne s) {
retourner s.find("01") == chaîne::npos;
}
};
«» "

---

- Oui. 5. Analyse de la complexité

L'approche Temps Espace
- C'est quoi ?
Analyse linéaire
Un-liner `contient`/`in`. **O(n)** (recherche toute la chaîne)
(mais avec des facteurs constants plus élevés)

`n` est la longueur de `s` (= 100). Toutes les approches sont assez rapides, mais le scan linéaire est la réponse d'interview -Clean.

---

- Oui. 6. Pièges communs et comment les éviter

1. **En supposant que `s` puisse commencer par `0`.**
*Fix*: Valider l'entrée ou le document qui `s` est garanti pour commencer par `1`.
"Java
si (s.charAt(0) == '0') lance un nouvel argument illégalException();
«» "

2. **Miss‐interpréter «Segment» comme «subséquence». * *
*Fix*: Précisez que ceux-ci doivent être contigus; n'importe quel `1` après un `0` casse le segment.

3. ** Erreurs hors ligne dans les boucles. **
*Fix*: Utilisez `for (char ch : s)` en Java/C++ ou itérez directement sur la chaîne en Python.

4. ** Utilisant des opérations coûteuses dans une boucle serrée** (par exemple, `s.contient` dans une boucle).
*Fix*: Ne faites la vérification qu'une seule fois, en dehors de la boucle.

---

- Oui. 7. Points de discussion prêts à l'entrevue

- ** Expliquer l'intuition de la machine d'état**: Premier bloc → zéro → deuxième bloc. (en milliers de dollars)
- ** Solutions alternatives de Mention** : approche à un liner, à un regex ou à deux pointeurs.
- **Discuss edge cases**: caractère unique, tous, tous zéros après le premier bloc.
- **Parler de l'évolutivité**: Même si `n ≤ 100`, l'algorithme est O(n) et fonctionne pour des entrées énormes.
- **Montrer que vous pouvez écrire un code propre et lisible**: Préférez la boucle explicite sur un monoligne cryptique.

Je préfère la boucle explicite car elle communique clairement les transitions d'état, ce qui est essentiel dans un cadre d'équipe où la lisibilité du code compte plus qu'une astuce intelligente.

---

- Oui. 8. Projet d'article sur le blog optimisé pour le référencement

> **Titre:**
> _Master LeetCode 1784 : voir si Binary String a au plus un segment de Ones – La solution Interview-Ready en Java, Python et C++_

> **Meta Description:**
> Apprenez comment résoudre LeetCode 1784 dans le temps O(n). Trouvez les solutions Java, Python et C++, comprenez le bon/mauvais/mauvais, et obtenez des conseils d'interview pour impressionner les recruteurs.

> ** Limace :**
> `leetcode-1784-binary-string-one-segment-solutions "

Aperçu

1. **Introduction** – Pourquoi cette question est une base pour les structures et chaînes de données.
2. **Énoncé de problème** – Description claire avec des exemples.
3. **Le bon, mauvais, mauvais** – vérification rapide de la santé mentale.
4. **Algorithme Walk‐through** – Machine d'État, pseudo-code.
5. **Code complet** – Java, Python, C++ avec commentaires.
6. **Complexité du temps et de l'espace** – Nombres de lignes de base.
7. **Cas d'urgence et erreurs courantes** – Ce que les intervieweurs attendent.
8. **Autres approches** – unilingues, régex, etc.
9. **Interview Talk-track** – Comment expliquer votre solution.
10. **Conclusion** – Recapture et prochaines étapes (variations d'essai, optimiser davantage).

> **Mots-clés cibles**: LeetCode 1784, chaîne binaire, un segment de ceux-ci, entretien par algorithme, questions d'entretien par codage, solution Java, solution Python, solution C++, problème de chaîne O(n), préparation d'entretien, entretien d'ingénierie logicielle.

---

- Oui. 9. Comment ce blog aide votre recherche d'emploi

- **Visibilité** – Un contenu convivial sur un problème populaire de LeetCode attire les recruteurs à la recherche d'une pratique d'entrevue.
- **Depth** – Démontre votre capacité à expliquer les algorithmes, gérer les cas de bord et écrire du code propre.
- **Portfolio** – Ajoutez les extraits de code à votre site GitHub README ou à votre site web personnel; montrez votre compréhension de plusieurs langues.
- **Réseau** – Partagez l'article sur LinkedIn, Medium, ou dev.to; engagez-vous avec des commentaires pour montrer la participation active dans la communauté des développeurs.

---

## 10. Mot final

LeetCode 1784 est une victoire rapide : il teste la manipulation des chaînes, la gestion de l'état et la capacité d'écrire un code propre et efficace. En maîtrisant l'astuce d'un liner et la solution de scan linéaire, vous serez prêt à répondre à la question lors de toute entrevue de codage. Jumelez le code avec un billet de blog poli, et vous aurez une solide pièce de portefeuille prête à l'entrevue que les recruteurs peuvent trouver et admirer.

Bon codage, et bonne chance d'atterrissage ce rôle d'ingénieur logiciel! C'est ce qu'il a dit