---
titre: LeetCode 491. Sous-séquences de non-diminution
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 491. Sous-séquences de non-diminution
> **Moyen******Backtracking + HashSet**

---

Déclaration du problème (Code Leet)

> **Grâce à un tableau entier `nums`, retournez **tous** les sous-séquences *différentes* possibles non décroissantes du tableau donné avec *au moins deux* éléments.
> La réponse peut être dans n'importe quel ordre.

**Exemple**

Entrée Sortie
C'est quoi ?
[4,6,7],[4,7],[6,7],[6,7],[6,7],[6,7],[6,7],[4,7],[6,7],[6,7]» Autres
[4,4] Autres

**Contrôles* *

"1 ≤ longueur nominale ≤ 15"
- `-100 ≤ nums[i] ≤ 100`

---

Aperçu de la solution

Les principaux défis :

1. ** Ordre non décroissant** – une subséquence ne peut être prolongée que si le nouvel élément est **≥** le dernier élément du chemin actuel.
2. **Duplications** – l'entrée peut contenir des nombres répétés, tant de chemins différents peuvent produire la sous-séquence * même*.
Nous devons afficher chaque sous-séquence **une fois**.

L'approche classique est **backtracking** (DFS) avec un **`HashSet`** pour éviter les duplications.

Étapes arrière

1. Commencez par un chemin vide `cur`.
2. Pour chaque indice `i` de `start` à `n-1`:
- Si `cur` est vide ou `nums[i] ≥ cur.last`, nous pouvons ajouter `nums[i]` à `cur`.
- Continuer de façon récursive à partir de "i+1".
- Retour en arrière en supprimant "nums[i]".
3. Chaque fois que la longueur du chemin courant ≥ 2, ajoutez une *copie* de celle-ci à une `Set<List<Integer>` (pour dédoubler).
4. Après avoir exploré toutes les possibilités, retourner l'ensemble converti à une liste.

### Éviter les doubles emplois efficacement

- Parce que la longueur du tableau est au plus 15, le nombre total de sous-séquences est gérable (`- 215 = 32 768`).
- Néanmoins, les duplicata peuvent être fréquentes (par exemple, `[4,4]`).
- Utiliser une `Set<List<Integer>>` dédouble automatiquement, et les frais généraux sont négligeables pour les limites données.

---

Mise en œuvre du code

Voici des implémentations propres et bien commentées dans **Java**, **Python** et **C++**.

---

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<Liste<entier>> trouver subséquences(int[] nombres) {
Définir <Liste<entier>> res = nouveau HashSet<>();
dfs(nums, 0, nouvelle ArrayList<>(), res);
retourner une nouvelle liste d'array<>(res);
}

vide privé dfs(int[] nums, int index, List<Integer> cur, Set<List<Integer>> res) {
si (cur.size() >= 2) {
// Conservez une *copie* pour que les modifications ultérieures n'affectent pas l'entrée définie
res.add(new ArrayList<>(cur));
}

pour (int i = index; i < nombres.longueur; i++) {
Si (cur.isEmpty()="nums[i] >= cur.get(cur.size() -1)) {
le nom et l'adresse du destinataire;
dfs(nums, i + 1, cur, res);
cur.remove(cur.size() - 1); // backtrack
}
}
}
}
«» "

> **Pourquoi un "HashSet"?**
> Javas `HashSet` utilise `equals()`/`hashCode()` sur les listes, de sorte que les séquences dupliquées sont automatiquement supprimées.

---

# # # # # #

'`python
de taper l'importation Liste, jeu, tuple

Solution de classe:
def trouver Subséquences(self, nombres: List[int]) -> List[List[int]]:
résultat: Set[Tuple[int, ...]] = set()
auto.backtrack(nombres, 0, [], résultat)
retour [liste(t) pour t en résultat]

def backtrack(self, nombres: List[int], index: int,
chemin : List[int], résultat : Set[Tuple[int, ...]]) -> Aucun:
si len(path) >= 2 :
result.add(tuple(path)) # tuples sont hashables

pour i dans la plage(index, len(nums)):
si non chemin ou nombres[i] >= chemin[-1]:
chemin.append(nums[i])
auto.backtrack(nums, i + 1, chemin, résultat)
chemin.pop() # retour
«» "

> ** Pourquoi tuples ? **
> Le "set" de Python n'accepte que les objets hashables. La conversion de la liste en tuple nous permet de stocker des sous-séquences sans duplicata.

---

C'est vrai. C++

'`cpp
#incluez <vecteur>
#incluez <set>
utilisant l'espace de noms std;

solution de classe {
public:
vector<vector<int>> findSubséquences(vector<int>& nums) {
ensemble <vector<int>> rés;
vecteur <int> cur;
dfs(nums, 0, cur, res);
vecteur de retour<vector<int>>(res.begin(), res.end());
}

particulier:
vide dfs(vecteur const<int>& nums, int idx,
vector<int>& cur, set<vector<int>& res) {
si (cur.size() >= 2) res.insert(cur);

pour (int i = idx; i < nums.size(); ++i) {
si (cur.vide()) {
cur.push_back(nums[i]);
dfs(nums, i + 1, cur, res);
cur.pop_back(); // retour
}
}
}
};
«» "

