---
titre: LeetCode 30. Sous-chaîner avec la concaténation de tous les mots -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 30. Sous-chaîner avec la concaténation de tous les mots
**Hard** – Code de leet

---

Récapitulation du problème
Étant donné une chaîne `s` et un tableau de mots `words` (toutes de la même longueur), trouver chaque index de départ d'une sous-chaîne de `s` qui est une concaténation de *chaque mot dans `words` exactement une fois, dans n'importe quel ordre.

> Exemple
> `s = "barfohefoobarman"`, `words = ["foo","bar"] "
> Réponse: `[0,9]` (`barfoo`` et ``foobar``)

---

Aperçu de la solution

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
Autres 1.- **Pré-processus** – construire une carte de hachage "cibleCount" qui stocke combien de fois chaque mot doit apparaître. Requis pour une recherche rapide et pour détecter la surutilisation. Autres
Autres 2) **Fenêtre coulissante** – déplacer une fenêtre de taille `len(word) * k` à travers `s`. La fenêtre est avancée **par longueur de mot** donc nous n'étudions jamais les mêmes caractères deux fois. Garanties *O(n)* durée où *n = longueur*. Autres
Autres 3.- **Maintenir un compteur de course** – une carte de hachage `currentCount` qui suit combien de fois chaque mot apparaît dans la fenêtre actuelle. Conservez une variable `utilisée` qui compte des mots distincts qui sont **non surutilisés**. Autres
Autres Si un mot non dans `targetCount` apparaît, réinitialisez la fenêtre en commençant juste après ce mot. Il rejette rapidement les sous-chaînes impossibles. Autres
Autres Lorsque la taille de la fenêtre est égale à « substringSize » ou que nous avons un mot surutilisé, glissez le bord gauche vers l'avant mot par mot, dépréciez les nombres et « used » au besoin. Autres

Cet algorithme fonctionne dans **O(n)** temps et utilise **O(k)** espace supplémentaire (pour les cartes de hachage), satisfaisant les contraintes de problème.

---

Mise en œuvre du code

Vous trouverez ci-dessous des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

Autres Toutes les solutions supposent que les mots sont non vides et que chaque mot a la même longueur.
> Ils se protègent aussi contre le cas de bord quand le `s` est trop court pour contenir une concaténation complète.

---

### 2.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<entier> trouverSubstring(String s, String[] mots) {
Liste du résultat <entier> = nouvelle liste de distribution<>();
if (s) == null="words" == null="words.longueur == 0) le résultat du retour;

wordLen = word[0].longueur();
Int mot Nombre = longueur de mots;
int totalLen = wordLen * wordCount;
si (s.longueur() < totalLen) résultat de retour;

// 1. Construire une carte de fréquence cible
Carte<String, entier> cible = nouvelle HashMap<>();
pour (Pièce w : mots) {
cible.put(w, cible.getOrDefault(w, 0) + 1);
}

// 2. Itérer sur tous les décalages possibles (0 ... wordLen-1)
pour (int offset = 0; offset < wordLen; offset++) {
int gauche = décalage, droite = décalage;
Carte<String, entier> fenêtre = nouvelle HashMap<>();
int utilisé = 0; // nombre de mots qui ne sont pas surutilisés
excès booléen = faux; // vrai si la fenêtre a un mot surutilisé

pendant que (droite + motLen <= s.longueur()) {
// Prenez le mot suivant
String word = s.substring(droite, droite + wordLen);
droite += mot Len;

si (!target.contientKey(word)) { // 3a. mauvais mot -> réinitialiser
window.clear();
utilisé = 0;
Excédent = faux;
gauche = droite;
poursuivre;
}

// 3b. ajouter le mot à la fenêtre
window.put(mot, window.get) OuDéfaut(mot, 0) + 1);
si (window.get(word) <= cible.get(word)) {
utilisé++;
} autre {
Excédent = vrai; // surutilisé
}

// 4. Réduire la fenêtre si elle est trop grande ou contient un excès
pendant que (droite - gauche)
Chaîne gaucheWord = s.substring(gauche, gauche + wordLen);
gauche += mot Len;
int cnt = window.get(leftWord) - 1;
window.put(leftWord, cnt);

si (cnt >= cible.get(leftWord)) {
// supprimé une instance excédentaire
Excédent = faux;
} autre {
utilisé...
}
}

// 5. Nous avons trouvé une fenêtre valide
si (utilisée)
résultat.add(à gauche);
}
}
}
le résultat du retour;
}
}
«» "

---

2.2 Python 3

'`python
Importations provenant des collections Compteur, débit par défaut
de taper l'importation Liste

Solution de classe:
def findSubstring(self, s: str, mots: List[str]) -> Liste[int]:
si les mots ne sont pas s:
retour []

