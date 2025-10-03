---
titre: LeetCode 691. Stickers pour épeler le mot -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 691 – **Stickers pour épeler le mot**

> ** Exposé des problèmes (abréviation)* *
> Vous avez une offre illimitée de *n* différents autocollants.
> Chaque autocollant est un mot anglais minuscule.
> En utilisant les lettres sur les autocollants (vous pouvez couper n'importe quelle lettre de n'importe quel autocollant, les réarranger, et vous pouvez réutiliser un autocollant n'importe quel nombre de fois) vous devez épeler une chaîne *cible* donnée.
> Retournez le nombre *minimum* d'autocollants requis ou **‐1** s'il est impossible.

- Oui.
-- -- -- -- -- --
1 ≤ n ≤ 50
1 ≤ ≤ 10
**Longueur de la cible**
** tous les caractères** Autres

> **Pourquoi ça compte**
> Les contraintes semblent petites, mais le problème est difficile NP.
> Les intervieweurs adorent ce problème car il vous force à penser à *représentation d'état* (bitmask, string, freq array) et *search* (BFS, DFS + mémoization, DP).

---

- Oui. 2. Aperçu de la solution

La méthode standard la plus facile à retenir est une méthode **Breadth‐First Search (BFS)** sur *remaining target strings*.

1. **Trier** chaque autocollant et la cible alphabétiquement.
Ceci permet à l'opération `filter()` d'exécuter dans *O(-cible) +-sticker* en scannant les deux chaînes triées.
2. Placez la cible triée dans une file d'attente.
Chaque niveau de la BFS représente l'utilisation d'un autre autocollant.
3. Pour chaque état, essayez chaque autocollant :
*Utilisez `filter()`* – supprimer les lettres que l'autocollant peut couvrir.
*Si rien ne reste → nous sommes fait* (profondeur actuelle + 1 autocollants).
*Si nous ne l'avons pas vu avant.
4. Si la file vide → impossible → retourne **‐1**.

Le BFS garantit que la première fois que nous atteignons une chaîne vide, nous avons utilisé le nombre minimal d'autocollants.

---

- Oui. 3. Code

### 3.1 Java – BFS (la solution de Gangjig)

"Java
Importation de java.util.*;

solution de classe {
public int minStickers(String[] autocollants, String cible) {
int n = autocollants. longueur;

// Trier chaque autocollant et la cible
cible = triChars(cible);
pour (int i = 0; i < n; ++i) autocollants[i] = triChars[i];

Queue<String> q = nouvelle liste liée<>();
Set<String> visité = nouveau HashSet<>();

q.offre(cible);
Étapes int = 0;

alors que (!q.isEmpty()) {
taille int = q.size();
steps++; // nous utilisons encore un autocollant
pendant que (taille-- > 0) {
Chaîne cur = q.poll();
pour (String strand : autocollants) {
Chaîne nxt = filtre(cur, st);
si (nxt.isEmpty()) les étapes de retour;
si (!nxt.equals(cur) && visited.add(nxt)) {
q.offre(nxt);
}
}
}
}
retour -1; // impossible
}

// Retirer les lettres de m d'un, triées
Filtre à cordes privé(String a, String b) {
StringBuilder sb = nouveau StringBuilder();
int j = 0; // pointeur dans b
pour (charc : a.toCharArray()) {
booléen trouvé = faux;
pendant que (j < b.longueur() && b.charAt(j) <= c) {
si (b.charAt(j++) == c) { // consommer cette lettre
trouvé = vrai;
pause;
}
}
si (!found) sb.append(c);
}
retour sb.toString();
}

Chaîne privée Chars(String s) {
char[] arr = s.toCharArray();
Tableau 3.
retourner la nouvelle chaîne(arr);
}
}
«» "

**Complexités* *

- Oui.
-- -- -- -- -- --
**Temps**="O( 2^m * n * m )" (faible cas, *m* = longueur cible) – mais pratiquement rapide pour *m* ≤ 15. Autres
**L'espace**"O( 2^m)" pour les États visités (le pire cas). Autres

---

#### 3.2 Python – Mémorisé DFS / DP (bit-masque)

L'implémentation Python utilise une mémoisation *récursive* avec un **bitmask** des caractères cibles restants.
C'est l'approche la plus concise mais la plus efficace.

'`python
Solution de classe:
def minStickers(self, autocollants: list[str], cible: str) -> Int:
à partir de functools importer lru_cache

# Autocollants préprocédés en compteurs de fréquence
m = len(cible)
cible_lettres = list(cible)

# Construire une liste de masques autocollants (bitmasque de lettres qu'il peut fournir)
masques = []
pour m en autocollants:
masque = 0
pour ch dans l'ensemble(s):
masque= 1 << (ord(ch) - 97)
masques.annexe(masque)

@lru_cache(Aucun)
def dfs(état: int) -> Int:
si état == 0:
retour 0
ans = flotteur('inf')
Essayez chaque autocollant
pour masques:
Si l'autocollant ne couvre aucune lettre nécessaire, sautez
si masque & état == 0:
poursuivre
# Construire un nouvel état après avoir utilisé ce sticker
nouvelle_état = état
pour i, ch dans énumérer(cible_lettres):
si l'état & (1 << i) et (masque & (1 << (ord(ch) - 97))):
nouvelle_état &= ~(1 << i)
ans = min(ans, 1 + dfs(nouvel_état))
retour et

res = dfs(1 << m) - 1)
retour -1 si res == float('inf') sinon res
«» "

