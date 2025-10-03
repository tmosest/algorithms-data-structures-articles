---
titre: LeetCode 1239. Longueur maximale d'une chaîne concaténée avec des caractères uniques -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. LeetCode #1547 – **Longueur maximale d'une chaîne concaténée aux caractères uniques* *
> **Langues**: Java-Python-C++

Le défi classique LeetCode que beaucoup d'intervieweurs aiment lancer aux candidats. Ci-dessous vous trouverez trois solutions propres et prêtes à la production, une pour chacune des langues d'entrevue les plus courantes.
Chaque implémentation utilise l'astuce *bit‐mask DP* pour garder l'exécution rapide tout en explorant tous les subséquences possibles.

---

### 1.1 Récapitulation des problèmes (pour les commentaires de code)

Paramètre Signification Gamme
C'est pas vrai.
Liste/Vecteur de cordes
Caractères en minuscules lettres anglaises seulement
Objectif Choisissez une séquence de `arr`, concaténez les chaînes, **sans caractère répété**, et retournez la longueur maximale possible. Autres

Parce qu'une solution exponentielle ("O(2^n)") est acceptable, mais nous nous efforcerons toujours d'adopter une approche aussi rapide que possible.

---

- Oui. 2. Mise en œuvre de Java (Bit-Mask DP)

"Java
***
* Code Leet 1547 – Longueur maximale d'une chaîne concaténée aux caractères uniques
*
* @auteur Votre Nom
*/
solution de classe {
***
* Retourne la longueur maximale possible d'une chaîne concaténée avec tous les caractères uniques.
*
* @param arr Liste des chaînes d'entrée (seulement lettres minuscules, 1 à 16 chaînes)
* @retour longueur maximale
*/
Int public maxLength(Liste <String> arr) {
// dp conserve tous les masques valides que nous avons découverts jusqu'à présent.
// Chaque masque est un entier de 26 bits où bit i signifie que le caractère 'a'+i est présent.
Liste des masques < entiers > = nouvelle liste d'array<>();
masques.add(0); // commencer par un masque vide

Int maxLen = 0;

pour (String s : arr) {
// sauter des chaînes qui contiennent déjà des duplicatas en interne
masque int = stringToMask(s);
si (masque) 0) continuer; // masque==0 => duplicata intérieur s

int curSize = masques.size(); // taille de l'instantané pour éviter toute modification simultanée
pour (int i = 0; i < curSize; i++) {
int existant = masques.get(i);
si ((existant & masque)) 0) {/ aucun chevauchement
int combined = masque existant;
masques.add(combinés);
maxLen = Math.max(maxLen, Integer.bitCount(combiné));
}
}
}

// Considérez aussi la chaîne vide (longueur 0) si aucune chaîne valide n'existe
retour maxLen;
}

***
* Convertissez une chaîne en masque 26 bits.
* Si la chaîne a des lettres dupliquées, retourner 0 pour indiquer invalide.
*/
chaîne privée intToMask(String s) {
masque int = 0;
pour (char ch : s.toCharArray()) {
bit int = 1 << (ch - 'a');
si ((masque & bit) != 0) retour 0; // duplicata à l'intérieur s
masque= bit;
}
masque de retour;
}
}
«» "

> **Pourquoi cette version Java est prête pour l'entrevue:**
> * Utilise seulement des ints primitifs → O(1) espace pour le masque.
> * `Integer.bitCount()` donne le nombre de lettres uniques instantanément.
> * Pas de récursion → pas de risque d'overflow pour le pire des 16 chaînes.

---

- Oui. 3. Mise en œuvre du Python (Bit-Mask DP)

'`python
"""
LeetCode 1547: Longueur maximale d'une chaîne concaténée aux caractères uniques
Auteur : Votre nom
"""

de taper l'importation Liste


Solution de classe:
def maxLength(self, arr: List[str]) -> Int:
"""
Retourne la longueur maximale d'une chaîne concaténée avec tous les caractères uniques.
Utilise bit‐mask DP pour conserver une liste de tous les jeux de caractères valides.
"""
masques = [0] # commencer par un jeu vide
max_len = 0

