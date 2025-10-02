---
titre: LeetCode 2110. Nombre de périodes de descente en douceur d'un stock -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1=1 Aperçu du problème – LeetCode 2110
**Nombre de périodes de descente en douceur d'un stock* *
- **Difficulté:** Moyenne
- **Idée clé :** Compter chaque sous-tribunement contigu dont les éléments consécutifs tombent de **exactement 1**.
- **Input:** "int[] prices" – prix journaliers des actions (1 ≤ n ≤ 105).
- ** Sortie:** `long` – le nombre total de périodes de descente en douceur.

> Une période de longueur 1 est toujours valable; des périodes plus longues doivent satisfaire
> "prix [i‐1] - prix [i] == 1` pour tous `i` dans la période.

---

- Oui. Pourquoi ce problème est important
- **Algorithme Insight:** Reconnaît un problème classique de comptage.
- **Contexte de l'entrevue :** Apparaît dans LeetCode, et est un favori de nombreuses équipes d'embauche pour la structure de données + pensée gourmande.
- ** Analogie du monde réel:** Détecter les séquences qui diminuent strictement dans les données des séries chronologiques (p. ex., chute de stock, chute de température).

---

- Oui. La fenêtre de glissement simple / Encodage de la longueur d'exécution
- **O(n) temps, O(1) espace supplémentaire. **
- Gardez un compteur `len` pour l'exécution consécutive actuelle de la commande "drop‐by‐1=".
- Lorsque l'exécution s'interrompt, ajouter le nombre de sous-réseaux associés à l'exécution :
\[
\text{add} = \frac{\text{len} \times (\text{len}+1)} {2}
\]
- Oui. Après la boucle, ajoutez la contribution de la dernière manche.

- Oui. Pourquoi ça marche ?
Chaque sous-tribu qui se trouve entièrement à l'intérieur d'un parcours de longueur `len` est une période de descente valide.
La formule ci-dessus compte tous **sub-arrays contigus** d'une séquence de longueur `len` – exactement ce dont nous avons besoin.

---

- Oui. Le "Bad" – Force brute O(n2)
Bouclez sur tous les indices de départ, prolongez jusqu'à ce que la règle s'arrête, et comptez chaque sous-cours valide.
- Temps: \(O(n^2)\) - inacceptable pour \(n = 10^5\).
- Espace: \(O(1)\) – mais le coût du temps le tue.

---

C'est pas vrai. Les arbres "Ugly" – DP / Segment
Certaines solutions tentent une programmation dynamique ou des arbres segmentés, ajoutant une complexité inutile.
- **Sur-ingénierie:** DP traquerait la plus longue course se terminant à chaque position, mais la fenêtre coulissante le fait déjà dans un espace constant.
** Lire comme suit :** Plus de lignes de code, plus de risques de bugs.
- **Performance:** Toujours \(O(n)\) mais avec des facteurs constants plus lourds.

---

# # # 6 La solution propre (fenêtre coulissante)
Ci-dessous vous trouverez des implémentations entièrement commentées, prêtes à la production en **Java, Python et C++**. Tous utilisent la même idée décrite ci-dessus.

Type de retour Remarques
- C'est quoi ?
Java "public long getDescentPériodes(int[] prix)""
Python Def get_descent_periods(prices: List[int]) -> int: '= `int`=' Python='s int est non consolidé
"DescentePériodes(vecteur<int>& prix) ""long long"" 64-bit signé

---

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
***
* Compter les périodes de descente en douceur dans une gamme de prix des actions.
*
* @param prix gamme de prix quotidiens
* @retour nombre de périodes de descente en douceur (long pour éviter le débordement)
*/
public long getDescentPeriods(int[] prix) {
n = prix, longueur;
si (n == 0) retourner 0; // défensive (problème garanti n >= 1 )

long total = 0;
int runLen = 1; // longueur du courant de chute-par-1 consécutive

pour (int i = 1; i < n; i++) {
si (prix [i Prix 1) {
runLen++; // poursuivre l'exécution
} autre {
total += (long) runLen * (runLen + 1) / 2; // ajouter la contribution
runLen = 1; // réinitialiser pour l'exécution suivante
}
}

// ajouter la dernière exécution
total += (long) runLen * (runLen + 1) / 2;
le total des retours;
}

// ---- Principale option pour les tests manuels rapides -----
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.getDescentPériodes(nouvelle int[]{3, 2, 1, 4})); // 7
Système.out.println(sol.getDescentPériodes(nouvelle int[]{8, 6, 7, 7}); // 4
Système.out.println(sol.getDescentPériodes(nouvelle int[]{1}); // 1
}
}
«» "

