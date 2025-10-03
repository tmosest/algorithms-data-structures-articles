---
titre: LeetCode 1941. Vérifiez si tous les caractères ont le même nombre d'occurrences -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 1941
**Titre:** *Vérifier si tous les caractères ont le même nombre d'occurrences*
**Difficulté:** Facile
**Lien:** https://leetcode.com/problèmes/check-if-all-caracters-have-equal-number-of-occurrences/

> **Objectif:** Avec une chaîne `s`, retourner `true` si chaque caractère qui apparaît dans `s` se produit le même nombre de fois, sinon retourner `faux`.
> **Contreparties :**
> - `1 <= longueur <= 1000`
> - `s` ne contient que des lettres anglaises minuscules.

---

- Oui. 2. Aperçu de la solution

La façon la plus simple de résoudre cela est de compter la fréquence de chaque caractère et ensuite de vérifier que toutes les fréquences sont identiques.

Langue Approche Complexité
C'est pas vrai.
**Java**=HashMap<Caractère,Intégré>=1 passe au compte,1 passe à comparer==**Time:** O(n) **Espace:** O(1) (max. 26 lettres distinctes)
**Python** Counter` → 1 passe pour compter, `set` pour vérifier l`uniformité. **Espace:** O(1)
**C++**"array<int,26>" ou `unordered_map` → 1 passe pour compter, scanner pour comparer" **Time:** O(n) **Espace:** O(1)

> **Pourquoi O(1) espace? **
> Seulement 26 lettres minuscules existent, de sorte que même la carte dynamique finit par contenir au plus 26 entrées.

---

- Oui. 3. Mise en œuvre du code

> Pour plus de clarté, nous incluons ** commentaires** qui expliquent la logique ligne par ligne.
> Toutes les implémentations sont prêtes à être collées dans l'éditeur LeetCode.

#### 3.1 Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe {
***
* Vérifie si tous les caractères de la chaîne ont la même fréquence.
*
* @param s la chaîne d'entrée (en minuscules seulement)
* @retour vrai si toutes les fréquences sont égales, faux sinon
*/
booléen public sontOccurrenceEqual(String s) {
// Compter les fréquences à l'aide d'une carte de hachage
Carte<Caractère, entier> freq = nouvelle HashMap<>();
pour (char ch : s.toCharArray()) {
freq.put(ch, freq.getOrDefault(ch, 0) + 1);
}

// Extraire la première fréquence comme référence
cible int = -1;
pour (int count : freq.values()) {
si (cible) -1) {
cible = nombre; // première fréquence rencontrée
} sinon si (compter != cible) { // inadéquation trouvée
retourner faux;
}
}
retour true; // toutes les fréquences correspondent
}
}
«» "

3.2 Python

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def areOccurrencesEqual(self, s: str) -> C'est vrai.
"""
Retourne Vrai si chaque caractère dans 's' se produit le même nombre de fois.
"""
# Compte chaque personnage
freq = compteur(s)

# Tous les comptes doivent être identiques – un ensemble d'un seul élément
retour len(set(freq.values())) <= 1
«» "

> **Pourquoi `<= 1`?**
> Une seule chaîne de caractères unique (`"a"`) satisfait également la condition, d'où nous acceptons un ensemble de taille 1.

### 3.3 C++

'`cpp
#incluez <vecteur>
#incluez <string>

solution de classe {
public:
bool areOccurrencesEqual(std::string s) {
// 26 lettres seulement, nous pouvons donc utiliser un tableau de taille fixe
std:vector<int> freq(26, 0);

// Fréquences de comptage
pour (charte : s) {
freq[ch - 'a']++;
}

// Trouver la première fréquence non nulle à utiliser comme cible
cible int = 0;
pour (int f : freq) {
si (f > 0) { cible = f; casse; }
}

// Vérifier que toutes les fréquences non nulles correspondent à la cible
pour (int f : freq) {
si (f > 0 & & f != cible) retourner false;
}
retour vrai;
}
};
«» "

---

