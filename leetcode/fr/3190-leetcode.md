---
titre: LeetCode 3190. Trouver des opérations minimales pour rendre tous les éléments divisibles par trois -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3190. Trouver des opérations minimales pour rendre tous les éléments divisibles par trois

### TL;DR
- **Solution :** Compter le nombre de nombres dans le tableau **pas** déjà divisible par 3.
- **Complexité temporelle :** "
- **Complexité spatiale :** `O(1)`

Ci-dessous vous trouverez des implémentations propres, prêtes à la production dans **Java, Python et C++**, suivies d'un court article de blog SEO-friendly qui explique le problème, le bon, mauvais et laid de la solution, et comment cette connaissance peut augmenter votre performance d'interview.

---

- Oui. 1. Remise en état des problèmes

On vous donne un tableau entier `nums`.
Dans une opération, vous pouvez **ajouter ou soustraire 1** à n'importe quel élément.
Retourner le nombre minimum d'opérations requis pour rendre chaque élément divisible par 3.

*Contrôles*

«» "
1 <= longueur totale <= 50
1 <= nombres[i] <= 50
«» "

---

- Oui. 2. Pourquoi la solution est si simple

Chaque entier a un reste de `0`, `1`, ou `2` quand divisé par 3.

Une seule opération ? Opération nécessaire
-- -- -- -- -- -- -- -- --
Numéro
Oui Soustraire
Autres Oui Ajouter

Ainsi, chaque élément qui n'est pas déjà un multiple de 3 doit exactement **un** ajustement.
Compter ces éléments donne la réponse.

---

- Oui. 3. Complexité

Aspect
C'est pas vrai.
Temps `O(n)` – un passage sur le tableau. Autres
Espace "O(1)" – seulement un compteur. Autres

---

- Oui. 4. Cas de bord et validation

Que vérifier ? Résultat
C'est pas vrai.
Remorque vide. Sans objet
Autres Tous les nombres divisibles par le compteur reste 0.
Autres Tous les numéros 1 (mod. 3)
Autres Tous les numéros 2 (mod. 3)

L'implémentation protège contre les valeurs inattendues (par exemple, les nombres négatifs) en utilisant correctement l'opérateur de module.

---

- Oui. 5. Mise en oeuvre des références

#### 5.1 Java (compatible avec le code leet)

"Java
// LeetCode 3190: Trouver des opérations minimales pour rendre tous les éléments divisibles par trois
solution de classe publique {
Nombre minimum d'opérations (int[] nombres) {
Int ops = 0;
pour (int num : nombres) {
si (nombre % 3 != 0) {
ops++;
}
}
les opérations de retour;
}
}
«» "

#### 5.2 Python (3.11+)

'`python
# LeetCode 3190: Trouver des opérations minimales pour rendre tous les éléments divisibles par trois
de taper l'importation Liste

Solution de classe:
def minimumOperations(self, nombres: List[int]) -> Int:
# Compter les éléments qui ne sont pas divisibles par 3
somme de retour(1 pour nombre en nombre si nombre % 3 != 0)
«» "

### 5.3 C++ (C++17)

'`cpp
// LeetCode 3190: Trouver des opérations minimales pour rendre tous les éléments divisibles par trois
#incluez <vecteur>

solution de classe {
public:
int minimumOpérations(std:vector<int>& nums) {
Int ops = 0;
pour (int num : nombres) {
si (nombre % 3 != 0) + op;
}
les opérations de retour;
}
};
«» "

---

- Oui. 6. Article de blog – Le bon, le mauvais, et le mauvais d'une solution LeetCode 3190

> **Meta Titre:** LeetCode 3190 – Opérations minimales pour rendre tous les éléments divisibles par 3
> **Meta Description:** Master LeetCode 3190 avec une solution claire, O(n) Java/Python/C++. Comprendre la logique, les pièges et les hacks d'entrevue.

---

6.1 Le problème en anglais clair

Vous avez un éventail d'entiers.
Vous pouvez changer n'importe quel entier en ajoutant ou en soustrayant **un** à la fois.
Combien de changements en une seule étape sont nécessaires pour que *chaque* entier dans le tableau soit un multiple de 3?

Il semble difficile, mais l'astuce est que chaque nombre a seulement besoin **un** tweak à moins qu'il soit déjà un multiple de 3.

---

6.2 Le bien

- **Simplicité** – Un passage, un comptoir.
- **Scalabilité** – temps "O(n)", espace "O(1)", fonctionne pour toute taille dans les limites des contraintes.
- **Readability** – Pas de boucles cachées, pas de nombres magiques ; quiconque lit le code peut le saisir instantanément.
- **Couverture de test** – Poigne tous les restes possibles et les cas de bord hors de la boîte.

---

### 6.3 La mauvaise

- **Complexité trompeuse** – Une personne qui ne connaît pas l'arithmétique modulaire pourrait surpenser et écrire une solution DP ou BFS.
- **Corner Cases in Other Languages** – En Python, `%` sur les nombres négatifs peut se comporter différemment, donc vous'd besoin d'ajuster la formule (`num % 3 != 0` fonctionne bien pour les nombres positifs, mais soyez prudent si les contraintes changent).
- **Over‐Optimization** – Essayer de micro‐optimiser la boucle (p. ex. déroulement, SIMD) n'offre aucun avantage réel compte tenu de la petite taille d'entrée.

---

### 6.4 L'Ugly

- **Code répété** – écrire la même logique en plusieurs langues en une seule entrevue peut encombrer le tableau blanc.
- **Lack of Commentary** – Sans commentaires en ligne ou une brève preuve de concept, les intervieweurs pourraient douter de votre compréhension.
- **Ignorer les contraintes** – L'oubli de la liaison `1 <= nums[i] <= 50' pourrait vous conduire à une solution surenginer qui gère les valeurs négatives ou importantes.

---

6.5 Comment cela vous aide à obtenir un emploi

1. **Reconnaissance Pattern** – Vous apprenez à repérer l'astuce "remainder" tôt.
2. **Communication** – Le blog démontre que vous pouvez expliquer l'idée, les pièges, et les compromis – compétences critiques d'entrevue.
3. **Compétence multilingue** – Le code Java, Python et C++ étant propre, vous pouvez vous adapter à n'importe quelle pile.
4. **SEO-Optimized Content** – Publier cet article sur Medium, Dev.to, ou votre propre blog renforce votre présence en ligne, faisant des recruteurs vous découvrir par des recherches par mots-clés comme la solution de LeetCode 3190 ou divisible par trois algorithmes. (en milliers de dollars)
5. **Portfolio Highlight** – Inclure le problème dans votre lecture GitHub avec les extraits de solution et un lien vers votre blog.

---

6.6 Dernier départ

- **Une opération par non-multiple** → Nombre de "nums[i] % 3 != 0'.
- **Heure**: "O(n)"
- **Espace**: "O(1)"

L'élégance du LeetCode 3190 réside dans la reconnaissance du fait que chaque numéro n'a besoin que d'une seule modification pour s'aligner sur sa classe modulo. Maîtrisez ce modèle, et vous résoudrez d'innombrables autres problèmes de divisibilité.

Joyeux codage – et heureux entretien!