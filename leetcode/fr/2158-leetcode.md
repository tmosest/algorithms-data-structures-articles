---
titre: LeetCode 2158. Quantité de nouvelle surface peinte chaque jour -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2158 – *Montant de nouvelle surface peinte chaque jour*
**LeetCode Solution d'entrevue en Java, Python et C++**

> Vous souhaitez montrer aux recruteurs que vous pouvez résoudre un problème *hard* LeetCode dans **O(n log n)** time?
> Voici une implémentation propre, prête à la production, un algorithme étape par étape et un article prêt à bloguer que vous pouvez copier dans Medium, Dev.to ou votre portfolio personnel.

---

Table des matières

Ce que vous apprendrez
- Oui.
Description du problème Le défi exact du LeetCode
Exemples
Limites de taille et implications
Description de la solution Pourquoi un `TreeMap` / `map` fonctionne
Algorithme Intervalles de fusion + calcul de la nouvelle zone Autres
Code en trois langues
Temps et complexité spatiale O analyse
Des choses qui font monter les gens
SEO & Career Tips Des mots clés, comment présenter ça sur un CV
Appel à l'action

---

Déclaration du problème

> **LeetCode 2158** – *Montant de nouvelle surface peinte chaque jour*
> On vous donne une liste `pain` où `paint[i] = [start_i, end_i]`.
> Le jour `i` vous peignez le segment `[start_i, end_i)` d'une toile 1-dimensionnelle.
> La peinture de la même zone à plusieurs reprises est un gaspillage; vous ne voulez compter que la zone *nouvelle* peinte chaque jour.
> Retourner un tableau `log` où `log[i]` est la quantité de nouvelle zone peinte le jour `i`.

Entrée

Variable Type Contraintes
- C'est quoi ?
"peinture" "int[]" "1 ≤ n ≤ 105", "0 ≤ start_i "end_i ≤ 5·104" Autres

Sortie

Variable Type Signification
- C'est quoi ?
"worklog" "int[]" Nouvelle zone peinte chaque jour

---

Exemples de cas

Entrée Sortie Explication
C'est pas vrai.
`[1,4],[4,7],[5,8]`" `[3,31]`" Jour 0 peintures 1 à 4 → 3 unités. Jour 1 peinture 4-7 → 3 unités. Jour 2 peintures 5‐8, mais 5‐7 était déjà peint → seulement une unité est nouvelle. Autres
La même logique, l'ordre compte. Autres
Jour 0 peintures 1 à 5 → 4 unités. Jour 1'intervalle est entièrement à l'intérieur du jour 0's région peinte → 0 nouvelles unités. Autres

---

Les contraintes

* `peint.longueur` peut être aussi grand que `105`.
* `end_i` ne dépasse jamais `5·104`, mais nous ne pouvons pas compter sur une petite plage de coordonnées parce que l'algorithme doit gérer efficacement *toute* grande valeur.
* Un scan naïf *O(n2)* est beaucoup trop lent.

---

Aperçu de la solution

Le point de vue clé :
**Gardez une BST équilibrée des intervalles peints *disjoints*. **
Quand un nouvel intervalle `[l, r)` arrive, nous:

1. **Trouver tous les intervalles de chevauchement** dans la TVB.
2. **Soustraire** les longueurs de chevauchement de la nouvelle longueur d'intervalle pour obtenir la zone *nouvelle*.
3. **Merge** tous les intervalles de chevauchement (plus le nouveau) dans un seul intervalle et insère-le en arrière.

Une `TreeMap` (`Java`), `std::map` (`C++`), ou une `map` de début → fin (`Python`) nous donne *O(log m)* recherche/insérer où `m` est le nombre actuel d'intervalles peints.
Puisque chaque intervalle est fusionné au plus une fois, la complexité totale est "O(n log n)".

---

L'algorithme

«» "
peint = carte ordonnée vide (key=start, value=end)
res = tableau de longueur n

pour chaque jour i:
l, r = peinture[i]
newLen = r - l

// 1) Fusionner tous les intervalles qui se croisent [l, r)
pendant qu'il y a un intervalle [s, e) dans la peinture avec s ≤ r et e ≥ l:
// Recoupement : soustraire le chevauchement
NouveauLen -= min(r, e) - max(l, s)
// prolonger le nouvel intervalle pour couvrir le syndicat
l = min(l, s)
r = max(r, e)
// supprimer l'ancien intervalle; il sera remplacé
supprimer [s, e) de la peinture

// 2) Enregistrer une nouvelle zone
res[i] = nouveauLen

// 3) Insérer l'intervalle fusionné retour
peint[l] = r
«» "

*La boucle "While" se termine toujours parce que chaque itération supprime un intervalle existant et n'ajoute jamais plus. *

---

Code en trois langues