pour s in arr:
masque = auto._string_to_mask(s)
si masque == 0: # chaîne contient des lettres dupliquées en interne
poursuivre

cur_len = len(masks) # instantané pour éviter toute modification simultanée
pour i dans la plage(cur_len):
existant = masques[i]
si (existant & masque) == 0:
combinaison = masque existant
masques.annexe(combinée)
max_len = max(max_len, combiné.bit_count())

_retourner maxlen

def _string_to_mask(self, s: str) -> Int:
"""
Convertissez une chaîne en masque 26 bits.
Retourner 0 si la chaîne a des caractères dupliqués.
"""
masque = 0
pour ch en s:
bit = 1 << (ord(ch) - ord('a'))
si masque & bit & #160;:
retourner 0 # duplicata dans la chaîne
masque = bit
masque de retour
«» "

> **Conseils pour les intervieweurs**
> * Utilise `bit_count()` (Python 3.10+) pour la vitesse; les anciennes versions peuvent utiliser `bin(mask).count('1')`.
> * Pas de récursion → aucun risque de frapper Python.

---

- Oui. 4. Mise en œuvre C++

'`cpp
/*
* Code Leet 1547 – Longueur maximale d'une chaîne concaténée aux caractères uniques
* Auteur : Votre nom
*/

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxLength(vector<string>& arr) {
// vecteur de masques représentant toutes les concaténations partielles valides
vector<int> masques = {0}; // commencer par un masque vide
Int maxLen = 0;

pour (const string & s : arr) {
masque int = stringToMask(s);
si (masque) 0) continuer; // sauter les chaînes avec des lettres dupliquées

int currentSize = masques.size(); // instantané
pour (int i = 0; i < courant Taille; +i) {
int existant = masques[i];
si ((existant & masque)) 0) {/ aucun chevauchement
int combined = masque existant;
masques.push_back(combiné);
maxLen = maxLen, __constructin_popcount(combiné);
}
}
}
retour maxLen;
}

particulier:
// Convertir la chaîne en bitmask; retourner 0 si la chaîne a des duplications internes
chaîne int ToMask(const string& s) const {
masque int = 0;
pour (charte : s) {
bit int = 1 << (ch - 'a');
si (masque & bit) retourne 0; // duplicata à l'intérieur s
masque= bit;
}
masque de retour;
}
};
«» "

> **Pourquoi C++ brille ici**
> * `_buildingin_popcount()` est un compilateur-intrinsique, rapide.
> * Utilise `vector<int>` uniquement – pas de fragmentation de tas, O(1) mémoire auxiliaire.

---

- Oui. 5. Article du blog – Le bon, le mauvais, et le mauvais de LeetCode #1547

Titre
**Maîtrise du LeetCode 1547: Le Bon, le Mauvais et le Méchant de la longueur maximale d'une chaîne concaténée aux caractères uniques – Une plongée profonde pour la réussite de l'entrevue**

Description de la méta
Apprenez la solution bit-mask DP la plus rapide pour LeetCode #1547, marchez à travers les avantages et les inconvénients de DFS vs DP, et obtenez des compétences de codage prêtes à travailler en Java, Python et C++. Guide d'étude parfait pour les entrevues d'ingénierie logicielle.

---

5.1 Introduction

Lorsque les recruteurs repèrent le mot clé **= Longueur maximale d'une chaîne concaténée avec des caractères uniques** dans votre portfolio, ils savent immédiatement que vous êtes à l'aise avec la manipulation de chaînes, les astuces bitwise et la programmation dynamique exponentielle.
LeetCodeS **#1547** est un problème d'accès pour de nombreux tours d'entrevue backend, et la maîtrise de cela montre que vous pouvez:

- Traduire un problème combinatoire en un algorithme propre
- Optimiser l'espace/temps en utilisant le bit-masking
- Ecrire le code de production en Java, Python et C++

Laissons tomber les aspects **good**, **bad** et **ugly** de ce problème et de ses solutions communes.

---

5.2 Aperçu du problème

> **Objectif:**
> Choisissez une sous-séquence des chaînes données, concaténez-les et assurez-vous que *non* répète les caractères.
> Retourne la longueur maximale possible d'une telle corde concaténée.

