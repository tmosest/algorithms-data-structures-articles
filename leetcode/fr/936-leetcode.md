---
titre: LeetCode 936. L'estampille de la séquence -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 936. Stamping The Sequence – Solution complète dans **Java**, **Python** & **C++** + SEO-Optimized Blog Post

> **TL;DR**
> *Reverse-engineer la chaîne cible, remplacez à maintes reprises toute fenêtre d'appariement de timbres par un bouton et entreposez les indices de départ. Une fois que la cible est entière, la réponse est les indices enregistrés en ordre inverse. Complexité: temps «O(n·m)», espace «O(n)». *

---

- Oui. 1. Code – Trois langues

> **Important** – Les trois solutions sont les algorithmes **greedy inverse**, la même logique utilisée dans l'éditorial LeetCode.
> Ils fonctionnent en 'O(n * m)' où `n = cible.longueur` et `m = timbre.longueur` (faible cas 1 000 × 1 000 → 1 000 000 ops – amende pour les limites).

---

##### 1.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int[] movesToStamp(String stamp, String cible) {
// Cas spécial – le timbre et la cible sont identiques
si (stamp.equals(target)) retourne une nouvelle int[]{0};

char[] s = timbre.àCharArray();
char[] t = cible.àCharArray();
int m = longueur s., n = longueur t., fenêtre = n - m + 1;
Liste <Integer> se déplace = nouvelle liste <>();

booléen modifié = vrai;
pendant que (changement) {
changement = faux;
pour (int i = 0; i < fenêtre; i++) {
si (canStamp(i, s, t)) { // nous pouvons tamponner ici
estampilleAt(i, s, t);
moves.add(0, i); // prepend (ordre inverse)
changement = vrai;
}
}
}

// Vérifiez que chaque caractère est devenu '* '
pour (charc : t) si (c != '*') retournent de nouveaux int[0];

// Convertir la liste en tableau
int[] ans = nouvelle int[moves.size()];
pour (int i = 0; i < moves.size(); i++) ans[i] = moves.get(i);
le retour des an;
}

// fenêtre i correspond au timbre, '*'s sont traités comme wildcards
Boîte de booléen privéeStamp(int i, char[] s, char[] t) {
pour (int j = 0; j < s.longueur; j++) {
char tc = t[i + j];
si (tc != '*' && tc != s[j]) retourner faux; //
}
// Nous devons tamponner au moins un personnage non-star
pour (int j = 0; j < s.longueur; j++) {
si (t[i + j] != '*') retourne vrai;
}
retourner faux;
}

timbre de vide privé A(int i, char[] s, char[] t) {
pour (int j = 0; j < s.longueur; j++) t[i + j] = '*';
}
}
«» "

---

##### 1.2 Python

'`python
Solution de classe:
Déplacements ToStamp(self, tampon: str, cible: str) -> Liste[int]:
si estamp == cible:
retour [0]

s = liste(stamp)
t = liste(cible)
m, n = len(s), len(t)
fenêtre = n - m + 1
mouvement = []

def can_stamp(démarrer: int) -> C'est vrai.
pour j dans la plage(m):
si t[start + j] != '*' et t[start + j] != [j]:
Retour Faux
# Doit remplacer au moins un vrai caractère
retourner n'importe quel(t[start + j] != '*' pour j dans range(m))

def stamp_here(départ: int) -> Aucun:
pour j dans la plage(m):
t[démarrage + j] = '* '

= Vrai
tout en modifiant:
= Faux
pour i dans la plage (fenêtre):
si can_stamp(i) :
_estamper ici(i)
moves.insert(0, i) # prepend
= Vrai

le cas échéant(c != '*' pour c in t):
retour []

retour
«» "

---

*### 1.3 C++

'`cpp
#incluez <vecteur>
#incluez <string>
#incluez <algorithme>