Voici les solutions **complètes, prêtes à coller** dans **Java**, **Python** et **C++**.
Tous les trois utilisent la même idée algorithmique mais s'adaptent à leurs structures de données natives.

> **Conseil:**
> • En Java, vous aurez besoin de `java.util. Carte des arbres.
> • Dans C++, utilisez `std::map<int,int>`.
> • Dans Python, la bibliothèque standard a `bisect`, mais pour plus de clarté, nous utilisons `conteneurs triés`.
> Si vous n'avez pas ce paquet, vous pouvez revenir à une liste + bisect.

---

### Java

"Java
Importation de java.util.*;

solution de classe {
// O(n log n) temps, O(m) espace
quantité de peinture(int[][] peinture) {
int n = longueur de la peinture;
int[] res = nouvelle int[n];
TreeMap<entier, entier> peint = nouveau TreeMap<>();

pour (int i = 0; i < n; ++i) {
int l = peinture[i][0];
int r = peinture[i][1];
int newLen = r - l;

// Trouver le premier intervalle avec le début <= r
Clé entière = peint.clef(l);
pendant que (clé != null) {
int s = clé;
int e = peint.get(s);

si (e <= l) { // aucun chevauchement
clé = peint.lowerKey(clé);
poursuivre;
}

// Le chevauchement existe
newLen -= Math.min(r, e) - Math.max(l, s);
l = Math.min(l, s);
r = Math.max(r, e);

// Supprimer l'intervalle de fusion
peinture.supprimer;
key = peint.floorKey(l);
}

// Après fusion tous les chevauchements
res[i] = nouveauLen;
la valeur de l'unité de mesure,
}
retour rés;
}
}
«» "

---

Python

'`python
de bisect importer bisect_left, bisect_right

Solution de classe:
# O(n log n) temps, O(m) espace
def quantityPeinted(self, paint: list[list[int]]) -> list[int]:
n = len(peinture)
res = [0] * n
# Utilisez deux listes parallèles : début et fin
commence, se termine = [], []

pour i, l, r dans l'énumération (peinture):
Nouveau_len = r - l

# Trouvez le premier intervalle qui peut se chevaucher
idx = bisect_right(démarrages, l) - 1
pendant que idx >= 0 et se termine[idx] > l:
s, e = début[idx], fin[idx]
Survol
new_len -= min(r, e) - max(l, s)
l = min(l, s)
r = max(r, e)
# Supprimer cet intervalle
commence.pop(idx)
fin.pop(idx)
idx -= 1

# Fusionner tous les intervalles qui commencent dans [l, r)
idx = bisect_left (démarrages, l)
pendant que idx < len(démarre) et commence[idx] < r:
s, e = début[idx], fin[idx]
new_len -= min(r, e) - max(l, s)
l = min(l, s)
r = max(r, e)
commence.pop(idx)
fin.pop(idx)

res[i] = nouveau_len
# Insérer l'intervalle fusionné
idx = bisect_left (démarrages, l)
début.insérer(idx, l)
fin.insérer(idx, r)

retour res
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> quantitéPeinte(vecteur<vecteur<int>>& peinture) {
int n = peinture.taille();
vecteur<int> res(n);
carte <int,int> peinte; // début -> fin

pour (int i = 0; i < n; ++i) {
int l = peinture[i][0];
int r = peinture[i][1];
int newLen = r - l;

// Trouver l'intervalle avec le plus grand démarrage <= l
auto it = peint.upper_bound(l);
si (it != peint.degin() --it;

pendant que (it != paint.end() && it->first <= r && it->second > l) {
int s = it->premier, e = it->seconde;
newLen -= min(r, e) - max(l, s);
l = min(l, s);
r = max(r, e);
auto toErase = it++;
peinture.erase(àErase);
}

res[i] = nouveauLen;
peint[l] = r; // insérer l'intervalle fusionné
}
retour rés;
}
};
«» "

> **Note :**
> Si vous utilisez Python sur une plateforme sans solutions basées sur «bisect», vous pouvez simplement installer des «conteneurs triés»:

