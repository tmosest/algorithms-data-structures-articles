---
titre: LeetCode 1791. Trouver le centre de l'étoile graphique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1791 – Trouvez le centre d'un graphique d'étoile
**Guide, extraits de code et explication favorable à l'entrevue* *

---

C'est vrai. Quel est le problème ?

On vous donne un graphe *star* – un graphe non dirigé avec un seul noeud de centre de l'étoile qui est connecté à chaque autre noeud.
Le graphique est décrit par un tableau `edges`, où chaque entrée `[u, v]` représente un bord entre les nœuds `u` et `v`.

**Retourner l'étiquette du nœud central. **

> **Constraints**
> * "3 ≤ n ≤ 105"
> * "longueur des bords".
> * Chaque entrée est une paire d'entiers distincts entre `1` et `n`.
> * L'entrée représente toujours un graphique stellaire valide.

---

L'intuition – l'astuce de l'homme

Dans un graphique stellaire, **chaque bord contient le centre**.
Choisissez deux bords – le centre doit apparaître dans *deux* d'entre eux.

- Si "semences[0]]" est le centre, il apparaîtra également dans les «edges[1]».
- Sinon, l'autre paramètre du premier bord doit être le centre.

Cela donne une solution *temps constant* (O(1)), sans boucles, sans mémoire supplémentaire.

---

Code – 3 langues

- Oui. 1. Java

"Java
***
* Leetcode 1791 – Centre de recherche de Star Graph
Espace O(1)
*/
solution de classe publique {
public int findCenter(int[][] bords) {
// Le centre est le nœud commun dans les deux premiers bords
retour [arêtes[0][0]== arêtes[1][0]="arêtes[0]=]== arêtes[1][1]]
? bords[0][0] : bords[0][1];
}

// harnais d'essai simple
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
[[]] bords1 = {{1, 2}, {2, 3}, {4, 2}};
Système.out.println(s.findCenter(edges1)); // 2

[[]] bords2 = {{1, 2}, {5, 1}, {1, 3}, {1, 4}};
Système.out.println(s.findCenter(edges2)); // 1
}
}
«» "

- Oui. 2. Python 3

'`python
Solution de classe:
def findCenter(self, bords: List[List[int]]) -> Int:
# O(1) – même logique que Java
les bords de retour[0][0] si [les bords[0][0]]]
arêtes[0][0]== arêtes[1][1]) autres arêtes[0][1]


♪ Démo
si __nom__ == "__main__" :
s = Solution()
print(s.findCenter([[[1, 2], [2, 3], [4, 2]]) # 2
imprimer(s.findCenter([[[1, 2], [5, 1], [1, 3], [1, 4]]) # 1
«» "

- Oui. 3. C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

***
* Leetcode 1791 – Centre de recherche de Star Graph
Espace O(1)
*/
solution de classe {
public:
int findCenter(vecteur<vecteur<int>>& bords) {
retour [arêtes[0][0]== arêtes[1][0]="arêtes[0]=]== arêtes[1][1]]
? bords[0][0] : bords[0][1];
}
};

Int main() {
Solution s;
vecteur<vecteur<int>> e1{{1,2},{2,3},{4,2}};
vecteur<vecteur<int>> e2{{1,2},{5,1},{1,3},{1,4}};
cout << s.findCenter(e1) << endl; // 2
Cout << s.findCenter(e2) << endl; // 1
}
«» "

---

J'ai une idée. Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
Autres **Complexité du temps**
Autres **Complexité de l'espace**
**Mise en oeuvre**= Un liner – propre, lisible== Aucune=La suringénierie avec des boucles ou des cartes perd du temps==
**Robustness**= Fonctionne pour tout graphe stellaire valide=______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________ Autres
**Readability**
**Cas d'escroquerie**

> **Astuce:** Mentionnez la propriété *observationnelle* (le centre apparaît à chaque bord) pendant l'entrevue; cela démontre que vous lisez la déclaration en détail.

---

Analyse de complexité

Métrique
- C'est quoi ?
**Heure**
L'espace
*Big-O**

Toutes les solutions sont * amorties* O(1) parce qu'elles inspectent au plus deux bords.

---

Les alternatives et quand les utiliser

L'approche quand elle rend sensé
- C'est quoi ?
**Scan complet** (`pour les bords dans les bords`)) Autres
**Enregistrement de la carte de l'hash**= Graphiques généraux où le centre peut être identifié par fréquence== O(n) temps et espace, overkill==
Autres Si vous voulez illustrer les opérations de réglage, mais plus clair pour les graphiques non-étoiles

---

Comment cela vous aide à trouver un emploi

* **Interview Prep** – Démontrer un knack pour *observation rapide* et *temps constant*.
* **Qualité du code** – Un liner, pas de nombres magiques, commentaires clairs.
* **La pensée algorithmique** – Montrez que vous pouvez identifier les propriétés du graphique (le centre apparaît dans chaque bord).
* **Performance** – Mettre l'accent sur la solution O(1); les intervieweurs aiment les compromis espace-temps.

Ajoutez ceci à votre portfolio, partagez sur GitHub, ou postez une entrée de blog. Mentionnez l'ID de Leetcode, les balises (`Easy`, `Graph`, `Arrays`), et soulignez l'heure **O(1)** dans le titre – SEO or pour les recruteurs à la recherche de la solution Leetcode 1791.

---

## OBJECTIFS SEO–Amis Résumé (pour votre blog)

- **Titre**: Leetcode 1791 – Centre de recherche de Star Graph en O(1): Java, Python, C++ One-Liner
- **Description détaillée**: Solve Leetcode 1791 – Centre de recherche de Star Graph en utilisant un monoligne à temps constant en Java, Python et C++. Apprenez l'astuce, la complexité du temps/de l'espace et les idées d'entrevue. (en milliers de dollars)
- **Mots clés**: *Leetcode 1791, Find Center of Star Graph, solution O(1), Java, Python, C++, algorithme de graphique, question d'entrevue, entretien d'ingénieur logiciel, prép d'entrevue d'emploi*

---

À emporter

Le graphe stellaire – chaque bord contient le centre – vous permet de résoudre le Leetcode 1791 en *une ligne* avec **O(1)** temps et espace.
Écrivez le code propre, expliquez l'intuition, et vous impressionnerez les intervieweurs et les recruteurs. Bon codage !