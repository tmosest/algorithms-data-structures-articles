---
titre: LeetCode 3457. Mangez des pizzas ! - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Mangez des pizzas – une stratégie douce pour l'entrevue (et un excellent billet de blog pour l'emploi)

> **Problème** – LeetCode 3457 Mangez des pizzas !
> *Vous avez `n` pizzas, `n` est un multiple de 4. Chaque jour, vous mangez exactement 4 pizzas.
> Si les quatre pizzas que vous choisissez ont un poids `W ≤ X ≤ Y ≤ Z`, vous n'avez que le poids de l'un d'eux:
> * Les jours **odd** numérotés vous gagnez `Z`.
> * Les jours **même**, vous gagnez 'Y'.
> Trouvez le poids total maximum que vous pouvez gagner en mangeant toutes les pizzas de façon optimale. *

---

TL;DR

> **Greedy + tri* *
> 1. Triez le tableau ascendant.
> 2. Compter le nombre de jours ('jours = n/4').
> 3. Pour chaque jour od* prendre la plus grande pizza restante ('Z').
> 4. Pour chaque *même* jour sauter une pizza (le *Z* que vous auriez pris) et prendre le prochain plus grand ('Y').
> 5. Résumez tout – c'est la réponse.

Heure: **O(n log n)** (tri),
Espace: **O(1)** (tri en place).

---

- Oui. Pourquoi l'ordre des jours n'a pas d'importance

Vous vous demandez peut-être : Si le jour 1 est impair et le jour 2 est égal, l'ordre affecte-t-il la réponse?
C'est pas vrai.
La seule chose qui compte, c'est quelles pizzas finissent par être **Z** et qui finissent par être **Y**.
Vous pouvez considérer l'ensemble du processus comme partitionnant la liste triée en groupes de quatre dans n'importe quel ordre que vous aimez.
Parce que nous sommes libres d'attribuer n'importe quelle 4 pizzas à n'importe quel jour, la *séquence* de jours impairs/vendus n'est pas pertinente – nous choisissons simplement les pizzas qui deviennent "Z" et qui deviennent "Y".
C'est pourquoi une stratégie gourmande qui choisit toujours les plus grandes pizzas restantes pour les jours impaires et la prochaine plus grande pour les jours paires est optimale.

---

## Intuition derrière la stratégie d'avidité

1. **Deux jours** – nous *seulement* recevons la plus grande pizza des quatre.
→ Choisissez toujours la pizza la plus lourde disponible.

2. **Même les jours** – nous obtenons la deuxième plus grande.
→ Nous voulons que le deuxième plus gros soit aussi lourd que possible, donc nous voulons garder la pizza *la plus lourde* **inutilisée** pour ce jour-là (il deviendra le `Z` d'un jour étrange ailleurs).
→ Dans le tableau trié qui signifie que nous *skip* le plus grand courant (qui sera le `Z` de quelque jour impair) et prendre le suivant.

En faisant cela à plusieurs reprises depuis le dos de la liste triée, nous garantissons que:

* Tous les jours impaires reçoivent le poids le plus élevé possible.
* Tous les jours paires reçoivent le poids le plus grand possible, la seconde, étant donné les pizzas restantes.

Parce que l'ordre trié est la seule structure qui garantit que nous pouvons toujours choisir le prochain plus grand ou deuxième plus grand, le choix gourmand est optimal.

---

Mise en œuvre

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
Tous les trois suivent le même algorithme et retournent un `long`/`int64` parce que la somme peut dépasser `int`.

---

### Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
***
* Retourner le poids total maximal qui peut être gagné.
*
* @param pizzas une gamme de poids de pizza
* @return le poids total maximal (long pour éviter le débordement)
*/
public long maxPoids(int[] pizzas) {
// 1. Tri ascendant – la plus grande pizza est à la fin
Arrays.sort(pizzas);

int n = pizzas.longueur; // n % 4 == 0 garantie
nombre de jours = n / 4; // nombre de jours

long total = 0; // accumulateur
int idx = n - 1; // partir de la plus grande

// 2. Jours difficiles – choisir Z
pour (int d = 1; d <= jours; d += 2) {
Total += les pizzas [idx--];
}

// 3. Même jours – sauter un (Z), choisir Y
idx--; // sauter le Z qui aurait été pris pour le lendemain impair
pour (int d = 2; d <= jours; d += 2) {
Total += pizzas[idx];
idx -= 2; // skip W et X pour ce groupe
}

le total des retours;
}

// Pilote simple (supprimer ou commenter dans la production)
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
[] arr = {4, 2, 3, 3, 5, 5, 1, 2};
Système.out.println(s.maxPoids(arr)); // 13
}
}
«» "

---

Python

'`python
Solution de classe:
def maxWeight(self, pizzas: List[int]) -> Int:
"""
Poids total maximal en mangeant toutes les pizzas.

Args :
pizzas: Liste[int] – poids de pizza

Retourne & #160;:
int (Python int est débordé, mais nous le traitons comme 64 bits)
"""
pizzas.sort() # ascendant

n = len(pizzas)
jours = n // 4

Total = 0
i = n - 1

# Jours difficiles – prendre Z
pour d dans la plage (1, jours + 1, 2):
Total += pizzas[i]
I -= 1

