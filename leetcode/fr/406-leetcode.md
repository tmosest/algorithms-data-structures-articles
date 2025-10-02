---
titre: LeetCode 406. Reconstruction des files d'attente par hauteur -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Reconstruction des files d'attente par hauteur – LeetCode 406
*Les bons, les mauvais et les méchants – Un profond Plongée + Java/Python/C++ Solutions*

---

TL; RD
> **Problème:** Reconstruire une file d'attente donnée par des paires de `[hauteur, k]` où `k` est le nombre de personnes devant qui sont **taller ou égal**.
> **Solution:** Trier les personnes **diminuer la hauteur** (années → augmenter `k`) et insérer chaque personne à l'index `k`.
> **Complexité:** temps `O(n2)`, espace `O(n)` (simple cupidité).
> **Variants:** `O(n log n)` utilisant un arbre indexé binaire / arbre de segment.

---

- Oui. 1. Présentation

Lors de la recherche d'un emploi en première ligne, les recruteurs aiment les problèmes de style LeetCode qui présentent des solutions *clever*.
La Reconstruction de Queue par Height est un problème moyen classique qui est souvent posé dans les entrevues.

Dans cet article, nous lisons:

1. Comprendre le problème et ses contraintes.
2. Marchez à travers l'algorithme avide «sort» et «insert» (la partie *bon*).
3. Discutez des pièges, des cas de bord, et pourquoi certains pensent que c'est la partie *mauvaise*.
4. Explorez le *ugly* – la complexité et les structures de données plus avancées.
5. Fournir le code prêt à la copie dans **Java**, **Python** et **C++**.
6. Offrez des conseils pour rendre l'emploi convivial (mots clés, méta-description, rubriques, etc.) pour attirer les gestionnaires d'embauche.

---

- Oui. 2. Exposé des problèmes

Vu un tableau "peuple" de paires "n" "[hi, ki]":

- "hi" – hauteur de la i-ème personne.
- `ki` – nombre de personnes devant la i-ème personne dont la hauteur est **≥** `hi`.

Reconstruisez la file d'attente qui satisfait toutes les paires.
Retourner la file d'attente en tant que tableau 2-D `queue[j] = [hj, kj]` où `queue[0]` est le front.

**Contrôles* *

Valeur des contraintes
C'est pas vrai.
1 ≤ n ≤ 2000
0 ≤ hl ≤ 106
0 ≤ ki < n ' est
Une reconstruction valide existe toujours.

---

- Oui. 3. Intuition – Pourquoi ♫Sort & Insertion

1. **Fixez d'abord les plus grands. **
Pour la personne la plus haute, le seul moyen de satisfaire `k` est de le placer `k`.
Puisque personne n'est plus grand, "k" ne compte que lui-même.

2. **Insérer des personnes plus courtes plus tard. **
Lors de l'insertion d'une personne plus courte, les personnes déjà placées plus grandes n'affecteront pas `k` parce qu'elles sont plus grandes ou égales.
En insérant à l'index exact `k`, nous garantissons que exactement `k` des personnes plus grandes ou égales sont en avance.

3. **Règle de classement**
*Trier par la hauteur descendante* → la plus haute d'abord.
*Tie*: trier en ascendant `k` de sorte que les personnes de la même hauteur mais plus petit `k` soient placés plus tôt, en assurant la justesse.

---

- Oui. 4. Algorithme (gredi)

Texte
Trier les personnes par:
1. hauteur descendante
2. k ascendant (pour des hauteurs égales)

file d'attente = liste vide
pour chaque personne (h, k) dans la liste triée:
insérer la personne à l'index k dans la file d'attente

file de retour
«» "

**Pourquoi `O(n2)`?**
Insertion dans un tableau à un indice aléatoire coûts `O(n)` en raison du déplacement.
Faire cela `n` fois donne `O(n2)`.

**Espace:**
Nous utilisons une liste supplémentaire pour la sortie – `O(n)`.

---

- Oui. 5. Code – 3 langues

### 5.1 Java (insertion de la liste des liens)

"Java
Importation de java.util.*;

solution de classe publique {
public int[][]rebâtirQueue[][[]]peuple] {
// 1. Tri par hauteur descendante, k ascendant
Arrays.sort(personnes, nouveau Comparateur<int[]>() {
public int compare(int[] a, int[] b) {
si (a[0] != b[0]) retour b[0] - a[0]; // hauteur descendante
retour a[1] - b[1]; // k ascendant
}
});

// 2. Insérer à l'index k en utilisant LinkedList (O(1) par insertion)
Liste<int[]> résultat = nouvelle liste liée<>();
pour (int[] p : personnes) {
résultat.add(p[1], p);
}

3. Convertir en int[]
int[] [] ans = nouveau int[people.longueur][2];
pour (int i = 0; i < result.size(); i++) {
ans[i] = result.get(i);
}
le retour des an;
}
}
«» "

