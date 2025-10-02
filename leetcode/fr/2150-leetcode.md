---
titre: LeetCode 2150. Trouver tous les nombres solitaires dans le tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 2150 – Trouver tous les numéros isolés dans le tableau
**Java.Solutions Python.++** + un article de blog optimisé pour le référencement qui couvre le bon, le mauvais et le laid* de ce problème – un post-mortem parfait pour votre prochaine interview de codage.

> **Mots-clés:** *LeetCode 2150, Trouver tous les numéros Lonely, interview de codage, solution Java, solution Python, solution C++, algorithme, complexité temporelle, complexité spatiale, carte de hachage, tableau de fréquence. *

---

Résumé du problème

On vous donne un nombre entier.
Un nombre `x` est **seulement** si:

1. `x` se produit **exactement une fois** dans le tableau.
2. Ni `x-1` ni `x+1` n'apparaît dans le tableau.

Retournez tous les numéros solitaires dans n'importe quel ordre.

*exemple*
`nums = [0,6,5,8] → [0,8]`
Les numéros 10 et 8 apparaissent une fois, et aucun n'a de nombres adjacents dans le tableau.

**Contrôles* *

Valeur des contraintes
C'est pas vrai.
1 ≤ longueur nominale ≤ 105
< 0 ≤ nums[i] ≤ 106 '

---

## Aperçu de la solution

Il existe trois stratégies communes:

L'approche Temps Espace Remarques
C'est pas vrai.
*Désormais** (en place) : Simple mais pas optimal pour les contraintes données. Autres
*HashMap / HashSet** Il manipule facilement les plages arbitraires. Autres
Tableau de fréquence** Le plus rapide si `max(nums)` est petit (1 e6). Autres

Le tableau **fréquence** est le plus rapide pour ce problème car la plage de valeurs est limitée.
Nous allons illustrer cela dans la section *bon* et le contraster avec l'approche de tri *mauvais*.

---

Mise en œuvre du code

> Les trois extraits suivent la stratégie **fréquence-array** pour le temps `O(n)` et l'espace `O(max(nums)+3)`.

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<entier> trouverLonely(int[] nums) {
// Trouvez la valeur maximale pour tailler le tableau de fréquences.
= 0;
pour (int v : nombres) max = Math.max (max, v);

int[] freq = nouveau int[max + 3]; // +3 pour accéder en toute sécurité à v-1 et v+1

// Créer des fréquences.
pour (int v : nombres) {
freq[v]++; // Compter les événements.
}

Liste <Integer> solitaire = nouvelle liste <>();

// Vérifiez chaque numéro unique.
pour (int v : nombres) {
si (freq[v]) 1 && freq[v - 1] == 0 && freq[v + 1] == 0) {
Solitaire.add(v);
}
}

retourner seul;
}
}
«» "

> **Pourquoi `max + 3`? **
> Le tableau doit supporter les indices `v-1` et `v+1`. Ajout de 3 assure que nous n'avons jamais frappé `ArrayIndexOutOfBoundsException` même pour `v = max`.

---

- Oui. 2. Python

'`python
de taper l'importation Liste

Solution de classe:
def findLonely(self, nombres: List[int]) -> Liste[int]:
max_val = max(nums)
freq = [0] * (max_val + 3) # +3 pour un accès sécurisé v-1, v+1

pour v en chiffres:
freq[v] += 1

solitaire = []
pour v en chiffres:
si freq[v] == 1 et fréq[v - 1] == 0 et freq[v + 1] == 0:
solitaire.append(v)

retour solitaire
«» "

---

- Oui. 3. C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
std::vector<int> findLonely(std::vector<int>& nums) {
int maxVal = *std::max_element(nums.begin(), nums.end());
std::vector<int> freq(maxVal + 3, 0); // +3 pour v-1 et v+1

pour (int v : nombres) {
freq[v]++; // Compter chaque événement
}

std::vector<int> solitaire;
pour (int v : nombres) {
si (freq[v]) 1 && freq[v - 1] == 0 && freq[v + 1] == 0) {
solitaire.push_back(v);
}
}

