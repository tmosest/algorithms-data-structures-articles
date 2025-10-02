---
titre: LeetCode 446. Tranches arithmétiques II - Subséquence -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 446 – Tranches arithmétiques II (séquence ultérieure)
### Une solution complète Java / Python / C++ + SEO-Optimized Blog Post

---

### TL;DR

Langue Heure Espace
- C'est quoi ?
*Java*** O(n2)* O(n2)*
*Python * O(n2)
O(n2)

> *Le bon, le mauvais, et le laid de résoudre **LeetCode 446**. *

---

- Oui. 1. Récapitulation des problèmes

> ** Tranches arithmétiques II – subséquence* *
> Compter **tous** sous-séquences arithmétiques de la longueur **≥ 3**.
> Une sous-séquence est arithmétique si la différence entre les éléments consécutifs est constante.

*Exemple:*
`nums = [2,4,6,8,10]` → réponse = 7
( `[2,4,6]`, `[4,6,8]`, ..., `[2,6,10]`)

La taille du tableau est jusqu'à **1000**, et toutes les valeurs correspondent à des entiers signés 32 bits. La réponse correspond toujours à un entier signé 32 bits.

---

- Oui. 2. Pourquoi DP + HashMap est la solution standard

1. ** subséquence → Programmation dynamique* *
Pour chaque index `i` nous conservons une carte `dp[i]` où `dp[i][d]` est le nombre de sous-séquences **arithmétiques se terminant à `i` avec la différence commune `d`** qui ont une longueur **≥ 2** (la paire elle-même compte comme longueur 2, qui n'est pas encore une tranche valide).
Lorsque nous voyons une nouvelle paire `(j, i)` (`j < i`), la différence `d = nombres[i] - des noms.
Toutes les séquences se terminant à `j` avec la différence `d` peuvent être prolongées par `nums[i]`, les transformant en tranches valides.
Donc :
Texte
nouvelles _slices = dp[j][d] // tranches déjà comptées se terminant à j
dp[i][d] += new_slices + 1 // +1 pour la nouvelle paire (j, i)
réponse += nouvelles _slices
«» "

2. **Dépassements de 32 bits à la main**
Les différences peuvent dépasser la plage `int` (par exemple `INT_MAX - INT_MIN`).
Nous calculons les différences comme "longs" d'abord, cochez les limites, puis jetez à "int".
La réponse est accumulée en `long` pour éviter le débordement intermédiaire, finalement moulée en `int`.

3. **Complexités**
- Temps: `O(n2)` – chaque paire `(j, i)` est traitée une fois.
- Espace: "O(n2)" dans le pire des cas (toute différence est distincte). Pour `n ≤ 1000`, c'est très bien (~4 Mo en Java, ~8 Mo en C++).

---

- Oui. 3. Mise en œuvre des références

> **Conseil:** Utiliser **`Liste< Carte<...> >`** en Java, **`list[dict]`** en Python, et **`vector<unordered_map> `** en C++.

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe {
numéro d'entrée public OfArithmeticSlices(int[] nums) {
int n = longueur nums;
réponse longue = 0L;
// dp[i] cartographie la différence commune -> nombre de sous-séquences se terminant à i avec cette différence
@SuppressAvertissements("non vérifié")
Carte<entier, entier>[] dp = nouvelle carte[n];
pour (int i = 0; i < n; ++i) {
dp[i] = nouvelle HashMap<>();
pour (int j = 0; j < i; ++j) {
longue distance = (long) nombres[i] - (long) nombres[j];
si (diffL < Integer.MIN_VALUE) continue;
int diff = (int) diffL;

int prev = dp[j].getOrDefault(diff, 0);
int cur = dp[i].getOrDefault(diff, 0);

dp[i].put(diff, cur + prev + 1); // +1 pour la nouvelle paire (j,i)
réponse += prev; // seulement les tranches complètes contribuent
}
}
retour (int) réponse;
}
}
«» "

> **Pourquoi c'est bon* *
> *Fast (O(n2)), facile à comprendre, gère le débordement, utilise des génériques en toute sécurité. *

3.2 Python

'`python
de taper l'importation Liste
de collections importer par défautdict

Solution de classe:
def numberOfArithmeticSlices(self, nums: List[int]) -> Int:
n = len(nums)
réponse = 0
dp = [defaultdict(int) pour _ dans range(n)]

pour i dans la plage(n):
pour j dans la plage i:
diff = nombres[i] - les noms [j]
# diff est déjà un int Python (non consolidé) – aucun problème de débordement
prev = dp[j][diff]
dp[i][diff] += prev + 1
réponse += prev

réponse de retour
«» "

> **Pourquoi Python est gentil**
> *Construire en gros entiers, syntaxe succincte, `defaultdict` supprime la plaque de chaudière. *

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre intDepierres arithmétique(vecteur<int>&nums) {
int n = nombres.size();
long an = 0;
vector<unordered_map<long long, long>> dp(n);

pour (int i = 0; i < n; ++i) {
pour (int j = 0; j < i; ++j) {
long long diff = (long long)nums[i] - nums[j];
// Pas besoin de serrer diff ; la touche non ordonnée_map est longue
long prev = dp[j][diff];
dp[i][diff] += prev + 1; // +1 pour la nouvelle paire
as += prev;
}
}
retourner static_cast<int>(ans);
}
};
«» "