- Oui. 4. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
Autres **Complexité du temps**
Autres **Utilisation de l'espace**
En C++, on peut oublier de sauter les nombres zéros, ce qui provoque de faux négatifs.
**Edge Cases**= Chaîne vide (non autorisée par les contraintes) – mais le code le gère== Chaînes de longueur 1 – manipulées automatiquement== Chaînes longues avec une seule lettre – mémoire O(1)
**Tests** Exclusions simples d'unités ({"abacbc":true, "aaabb":false, "":true}) Exclusion pour convertir des caractères en indices dans C++ Exclusion Le mélange de `unordered_map` et de tableaux conduit à l'espace O(n) inutilement
**Préparé par l'interview**= Afficher la carte/l'arrachage, expliquer l'espace `O(1)', mentionner la sortie anticipée si l'inadéquation s'est produite.

---

- Oui. 5. Notes d ' exécution

Langue
- C'est quoi ?
Autres **Java**
**Python**
0-1 ms

> ** Pourquoi si vite ? * *
> La solution touche chaque caractère une fois et n'utilise que des données auxiliaires de taille constante.
> Sur le LeetCode, les implémentations pour Java et Python sont hautement optimisées ; le tableau statique C++ est le plus efficace.

---

- Oui. 6. Comment utiliser ceci pour une entrevue d'emploi

1. ** Expliquer l'intuition d'abord**
Parce que seulement 26 lettres existent, je peux simplement compter les fréquences en un seul passage.
2. **Afficher le compromis* *
* Heure: O(n)= Espace: O(1)*
3. **Cas de bord des discussions**
* Chaîne à caractères simples, toutes lettres les mêmes, fréquences mixtes. *
4. **Va à travers le code* *
* Mettre en évidence la sortie anticipée sur l'inadéquation, utilisation de `HashMap`/`Counter`/array. *
5. **Demandez si l'intervieweur veut une approche différente* *
*Par exemple, le tri du tableau de fréquences fonctionnerait aussi mais ajouterait des coûts O(k log k). *

---

- Oui. 7. Aperçu du blog SEO optimisé

Vous trouverez ci-dessous un article complet prêt à être publié sur le blogue, que vous pouvez copier dans Medium, Dev.to ou votre portfolio personnel.
Il contient les mots clés et la structure que les recruteurs aiment.

---

# LeetCode 1941: Vérification des fréquences de caractères égales – Une plongée profonde

**Mots clés:** LeetCode 1941, Vérifiez si tous les caractères ont le même nombre d'occurrences, solution Java, solution Python, solution C++, entretien de codage, entretien d'algorithme, entretien d'ingénieur logiciel, codage d'entretien d'algorithme, prép.

---

TL;DR
LeetCode 1941 vous demande de confirmer que chaque lettre d'une chaîne apparaît le même nombre de fois.
La solution la plus simple et la plus rapide compte les fréquences une fois et vérifie que tous les nombres sont identiques – temps O(n), espace O(1).
Vous trouverez ci-dessous des implémentations **Java, Python et C++** et un guide rapide pour expliquer la solution dans un entretien d'embauche.

---

- Oui. 1. Exposé des problèmes

> **Input**: une chaîne de lettres anglaises minuscules (longueur 1 – 1000).
> **Output**: `true` si chaque lettre dans `s` se produit le même nombre de fois; sinon `faux`.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
""abacbc" ""true" "a", "b", "c" apparaissent deux fois. Autres
"aaabb" "false" "a" apparaît 3 fois, "b" 2 fois. Autres

---

- Oui. 2. Pourquoi c'est facile (mais qui vaut toujours la maîtrise)

- **Seulement 26 clés distinctes** → la mémoire reste constante quelle que soit la taille de l'entrée.
- Un seul balayage linéaire suffit; aucune structure de tri ou de données avancées.
- Oui. Il teste votre capacité à penser en termes de **nombre de fréquences**, un modèle d'entrevue commun.

---

- Oui. 3. Algorithme Passage

1. **Count**: Construire une carte de fréquence (`HashMap`/`Counter`/array).
2. **Cochez une cible**: La première fréquence non nulle est la référence.
3. **Validité**: Si une autre fréquence diffère de la cible → retourner `false`.
4. **Retour** : « vrai » si toutes les fréquences correspondent.