word_len, word_count = len(words[0]), len(words)
total_len = word_len * word_count
si len(s) < total_len:
retour []

cible = Contre(mots)
res = []

pour offset dans range(word_len):
gauche = décalage
droite = décalage
window = defaultdict(int)
utilisé = 0
excès = Faux

alors que droite + word_len <= len(s):
mot = s[right:right+word_len]
droite += mot_len

si mot n'est pas dans la cible:
# Réinitialisez le mauvais mot
window.clear()
utilisé = 0
excès = Faux
gauche = droite
poursuivre

# ajouter mot
fenêtre[mot] += 1
si window[word] <= cible[word]:
utilisé += 1
Sinon:
Excédent = Vrai

# rétrécir si nécessaire
alors que droite - gauche == total_len ou excédent:
Mots de gauche = s[left:left+word_len]
gauche += mot_len
fenêtre[mot_de_gauche] -= 1

si window[left_word] >= cible[mot_left]:
excès = Faux
Sinon:
utilisé -= 1

si utilisé == word_count et non excédentaire:
res.append(gauche)

retour res
«» "

---

#### 2.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findSubstring(string s, vector<string> mots) {
vecteur<int> rés;
si (s.vide()) mots.vide() retourne rés;

wordLen = words[0].size();
Int mot Nombre = mots.size();
int totalLen = wordLen * wordCount;
si (s.size() < totalLen) retour rés;

// carte des fréquences cibles
non ordonné_map<string, int> cible;
pour (cost string & w : mots)
++cible[w];

pour (int offset = 0; offset < wordLen; ++ offset) {
int gauche = décalage, droite = décalage;
unordered_map<string, int> fenêtre;
Int utilisé = 0;
excès de bool = faux;

pendant que (droite + motLen <= (int)s.size()) {
string word = s.substr(right, wordLen);
droite += mot Len;

si (!target.count(word)) { // mauvais mot – réinitialiser
window.clear();
utilisé = 0;
Excédent = faux;
gauche = droite;
poursuivre;
}

// ajouter à la fenêtre
++fenêtre[mot];
si (fenêtre[mot] <= cible[mot])
++utilisé;
Autre
Excédent = vrai;

// rétrécir si la fenêtre est trop grande ou trop grande
pendant que (droite - gauche)
chaîne lWord = s.substr(gauche, motLen);
gauche += mot Len;
--fenêtre[lWord];

si (fenêtre[lWord] >= cible[lWord])
Excédent = faux;
Autre
--utilisés;
}

si (utilisée)
res.push_back(gauche);
}
}
retour rés;
}
};
«» "

---

- Oui. Les bons, les mauvais, les méchants

L'aspect L'aspect
C'est pas vrai.
Temps linéaire, petite mémoire
**Scalabilité**=Poignées de 105 chaînes de longueur facilement
**Readability**
Autres **Edge‐Case Safety**
**Caractéristiques du langage idiomatique**
**Pièges potentiels**
**Débogage de l'aide**

- Oui. Que garder dans une entrevue d'emploi

* **Afficher le *pourquoi*** – Ne laissez pas tomber le code. Marchez dans la logique de la fenêtre coulissante et pourquoi il atteint *O(n)*.
* **Parlez des cas de bord** – demandez à l'intervieweur si `mots` pourraient être vides ou des mots de longueur différente; montrez comment vous avez gardé contre elle.
* ** Expliquez votre choix de structures de données** – pourquoi une carte de hachage, pas un tableau.
* **Mention la boucle offset** – c'est l'astuce qui vous garantit de ne pas manquer toutes les positions de départ valides.

---

## 4=2 SEO–Optimized Title & Meta Description

Titre
> **Leet Code #30: Efficace Soustraction avec la concaténation de tous les mots – Java, Python & C++ Solutions**

Description de la méta
> Découvrez une solution rapide et coulissante pour Leet Code #30. Lisez le code Java, Python et C++ détaillé, passez à travers l'algorithme, et apprenez à aser ce problème dur dans votre prochaine interview technique.

---

## 5-

La partie « good » est la solution *linear* qui mélange élégamment le suivi des fréquences de hash-map avec une fenêtre coulissante avancée par la longueur des mots.
La partie "bad" est la tentation de glisser un personnage à la fois – qui exploserait à *O(n·wordLen*).
La partie "gugly" consiste à gérer les mots surutilisés à l'intérieur de la fenêtre ; c'est subtil, mais la boucle "while-rrink" la corrige proprement.

Avec ces implémentations et l'explication qui les accompagne, vous êtes prêt à passer à un entretien d'emploi et à parler avec confiance du problème 30 du Leet Code. Bon codage 