---
titre: LeetCode 2057. Le plus petit indice de valeur égale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2057 – *Indice le plus petit ayant une valeur égale*
### Une solution complète Java/Python/C++ + un article de blog favorable à la recherche d'emploi

> **Mots clés:** LeetCode 2057, indice le plus petit Avec égalité Valeur Solution Java, Solution Python, Solution C++, Algorithme d'entretien, Interview de codage, Interview d'emploi, Pensée algorithmique

---

Récapitulation des problèmes

On vous donne un tableau entier 0 indexé «nums».
Trouvez le plus petit indice `i` tel que `i % 10 == nums[i]`.
Retourner `-1` s'il n'existe pas de tel indice.

«» "
Entrée : nombres = [4,3,2,1]
Produit: 2 // 2 % 10 == 2
«» "

**Contrôles* *

Valeur de la propriété
C'est quoi ?
1 ≤ "longueur en chiffres" ≤ 100
0 ≤ «nums[i]» Autres

Les limites sont minuscules, mais le défi est d'écrire une solution propre et lisible qu'un gestionnaire d'embauche peut skim en quelques secondes.

---

- Oui. Les bons, les mauvais et les méchants

Aspect Ce que vous aimez Qu'est-ce qui pourrait vous faire monter
C'est-à-dire
**Bon**• Temps O(n), espace O(1).<br>• Pas de structures de données supplémentaires.<br>• Un passage, logique de sortie précoce.
Autres La base modulo est codée "10". Si vous avez plus tard besoin d'une vérification générique de mod, vous aurez besoin de refactor.
Certains intervieweurs lanceront un cas *corner* : un tableau des 9s. La solution naïve *travaille* mais on pourrait encore vous demander d'expliquer *pourquoi* vous avez utilisé `break` au lieu de revenir immédiatement.

> **Ligne de bottom:** Gardez l'algorithme simple, expliquez la raison d'être de la sortie précoce, et soyez prêt à généraliser si l'intervieweur dit : "Et si la base était "k" ?"

---

- Oui. Brute- Force vs One-Pass

Une approche naïve « two-loop » revérifierait chaque paire – clairement surqualifiée.
La solution à un passage inférieure à l'itérée depuis le début, vérifie l'état et s'arrête au premier coup. C'est tout ce dont vous avez besoin.

---

Solutions en 3 langues

> Les trois extraits sont **fonction-seulement** – le "main" ou harnais de test environnant est omis pour garder l'accent sur la logique de base.

#### 4.1 Java

"Java
// LeetCode 2057 – Indice le plus petit avec une valeur égale
solution de classe {
de l'État
pour (int i = 0; i < nombres de longueur; i++) {
si (i % 10 == nombres[i]) {
retour i; // première correspondance = plus petit indice
}
}
retour -1; // aucune correspondance trouvée
}
}
«» "

**Pourquoi `retour` au lieu de `break`?**
Le retour immédiat est plus clair pour un examinateur – la fonction quitte dès que la réponse est connue.

---

4.2 Python

'`python
# LeetCode 2057 – Indice le plus petit avec une valeur égale
Solution de classe:
def le plus petit Equal(self, nombres: Liste[int]) -> Int:
pour i, val dans l'énumération(nombres):
i % 10 == valeur:
retour
retour -1
«» "

*Note:* "énumérer" donne à la fois l'indice et la valeur en un seul passage.

---

### 4.3 C++

'`cpp
// LeetCode 2057 – Indice le plus petit avec une valeur égale
solution de classe {
public:
Int plus petitEqual(vecteur<int>& nums) {
pour (int i = 0; i < nums.size(); ++i) {
si (i % 10 == nombres[i]) retourne i;
}
retour -1;
}
};
«» "

`vector<int>&` passe par référence pour l'efficacité, bien que copier un tableau de 100 éléments soit trivial.

---

Analyse de complexité

Métrique
- C'est quoi ?
Temps **O(n)**
Espace

`n` est la longueur de `nums` (= 100).
Parce que nous brisons sur le premier coup, le temps moyen* est encore moins que `n` dans les entrées typiques.