---

6.2 Python

'`python
de taper l'importation Liste

def get_descent_periods(prix: Liste[int]) -> Int:
"""
Compter les périodes de descente en douceur dans une liste de prix.

Paramètres
- Oui.
prix : Liste[int]
Prix journalier des actions, 1 <= len(prix) <= 1e5

Retourne
- Oui.
Int
Nombre total de périodes de descente en douceur.
"""
n = len(prix)
si n] 0:
retour 0

Total = 0
run_len = 1 # longueur d'exécution courante

pour i dans la plage (1, n):
si les prix[i Prix 1 :
run_len += 1
Sinon:
total += run_len * (run_len + 1) // 2
run_len = 1

total += run_len * (run_len + 1) // 2
retour total

# ---- Test rapide facultatif ----
si __nom__ == "__main__" :
print(get_descent_périodes([3, 2, 1, 4])) # 7
print(get_descent_périodes([8, 6, 7, 7])) # 4
print(get_descent_périodes([1])) # 1
«» "

---

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
***
* @param prix vecteur des prix quotidiens des actions
* @retour nombre de périodes de descente lisses aussi longtemps
*/
longue durée getDescentPériodes(vecteur<int>& prix) {
int n = prix.taille();
si (n == 0) retour 0; // garde de sécurité

long total = 0;
int runLen = 1; // longueur d'exécution du courant

pour (int i = 1; i < n; ++i) {
si (prix [i-1] - prix [i]] 1) {
++runLen; // extension
} autre {
Total += 1LL * runLen * (runLen + 1) / 2; // ajouter contribution
runLen = 1; // lancer une nouvelle course
}
}

Total += 1LL * runLen * (runLen + 1) / 2; // dernier run
le total des retours;
}
};

// ----- Principale option pour les tests rapides -----
Int main() {
Solution sol;
<< sol.getDescentPériodes({3,2,1,4}) << endl; // 7
<< sol.getDescentPériodes({8,6,7,7}) << endl; // 4
Cout << sol.getDescentPériodes({1}) << enl; // 1
retour 0;
}
«» "

---

Article du blog – Le bon, le mauvais et le mauvais de LeetCode 2110

Titre
**LeetCode 2110 – Nombre de périodes de descente en douceur d'un stock : le bon, le mauvais et le mauvais**

> *Balises de référencement:*
> `Nombre de périodes de descente en douceur d'un stock`, `LeetCode 2110`, `périodes de descente en douceur`, `algorithme du prix du stock`, `DP vs Sliding Window`, `Java Python C++ solutions`, `questions d'entrevue sur la structure des données`.

---

7.1 Introduction

Si vous avez pratiqué sur LeetCode, vous allez tomber dans **Problème 2110 – Nombre de périodes de descente lisse d'un stock**. Au premier coup d'oeil, il ressemble à un simple problème de sous-réseaux de comptes, mais il enseigne en fait un truc soigné qui apparaît dans de nombreuses questions d'entrevue : *compte de la longueur d'exécution*. Dans ce post, nous allons disséquer le problème, discuter des pièges communs, et présenter une solution propre et prête à la production qui fonctionne en Java, Python et C++.

---

#### 7.2 Énoncé du problème (reformulé)

> On vous donne un tableau « prix » de longueur *n* (1 ≤ *n* ≤ 105).
> Une période de descente **smooth** est une sous-entente contiguë où le prix de chaque jour est **exactement 1 de moins** que le prix de la veille.
> Les sous-groupes de longueur 1 sont toujours admissibles.
> Retourner le nombre total de périodes de descente en douceur.

---

7.3 Exemple

Entrée Sortie Explication
C'est pas vrai.
Périodes d'un jour (4 d'entre elles) + périodes de 2 jours `[3,2]`, `[2,1]` + période de 3 jours `[3,2,1]` Autres
"[8, 6, 7, 7]"" "4"" Seulement des périodes d'un jour parce que "[8,6]" échoue la différence = règle de 1
Un seul élément trivial

---

7.4 La bonne – Fenêtre coulissante / Encodage de longueur d'exécution

La principale observation: **Si vous avez un parcours contigu de longueur `L` où chaque paire d'éléments consécutifs diffère de 1, alors chaque sous-cours à l'intérieur de ce parcours est valide**.
- Le nombre de sous-réseaux dans un parcours de longueur `L` est \(\frac{L(L+1)}{2}\).
- Oui. Il suffit de trouver chaque course maximale et d'ajouter le résultat de la formule.

