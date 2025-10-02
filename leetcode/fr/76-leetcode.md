---
Titre: LeetCode 76. Sous-chaîne de fenêtres minimum -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. LeetCode 76 – Sous-chaîne minimale de fenêtres
**Objectif** – Trouvez la plus petite sous-chaîne de `s` qui contient chaque caractère de `t` (y compris les duplicatas).
**Complexité** – La solution optimale s'exécute dans le temps **O(=2 +=2)** et dans l'espace auxiliaire **O(1)** (128-size tableau pour ASCII).

Ci-dessous vous trouverez le code entièrement commenté, prêt à la production en **Java**, **Python** et **C++** qui satisfait aux contraintes (===,=== ≤ 105).
Après le code, vous trouverez un article de blog favorable au référencement qui explique le problème, l'analyse classique du bon mal, et comment cette solution se distingue dans une entrevue d'emploi.

---

- Oui. 2. Code de solution

### 2.1 Java

"Java
***
* LeetCode 76 – sous-chaîne minimale de fenêtres
* O(=S) +=T, espace O(1) (taille ASCII 128).
*/
solution de classe publique {

chaîne publique minWindow(chaîne s, chaîne t) {
Si (s) : null (s) : null (s) : s.longueur() {
retour ";
}

// Fréquence de chaque char en t
int[] need = nouveau int[128];
pour [charc : t.toCharArray()] besoin[c]++;

Int gauche = 0, droite = 0;
int manquant = t.longueur(); // nombre de caractères encore nécessaires
int minLen = entier.MAX_VALUE;
Int minStart = 0;

char[] sArr = s.toCharArray();

pendant que (droite < sArr.longueur) {
char c = sArr[right++];
si (nécessite[c] > 0) manquant--; // nous avons trouvé un char nécessaire
besoin[c]--; // consommer

// Quand tous les chars sont satisfaits, essayez de rétrécir de la gauche
pendant qu'il manque 0) {
si (droite - gauche < minLen) { // mettre à jour la meilleure fenêtre
minLen = droite - gauche;
minStart = gauche;
}
char gauche Char = sArr[left++];
besoin[gauche Char]++; // le remettre
si (nécessité[gaucheChar] > 0) manquant++; // nous avons perdu un char nécessaire
}
}

Retour minLen == Integer.MAX_VALUE
? ""
: s.substring(minStart, minStart + minLen);
}
}
«» "

2.2 Python

'`python
"""
LeetCode 76 – Sous-chaîne minimale de fenêtres
Heure: O(len(s) + len(t)
Espace: O(1) (128 dimensions)
"""

Solution de classe:
def minWindow(self, s: str, t: str) -> str:
si non s ou non t ou len(s) < len(t):
retour ""

besoin = [0] * 128
pour ch in t:
besoin[ord(ch)] += 1

gauche = 0
manquant = len(t)
min_len = len(s) + 1
min_start = 0

s_chars = liste(s)

pour droite, ch in énumérate(s_chars, 1: # droit est exclusif
si nécessaire[ord(ch)] > 0:
manquant -= 1
besoin[ord(ch)] -= 1

alors qu'il manque == 0:
si droite - gauche < min_len:
min_len = droite - gauche
min_start = gauche
gauche_ch = s_chars[gauche]
besoin[ord(left_ch)] += 1
si nécessaire[ord(left_ch)] > 0:
manquant += 1
gauche += 1

retourner "" si min_len > len(s) sinon s[min_start:min_start + min_len]
«» "

C++

'`cpp
***
* LeetCode 76 – sous-chaîne minimale de fenêtres
* Temps O(n + m), espace O(1) (taille ASCII 128).
*/
solution de classe {
public:
chaîne minWindow(chaîne s, chaîne t) {
si (s.vide())
retour ";

le besoin int[128] = {0};
pour (char c : t) besoin[(int)c]++;

Int gauche = 0, droite = 0;
int manquant = t.size(); // caractères encore requis
Int minLen = INT_MAX;
Int minStart = 0;

pendant que (à droite < (int)s.s.size()) {
char c = s[right++];
si [besoin[(int)c] > 0) manquant...
besoin[(int)c]--; // consommer

// rétrécir pendant que tous les caractères nécessaires sont dans la fenêtre
pendant qu'il manque 0) {
si (droite - gauche < minLen) {
minLen = droite - gauche;
minStart = gauche;
}
char lc = s[left++];
besoin[(int)lc]++; // remise
Si [besoin] > 0) manquant++;
}
}

retour minLen == INT_MAX ? "" : s.substr(minStart, minLen);
}
};
«» "