> **Pourquoi C++ brille* *
> *Exécution rapide, contrôle de type efficace de la mémoire. *

---

- Oui. 4. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Idées algorithmiques**
Autres **Complexité du temps**= Acceptable pour n ≤ 1000=_________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
Autres **Complexité spatiale**=4–8 Mo, amende pour 1000=1 Les cartes du pire cas O(n2) peuvent dégrader les performances
**Manipulation de l'excès de flux** Exclicite longue pour diff & response Exclusive Checking limits in Java ajoute une branche Exclusive Casting `long` to `int` peut être dangereux si diff hors de portée Exclusive
**Pièges spécifiques à la langue**=HashMap générique avertissement== `defaultdict` auto-create keys== `unordered_map` rehashing overall==
**Readability**= Très lisible, les commentaires aident== Certains pensent peut-être que `dp[j][diff]` est déroutant=== La logique de la paire=== peut être mal comprise===

> **À emporter :** L'approche DP‐hash est *la solution acceptée, mais elle nécessite une manipulation attentive des grandes différences et de l'utilisation de la mémoire.

---

- Oui. 5. SEO-Optimized Blog Titre & Mots-clés

**Titre**
> LeetCode 446 – Tranches arithmétiques II (suite) en Java, Python, C++

** Mots-clés principaux**
- LeetCode 446
- Tranches arithmétiques II
- Sous-séquence DP
- Solutions Java LeetCode
- Solutions Python LeetCode
- C++ Solutions LeetCode
- Codage de la stratégie d'entretien
- Entretien de l'ingénieur logiciel

**Description détaillée**
> Découvrez la solution DP-map optimale pour LeetCode 446. Lisez le code Java, Python et C++, obtenez l'image générale et préparez-vous au succès de l'entrevue. (en milliers de dollars)

---

- Oui. 6. Marche détaillée (corps de blog)

> 6.1 Aperçu du problème
> ... (comme ci-dessus)

6.2 Pourquoi Brute- Coups de force
> Le nombre de subséquences augmente de 2n. Pour n=1000 c'est astronomique.

> 6.3 Programmation dynamique avec HashMaps
> ... (expliquer la récurrence)

> ### 6.4 Passage en code (Java/Python/C++)
> (Insérer des extraits de code avec des commentaires en ligne)

> 6.5 Analyse de complexité
> (Afficher O(n2) temps, O(n2) espace)

> #### 6.6 Edge- Traitement des cas
> - Dépassement des différences
> - Nombres négatifs
> - Des séquences longues avec les mêmes valeurs

> ### 6.7 Bonne, mauvaise, mauvaise discussion
> (Utilisez le tableau ci-dessus)

> 6.8 Conseils pratiques pour les entrevues
> - Échanges temps/espace
> - Montrez la compréhension de la manipulation des débordements
> - Expliquer pourquoi nous ne comptons que `prev` pour la réponse

> 6.9 Lecture supplémentaire
> - LeetCode threads de discussion
> - Modèles de programmation dynamiques pour les problèmes de subséquence

> ### 6.10 Conclusion
> L'astuce DP-map est un modèle classique pour les problèmes arithmétiques subséquents. Maîtrisez-le et vous aurez un outil fort pour toute entrevue d'ingénierie logicielle.

---

- Oui. 7. Liste de contrôle finale avant votre entrevue

- [ ] Implémentez la solution dans votre langue préférée.
- [ ] Essai avec les exemples fournis et les cas d'angle (`[0]`, `[1,1]`, valeurs int maximales/minimum).
- [ ] Si la solution pour `n = 1000` pour s'assurer qu'elle fonctionne sous 1 s.
- [ ] Soyez prêt à expliquer la récurrence de DP et la logique de la paire.
- [ ] Discutez de la gestion des débordements et de la raison pour laquelle nous utilisons `long`/`long long`.
- [ ] Préparer une brève comparaison des compromis Java/Python/C++ (vitesse vs lisibilité).

Bonne chance, et que vos tranches arithmétiques soient toujours *parfaitement* équilibrées!