---
titre: LeetCode 3498. Degré inverse d'une chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3498 – Degré inverse d'une chaîne
**Problème**
- Oui.
Inverser le degré d'une chaîne de caractères (facile) Java / Python / C++= https://leetcode.com/problems/reverse-degree-of-a-string/

> **Objectif** – Pour une chaîne inférieure donnée `s` calculer
> \[
> \text{reverse degree}= \sum_{i=1}^{ cris} \text{(reverse alphabet value of }s[i]\text{)} \times i
> \]
> où *valeur alphabet inverse* est `a → 26, b → 25, ..., z → 1`.

Ci-dessous vous trouverez:

1. Une implémentation propre et prête à la production en **Java, Python, C++**.
2. Un liner complet (pour ceux qui aiment la brièveté).
3. Une plongée profonde de style **blog** qui parle du bon, du mauvais, du laid – ainsi que des mots-clés qui vous aident à décrocher votre prochaine entrevue.

---

1. Solution O(n) directe

L'idée principale est simple : traverser la chaîne une fois, calculer la valeur de l'alphabet inverse avec `123 - ch` (depuis `123 – 'a' = 26`, `123 – 'b' = 25`, ..., `123 – 'z' = 1`), multiplier par l'indice 1-basé, et accumuler.

### Java

"Java
Java 17+
solution de classe publique {
intérêt public inverse Degré(s) {
= 0;
pour (int i = 0; i < s.longueur(); i++) {
// 123 - 'a' = 26, 123 - 'z' = 1
int inverseVal = 123 - s.charAt(i);
sum += inverseVal * (i + 1); // 1-based position
}
la somme de retour;
}
}
«» "

Python

'`python
Solution de classe:
Degree(self, s: str) -> Int:
Total = 0
pour idx, ch dans le(s) énuméré(s), 1 : # le dénombrement donne un indice basé sur 1
inverse_val = 123 - ord(ch)
total += valeur_inverse * idx
retour total
«» "

C++

'`cpp
solution de classe {
public:
int inverse Degré(s) {
= 0;
pour (int i = 0; i < s.size(); ++i) {
int inverse_val = 123 - s[i]; // s[i] est un char, implicitement converti en int
somme += valeur inverse * (i + 1);
}
la somme de retour;
}
};
«» "

Les trois solutions fonctionnent dans **O(n)** temps et **O(1)** espace supplémentaire.

---

2. Version monoligne (pour code golf / interviews)

