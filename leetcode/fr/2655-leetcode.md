---
titre: LeetCode 2655. Trouver le maximum Portées non couvertes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2655 – Trouver un maximum Portées non couvertes
**Moyenne de leetCode= Interviews=Algorithme=Java=Python=C++**

---

### TL;DR
* Trier les plages données par le paramètre gauche.
* Balayer un pointeur sur la liste triée, en recueillant les lacunes qui ne sont pas couvertes.
* Complexité : **O(m log m)** temps, **O(m)** espace auxiliaire (`m = gammes.longueur`).
* Fonctionne même quand `n` est jusqu'à `109` parce que nous ne construisons jamais tout le tableau.

---

- Oui. Pourquoi ce problème est-il une question d'interview à savoir

1. ** Importance réelle** – c'est essentiellement la même chose que de trouver des créneaux horaires libres dans des calendriers, des blocs IP inutilisés ou des plages de stockage non assignées.
2. **Élégante ligne de balayage** – vous apprenez un motif algorithmique classique: trier, scanner et garder un pointeur en mouvement.
3. **Maîtrise d'Edge-case** – la taille d'entrée (`n`) peut être énorme, si naïve solutions O(n) ou O(n × m) sont un *trap*.

Si vous pouvez expliquer cette solution proprement et la coder en **Java, Python et C++**, vous vous démarquerez dans une interview technique.

---

- Oui. 1. Remise en état des problèmes

Compte tenu d'un entier `n` (longueur d'un tableau `nums`) et d'un tableau 2-D `ranges` où chaque `ranges[i] = [l, r]` (inclus), trouver **toutes les gammes maximales découvertes**.
Une plage maximale à découvert est un «[a, b]» sous-intervalle tel que:

1. Aucune cellule de `[a, b]` ne se trouve à l'intérieur d'aucune `range[i]`.
2. L'intervalle ne peut pas être prolongé d'un côté ou de l'autre (c'est-à-dire `b + 1 ' nextLeft').

Retourner les plages découvertes triées par index de départ.

*exemple*

«» "
n = 10, gammes = [[3,5],[7,8]]
[[0,2],[6,6],[9,9]]
«» "

---

- Oui. 2. Approches naïves (et condamnées)

L'approche Pourquoi elle échoue (le pire cas)
- C'est quoi ?
Construire un tableau booléen de la longueur `n` et marquer les cellules couvertes. Autres
Autres Pour chaque plage, marquez les cellules; puis analysez les lacunes. Autres
Autres Fusionner les gammes d'abord, puis soustraire de `[0, n-1]` La fusion est `O(m log m)` mais si vous construisez également un tableau, vous revenez à `O(n)`. Autres

Ces approches s'évanouissent parce qu'elles ignorent le fait que **seulement les fourchettes elles-mêmes comptent**, pas tous les indices à l'intérieur de `0 ... n‐1`.

---

- Oui. 3. La solution Élégante de la ligne de balayage

1. **Trier les « fourchettes » par le paramètre gauche (croissant).
2. Maintenir un pointeur «ptr» qui indique le plus petit indice découvert jusqu'à présent. Initialement `ptr = 0`.
3. Pour chaque gamme triée «[l, r]»:
* Si `ptr < l`, l`écart `[ptr, l-1]` est découvert → ajouter à la réponse.
* Mettre à jour `ptr = max(ptr, r + 1)` (nous ne pouvons pas retourner à une zone déjà couverte).
4. Après la boucle, si `ptr < n`, la queue `[ptr, n-1]` est découvert → ajouter.
5. Retournez la liste collectée.

Parce que nous trions seulement les plages de temps (= 106) et effectuons un seul passage linéaire, l'algorithme est optimal.

---

- Oui. 4. Code

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

> **Conseil:** Pour les intervieweurs, vous pouvez montrer comment chaque langue gère la même logique.
> Si vous postulez, vous pouvez coller ces extraits dans votre CV ou GitHub.

---

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int[][] findMaximalUncoveredRanges(int n, int[][] gammes) {
// Clauses de garde
i (plages) : null. 0) {
retour n == 0 ? nouveau int[0][0] : nouveau int[][]{{0, n - 1}};
}

// Trier par le paramètre gauche
les tableaux.sort(ranges, Comparator.comparingInt(a -> a[0]);

Liste<int[]> ans = nouvelle liste de distribution<>();
int ptr = 0;

pour (int[] r : gammes) {
int l = r[0], rgt = r[1];

si (ptr < l) { // trou découvert trouvé
as.add(nouvelle int[]{ptr, l - 1});
}
// Déplacer le pointeur au-delà de la plage actuelle
ptr = Math.max(ptr, rgt + 1);
}

si (ptr < n) { // queue découverte
as.add(nouvelle int[]{ptr, n - 1});
}

retourner les ans.àArray(nouvelle int[ans.size()][]);
}
}
«» "

