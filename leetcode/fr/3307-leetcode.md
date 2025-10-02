---
titre: LeetCode 3307. Trouvez le personnage K-th dans le jeu de chaînes II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3307 – Trouvez le personnage K-th dans le jeu de cordes II
*Une solution complète, prête à l'interview en Java, Python & C++ + un blog convivial pour les développeurs*

---

Table des matières
1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Intuition et principale conclusion] (#intuition)
3. (#algorithme)
4. [Complexité temporelle et spatiale] (#complexité)
5. [Code Snippets](#codes)
* Java
* Python
* C++
6. [Bonne, mauvaise et mauvaise] (#bonne et mauvaise)
7. [SEO-Optimized Blog Post](#blog)
8. [Takeaway & Comment l'utiliser dans une entrevue] (#takeaway)

---

- Oui. 1. Récapitulation du problème <un nom="problème-recap"></a>

Alice commence par la corde **-a**.
Bob donne une liste "opérations" de longueur "n" (1 ≤ n ≤ 100) où

Opération Effet
C'est quoi ?
(Appendice une copie de lui-même)
**1**"mot = mot + changement(mot)" où `shift` tourne chaque lettre à sa lettre suivante dans l'alphabet (z → a)

Compte tenu d'un indice 1 «k» (1 ≤ k ≤ 1014) qui est garanti à l'intérieur de la chaîne finale, retourner le caractère à la position «k».

**Exemple**

Texte
k = 10, opérations = [0,1,0,1]
dernier mot: abababbbbccbbcc
caractère k‐th (10ème) → 'b '
«» "

---

- Oui. 2. Intuition et principale conclusion <un nom></a>

* ** Les deux opérations doublent la longueur. **
Que l'on copie la chaîne ou copie une copie décalée, la longueur est toujours `2 × longueur précédente`.

* **Nous n'avons jamais besoin de construire la chaîne. **
La corde peut être astronomiquement grande (2100 > 1030).
Nous n'avons besoin que de localiser le caractère *k-th*, donc nous pouvons **marcher en arrière** à travers les opérations, rétrécir `k` et accumuler combien de fois les caractères ont été déplacés.

* ** Simulation inverse* *
Commencez à partir de la fin de la liste des opérations.
Pour chaque opération:

* Si `k` est dans la *seconde* moitié du mot actuel, nous sommes dans la partie qui a été annexée en dernier.
* Pour op 0 → pas de changement, il suffit de soustraire la longueur de la première moitié.
* Pour op 1 → soustraire la première moitié et **en ajouter une au compteur de quarts** (parce que cette moitié est la copie * décalée*).

* Si `k` est dans la première moitié → rien ne change; continuez.

Après le traitement de toutes les opérations, `k` indiquera le premier caractère de l'original.
Le caractère final est simplement « a » déplacé par le compteur accumulé (mod 26).

* ** Longueurs énormes à la main**
Nous devons seulement savoir si une longueur dépasse "k".
Pendant la construction du tableau de longueur, serrez chaque valeur à `k + 1` (ou `Long.MAX_VALUE`) pour éviter le débordement et garder les comparaisons rapides.

---

- Oui. 3. Algorithme Parcours <un nom="algorithme"></a>

«» "
1. Let n = opérations. longueur
2. len[0] = 1 // longueur après 0 opérations
Pour i = 0 ... n-1:
len[i+1] = min(len[i] * 2, k + 1)
3. déplacement = 0
4. Pour i = n-1 jusqu ' à 0:
moitié = len[i] // longueur avant cette opération
si les opérations[i]] 0:
si k > la moitié: k -= moitié
autres (opérations [i]] 1):
si k > la moitié:
k -= moitié
fonction = (poste + 1) % 26
5. réponse = char('a' + quart)
«» "

**Pourquoi ça marche* *

* Lors de l'inversion d'une op 0, le mot est `firstHalf + firstHalf`.
La *seconde* moitié est une copie identique, de sorte que le caractère à `k` (si dans la deuxième moitié) est le même que le caractère à `k-moitié` dans la première moitié.

* Lors de l'inversion d'une op 1, le mot est "première moitié + quart (première moitié)".
La seconde moitié est la copie *transférée*, de sorte que le caractère à `k` (si dans la seconde moitié) est le même que le caractère à `k-moitié` dans la première moitié, **mais déplacé par un**.
Nous le saisissons en augmentant le « changement ».

* Répéter jusqu'à ce que nous atteignions l'original garantie que nous pointons vers le caractère correct.

---

- Oui. 4. Complexité temporelle et spatiale <un nom=complexité></a>

Complexe métrique
C'est pas vrai.
Temps **O(n)** (n ≤ 100)
Espace **O(n)** pour le tableau de longueur (= 100 valeurs longues)

Toutes les opérations sont à temps constant; l'algorithme ne touche jamais la chaîne réelle.

---

- Oui. 5. Extraits de code <a name="codes"></a>

### Java

"Java
Importation de java.util.*;

solution de classe {
char kthCaractère(long k, opérations int[]) {
n = opérations. longueur;
long[] len = nouveau long[n + 1];
len[0] = 1;
pour (int i = 0; i < n; i++) {
longueur suivante = len[i] << 1; // len[i] * 2
si (suivant > k) suivant = k + 1; // pince pour éviter le débordement
len[i + 1] = suivant;
}

nombre de postes appliqués
pour (int i = n - 1; i >= 0; i--) {
la moitié longue = len[i];
si (opérations [i]] 0) {/ duplicata
si (k > la moitié) k -= la moitié;
} autre { // copie de décalage
si (k > la moitié) {
k = moitié;
poste = (poste + 1) % 26;
}
}
}
retour (char) ('a' + quart);
}
}
«» "

Python

'`python
Solution de classe:
def kthCharacter(self, k: int, operations: List[int]) -> str:
n = len(opérations)
longueurs = [1] * (n + 1)
pour i dans la plage(n):
nxt = longueurs[i] * 2
si nxt > k:
nxt = k + 1 # pince pour éviter le débordement
longueurs[i + 1] = nxt

changement = 0
pour i dans la fourchette(n - 1, -1, -1):
moitié = longueurs[i]
si les opérations[i]] 0:
si k > la moitié:
k -= moitié
Autre: # opération de quart
si k > la moitié:
k -= moitié
fonction = (poste + 1) % 26

retour chr(ord('a') + quart)
«» "

C++

'`cpp
solution de classe {
public:
char kthCharacter(long long k, vector<int>& operations) {
int n = operations.size();
vecteur <long> len(n + 1);
len[0] = 1;
pour (int i = 0; i < n; ++i) {
longueur longue nxt = len[i] << 1; // multiplier par 2
si (nxt > k) nxt = k + 1; // pince
len[i + 1] = nxt;
}

poste int = 0;
pour (int i = n - 1; i >= 0; --i) {
longue moitié longue = len[i];
si (opérations [i]] 0) {
si (k > la moitié) k -= la moitié;
} autre {
si (k > la moitié) {
k = moitié;
poste = (poste + 1) % 26;
}
}
}
retour char('a' + quart);
}
};
«» "

> **Astuce**: La clé est de stocker *demi-longueur* et **de simuler-inverse** les opérations. Aucun bâtiment à cordes n'arrive jamais.

---

- Oui. 6. Bon, mauvais et humble <a name="goodbadugly"></a>

Category Category What Works Qu'est-ce que regarder Comment réparer
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bon**• Algorithme linéaire temps<br>• Mémoire O(1) par opération<br>• Poignées `k` jusqu'à 1014 sans débordement<br>• Fonctionne pour tous les boîtiers de bord (ops vides, tous les 0s, tous les 1s)
**Bad**) • Une implémentation naïve qui construit la chaîne TLE/MLE.<br>• L'oubli des valeurs de longueur de serrage conduit au débordement (2100 > long max). Gardez toujours le « poste % 26 ».<br>• Traitez le « k » de façon cohérente. Autres
**Les solutions récursives qui recalculent les longueurs de chaque appel peuvent atteindre les limites de la pile. Complication excessive avec des astuces bit-mask qui obscurcissent la logique. Préférez l'arithmétique entier clair sur les hacks flottants ou bit. Autres

---

- Oui. 7. SEO-Optimized Blog Post <a name="blog"></a>

Titre
*Master LeetCode 3307: Trouvez le caractère K dans le jeu de chaînes II – Java, Python & C++ Solutions**

Description de la méta
Résolvez le LeetCode 3307 (hard) en quelques minutes. Apprenez l'astuce de simulation inverse, obtenez le code Java/Python/C++ et des explications prêtes à l'entrevue. Parfait pour les ingénieurs logiciels se préparant pour les entrevues de codage.

### Rubriques & Contenu

1. **Qu'est-ce que LeetCode 3307? **
* Expliquez le problème, les contraintes, et pourquoi il est étiqueté "hard". *

2. **Pourquoi l'approche droite vers l'avant fait défaut* *
*Construire la corde explose en mémoire (2100 chars). *

3. **Le point de vue clé: simulation inverse**
*Les deux ops double longueur → nous pouvons réduire `k`. *

4. **Algorithme étape par étape**
*Afficher le pseudocode avec des diagrammes. *

4. **Cases de cornière et manipulation des bords**
*Longues de serrage, indexation 1-basée, modulo de déplacement. *

5. ** Mise en œuvre de Java**
* Code complet + commentaire. *

6. **Mise en œuvre du Python**
* Code complet + commentaire. *

7. **C++ Mise en œuvre**
* Code complet + commentaire. *

8. ** Analyse de complexité**
*O(n) temps, O(n) espace – idéal pour les intervieweurs. *

9. **Pièges et correctifs communs**
* Bonne/Bad/Ugly table. *

10. ** À emporter – Ce que les intervieweurs Veux**
* raisonnement clair, temps optimal, code concis. *

11. ** Prêt à impressionner dans votre prochaine entrevue? **
*Pratique avec cette solution, partagez sur LinkedIn, demandez aux recruteurs pour les défis de codage. *

Mots clés
- LeetCode 3307
- Jeu de caractères K-th
- Entretien de codage de simulation inverse
- Solutions de leetcode Python Java C++
- Préparation de l'entrevue de codage

### Appels à l'action
> **Essayez-le maintenant!** Copiez le code, lancez-le sur LeetCode, et voyez les économies de temps.
> **Partagez vos pensées** dans les commentaires—etons discuter des optimisations et des astuces alternatives.

Image & schéma
Inclure un diagramme de marche arrière (deux flèches pointant à gauche) et ajouter un schéma JSON‐LD pour *TechArticle*.

---

Pourquoi ce blog aide votre carrière

* **Visibilité** – Mots-clés ciblés (=LeetCode 3307 solution==, =Java interview problem===, =Codage interview hard==) attirent les recruteurs.
* ** Crédibilité** – Fournir des solutions propres et multilingues montre une vaste gamme de connaissances.
* **Engagement** – Le tableau "Good/Bad/Ugly" est une référence rapide que les lecteurs signent.

Publiez sur un blog personnel ou des pages GitHub, liez-le dans votre CV, et regardez les gestionnaires d'embauche prendre note.

---

- Oui. 8. Réflexions finales <un nom="final"></a>

Le défi LeetCode 3307 est un problème classique de réflexion inverse.
En observant que chaque opération ne fait que doubler la chaîne et que la partie annexée est soit une copie identique, soit une copie décalée, nous pouvons faire tomber la recherche en quelques étapes arithmétiques.

Rappelez-vous :
* **Ne jamais construire la chaîne. **
* **Simulez inversement** tout en accumulant les quarts.
* ** Longueurs de la pince** pour éviter les débordements.

Avec les extraits ci-dessus en Java, Python ou C++, vous pouvez répondre au 1014ème caractère en moins d'une milliseconde pour votre prochaine interview de codage.

Bon codage ! C'est ce qu'il a dit.

---

**Bonne entrevue Préparez !**
N'hésitez pas à poser des questions de suivi sur les commentaires ou sur votre réseau personnel.