Langue
C'est pas vrai.
Int public inverse Degré(String s){int sum=0;pour(int i=0;i<s.longueur();i++)sum+=123-s.charAt(i)*(i+1);somme de retour;}» Autres
Solution de classe de Python: def inverseDegree(self, s): somme de retour(((123-ord(c)))*(i+1) pour i,c in énumérate(s,1)» Autres
Degree(string s){int sum=0;for(int i=0;i<s.size();++i)sum+=123-s[i]*(i+1);return sum;}» Autres

> **** Un liner sacrifie la lisibilité. Utilisez-les seulement lorsque l'entrevue demande explicitement la brièveté.

---

3. Article du blog – Degré inverse d'une chaîne: le bon, le mauvais, et le mauvais

### Titre (optimisé par le référencement)

> ** Degré inverse d'une chaîne – Solutions Java, Python et C++

Description de la méta

> Master LeetCodes -Digest inverse d'une chaîne (Easy) avec des solutions Java, Python et C++ propres. Apprenez l'algorithme, les pièges et les idées prêtes à l'entrevue.

---

Introduction

Dans chaque interview, le LeetCodeS est un terrain d'essai en or pour la manipulation des chaînes et l'arithmétique simple. Problème **3498 – Inverse Degree of a String** est un exemple de manuel : *on passe sur la chaîne, la mémoire supplémentaire constante et une petite torsion sur les indices alphabétiques*.

Voici une plongée profonde qui couvre:

- L'algorithme **core** et pourquoi il est O(n).
- **Cas d'Edge** qui peut vous faire monter (chaîne vide, longueur maximale).
- **Pièges communs** dans différentes langues.
- Un rapide** pour quand vous êtes pressé.
- Comment **en parler dans une interview** – ce que l'intervieweur tient vraiment à.

> *Mots clés:* Inverser le degré d'une chaîne, LeetCode 3498, entretien de manipulation de chaîne, problème d'entrevue Java, entretien Python, entretien C++, algorithme O(n), préparation d'entrevue.

---

####=== Réaffirmation du problème

> **Input:** `s` – une chaîne de lettres anglaises minuscules (`1 ≤=1 ≤ 1000`).
> **Output:** entier représentant le degré inverse.

**Digrément inverse** = . (valeur de l'alphabet inverse de `s[i]`) × (i + 1), où `i` est basé sur 0.

*La valeur de l'alphabet inverse* est simplement `123 - ascii_value_of_char`.
- `'a` → `123-97 = 26`
- `'b` → `123-98 = 25`
- ...
- `'z` → `123-122 = 1`

---

####=2=1 Intuition et pas à pas

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
Autres Convertir chaque caractère en sa valeur de l'alphabet inverse. Autres
Autres 2. Multiplier par sa position 1-basée. La définition du problème exige une pondération de position. Autres
Autres La somme est associative, l'ordre n'a pas d'importance. Autres

Toutes les opérations sont **temps constant** par caractère, nous donnant un algorithme linéaire.

---

Détails de mise en oeuvre (spécificité linguistique)

C'est vrai. Java

- Utilisez `charAt(i)` pour récupérer un caractère.
- `123 - s.charAt(i)` donne un `int` parce que `char` est promu à `int`.
- Multiplier par `(i + 1)` pour ajuster pour l'indexation 1-basée.

Python

- «énumérer(s, 1)» donne à la fois le caractère et un indice basé sur 1.
- "ord(ch)" retourne le code ASCII.
- Gardez la boucle simple – pas de listes ou de structures de données supplémentaires.

C++

- Accédez aux caractères via `s[i]`.
- `123 - s[i]` fonctionne parce que `char` convertit en `int`.
- La variable `sum` est `int` – sûre jusqu'aux contraintes (`1000 * 26 * 1000 = 26 000 000 < 2^31`).

---

####4-

Pourquoi ça compte ? Comment manipuler ?
- C'est quoi ?
**Caractère unique**= La pondération de position commence à 1.= Fonctionne automatiquement parce que nous utilisons `i+1`. Autres
**Longueur maximale (1000)**= Débordement potentiel en utilisant 32 bits?= Somme < 26 * 1000 * 1000 = 26M – correspond à 32 bits signés. Autres
**Input non-alphabétique**=Le problème ne garantit que les lettres minuscules. Aucune validation nécessaire; mais la programmation défensive peut vérifier `s.charAt(i) >= 'a' && s.charAt(i) <= 'z''.
**Signature d'empeigne**** Non autorisée par les contraintes. Si vous voulez être défensif, retournez 0. Autres
**Grands nombres entiers dans d'autres langues. Int si vous avez besoin de supporter de très longues chaînes (contrats extérieurs). Autres

---

Erreurs courantes

Erreur Ce qui ne va pas
C'est-à-dire
En utilisant la position 0 (`i`) au lieu de `i+1`. Une erreur hors-par-un – le résultat est trop petit. Ajouter 1 à l'index. Autres
En utilisant `s.length()` dans l'état de la boucle et à nouveau dans l'état de la boucle (par exemple, `pour (int i = 0; i < s.length(); i++)`). Calculer `int n = s.longueur();` une fois.
Autres Oublier de lancer `char` à `int` avant la soustraction en C++. Une promotion implicite peut conduire à une inadéquation signée/non signée. `int reverse_val = 123 - static_cast<int>(s[i]);` Autres
Utiliser le point flottant pour la somme. Utilisez l'arithmétique entier seulement. Autres

---

#### 6-Liner Feuille de chauffage

"Java
int inverse Degré(String s){int r=0;pour(int i=0;i<s.longueur();i++)r+=123-s.charAt(i)*(i+1);retour r;}
«» "

'`python
class Solution: def reverseDegree(self, s): somme de retour((123-ord(c))*(i+1) pour i,c inénuméré(s,1))
«» "

'`cpp
int inverseDegree(string s){int r=0;for(int i=0;i<s.size();++i)r+=123-s[i]*(i+1);retour r;}
«» "

> ** Conseil professionnel :** Gardez le monoligneur dans votre boîte à outils pour les défis de codage rapide, mais dans une vraie entrevue, expliquez chaque étape.

---

### 7--Interrogatoire

Lorsqu'on lui demande de résoudre ce problème, un bon candidat devrait :

1. **Énoncer clairement le problème** – confirmer les contraintes et la cartographie de l'alphabet inverse.
2. **Expliquer l'algorithme** – un passage, temps O(n), espace O(1).
3. **Dériver la formule** – montrer comment `123 - ch` fonctionne.
4. **Parcourir un exemple** – par exemple, `"abc"` → 148.
5. **Discuss edge cases** – chaîne vide, longueur maximale, validation d'entrée.
6. **Complexité du comportement** – soulignez pourquoi il est efficace.
7. **Offre des solutions alternatives** – p.ex., précalculer un tableau de correspondance ou utiliser un dictionnaire pour la lisibilité.

> *Pourquoi cela importe:* Les intervieweurs veulent voir que vous comprenez **temps/espace compromis**, peut **translate un énoncé de problème dans un algorithme**, et peut **anticiper des pièges**.

---

- Oui. Finale Pensées : Tant mieux. Méchant

Aspect du bien
- C'est quoi ?
**L'algorithme** Peut confondre les novices avec l'alphabet inverse. Sur-ingénierie avec des cartes de hachage ou grand- O preuves pour un problème facile. Autres
**Lisibilité du code**= Effacer les noms de variables (`reverse_val`, `sum`). Le mélange des langages – une solution C++ qui retourne "long long" pendant que les autres utilisent `int`. Autres
**Manipulation d'un boîtier d'Edge** Ignorer les contraintes peut conduire à des bugs subtils. Ne pas considérer le débordement entier pour des entrées plus longues. Autres
**Parler d'interview**= Expliquer chaque étape, utiliser des exemples. Laisse tomber le code. Rush dans le codage sans raisonnement – vous fait paraître non préparé. Autres

---

Appel à l'action

Si vous vous préparez à votre prochain entretien technique, commencez par maîtriser le degré inverse d'une chaîne. Il démontre :

- C'est un moyen de traverser.
- Des arithmétiques simples.
- Connaissance des pièges d'indexation.

Ajoutez les implémentations Java, Python et C++ ci-dessus à votre feuille de triche, pratiquez le un-liner, et vous serez prêt à aser la partie Easy de LeetCode et impressionner vos intervieweurs.

---

Résumé

- **Algorithme:** O(n) temps, O(1) espace.
- **Formule:** `reverse_val = 123 - ascii(ch)`; somme += `reverse_val * (index + 1)`.
- **Cas d'Edge:** longueur maximale, char simple, validation défensive.
- **Pitfalls:** off‐by‐one, recomputation de longueur, entier vs flotteur.
- **Conseils d'entrevue :** clarté, complexité, discussion de cas de pointe.

Bon codage, et que vos degrés inverses s'additionnent toujours correctement!

---

* Fin de l'article. *

---

Références

- LeetCode Problème 3498 – *Digest inverse d'une chaîne*.
- Question d'entrevue du jour : Inverser le degré d'une chaîne – *Blogue Pramp*.
- Java Effective – pour les conversions implicites Java.
- Le Python Fluent – pour une utilisation énumérée.
- *C++ Primer* – pour les règles de promotion char-to-int.

---

> **Télécharger cet article en format PDF** ou **partager** sur LinkedIn avec les balises #LeetCode #JavaInterview #PythonInterview.

---

**Bon entretien!**

---

> **Auteur:** *Votre nom*, ingénieur logiciel et coach de préparation d'entrevue.

---

*Disclaimer:* Les solutions ci-dessus sont adaptées aux contraintes fournies par LeetCode. Ajuster les types ou la validation si vous travaillez avec des entrées plus grandes ou des spécifications différentes.

---

**Codage heureux!**