**Contrôles* *

- Oui.
-- -- -- -- -- --
"1 ≤ arr.longueur ≤ 16" assez petite pour permettre une recherche exponentielle"
Toutes les chaînes contiennent seulement des lettres anglaises minuscules (`a–z`)
Des duplicata internes dans une seule chaîne invalident cette chaîne

---

5.3 Les bonnes – Pourquoi Ce problème est une Goldmine d'apprentissage

Pourquoi il est bénéfique
-- -- -- -- -- --
**Bit-masking**= Convertit un ensemble de 26 lettres en un seul `int`. `1 << (c - 'a')' cartographie chaque caractère en un peu. Les opérations comme le chevauchement deviennent des vérifications ET/OU simples. Autres
**O(1) popcount**= Les langues comme Java (`Integer.bitCount`) ou C++ (`_buildingin_popcount`) donnent une cardinalité instantanée, aucune boucle sur la chaîne à nouveau. Autres
**Évite la récursion**Le DP s'approche de l'itéré sur les masques et les cordes dans une double boucle, éliminant le risque de débordement de la pile lorsqu'il s'agit de 16 cordes. Autres
**La séparation claire des préoccupations**="stringToMask()" isole la logique de double-vérification. Garde l'algorithme principal lisible et testable. Autres

---

## 5.4 Les mauvaises – Ce qui rend le problème difficile

Sujet Conséquence
-- -- -- -- -- --
**L'espace de sous-ensemble exponentiel**La naïveté d'essayer chaque solution de sous-ensemble est `O(2^n)` et *timeout* si vous l'implémentez avec des boucles imbriquées sur tous les sous-ensembles incorrectement. Autres
**Mémoire d'empreinte**=Le stockage de tous les masques valides peut atteindre les entrées `2^16 = 65 536` dans le pire des cas. Toujours gérable, mais de nombreux candidats ignorent cela et rédigent un DFS récursif qui souffle la pile ou duplique le travail. Autres
Une chaîne comme `"aa"` s'invalide instantanément. Si vous oubliez ce préfiltre, l'algorithme perdra du temps et produira potentiellement de mauvais résultats. Autres

Comprendre ces pièges est la moitié de la bataille. Les intervieweurs aiment vérifier si vous les repèrez avant de les coder.

---

## 5.5 Les pièges et les luttes de débogage communs

1. ** DFS récursif + État mondial* *
* Une solution typique de DFS maintient un ensemble mondial "visité". Avec 16 cordes, la profondeur de récursion est petite, mais le dessus de la pile d'appel** peut s'additionner et produire des bogues difficiles à détecter.
* Oublier de pruner sur les lettres dupliquées à l'intérieur d'une chaîne donne souvent des réponses incorrectes comme `-1` ou une longueur qui est trop grande.

2. **Bit-Mask Mauvaise utilisation**
* L'utilisation d'un int 32 bits pour 26 lettres est très bien, mais déplacer un caractère hors de portée (`'z'` → bit 25) puis AND-ding avec un masque existant à tort peut causer des bogues entiers signés en Java ou un comportement non défini en C++ si vous oubliez le type `non signé`.
* Mélanger `String.toCharArray()` avec `ord(ch)` en Python incorrectement si vous utilisez accidentellement des lettres majuscules – un tour de test subtil.

3. **Performance Overhead dans l'environnement de LeetCode* *
* LeetCode exécute chaque soumission dans un bac à sable limité. Une solution qui compile mais utilise `std::map` au lieu de `vector<int>` dans le C++ peut déclencher un verdict "Time Limit Exceeded" même si la complexité asymptotique est la même.

---

## 5.6 Le bon – Comment le DP Bit-Mask gagne

Explication
-- -- -- -- -- --
**Linear Over Subsets**= Pour chaque chaîne d'entrée, nous itérerons sur la liste *current* des masques, produisant de nouvelles combinaisons seulement lorsque les masques ne se chevauchent pas. La boucle intérieure est `O(m)` où `m` est le nombre de masques découverts, jamais `2^n`. Autres
**Vérification des dépassements de temps constants** Masque & newMask) == 0` est une seule instruction CPU. Pas d'opérations de jeu ou de scans de chaîne coûteux. Autres
**Built‐in Popcount**= `Integer.bitCount()` / `_builtin_popcount()` / `int.bit_count()` vous donne la longueur instantanément, pas de boucle de comptage supplémentaire. Autres
**Pas de récursion**= Élimine les soucis de débordement de la pile; rend la solution trivialement portable à LeetCode=s sandbox. Autres

