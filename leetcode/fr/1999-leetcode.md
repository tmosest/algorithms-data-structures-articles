---
titre: LeetCode 1999. Plus petit plus grand multiple fait de deux chiffres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* 1999 Plus petit plus grand multiple fait de deux chiffres
**LeetCode Problème** – Moyen
**Références clés:** *La solution BFS Java, solution Python, solution C++, algorithme d'entretien, conseils d'entretien

---

TL;DR

* Compte tenu de "k, chiffre1, chiffre2", trouver le **le plus petit entier**
1. ** est nettement plus grand** que " k " ;
2. est un multiple de "k"**,
3. Se compose **seulement** des deux chiffres "digital1" et "digital2".
* Retour `-1` si un tel nombre n'existe pas ou dépasse "INT_MAX".

**Solution** – Breadth‐First Search (BFS) sur les nombres construits à partir des deux chiffres.
Complexité: `O(2^len)` où `len` ≤ 10 (parce que `INT_MAX` a 10 chiffres).
Mémoire: 'O(2^len)'.

---

Déclaration de problème (de LeetCode)

Texte
Avec trois entiers, k, chiffre1, et chiffre2, vous voulez trouver le plus petit entier qui est:
1. Plus grande que k,
2. Un multiple de k,
3. Comprend seulement les chiffres numéro1 et/ou numéro2.
Rendez le plus petit entier. En l'absence d'un tel nombre entier ou si le nombre entier dépasse la limite d'un nombre entier de 32 bits signé (2^31-1), retourner -1.
«» "

**Contrôles* *

- `1 ≤ k ≤ 1000`
- `0 ≤ chiffre 1, chiffre 2 ≤ 9`

---

Idée de base

L'espace de recherche est l'ensemble de tous les chiffres qui peuvent être écrits avec les deux chiffres autorisés.
Parce que nous voulons le **le plus petit** tel nombre, explorer les nombres dans *longueur croissante* et *ordre lexicographique* garantit le premier nombre valide que nous rencontrons est la réponse.

**Pourquoi BFS? **
* BFS visites nombres par longueur croissante, de sorte que le premier match est garanti d'être minimal.
* La longueur maximale que nous devons explorer est de 10 (puisque `2^31‐1' a 10 chiffres).
* Le facteur de branchement n'est que de 2 (numérique 1 ou chiffre 2), de sorte que l'espace d'état est minuscule (nœuds ''2^10 = 1024').

---

Mise en œuvre (Python, Java, C++)

Voici des implémentations propres et prêtes à la production pour chaque langue.
N'hésitez pas à copier-coller dans votre IDE ou un bac à sable LeetCode.

---

### Python 3 (BFS)

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def trouver Integer(self, k: int, digit1: int, digit2: int) -> Int:
Si le chiffre1 est le suivant: chiffre 2 et chiffre 1 == 0:
retour -1 # seulement zéros -> impossible

# Les chiffres de départ ne peuvent pas être zéro (les zéros de début sont invalides)
_chiffres de début = []
si chiffre1 != 0:
start_digets.append(digits1)
si chiffre2 != 0 et chiffre 2 != numéro1:
start_numers.append(numer2)

q = deque(start_digets)

INT_MAX = 2 ** 31 - 1

alors que q:
num = q.popleft()
si num > k et num % k == 0:
retour num

# Ajouter le chiffre suivant seulement si nous n'excédons pas INT_MAX
si num <= INT_MAX // 10:
pour d en (chiffre 1, chiffre 2):
new_num = nombre * 10 + d
si new_num <= INT_MAX:
q.append(new_num)

retour -1
«» "

---

### Java (BFS itératif)

"Java
Importer java.util. - ArrayDeque;
Importer java.util. Deque;

solution de classe {
public int find Integer(int k, int digit1, int digit2) {
// Cas de bord : les deux chiffres sont zéro
si (chiffre1==0 &&chiffre2] 0) retour -1;

Deque<integer> file d'attente = nouveau ArrayDeque<>();

// file d'attente des semences avec chiffres de départ non zéro
si (chiffre1 != 0) file d'attente.offre(numérique1);
si (digital2 != 0 & & digital2 != digital1) file d'attente.offre(digital2);

INT_MAX = (1L << 31) - 1; // 2^31 - 1

pendant que (!queue.isEmpty()) {
int cur = file d'attente.poll();

si (cur > k && cur % k) 0) cur de retour;

si (cur <= INT_MAX / 10) {
// Ajouter le chiffre1
long suivant = cur * 10L + chiffre1;
si (suivant <= INT_MAX) file d'attente.offre((int) suivante);

// Ajouter le chiffre2 (éviter le duplicata lorsque les chiffres sont égaux)
si (chiffre2 !=chiffre1) {
suivant = cur * 10L + chiffre 2;
si (suivant <= INT_MAX) file d'attente.offre((int) suivante);
}
}
}
retour -1;
}
}
«» "

---

C++ (BFS itératif)

'`cpp
#incluez <queue>
#incluez <limites>

solution de classe {
public:
int trouver Integer(int k, int digit1, int digit2) {
si (chiffre1==0 &&chiffre2] 0) retour -1;

à:queue<int> q;
si (chiffre1 != 0) q.push(numérique1);
si (chiffre2 != 0 &&chiffre2 !=chiffre1) q.push(chiffre2);

Const longue INT_MAX_LL = static_cast<long long>(INT_MAX);

pendant que (!q.vide()) {
int cur = q.front(); q.pop();

si (cur > k && cur % k) 0) cur de retour;

si (curir <= INT_MAX_LL / 10) {
long long suivant = 1LL * cur * 10 + chiffre 1;
si (suivant <= INT_MAX_LL) q.push(static_cast<int>(suivant));

si (chiffre2 !=chiffre1) {
suivant = 1LL * cur * 10 + chiffre 2;
si (suivant <= INT_MAX_LL) q.push(static_cast<int>(suivant));
}
}
}
retour -1;
}
};
«» "

