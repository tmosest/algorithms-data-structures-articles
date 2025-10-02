---
titre: LeetCode 1087. Expansion de Brace - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1087 – Expansion de Brace
**Difficulté**: Moyenne
**Tags**: Chaîne, Récursion, Retraçage, Parsing

---

Résumé rapide du problème
Étant donné une chaîne qui contient des lettres et des groupes *choix* désignés par `{}` (par exemple `{a,b,c}`), générer **chaque mot** qui peut être produit en choisissant une lettre de chaque groupe.
Retourne les mots résultants ** triés lexicographiquement**.

**Exemples**

Entrée Sortie
C'est quoi ?
"["acef", "bcdf", "bcef"] Autres
"["abcd"]" Autres

---

- Oui. Pourquoi ce problème compte dans les entrevues

1. **Parsing de chaîne** – Le candidat doit être à l'aise de scanner une chaîne et de regrouper les caractères.
2. **Suivi / Récursion** – Générer toutes les combinaisons est un problème classique d'explosion combinatoire.
3. **Création lexicographique** – Sensibilise au tri et à la nécessité de retourner les résultats dans un ordre spécifié.
4. **Analyse du temps et de l'espace** – Les intervieweurs s'attendent à une discussion de la complexité de l'oxygène, où k est la taille de chaque groupe.

Démontrer une solution propre et lisible en *langues multiples* montre une polyvalence – parfaite pour un portefeuille de recherche d'emploi!

---

- Oui. L'idée – construire et étendre

1. **Parcourez l'entrée** dans une liste de *options* pour chaque poste.
* Une seule lettre → `[lettre]`.
* `{a,b,c}` → `['a', 'b', 'c']`.

2. **Construisez des mots avec récursivité**.
* À la profondeur *i*, choisissez un caractère dans `options[i]` et ajoutez-le au préfixe actuel.
* Lorsque la longueur du préfixe correspond au nombre de groupes, ajouter le mot rempli à la liste de réponses.

3. **Trier** la liste finale avant le retour.

La profondeur de récursion est égale au nombre de groupes 50, donc l'utilisation de la pile est insignifiante.

---

Analyse de complexité

Commentaire Explication Résultat
- C'est quoi ?
Pour chaque groupe, nous itérerons sur ses choix; mots totaux = options [i] Autres
**Space**= pile de récursion + liste de résultats.

---

Solutions de code

Ci-dessous vous trouverez *clean, commented* solutions dans **Java**, **Python** et **C++**.

> **Conseil:** Le code est intentionnellement minimaliste afin que vous puissiez le coller dans votre boîte à sable IDE ou LeetCode sans modification.

---

- Oui. 1. Java (retrait + tri)

"Java
Importation de java.util.*;

solution de classe publique {
chaîne publique[] expansion(chaîne s) {
// Analyser la chaîne dans une liste d'options
Liste<Liste<Caractère>> groupes = parse(s);

// 2.
Liste du résultat <String> = nouvelle liste de distribution<>();
backtrack(groupes, 0, nouveau StringBuilder(), résultat);

Tri lexicographiquement
Collections.sort(résultat);

retour résultat.àArray(nouvelle chaîne[0]);
}

liste privée<Liste<Caractère>> parse(String s) {
Liste<Liste<Caractéristiques>> groupes = nouvelle liste<>();
pour (int i = 0; i < s.longueur(); ) {
Liste<Caracter> opte pour une nouvelle liste d'images<>();
si (s.charAt(i) == '{') { // début d'un groupe
i++; // skip '{ '
pendant que (s.charAt(i) != '}') {
c = s.charAt(i);
si (c != ',') opte.add(c);
i++;
}
i++; // skip '} '
} autre { // lettre unique
opte.add(s.charAt(i));
i++;
}
groupes.add(opts);
}
les groupes de retour;
}

vide privé retour(Liste<Liste<Caracter>> groupes, profondeur int,
Préfixe StringBuilder, liste <String> out) {
si (profondeur) groups.size() {
out.add(préfix.toString());
retour;
}

pour (char c : groupes.get(profond)) {
l'annexe c);
backtrack(groupes, profondeur + 1, préfixe, sortie);
prefix.deleteCharAt(prefix.longueur() - 1); // backtrack
}
}
}
«» "

---

- Oui. 2. Python (DFS récursif)

'`python
de taper l'importation Liste

Solution de classe:
-> Liste[str]:
groupes = auto._parse(s)
res: Liste[str] = []
auto._dfs(groupes, 0, [], res)
retour trié(s)

