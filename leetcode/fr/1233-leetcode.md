---
titre: LeetCode 1233. Supprimer les sous-dossiers du système de fichiers -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1233. Supprimer les sous-dossiers du système de fichiers
**Java • Python • C++** , **LeetCode** , **Interview-Ready**

> **TL;DR** – Triez les chemins par ordre alphabétique, conservez le premier dossier de chaque bloc et déposez n'importe quel dossier qui commence avec le précédent dossier conservé + .
> Complexité : **O(n log n)** temps, **O(n)** espace supplémentaire.

---

Table des matières

1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Jurisprudences d'intuition et de bord] (#Cours d'intuition et de bord)
3. [Solution de balayage triée par Gredy](#solution de balayage triée par Gredy)
4. [Mise en œuvre en trois langues] (#Mise en œuvre en trois langues)
- [Java] (#Java)
- [Python] (#python)
- [C++](#c++)
5. [Temps/Complexité spatiale] (#temps--complexité spatiale)
6. [Approches alternatives] (#approches alternatives)
7. [Pièges communs et FAQ](#pièges communs--faq)
8. [Pourquoi cela compte pour votre entrevue](#pourquoi-ce-questions-pour-votre-entrevue)

---

Récapitulation du problème

Vous avez une liste de chemins de dossiers absolus, par exemple.

Texte
dossier = ["/a", "/a/b", "/c/d", "/c/d/e", "/c/f"]
«» "

Retournez la liste après avoir supprimé *any* dossier qui est un **sous-dossier** d'un autre dossier dans la liste.
Un chemin `x` est un sous-dossier de `y` si:

1. `x` commence par `y` ** et**
2. le caractère immédiatement après `y` est un `'/'`.

L'ordre de la liste qui en résulte n'a pas d'importance.

---

## Cas d'intuition et de bord

* La longueur de chemin la plus longue possible est de 100 caractères – nous pouvons traiter chaque chaîne comme une chaîne Java/Python ou `std::string` en C++.
* Trier le tableau de manière lexicographique garantit qu'un dossier parent apparaît toujours *avant* l'un de ses sous-dossiers.
* Après tri, nous avons seulement besoin de comparer le chemin actuel avec le dossier **dernier** que nous avons décidé de conserver.
Si le chemin actuel commence par `dernier + '/', il s'agit d'un sous-dossier et peut être ignoré; sinon, nous l'ajoutons au résultat.
* Cas de bord à surveiller:
* Un dossier qui est un préfixe d'un autre mais **pas** un sous-dossier (par exemple `"/a"` vs `"/ab"`).
* Dupliquer les chemins – le problème garantit l'unicité, mais attention si vous adaptez le code.
* Des entrées très longues (4 × 104) – la solution doit être O(n log n) pour passer.

---

Solution de numérisation triée par Greedy

1. **Trier** le tableau des chemins de dossiers.
2. **Itérer** dans la liste triée.
3. Pour chaque dossier `curr`:
* Si la liste de résultats est vide → ajouter `curr`.
* Sinon, le dernier dossier de la liste de résultats.
* Si `curr` commence par `dernier + '/'` → skip `curr` (sous-dossier).
* Sinon ajouter "curr".

Parce que le tri des places de tous les enfants après leur parent, la comparaison avec seulement le dossier *dernier* conservé est suffisante.

---

## Mise en oeuvre en trois langues

Voici des implémentations propres et prêtes à la production pour Java, Python et C++.

### Java

"Java
Importation de java.util.*;

solution de classe {
liste publique<String> supprimerSous-dossiers(dossier String[]) {
//
les tableaux.sort(dossier);

Liste du résultat <String> = nouvelle liste de distribution<>();

// 2--Scanner et ne conserver que les dossiers de haut niveau
pour (Streenring curr : dossier) {
si (résultat estEmpty()) {
résultat.add(curr);
poursuivre;
}

Chaîne last = result.get(result.size() - 1);
// vérifier si curr est un sous-dossier du dernier
si (curr.démarre avec (dernier + "/")) {
continuer; // sauter sous-dossier
}
result.add(curr); // conserver un nouveau dossier de haut niveau
}
le résultat du retour;
}
}
«» "

*Heure*: `O(n log n) "
*Espace*: `O(n)` (pour la liste des résultats)

Python

'`python
de taper l'importation Liste

Solution de classe:
def supprimer Sous-dossiers(self, dossier: List[str]) -> List[str]:
N° 1 Tri lexicographiquement
dossier.sort()

res = []

N° 2 Balayage de l'avidité
pour cur dans le dossier & #160;:
si non rés:
res.append(cur)
poursuivre

dernier = res[-1]
# sous-dossier si cur commence par le dernier + '/ '
si cur. commence avec (dernier + "/"):
poursuivre
res.append(cur)

retour res
«» "

C++

'`cpp
#incluez <vecteur>
#incluez <string>
#incluez <algorithme>

solution de classe {
public:
md::vecteur<std::chaîne> removeSubfolders(std::vector<std::string>& dossier) {
//
std::sort(folder.begin(), dossier.end());

md::vecteur<std::chaîne> rés;

pour (const std::string& cur : dossier) {
si (res.vide()) {
res.push_back(cur);
poursuivre;
}

const std::string& last = res.back();
// Sous-dossier de vérification
si (cur.size() > last.size() &&
cur.compare(0, last.size(), last) == 0 &&
[dernier.size()] == '/') {
continuer; // sauter
}
res.push_back(cur); // conserver
}
retour rés;
}
};
«» "

---

## Complexité temps/espace

Opération Temps Espace
- C'est quoi ?
Tri de **O(n log n)**
Détection **O(n)**

Total : **O(n log n)** temps, **O(n)** espace auxiliaire.

---

Autres approches

Démarche
C'est quoi ?
**Trie** (arborescence préfixe)
**Hash Set + Parent Check**
**Désormais + empilé**

Le scan trié est le plus propre pour les paramètres d'entrevue.

---

## Pièges communs & FAQ

Question Réponse
C'est pas vrai.
*Le sous-dossier ""/a" est-il en conflit avec ""/ab"?*Le sous-dossier ""/a" est **non** parce que le caractère après ""/a" n'est pas "/"". Le code utilise correctement `startsWith(dernier + "/")`. Autres
*Et si la liste ne contient qu'un seul dossier? L'algorithme fonctionne toujours : le résultat contiendra ce dossier unique. Autres
*L'ordre de la liste retournée est-il important? Non – LeetCode accepte toute commande. L'algorithme préserve l'ordre trié, ce qui est bien. Autres
*Pouvons-nous utiliser un `HashSet` pour débusquer? Le problème garantit l'unicité, donc un ensemble n'est pas nécessaire. Autres
*Qu'en est-il des limites de mémoire? espace supplémentaire est acceptable pour `n ≤ 4×104`. Autres

---

Pourquoi cela compte pour votre entrevue

1. **Simplicité** – Un scan trié en deux étapes est facile à expliquer et à implémenter, réduisant ainsi les risques de bogues.
2. **Sensibilisation générale** – Démontrer que vous considérez les compromis temps/espace montre la maturité.
3. **Edge‐Case Thinking** – Manipulation `"/a"` vs `"/ab"` démontre une manipulation attentive des chaînes.
4. ** Flexibilité linguistique** – Connaître le même algorithme en Java, Python et C++ prouve que vous êtes à l'aise à travers les piles, un plus pour de nombreux gestionnaires d'embauche.

> *Rappelez-vous*: Les intervieweurs apprécient souvent **clarité** sur l'intelligence. Une solution triée qui fonctionne dans `O(n log n)` et est simple à lire est souvent le meilleur choix.

---

## SEO – Sommaire optimisé

- **Mots-clés**: *code 1233*, *supprimer les sous-dossiers*, *algorithme de numérisation trié*, *solution Java/Python/C++*, *codage d'entrevue*, *conseils d'entrevue en génie logiciel*, *question d'entrevue d'algorithme*, *codage d'entrevue d'emploi*.
- **Description détaillée**: Apprendre à résoudre le LeetCode 1233 – Supprimer les sous-dossiers du système de fichiers – avec le code Java, Python et C++ propre. Comprendre l'algorithme trié, la complexité temporelle, les cas de bord, et pourquoi c'est un choix idéal pour les entrevues d'ingénierie logicielle. (en milliers de dollars)

---

Bon codage, et bonne chance de clouer cette prochaine interview!