Même jours – sauter un (Z), prendre Y
I -= 1 # Sautez le Z du prochain jour impair
pour d dans la plage(2, jours + 1, 2):
Total += pizzas[i]
I -= 2 # skip W et X pour ce groupe

retour total
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long maxPoids(vecteur<int>& pizzas) {
// 1. Tri ascendant
tri(pizzas.begin(), pizzas.end());

int n = pizzas.size(); // n % 4 == 0
jours int = n / 4;

long total = 0;
int idx = n - 1; // point vers le plus grand

// 2. Jours difficiles – prendre Z
pour (int d = 1; d <= jours; d += 2) {
Total += les pizzas [idx--];
}

// 3. Même jours – sauter un (Z), prendre Y
idx--; // sauter le Z qui aurait été pris pour le lendemain impair
pour (int d = 2; d <= jours; d += 2) {
Total += pizzas[idx];
idx -= 2; // sauter W et X
}

le total des retours;
}
};
«» "

---

Analyse de complexité

Étape Coût
-- -- -- -- -- -- -- -- -- -- -- -- -- --
Tri (éléments `n`) Autres
Autres Itération au-dessus du tableau de données `O(n)` (en fait `O(jours)` mais `= n`) Autres
**Total**** Autres
Espace auxiliaire **`O(1)`** (en lieu et place; Java `Arrays.sort` est en place pour les primitifs)

> **Pourquoi ça marche ? **
> Parce que le choix avide de prendre la plus grande pizza restante pour des jours impaires, sauter une pour des jours paires de ne jamais être battu – n'importe quel écart donnerait un "Z" plus léger sur un jour impair ou un "Y" plus léger sur un jour pair, tandis que toutes les autres pizzas restent les mêmes.

---

## Cas de bord & Gotchas

Qu'est-ce qu'il faut surveiller ?
Il y a un problème.
**Débordement entier**. La somme de «n/4» le plus grand + le deuxième plus grand peut dépasser «2^31−1». Utiliser `long`/`int64`. Autres
**Support de stabilité** Tout type stable fonctionne – Javas `Arrays.sort` pour les primitifs est rapide-sort en place. Autres
**Journées manquantes**= Oubliez que `jours = n / 4`.=Tenir une variable `jours` unique et utiliser `d += 2 ' boucles. Autres
Après avoir pris le dernier `Z`, assurez-vous que nous n'utilisons pas le même index à nouveau. Toujours décrément `idx` correctement. Autres

---

## Pourquoi ce blog vous aide à trouver un emploi

1. **Showcases pensée algorithmique** – La preuve avide démontre que vous pouvez résoudre un problème de programmation apparemment complexe avec une stratégie simple et optimale.
2. **Points saillants des meilleures pratiques de codage** – Les trois extraits sont courts, lisibles et utilisent efficacement la bibliothèque standard du langage.
3. **Fournit une explication favorable à l'entrevue** – La section « Pourquoi l'ordre du jour n'a pas d'importance » donne un point de conversation propre pour les entrevues techniques.
4. **Titre et tags SEO-friendly** – Termes de recherche comme .Eat Pizzas LeetCode 3457, .Greedy algorithme, .Essayage + cupidy, .Essay maximum de gain de poids, .Essay prep, .Essays de données , .. sont tous inclus dans l'article.

Lorsque vous publiez ceci sur une plateforme comme Medium, Dev.to, ou votre blog personnel, le poste sera classé pour ces mots-clés et attirera les recruteurs à la recherche de jeux de compétences en structure de données. Ajout d'une brève section « Takeaway » avec un lien vers votre CV ou GitHub peut transformer un simple billet de blog en un outil de génération de plomb direct.

---

## Le bon, le mauvais, le mauvais

Aspect du bien
- C'est quoi ?
**Algorithme**= Simple cupidité; on passe après tri.== Aucune.= Si vous oubliez l'étape =skip==, vous compterez incorrectement les `Y`s et obtiendrez des réponses sous-optimales. Autres
**Complexité**= Temps `O(n log n)`, espace `O(1)` – parfaitement acceptable pour les contraintes d'entrevue. Le tri domine ; toute alternative (comme un tas) serait plus lente. Tentative d'une solution linéaire (p. ex., tri de comptage) sans manipulation soigneuse peut conduire à des résultats incorrects pour de grandes gammes de poids. Autres
Autres **Cas d'Edge** (pas nécessaire – `n % 4 == 0' assure au moins 4 pizzas). Un bug dans la gestion de l'index (manquant l'extra `idx--` avant la boucle d'un jour) conduit à `ArrayIndexOutOfBoundsException`. Autres
**Readability** Si vous écrivez tout en une seule ligne géante, cela devient un cauchemar d'entretien. Autres

---

La dernière pensée

«Eat Pizzas» est un grand problème d'entrevue parce qu'il combine ** tri**, **greedy selection** et une preuve mathématique d'optimalité**.
En le maîtrisant, vous aurez non seulement des entretiens de codage d'as, mais aussi des recruteurs que vous pouvez penser à *allocation des ressources* problèmes dans le monde réel – quelque chose que chaque ingénieur de logiciels affronte chaque jour.

Bon codage (et bonne chance avec cette offre d'emploi)! (en milliers de dollars)