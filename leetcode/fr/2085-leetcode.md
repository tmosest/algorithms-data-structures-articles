---
titre: LeetCode 2085. Comptez les mots communs avec une seule apparition -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Compter les mots communs avec une seule occasion – LeetCode 2085
**Facile******Heure O(n + m)****Espace O(n + m)**

> **Mots clés:** LeetCode 2085, Compter les mots communs avec une occurrence, carte de hash, solution Java, solution Python, solution C++, préparation d'entrevue, interview de codage, pensée algorithmique

---

TL;DR
Nous devons compter le nombre de chaînes distinctes qui apparaissent **exactement une fois** dans les tableaux d'entrée *deux*.
La solution la plus propre est un seul `HashMap` (ou `unordered_map` / `dict`) qui stocke les fréquences du premier tableau, puis met à jour compte en scannant le deuxième tableau.
La complexité est linéaire dans la taille totale des deux tableaux et l'utilisation de la mémoire est proportionnelle au nombre de mots uniques.

---

Récapitulation du problème

Texte
Entrée: words1 = ["leetcode", "is", "amazing", "as", "is"]
words2 = ["amazing", "leetcode", "est"]
Produit: 2
«» "

Seuls les "codes de transport" et les "messages" satisfont à la condition.

---

- Oui. Pourquoi un HashMap est le bon outil

1. ** Compte de fréquence** – Nous devons savoir combien de fois chaque mot se produit dans chaque tableau.
2. **O(1) recherche et mise à jour** – `HashMap` nous permet d'ajouter et d'ajuster les comptes en temps constant.
3. ** Solution compacte** – Pas besoin de deux cartes séparées; nous pouvons plier la logique en un seul passage après le premier passage de fréquence.

---

## La solution "Good" – Un HashMap

1. **Première passe** – Compter les fréquences de chaque mot en mots1.
2. **Deuxième laissez-passer** – Pour chaque mot en «mots2»:
* S'il existait dans la première carte et son nombre était `1`, définissez-le `0` (candidat valide).
* S'il existait mais que son nombre était > 1, définissez-le `-1` (invalide).
3. **Comptabilité finale** – Compter le nombre d'entrées ayant une valeur `0`.

Pourquoi se mettre à l'aide `-1`? Il garantit que tout mot qui apparaît plusieurs fois dans le tableau *ni l'un ni l'autre* n'est jamais compté.

### Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
public int countWords(String[] words1, String[] words2) {
Carte<String, entier> freq = nouveau HashMap<>();

// Compter les mots en mots1
pour (Pièce w : mots1) {
freq.put(w, freq.getOrDefault(w, 0) + 1);
}

// La mise à jour compte basé sur les mots2
pour (Pièce w : mots2) {
si (freq.contientKey(w)) {
int cur = freq.get(w);
si (cur == 1) { // apparaît une fois en mots1
freq.put(w, 0); // candidat
} sinon si (cur > 0) { // apparaît plus d'une fois en mots1
freq.put(w, -1); // invalider
}
// cur < 0 signifie déjà invalide, ne rien faire
}
}

// Compter les entrées valides (valeur) 0)
Int ans = 0;
pour (int val : freq.values()) {
si (val) 0) ans++;
}
le retour des an;
}
}
«» "

Python

'`python
Importations provenant des collections Compteur

Solution de classe:
def countWords(self, mots1: list[str], mots2: list[str]) -> Int:
freq = compteur()
pour w en mots1:
freq[w] += 1

pour w en mots2:
si w en freq:
si freq[w] == 1 :
freq[w] = 0 # candidat
elif freq[w] > 0:
freq[w] = -1 # invalide

retour sum(1 pour v dans freq.values() si v == 0)
«» "

C++

'`cpp
#inclut <non-ordonné_map>
#incluez <vecteur>
#incluez <string>

solution de classe {
public:
int countWords(std::vector<std::string>& words1,
std::vector<std::string>& words2) {
std::unordered_map<std::string, int> freq;
pour (const auto& w : words1) freq[w]++; // count words1

pour (const auto& w : mots2) {
auto it = freq.find(w);
si (it != freq.end()) {
Si (il->seconde) 1 )
it->seconde = 0; // candidat
Sinon si (it->seconde > 0)
it->seconde = -1; // invalider
}
}

Int ans = 0;
pour (const auto & p : freq)
si (p.second) 0) + ans;
le retour des an;
}
};
«» "

---

## L'approche "Bad" – Deux cartes séparées

"Java
Carte <String,Integer> m1 = nouveau HashMap<>();
Carte <String,Integer> m2 = nouveau HashMap<>();
// remplir les deux cartes, puis itérer sur une et vérifier compte dans l'autre
«» "

** Retirements* *

- Mémoire supplémentaire ('O(n + m)' chacun).
- Deux boucles séparées, mais toujours linéaires.
- Un peu plus de code pour être synchronisé.

---

## L'approche "Ugly" – Force brute

"Java
nombre int = 0;
pour (String w1 : mots1) {
si (Arrays.stream(words2).filter(w2 -> w2.equals(w1)).count() == 1
&& Arrays.stream(words1).filter(w -> w.equals(w1)).count() == 1 )
count++;
}
«» "

** Problèmes* *

- Temps O(n m), bien trop lent pour 1000 éléments.
- scanne à plusieurs reprises les tableaux; très difficile à lire et à entretenir.
- Prononcer aux bugs subtils (comptage double, erreurs hors-par-un).

---

## Cas de bord et essais

Cas Mot(s) Mot(s)
- C'est quoi ?
Tableau vide non autorisé par les contraintes
Autres Tous les mots mêmes, > 1 occurrence
Autres Tous les mots sont distincts, une occurrence est "["a", "b"] "["b", "c"] "1
Autres Grandes tables aléatoires (1000 éléments) (1000 éléments)

Testez toujours l'intersection, l'unicité et les limites.

---

## Conseils d'entrevue

1. ** Expliquez l'idée d'abord** – Compte de fréquence de citation, cartes de hachage.
2. **Va à travers l'algorithme** – Afficher les deux passes et pourquoi `-1` fonctionne.
3. **Complexité** – temps O(n + m), espace O(n + m).
4. **Cas de bord de Mention** – p.ex. mots apparaissant plusieurs fois dans chaque tableau.
5. ** Optimisation facultative** – Utilisez une carte unique si vous voulez être fantaisiste, mais gardez le code lisible.

---

## Référencement optimisé à emporter

Si vous vous préparez à coder des interviews et voulez décrocher un emploi, maîtrisez **LeetCode 2085: Comptez les mots communs avec une seule apparition** est une grande vitrine de:

- **Compétence de la carte deash**
- ** Solutions O(n + m) efficaces* *
- **Réflexion claire**

Ajoutez ce problème à votre portfolio et mentionnez l'astuce **one-hashmap** dans votre CV ou votre profil LinkedIn. Les recruteurs aiment des solutions concises et élégantes qui résolvent le problème en temps linéaire.

Bon codage, et bonne chance pour votre prochaine interview!