---
titre: LeetCode 3450. Maximum d'élèves sur un seul banc -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## C'est la maîtrise de LeetCode 3450 – C'est le plus grand nombre d'élèves sur un seul banc

> **Vous souhaitez décrocher votre job d'ingénierie logicielle de rêve? * *
> Maîtriser les problèmes classiques de LeetCode est le moyen le plus rapide de prouver votre codage des cliquets aux recruteurs.
> Ce billet passe par tous les angles du défi *Maximum Students on a Single Bench* – de la solution la plus propre aux cases de bord, pièges, et même un guide rapide pour aider votre article se classe haut sur Google et vous faire remarquer par les gestionnaires d'embauche.

---

Récapitulation des problèmes (Codeleet 3450)

> **On vous donne un tableau entier 2-D `étudiants`, où chaque `étudiants[i] = [étudiants_id, banc_id]`**
> indiquant qu'un étudiant avec `student_id` est assis sur le banc `bench_id`.
> **Retournez le nombre maximum d'élèves *uniques* assis sur un seul banc. **
> Si aucun étudiant n'est présent, retourner `0`.

> **Constraints**

- Oui.
-- -- -- -- -- --
= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = Autres

---

Solution rapide Capture instantanée

Code 4-6 lignes
-- -- -- -- -- --
**Python** OnBench(self, students):`<br>`d = defaultdict(set)`<br>`pour s, b dans students: d[b].add(s)`<br>`return max(map(len, d.values()), default=0)` Autres
**Java**= `class Solution { public int maxStudentsOnBench(int[]] students) { ... }="
**C++**=int maxÉtudiantsOnBench(vecteur<vecteur<int>&étudiants) { ...}=

> Toutes les solutions fonctionnent dans **O(n)** temps, **O(n)** espace – optimal pour les contraintes données.

---

## -Détails

Idées fondamentales

- **Etudiants de groupe par banc** → `bench_id → {unique student_id} "
- **Couverner des étudiants uniques** pour chaque banc → taille de l'ensemble
- **Retourner le maximum** parmi tous les bancs

Utiliser un *set* gère automatiquement les duplicata `student_id`s sur le même banc.

---

Cas de bord

Autres Décision Pourquoi ça compte ?
C'est le cas.
Les élèves sont vides. Pas de bancs → réponse `0`=" `max(..., par défaut=0)` dans Python, vérifier `benchToStudents.isEmpty()` dans Java/C++="
Un étudiant peut apparaître plusieurs fois
Les ID de bancs ne sont pas contigus.Les ID de bancs peuvent être n'importe quelle valeur entre 1 et 100.Utilisez une `Map` / hash‐table plutôt qu'un tableau fixe (bien que le tableau fonctionne aussi parce que les limites sont minuscules).

---

Détails de la mise en œuvre

Python 3

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maxÉtudiants OnBench(soi-même, étudiants: Liste[Liste[int]]) -> Int:
# banc_id → ensemble d'élèves uniques id
bench_to_students = defaultdict(set)

pour étudiant_id, banc_id dans les étudiants:
banc_à_étudiants[bench_id].add(student_id)

# Si banc_à_étudiants est vide, max retourne 0
retourner max(map(len, bench_to_students.values()), par défaut=0)
«» "

- **Heure**: `O(n)` – un passage sur `étudiants'.
- **Espace**: `O(n)` – chaque élève unique occupe une entrée fixe.

---

##### Java 17

"Java
Importation de java.util.*;

solution de classe {
Int public maxÉtudiantsOnBench[][]étudiants] {
// banc_id -> ensemble d'élèves id
Carte<entier, ensemble<entier>> bancMap = nouvelle HashMap<>();

pour (int[] paire : étudiants) {
Int étudiant Id = paire[0];
banc int Id = paire[1];
benchMap.computeIfAbsent(benchId, k -> nouveau HashSet<>())add(étudiant Id);
}

= 0;
pour (Set<Integer> set : benchMap.values() {
max = Math.max(max, set.size());
}
retour max; // automatiquement 0 si banc La carte est vide
}
}
«» "

- `computerIfAbsent` crée paresseusement un `HashSet` lors de la rencontre d'un nouveau banc.
- Même "O(n)" temps et espace.

---

C++17

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
#inclut <unordered_set>
#incluez <algorithme>

solution de classe {
public:
int maxÉtudiantsOnBench(std::vector<std::vector<int>&étudiants) {
// banc_id -> ensemble d'élèves id
std::unordered_map<int, std::unordered_set<int>> bancMap;

pour (const auto & p : étudiants) {
Int étudiant Id = p[0];
banc int Id = p[1];
bancMap[benchId].insérer(étudiant Id);
}

à l'intérieur maxCnt = 0;
pour (const auto& kv : benchMap) {
maxCnt = md:max(maxCnt, static_cast<int>(kv.second.size()));
}
retour maxCnt; // 0 si banc Carte vide
}
};
«» "

- Utilise `unordered_map`/`unordered_set` pour les opérations de type `O(1)`.

---

C'est pas vrai. Bon, le méchant et le méchant

