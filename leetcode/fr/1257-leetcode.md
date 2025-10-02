---
titre: LeetCode 1257. Région commune la plus petite -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1257 – Petite région commune
> *Découvrez le plus petit ancêtre commun de deux nœuds dans une hiérarchie*
> **Langues**: Java-Python-C++
> **SEO Mots-clés**: Petite Région Commune, LeetCode 1257, LCA dans un arbre, Tree traversal, question d'entrevue Java, problème d'entrevue Python, codage d'entrevue C++

---

Aperçu du problème

On nous donne une hiérarchie des régions géographiques.
Chaque liste d ' entrées `régions[i]` est de la forme

«» "
[parent, enfant1, enfant2, ...]
«» "

* "parent" **directement** contient tous les «enfants».
* La relation est transitoire – si *A* contient *B* et *B* contient *C*, alors *A* contient indirectement *C*.

Compte tenu de deux noms de région (`région1`, `région2`), nous devons retourner **la plus petite région qui contient les deux**.
Il est garanti qu'une telle région existe (la racine de l'arbre).

> Exemple
> `region1 = "Québec"`, `region2 = "New York"` → Amérique du Nord**

---

- Oui. Le point de vue fondamental

La hiérarchie est un arbre **raciné** où chaque noeud a *exactement un* parent.
La recherche de la plus petite région commune équivaut à la recherche de l'ancêtre commun **Lowest (LCA)** des deux noeuds.

Deux façons classiques de résoudre les problèmes de LCA :

Démarche Temps Espace Quand utiliser
- C'est quoi ?
**Parent-Map + Set** (notre solution)="O(N)` pour construire la carte + `O(H)` pour traverser chaque nœud les ancêtres="O(N)` pour la carte, `O(H)` pour set=" Simple, pas de structure d`arbre supplémentaire nécessaire, fonctionne pour tout `H` ≤ `N`
**Binary Lifting / Euler Tour + RMQ**=1 `O(log N)` par requête après `O(N log N)` préprocessing=1 `O(N log N)`=1 Besoin de nombreuses requêtes sur un grand arbre statique=1

Parce que le problème demande une seule requête, la première approche est la plus naturelle et la plus facile à mettre en œuvre dans chaque langue.

---

Algorithme (parent-carte + jeu)

1. **Construire un enfant → carte des parents* *
Pour chaque liste `L`:
* `parent = L[0]`
* Pour chaque `enfant` dans `L[1 ...]`, carte `enfant → parent`.

2. **Collecter les ancêtres de la région1**
Montez de `region1` à la racine, en insérant chaque noeud visité dans un hachage.

3. **Trouver le premier ancêtre commun**
Marchez depuis la "région2".
Le premier noeud qui apparaît dans l'ensemble est la plus petite région commune.

Parce que la hauteur de l'arbre est au plus `N`, chaque promenade prend `O(H)` temps.

---

La complexité

Étape Temps Espace
C'est pas vrai.
Construire une carte Autres
Marcher "région1" Autres
Marcher "région2"
Total** Autres

`N` = nombre total de régions (`- 10^4`), `- H` = hauteur de l'arbre (`- N`).

---

Mise en œuvre

Voici des implémentations propres et prêtes à la production pour **Java, Python et C++**.
Les trois suivent les mêmes étapes algorithmiques et utilisent les mêmes conventions de nommage.

Autres **Astuce** – Toujours lire l'entrée dans les structures de données correctes (par exemple, `Liste<Liste<String>>` dans Java, `Liste[Liste[str]]` dans Python, `vector<vector<string>>` dans C++).
Autres **Edge Cases** – La racine peut apparaître comme un enfant dans une liste différente? Non – le problème garantit un parent unique par enfant, donc notre construction de carte est sûre.

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
***
* Trouver la plus petite région commune qui contient à la fois la région1 et la région2.
*
* Régions @param Liste des listes régionales. Le premier élément de chaque liste est le parent,
* les autres sont ses enfants directs.
* @param région1 Le nom de la première région.
* @param région2 Le nom de la deuxième région.
* @retour Le nom de la plus petite région commune.
*/
public Recherche à chaînesRégion(Liste<Liste<String>> régions,
Région chaîne1, région chaîne2) {
// 1. Construire la carte de l'enfant → parent
Carte <String, String> enfantParent = nouveau HashMap<>();
pour (Liste<String> liste : régions) {
Chaîne parent = list.get(0);
pour (int i = 1; i < list.size(); i++) {
enfantParent.put(list.get(i), parent);
}
}

// 2. Ancêtres de la région
Définir <String> ancêtres = nouveau HashSet<>();
pendant que (région1 != null) {
ancêtres.add(région1);
région1 = enfantParent.get(région1);
}

// 3. Marchez de la région2 pour trouver le premier ancêtre commun
alors que (région 2 != null) {
si (les agents.contient(région2)) {
région de retour2;
}
région2 = enfantParent.get(région2);
}

// Garanti par le problème qu'existe une région commune.
retour nul;
}

// Exemple d'utilisation / test
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Liste<Liste<String>> Régions = Arrays.asList(
Arrays.asList("Terre", "Amérique du Nord", "Amérique du Sud"),
Arrays.asList("Amérique du Nord", "États-Unis", "Canada"),
Arrays.asList("États-Unis", "New York", "Boston"),
Arrays.asList("Canada", "Ontario", "Québec"),
Arrays.asList("Amérique du Sud", "Brésil")
);
System.out.println(sol.findSmallestRegion(régions, "Québec", "New York"); // Amérique du Nord
System.out.println(sol.findSmallestRegion(régions, "Canada", "Amérique du Sud"); // Terre
}
}
«» "

5.2 Python

'`python
de taper l'importation Liste, Dict, Jeu

