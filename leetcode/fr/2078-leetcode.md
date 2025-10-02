---
titre: LeetCode 2078. Deux maisons avec des couleurs différentes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Récapitulation des problèmes – LeetCode 2078
**Deux maisons les plus luxueuses aux couleurs différentes* *
> **Signature (Java)* *
> `public int maxDistance(int[] couleurs) "

Vous êtes donné un tableau `colors` où `colors[i]` est la couleur de la peinture de la maison *i*-th (les maisons sont disposées en une seule ligne).
Retournez la distance maximale entre deux maisons qui sont ** peintes en différentes couleurs**.
La distance entre les maisons *i* et *j* est `=i – j=.

Contraintes
* `2 ≤ n = longueur de couleur ≤ 100`
* `0 ≤ couleurs[i] ≤ 100`
* Il y a au moins deux maisons de couleurs différentes.

---

- Oui. 2. L'approche directe vers l'avant (O(n2))

"Java
solution de classe {
int public maxDistance(int[] couleurs) {
int n = couleur.longueur;
int best = 0;
pour (int i = 0; i < n-1; i++) {
pour (int j = i+1; j < n; j++) {
si (couleurs[i] != couleurs[j]) {
best = Math.max (best, j-i);
}
}
}
le meilleur retour;
}
}
«» "

* **Heure** – "O(n2)"
* **Espace** – "O(1)"

Avec `n ≤ 100` c'est assez rapide pour LeetCode, mais nous pouvons faire mieux.

---

- Oui. 3. La solution "Good" – Espace constant, temps linéaire

L'observation clé :
**La plus éloignée implique toujours la première ou la dernière maison. **
Si vous avez une paire qui ne touche aucune des deux extrémités, vous pouvez toujours déplacer une extrémité de la paire vers un bord et la distance ne peut qu'augmenter.

Il suffit donc d'examiner deux positions :

Poste Ce qu'il représente Pourquoi il importe
-- -- -- -- -- -- -- -- --
`i` – la maison la plus à gauche qui est *différente* de la dernière couleur Autres
`j` – la maison la plus droite qui est *différente* de la première couleur="la plus éloignée de l'extrémité gauche="distance à la première maison="j-0`"

La réponse est simplement "max(j, n-1-i)".

### Java – Espace constant (mémoire O(1))

"Java
solution de classe publique {
int public maxDistance(int[] couleurs) {
int n = couleur.longueur;
int gauche = 0; // indice de la première maison
int droite = n - 1; // dernier indice de la maison

// Trouver la maison la plus à gauche qui diffère de la dernière couleur
pendant que (couleurs[gauche] == couleurs[droite]) {
gauche++;
}

// Trouver la maison la plus droite qui diffère de la première couleur
pendant que (couleurs[droite]== couleurs[gauche]) {
droit...
}

// La distance la plus éloignée est le maximum de deux candidats
retour Math.max(à droite, n - 1 - à gauche);
}
}
«» "

### Python – Espace constant (mémoire O(1))

'`python
Solution de classe:
def maxDistance(self, couleurs: Liste[int]) -> Int:
n = len(couleurs)
gauche, droite = 0, n - 1

# index le plus à gauche avec une couleur différente de la dernière maison
tandis que colors[left] == colors[right]:
gauche += 1

# index le plus droit avec une couleur différente de la première maison
tandis que colors[right] == colors[left]:
droite -= 1

retour max(à droite, n - 1 - à gauche)
«» "

### C++ – Espace constant (mémoire O(1))

'`cpp
solution de classe {
public:
int maxDistance(vecteur<int>& couleurs) {
int n = colors.size();
Int gauche = 0, droite = n - 1;

pendant que (couleurs[gauche] == couleurs[droite]) --droite;
pendant que (couleurs[droite] == couleurs[droite]) ++gauche;

retour max (droite, n - 1 - gauche);
}
};
«» "

**Complexités* *
* **Heure** – `O(n)` (un laissez-passer pour chaque côté, le pire cas `O(n)` total)
* **Espace** – "O(1)" (seulement quelques indices)

