---
titre: LeetCode 1090. Les plus grandes valeurs des étiquettes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Réponse courte**

Vous pouvez transférer la solution JavaScript vers Java presque ligne par ligne.
Les seules choses que vous devez changer sont:

Pourquoi ?
C'est le cas.
"const" "final" (ou aucun mot clé) "Java n'a pas "const". Autres
Une déclaration variable normale («int», «String», ...)
"=>` fonction" `() ->` dans lambda, ou une méthode normale
"Array.prototype.sort" "Collections.sort" ou "Arrays.sort"
"map.hasKey()"" `map.contientKey()""
"map.getOrDefault(key, 0)"""map.getOrDefault(key, 0)" (même)"
"retour"
"Push"

Ci-dessous se trouve une implémentation Java **minimum, idiomatique** qui suit la même logique que votre solution JavaScript.

"Java
Importation de java.util.*;

***
* Les plus grandes valeurs des étiquettes
* (Code Leet 2291)
*
* L'implémentation Java reflète la logique du JavaScript
* solution que vous avez postée:
*
1. Construisez une liste des paires (étiquette, valeur).
2. Trier cette liste par valeur (en déclin).
* 3. Choisissez avec plaisir les articles les plus évalués, en respectant:
* – une limite globale (numWanted)
* – une limite par étiquette (useLimit)
*
* Toutes les structures et opérations de données sont Java standard:
* - Liste/ArrayList
* - Collections.sort avec un comparateur
* - Carte <String,integer> pour les compteurs d'étiquettes
*/
solution de classe publique {

***
* Aide à l'avidité qui choisit les meilleurs articles pour une seule étiquette.
*
* @param valeurs triées en ordre décroissant
* Utilisation @param Limiter le nombre de fois où une étiquette peut être utilisée
* @param num Nombre souhaité d'articles que nous devons encore choisir
* @retour [somme des valeurs cueillies, restant numWanted]
*/
privé long[] cupidy(int[] valeurs, int useLimit, int numWanted) {
somme longue = 0;
limite int = Math.min(useLimit, numWanted);

pour (int i = 0; i < limite; i++) {
la somme += valeurs[i];
}

numWanted -= limite;
retour de nouveau long[]{sum, numWanted};
}

public long plus grandValues(int[] valeurs, chaînes[] étiquettes,
int numWanted, int useLimit) {
int n = valeurs.longueur;

// Construire une liste de paires (étiquette, valeur)
Liste des paires <Pair> = nouvelle liste <>(n);
pour (int i = 0; i < n; i++) {
pair.add(nouvelle paire(étiquettes[i], valeurs[i]);
}

// Tri des paires par valeur descendante
pair.sort(a, b) -> Integer.compare(b.value, a.value));

// Compter combien de fois chaque étiquette a été utilisée
Carte <String, Integer> utilisée = nouvelle HashMap<>();
long total = 0;
int restant = num Recherché;

pour (Paire p : paires) {
si (rester) 0) pause;

Int utilisé Cnt = used.getOrDefault(p.label, 0);

si (usedCnt < useLimit) { // nous pouvons encore utiliser cette étiquette
Total += p. valeur;
used.put(p.label, usedCnt + 1);
restant--;
}
}

le total des retours;
}

*** Support de données simple pour une paire d'étiquettes/valeurs */
Paire de classe statique privée {
finale Étiquette à cordes;
valeur finale int;
Paire(Étiquette de fixation, valeur int) {
Ça. étiquette = étiquette;
Ça. valeur = valeur;
}
}
}
«» "

- Oui. Comment il correspond à la version JS

JS-Java Explication
- Oui.
"values.map((v, i) => [labels[i], v])"""Construisez `Liste<Pair>"" Java n'a pas de tableau de distribution; utilisez une petite classe. Autres
"arr.sort((a,b)=> b[1] - a[1])"""pairs.sort(a,b) -> Integer.compare(b.value,a.value)" Le comparateur trie par la valeur numérique. Autres
`const cnt = new Map();`= `Map<String,Integer> utilisé = new HashMap<>();`= Java `Map` remplace JavaScript `Carte`.
`cnt.get(...)` / `cnt.set(...)```used.get(...)` / `used.put(...)` Même idée. Autres
Pour (const [étiquette, val] d ' arr) Il faut passer par la liste triée. Autres
La même logique. Autres
Le type de retour est `long` parce que la somme peut dépasser `int`.

Exécution

* **Time**: `O(n log n)` en raison du tri; le scan gourmand est linéaire.
* **Espace**: `O(n)` pour la liste `Pair` et la `Carte`.

Les deux versions ont le même comportement asymptotique ; l'implémentation Java est plus sûre de type et plus facile à lire une fois que vous êtes habitué à la syntaxe Java.