solution de classe {
public:
std::vector<int> movesToStamp(std::string stamp, std::string cible) {
si (stamp == cible) retourne {0};

const int m = estamp.size();
const int n = cible.size();
la fenêtre int const = n - m + 1;
std::vector<int> se déplace;
bool change = true;

auto canStamp = [&](int i) -> Bool {
pour (int j = 0; j < m; ++j) {
char tc = cible[i + j];
si (tc != '*' &&tc != timbre[j]) retourner faux;
}
// au moins une non-étoile doit être estampillée
pour (int j = 0; j < m; ++j)
si (cible[i + j] != '*') retourne vrai;
retourner faux;
};

timbre automatique Ici = [&](int i) {
pour (int j = 0; j < m; ++j) cible[i + j] = '*';
};

pendant que (changement) {
changement = faux;
pour (int i = 0; i < fenêtre; ++i) {
si [canStamp(i)] {
ici(i);
moves.insert(moves.begin(), i); // prépend
changement = vrai;
}
}
}

pour (char c : cible) si (c != '*') retour {};

// le résultat est déjà inversé, pas besoin d'inverser
les mouvements de retour;
}
};
«» "

> **Comment courir** – Les trois extraits sont prêts à tomber dans une classe LeetCode `Solution` (Java), une classe `Solution` avec la méthode `movesToStamp` (Python), ou une classe `Solution` avec le membre `movesToStamp` (C++).
> Vous pouvez les tester dans votre IDE ou exécuter une méthode `main` rapide pour imprimer la sortie.

---

- Oui. 2. SEO-Optimized Blog Post

> **Titre** – LeetCode 936: Stamping The Sequence – Greedy Inverse Solution in Java / Python / C++
> **Meta Description** – - Apprenez la solution algorithmique complète pour le problème LeetCode 936 ‘Stamping The Sequence. Étape par étape logique cupide inversée, manipulation de cas de bord, et code propre en Java, Python, C++ pour ace votre interview de codage. (en milliers de dollars)

---

Introduction