---

- Oui. 4. L'Énorme – Pourquoi ne pas iter sur toutes les paires

* complexité O(n2) – trop de compétences pour les limites, mais toujours facile à coder.
* Fonctionne pour chaque scénario mais gaspille du temps CPU si `n` augmente au-delà de 100.

Parfois, les intervieweurs demandent explicitement la meilleure solution possible. Fournir une solution quadratique est une réponse *mauvaise* car elle ne montre pas la compréhension de la structure du problème.

---

- Oui. 5. L'Ugly – Edge Tricky Mise en œuvre des cas

Une version buggy peut mal gérer des tableaux où toutes les maisons ont la même couleur, sauf une à la fin.
"Java
pendant que (couleurs[0] == couleurs[i]) i++; // s'arrête quand i == N- 1
// Je pourrais devenir n, menant à ArrayIndexOutOfBoundsException
«» "
Assurez-vous de ** vérifier les limites** ou d'utiliser un état de boucle sécuritaire (`i < n`) et de gérer le cas où aucune couleur différente n'est trouvée d'un côté.

---

- Oui. 6. Succès d'entrevue

1. **Lisez attentivement l'invite** – notez que la réponse doit impliquer la première ou la dernière maison.
2. ** Pensez aux invariants** – la paire la plus éloignée touchera toujours un bord.
3. ** Fournit une solution propre et linéaire** – O(n) temps, O(1) espace est optimal ici.
4. **Mentionnez la manipulation de cas** – si vous montrez la conscience des pièges, vous démontrez la maturité.
5. ** Expliquez votre raisonnement** – les intervieweurs aiment les candidats qui expliquent pourquoi une solution fonctionne.

---

- Oui. 7. SEO-Optimized Blog Post

> **Titre**
> Cracking LeetCode 2078 – Deux maisons avec des couleurs différentes (Java, Python, C++)

> **Description détaillée**
> Apprenez à résoudre le LeetCode 2078 en temps linéaire. Lisez les implémentations Java, Python et C++ de l'espace constant, plus des conseils pour aser votre interview de codage.

> ** Aperçu général**
> 1. Exposé des problèmes et contraintes
> 2. Approche fondée sur la force brute (O(n2))
> 3. Solution O(n) optimale – Pourquoi elle fonctionne
> 4. Mise en œuvre de Java
> 5. Mise en œuvre de Python
> 6. Mise en œuvre C++
> 7. Manipulation des cas et pièges communs
> 8. A emporter pour les entrevues de codage
> 9. Foire aux questions
> 10. Appel à l'action – Pratique sur LeetCode

> **Mots clés**
> LeetCode 2078, Two Furthest Houses with different Colors, coding interview, algorithme, Java, Python, C++, solution O(n), espace constant, conseils d'entretien, prép d'entretien technique, structure des données, complexité temporelle, complexité spatiale.

> ** Liens internes**
> *Lien vers d'autres blogs de problèmes LeetCode dans la série (par exemple, 2048, 2099). *

> ** Liens externes**
> *LeetCode page de problème officielle*, *LeetCode threads de discussion*, *HackerRank, CodeSignal ressources. *

> **Idées d'image**
> 1. Diagramme de flux montrant pourquoi la paire doit toucher un bord.
> 2. Les extraits de code côte à côte.
> 3. Un petit GIF animé de deux maisons se déplaçant vers le bord.

> **CTA**
> Prêt pour votre prochain entretien de codage ? Résolvez plus de problèmes LeetCode et créez votre confiance! (en milliers de dollars)

---

Dépôt de code final

Si vous souhaitez voir les trois implémentations dans une seule repo, clonez le dépôt GitHub suivant :

«» "
clone git https://github.com/votre nom d'utilisateur/code de transport-2078-deux-autres maisons
«» "

Il contient:

* `Solution.java "
* `Solution.py "
* `Solution.cpp "
* Un `README.md` avec le texte de l'article de blog.

Bon codage, et bonne chance dans votre prochain entretien d'emploi!