> **C++ `set`** commande automatiquement et dédouble les sous-séquences.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Exploration du DFS **O(n · 2n)** ( pire cas) – chaque sous-ensemble peut être visité
Autres Définissez l'insertion **O(k log k)** par insertion, où *k* est le nombre de sous-séquences uniques (2n))**O(k · n)** total pour toutes les sous-séquences stockées

Compte tenu de «n ≤ 15», l'algorithme s'adapte confortablement dans les délais.

---

Conseils pour l'entrevue

C'est bien, c'est mal.
C'est pas vrai.
Utilisez le rétrotraçage pour générer des sous-séquences de manière progressive. Autres
Il en résulte un `Set` (ou `unordered_set` / `HashSet`) pour déduper automatiquement. Autres
Expliquez clairement la complexité du temps et de l'espace. Ne pas manipuler les nombres négatifs – s'assurer que la comparaison est `>=`. Autres

---

Article du blog : Le bon, le mauvais et le mauvais de LeetCode

> **Meta-Titre:** *Master LeetCode 491: Subséquences non déclenchantes – Le bon, le mauvais et le mauvais (Java, Python, C++)*
> **Méta—Description:** *Découvrez la solution étape par étape de LeetCode 491. Apprenez les pièges, le code en Java/Python/C++, et ace votre interview de codage. Boostez votre CV aujourd'hui! *

---

C'est pas vrai. Ce qui fait Ce problème
- Petite taille d'entrée (`n ≤ 15`) mais explosion combinatoire de possibles sous-séquences.
- Nécessite une manipulation soigneuse de ** duplicata** – un piège d'entrevue commun.
- Doit respecter la contrainte **non-diminution** tout en générant tous les sous-ensembles valides.

---

C'est vrai. Le bon : le retour élégant + HashSet

- **Le backtracking** donne une structure récursive naturelle : à chaque index, décidez si *inclut* ou *skip* l'élément courant.
- **HashSet** (ou `set` en C++ / `Set` en Java) supprime le fardeau des vérifications manuelles dupliquées.
- Un code propre et lisible qui peut être adapté à de nombreuses variantes de suite.

---

C'est vrai. Les mauvaises: pièges communs

Pourquoi ça arrive ?
- Oui.
*Ne pas copier le chemin avant de l'insérer dans le jeu * La même instance `Liste` est mutée plus tard. Créer une nouvelle `ArrayList<>(path)` (ou `tuple(path)` dans Python). Autres
*Ajout de subséquences de longueur 1*= État du problème *au moins deux* éléments. Vérifier `path.size() >= 2' avant d'ajouter. Autres
*L'utilisation d'une liste globale au lieu d'un ensemble*=Les duplicatas survivent parce que l'égalité de liste n'est pas utilisée automatiquement. Autres Utilisez un conteneur `Set`. Autres

---

C'est pas vrai. L'Ugly : les joueurs de performance

Dans le pire des cas (par exemple, tous les éléments sont égaux), la récursion explore les chemins `2n`. Pour `n=15`, il est d'environ 32k, ce qui est bien.
- **Espace**: Entreposer chaque sous-séquence unique pourrait exploser si le tableau contient de nombreuses valeurs distinctes. Cependant, les contraintes maintiennent cette gestion.
- **Éviter**: Concaténation excessive de cordes, récursion profonde au-delà de `n` (mais ici `n ≤ 15`).

---

Code en trois langues – Un pour chaque pile

> *Voir les implémentations ci-dessus. *
> Choisissez la langue avec laquelle vous êtes le plus à l'aise, ou présentez les trois sur votre GitHub.

---

#### 6-SEO-Friendly Takeaways for Job Seekers

- **Mots-clés**: LeetCode 491 solution, non-décroissant subséquences, interview backtracking, Java Python C++, conseils d'entrevue de codage.
- **En-têtes**: Utilisez H1 pour le titre, H2 pour les sections comme .Good, .Bad, .Ugly, et H3 pour les sous-points.
- **Meta Tags**: Inclure le numéro de problème et les termes clés dans la méta-description.
- **Édifice Link** : Référencez le problème officiel LeetCode, des solutions similaires, et votre propre repo GitHub.
- **Engagement**: Ajouter un court paragraphe pour encourager les commentaires.

---

Liste de contrôle finale avant de soumettre

- Essai avec les exemples fournis.
- Ajouter des cas de bord : tous les nombres négatifs, élément unique répété, tableau en pleine croissance.
- S'assurer que la profondeur de récursion ne dépasse pas les limites de la pile.
- Exécuter des tests de temps et de mémoire (sections LeetCode-Runtime)

---

À emporter

LeetCode 491 est un puzzle *classique* qui teste la pensée algorithmique et l'attention aux détails. En maîtrisant le modèle de retour et le tour de déduplication, vous allez non seulement résoudre ce problème, mais aussi gagner une boîte à outils réutilisable pour une large gamme de questions suivantes.

Allez-y, polissez votre solution et partagez-la sur votre portefeuille. Bonne chance pour ce travail de rêve !