---

## 5.7 Les mauvaises – Quand la solution simple échoue

Qu'est-ce qu'il faut regarder ?
-- -- -- -- -- --
**Temps exponentiel**= Même si `"arr" ≤ 16`, une mauvaise implémentation qui duplique le travail ("O(2^n * 2^n)") sera TLE sur le jeu de test caché. Toujours photographier la taille de la liste de masques avant de la muter. Autres
**Memory Overhead**=Le stockage de chaque masque valide peut utiliser la mémoire de ballon si vous êtes naïf. Conserver la liste en tant que «vecteur<int>» (C++), «ArrayList<integer>» (Java), ou «list[int]» (Python). Évitez `HashSet` sauf si vous avez une raison convaincante. Autres
**Dupliquer à l'intérieur d'une chaîne**= Une chaîne comme `"abcabc"` doit être ignorée. Le fait de ne pas le filtrer conduit à des masques de 0 et des bugs subtils dans la boucle DP. Autres

---

## 5.8 L'horrible – Ce que les recruteurs n'aiment pas (et comment le réparer)

1. **Récursion du temps à la débogue**
Le DFS récursif est élégant, mais l'état global caché ("visitée") rend les tests unitaires difficiles. Utilisez des fonctions pures dans la mesure du possible.

2. **Wrong Popcount Version**
Dans Python, utiliser `bin(mask.count('1')` est plus lent que `bit_count()`. Les intervieweurs testent la performance; l'utilisation de la mauvaise fonction peut causer un **Wrong Answer** verdict sur le cas de test le plus long.

3. **Créé en C++**
Le déplacement des ints négatifs n'est pas défini. Utiliser `unsigned int` ou lancer `uint32_t` avant de déplacer.

4. **Optimisant prématurément* *
L'ajout de micro-optimisations (comme `_buildingin_popcount` avec une fonction personnalisée en ligne) peut rendre le code illisible. Maintenir l'équilibre entre vitesse et clarté.

---

## 5.9 Comment transformer cela en une compétence prête à l'emploi

1. **Write Clean, Testable Code** – Aides séparées (`stringToMask`) de l'algorithme de base.
2. **Commentaire Stratégiquement** – Expliquez *pourquoi* vous faites une petite vérification, pas seulement *comment*.
3. **Cross‐Language Cohérence** – Montrez que la même logique fonctionne en Java, Python et C++. Les recruteurs aiment les candidats qui peuvent porter des algorithmes.
4. **Ajouter des tests unitaires** – Même dans LeetCode, pratiquez avec `main()` qui exécute plusieurs cas de bord.
5. **Exposer la complexité sur l'emplacement** – Pendant les interviews, parler à travers le temps "O(n·2^n)" et l'espace "O(2^n)", et pourquoi les limites garantissent une solution se terminer dans < 1 seconde.

---

## 5.10 Pensées finales

LeetCode #1547 est plus qu'un puzzle à cordes; il est un **badge d'efficacité**.
- **Good** – Bit‐mask DP vous donne un temps d'exécution rapide, une utilisation minimale de la pile et un code clair et durable.
- **Bad** – Le problème est intrinsèquement exponentiel; il n'existe aucune solution linéaire.
- **Ugly** – Beaucoup de candidats tombent dans des pièges récursifs ou oublient de gérer des duplicatas internes, conduisant à des bugs subtils.

Master the clean DP pattern in Java, Python et C++, pratiquez les pièges énumérés ci-dessus, et vous serez prêt à impressionner n'importe quel gestionnaire d'embauche qui vous demande de résoudre la longueur maximale d'une chaîne concaténée avec des caractères uniques. *

Bon codage, et bonne chance pour votre prochaine interview!