> **Pourquoi une liste liée?**
> Insérer dans une `Liste Linkée` à un index connu est `O(1)` Une fois que vous avez le nœud.
> Mais parce que nous utilisons `List.add(index, element)`, Java marche toujours à l'index ('O(n)') – le même coût asymptotique.
> Le code est concis et reflète la solution LeetCode typique.

---

#### 5.2 Python (insertion de la liste)

'`python
Solution de classe:
def reconstruction Queue(self, people: List[List[int]]) -> Liste[Liste[int]]:
# Tri: hauteur descendante, k ascendant
personnes.sort(key=lambda x: (-x[0], x[1]))

res = []
pour h, k dans les gens:
res.insert(k, [h, k]) # O(n) par insert
retour res
«» "

---

### 5.3 C++ (insertion de vecteurs)

'`cpp
solution de classe {
public:
vecteur<vecteur<int>> ReconstructionQueue(vecteur<vecteur<int>>&personnes) {
// 1. Tri par hauteur descendante, k ascendant
tri(people.begin(), people.end(),
[](const vector<int>& a, const vector<int>& b) {
si (a[0] != b[0]) retourne a[0] > b[0]; // hauteur descendante
retour a[1] < b[1]; // k ascendant
});

// 2. Insérer à l ' index k
vecteur<vecteur<int>> rés;
pour (auto &p : personnes) {
res.insert(res.begin() + p[1], p); // O(n) par insert
}
retour rés;
}
};
«» "

---

- Oui. 6. Le bon, le mauvais, le mauvais

Aspect du bien
- C'est quoi ?
**Complexité temporelle**= Simple `O(n2)` – acceptable pour `n ≤ 2000`.= Pas optimal pour `n` très grande.== Pour `n` jusqu`à 105, `O(n2)` serait temps-out. Autres
**L'espace**="O(n)" – trivial.
**Mise en œuvre Simplicité** Requiert un comparateur de tri soigneux. Autres
**Readability** La règle du tri peut confondre les débutants. Le code de l'arbre de segment est verbeux. Autres
**Boîtes d'Edge** Aucun.
**Real-world Applicabilité**= Bon pour les démos d'entrevue.= Pas évolutive pour les ensembles de données énormes. Il faut connaître la structure des données. Autres

---

- Oui. 7. Optimisation en O(n log n) – L'arbre du segment

Lorsque `n` est grand, nous pouvons maintenir un **Binary indexed Tree (Fenwick)** ou **Segment Tree** pour trouver la `k`-th position vide dans `O(log n)`.
L'idée :

1. Tri comme avant (hauteur descendante, k ascendant).
2. Au départ, toutes les positions sont libres (`1`).
3. Pour chaque personne, trouvez l'index de l'emplacement `(k+1)'.
4. Marque cette fente comme occupée.

Cela réduit la complexité globale à "O(n log n)".

> *Pourquoi l'article? *
> Elle démontre un ensemble de compétences plus profond en matière de structure de données – souvent recherchées par les gestionnaires d'embauche.

---

- Oui. 8. Référencement et entretien— Conseils prêts pour le blog

Élément Recommandation
C'est-à-dire
**Titre** (LeetCode 406) – Java / Python / C++ Solution
**Meta Description**=Apprendre l'approche avide de LeetCode 406 – Reconstruction de file par hauteur. Code complet en Java, Python et C++. Comprendre la complexité temporelle, les cas de bord et les optimisations avancées. Autres
**H1 pour le titre, H2 pour les sections, H3 pour les sous-sections. Autres
**Mots clés**= `Queue Reconstruction by Height`, `LeetCode 406`, `Java solution`, `Python solution`, `C++ solution`, `greedy algorithme`, `segment tree`, `binary indexed tree`. Autres
** Formatage du code** Exclusivité triple avec identifiants de langue. Autres
**Call‐to‐Action**=Si vous préparez des entrevues de codage, ajoutez ce problème à votre liste de pratique. Autres
**Images** Autres
**Liens internes**= Lien vers d'autres blogs d'algorithmes (=Tricks d'algorithmes,=Binary Indexed Tree). Autres
**Liens externes**=La page de problème officiel LeetCode et les solutions principales (comme dans l'invite). Autres

---

- Oui. 9. Conclusion

- **Greedy Tri & Insert** est la solution canonique pour *Queue Reconstruction by Height*.
- Fonctionne en `O(n2)` – amende pour les contraintes d'entretien.
- Pour les grands ensembles de données, passer à une solution `O(n log n)` en utilisant BIT/Segment Tree.
- Les extraits de Java, Python et C++ fournis couvrent la version conviviale de l'interview et peuvent être copiés dans votre espace de travail IDE ou LeetCode.

Bon codage ! C'est ce qu'il a dit.
*(Si vous avez trouvé cet article utile, envisagez de partager ou de laisser un commentaire. Joyeux entretien!) *

---