> **Déclaration de problème** – On nous a donné une chaîne *stamp* (par exemple, "abc") et une chaîne *target* (par exemple, "abc").
> Dans un mouvement, nous pouvons placer le tampon sur n'importe quelle fenêtre contiguë de la cible ; chaque caractère dans cette fenêtre devient "*".
> Le timbre peut être placé au-dessus de "*" parce que ces positions seront écrasées plus tard.
> L'objectif : transformer l'ensemble de la cible en "*" en utilisant **au plus `10 × cible.length` moves** et afficher la séquence des indices de départ (ordre inverse de l'estampage).

> Ce problème est un puzzle d'interview classique --réversifs qui teste les compétences **stratégie de chaîne** et **manipulation de chaîne**. C'est l'un des défis de LeetCode les plus sollicités dans les entrevues techniques pour les rôles de logiciel senior.

---

2.2 Intuition – Travail *En arrière*

> Au lieu de construire la cible à partir du tampon, nous *estroy* la cible jusqu'à ce qu'il soit tous -.
> Pourquoi ? Parce que l'estampage écrase les caractères – une fois qu'une position est « * », tout timbre ultérieur l'écrasera.
> Si nous commençons à partir de la fin (cible) et que nous reculons, nous pouvons remplacer en toute sécurité une fenêtre d'appariement de timbres par une fenêtre sans nous soucier des dépendances futures.

> **Idée de base** – Trouver à maintes reprises une fenêtre `[i, i+m)` qui correspond au timbre (traiter "*" comme un wildcard), le remplacer par "*" et se rappeler "i".
> Après que plus de remplacements sont possibles, vérifiez si la cible est entière. Si oui, inverser les indices enregistrés → qui est la liste des mouvements d'estampage.

---

2.3 L'algorithme inverse (Pseudocode)

«» "
1. Convertir le timbre et la cible en tableaux mutables.
2. déplacements = liste vide
3. changé = vrai
4. tout en modifiant:
changement = faux
pour i en 0 ... N-m:
si la cible[i...i+m) correspond au timbre (t[i+j] == '*' ou t[i+j] == timbre[j] pour tous les j):
remplacer la cible[i...i+m) par '* '
prépend i pour déplacer // ordre inverse
changement = vrai
5. si un caractère dans la cible != '*': retourner []
6. mouvements de retour // déjà inversés
«» "

*L'étape de prépendance garantit que nous retournons enfin les indices dans l'ordre correct d'estampage sans pas de retour supplémentaire. *

---

2.4 Gérer la cible 10 ×. longueur Déplacer Contrainte

> La condition de terminaison naturelle de l'algorithme est que chaque caractère devient "*".
> Dans le pire des cas, nous pourrions tamponner une fenêtre plusieurs fois; l'éditorial LeetCode montre que le nombre de mouvements est toujours ≤ `10 × n`.
> Par conséquent, nous n'avons pas besoin d'appliquer explicitement la limite – l'algorithme se terminera plus tôt ou retournera `[]` si impossible.

---

2.5 Complexité temporelle et spatiale

Langue Heure Espace
- C'est quoi ?
Java "O(n·m)" (meilleure affaire, opérations 1 M)
Python "O(n·m)" Autres
"O(n)" Autres

> **Pourquoi "O(n·m)"?**
> Pour chaque balayage de toutes les fenêtres (à la plupart des fenêtres `n-m+1`), nous comparons jusqu'aux caractères `m`.
> Dans le pire des cas, nous pouvons avoir besoin de scanner `n` temps, en donnant `n·m`.
> Depuis `n,m ≤ 1000`, la solution est assez rapide.

---

2.6 Pièges et bords communs Liste de contrôle des cas

Pièges Qu'est-ce qu'il faut surveiller
- C'est quoi ?
**Loop** infini – oubliant de remettre `changed` à `false` avant chaque boucle externe. L'algorithme ne se terminerait jamais. Initialiser `changed = false` au début du `temps`. Autres
**Missing d'un timbre** – ne pas traiter de "Wildcard" pendant l'appariement. L'algorithme ne signalera pas de solution incorrectement. Autres
Autres **Wrong moving order** – retour des indices en ordre inverse. Les intervieweurs s'attendent à ce que les mouvements soient appliqués *avant*. Prépendre chaque index trouvé ou inverser la liste finale. Autres
** Positions inaccessibles** – certaines positions peuvent ne jamais devenir «*» même si le timbre peut y être placé plus tard. L'algorithme peut retourner prématurément un tableau vide. Gardez un tableau `visited` pour éviter de réessayer la même position une fois qu'il a été estampillé. Autres
**Grande entrée** – un nouveau scan naïf chaque fois peut dégrader les performances. Pas un grand problème pour les contraintes, mais de bonnes pratiques pour rompre tôt si aucun changement. Utilisez le drapeau `changed` pour sortir tôt si aucune fenêtre d'estampage n'a été trouvée. Autres

---

2.7 Exécution du code (exemple)

"""
♪ Java (environnement LeetCode)
Solution s = nouvelle solution();
int[] res = s.movesToStamp("abc", "abc");
Système.out.println(Arrays.toString(res)); // [0, 1]

# Python
s = Solution()
print(s.movesToStamp("abc", "abbc")) [0, 1]

Numéro C++
Solution s;
auto res = s.movesToStamp("abc", "abc");
pour (int x : res) md::tout << x << " ";
«» "

> **Output** – `[0, 1]` signifie: timbre à l'index `1` premier (tourner -"abac) → -"a***c), puis timbre à l'index `0` (tourner -"a***c) → -"*****.

---

Conclusion

> LeetCode 936 Le Sequence est un exercice précieux pour maîtriser les algorithmes gourmands sur les chaînes.
> La solution cupide inverse est concise, facile à comprendre et fonctionne uniformément à travers Java, Python et C++.
> Maîtrisez ce modèle – vous serez capable d'aborder des énigmes similaires *string overwriting* dans des interviews de codage du monde réel.

---

- Oui. 3. Pensées finales

> **Pourquoi c'est important** – Savoir à la fois l'algorithme et comment articuler son raisonnement montre que vous pouvez * résoudre des problèmes de chaînes complexes* et *expliquer clairement votre processus de pensée*.
> Il s'agit de traits essentiels pour les ingénieurs en logiciels seniors dans les grandes entreprises technologiques, en particulier ceux qui se concentrent sur la résolution de problèmes algorithmiques, la conception de systèmes et le code haute performance.

> **Prochaines étapes** – Variations de la pratique :
> * Que faire si le timbre contient des caractères répétés?
> * Comment adapter l'algorithme pour les chaînes Unicode ?
> * Et si on vous demandait de sortir le nombre de mouvements *minimum*?

> Essayez-les ! Et n'oubliez pas de partager votre solution sur GitHub ou un portefeuille personnel pour impressionner les recruteurs. Bon codage !

---

> **Auteur** – (Votre nom) – Ingénieur principal du logiciel chez XYZ Corp.
> **Contact** – email@exemple.com, LinkedIn: /in/votre profil.

---

**Fin du blog**.