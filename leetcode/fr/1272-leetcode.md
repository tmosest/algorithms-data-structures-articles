---
titre: LeetCode 1272. Supprimer l'intervalle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1272 – Supprimer l'intervalle
> **Java / Python / C++ Solutions + Blog
> *Le bon, le mauvais, et le laid – et pourquoi il vous poser un travail. *

---

TL;DR

Langue Heure Espace
- C'est quoi ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Python******O(N)****O(1)** (sortie non comptée)
* * * * * * * * *

Autres Les trois implémentations fonctionnent dans le temps linéaire, n'ont pas besoin de stockage supplémentaire, et sont triviales à lire – parfait pour une interview.

---

- Oui. 1. Récapitulation des problèmes

> **Supprimer l'intervalle**
> Une liste triée d'intervalles demi-ouverts *disjoint* décrit un ensemble de nombres réels.
> On vous donne un autre intervalle `à être retiré`.
> **Objectif:** Retourner l'ensemble après avoir supprimé `à être retiré` de chaque intervalle dans `intervalles`.
> Le résultat doit également être une liste triée des intervalles disjoints.

**Exemples**

Entrée Sortie
C'est quoi ?
"Intervalles = [[0,2],[3,4],[5,7]", "à supprimer = [1,6]" `[[0,1],[6,7]" Autres
«intervalles = [[0,5]]», «à supprimer = [2,3]«[[0,2],[3,5]» Autres
"intervalles = [[-5,-4],[-3,-2],[1,2],[3,5],[8,9]", "à supprimer = [-1,4]`"[[-5,-4],[-3,-2],[4,5],[8,9]" Autres

---

- Oui. 2. Pourquoi ce problème se pose pour les entrevues

Pourquoi ça compte ?
- Oui.
**Scannage linéaire**** Affiche que vous pouvez traiter les données triées en un seul passage. Autres
**Manipulation d'un boîtier d'Edge** Autres
**Space‐efficacity** Autres
**Multiple language support** Autres

---

- Oui. 3. L ' idée fondamentale

1. **Split chaque intervalle s'il se chevauche Être retiré.**
Parce que les intervalles sont * disjoints et triés*, il suffit de vérifier deux possibilités pour chacun :
* **La partie gauche** – la partie avant* `à être retirée' (le cas échéant).
* **La partie droite** – la partie *après* `S'il y a lieu'.

2. **Afficher le segment du milieu qui chevauche. **

3. **Collectez les pièces valides dans le même ordre. **

Puisque l'entrée est triée, nous pouvons simplement itérer une fois – **O(N)** temps.

---

- Oui. 4. Le Code (Java, Python, C++)

### 4.1 Java – Temps linéaire, Concise

"Java
Importation de java.util.*;

solution de classe {
liste publique<Liste<Intégrée>> supprimerInterval(int[][] intervalles, int[] à être retiré) {
début int = à être retiré[0];
int end = à être déplacé[1];
Liste <Liste<entier>> résultat = nouvelle liste <>();

pour (int[] intervalle : intervalles) {
// Côté gauche: [intervalle[0], min(intervalle[1], début)
si (intervalle[0] < début) {
result.add(Arrays.asList(intervalle[0], Math.min(intervalle[1], début)));
}

// Côté droit: [max(intervalle[0], fin), intervalle[1])
si (intervalle[1] > fin) {
résultat.add(Arrays.asList(Math.max(intervalle[0], fin), intervalle[1]);
}
}
le résultat du retour;
}
}
«» "

> **Pourquoi c'est génial**
> *Utilise uniquement la bibliothèque standard. *
> *Pas de frais généraux de construction. *
> *Toute logique reste dans une boucle. *

---

4.2 Python – uniligne, lisible

'`python
de taper l'importation Liste

Solution de classe:
def supprimer Intervalle(self, intervalles: Liste[List[int]], à être retiré: Liste[int]) -> Liste[List[int]]:
s, e = être déplacé
res = []

pour a, b par intervalles:
si < s: # partie gauche
Annexe([a, min(b, s)])
si b > e: # partie droite
Annexe([max(a, e), b])

retour res
«» "

> **Pourquoi c'est génial**
> *Pythonique, plaque de chaudière minimale. *
> * exprime directement la logique de gauche / droite. *

---

### 4.3 C++ – Moderne, sans OOP

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vector<vector<int>> supprimerInterval(vector<vector<int>>& intervals, vector<int>& toBeRemoving) {
int s = à être retiré[0], e = à être retiré[1];
vecteur<vecteur<int>> ans;

pour (const auto& iv : intervalles) {
Int a = iv[0], b = iv[1];

Si (a < s) // côté gauche
le nom de l'autorité compétente;

si (b > e) // côté droit
l'alinéa suivant est ajouté:
}
le retour des an;
}
};
«» "

