---
Titre: LeetCode 544.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# LeetCode 544 – *Contrôles de sortie*
C++ – Code complet, algorithme et interview-Ready Blog**

---

Récapitulation des problèmes

Vous avez des équipes **n** (n = 2^k, 1 ≤ k ≤ 12).
Les équipes sont classées 1 ... n (1 = le plus fort, n = le plus faible).

Au cours de chaque ronde, vous jumelez toujours l'équipe **la plus forte** avec l'équipe **la plus faible**:

«» "
Premier tour : (1,n), (2,n‐1), (3,n‐2), ...
Deuxième manche : gagnants de (1,n) vs gagnants de (n‐1,2), ...
...
«» "

La tâche : **Retourner le support complet en une seule chaîne** en utilisant les parenthèses, les virgules et les numéros d'équipe.

> Exemple
> `n = 4` → `"((1,4),(2,3))"`
> `n = 8` → `"((1,8),(4,5),((2,7),(3,6))"

---

L'idée de base

Le support est un arbre binaire parfaitement équilibré.
Si l'on divise récursivement l'ensemble des équipes en deux moitiés qui contiennent toujours les moitiés les plus faibles* et les plus fortes*, on peut construire la corde à partir des feuilles.

** Formule récursive**

«» "
build(l, r) = // l = indice de gauche (inclus), r = indice de droite (exclusif)
Si r - l == 1 // une équipe
retour de la chaîne(l+1)
Autre
m = (l + r) / 2
retour "(" + build(l, m) + "," + build(m, r) + ")"
«» "

Pour le premier appel `build(0, n)` nous obtenons le support final.
Cet algorithme fonctionne dans le temps **O(n)** et **O(log n)** profondeur de récursion (max 12), facilement en fonction des contraintes.

---

Code complet – 3 langues

> **Astuce:** Dans les interviews, vous êtes généralement autorisé à utiliser une récursion unique qui écrit directement à un `StringBuilder` / `list` / `stringstream` pour éviter la copie excessive de chaînes.

---

#### 3.1 Java

"Java
solution de classe {
public Chaîne trouverContestMatch(int n) {
StringBuilder sb = nouveau StringBuilder();
construction(sb, 0, n);
retour sb.toString();
}

construction privée de vide(StringBuilder sb, int l, int r) {
si (r - l) 1) { // feuille
sb.append(l + 1); // les numéros d'équipe commencent à partir de 1
retour;
}
int m = (l + r) / 2;
sb.annexe('(');
construction(sb, l, m);
sb.annexe(',');
construction(sb, m, r);
sb.annexe(')»;
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
def findContestMatch(self, n: int) -> str:
def build(l, r, out):
Si r - l == 1: # une équipe
out.append(str(l + 1))
retour
m = (l + r)/ 2
out.append(')
construire(l, m, out)
out.append(',')
build(m, r, out)
out.append(')')

out = []
build(0, n, out)
retour ''.join(out)
«» "

---

### 3.3 C++

'`cpp
solution de classe {
public:
chaîne findContestMatch(int n) {
la chaîne rés;
build(0, n, res);
retour rés;
}

particulier:
vide build(int l, int r, string &out) {
si (r - l) 1) { // une seule équipe
out += to_string(l + 1);
retour;
}
int m = (l + r) / 2;
sortie += '(';
construire(l, m, out);
sortie += ',';
build(m, r, out);
hors += ')';
}
};
«» "

---

Analyse de complexité

Métrique
- C'est quoi ?
Durée
Mémoire de la chaîne O(n) + O(log n) récursion

L'algorithme est linéaire dans le nombre d'équipes et utilise un espace supplémentaire négligeable (profondeur maximale 12).

---

C'est pas vrai. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Simplicité**La solution récursive est intuitive, pas de trucs de structure de données. Certains intervieweurs pourraient pénaliser la profondeur de récursion (bien que la profondeur soit ≤ 12). Sur-ingénierie : l'utilisation de files d'attente ou de bit-twiddling pour générer des appariements peut masquer la logique. Autres
**Readability** Java La liste `StringBuilder` et Python's peut sembler verbeuse pour les nouveaux venus. La manipulation de chaînes en place en C++ peut être sujette à erreur (surcharge de l'opérateur). Autres
**Performance** Le Python peut être un peu plus lent mais toujours dans les limites. Autres Toutes les langues fonctionnent bien; Python plus lentement sur les entrées massives (pas de souci ici). Autres
**Space**= Seulement nécessaire pour la chaîne finale et la pile. Aucun.

**Ce qu'il faut éviter *
- **Bitwise hacks** (comme la solution de LeetCode éditorial) qui fonctionnent mais sont cryptiques.
- ** Simulation itérative** qui scanne à plusieurs reprises le tableau pour trouver des paires – O(n2) et inutiles.
- **Logique de base codée en dur** qui ne généralise pas pour la non-puissance de deux entrées (bien que le problème garantisse 2^k).

---

## 6-

1. **Exposer l'arbre récursif** avant le codage. Montrez que chaque noeud représente une correspondance, et que les enfants sont les deux sous-combinaisons qui s'y nourrissent.
2. **Mention base case**: une seule équipe.
3. **Parler de la complexité**: temps O(n), profondeur de récursion O(log n).
4. **Afficher la version itérative** si demandé (utiliser une file d'attente ou une pile pour simuler des tours).
5. **Cas de bord de poignée**: `n = 2` → `(1,2)`; `n = 4096` convient à la pile de récursion.

---

Conclusion

Le problème LeetCode 544 est un exemple de manuel d'arbre binaire parfaitement équilibré.
Un simple algorithme récursif qui s'ajoute à un constructeur de chaînes / list / stream donne une solution propre, lisible et très efficace.

> **Traitement des clés:**
> *Considérez toujours le support comme un arbre binaire; la règle -vs-faible signifie simplement que vous divisez la gamme en deux à chaque tour. *

---

Mots clés & Mots clés

- LeetCode 544
- Matchs du concours de sortie
- Solution Java LeetCode
- Solution Python LeetCode
- Solution C++ LeetCode
- Problèmes de codage des entretiens
- Récursion de l'arbre binaire
- complexité temporelle O(n)
- Algorithme interview prep
- Entretien en génie logiciel

---

Essai rapide

'`python
# Python
((1,4),(2,3))
print(Solution().findContestMatch(8)) # ((1,8),(4,5)),(2,7))
«» "

Exécutez la même chose pour Java et C++ – les sorties correspondent aux résultats attendus.

Bon codage et bonne chance pour votre prochaine interview! C'est ce qu'il a dit