"""
pip installer triés conteneurs
«» "

Ensuite, remplacez l'approche à deux listes par un `SortedDict` (début → fin) – cela fonctionne exactement comme la version Java `TreeMap`.

---

La complexité temporelle et spatiale

Langue Heure Espace
- C'est quoi ?
**O(m)** – `m` est le nombre d'intervalles peints * disjoints* (= n). Autres
Python **O(n log n)** (bisect + liste effacer)
C++. **O(n log n)** (voir la carte et effacer)

*Pourquoi `m` ≤ n? *
Chaque jour peut ajouter au plus un nouvel intervalle, et chaque fusion supprime au moins un ancien intervalle.
Par conséquent, à tout moment, nous n'avons jamais plus d'intervalles "n".

---

Pièges communs

Pourquoi il casse
C'est pas vrai.
**Utiliser une `list` et scanner tous les intervalles**= `O(n2)` – trop lent.= Utiliser une structure *ordered* (`TreeMap` / `map`). Autres
**Soustraire seulement de `r-l` une fois**. Autres
**Ne pas supprimer les intervalles fusionnés** Supprimer chaque intervalle de chevauchement dans la boucle. Autres
**Affaire Edge '[l, l]'** Espace de l'intervalle vide → 0. L'algorithme le gère naturellement ('newLen = 0'). Autres
**Python `bisect` off‐by‐one** Testez attentivement avec `bisect_left`/`bisect_right` ; le code ci-dessus montre les deux extrémités. Autres

---

## OBJECTIFS ET CONSEILS DE Carrière

Mot-clé Comment l'utiliser
C'est quoi ?
Dans votre curriculum vitæ: LeetCode 2158 (Hard) – 100% correct. Autres
Dans un billet de blog ou une interview : - Implemented a disjoint-interval BST for optimum time. Autres
*TreeMap / std::map*= Démontre la connaissance des arbres équilibrés. Autres
*O(n log n) algorithme Ça montre que vous pouvez raisonner sur l'asymptotique. Autres

**Montrer sur votre CV**

Texte
- Mise en œuvre d'un problème de LeetCode dur (2158 – Nombre de nouvelles surfaces peintes chaque jour) en <O(n log n)> temps.
- Utilisé une BST équilibrée (TreeMap / std::map) pour maintenir les intervalles de peinture.
- Démontré de solides compétences en résolution de problèmes et en structure de données.
«» "

**Posez-le sur Medium / Dev.to**

- Copiez la section *blog* ci-dessous.
- Marquez-le avec `#LeetCode`, `#Algorithm`, `#Java`, `#Python`, "#C++".
- Ajoutez une courte vidéo (ou GIF) qui traverse les 3 premiers cas de test.

---

Appel à l'action

1. **Run le code sur LeetCode.**
Vérifier que l'implémentation `O(n log n)` passe tous les tests cachés.

2. **Ajouter la solution à votre portefeuille.**
Texte
- LeetCode résolu 2158 – Quantité de nouvelle surface peinte chaque jour (Hard)
- Langues: Java, Python, C++
- Algorithme: TB équilibrée des intervalles disjoints
- Complexité: temps O(n log n), espace O(m)
«» "

3. **Publier un billet de blog. **
Utilisez l'article ci-dessous (ou l'adapter) et incluez un lien vers votre repo GitHub.

4. **La pratique de l'entrevue.**
Demandez à un ami ou à un mentor de simuler une entrevue de tableau blanc où vous expliquez l'algorithme *sans* regarder le code.

---

Article prêt à imprimer (copie-coller dans Medium / Dev.to)

> **Titre**: *Code de leet 2158 – Montant de la nouvelle surface peinte chaque jour – O(n log n) Solution en Java, Python et C++ *
> **Tags**: #LeetCode #Hard #Interview #Algorithmes #Java #Python #C++

```markdown
# 2158 – *Montant de nouvelle surface peinte chaque jour*
**LeetCode Hard – O(n log n) Solution en Java, Python & C++**

> Vous voulez impressionner les recruteurs avec un problème de LeetCode dur ?
> Voici une implémentation propre et prête à la production en trois langues, ainsi qu'une plongée profonde dans l'algorithme.

## Déclaration du problème
> (copier la déclaration complète de la section Déclaration du problème)

- Oui. Exemples de cas
> (copier le tableau de l'échantillon)

Aperçu de l'algorithme
> (copiez le paragraphe Aperçu de la solution)

## Étape par étape
> (copie le diagramme de l'algorithme)

Code

### Java
> (coller le bloc de code Java)

Python
> (coller le bloc de code Python)

C++
> (coller le bloc de code C++)

Analyse de complexité
> (copier la section de complexité)

Pièges communs
> (copiez la section des pièges)

## SEO & Boost carrière
> (copiez la section sur le référencement et les conseils professionnels)

---

«» "

N'hésitez pas à modifier le ton, à ajouter vos propres anecdotes ou à insérer un court **vidéo demo**.

---

Appel à l'action

1. **Soumettre** la solution sur LeetCode et regarder apparaître l'insigne .
2. **Ajoutez-le à votre GitHub** avec un README qui reflète cet article.
3. **Tweet** a short ##LeetCodeHard #Java #Python #C++.
4. **Préparer pour les entrevues** – vous avez maintenant un exemple solide et prêt à l'essai que vous pouvez expliquer en moins de 5 minutes.

Bonne chance, et le codage heureux! C'est ce qu'il a dit