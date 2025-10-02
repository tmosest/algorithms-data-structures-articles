---
titre: LeetCode 2311. La plus longue séquence binaire inférieure ou égale à K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solution – Code dans **Java, Python et C++**

Voici une implémentation compacte et prête à la production pour LeetCode 2311 – *La plus longue séquence binaire inférieure ou égale à K*.
La même idée gourmande fonctionne pour les trois langues.

Langue Complexité Remarques
C'est quoi, ça ?
**Java** espaceUtilise `long` pour la valeur accumulée et les pouvoirs de deux. Autres
**Python** l'espace. Python's `int` est débordé – pas de soucis de débordement. Autres
**C++** L'espace utilise "long long" pour la sécurité. Autres

---

#### 1.1 Java

"Java
// LeetCode 2311 – Le plus long Subséquence binaire Moins Qual ou égal à K
solution de classe publique {
public int le plus longSujet(String s, int k) {
= 0; // tous les zéros peuvent toujours être pris
int = 0; // nombre de '1's sélectionnés
valeur longue = 0; // valeur numérique courante de la sous-séquence choisie
long pow = 1; // 2^position, en commençant par le bit le moins significatif

// 1/== Comptabiliser tous les '0' – ils n'augmentent jamais la valeur
pour [charc : s.toCharArray()) {
si (c == '0') zéros++;
}

2/ Scanner la chaîne de droite (le moins significatif) à gauche
pour (int i = s.longueur() - 1; i >= 0; i--) {
c = s.charAt(i);
si (c) «1») {
// peut-on ajouter ce bit sans dépasser k ?
si (valeur + pow <= k) {
valeur += pow;
les++;
}
}

// Passons au prochain bit (doublant la puissance de deux)
pow <<= 1;

// Si le prochain morceau est déjà > k, nous pouvons arrêter tôt
en cas de rupture (pow > k);
}

// Longueur totale = tous les zéros + les zéros sélectionnés
retour des zéros + des zéros;
}
}
«» "

---

#### 1.2 Python

'`python
# LeetCode 2311 – Le plus long Subséquence binaire Moins Qual ou égal à K
Solution de classe:
def leastSubséquence(s: str, k: int) -> Int:
zéros = s.count('0')
Nombre de personnes = 0
valeur = 0 # valeur courante des bits choisis
pow_ = 1 # 2^pos, à partir du bit le moins significatif

# Scanner de droite à gauche
pour ch en sens inverse(s):
si ch == '1':
si valeur + pow_ <= k:
valeur += pow_
+= 1
Pow_ <<= 1
si pow_ > k:
pause

retour zéros + un
«» "

---

*## 1.3 C++

'`cpp
// LeetCode 2311 – Le plus long Subséquence binaire Moins Qual ou égal à K
solution de classe {
public:
int le plus longSujet(chaîne s, int k) {
= 0;
longue valeur = 0, pow = 1; // pow = 2^pos

pour (charc : s) si (c == '0') zéros++;

pour (int i = (int)s.size() - 1; i >= 0; --i) {
Si (s[i]] '1') {
si (valeur + pow <= k) {
valeur += pow;
+ones;
}
}
pow <<= 1; // passer à la partie supérieure suivante
si (pow > k) rupture; // autres bits ne peuvent pas s'adapter
}
retour des zéros + des zéros;
}
};
«» "

Les trois solutions fonctionnent dans le temps **O(n)** et dans l'espace auxiliaire **O(1)**, en s'adaptant facilement aux contraintes du problème (`n ≤ 1000`, `k ≤ 109`).

---

- Oui. 2. Article du blog – *Le bon, le mauvais, le mauvais de LeetCode 2311*

> **Titre**
> La plus longue séquence binaire ≤ K: Un gemme de graisse pour votre prochaine interview

> **Description détaillée**
> Master LeetCode 2311 avec une solution simple et gourmande. Comprendre l'intuition, les pièges, et comment ce problème peut vous poser un travail technique. Code en Java, Python, C++.

---

2.1 Pourquoi ce problème se trouve-t-il

* **Entretien-Amis** – Il s'agit d'un problème classique de "greedy + bit manipulation". Les recruteurs adorent parce qu'il teste deux compétences de base :
1. *La pensée de Dieu* – pouvez-vous prouver que le choix des plus petites contributions d'abord est optimal?
2. *Connaissance du bit* – comprendre qu'une valeur de chaîne binaire dépend de deux puissances.

* **Exécution rapide** – Un seul passage sur la chaîne (O(n)) et la mémoire constante. Parfait pour les entrevues de codage haute pression où vous devez terminer en moins de 30 secondes.

* **Langue-neutrale** – Œuvres en Java, Python, C++, JavaScript, Allez, etc. Vous montre que la pensée algorithmique transcende la syntaxe.

* **Évoluable** – Même si les contraintes ballon (`n = 106` ou `k = 1018`), la logique gourmande reste la même. Vous devez seulement ajuster les types entiers (utiliser `long`/`long long`/`BigInteger`).

---

2.2 Ce que vous pourriez voyager (les méchants)

