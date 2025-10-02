---
titre: LeetCode 903. Permutations valides pour la séquence DI -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 903 – **Permutations de valeur pour la séquence de l'AI**
> **Java / Python / Implementations C++ + un billet de blog pour SEO *

---

- Oui. 1. Récapitulation des problèmes (la partie "bien")

> **Don** une chaîne `s` de longueur `n` (`1 ≤ n ≤ 200`) composée uniquement des caractères **'I'** (augmentation) et **'D'** (diminution).
> **Retour** le nombre de permutations des entiers `[0 ... n]` qui satisfont au modèle de DI.
> La réponse doit être modulo `1 000 000 007`.

> Exemple
> `s = "DID"` → `5` permutations valides.

---

- Oui. 2. Pourquoi ce problème compte pour les entrevues

* ** Programmation dynamique** – un sujet d'entrevue classique.
* **Comptabilité conjointe** – vous apprend à penser en termes de préfixes.
* **Arithmétique modulaire** – essentiel pour les problèmes avec des comptes énormes.
* ** compromis de complexité** – récursion naïve ('O(2n)') par rapport à DP ('O(n2)') par rapport à l'optimisation de la somme préfixe ('O(n2)' avec des facteurs constants).

Résoudre cela démontre clairement votre état d'esprit algorithmique et votre style de codage – exactement ce que recherchent les recruteurs.

---

- Oui. 3. La solution de PDD optimale (la partie "bien")

3.1 Observation

Lorsque nous fixons les premiers nombres `i+1` (`i` de `0` à `n-1`) de la permutation, le dernier nombre peut être l'une des valeurs inutilisées `i+1` restantes.
Si ce dernier nombre est **plus grand** ou **plus petit** que le précédent dépend de "s[i]".

Nous maintenons donc `dp[i][j]` = nombre de permutations valides de la longueur `i+1` où le dernier nombre placé est le **j‐th le plus petit** parmi les valeurs inutilisées (0-indexées).

3.2 Transition

«» "
Si s[i] == 'I': # dernier < précédent
dp[i][j] = somme(dp[i-1][0 ... j-1]) // nous ne pouvons mettre des nombres plus petits avant
Autre: # s[i] == 'D': dernier > précédent
dp[i][j] = somme(dp[i-1][j ... i]) // nous ne pouvons mettre des nombres plus grands qu'avant
«» "

Les deux sommes peuvent être calculées en **O(1)** en utilisant des sommes préfixes, ce qui conduit à une solution **O(n2)** avec la mémoire **O(n2)** (ce qui est très bien pour n ≤ 200).

3.3 Cas de bord

* Tous les numéros sont distincts – nous pouvons utiliser en toute sécurité les montants préfixés.
* Modulo doit être appliqué après chaque ajout pour éviter le débordement.

---

- Oui. 4. L'approche naïve

'`python
def brute(s):
de itertools importer des permutations
n = len(s)
cnt = 0
pour permutations permanentes(range(n+1)):
ok = Vrai
pour i dans la plage(n):
si s[i] == 'I' et perm[i] >= [i+1]:
ok = Faux; casse
si s[i] == «D» et perm[i] <= perm[i+1]:
ok = Faux; casse
si bon : cnt += 1
retour cnt
«» "

* **Heure**: "O(n+1)!" – totalement impraticable au-delà de "n=8".
* **Espace**: "O(n)" pour chaque permutation.
* **Pourquoi il échoue**: Explique pourquoi les intervieweurs demandent une solution DP.

---

- Oui. 5. – Optimisations trop compliquées

* Utilisation d'arbres segmentés ou d'arbres binaires indexés pour demander des sommes de gamme.
* Utilisation intensive de récursion + mémoisation avec encodage d'état compliqué.
* Pas nécessaire `HashMap` par cellule DP (par exemple, stocker des cartes de fréquence).

Bien que ceux-ci puissent fonctionner, ils ajoutent des coûts de bruit et de lisibilité, que les recruteurs n'aiment pas. Tenez-vous à nettoyer DP avec des sommes préfixées.

---

- Oui. 6. Mise en œuvre du code

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.
Tous utilisent la stratégie DP + prefix-sum et s'exécutent dans le temps `O(n2)` et la mémoire `O(n2)`.

---

#### 6.1 Java (Recommandé pour les intervieweurs)

"Java
Importation de java.util.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

public int numPermsDISéquence(String s) {
int n = s.longueur();
int[] dp = nouveau int[n + 1] [n + 1];
int[] pref = nouvelle int[n + 2]; // préfixe les sommes

// cas de base: 0 nombres placés -> 1 voie (préfixe vide)
les tableaux.fill(dp[0], 1);
pref[1] = 1; // préfix[1] = somme(dp[0]]

pour (int i = 1; i <= n; i++) {
c = s.charAt(i - 1);

// recalculer les montants de dp[i-1]
pref[0] = 0;
pour (int j = 0; j <= i; j++) {
pref[j + 1] = (pref[j] + dp[i - 1][j]) % MOD;
}

pour (int j = 0; j <= i; j++) {
i c == 'I') { // dernier < précédent
dp[i][j] = pref[j]; // somme(dp[i-1][0 ... j-1])
} autre { // 'D', dernier > précédent
dp[i][j] = (pref[i + 1] - pref[j] + MOD) % MOD;
}
}
}