> **Astuce** – Le tableau `besoin` est toujours de 128 éléments (ASCII).
> Si vous avez besoin de prendre en charge Unicode, remplacez-le par un `HashMap<Caracter, Integer>` et l'algorithme reste le même, seul l'espace constant devient *O(-)*.

---

- Oui. 3. Article de blog – sous-chaîne de fenêtre minimale (friendly SEO)

> **Titre**:
> **Sous-chaîne de fenêtre minimal – LeetCode 76. Solution de fenêtre en Java, Python et C++= O(n) Time, O(1) Space**

> **Description détaillée**:
> Apprenez le classique LeetCode 76 Minimum Window Substring problème, pourquoi l'approche de la fenêtre coulissante est la norme de l'or, et comment répondre à cette question dans une entrevue d'ingénierie logicielle. Code en Java, Python et C++ inclus.

---

3.1 Introduction (250 mots)

> Le *Minimum Window Substring* (LeetCode 76) est l'un des puzzles d'entrevue les plus courants qui teste la capacité d'un candidat à appliquer la technique **sliding-window**.
> Avec un texte `s` et un motif `t`, le but est de trouver la sous-chaîne la plus courte de `s` qui contient tous les caractères `t`, **y compris les multiplicités**.
>
> Dans un entretien d'embauche, les intervieweurs aiment ce problème parce que:
> 1. Il vous force à penser en deux pointeurs.
> 2. Il teste votre maîtrise des tables de hachage ou des tableaux de taille fixe pour le comptage des fréquences.
> 3. Il récompense une solution **O(=S +=S)** sur une recherche naïve **O(=S2)**.

> Mots-clés we=ll saupoudrer tout au long de cet article : *Fenêtre Minimum Substring*, *LeetCode 76*, *Fenêtre coulissante*, *O(n)* algorithme, *Java Python C++*, *entretien d'ingénieur logiciel*, *conseils d'entretien d'emploi*.

---

3.2 Énoncé du problème (150 mots)

> **Input**:
> `s` – une chaîne jusqu'à 105 caractères.
> `t` – une chaîne plus petite (jusqu'à 105).
> **Résultat**:
> La lexicographie d'abord (puisque seule une réponse unique est garantie) la plus courte sous-chaîne de `s` qui contient chaque caractère de `t`.
> Si une telle fenêtre n'existe pas, retournez une chaîne vide.

> Cas de bord:
> * `s` ou `t` vide → `""
> * """""

---

### 3.3 Bon – Mauvais – Mauvaise analyse (=300 mots)

Aspect du bien
- C'est quoi ?
Autres La solution **O(n+m)** utilise deux pointeurs et des tables de fréquences de grandeur constante. Essayer de construire un automate suffixe ou un arbre suffixe généralisé – trop compétent et difficile à expliquer. Autres
Autres **L'utilisation de l'espace** `HashMap` avec de nombreuses entrées si Unicode – toujours linéaire mais pas constante. Tableau de programmation dynamique de la taille `=================– espace quadratique, impossible pour 105. Autres
**Clarté**La logique des deux points est claire et facile à lire. Garder deux cartes de fréquence distinctes pour les besoins et la fenêtre rend le code verbeux. L'utilisation de la récursion ou du style fonctionnel (carte/réduction) rend l'intention difficile à suivre pour un gestionnaire d'embauche. Autres
**Portabilité**L'algorithme est identique en Java, Python, C++ – juste des changements de syntaxe. (p. ex., liste mutable de Python ou tranche). En utilisant des fonctionnalités de langage qui ne sont pas bien connues (p. ex., des flux Java pour la mutation). Autres

> ** Ligne de bottom** – Dans une entrevue, vous voulez présenter le *bon* (fenêtre coulissante, O(n), code clair) et éviter le *ugly* (sur-ingénierie, structures de données peu claires). Le *mauvais* – une solution un peu moins efficace – peut encore passer devant le juge mais peut coûter des points d'entrevue.

---

3.4 Pourquoi cette solution se trouve dans une entrevue d'embauche

1. **Time-optimal** – "O(=" +="t)" bat la force brute "O(="2)" par ordre de grandeur.
2. **Efficacité de l'espace** – Un seul tableau de fréquences 128 éléments; pas de cartes de hachage, pas de vecteurs supplémentaires.
3. **Deux points de clarté** – L'algorithme peut être expliqué en une seule phrase : *développer jusqu'à ce que nous ayons tous les caractères requis, puis contracter avidement de la gauche*.
4. **agnostique de langue** – La même logique se traduit par **Java, Python et C++**, de sorte que vous pouvez mettre en évidence la compétence dans la langue requise par votre entrevue.
5. **Scalable** – Gérez confortablement les tailles d'entrée maximales; vous pouvez démontrer l'exécution en exécutant `python3 solution.py < big_input.txt`.

