---
titre: LeetCode 32. Parentheses les plus longues
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
32. Les parenthèses les plus longues – un guide complet
*(Hard – 36,9 % du taux d'acceptation)*

> Avec une chaîne contenant seulement les caractères ‘(= et ‘)=, retournez la longueur de la plus longue **valide** (bien formée) entre parenthèses sous-chaîne. (en milliers de dollars)

Le problème est un LeetCode classique qui teste votre capacité à penser à l'état, aux conditions limites et aux structures de données optimales. Ci-dessous vous trouverez:

* **Trois solutions prêtes à la production** – Java, Python et C++
* A **détaillé, SEO-friendly blog post** qui marche à travers le bon, le mauvais, et la laid de résoudre ce défi.
* Conseils sur la façon de **pitcher ce problème dans une entrevue** et faire du code votre meilleur point de conversation.

---

- Oui. 1. Pourquoi ce problème est important

* **La manipulation de la chaîne** est l'un des sujets d'entrevue les plus courants.
* Le défi vous force à **équilibrer l'état** (ouverture vs fermeture des crochets).
* C'est un *benchmark* pour les approches basées sur la pile par rapport au PDD – les deux valent la peine d'être connus.

Si vous pouvez résoudre ce problème, vous aurez un point de discussion solide pour les entrevues à Meta, Google, Microsoft, Uber et d'autres entreprises de haute technologie.

---

- Oui. 2. Trois solutions optimales

Vous trouverez ci-dessous des implémentations propres, prêtes à coller en Java, Python et C++.
Tous les trois fonctionnent dans **O(n)** temps et **O(n)** espace auxiliaire (piste) ou **O(1)** espace supplémentaire (version PD).

Langue Approche Complexité Remarques
- C'est quoi ?
#Java #Stack + sentinelle # O(n) / O(n) # Facile à lire, gère les cas bord avec sentinelle #
Python Exclusivité + sentinelle O(n) / O(n) Exclusivité Pythonique style monoligne
Utiliser deux tableaux entiers, mémoire minimale

> **Astuce** – Dans les entrevues, demandez à l'intervieweur quelle approche ils préfèrent : *stack* pour la clarté conceptuelle () ou *DP* pour l'efficacité spatiale ().

---

2.1 Java – Empiler avec Sentinel

"Java
***
* LeetCode 32 – Parentheses les plus valides
* Heure: O(n)
* Espace: O(n)
*/
solution de classe publique {
publique Parenthèses valides(String s) {
// index sentinelle -1 aide à calculer les longueurs sans cas particuliers
Pile <integer> = nouvelle pile<>();
Le paragraphe 2 est remplacé par le texte suivant:
Int maxLen = 0;

pour (int i = 0; i < s.longueur(); i++) {
c = s.charAt(i);
si c == '(') {
Le point i) est remplacé par le texte suivant:
} autres { // ' ) '
empile.pop(); // correspond ou enlève '('
si (stack.isEmpty()) {
stack.push(i); // nouvel indice de base
} autre {
maxLen = Math.max(maxLen, i - empil.peek());
}
}
}
retour maxLen;
}
}
«» "

---

2.2 Python – Stack avec Sentinel

'`python
# LeetCode 32 – Parentheses les plus valides
♪ Heure: O(n)
♪ Espace: O(n)

Solution de classe:
def le plus longValidParentheses(self, s: str) -> Int:
pile = [-1] # sentinelle
max_len = 0

pour i, ch dans le(s) énuméré(s):
Si ch == '(':
pile.annexe(i)
Autre: # ') '
Pile.pop()
si elle n'est pas empilée:
pile.append(i) # nouvelle base
Sinon:
max_len = max(max_len, i - pile[-1])

_retourner maxlen
«» "

---

#### 2.3 C++ – DP avec deux passes (O(1) Espace supplémentaire)

'`cpp
// LeetCode 32 – Parentheses les plus longues valides
// Heure: O(n)
// Espace : O(1) (seulement quelques entiers, pas des tableaux)

solution de classe {
public:
Int le plus longValidParentheses(chaîne s) {
int n = s.size(), maxLen = 0;
vecteur<int> dp(n, 0);

pour (int i = 1; i < n; ++i) {
si (s[i] == ') {
si (s[i-1] == '(') { // "...
dp[i] = (i >= 2 ? dp[i-2] : 0) + 2; // "...
} sinon si (i - dp[i-1] > 0 && s[i-dp[i-1]-1] == '(') {
dp[i] = dp[i-1] + 2 +
(i - dp[i-1] >= 2 ? dp[i-dp[i-1]-2] : 0);
}
maxLen = maxLen, dp[i];
}
}
retour maxLen;
}
};
«» "