---

Pourquoi ça marche – Étape par étape

1. **Démarrer avec les plus petits chiffres non zéro. **
Tout numéro valide ne peut pas commencer par `0`.
Par conséquent, nous ensemencerons la file d'attente BFS avec les deux chiffres autorisés s'ils ne sont pas zéro.

2. **Première exploration. **
*Queue* → pop → vérifier → attirer les enfants (`cur*10 + digit`).
Parce que nous popons toujours les chiffres les plus courts (les chiffres festifs) d'abord, le premier nombre qui satisfait les deux conditions est garanti être le minimum.

3. **Dépassement de la prime.**
Nous ne générons jamais de nombres supérieurs à `INT_MAX`.
Avant d'ajouter un nouveau chiffre, nous vérifions `cur <= INT_MAX / 10`.
Cela garantit que le nombre résultant correspond à un entier signé 32 bits.

4. **Sortir tôt.**
Dès que nous trouvons un nombre qui est `> k` et divisible par `k`, nous le retournons.
Pas besoin d'explorer des niveaux plus profonds.

5. **Retour -1 si les gaz d'échappement de la file d'attente. * *
Si le BFS se termine sans trouver de numéro valide, la réponse est `-1`.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
"Bâtir tous les numéros des candidats" **O(2^L)**, où `L ≤ 10` (chiffres d'INT_MAX)" **O(2^L)** pour la file d'attente et l'état visité"

Puisque `L` est au maximum 10, l'algorithme fonctionne en microsecondes, même dans le pire des cas.
Il est bien en dessous de la limite de temps de LeetCode de 1 seconde.

---

## Categories et scénarios

Pourquoi ça compte ? C'est
- Oui.
Les deux chiffres sont 0. Le seul nombre possible serait 0, ce qui n'est pas > `k`.
Nous enquêtons sur les numéros dupliqués, ce qui pourrait causer des boucles infinies.Nous vérifions `digit2 != digit1` avant d'enquêter sur le deuxième chiffre.
"En tête des zéros autorisés ?" Les chiffres comme `012` sont invalides.Les chiffres de départ ne sont jamais nuls.
Autres Le dépassement après multiplication est supérieur à 10 + d Nous utilisons `long long` (ou `long`) et nous comparons avec `INT_MAX` Autres
Autres Très grand `k` près de `INT_MAX`. Aucun nombre > `k` ne peut être construit.

---

## # # Le bien, le mal et le mal du problème

Aspect du bien
- C'est quoi ?
**Problèmes Clarté**
**Espace de recherche**
Des implémentations DFS naïves peuvent exploser.
**Tester les difficultés**=Les cas de bord sont bien définis== Nécessite une manipulation attentive de `INT_MAX`= Le cas `k = 1, nombres = {0,1}` tests que nous ne retournons jamais
**La valeur d'interview**= montre la compréhension de BFS & la théorie des nombres==Peut être perçu comme =trivial===Requiert une manipulation réfléchie des zéros et des débordements

**À emporter :**
Ce problème est un excellent jouet d'entrevue parce qu'il mélange BFS simple avec des contrôles de théorie du nombre et une manipulation prudente du débordement. Il teste la capacité d'un candidat à raisonner sur les contraintes et les cas de bord sans se noier dans des structures de données complexes.

---

Résumé du blog optimisé du SEO

- **Titre:** *LeetCode 1999 – Le plus petit multiple de deux chiffres (Java, Python, C++)*
- **Meta Description:** *Découvrez comment résoudre LeetCode 1999 avec BFS en Java, Python et C++. Découvrez les cas de bord, la complexité et les conseils d'entrevue.
- **Mots clés:** LeetCode 1999, le plus petit plus grand Multiple, BFS, solution Java, solution Python, solution C++, algorithme d'entretien, conseils d'entretien d'emploi, défi de programmation.
- **Structure:** Intro → Déclaration de problème → Contraintes → Approche BFS → Code (Python, Java, C++) → Edge Cases → Complexité → Bon/Bad/Ugly → Conclusion.

N'hésitez pas à intégrer les blocs de code et les captures d'écran des résultats LeetCode pour stimuler l'engagement et partager sur LinkedIn ou Twitter.

---

Les pensées de clôture

* La solution **BFS** est la plus propre et la plus efficace.
* Il garantit la minimalité parce que nous explorons les nombres par ordre de longueur croissante.
* La manipulation du débordement et de l'étui à doublon rend le code robuste.
* Ce problème est parfait pour la préparation d'entrevue: il est court, mais teste BFS, la manipulation de débordement, et l'attention au détail.

Bonne chance avec vos interviews de codage ! C'est ce qu'il a dit