**Complexités* *

- Oui.
-- -- -- -- -- --
**Temps** (m ≤ 15 > 32 768 états)
**Space**="O( 2^m )" pour mémoisation + pile de récursion="

---

### 3.3 C++ – PDD avec Bitmask (itatif)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minStickers(vecteur<string>& autocollants, cible de chaîne) {
int m = cible.size();
Int pleine = (1 << m) - 1;

// Masques autocollants précalculés
vecteur<int> masques;
pour (auto et st : autocollants) {
masque int = 0;
pour (charc : m) masque= 1 << (c - 'a');
masques.push_back(masque);
}

INF = 1e9;
vecteur<int> dp(1 << m, INF);
dp[0] = 0; // aucune lettre nécessaire → 0 autocollants

pour (état int = 0; état <= complet; état ++) {
si (dp[state] == INF) continuer;
pour (int smask : masques) {
int new_state = état;
// Essayez de couvrir chaque lettre restante avec ce sticker
pour (int i = 0; i < m; ++i) {
si (!(état & (1 << i))) continuer; // déjà couvert
si (smask & (1 << (cible[i] - 'a')))
nouveau_état &= ~(1 << i); // supprimer
}
dp[new_state] = min(dp[new_state], dp[state] + 1);
}
}
retour dp[full] == INF ? -1 : dp[full];
}
};
«» "

**Complexités* *

- Oui.
-- -- -- -- -- --
**Temps**="O( 2^m * n * m )" – avec *m* ≤ 15 toujours rapide="
**L'espace**

---

