---
titre: LeetCode 2236. Égal à la racine Somme des enfants
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2236 – Égales de racine Somme des enfants
> **Facile, ligne unique, 100 %** – Le démarreur d'interview parfait

---

Table des matières
1. [Pourquoi ce problème est-il un must-now](#pourquoi ce problème-est-un-savoir)
2. [Déclaration de problème (officielle)]
3. [Aperçu de la solution – Le bon, le mauvais, le mauvais] (#solution-overview)
4. [Applications de référence] (#applications de référence)
* Java
* Python
* C++
5. [Cas d'escroquerie et pièges communs]
6. [Analyse de la complexité] (#analyse de la complexité)
7. [Comment en parler dans une entrevue] (#comment parler à propos-il-dans-une-entrevue)
8. [FAQ et référence rapide] (#faq-quick-référence)
9. [Remplissage et retrait](#Remplissage et retrait)

> **SEO Mots-clés**: LeetCode Root Equals Sum of Children, Solution de Java, Solution de Python, Solution de C++, Problème de LeetCode facile, Question d'entretien d'arbre binaire, Conseils d'entretien de codage, Algorithme d'entretien d'emploi, Entretien d'ingénieur logiciel

---

## Pourquoi ce problème est un must-Know

**Beau**
C'est quoi ?
C'est vrai. Extrêmement simple – parfait pour un *warm-up* dans un entretien . . Les gens over-engineer: écrivez un traversal récursif ou une méthode d'aide qui n'est pas nécessaire .

Même les ingénieurs les plus expérimentés sont parfois tombés dessus. Être capable de répondre *en 1–2 lignes* démontre:

- Réflexion rapide
- Compréhension de la structure binaire des arbres
- Capacité de repérer les simplifications

---

## Déclaration de problème (officielle)

> **Root égale la somme des enfants* *
> **Difficulté:** Facile
> On vous donne la racine d'un arbre binaire qui contient exactement **trois nœuds** : la racine, son enfant gauche et son enfant droit.
> Retourner `true` si la valeur du nœud racine est égale à la somme des valeurs de ses deux enfants, sinon retourner `faux`.

**Contrôles* *

Valeur du paramètre
C'est quoi ?
Nombre de nœuds
`-100 <= Noeud.val <= 100 '
Autres L'arbre est *non-vide* et a *exactement* un enfant droit et gauche.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
"[10, 4, 6]" "vrai" "10 == 4 + 6"
"[5, 3, 1]" "faux"" "5 != 3 + 1

---

## Aperçu de la solution – Le bon, le mauvais, le mauvais

Bonne
- **Temps continu** Parce qu'on ne regarde que trois nœuds.
- ** Espace permanent** (`O(1)`).
- Oui. Aucune récursion ou fonction d'aide nécessaire.

Mauvais
- Beaucoup de gens écrivent une solution *generic* qui fonctionne pour n'importe quel arbre binaire, mais qui est inutile ici.
- Oui. Si vous oubliez de vous protéger contre les enfants `null` (bien que les contraintes garantissent leur existence), votre code s'écrasera.

# # # # Ugly
- Oui. Les contraintes du problème sont *très* spécifiques; une solution générique de "root‐equals‐sum" peut sembler trop sophistiquée et ne pas impressionner les intervieweurs qui s'attendent à ce que vous *optimisez*.

---

## Mise en œuvre des références

Autres **Les trois solutions sont de type monoligne. **
> Ajoutez quelques commentaires si vous les partagez dans une session de codage en direct.

### Java

"Java
***
* Définition d'un noeud d'arbre binaire.
* classe publique TreeNode {
* Int val;
* TreeNode gauche;
* TreeNode droit;
* TreeNode() {}
* TreeNode(int val) { this.val = val; }
* TreeNode(int val, TreeNode gauche, TreeNode droite) {
* ce.val = valeur;
* ce.gauche = gauche;
* ce droit = droit;
*}
*}
*/
solution de classe {
contrôle public du booléen Arbre(racine du node d'arbre) {
// L'arbre a toujours la racine, la gauche et la droite.
retour root.val == root.left.val + root.right.val;
}
}
«» "

Python

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

Solution de classe:
Contrôle Arbre(même, racine: TreeNode) -> bool:
# Simple et rapide – juste une comparaison
retour root.val == root.left.val + root.right.val
«» "

C++

'`cpp
***
* Définition d'un noeud d'arbre binaire.
* struct TreeNode {
* Int val;
* TreeNode * gauche;
* TreeNode *right;
* TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
* TreeNode(int x, TreeNode *l, TreeNode *r) : val(x), gauche(l), droite(r) {}
* };
*/
solution de classe {
public:
Contrôle des bools Arbre(racine TreeNode*) {
// Comparaison directe – O(1)
retour root->val == root->left->val + root->right->val;
}
};
«» "

---

## Cas de bord et pièges communs

Pourquoi ça arrive ?
- Oui.
`NullPointerException` / `AttributeError`. Null & & racine. droite != null` (pas nécessaire par contraintes mais sûr)
Autres Mauvaise préséance de l'opérateur.
Autres Retour du mauvais type Retourner un entier ou une chaîne au lieu de booléen Retourner `true/false` ou `True/False` explicitement

> **Conseil pro** – Si vous travaillez dans un environnement d'entrevue où les contraintes ne sont pas garanties, vous pouvez garder en toute sécurité:

"Java
si (racine) null. gauche == null=" root.right == null) retourner false;
«» "

---

Analyse de complexité

Valeur métrique
C'est pas vrai.
**Temps** **O(1)** – seulement trois accès
**Espace******O(1)** – aucune structure de données auxiliaire

---

Comment parler Dans une interview

1. **Déclarer les contraintes en premier**: L'arbre a exactement trois nœuds – racine, gauche, droite. (en milliers de dollars)
2. **Exposer l'observation** : Parce que nous avons toujours les deux enfants, nous n'avons pas besoin d'une traversée. (en milliers de dollars)
3. **Montrer la solution**: Il suffit de comparer `root.val` avec `root.left.val + root.right.val`. (en milliers de dollars)
4. **Complexité de l'action**: temps et espace. (en milliers de dollars)
5. **Demander des éclaircissements**: Si nous nous occupons du cas où un enfant manque?

---

## FAQ & Rapide Référence

Question Réponse
C'est pas vrai.
**Puis-je utiliser la récursion?**= Oui, mais il est inutile et ajoute des frais généraux. Autres
Autres **Et si l'arbre avait plus de nœuds?** Ensuite, vous auriez besoin d'une traversée (DFS/BFS) pour calculer les sommes. Autres
**Ce problème est-il souvent posé? En codant les entrevues pour les postes subalternes, oui. Autres
Autres **Comment gérer les enfants nuls dans Python?**= Utiliser `if root.left and root. Garde de droite. Autres
Autres **S'agit-il d'un problème de réchauffement ou de réchauffement?

---

## Wrap-Up & A emporter

- **Root Equals Sum of Children** est la définition d'une question d'entrevue de codage concise*.
- Oui. La solution optimale est un **one-liner** dans n'importe quelle langue.
- Savoir *reconnaître* que vous pouvez raccourcir une approche générique est une compétence clé dans les entrevues.
- Oui. Partagez l'extrait de code avec confiance ; il montre que vous pouvez repérer les motifs et optimiser rapidement.

Autres **Étape suivante:** Implémentez la solution dans votre langue préférée, ajoutez des tests unitaires et pratiquez l'expliquer à haute voix. Une réponse claire et rapide fera une grande première impression sur l'embauche des gestionnaires à la recherche de *solveurs de problèmes efficaces*.

Bon codage et bonne chance pour votre voyage d'entrevue!