---

### 3.5 Liste de contrôle prête à l'entrevue

Questions Que demander
C'est pas vrai.
Autres Comment traitez-vous les personnages en dehors d'ASCII ? Utiliser `HashMap` ou un tableau 256-size pour l'ASCII étendu; pour Unicode, utiliser un `HashMap<Caracter,Integer>` en Java/Python. Autres
Autres Pourquoi décrémentons-nous les besoins [c] après avoir consommé? Il garde une trace du nombre de fois où nous *toujours* avons besoin de ce caractère; valeurs négatives signifie que nous avons plus qu'assez de ce char dans la fenêtre. Autres
Autres Pouvez-vous prouver que la logique de rétrécissement de la fenêtre est correcte ? Lorsque `missing == 0`, le caractère le plus à gauche n'est supprimé que si son nombre est > 0; sinon il est nécessaire pour une fenêtre valide. Autres
Autres Que se passe-t-il si `t` contient des caractères répétés? Le tableau `need` commence par la multiplicité exacte, de sorte que l'algorithme nécessite automatiquement chaque répétition. Autres

---

3.6 Conclusion (100 mots)

> Le problème de sous-chaîne de fenêtre minimale est un exercice de fenêtre coulissante quintessence.
> En utilisant un tableau de fréquences **fixe** et **deux pointeurs**, nous obtenons un temps linéaire et un espace auxiliaire constant – exactement ce que cherche un gestionnaire d'embauche.
> Présenter la solution dans **Java, Python ou C++** démontre votre polyvalence à travers les piles.
> N'oubliez pas : concentrez-vous sur la clarté, expliquez l'étape de réduction et soulignez la complexité de l'O(n) – ce sont les signaux d'entrevue que vous êtes prêt pour un rôle d'ingénierie logicielle à temps plein.

---

- Oui. 4. SEO-Optimized Blog Post (Markdown)

```markdown
♪ Sous-chaîne minimale de fenêtres – LeetCode 76
## Sliding-Window Solution en Java, Python & C++ (O(n) Time, O(1) Space)

> **Description détaillée**: Maîtriser le problème de sous-chaîne minimum de fenêtres (LeetCode 76).
> Trouvez la sous-chaîne la plus courte contenant tous les caractères de motif en utilisant l'approche de la fenêtre coulissante.
> Obtenez du code en Java, Python et C++ plus des conseils prêts à l'interview.

---

Table des matières
- [Aperçu du problème] (#problème-aperçu)
- [Technique de la fenêtre coulissante] (#technique de la fenêtre coulissante)
- [Complexité temporelle expliquée] (#expliquée par complexité temporelle)
- [Mise en œuvre de Java] (#Mise en œuvre de Java)
- [Python implementation] (#python implementation)
- [Mise en œuvre C++] (#cpp-mise en œuvre)
- [Conseils d'entrevue et liste de vérification](#interview-tips-and-checklist)
- [Pourquoi cette solution se détache]
- [Conclusion] (#Conclusion)

---

## Aperçu du problème
LeetCode 76, intitulé *Minimum Window Substring*, vous demande de trouver la plus petite sous-chaîne contiguë d'une chaîne donnée `s` qui contient tous les caractères d'une autre chaîne `t`.
Ce problème teste:
- La logique de la fenêtre coulissante à deux points.
- ** Compte de fréquence** avec tables de hachage ou tableaux fixes.
- Capacité d'optimiser la complexité **temps** de O(n2) à O(n).

---

## Technique de glisse
1. **Expand** le pointeur droit jusqu'à ce que la fenêtre actuelle couvre tous les caractères requis.
2. **Contractez** le pointeur gauche avidement pour réduire la fenêtre alors qu'elle reste valide.
3. Gardez une trace de la meilleure fenêtre (la plus courte) trouvée.

L'astuce : utilisez un tableau *fréquence* de taille 128 (ASCII) ou un `HashMap` pour Unicode pour compter les caractères nécessaires.
Ceci donne un algorithme **O(=S +=T)**.

---

La complexité temporelle expliquée
- L'élargissement de la fenêtre touche chaque personnage au plus une fois → **O(=)**.
- La passation de contrats touche aussi chaque personnage au plus une fois → **O(=)**.
- Total: **O(=S +=T)**, ce qui est optimal pour une longueur d'entrée allant jusqu'à 105.

---

- Oui. Mise en œuvre Java
"Java
solution de classe publique {
chaîne publique minWindow(chaîne s, chaîne t) {
si (s.isEmpty()) t.isEmpty() s.longueur() < t.longueur())
retour ";
int[] need = nouveau int[128];
pour [charc : t.toCharArray()] besoin[c]++;
int gauche = 0, droite = 0, manquant = t.longueur();
int minLen = entier.MAX_VALUE, minStart = 0;
pendant que (droite < s.longueur())) {
char c = s.charAt(right++);
si (nécessite[c] > 0) manquant...
besoin[c]--;
pendant qu'il manque 0) {
si (droite - gauche < minLen) {
minLen = droite - gauche;
minStart = gauche;
}
char lc = s.charAt(gauche++);
besoin[lc]++;
si (nécessite[lc] > 0) manquant++;
}
}
retour minLen == Integer.MAX_VALUE ? "" : s.substring(minStart, minStart + minLen);
}
}
«» "

---

## Mise en œuvre de Python
'`python
Solution de classe:
def minWindow(self, s: str, t: str) -> str:
si non s ou non t ou len(s) < len(t):
retour ""
besoin = [0] * 128
pour ch in t:
besoin[ord(ch)] += 1
gauche, manquante, min_len, min_start = 0, len(t), len(s)+1, 0
pour droite, ch en énumération(s, 1):
si nécessaire[ord(ch)] > 0:
manquant -= 1
besoin[ord(ch)] -= 1
alors qu'il manque == 0:
si droite - gauche < min_len:
min_len = droite - gauche
min_start = gauche
gauche_ch = s[gauche]
besoin[ord(left_ch)] += 1
si nécessaire[ord(left_ch)] > 0:
manquant += 1
gauche += 1
retourner "" si min_len > len(s) sinon s[min_start:min_start+min_len]
«» "