Solution de classe:
trouverSmallestRegion(
soi-même,
régions: Liste[Liste[str]],
région1: str,
région2: str
) -> str:
# 1. enfant -> carte des parents
_parent de l'enfant : Dict[str, str] = {}
pour les régions:
parent = lst[0]
pour l'enfant dans lst[1:]:
enfant_parent[enfant] = parent

2. Ancêtres de la région1
ancêtres: Set[str] = set()
alors que la région1 n'est pas Néant:
ancêtres.add(région1)
region1 = child_parent.get(region1)

# 3. Marche vers le haut de la région2
alors que la région2 n'est pas Néant:
si région2 chez les ancêtres:
région de retour2
region2 = child_parent.get(region2)

retour "" # inaccessible – problème garantit une solution


♪ Exemple d'essai
si __nom__ == "__main__" :
sol = Solution()
régions = [
["Terre", "Amérique du Nord", "Amérique du Sud"],
["Amérique du Nord", "États-Unis", "Canada"],
["États-Unis", "New York", "Boston"],
[Canada, Ontario, Québec],
["Amérique du Sud", "Brésil"]
- Oui.
print(sol.findSmallestRégion(régions, "Québec", "New York") Amérique du Nord
print(sol.findSmallestRégion(régions, "Canada", "Amérique du Sud") # Terre
«» "

C++

'`cpp
#incluez <iostream>
#incluez <vecteur>
#inclut <non-ordonné_map>
#inclut <unordered_set>
#incluez <string>

solution de classe {
public:
std::chiffre trouvéLa région la plus petite(
mtd::vector<std::vector<std::string>& régions,
md::région de corde1, md::région de corde2) {

// 1. enfant → carte des parents
std::unordered_map<std::string, std::string> enfant parent;
pour (const auto & lst : régions) {
const std::string & parent = lst[0];
pour (size_t i = 1; i < lst.size(); ++i) {
enfantParent[lst[i]] = parent;
}
}

// 2. ancêtres de la région1
std::unordered_set<std::string> ancêtres;
pendant que (!region1.vide()) {
ancêtres.insert(région1);
auto it = childParent.find(region1);
region1 = (it == childParent.end()) ? "" : it->seconde;
}

// 3. monter de la région2
pendant que (!region2.vide()) {
si (avertisseurs.count(region2)) région de retour2;
auto it = enfantParent.find(région2);
region2 = (it == childParent.end()) ? "" : it->seconde;
}

retour "; // Ne devrait jamais frapper ici
}
};

Int main() {
Solution sol;
md::vector<std::vector<std::string>> régions = {
"Terre", "Amérique du Nord", "Amérique du Sud",
{"Amérique du Nord", "États-Unis", "Canada"},
"États-Unis", "New York", "Boston",
"Canada", "Ontario", "Québec",
{"Amérique du Sud", "Brésil"}
};

À l'exception de l'Amérique du Nord, l'Amérique du Nord est la région la plus peuplée.
std::tout << sol.findSmallestRegion(régions, "Canada", "Amérique du Sud") << '\n'; // Terre
}
«» "

---

# # # 6 Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
**Bon**. • Construction d'un 1-pass d'une carte – O(N) temps et espace. <br>• Fonctionne pour toute forme d'arbre, aucune hypothèse particulière. Le code est court, facile à vérifier.
**Bad** mémoire supplémentaire pour la carte – pas idéal pour les arbres gigantesques. <br>• Pour de nombreuses requêtes répétées, nous payons `O(N)` carte construire chaque fois.
**Désormais** Si les listes de saisie ne sont pas triées ou contiennent des duplicatas, la carte peut écraser les parents. <br>• L'algorithme ne détecte pas les cycles – suppose un arbre valide selon les contraintes. <br>• Dans des langages comme Python, la profondeur de récursion n'est pas pertinente ici, mais un parcours basé sur une pile est plus simple.

**Ce que les intervieweurs veulent vraiment**
- Correction pour tous les cas de bord (racine seulement, hiérarchies profondes).
- Un raisonnement clair sur la raison pour laquelle l'algorithme trouve la région *la plus petite* commune (le premier ancêtre commun qui monte).
- Discussion sur le temps/l'espace – mentionner qu'une solution de levage binaire réduirait le temps de requête au coût de plus de mémoire et de prétraitement.

---

## 7-

1. **Clarifier le nombre de requêtes** – demander si plusieurs requêtes peuvent être nécessaires.
2. **Énoncer les contraintes** – confirmer que chaque enfant n'a qu'un seul parent et n'a aucun cycle.
3. **Afficher la première intuition commune de l'ancêtre** – de nombreux candidats oublient que la marche doit partir de la "région1" et utiliser un ensemble.
4. **Exposer la complexité** – mettre en évidence le prétraitement linéaire et le passage de l'ancêtre linéaire.
5. **Demander au sujet du prétraitement** – un bon suivi: Si nous avions 105 requêtes, qu'est-ce que vous changeriez ? – réponse avec levage binaire / RMQ.

---

- Oui. Pensée finale

La solution « & #160; parent‐map & #160; set=» est un exemple de manuel de suivi de l'ancêtre basé sur la carte**.
Il combine lisibilité, simplicité et performance solide pour une seule requête – exactement ce que ce problème LeetCode nécessite.
Avec les trois implémentations linguistiques ci-dessus, vous êtes prêt à aborder le problème dans n'importe quel contexte d'entretien ou de production.

Bon codage ! C'est ce qu'il a dit.

---

*Si vous avez trouvé ce guide utile, n'hésitez pas à "" sur GitHub, partagez-le avec des amis, ou commentez ci-dessous si vous avez des questions sur les cas de bord de ""ugly". *