---

- Oui. 4. Code en trois langues

*(Chaque extrait est prêt pour le LeetCode.) *

#### 4.1 Java

"Java
solution de classe {
booléen public sontOccurrenceEqual(String s) {
Carte <Character,Intégre> freq = nouveau HashMap<>();
pour (char ch : s.toCharArray()) {
freq.put(ch, freq.getOrDefault(ch, 0) + 1);
}

cible int = -1;
pour (int count : freq.values()) {
si (cible) -1) objectif = nombre;
sinon si (comptez != cible) retourner faux;
}
retour vrai;
}
}
«» "

4.2 Python

'`python
Solution de classe:
def areOccurrencesEqual(self, s: str) -> C'est vrai.
du comptoir d'importation des collections
retourner len(set(Counter(s).values()) <= 1
«» "

### 4.3 C++

'`cpp
solution de classe {
public:
bool areOccurrencesEqual(string s) {
int freq[26] = {0};
pour (char c : s) freq[c-'a']++;

cible int = 0;
pour (int f : freq) si (f) { cible = f; casse; }

pour (int f : freq) si (f & & f != cible) retourner false;
retour vrai;
}
};
«» "

---

- Oui. 5. Analyse de la complexité

Langue Heure Espace
- C'est quoi ?
**O(n)** **O(1)** (max. 26 entrées)
Python **O(n)**
* * * * * * * * *

*Tous les trois courent dans le temps linéaire; la mémoire est limitée par la taille de l'alphabet. *

---

- Oui. 6. Liste de contrôle des cas de bord

Autres Résultats attendus Pourquoi
- C'est quoi ?
"a""""""true"" Un seul caractère – la fréquence est uniforme. Autres
Les trois lettres apparaissent deux fois. Autres
""zzzz" """ "true"" caractère unique répété. Autres
""aabbccdde" """ "false"" "e" apparaît une fois tandis que d'autres apparaissent deux fois. Autres

---

- Oui. 7. Conseils d'entrevue

1. **Commencez avec l'intuition**: Comme nous n'avons que 26 lettres, un tableau de taille fixe le fera. (en milliers de dollars)
2. **Complexité de l'état**: temps O(n), espace O(1). (en milliers de dollars)
3. **Afficher le code** (copie-coller d'en haut) et le parcourir.
4. **Discuss cases bord**: chaîne vide, chaîne à lettre unique, toutes les lettres les mêmes.
5. **Demander au sujet des contraintes**: Et si l'alphabet était plus grand? → Discuter de l'adaptation à `unordered_map`.
6. **Lisibilité lumineuse**: concise mais claire.

---

- Oui. 8. Ce qui fait cette solution **Grand** (bon, mauvais, mauvais)

- **Bien**: Temps linéaire, espace constant, code minimal.
- **Bad**: Oublier le nombre zéro dans la vérification finale peut causer de faux négatifs.
- **Ugly**: Suringénierie avec tri ou regex – complexité inutile.

---

- Oui. 9. Dernier départ

LeetCode 1941 est un exemple de manuel d'un problème qui récompense une solution propre et efficace par des astuces intelligentes.
La maîtrise démontre votre capacité à :

- Utilisez des cartes ou des tableaux de hachage pour le comptage des fréquences.
- Raison de l'espace dans le pire des cas avec un alphabet fixe.
- Ecrivez un code autonome prêt à l'entrevue.

Si vous pouvez expliquer cette solution en moins d'une minute, vous êtes prêt à recevoir la prochaine entrevue de codage.

---

Tu en veux plus ?
- Suivez-moi sur LinkedIn pour l'interview.
- Consultez mon GitHub pour un portfolio complet de solutions **Java, Python, C++**.
- Prépare un entretien !

Bonne chance, et le codage heureux!

---

* Fin de l'article. *

---

N'hésitez pas à modifier le formatage ou à ajouter des anecdotes personnelles pour rendre votre post unique. Joyeux entretien !