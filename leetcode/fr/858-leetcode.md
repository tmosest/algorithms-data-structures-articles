---
titre: LeetCode 858. Réflexion miroir -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Réflexion miroir – LeetCode 858
### Les bons, les mauvais et les méchants (Java-Python C++)

---

### TL;DR
- **Problème** – Trouvez le premier récepteur qu'un rayon laser frappe dans une pièce carrée avec des murs miroirs.
- **Idée clé** – Réduisez le problème à un puzzle théorique en utilisant *gcd* et *lcm*.
- **Complexité** – **O(log min(p,q))** temps, **O(1)** mémoire.
- **Pourquoi c'est important** – Un favori d'interview classique qui teste l'intuition mathématique, la pensée gourmande et l'élégance du code.

---

- Oui. 1. Énoncé de problème (court et doux)

Dans une pièce carrée de longueur latérale `p` un laser part du coin sud-ouest et se déplace vers le mur est.
La première fois qu'il atteint le mur est, il est à une distance `q` du 0-récepteur (le coin sur le mur est).

Les récepteurs se trouvent aux trois autres coins (0, 1, 2).
**Retourner le numéro du récepteur que le rayon rencontre en premier. **

*Contrôles*
`1 ≤ q ≤ p ≤ 1000` – le rayon rencontre toujours un récepteur en fin de compte.

---

- Oui. 2. La bonne – Intuition et la solution élégante

2.1 Visualisation des réflexions

Pensez à déplier la pièce.
Chaque fois que le rayon frappe un mur, au lieu de réfléchir, nous miroir la pièce et laisser le rayon continuer tout droit.
Après le déploiement, le rayon voyage en ligne droite de `(0,0)` au premier coin *virtuel* qui se trouve sur la grille de la taille `p × p`.

La coordonnée verticale lorsque le rayon atteint pour la première fois une limite verticale (mur est ou ouest) est un multiple de `p`.
La coordonnée horizontale est un multiple de `p` aussi bien – mais seulement quand `m × q` est un multiple de `p`, où `m` est le nombre de fois où nous avons heurté un mur vertical.

Nous avons donc besoin du plus petit entier `m` de telle sorte que:

«» "
m × q 0 (mod p)
«» "

2.2 Utilisation de GCD / LCM

`m` est simplement le multiple le moins commun de `p` et `q` divisé par `q`:

«» "
lcm(p, q) = p × q / gcd(p, q)
m = lcm(p, q) / q = p / gcd(p, q)
«» "

Laissez

«» "
p_div = p / gcd(p, q)
q_div = q / gcd(p, q)
«» "

Maintenant :

- Si `q_div` est même → le rayon touche le récepteur **2** de la paroi ouest**.
- Si `q_div` est étrange :
- Si `p_div` est impair → récepteur **1**.
- Else (`p_div` même) → récepteur **0**.

C'est ça ! Un seul calcul GCD et quelques contrôles de parité.

2.3 Extraits de code