def _parse(self, s: str) -> Liste[Liste[str]]:
groupes: Liste[Liste[str]] = []
i = 0
alors que i < len(s):
si s[i] == «{»
i += 1
opte pour : Liste[str] = []
alors que s[i] != '}':
Si s[i] != ',':
opte.append(s[i])
i += 1
groupe.annexe(opts)
i += 1 # sauter '} '
Sinon:
groupes.append([s[i]])
i += 1
Groupes de retour

def _dfs(self, groupes: List[List[str]]], profondeur: int,
cur: Liste[str], res: Liste[str]) -> Aucun:
si profondeur == len(groupes):
Annexe('.join(cur))
retour
pour ch en groupes[profond]:
cur.append(ch)
auto_dfs(groupes, profondeur + 1, cur, res)
cur.pop() # retour
«» "

---

- Oui. 3. C++ (DFS + STL)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<string> expansion(string s) {
vecteur<vecteur<char>> groupes = analyse(s);
vecteur <string> rés;
chaîne de caractères cur;
dfs(groupes, 0, cur, res);
tri(res.begin(), res.end());
retour rés;
}

particulier:
vector<vector<char>> parse(const string &s) {
vecteur<vecteur<char>> les groupes;
pour (size_t i = 0; i < s.size(); ) {
le vecteur<char> opte;
si (s[i] == '{') { // groupe
++i;
pendant que (s[i] != '}') {
si (s[i] != ',') optes.push_back(s[i]);
++i;
}
++i; // skip '} '
} autres { // monochar
opts.push_back(s[i]);
++i;
}
groups.push_back(opts);
}
les groupes de retour;
}

vide dfs(vecteur Const<vecteur<char>> &groupes, profondeur int,
chaîne &cur, vecteur<chaîne> &res) {
si (profondeur) groups.size() {
res.push_back(cur);
retour;
}
pour (charc : groupes[profond]) {
cur.push_back(c);
dfs(groupes, profondeur + 1, cur, res);
cur.pop_back(); // retour
}
}
};
«» "

---

## Article du blog – L'expansion de Brace: le bon, le mauvais, et le mauvais

Titre
**Extension de Brace (LeetCode 1087): Le Bon, le Mauvais et le Méchant – Maîtriser un problème d'entrevue classique* *

### Méta-Description (pour référencement)
Apprendre à résoudre le LeetCode 1087 – Extension de Brace – en Java, Python et C++. Plongez dans l'algorithme, la complexité et les conseils d'entrevue du monde réel. Boostez votre CV d'entrevue de codage maintenant! (en milliers de dollars)

Aperçu

Section des points clés Autres
C'est pas vrai.
**Intro**= Pourquoi l'expansion d'un appareil montre vos compétences en analyse + récursion. Autres
**Découvrement des problèmes** Autres
Autres **Bien – Ce qui le rend facile**. Autres
**Bad – Pièges communs**. Autres
Autres **Ugly – Variantes plus rigides** Exclusivités imbriquées, tailles de groupe variables, ensemble de sortie énorme. Autres
Une approche en deux phases : parse → DFS.
**Discussion sur la complexité** Autres
**Language-Specific Code**. Autres
**Conseils d'entrevue**= Comment expliquer votre solution, discuter de cas de bord, de compromis temps/espace. Autres
Pourquoi maîtriser ce problème renforce votre confiance dans l'entrevue. Autres

---

### Le bon – Pourquoi Brace Expansion est un exercice d'entrevue agréable

- **Pas de Braces Nichés** – Garde l'analyse linéaire ('O(n)'), pas de récursion pour l'analyse.
- **Alphabet fixe** – Seules les lettres minuscules, donc pas de surprises Unicode.
- **Small String Length (γ 50)** – Garantie que la profondeur de récursion reste minuscule.
- **Production déterministe** – Après tri, vous savez toujours exactement quoi retourner.

Ces contraintes vous permettent de vous concentrer sur deux compétences de base : la numérisation de chaînes de caractères et le rétrotraçage.

---

### Les mauvais – Où les intervieweurs vous poussent

Qu'est-ce que regarder ?
- C'est quoi ?
Autres **Manipulation de comma** , Oubliez de sauter les virgules à l'intérieur des appareils , Utilisez `si (c != ',') ' pour construire des options ,
**Off‐by‐One**
**Désormais**= Retourner une liste non triée="Collections.sort(result)` en Java, `sorted(res)` en Python, `sort(res.begin(), res.end()` en C++="
**Empty String**= Comportement inattendu lorsque s est vide (non autorisé mais bonne pratique)== Gestion gracieusement, retour `[]` ou `[""]` selon les spécifications

