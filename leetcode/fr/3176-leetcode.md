---
titre: LeetCode 3176. Trouvez la longueur maximale d'une bonne séquence I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Trouver la longueur maximale d'une bonne séquence (Code Leet 3176)

> **TL;DR** – Utilisez un PDD * bidimensionnel* qui garde la meilleure longueur possible pour chaque *nombre de pauses autorisées* (`k`) et *dernière valeur* vue.
> **Complexité** – temps "O(n·k)", espace "O(n·k)" (= 500 × 25).
> **Langues** – Java, Python, C++.

---

- Oui. 1. Récapitulation des problèmes

On vous donne un tableau entier `nums` (taille ≤ 500) et un entier non négatif `k` (25).
A **bonne** subséquence "seq" satisfait:

«» "
# de i en [0,0]seq=2] tel que seq[i] != seq[i+1] ≤ k
«» "

En d'autres termes, la subséquence peut contenir au maximum `k` =breaks= entre des éléments égaux consécutifs.
Retournez le *longueur maximale possible* d'une telle séquence.

---

- Oui. 2. Pourquoi un DP sur "k" et "last value" fonctionne

Si nous balayons `nums` de gauche à droite, à chaque étape nous devons décider si **prendre** l'élément actuel dans la séquence ou **skip**.

* Lorsque nous le prenons, deux cas se présentent :
* **Pas de nouvelle pause** – l'élément précédent de la séquence est égal à l'élément actuel.
→ `breaks` reste le même.
* **Nouvelle pause** – l'élément précédent est différent et nous sommes autorisés à utiliser une pause de plus (`k > 0`).
→ `breaks` augmente d'un seul.
* Quand nous la sautons, rien ne change.

La réponse optimale pour un préfixe dépend uniquement de:
1. Combien de pauses nous avons utilisées jusqu'à présent ( 'i').
2. Qu'est-ce que la valeur **dernière** dans la séquence (`a`), parce que seule cette valeur décide si une nouvelle pause serait nécessaire.

Nous pouvons donc maintenir

«» "
dp[i][a] = longueur maximale d'une bonne séquence observée jusqu'à présent
qui utilise exactement i casse et se termine avec valeur a
«» "

Pendant l'analyse, nous mettons à jour `dp` dans l'ordre *reverse* de `i` (pour éviter de réutiliser l'élément courant dans la même itération).

---

- Oui. 3. La transition du PDD

Pour chaque élément «a» en «nums»:

«» "
pour i de k à 0
// Option 1: poursuivre la course en cours (pas de nouvelle pause)
cand1 = dp[i][a] + 1

// Option 2: lancer une nouvelle course avec un nombre différent
// (seulement si nous avons une valeur précédente et que nous avons encore des pauses à gauche)
Cand2 = (i > 0) ? res[i-1] + 1 : 0

dp[i][a] = max(dp[i][a], cand1, cand2)
res[i] = max(res[i], dp[i][a]) // res[i] = meilleure longueur pour toute dernière valeur
«» "

"res[i]" conserve la meilleure longueur sur *toutes* dernières valeurs pour un `i` fixe, qui est nécessaire pour `cand2`.
Après avoir traité tout le tableau, la réponse est `res[k]`.

---

- Oui. 4. Code – Java

"Java
Importation de java.util.*;

solution de classe {
valeur maximale de longueur(int[] nums, int k) {
// dp[i] – carte de la dernière valeur à la meilleure longueur avec i breaks
@SuppressAvertissements("non vérifié")
Carte<entier,entier>[]dp = nouveau HashMap[k + 1];
pour (int i = 0; i <= k; i++) dp[i] = nouvelle HashMap<>();

int[] res = nouvelle int[k + 1]; // meilleure longueur pour chaque i sur toutes les dernières valeurs

pour (int a : nombres) {
pour (int i = k; i >= 0; i--) {
int v = dp[i].getOrDefault(a, 0);
// Poursuivre l'exécution
v = Math.max(v + 1, (i > 0 ? res[i - 1] + 1 : 0));
dp[i].put(a, v);
res[i] = Math.max(res[i], v);
}
}
retour [k];
}

// Pilote rapide pour les tests locaux
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.maximumLength(nouvelle int[]{1,2,1,3}, 2)); // 4
Système.out.println(s.maximumLength(new int[]{1,2,3,4,5,1}, 0)); // 2
}
}
«» "

---