Code de la langue
C'est quoi, ça ?
{<br> miroir int public intReflexion(int p, int q) {<br> int g = gcd(p, q);<br> int pDiv = p / g;<br> int qDiv = q / g;<br> si (qDiv % 2 == 0) retour 2; // frappe le mur ouest d'abord<br> retour (pDiv % 2 == 1) ? 1 : 0; // impair→1, even→0<br> }<br> int privé gcd(int a, int b) {<br> pendant (b != 0) {<br> int t = a % b;<br> a = b;<br> b = t;<br> }<br> retourner a;<br> }<br>}<br> Autres
**Python** $ ``python<br>class Solution:<br> def mirrorReflexion(self, p: int, q: int) -> int:<br> de maths import gcd<br> g = gcd(p, q)<br> p_div, q_div = p // g, q // g<br> if q_div % 2 == 0:<br> retourner 2<br> retourner 1 si p_div % 2 == 1 autre 0<br>`"
**C++**="cpp<br>#include <bits/stdc++.h><br>using namespace std;<br><br>class Solution {<br>public:<br>int mirrorReflexion(int p, int q) {<br> int g = gcd(p, q);<br> int pDiv = p / g;<br> int qDiv = q / g;<br> si (qDiv % 2 == 0) retour 2; // mur ouest<br> retour (pDiv % 2 == 1) ? 1 : 0; // mur est ou sud<br>};<br>`` Autres

> **SEO Conseil:** Utilisez le nom de classe exact `Solution` – LeetCode l'attend.

---

- Oui. 3. Les mauvaises – pièges communs

Pourquoi ça se casse
C'est pas vrai.
**L'utilisation de `lcm` directement**L'utilisation de `lcm` peut déborder si `p*q` dépasse la portée int (probablement avec des limites données mais toujours). Calculer `p / gcd(p, q)` au lieu de `p * q / gcd(p, q)`. Autres
**Ignorer la parité** Rappelez-vous : même `q_div` → récepteur 2.
**Off‐by‐one dans l'indexation**Le problème utilise la numérotation des récepteurs à 0; un modèle mental à 1 peut causer de mauvaises sorties. C'est la règle. Autres
**La simulation de la force brute**=La simulation des réflexions étape par étape est O(p/q) et peut être lente pour de grandes valeurs. Utilisez le raccourci mathématique. Autres

---

- Oui. 4. La folie – ce qui arrive quand nous sur-optimisons

- **Micro-optimisations** comme l'inline `gcd` pour chaque cas d'essai (si de nombreux cas d'essai) peuvent rendre le code illisible.
- **Suringénierie** – l'utilisation de la théorie des nombres complexes (inverses modulaires, Euclid étendu) ajoute du bruit.
- ** Obfuscation de code** – un-liner, l'enfer ternaire a l'air léché mais difficile à déboguer.

> *Leçon*: Gardez-le simple, lisible et correct. Les intervieweurs apprécient le code propre plus que les astuces intelligentes.

---

- Oui. 5. Analyse de la complexité

- **Time**: `O(log min(p,q)' – le temps pour l'algorithme de GCD euclidean.
- **Espace**: "O(1)" – espace auxiliaire constant.

---

- Oui. 6. Comment cela vous aide à chasser votre emploi

1. ** Démontre la perspicacité mathématique** – De nombreux intervieweurs aiment les candidats qui transforment la géométrie en algèbre.
2. **Afficher des habitudes de codage propres** – Votre solution est courte, lisible et couvre les cas de bord.
3. **Illustre la pensée algorithmique** – Vous êtes passé de la simulation à la théorie des nombres efficacement.
4. **Suit plusieurs langues** – Vous pouvez basculer facilement entre Java, Python, C++ – idéal pour les équipes multilingues.

---

- Oui. 7. Liste de contrôle des blogs optimisés par le SEO

Mise en œuvre
C'est-à-dire
**Titre** *Miror Reflection LeetCode 858 – Solution Java, Python, C++ (GCD & LCM)* Autres
**Description de la Méta*** *Solve LeetCode 858 – Réflexion miroir. Comprendre les maths derrière GCD/Lcm, voir Java propre, Python, C++ code, et apprendre pourquoi ce problème est parfait pour la préparation d'entrevue.* Autres
**En-têtes**= Utiliser H1 pour le titre, H2 pour les sections (Problème, Intuition, Code, etc.). Autres
**Mots clés**= `Réflexion de mirreur`, `LeetCode 858`, `GCD`, `LCM`, `algorithme interview`, `Java solution`, `Python solution`, `C++ solution`. Autres
**Liens internes**= Lien vers des problèmes liés au LeetCode (p. ex. 87, 994). Autres
**Liens externes**=Cite la page de problème officielle LeetCode, et référez-vous aux liens que vous avez fournis. Autres
**Images/Diagrammes** Un petit diagramme de la pièce déployée peut stimuler l'engagement. Autres
**Readability** Autres
**Appelez à l'action**=Essayez ceci sur LeetCode maintenant et dites-moi combien de points vous avez gagnés!= Autres

---

- Oui. 8. Dernier départ

Mirror Reflection est plus qu'un puzzle de géométrie – c'est une étude de microcase en *simplifiant* un problème.
En cartographiant les réflexions sur une grille déployée et en utilisant la relation gcd/lcm, nous transformons un problème physique apparemment complexe en une poignée d'opérations arithmétiques.

**Bonne**: Maths élégants, code minimal.
**Bad**: Erreurs communes de parité.
**Ugly**: Suringénierie et illisible monolignes.

Maîtrisez ceci, et vous allez non seulement ace LeetCode 858 mais impressionner également les intervieweurs avec votre capacité à distiller des problèmes dans des solutions propres et efficaces. Bon codage !