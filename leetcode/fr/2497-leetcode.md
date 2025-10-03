---
titre: LeetCode 2497. Somme maximum d'étoile d'un graphique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 2497
**Étoile maximale Somme d'un graphique**

*Nous avons un graphique non dirigé.
«vals[i]» – valeur du nœud 'i'.
`edges` – liste des bords non dirigés.
Un *star* est un sous-graphe qui a un nœud central et un certain nombre de ses bords incidents (tous partageant le même centre).
Pour un entier `k` nous voulons la somme maximum possible d'étoiles (somme de toutes les valeurs de nœuds qui apparaissent dans l'étoile) en utilisant **au plus `k` bords**. *

> **Input**
> `int[] vals, int[][] bords, int k`
> ** Sortie** – somme maximum de l'étoile

**Contrôles* *

1 ≤ n ≤ 105