---

## 6--Cas de bord & Gotchas

Que vérifier ?
- C'est quoi ?
Ajouter `si (nums.vide()) retourner -1;`
Tous les 9=2 Aucune correspondance → retour -1=2 Poigné automatiquement
"i % 10 == nombres[i]" quand `nums[i] == 0 '..0 0 travaux fin.
"nums[i] > 9"" Violates contraintes – vous pouvez encore écrire le code robuste" "si (i % 10 == nums[i] % 10)" – mais pas requis"

---

Variantes et généralisations

Question: Comment s'adapter?
C'est pas vrai.
Autres Et si la base était **k** au lieu de 10 ? Remplacer `10` par `k`. Autres
Trouver tous les indices, pas seulement les plus petits. Recueillir des indices dans un «vecteur<int>» et retourner. Autres
Autres Le tableau pourrait être extrêmement grand (106). Toujours temps O(n); mémoire non affectée. Autres

---

## 8-- Interview-Style Questions

1. **Pourquoi retournez-vous immédiatement au lieu de casser? * *
*Réponse:* Il raccourcit le code et signale clairement le point de sortie de l'algorithme.

2. **Et si "nums[i]" Ça pourrait être négatif ? * *
*Réponse:* Dans Python et Java, l'opérateur `%` gère les négatifs en retournant un reste non négatif (Python="s `%`), mais vous devez ajuster pour le comportement des signes C++.

3. **Comment gérer un scénario où vous devez retourner l'indice *seconde* le plus petit correspondant? * *
*Réponse:* Suivez le premier match, continuez la boucle et capturez le second lorsqu'il est trouvé.

---

Aperçu du blog optimisé du SEO

Vous trouverez ci-dessous une ébauche que vous pouvez copier dans une plateforme de blogs (Medium, Dev.to, LinkedIn Pulse, etc.).

> **Titre**: LeetCode 2057 – Indice le plus petit avec une valeur égale – Java, Python, C++ + Conseils d'entrevue

«» "
# Cracking LeetCode 2057 – Indice le plus petit avec une valeur égale

## Déclaration du problème
...

- Oui. Pourquoi ce problème est important
...
## La solution One-Pass – O(n) Time, O(1) Espace
...

- Oui. Mise en œuvre Java
...

Mise en œuvre de Python
...

C++ Mise en œuvre
...

Analyse de complexité
...

Pièges communs
...

## Interview‐Ready Variantes
...

## Pensées finales & A emporter
...
«» "

*Ajouter des métabalises:*
- `meta name="keywords" content="LeetCode 2057, Index le plus petit Avec égalité Valeur Solution Java, Solution Python, Solution C++, Codage interview, Algorithme interview, Job interview"
- `meta name="description" content="Apprendre à résoudre le LeetCode 2057 (le plus petit indice ayant une valeur égale) en Java, Python et C++. Comprendre l'algorithme, la complexité et les conseils d'entrevue pour impressionner les gestionnaires d'embauche. "

*Utilisez des rubriques (`h1`, `h2`, `h3`) et des listes de puces pour la lisibilité. *
*Ajouter des blocs de code avec mise en évidence syntaxique. *

---

Liste de contrôle finale avant de soumettre

- **Correctness** – Exécutez tous des exemples et des tests aléatoires.
- **Readability** – Les noms variables («i», «val», «réponse») s'expliquent eux-mêmes.
- ** Temps/Espace** – Documenté et prouvé optimal.
* Entretien** – Soyez prêt à expliquer *pourquoi* vous cassez/retournez tôt et *comment* vous généraliseriez.
- **Blog** – Utilisez le contour, publiez et partagez sur LinkedIn/Twitter avec une légende convaincante.

---

Félicitations !

Vous avez maintenant :

- Une solution propre et prête à la production en **Java, Python et C++**.
- Un billet de blog favorable au travail qui montre votre compréhension du problème, de l'algorithme et de la communication de type interview.
- Un guide de référence rapide pour les suivis d'entrevues communs.

Bonne chance pour vos interviews de codage ! C'est ce qu'il a dit