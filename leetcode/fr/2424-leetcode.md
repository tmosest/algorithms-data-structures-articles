---
titre: LeetCode 2424. Préfixe le plus long téléchargé -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Aperçu de la solution

**Problème 2424 – Préfixe le plus long envoyé**
On vous donne un flux de vidéos distinctes `n` numérotées de `1` à `n`.
* `upload(video)` – indique qu'une vidéo a été téléchargée.
* `longest()` – retourne le plus grand `i` de sorte que chaque vidéo `1 ... i` a déjà été téléchargé.

L'objectif est de concevoir une structure de données qui supporte les deux opérations en **temps O(1)** amorti et en **temps O(n)** mémoire.

> **Connaissance des clés** – Gardez une variable d'exécution `max` qui stocke la longueur de préfixe la plus longue.
> Chaque fois qu'une nouvelle vidéo est téléchargée, si elle équivaut à `max+1` nous pouvons étendre en toute sécurité le préfixe; sinon nous nous souvenons simplement que la vidéo existe.
> Après chaque téléchargement, augmenter à plusieurs reprises `max` tandis que le nombre suivant est présent.

Cette approche utilise un hash-set (ou un tableau booléen) pour se souvenir des vidéos téléchargées qui sont *derrière* le préfixe courant.

---

Code – Java, Python, & C++

Voici des implémentations propres et idiomatiques pour chaque langue. Tous fonctionnent en **O(1) amorti** par appel.