Ce sont des bogues courants qui font échouer votre solution dans les tests système.

---

- Oui. L'horrible – Extensions qui vous tuent

- **Braces nestées** – Nécessite un analyseur à base de pile.
- **Grande sortie** – Le produit des tailles de groupe peut exploser (par exemple « {a,b,c,d,e,f,g} » répété 10 fois).
- **Caractères de cartes marines** – Si vous deviez traiter `*` ou `?` comme des options, vous auriez besoin d'une correspondance plus complexe.

Comprendre ces variations vous aide à expliquer l'échelle de votre solution et quels changements seraient nécessaires.

---

- Oui. L'algorithme – Parse + DFS

1. **Parsing**
* Scannez la chaîne une fois.
* Construisez un vecteur/une liste de listes : chaque liste contient les caractères possibles pour cette position.

2. **Deuxième et première recherche**
* Construisez récursivement un préfixe.
* En profondeur *i*, itérer au-dessus des "options[i]", ajouter, revenir à *i + 1*.
* Lorsque la longueur du préfixe est égale au nombre de groupes, poussez-le vers la liste de réponses.

3. **Traitement et retour**
* Après la fin de l'enquête, trier la liste des réponses et la convertir à la structure de données requise.

Pourquoi ? Parce que le jeu de sortie est exactement le produit cartésien de toutes les listes d'options, et DFS explore naturellement chaque combinaison dans `O(="k)`.

---

La complexité – Pourquoi ça compte

- **Time**: Chaque mot prend `O(L)` pour construire où `L` est le nombre de groupes, mais vous générez tous les mots. D'où le temps "O"[i]]".
- **Space**: La pile de récursion est `O(L)`, mais la liste de réponses stocke tous les mots → `O(="options[i]=")` mémoire.

Vous pouvez expliquer que pour les contraintes typiques de l'entrevue, c'est très bien, mais si le nombre de groupes ou la taille du groupe augmente, vous avez frappé un coup exponentiel.

---

### Mise en oeuvre spécifique de la langue (extraits de code)

Inclure les trois solutions ci-dessus, chacune annotée pour mettre en évidence les sections d'analyse et de retour. Encouragez les lecteurs à essayer de les réécrire dans d'autres langues (Go, Rust, etc.) – un excellent exercice pour votre portfolio.

---

### Stratégie de l'entrevue – Comment faire face à l'explication

1. ** Expliquez les deux phases** – d'abord j'analyse les options, puis I DFS pour construire toutes les combinaisons. (en milliers de dollars)
2. **Afficher l'arbre de récursion** – Dessiner un petit exemple sur le tableau blanc.
3. **Address Edge Cases** – Afficher ce qui se passe quand il n'y a qu'un seul groupe, ou quand la sortie est grande.
4. **Talk About Triing** – Mettez en évidence pourquoi la sortie triée est nécessaire.
5. **Parler de complexité** – Mentionner le produit des tailles; comparer au pire des cas.
6. ** Discussion sur l'optimisation** – Si l'intervieweur demande, expliquez que vous pourriez générer des mots *à la volée* et les diffuser si la mémoire était une contrainte.

En suivant cette feuille de route, vous répondrez à chaque question qu'un recruteur pourrait vous poser.

---

### Takeaway – Pourquoi ajouter l'extension Brace à votre CV

- ** Démontre la compétence parsing** – Analyse systématique de l'entrée.
- **Shows Recursive Backtracking Mastery** – Une base de nombreuses entrevues de codage.
- **La polyvalence des langues** – Résolue proprement en Java, Python et C++.
- **Défense de complexité claire** – Vous pouvez discuter avec confiance des compromis temps/espace.

Ajoutez le code à votre profil GitHub, écrivez un message de blog rapide, ou même créez un parcours YouTube. Plus vous pouvez articuler *pourquoi* votre solution fonctionne, plus vous aurez l'impression d'embaucher des gestionnaires.

---

Mot final

Brace Expansion est la solution parfaite pour les problèmes de microscopie qui vous permet de briller dans une entrevue de codage. Résolvez-le une fois, et vous serez prêt pour les variantes plus difficiles, mieux à expliquer la récursion, et le changement confortable entre Java, Python, et C++.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---

> ** Prêt à déposer ça dans votre portfolio? **
> Copier l'un des extraits de langue ci-dessus, ajouter un court README qui explique l'algorithme, et le transférer à une repo publique GitHub. Les chercheurs le trouvent via la méta-description du référencement – vous obtiendrez les clics dont vous avez besoin!