> **Pourquoi c'est génial**
> *Utilise un «vecteur» et un «pour» basé sur la plage. *
> *Aucune mémoire dynamique au-delà du vecteur de sortie. *

---

- Oui. 5. Cas de bord et pièges (les voyous)

Pourquoi il peut échouer
Il n'y a pas de lien entre les deux.
La logique rejette automatiquement l'intervalle parce que `min(b,s)` ≤ `max(a,e)`. Pas besoin de changement de code. Autres
`toBeRemofted` commence ou se termine exactement sur une limite d'intervalle. Autres
Notre code renvoie simplement un vecteur/liste vide – correct. Autres
Un grand nombre (int superple) 109.Utilisez 64-bit (`long long`/`long`) si la langue le permet; LeetCode.Les contraintes s'adaptent dans 32-bit, donc nous sommes en sécurité. Autres

---

- Oui. 6. Analyse de la complexité

Mesure Java Python C++
C'est quoi, ça ?
**Heure**="O(N)" – un passage sur les "intervalles"="="O(N)="=" Autres
**Space**= `O(1)` extra – sortie non comptée= `O(1)`= `O(1)` Autres

*`N = intervalles.longueur`*.

---

- Oui. 7. Harnais d ' essai (exemple de python)

'`python
def test():
sol = Solution()
[[[0,2],[3,4],[5,7], [1,6]] ==[0,1],[6,7]]]
affirmer sol.removeInterval([[0,5]], [2,3]) ==[0,2],[3,5]]
affirmant sol.removeInterval([[-5,-4],[-3,-2],[1,2],[3,5],[8,9], [-1,4]) == [[-5,-4],[-3,-2],[4,5],[8,9]]
affirmant sol.removeInterval([[0,1]], [0,1]) == []
affirmant sol.removeInterval([[0,5],[6,10]], [2,7]==[0,2],[7,10]]
print("Tous les tests sont passés!")

essai()
«» "

---

- Oui. 8. Le bon, le mauvais, le mauvais

Catégorie de ce que vous obtenez Où vous pouvez briller
- C'est quoi ?
**Bon**=Linéaire, espace O(1); facile à raisonner; fonctionne pour tous les cas de bord. Autres
Aucun vraiment – l'algorithme est simple Faites attention à ne pas trop compliquer (p. ex. boucles inutiles de temps). Autres
Certains langages utilisent la syntaxe verbose (`Arrays.asList` en Java) Autres

---

- Oui. 9. SEO-Friendly à emporter

- **Mots clés**: `Supprimer l'intervalle`, `LeetCode 1272`, `Java solution`, `Python solution`, `C++ solution`, `problème de suppression d'intervalle`, `codage interview question`, `algorithm interview`, `job interview interview coding`, `disjoint intervals`.
- **Description détaillée**: Code du leet 1272 – Supprimer Interval en Java, Python et C++ avec code linéaire. Lire notre blog complet couvrant l'algorithme, les cas de bord et les conseils d'entrevue. (en milliers de dollars)

---

10. Pensées finales

Vous venez de maîtriser une question d'interview classique qui teste:

1. **Array traversant**
2. **Conditions limites**
3. **Efficacité spatiale**

Avec ces trois implémentations, vous pouvez répondre en toute confiance. N'oubliez pas de parler à travers la logique, de passer à travers les cas de bord, et de présenter la solution propre, linéaire-temps. Bonne chance pour ce travail de rêve ! C'est ce qu'il a dit.

---