retourner seul;
}
};
«» "

> Dans les trois langues, nous construisons d'abord une table de fréquence, puis nous balayons le tableau une fois de plus pour sélectionner les nombres isolés.

---

Les bons, les mauvais et les méchants

Autres Phase Ce que nous avons appris Pourquoi ça compte
-- -- -- -- -- -- -- --
**Le bon*** *Le tableau de fréquence* donne **le temps linéaire** ('O(n)') et un minimum de facteur constant. Fonctionne parfaitement lorsque le domaine d'entrée (`0‐106`) est délimité. Dans les entrevues, la sensibilisation aux contraintes d'entrée permet aux intervieweurs de voir que vous pouvez adapter des solutions. Autres
**Le mauvais*** *Trier* ("O(n log n)") est simple mais gaspillé pour ce problème. Il casse également lorsque les nombres dépassent la plage `int` ou lorsque vous êtes demandé pour l'espace `O(1)`. Autres
**L'Ugly**=S'appuyer sur un **HashMap** ou **unordered_map** fonctionne, mais vous pouvez oublier de gérer des cas de bord `-1` ou `+1`, conduisant à des bogues hors-de-l'échelle ou logiques. Beaucoup d'intervieweurs testent votre attention au détail; toujours valider les voisins et être prudent avec des indices de tableau. Autres

### TL;DR

- **Préférez le tableau de fréquences** chaque fois que la plage de valeurs est connue et petite.
- Évitez de trier à moins qu'il ne soit nécessaire (p. ex. pour un ordre de rupture de cravate).
- Double-vérifier les conditions des limites : `v-1` lorsque `v = 0`, et `v+1` lorsque `v = max(nums)`.

---

Analyse de complexité

Algorithme Temps Espace
- C'est quoi ?
Tableau de fréquence (nos) "O(max(nums)+3)" (1 e6)
"O(n)" Autres
Trier "O(n log n)" "O(1)" (en place)

> **Note pratique :**
> Même si le tableau de fréquences utilise environ 4 Mo pour `max = 1 e6`, qui est trivial sur les machines modernes et bien dans les limites de LeetCode.

---

Les dernières réflexions et conseils d'entrevue

1. **Demander des contraintes** tôt. Si l'intervieweur mentionne une plage délimitée, proposez immédiatement un tableau de fréquence.
2. ** Expliquez clairement la logique** : les occurrences de comte → vérifier les voisins → recueillir des nombres solitaires. (en milliers de dollars)
Les aides visuelles (comme une table simple) peuvent aider.
3. **Cas de sauvegarde**: tableau vide (non autorisé par les contraintes), élément unique, duplicata, limites (`0` et `max`).
4. **Test**: Effectuez un test de santé rapide (‘[1, 2, 3, 5, 7] → [5, 7]').
5. **Suivi** : Peut-on faire mieux dans l'espace ? La réponse: pas beaucoup; une carte de hachage nécessite un espace `O(n)`, alors que le tableau est déjà optimal étant donné le domaine d'entrée.

---

## -Référencement optimisé

Si vous vous préparez à une entrevue d'ingénierie logicielle, maîtrisez *LeetCode 2150 – Trouvez tous les numéros lunaires dans le tableau* démontre:

- Votre capacité à analyser les contraintes d'entrée et choisir une structure de données optimale.
- Votre compétence en Java, Python et C++.
- Votre capacité à expliquer les compromis algorithmiques (bon, mauvais, laid).

Gardez ce problème sur votre radar : c'est un favori d'interview classique qui teste à la fois la logique **de comptage des fréquences** et **de contrôle des voisins**. Bon codage !

---

*Sources : Problème officiel de LeetCode 2150, et solutions communautaires telles que celles de Subrata Jana et Kushal Bharadwaj. *