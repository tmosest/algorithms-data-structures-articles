---
titre: LeetCode 3228. Nombre maximum d'opérations à déplacer à la fin -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

LeetCode 3228 – **Nombre maximum d'opérations pour déplacer les uns à la fin**
**Tag** – Moyens – Greedy

> *Vous voulez avoir la prochaine interview ? Maîtrisez ce problème de LeetCode, obtenez le code en Java, Python et C++, et apprenez à l'expliquer comme un pro.

---

Table des matières
1. [Déclaration du problème](#1)
2. [Intuition et bonne, la mauvaise et la mauvaise] (#2)
3. [Solution de laissez-passer unique pour le mariage](#3)
4. [Analyse de la complexité](#4)
5. [Applications de référence](#5)
- Java
- Python
- C++
6. [Dossiers et pièges courants](#6)
7. [Test et exécution d'échantillons](#7)
8. [Pourquoi cela fait une grande question d'entrevue](#8)
9. [Conclusion et OEA à emporter](#9)

---

<un nom="1"></a>
- Oui. 1. Exposé des problèmes

Avec une chaîne binaire `s`, vous pouvez effectuer l'opération suivante ** n'importe quel nombre de fois**:

1. Choisissez un indice `i` tel que `i + 1 < s.length`, `s[i] == '1'` et `s[i+1] == '0'`.
2. Déplacez ce `'1'` vers la droite jusqu'à ce qu'il atteigne la fin de la chaîne ou rencontre un autre `'1'`.

**Objectif :** Retournez le nombre maximum d'opérations que vous pouvez effectuer.

> **Exemple**
> `s = "1001101"`
> Opérations :
> 1. `i=0` → `"0011101"`
> 2. `i=4` → `"0011011"`
> 3. `i=3` → `"0010111"`
> 4. `i=2` → `"0001111"`
> **Réponse:** `4`

---

<un nom="2"></a>
- Oui. 2. Intuition – Le Bien, le Mal et le Malheur

Aspect Explication
C'est pas vrai.
**Bien** L'opération est *locale* – vous ne vous souciez qu'un `'1'` immédiatement suivi d'un `'0'`. <br>• Chaque zéro sera effacé par chaque précédent exactement une fois. <br>• Un seul scan de gauche à droite avec un compteur de vues `'1''' suffit. Autres
**Bad** Il est facile de mal interpréter l'opération: certains pensent déplacer un `'1'` consomme le `'1'` (il ne le fait pas). <br>• Des bogues hors-par-un se produisent si vous oubliez de sauter des zéros consécutifs; sinon vous doublez les opérations de compte. Autres
Une simulation naïve (mouvant une étape à la fois) serait **O(n2)** et impossible pour `n = 105`. <br>• Si vous essayez d'utiliser une pile ou une file d'attente, vous êtes sur-ingénierie; le tour avide est tout ce dont vous avez besoin. Autres

---

<un nom="3"></a>
- Oui. 3. Solution de laissez-passer unique pour l'avidité

Idée de base
- **`ones`** = nombre de caractères `'1'' vus jusqu'à présent.
- Oui. Lorsque nous avons frappé un `'0'` qui est *après* au moins un `'1'`, ce zéro peut être déplacé par **chaque** précédant `'1'`.
Ainsi, nous ajoutons "ones" à la réponse.
- Oui. Une fois que nous voyons une série de zéros, nous sautons toute la série – la contribution a déjà été comptée.

Ce choix avide est optimal car:
- Déplacer un `'1'` sur un zéro ne crée jamais de nouvelles opportunités plus tôt dans la chaîne.
- Chaque zéro peut être manipulé par chacun d'eux exactement une fois; toute stratégie qui retarde le déplacement d'un «1» ne peut pas augmenter le total des opérations.

---

<un nom="4"></a>
- Oui. 4. Analyse de la complexité

Valeur métrique
C'est pas vrai.
Temps **O(n)** – un seul passage à travers la chaîne. Autres
Espace **O(1)** – seulement quelques compteurs entiers. Autres
La longueur des " s " (= 105). Autres

---

<un nom="5"></a>
- Oui. 5. Mise en oeuvre des références

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**. Chacun suit la même logique gourmande.

### Java

"Java
solution de classe publique {
***
* Renvoie le nombre maximal d'opérations pour déplacer toutes les '1's à la fin.
*
* @param s Chaîne binaire
* @retour Nombre d'opérations
*/
int. statique publique maxOpérations(String s) {
= 0; // nombre de '1's vu jusqu'à présent
Int ops = 0; // réponse
i = 0, n = s.longueur();

pendant que (i < n) {
si [s.charAt(i)] '1') {
les++;
i++; // passer au-delà de ce '1 '
} autre { // s.charAt(i) == '0'
si (one > 0) {
ops += un; // ce zéro sera déplacé par chaque précédent «1 '
}
// sauter des zéros consécutifs pour éviter le double comptage
alors que (i < n& s.charAt(i)) == '0') {
i++;
}
}
}
les opérations de retour;
}

// Exemple d'utilisation
public statique vide principal(String[] args) {
Système.out.println(maxOpérations("1001101")); // 4
Système.out.println(maxOpérations("00111")); // 0
}
}
«» "

> **Pourquoi cette version? * *
> - Utilise une boucle `while` pour sauter les tours de zéros efficacement.
> - Poigne les cas de bord où la chaîne commence par zéros ou se termine par zéros.
> - Compile en Java 17+ et fonctionne en microsecondes.

---

Python

'`python
def max_operations(s): str) -> Int:
"""
Retourner le nombre maximum d'opérations pour déplacer toutes les '1' à la fin.

:param s: Chaîne binaire
:retour: Nombre d'opérations
"""
onces = 0 # nombre de '1's vu jusqu'à présent
ops = 0
i = 0
n = len(s)

alors que i < n:
si s[i] == «1»:
+= 1
i += 1
Sinon : # s[i] == '0'
si:
Opérations +=
# sauter les zéros consécutifs
alors que i < n et s[i] == «0»:
i += 1
retour ops

♪ Démo
si __nom__ == "__main__" :
print(max_operations("1001101")) # 4
print(max_operations("00111") # 0
«» "

> Les boucles de Python sont propres et assez rapides pour `n = 105`.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

int maxOpérations(chaîne de &s Const) {
longues longues = 0; // nombre de '1's vu
longues opérations = 0; // réponse
i = 0, n = s.size();

pendant que (i < n) {
Si (s[i]] '1') {
+ones;
++i;
} autres { // s[i] == '0'
si (ones) ops += uns;
// sauter les zéros consécutifs
alors que (i < n& s[i]) '0') ++i;
}
}
retourner static_cast<int>(ops);
}

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

<< maxOpérations("1001101") << '\n'; // 4
Cout << maxOpérations("00111") << '\n'; // 0
}
«» "

> Utilise `long' pour la sécurité (bien que la réponse corresponde à `int` pour `n ≤ 105`).
> Garantie rapide d'entrée/sortie et d'entrée unique `O(n)`.

---

<un nom="6"></a>
- Oui. 6. Cas de bord et pièges communs

Cas de bord Qu'est-ce que regarder ?
- C'est quoi ?
La chaîne commence par zéros. 0` → aucune opération comptée. Conserver les `ones` à 0; sauter les zéros normalement. Autres
Autres Zéros consécutifs après beaucoup de ceux-ci. Après avoir ajouté `ones` à `ops`, **skip tous les zéros consécutifs**. Autres
Autres Tous les zéros (`"1111"`) Loop continue de courir; les «ops» restent 0.
Autres Tous les zéros (`"0000"`) Comme ci-dessus. Autres
Autres Importante entrée (`n = 105`) Utilisez un compteur avide; pas de simulation. Autres

---

<un nom"7"></a>
- Oui. 7. Essais et essais d'échantillons

Texte
Entrée : 1001101
Produit : 4 (comme indiqué dans l ' état)

Entrée: 00111
Produit: 0 (n° 1 suivi de 0)

Entrée : 010010
Produit : 3
Explication : les zéros aux postes 1,3,4 sont chacun déplacés par les postes précédents.
«» "

Vous pouvez coller les extraits Java, Python ou C++ dans votre IDE ou compilateur en ligne (LeetCode utilise un environnement similaire) et exécuter les tests d'échantillons.

---

<un nom="8"></a>
- Oui. 8. Pourquoi c'est une grande question d'entrevue

- **Le raisonnement général** : Montrez que vous pouvez repérer un modèle simple dans des opérations apparemment complexes.
- **Temps linéaire à un passage**: Démontre l'efficacité de la première pensée.
- **Manipulation des caisses**: Vous devez penser aux cordes de tous les zéros, de tous les zéros, et des longueurs variables.
- ** Mise en oeuvre en plusieurs langues** : Beaucoup d'interviews vous demandent d'écrire du code dans une langue de votre choix ; parler couramment Java, Python et C++ montre de la polyvalence.

> *Astuce:* Quand vous expliquez, commencez par un petit exemple, montrez l'étape gourmande, puis argumentez pourquoi déplacer un `'1'` plus tôt ne peut jamais blesser, et terminez avec la preuve O(n).

---

<un nom="9"></a>
- Oui. 9. Conclusion et appellation d'origine

- **Problème:** Tirer parti d'un simple compteur cupide pour calculer le nombre maximum de mouvements "1→0".
- **Solution:** `O(n)` passe simple avec le compteur `ones`; sautez zéro parcours.
- **Codes:** Impléments Java, Python et C++ propres, prêts à la production.

**Si vous vous préparez à coder des entrevues ou des concours de codage, la maîtrise de ce problème renforcera votre boîte à outils algorithmique. **

### SEO Pointeurs pour votre billet de blog

Objectif Mot-clé Pourquoi ça compte
- Oui.
LeetCode 1001101, les opérations maximum se déplacent 1=1 pour finir La spécificité attire les lecteurs à la recherche de ce problème exact. Autres
Le contenu multi-langue de la solution Java Python C++ améliore les classements pour les recherches linguistiques spécifiques. Autres
Expliquez et optimisez l'algorithme LeetCode, les opérations de chaînes de caractères O(n) Signalent une compréhension profonde et une efficacité algorithmique. Autres
Contexte réel de l'entrevue, questions d'entrevue de codage Appels aux recruteurs et aux développeurs. Autres

Maintenant vous êtes entièrement équipé pour conquérir **LeetCode** ou toute interview qui jette ce problème à votre manière. Bon codage !

---

**Préparé par :** *[Votre nom]* – Algorithme Enthousiaste et développeur Full-Stack
**Tags:** #LeetCode #AlgorithmDesign #Greedy #Java #Python #C++ #InterviewPrep #O(n) #CodageChallenge