- Oui. 5. Code – Python

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maximumLength(self, nombres: List[int], k: int) -> Int:
# dp[i] – dict: dernière valeur -> meilleure longueur avec i cass
dp = [defaultdict(int) for _ in range(k + 1)]
res = [0] * (k + 1) # meilleure longueur pour chaque i sur toutes les dernières valeurs

pour les nombres:
pour i dans la plage(k, -1, -1):
Option 1: poursuivre la course
val = dp[i][a] + 1
# Option 2 : nouvelle pause
i > 0:
val = max(val, res[i - 1] + 1)
dp[i][a] = valeur
res[i] = max(res[i], val)

retour res[k]

# Pilote rapide pour les tests locaux
si __nom__ == "__main__" :
s = Solution()
print(s.maximumLongueur([1, 2, 1, 1, 3], 2)) # 4
print(s.maximumLongueur([1, 2, 3, 4, 5, 1], 0) # 2
«» "

---

- Oui. 6. Code – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maximum Longueur(vecteur<int>& nums, int k) {
// dp[i] – non ordonné_map: dernière valeur -> meilleure longueur avec i cass
vector<unordered_map<int,int>> dp(k + 1);
vector<int> res(k + 1, 0); // meilleure longueur pour chaque i sur toutes les dernières valeurs

pour (int a : nombres) {
pour (int i = k; i >= 0; --i) {
int val = dp[i][a] + 1; // continuer la course
Si (i > 0) val = max(val, res[i - 1] + 1); // nouvelle pause
dp[i][a] = valeur;
res[i] = max(res[i], val;
}
}
retour [k];
}
};

// Pilote rapide pour les essais locaux
Int main() {
Solution s;
durée maximale({1, 2, 1, 1, 3}, 2) << finl; // 4
durée maximale({1, 2, 3, 4, 5, 1}, 0) << finl; // 2
retour 0;
}
«» "

---

- Oui. 7. Les bons, les mauvais et les méchants

Qu'est-ce qui a marché Pourquoi ça compte
- C'est quoi ?
Autres **Bon – Intuitif DP**L'état (breaks used, last value)» capture exactement ce dont nous avons besoin. Conserve la solution à la fois simple et efficace ('O(nk)'). Autres
Autres **Bien – Sauvage de l'espace au lieu d'une table pleine `n × k` réduit la mémoire à tout au plus `k × distinct(valeurs)` (=25 × 500). Il gère la gamme de valeurs 10^9 sans grandes tables de hachage. Autres
Autres **Bad – Edge Cases**= Lorsque `k = 0`, la transition doit sauter `res[-1]`. Le code s'occupe explicitement de cela. Autres
Autres **Bad – Inverser la boucle**. Une boucle avant rompt la justesse. Évite d'utiliser le même élément deux fois dans un seul passage. Autres
Autres **Ugly – Large `k`**. Si `k` était plus grand (par exemple 500), l'algorithme se dégraderait en `O(n^2)` ou utilisez trop de mémoire. Le problème limite délibérément le "k ≤ 25". Autres
Autres **Ugly – Implementation Detail**.Certaines langues (par exemple Java) nécessitent des astuces d'effacement de type pour les tableaux génériques. La plaque de chaudière cachée peut distraire du noyau algorithmique. Autres

---

- Oui. 8. Résumé optimalisé du SEO pour les entrevues d'emploi

- **Mots clés**: LeetCode, Bonne séquence, DP, Programmation dynamique, Interview, Codage Interview, Algorithme, Python, Java, C++
- **Description détaillée**: Master LeetCode 3176 – Longueur maximale d'une bonne séquence. Apprenez une solution O(n·k) DP en Java, Python et C++. Parfait pour votre prochaine interview en génie logiciel. (en milliers de dollars)
- **H1**: Programmation dynamique – LeetCode 3176 Bonne séquence
- **Call‐to‐Action**: Vous souhaitez obtenir une note plus élevée dans les entrevues de codage? Essayez de mettre en œuvre ce DP efficace dans votre langue préférée aujourd'hui! (en milliers de dollars)

---

- Oui. 9. Réflexions finales

LeetCode 3176 est une grande aire de jeux pour présenter:

1. **Décomposition du problème** – choisir le bon état DP.
2. **Handling Large Ranges** – avec des cartes de hachage au lieu de tableaux denses.
3. **Idiomes spécifiques à la langue** – utilisation efficace des cartes en Java, Python, C++.

Si vous pouvez expliquer le PDD en **moins de 2 minutes** et remettre le code ci-dessus dans une entrevue d'emploi, vous démontrerez à la fois *perspective algorithmique* et *mise en oeuvre propre* – exactement ce que les intervieweurs recherchent. Bon codage !