**Étapes d'algorithme**

1. Initialiser «runLen = 1» et «total = 0».
2. Il faut passer du deuxième élément à la fin.
3. Si "prix[i-1] - prix[i] == 1`, augmenter "runLen".
4. Sinon (cours cassé):
- Ajouter `runLen * (runLen + 1) / 2` à `total`.
- Réinitialiser `runLen = 1`.
5. Après la boucle, ajoutez la contribution de la dernière manche.

**Pourquoi est-ce O(n)? * *
Nous ne numérisons le tableau qu'une seule fois; chaque opération dans la boucle est O(1).

**Espace?**
Seulement quelques variables entières – O(1).

---

#### 7.5 La mauvaise – Force brute O(n2)

Une approche naïve vérifie chaque sous-cours possible et vérifie la règle de la descente. Bien qu'il fonctionne pour de petites entrées, il devient rapidement invraisemblable pour *n* = 105:

- **Heure:** ~5 × 109 opérations → minutes ou heures.
- **Espace:** Toujours O(1), mais le simple temps a coûté la vie.

---

#### 7.6 L'Ugly – Sur-ingénierie (DP / Arbres de segments)

Certaines solutions mettent en œuvre une programmation dynamique ou un arbre de segments pour suivre la descente la plus longue se terminant à chaque indice.
- **Pour:** Toujours O(n).
- **Cons:** Ajoute ~20 lignes de code supplémentaires, plus de maux de tête débogants, et un facteur constant plus grand.
- **Résultat:** Plus difficile à maintenir, plus difficile à lire et n'offre aucun avantage sur la fenêtre coulissante.

---

### 7.7 Code de nettoyage final (Java / Python / C++)

(Voir les implémentations énumérées à la section 6 ci-dessus.)

*Astuce:* En Java et C++ utilisent 64-bit entiers (`long` / `long long`) pour se protéger contre le débordement; Python=s entiers sont arbitraire-précision, vous êtes donc sûr.

---

### 7.7 Que faire pour exercer Suivant

Une fois que vous maîtrisez le problème 2110, essayez ces variations:

- **LeetCode 1576 – Trouvez Min Flèche Vitesse pour frapper les cibles** (également la longueur de course).
- **La plus longue subséquence arithmétique** (généralise la règle de différence = 1).
- **Couvercle « good sub‐arrays » lorsque le produit est divisible par un nombre** (DP ou deux-pointeurs).

---

#### 7.8 Liste de contrôle à emporter

C'est pas vrai.
- Oui.
Autres Utilisez un seul balayage pour détecter les exécutions. Conserver `runLen` et ajouter \(\frac{L(L+1)}{2}\) pour chaque course. Autres
Retour `long` (Java/C++) ou `int` (Python). L'arithmétique 64 bits pour éviter le débordement. Surmoteur avec des arbres DP ou segment. Autres

---

7.9 Clôture

LeetCode 2110 est un micro-leçon dans *comptage efficace*. L'approche de la fenêtre coulissante est élégante, rapide et facile à mettre en œuvre dans toute langue majeure. Si vous préparez des interviews techniques, maîtriser ce modèle vous fera gagner du temps et impressionner les intervieweurs.

> **Vous voulez plus de conseils d'entrevue?** Abonnez-vous à ma newsletter pour les défis de codage hebdomadaires en Java, Python et C++.

---

7.10 Appel à l'action

> **Essayez le code vous-même!**
> Copiez l'implémentation pour votre langue préférée, exécutez les échantillons, puis testez sur des tableaux aléatoires pour voir la différence de performance.
> Bon codage !

---

- Oui. Mot final

- **LeetCode 2110** est un problème classique de comptage.
- Oui. La solution **sliding window** est la plus propre, la plus rapide et la plus durable.
- La suringénierie avec DP ou arbres est inutile; la formule mathématique simple vous donne déjà la réponse.

Si vous trouvez cet article utile, partagez-le sur LinkedIn ou Twitter et marquez vos autres codeurs. Bonne chance pour votre prochain entretien ! C'est ce qu'il a dit.

---

*Auteur:* [Votre nom] – Ingénieur logiciel principal et mentor de code.
*Contact:* `you@example.com`" `@votre main` sur Twitter

---

* Sentez libre de modifier le ton ou la structure de l'article pour convenir à votre marque personnelle. La partie la plus importante : les idées algorithmiques restent les mêmes. *