Pourquoi ça arrive ?
- Oui.
**Débit dans le calcul de la puissance** Dans les langues avec entiers de taille fixe, `pow <<= 1` peut déborder avant de vérifier `pow > k`. Autres
Oubliez que les zéros peuvent toujours être conservés – ils n'affectent pas la valeur mais augmentent la longueur. Autres Première passe pour compter zéros, ou les compter sur la mouche mais ne pas ajouter à la valeur. Autres
Le traitement de gauche à droite (le plus significatif au moins) échoue parce que vous pouvez verrouiller de grands bits tôt. Toujours itérer de ** de droite à gauche** (le moins significatif d'abord). Autres
**Off‐by‐one avec des indices de chaînes**= Mélange d'indices à base de 0 avec des positions de puissance à base de 1. Réserver `pow` à `1` (pour le dernier caractère) et déplacer chaque boucle. Autres
**En supposant que tous les bits s'intègrent dans `int`**" `k` peut être jusqu'à 109; les pouvoirs de deux peuvent dépasser cela rapidement. Utiliser `long`/`long` pour `valeur` et `pouvoir`. Autres

---

2.3 Les cas les plus odieux – Les causes qui rompent le code naïf

1. **Tous les zéros**
*Input:* `s = "0000", k = 1`
* Attendu :* 4 (prendre tous les zéros).
*Bug commun:* Code qui compte seulement ceux qui retourneront 0.

2. **K Plus petit que le plus petit peu**
*Input:* `s = "101", k = 0`
3 (tous zéros, aucun).
*Bug:* Ne pas s'arrêter lorsque `pow > k` peut conduire à des itérations inutiles.

3. **Maximum `k`**
*Input:* `s` longueur 1000, `k = 109`
*Bug:* `pow` peut dépasser 109 tôt, mais vous continuez à déplacer, risque de débordement.

4. **Les plus grands zéros en 's'**
*Input:* `"0000001", k = 1`
*Bug:* Certaines solutions interprètent mal les zéros de leader comme des bits significatifs et sautent incorrectement le `1` final.

Une solution robuste ** compte tous les zéros d'abord** et puis choisit avidement ceux-ci, cassant dès que le prochain bit ne correspond pas. C'est le cœur de la mise en œuvre *difficile* ci-dessus.

---

2.4 Preuve de l'optimalité – Argument de l'avidité

1. **Observation** – La valeur numérique d'une chaîne binaire est
\[
\text{value} = \sum_{\text{choisi bits } i} 2^{p_i}
\]
où `p_i` est la distance de bits de la droite (0-basée).

2. **Greedy Choice** – Supposez que vous ayez deux bits, `2^a` et `2^b` avec `a < b`.
Prendre `2^a` d'abord ne fait jamais mal car toute subséquence ultérieure qui prend `2^b` aura *au moins* la même longueur, mais la valeur est plus grande.

3. **Affaire sur l'échange** – Si une solution optimale choisit un plus grand peu avant un plus petit, l'échange garde la valeur ≤ k et **ne réduit pas** la longueur de subséquence.

4. ** Conclusion** – La stratégie optimale est : * garder tous les zéros*, puis **de droite à gauche** choisir un `1` seulement si sa contribution vous maintient ≤ k.

---

2.5 Tester votre solution

Source :
C'est pas vrai.
""11001"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" (2) → 5
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" Longueur = 2 zéros
Valeur 4 peut être formé comme `100`, tous les zéros ajouter la longueur
""111111""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Exécutez-les contre les extraits de code ci-dessus – vous verrez des résultats cohérents et corrects.

---

2.6 Ce que les recruteurs recherchent

* **Correctness** – Un candidat qui peut prouver l'optimalité gourmande et gérer tous les cas de bord.
* **Speed** – Les solutions O(n) sont essentielles ; un DP lent lèverait les drapeaux rouges.
* **Clean Code** – Effacer les noms de variables (`zeros`, `ones`, `pow`, `value`), les premières ruptures et les commentaires en ligne.
* **Discussion** – Parler à travers le *pourquoi* (pas seulement le *quoi*) montre une profonde compréhension.

---

#### 2.7 A emporter: Comment transformer ce problème en une étoile de rappel

1. ** Expliquez le choix de Greedy** – Nous essayons toujours d'ajouter le plus petit peu d'abord parce qu'un plus grand peu nous bloquerait plus tôt. (en milliers de dollars)
2. **Afficher la cartographie Bitwise** – Convertissez la chaîne en un nombre mentalement, illustrer avec un court exemple.
3. **Présentez le code** – Utilisez l'extrait ci-dessus, soulignez la logique de rupture.
4. **Complexité de la concentration** – temps O(n), espace O(1).
5. **Ajouter une démo rapide** – Utilisez un éditeur en ligne pour exécuter le code en direct, prouver qu'il fonctionne sur les entrées d'échantillon.

C'est exactement ce que les recruteurs de style attendent d'un candidat de premier ordre. Finissez le problème, vantez-le sur LinkedIn, et vous aurez un point de discussion concret pour votre prochain entretien technique.

---

2.8 Les derniers mots (les bons, les mauvais, les méchants)

*Bien:* Facile à comprendre, rapide, linguistique-agnostique.
*Bad:* Les dépassements et l'ordre de traitement sont des erreurs courantes.
*Les cas de bords impliquant tous les zéros ou très petits `k` peuvent trébucher le code naïf.

Avec la solution gourmande ci-dessus et l'explication amicale de l'interview dans cet article, vous êtes prêt à ace LeetCode 2311, impressionner les gestionnaires d'embauche, et peut-être même débarquer ce rôle de rêve technologique.

Bon codage ! C'est ce qu'il a dit