Code de la langue
C'est quoi, ça ?
[Code de Java] (#java)
[Code Python] (#python)
[Code C++](#cpp)

---

### Java
"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

***
* Leetcode 2424 – Préfixe le plus long téléchargé
*/
classe publique LUPréfixe {

// Ensemble de vidéos qui ont été téléchargées mais ne font pas encore partie du préfixe.
Finale privée Set<entier> vu;
// Longueur actuelle du préfixe le plus long.
Int max privé;

public LUPréfixe(int n) {
// Nous avons seulement besoin de stocker des vidéos téléchargées, taille ≤ n
ce.seen = nouveau HashSet<>(n);
ce.max = 0;
}

*** Télécharge une nouvelle vidéo */
téléchargement public vide(int video) {
voir.add(vidéo);
// Avance max alors que la vidéo suivante est déjà téléchargée
pendant que (voir.contient(max + 1)) {
max++;
}
}

*** Retourne la longueur du préfixe le plus long téléchargé */
public int le plus long() {
retour max;
}
}
«» "

---

Python
'`python
classe LUPréfixe:
"""
Leetcode 2424 – Préfixe le plus long téléchargé
Mise en œuvre de Python 3
"""

def __init_(self, n: int):
# Magasinez les vidéos téléchargées qui ne font pas encore partie du préfixe
Self.seen = set()
auto.max = 0

def upload(self, vidéo: int) -> Aucun:
self.see.add(vidéo)
# Grow max alors que la prochaine vidéo nécessaire est présente
pendant que self.max + 1 en soi. vu:
auto.max += 1

def le plus long(s) -> Int:
retour self.max
«» "

---

C++
'`cpp
#inclut <unordered_set>

***
* Leetcode 2424 – Préfixe le plus long téléchargé
* Mise en œuvre C++17
*/
classe LUPréfixe {
particulier:
std::unordered_set<int> vu; // Vidéos téléchargées non encore dans le préfixe
int maxPrefix; // Préfixe actuel le plus long

public:
explicite LUPrefix(int n) : maxPrefix(0) {
// Réserver de l'espace pour éviter le remblayage
voir.reserve(n * 2);
}

vide upload(int video) {
voir.insert(vidéo);
pendant que (seen.find(maxPréfixe + 1) != vu.end()) {
++maxPréfixe;
}
}

int le plus long() const {
retour maxPrefix;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et l'horrible préfixe le plus chargé

> **Référencement au titre optimisé* *
> *Le plus long préfixe téléchargé – Leetcode 2424 : des bases à la maîtrise d'entrevue*

> **Méta—Description* *
> *Découvrez la solution O(1) la plus efficace pour Leetcode 2424 (préfixe le plus long téléchargé). Apprenez les implémentations Java, Python et C++, les pièges communs et les conseils d'entretien qui vous aideront à décrocher votre job d'ingénierie logicielle de rêve. *

---

3.1 Pourquoi ce problème se complique

* **La pertinence du monde réel** – Pensez à un service de streaming qui télécharge les vidéos séquentiellement; le plus long préfixe vous indique combien de vidéos sont prêtes à être diffusées.
* **Favoris d'interview** – C'est un problème de structure propre et unique de données qui teste votre capacité à penser à l'état et à l'analyse amortie.
* **La pratique de la langue brut** – Vous pouvez le résoudre en Java, Python, C++ et bien d'autres ; le motif reste le même.

---

3.2 Le bon – Une vision d'une seule ligne

Texte
max += 1 alors que max+1 est déjà téléchargé
«» "

La seule astuce est de garder une variable `max` qui *toujours* représente le plus long préfixe contigu.
Quand une vidéo arrive, vous l'ajoutez simplement à un ensemble (ou à un tableau booléen).
Si cette vidéo est la suivante dans la séquence, vous bossez `max` et vérifiez à nouveau.

*Heure* – O(1) amorti par appel.
*Espace* – O(n) dans le pire des cas, mais souvent moins parce qu'une fois qu'une vidéo devient partie du préfixe, elle peut être supprimée.

---

3.3 Les mauvaises – erreurs courantes

Une erreur Pourquoi ça se trompe
- Oui.
**Utiliser un balayage linéaire à chaque fois** – `alors que (max+1 <= n & uploaded[max+1])` "Scans jusqu'à "n" sur chaque appel, dans le pire des cas O(n2). Utilisez un hash-set ou un tableau booléen et itérer seulement pendant que la vidéo suivante est présente. Autres
**Obligation de mettre à jour `max` après téléchargement** – `upload()` ajoute au réglage mais ne déplace jamais le pointeur. "le plus long" retourne toujours Après `upload`, exécutez la boucle de temps qui augmente `max`. Autres
Autres **Travailler trop d'États** – par exemple, tenir une liste complète d'adjacence. Autres Mémoire inutile, opérations plus lentes. Enregistrez uniquement les numéros téléchargés; le préfixe est implicite dans `max`. Autres
** Erreurs hors-par-un** – utiliser `max` au lieu de `max+1` dans l'état de la boucle. Cause des boucles infinies ou des mises à jour manquées. Testez soigneusement avec `alors que (set.contient(max + 1))`. Autres

---

3.4 Les solutions les plus complexes que vous devriez éviter

1. **Union‐Find** – Certains résolvent cela avec une union disjointe (DSU) où chaque composant représente un bloc contigu. Bien qu'il fonctionne, il introduit une comptabilité supplémentaire et un facteur constant plus lourd.
2. **Segment Trees** – Construire un arbre segment pour vérifier si toutes les vidéos de `[1, i]` sont téléchargées est surkill et a O(log n) par appel.
3. **Récursifs/retraits** – Tenter de reconstruire le préfixe sur chaque requête est à la fois lent et difficile à raisonner.

> *Ligne de bottom*: Le pointeur de hachage + `max` est la solution "golden" – propre, rapide et conviviale.

---

3.5 Conseils d'entrevue

1. **Exposer l'idée d'abord** – Parlez du pointeur `max` et pourquoi il suffit.
2. **Discuse la complexité** – Souligner *amortis* O(1) et pourquoi la boucle de temps est limitée par "n".
3. **Cas de bord des peines** – Aucune vidéo téléchargée, dernière vidéo téléchargée en premier, ordre aléatoire.
4. **Afficher le code dans la langue choisie** – Gardez-le concis, utilisez des noms significatifs (`maxPrefix`, `seen`, etc.).
5. **Parler des alternatives** – Décrivez brièvement le DSU ou l'arborescence du segment, puis expliquez pourquoi la solution plus simple gagne.

---

3.6 Réflexions finales – Déposez le travail

* Leetcode 2424 est un **micro-problème** qui démontre votre maîtrise des structures de données et des compromis temporels.
* En maîtrisant cela, vous montrez aux intervieweurs que vous pouvez choisir l'algorithme *right* plutôt que de par défaut à la force brute.
* Variantes de pratique: que faire si les téléchargements ne sont pas distincts? Et si `longest()` est appelé après chaque téléchargement ?
* Jumeler ceci avec d'autres problèmes de préfixe/suffixe (par exemple, la Subarray la plus longue avec Sum Equals K) pour présenter un motif.

> **A emporter**: Gardez votre solution élégante, commentez-la, et soyez prêt à expliquer l'intuition. C'est ce que cherchent les recruteurs, et c'est ce qui vous fait jouer ce rôle d'ingénieur logiciel.

Bon codage, et bonne chance sur votre interview! C'est ce qu'il a dit.

---