Catégorie
C'est pas vrai.
**Clarté**="set` + `map` explicit intention clairement=" Aucune=" Certains intervieweurs préfèrent une solution de tableau "raw" pour les micro-optimisations="
**Performance**=Le temps `O(n)`, l'espace `O(n)` – optimum==Le surf constant des tables de hachage==L'utilisation d'un tableau 2-D (taille 101×101) est toujours bonne, mais la perte de mémoire si de nombreux bancs inutilisés==
**Robustness**
**Readability**=======================================================================================================================================================================================================================

---

Analyse de complexité

**Heure**
C'est le cas.
**Python** Autres
*Java** Autres
*C++**=O(n)==O(n)= Autres

- "n = étudiants.longueur" (max. 100).
- Toutes les solutions sont bien dans les limites du LeetCode.

---

Solutions de rechange et compromis

1. **Utilisation d'un tableau booléen 2D**
- `bool occupé[101][101]` → `bench_id`, `student_id` indexing.
- Rapide et sensible à la mémoire pour les limites du problème, mais moins flexible si les ID de banc/d'élève ont augmenté.

2. **Découpage + balayage linéaire**
- Trier par `bench_id` puis compter les `student_id`s uniques par banc.
- Temps `O(n log n)`; travail supplémentaire inutile pour ce simple problème.

3. **Bitmasking**
- Depuis les ID ≤ 100, nous pourrions utiliser un masque 128 bits par banc.
- Surfait et moins lisible.

---

Structure du poste de blog optimisé par le SEO

1. **Titre (SEO)** – `Les étudiants maximum sur un seul banc – LeetCode 3450: Java, Python, C++ Solutions et conseils d'entrevue "
2. **Meta Description** – `Apprenez la solution optimale pour LeetCode 3450, avec le code Java, Python et C++ propre. Comprendre la complexité du temps et de l'espace, les cas de bord et les idées d'entrevue pour stimuler votre recherche d'emploi. "
3. **Étiquettes en tête** –
- Nombre maximum d ' élèves sur un banc unique (LeetCode 3450) "
- Oui. Énoncé du problème "
- Oui. Aperçu de la solution "
- Mise en œuvre de Python "
- Oui. Mise en œuvre Java "
- Oui. C++ Mise en œuvre "
- Oui. Analyse de complexité "
- Oui. Bon, mauvais, affreux "
- Oui. Conseils d'entrevue et conseils professionnels "
4. **Mots clés** – `LeetCode, codage d'entrevue, élèves maximum, Java, Python, C++, carte de hachage, ensemble de hachage, structures de données, complexité du temps, complexité de l'espace, entretien d'emploi, entretien d'ingénieur logiciel, questions d'entrevue de codage "
5. **Liens internes/externes** – Lien vers le problème LeetCode, les tutoriels connexes et votre portfolio ou LinkedIn.
6. **Call‐to‐Action** – `Comme, commentez et partagez si vous avez trouvé cela utile. Tu veux plus d'entretiens ? Abonnez-vous à ma newsletter ! "

---

À emporter

- Oui. Le modèle **set‐in‐a‐map** est la façon la plus propre, la plus rapide et la plus idiomatique de résoudre les étudiants maximums sur un seul banc. (en milliers de dollars)
- Oui. Il gère gracieusement les duplicatas et les entrées vides avec un code minimal.
- La compréhension de ce modèle démontre la maîtrise des tableaux **hash**, **set operations** et **edge-case raisonning**—key kill interviewers chercher.

> **Vous voulez impressionner les recruteurs? * *
> Déposer cet article sur votre blog, l'ajouter à votre portfolio et le partager sur LinkedIn. La combinaison d'une solution claire et d'une écriture conviviale au référencement est une façon éprouvée de se faire remarquer et de décrocher votre prochain rôle d'ingénierie logicielle. C'est ce qu'il a dit.

---

Bonus : Extraits de code complet

'`python
# Python 3
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maxÉtudiants OnBench(soi-même, étudiants: Liste[Liste[int]]) -> Int:
d = débit(set) par défaut
pour s, b chez les élèves:
d[b].add(s)
retourner max(map(len, d.values()), par défaut=0)
«» "

"Java
// Java 17
Importation de java.util.*;

solution de classe {
Int public maxÉtudiantsOnBench[][]étudiants] {
Carte<entier, ensemble<entier>> banc = nouveau HashMap<>();
pour (int[] p : étudiants) {
ifAbsent(p[1], k -> nouveau HashSet<>()).add(p[0]);
}
= 0;
pour (Set<Integer> set : bench.values()) {
max = Math.max(max, set.size());
}
retour max;
}
}
«» "

'`cpp
// C++17
#incluez <vecteur>
#inclut <non-ordonné_map>
#inclut <unordered_set>
#incluez <algorithme>

solution de classe {
public:
int maxÉtudiantsOnBench(std::vector<std::vector<int>&étudiants) {
std::unordered_map<int, std::unordered_set<int> banc;
pour (auto & p : étudiants) banc[p[1]].insérer(p[0]);

l'entrée mx = 0;
pour (auto& kv : banc) mx = md::max(mx, static_cast<int>(kv.second.size()));
retour mx;
}
};
«» "

Bon codage et bonne chance pour votre voyage d'entrevue!