- Oui. 4. Article de blog
*(SEO-optimized – "Stickers to Spell Word" + "LeetCode 691" + "Interview Prep"*

---

Les bons, les mauvais et les méchants *

> **Mots clés** – *LeetCode 691*, *Stickers to Spell Word*, *DP bitmask*, *BFS solution*, *coding interview*, *algorithm interview questions*, *job interview conseils*, *Java BFS*, *Python DP*, *C++ bitmask*.

---

C'est vrai. Quel est le problème ?

On vous donne une poignée d'autocollants, chacun un petit mot.
Votre objectif : ** Coupez des lettres** de ces autocollants (vous pouvez couper *toute* lettre, les réorganiser et utiliser des autocollants n'importe quel nombre de fois) pour épeler un mot cible.

*Retourner le nombre minimal d'autocollants nécessaires ou -1 s'il ne peut pas être fait. *

---

C'est pas vrai. Pourquoi est-ce si important dans les entrevues?

- **Profondeur algorithmique**: Il touche à *compression d'état*, *bitmask DP*, *BFS sur cordes* – tous les concepts de base interviewers aiment.
- ** Pensée de cas** : Vous devez considérer *les lettres non recouvrables*, *les autocollants dupliqués*, *la couverture de recouvrement*.
- **Offre d'espace temporel**: Le résoudre naïvement peut exploser; trouver une représentation intelligente et compacte est la clé.

Si vous clouez cette question, vous impressionnerez les recruteurs avec *codage* et *design* côtelettes.

---

- Oui. Le bon – Intuition et ce qui fonctionne

1. **Trier pour simplifier la correspondance* *
Tri des autocollants et la cible vous permet d'exécuter `filter()` dans le temps linéaire.
Pas de boucles imbriquées sur les personnages – seulement deux pointeurs.

2. **BFS garantit une optimisation* *
Chaque couche de BFS représente *en utilisant un autre autocollant*.
La première fois que nous avons touché une chaîne cible vide est la réponse.

3. **Compression de l'état avec des bits* *
Les solutions DP Python et C++S compressent les lettres restantes en un seul entier (`1 < < m`).
Seulement 2^15 = 32.768 états – minuscules et rapides.

4. **Récursion des coupes de mémoire**
Dans Python, `@lru_cache` stocke des résultats pour chaque sous-problème, transformant un DFS exponentiel en une recherche gérable.

---

- Oui. Les mauvaises – pièges communs

Pourquoi il échoue
- C'est quoi ?
Autres **L'utilisation d'une file d'attente de chaînes de caractères **Les chaînes de caractères peuvent être longues (jusqu'à 15 caractères) et de nombreux duplicatas – l'explosion de la mémoire. Utilisez *chaînes triées* + un `Set` pour suivre les visites. Autres
**L'autocollant recomputant masque chaque appel DFS**. Pré-calculez un bitmask par autocollant une fois. Autres
**Ignorer les autocollants duplicata**=Vous pourriez perdre du temps à explorer à nouveau le même autocollant. Dupliquer les autocollants ou utiliser un ensemble de masques. Autres
Autres **Caisse de base de Wong dans DFS**. Cas de base: "État". 0 → 0 autocollants`. Autres
**Ne pas traiter des cas impossibles** . Le retour de `float('inf')` directement peut causer un débordement. Après DP, vérifier `INF` et retourner -1.

---

C'est pas vrai. L'horrible – Quand la complexité devient sauvage

Si vous essayez naïvement de générer **toutes les combinaisons** d'autocollants, vous allez créer des arbres de recherche *exponentielle* :

- Chaque état de chaîne peut se brancher dans des autocollants *n* → chemins `O(n^m)`.
- Sans masque intelligent ou astuce triée, vous aurez le temps de ne pas atteindre de cibles plus grandes.

**Solution**:
Gardez votre *state representation* serré (bitmask ou chaîne triée) et évitez le travail en double.
C'est la sauce secrète pour transformer le "gugly" en "efficace".

---

Vite Début : Quelle langue préférez-vous ?

Qu'est-ce que vous allez apprendre ?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Java (BFS)** Autres
**Python (DP)** Autres
**C++ (pDD implicite)**

Choisissez celui qui correspond à votre pile d'entrevue.

---

C'est vrai. Finale Pensée : Afficher *Design* Pas seulement *Mise en œuvre*

Lors d'une entrevue en direct :

1. ** Expliquer la représentation de l'État** (pourquoi bitmask? Pourquoi trier les cordes?)
2. **Passer à travers les couches BFS** – mettre l'accent sur l'optimalité.
3. **Élagage et mémorisation de Mention** – montrez que vous connaissez l'échange espace-temps.
4. **Boîtes de bord à poignée** – test des scénarios impossibles et à lettre unique.

Vous allez transformer cette question de codage en un récit ** animé par la conception** que les recruteurs aiment.

---

À emporter

- LeetCode 691 est *une des meilleures questions d'entrevue pour *demandeurs d'emploi*.
- Utilisez **BFS** avec des chaînes triées *ou* **bitmask DP** avec mémoisation.
- Gardez le code propre, les états petits, et les cas de base correct.

---

> ** Prêt à s'entraîner ? **
> Clone la repo, exécute les solutions Java, Python et C++, et teste les cas de test officiels de LeetCode.
> Lorsque vous êtes à l'aise, ajoutez une étape *deduplication* et essayez de réduire encore la mémoire – c'est comment vous allez de *bon* à *grand*.

Bon codage ! Les

---

* (fin de l ' article)*

---

- Oui. 5. Conclusion

- Oui. Nous avons couvert trois solutions idiomatiques : Java BFS, Python mémorisé DFS, C++ iterative DP.
- L'implémentation Java est un favori de l'interview du monde réel – concis, rapide et facile à expliquer.
- Les extraits de Python et C++ mettent en évidence la puissance de la compression de l'état de *bitmask* – le truc algorithmique ultime pour LeetCode 691.
- Oui. L'article de blog explique pourquoi le problème compte, comment éviter les pièges, et comment encadrer votre réponse pour les recruteurs.

Joyeux entretien, et que vos offres d'emploi viennent *dans le bon nombre d'autocollants*