Int ans = 0;
pour (int val : dp[n]) {
ans = (ans + valeur) % MOD;
}
le retour des an;
}

// Pour des tests rapides
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.numPermsDISequence("DID")); // 5
Système.out.println(sol.numPermsDISequence("D")); // 1
}
}
«» "

**Points clés**

* Le tableau `pref` contient des montants préfixés pour chaque transition `O(1)`.
* Modulo manipulé avec `+ MOD` pour éviter les valeurs négatives.
* Aucun objet inutile → rapide et efficace en mémoire.

---

#### 6.2 Python (Clean & Pytonic)

'`python
Solution de classe:
MOD = 10**9 + 7

def numPermsDISéquence(s: str) -> Int:
n = len(s)
dp = [[0] * (n + 1) pour _ dans l ' intervalle (n + 1)]
dp[0] = [1] * (n + 1) # cas de base

pour i dans la plage(1, n + 1):
pref = [0] * (n + 2)
pour j dans la plage i:
pref[j + 1] = (pref[j] + dp[i - 1][j]) MOD

pour j dans la plage (i + 1):
Si s[i - 1] == "Je":
dp[i][j] = pref[j] # sum 0 ... j-1
Sinon : # 'D'
dp[i][j] = (pref[i + 1] - pref[j]) MOD

retour sum(dp[n]) % self. MOD

# Vérifications rapides de la santé mentale
si __nom__ == "__main__" :
sol = Solution()
print(sol.numPermsDISequence("DID") # 5
print(sol.numPermsDISequence("D") # 1
«» "

**Pourquoi c'est génial**

* Utilise la compréhension de la liste pour la clarté.
* Le tableau explicite `pref` conserve les transitions O(1).
* Poignées modulo soigneusement.

---

*### 6.3 C++ (haute performance)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
static const int MOD = 1'000'000'007;

Int num PermsDISequence(s) {
int n = s.size();
vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));
fill(dp[0].begin(), dp[0].end(), 1); // cas de base

vecteur<int> pref(n + 2);

pour (int i = 1; i <= n; ++i) {
pref[0] = 0;
pour (int j = 0; j <= i; ++j)
pref[j + 1] = (pref[j] + dp[i - 1][j]) % MOD;

pour (int j = 0; j <= i; ++j) {
si (s[i - 1] == 'I') { // dernier < précédent
dp[i][j] = pref[j];
} autre { // 'D': dernier > précédent
dp[i][j] = (pref[i + 1] - pref[j] + MOD) % MOD;
}
}
}

Int ans = 0;
pour (int val : dp[n]) {
ans = (ans + valeur) % MOD;
}
le retour des an;
}
};

Int main() {
Solution sol;
Cout << sol.numPermsDISequence("DID") << endl; // 5
<< sol.numPermsDISequence("D") << endl; // 1
}
«» "

** Faits saillants* *

* Utilise `std::vector` pour les tableaux dynamiques.
* Mises à jour de la somme du préfixe temps constant.
* Sécurité Modulo avec `+ MOD`.

---

- Oui. 7. Analyse de la complexité

Heure de mise en oeuvre
- Oui.
Java / Python / C++. **O(n2)**. **O(n2)**.
Autres Naïve Brute Force: **O((n+1)!)
Arbre trop compliqué **O(n2 log n)**

---

- Oui. 8. Ce que les recruteurs veulent vraiment voir

1. **Réévaluation claire des problèmes** – montrez que vous avez compris les contraintes.
2. **Thoughtful Approach** – expliquer l'idée du PDD avant le codage.
3. **Mise en oeuvre efficace** – éviter les temps d'arrêt, gérer le module.
4. **Cas de sensibilisation** – par exemple, quand `s` est tout 'I' ou tout 'D'.
5. ** Code lisible** – nom propre (`dp`, `pref`, `MOD`).

Inclure une brève discussion sur les pièges et comment les éviter – un bonus dans les entretiens techniques.

---

- Oui. 9. Liste de contrôle finale

- [ ] L'affaire est réglée.
- [ ] Préfixez les montants mis à jour avant chaque ligne DP.
- Modulo appliqué après chaque opération arithmétique.
- [ ] Essai avec des cas d'échantillonnage (`"DID"` et `"D"`).
- [ ] Fournir rapidement `main` / `if __name__ == "_main__"` pour auto-test.

---

10. Enveloppe

- **Optimal**: DP + préfixation des montants.
- **Éviter**: Force brute, segments d'arbres, cartes lourdes.
- **Livraison**: Code propre et bien documenté dans la langue de votre choix.

En maîtrisant cette solution, vous acquerrez la question DP sur LeetCode et démontrerez l'envie des recruteurs de fluence algorithmique. Bonne chance avec votre interview prep! C'est ce qu'il a dit.

---

* Sentez-vous libre de copier, tester et adapter ces extraits à votre style de codage. Bon codage ! *