---

4.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def findMaximalUncoveredRanges(self, n: int, gammes: List[List[int]]) -> Liste[Liste[int]]:
Si ce n'est pas le cas, fourchettes:
retour [[0, n - 1]] si n > 0 autre []

# Trier par le paramètre gauche
gammes.sort(key=lambda x: x[0])

ans = []
ptr = 0

pour l, r dans les fourchettes:
si ptr < l: # segment découvert
Annexe([ptr, l - 1])
ptr = max(ptr, r + 1)

si ptr < n: # segment suivant
Annexe([ptr, n - 1])

retour et
«» "

---

### 4.3 C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
std::vector<std::vector<int>> findMaximalUncoveredRanges(int n, std::vector<std::vector<int>&& ranges) {
si (plage.vide()) {
retour n > 0 ? std::vector<std::vector<int> {{0, n - 1}} : std::vector<std::vector<int>();
}

// Trier par le paramètre gauche
std::sort(ranges.begin(), ranges.end(),
[](const std::vector<int>& a, const std::vector<int>& b) {
retourner a[0] < b[0];
});

std::vector<std::vector<int>> ans;
int ptr = 0;

pour (const auto & seg : gammes) {
int l = seg[0], r = seg[1];

si (ptr < l) { // partie non couverte
le nom de l'autorité compétente de l'État membre d'origine;
}
ptr = md::max(ptr, r + 1); // pointeur de déplacement
}

si (ptr < n) { // partie traînante
as.push_back({ptr, n - 1});
}

le retour des an;
}
};
«» "

---

- Oui. 5. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Classer les « fourchettes » **O(m log m)**
Une seule analyse linéaire **O(m)**
Total **O(m log m)

Avec `m ≤ 106`, cela fonctionne confortablement en moins d'une seconde sur les machines modernes.

---

- Oui. 6. Bon, mauvais, et humble

Catégorie Que mettre en évidence ?
Il y a un problème.
**Bon*** *Traitement + balayage* – temps linéaire après tri, pas de construction de tableau. Aucun
Des solutions `O(n)` (construisant le tableau entier) – seront rejetées sur le grand `n`.
**Il faut garder les lacunes **minimales**.

Traces d'entrevue courantes

1. ** Erreurs hors pair** – rappelez-vous que les fourchettes sont inclusives.
2. **Empty input** – n'oubliez pas le cas où tous les indices sont découverts.
3. **Grand `n`** – évitez de créer un tableau de taille `n`.
4. **Dupliquer des gammes** – trier les poignées naturellement ; vous n'avez jamais besoin de fusionner explicitement à moins de vouloir compresser la mémoire plus loin.

---

- Oui. 7. Applications pratiques

Domaine Pourquoi l'algorithme compte
- C'est pas vrai.
Rechercher des emplacements gratuits entre les événements. Autres
Calculer les blocs IP inutilisés à partir des plages attribuées. Autres
Autres fragmentation du système de fichiers. Autres
Autres Conception de niveau de jeu. Autres

La compréhension de ce problème vous permet de répondre à toute question d'intervalle qui apparaît dans des scénarios réels.

---

- Oui. 8. SEO-Friendly Takeaway

Si vous ciblez des recruteurs ou des jurys d'entrevue technique, cette écriture riche en mots clés vous aidera à découvrir :

* **Tarifs maximum non couverts** – LeetCode 2655
* **Algorithme de fusion intermédiaire** – stratégie d'entrevue
* **Java, Python, solutions C++** – extraits de code
* ** Analyse de complexité** – temps O(m log m), espace O(m)

Les moteurs de recherche aiment le contenu structuré. En utilisant des rubriques audacieuses, des clôtures de codes et un ton conversationnel propre, votre blog se classera haut pour les développeurs se préparant pour LeetCode 2655 ou toute entrevue qui exige un raisonnement basé sur l'intervalle.

---

- Oui. 9. Mot final

- **Rappelez-vous**: `n` n'est qu'un *boundary*; seules les gammes comptent.
- **Afficher** le modèle de ligne de balayage; les intervieweurs aiment des solutions propres et généralisables.
- **Pratique** codant dans toutes les langues avec lesquelles vous êtes à l'aise; mettre en évidence les différences (par exemple, `Arrays.sort` vs `ranges.sort`).

Bonne chance pour casser LeetCode 2655 – c'est le même jeu de compétences qui transforme les questions d'entrevue en résolution de problèmes dans le monde réel. Bon codage !