---

C++ Mise en œuvre
'`cpp
solution de classe {
public:
chaîne minWindow(chaîne s, chaîne t) {
si (s.vide())
retour ";
le besoin int[128] = {0};
pour (char c : t) besoin[(int)c]++;
int gauche = 0, manquant = t.size(), min_len = INT_MAX, min_start = 0;
pour (int right = 0; right < s.size(); ++right) {
c = s[droite];
si [besoin[(int)c] > 0) manquant...
besoin[(int)c]--;
pendant qu'il manque 0) {
si (droite - gauche + 1 < min_len) {
min_len = droite - gauche + 1;
min_start = gauche;
}
char lc = s[left++];
besoin[(int)lc]++;
Si [besoin] > 0) manquant++;
}
}
Retour min_len == INT_MAX ? "" : s.substr(min_start, min_len);
}
};
«» "

---

## Conseils d'entrevue
- **Exposer la fenêtre coulissante**: "Expand jusqu'à ce que nous ayons tous les caractères requis, puis contrat de la gauche."
- **Présentation de l'heure O(n)**: C'est une mesure d'entrevue clé.
- **Montrer la portabilité**: Mention vous pouvez vous adapter à Java, Python ou C++.
- **Cas d'Edge**: "S" <"T", chaînes vides, non- Caractères ASCII.

---

- Oui. Pourquoi la sous-chaîne de fenêtres minimum est une classique
- Oui. Il teste la technique à deux points.
- Oui. Cela force la compréhension des tables de fréquence.
- Oui. Il récompense l'optimalité : **O(n)** vs **O(n2)**.

---

Conclusion
Mastering the Minimum Window Substring problem démontre que vous pouvez résoudre les défis réels du traitement des chaînes de manière efficace et propre.
Gardez cette solution de fenêtre coulissante dans votre boîte à outils d'entrevue et vous impressionnerez les gestionnaires d'embauche à la recherche d'un ingénieur logiciel qualifié.

---

**Tags**: #Findow minimal Sous-chaîne #LeetCode76 #SlidingWindow #O(n) #Java #Python #C++ #Engineer logiciel #Conseils d'entrevue
«» "

> Le format Markdown ci-dessus peut être copié sur n'importe quelle plate-forme de contenu (WordPress, Jekyll, Hugo) et rendra magnifiquement avec la syntaxe appropriée sur les blocs de code.

---

> **Note finale** – Utilisez cet article comme un message LinkedIn ou un article moyen; les rubriques structurées, les extraits de code et les paragraphes de mot-clé aideront votre classement de contenu pour les requêtes *Fenêtre Minimum Substring* tout en montrant vos côtelettes de codage.

---

> Fait !