> ** Pourquoi DP ? **
> L'approche DP garantit **O(1)** espace auxiliaire, mais il est un peu plus complexe à raisonner. La méthode de la pile est habituellement le choix convivial pour l'entrevue.

---

- Oui. 3. Billet de blog – Le bon, le mauvais, et le lamentable de longues parenthèses valides

### 3.1 Titre & Méta‐Description (SEO)

> **Titre** – LeetCode de maîtrise 32: Parentheses les plus valides – Stratégies, pièges et conseils d'entrevue
> **Description de la Meta** – Découvrez comment résoudre LeetCode 32 en Java, Python et C++. Comprendre les solutions de la pile par rapport au PDD, les cas courants et la façon d'assembler ce problème dans une entrevue technique. (en milliers de dollars)

3.2 Aperçu

1. **Introduction** – Pourquoi ce problème est un point de départ.
2. **Déclaration de problème** – Récapitulation rapide et contraintes.
3. **Approche naïve (Bad)** – Contrôle de la force Brute.
4. **Bien – La méthode de la pile** – Étape par étape, extrait de code, cas de bord.
5. **Bien – L'approche du PDD** – Comment ça marche, pourquoi il est O(1) espace supplémentaire.
6. **Les pièges communs** –
* Oublie l'index sentinelle.
* Erreurs hors pair dans les indices DP.
* Mauvaise interprétation de "bien formé" vs "équilibré".
7. **Stratégie d'entrevue** – Comment discuter de la complexité, poser des questions claires et montrer les compromis entre la pile et le PDD.
8. **Take‐aways & Practice** – Ressources, variations, et comment cette échelle à plus grands problèmes entre crochets.
9. **Conclusion** – Confiance et prochaines étapes.

3.3 Exemple de contenu du blog

> **Les bonnes**
> *Stack gagne* – Une simple pile contient des indices de caractères non appariés '('. Chaque fois que nous voyons un ')', nous sortons. Si la pile devient vide, nous poussons l'indice actuel comme une nouvelle base. Cela garantit que nous mesurons toujours une sous-chaîne valide par rapport à la dernière «(. (en milliers de dollars)
> *Le PD brille* – En stockant la longueur valide la plus longue se terminant à chaque indice, nous pouvons utiliser des valeurs calculées antérieurement pour étendre la correspondance actuelle. Il se sent plus «mathématique» et met en valeur vos côtelettes de programmation dynamique.

> **Les mauvais**
> L'approche de la force brute, qui vérifie la validité de toutes les sous-chaînes, explose rapidement à **O(n3)**. C'est un point de départ éducatif mais non viable pour 3 × 104 longueur d'entrée.

> **Les impies**
> De nombreux candidats oublient l'indice sentinelle, entraînant des indices négatifs ou des erreurs hors-par-un. Dans DP, la condition `i - dp[i-1] > 0` est facile à mélanger avec `>=`. Soyez méticuleux.

3.4 Crochet de fermeture

> Si vous clouez LeetCode 32, vous aurez un démarreur de conversation pour votre prochaine interview. Non seulement vous pouvez expliquer la logique de la pile en une minute, mais vous pouvez aussi pivoter vers DP si l'intervieweur demande l'optimisation de l'espace. Pratiquez ceci aujourd'hui, et vous serez prêt à impressionner à Meta, Google ou Amazon. (en milliers de dollars)

---

- Oui. 4. Comment utiliser ce poste pour la chasse à l'emploi

1. **Ajouter le blog à votre portfolio** – Organisez-le sur GitHub Pages ou sur votre site personnel.
2. **Partagez sur LinkedIn** – Écrire un court message de lien à l'article; utilisez des hashtags comme `#LeetCode`, `#SoftwareEngineering`, `#InterviewPrep`.
3. **SEO Boost** – Les tags meta ci-dessus le feront apparaître dans la recherche Google pour la solution entre parenthèses la plus longue valide.
4. **Afficher le code** – Joindre les trois implémentations linguistiques dans votre CV ou GitHub.
5. **Interview Drill** – Pratique expliquant la solution de la pile en moins de 2 minutes, puis discuter du compromis du PDD.

> **Conseil pro** – Dans les interviews, après avoir résolu le problème, demandez à l'intervieweur s'il préfère une pile ou une solution DP. Cela vous montre non seulement le codage, mais aussi une réflexion stratégique sur les compromis.

---

- Oui. 5. Mot final

*LeetCode 32* est plus qu'un problème difficile – c'est une vitrine de l'intuition de la structure des données et du codage propre. Avec les solutions ci-dessus et le blog, vous allez non seulement as la partie de codage, mais aussi se démarquer en tant qu'interviewé réfléchi. Bon codage, et la meilleure chance d'atterrir ce travail de rêve!