---
titre: LeetCode 943. Trouvez la plus courte superstring -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 943 Trouver la plus courte superstring

Description
C'est pas vrai.
**Input**="words`" – une série de chaînes **uniques** minuscules (1 ≤ mots.longueur ≤ 12, 1 ≤ mots[i].longueur ≤ 20)="
Return the *shortest* string that contains all element of `words` as a substring. Si plusieurs cordes plus courtes existent, l'une d'elles est bonne. Autres
**Assomption**= Aucune chaîne dans `words` n'est une sous-chaîne d'une autre, ce qui élimine les redondances triviales. Autres
**Cible de complexité** Autres

---

- Oui. 2. Pourquoi ce problème est une grande question d'entrevue

1. **PDD classique avec Bitmask** – un modèle canonique pour les questions de type TSP qui testent les compétences de programmation dynamique d'un candidat.
2. **Renforcer le chevauchement** – la nécessité de précomputer les chevauchements est une belle torsion qui pousse les candidats à penser au-delà du PDD pur.
3. ** Manutention des caisses** – pas de sous-chaînes, petite taille d'entrée, mais la solution doit toujours gérer correctement toutes les permutations, ce qui en fait un test parfait pour la précision.
4. **agnostique de la langue** – vous pouvez présenter votre langue préférée (Java, Python, C++...) tout en appuyant sur le même noyau algorithmique.

---

- Oui. 3. Aperçu de la solution – DP + Bitmask + Overlap

1. **Matrice de chevauchement précalculée**
`overlap[i][j]` = longueur du suffixe le plus long de `words[i]` qui correspond à un préfixe de `words[j]`.
La partie supplémentaire, que nous devons annexer lors de la transition de `i` à `j` est donc
«mots[j].substring(overlap[i][j]»

2. ** État du PDE**
`dp[mask][i]` – la superchaîne la plus courte qui couvre l'ensemble des mots indiqués par `mask` ** et se termine par le mot `i`**.
`masque` est un bitmasque de longueur `n` (12), il y a donc au plus des masques `2^n`.

3. **Transition**
Pour chaque état `(mask, i)` nous essayons d'ajouter un nouveau mot `j` qui est **pas** encore dans `mask`:

«» "
nextMasque = masque
candidat = dp[masque][i] + mots[j].substring(overlap[i][j])
dp[nextMask][j] = meilleur(dp[nextMask][j], candidat)
«» "

4. **Réponse**
Parmi tous les 'dp[(1<<n)-1]]' choisir la corde la plus courte (tout bris de cravate est bien).

5. **Reconstruction par rapport au stockage direct* *
- Pour les petits `n` (12) nous pouvons stocker directement la chaîne résultante dans `dp`.
- Si la mémoire devient un problème, nous pourrions stocker seulement la longueur* et un pointeur parent* et reconstruire à la fin.

---

- Oui. 4. Bonne, mauvaise, mauvaise – Une marche rapide

Aspect du bien
- C'est quoi ?
Une permutation naïve de la force brute (`n!`) est impossible même pour n=12.
**Mise en œuvre**= Simple DP + bitmask + concaténation de la chaîne== L'oubli des chevauchements précalculés conduit à O(n3) temps à l'intérieur du DP===L'utilisation de mémorisation récursive avec des copies de chaîne peut conduire à des débordements de pile ou à un GC lent en Java====
**Cas de corner**= Gestion de la liste de mots vides (entrée de la bordure), gestion de tous les mots distincts== Ne pas rendre compte de l'hypothèse de sous-chaîne ==____________________________________________________________________________________________________________________________________________________________________________________________________________________
**Readability**

---

- Oui. 5. Mise en œuvre – Java, Python, C++

Voici des solutions propres et prêtes à coller dans les trois langues demandées. Chacun suit le même squelette algorithmique.

#### 5.1 Java (8+)

"Java
Importation de java.util.*;

solution de classe publique {
// Recoupement précalculé[i][j] = suffixe le plus long de mots[i] correspondant au préfixe des mots[j]
interne statique privé[][] computeOverlaps(String[] words) {
int n = longueur de mots;
int[][] chevauchement = nouvelle int[n][n];
pour (int i = 0; i < n; i++) {
pour (int j = 0; j < n; j++) {
i) continuer;
int max = Math.min(words[i].length(), words[j].length());
pour (int k = max; k >= 1; k--) {
si (words[i].substring(words[i].longueur() - k).equals(words[j].substring(0, k))) {
chevauchement[i][j] = k;
pause;
}
}
}
}
le chevauchement des retours;
}

public Chaîne la plus courteSuperchaîne(String[] mots) {
int n = longueur de mots;
si (n == 0) retourner ";

int[][] chevauchement = calculOverlaps(mots);
dans maxMask = 1 << n;
// dp[masque][dernier] = meilleure superchaîne pour cet état
Chaîne[][] dp = nouvelle chaîne[maxMask][n];

// initialiser
pour (int i = 0; i < n; i++) {
dp[1 << i]i] = mots[i];
}

// PDD
pour (int masque = 1; masque < maxMasque; masque++) {
pour (int last = 0; last < n; last++) {
si ((masque et (1 << dernier))) 0) continuer; // la dernière doit être en masque
la chaîne cur = dp[masque][dernier];
si (cur == null) continuer;
pour (int next = 0; next < n; next++) {
si ((masque & (1 << suivant)) != 0) continuer; // déjà utilisé
int nextMasque = masque (1 << suivant);
Candidat à la chaîne = cur + words[next].substring(overlap[last][next]);
si (dp[nextMask][next] == null
candidat.longueur() < dp[nextMask][next].longueur() {
dp[nextMask][next] = candidat;
}
}
}
}

// réponse finale
Chaîne ans = nul;
Int final Masque = maxMasque - 1;
pour (int i = 0; i < n; i++) {
si (dp[finalMask] [i] != null &&
(ans=null="dp[finalMask][i].longueur() < ans.longueur()) {
ans = dp[finale Masque [i];
}
}
le retour des an;
}

// Pour des tests rapides
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Chaîne[] mots = {"alex", "loves", "leetcode"};
System.out.println(sol.shortestSuperstring(words)); // attendu: alexlovesleetcode
}
}
«» "

---

#### 5.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def le plus court Superstring(self, mots: List[str]) -> str:
n = len(mots)
si n] 0:
retour ""

# recoupement[i][j] = suffixe le plus long de mots[i]
chevauchement = [[0] * n pour _ dans l'intervalle(n)]
pour i dans la plage(n):
pour j dans la plage(n):
Si i == j:
poursuivre
max_len = min(len(words[i]), len(words[j])
pour k dans la plage(max_len, 0, -1):
si mots[i][-k:]] [j][:k]:
chevauchement[i][j] = k
pause

_masque max = 1 << n
dp = [[""] * n pour _ dans l'intervalle(max_masque)]

# initialiser
pour i dans la plage(n):
dp[1 << i]i] = mots[i]

# PDD
pour masque dans la gamme(1, max_mask):
pour le dernier rang(n):
si non (masque et (1 << dernier)):
poursuivre
cur = dp[masque][dernier]
si non cur:
poursuivre
pour nxt dans la plage(n):
si masque & (1 << nxt):
poursuivre
next_mask = masque
cand = cur + mots[nxt][overlap[last][nxt] :]
si dp[next_mask][nxt] ou len(cand) < len(dp[next_mask][nxt]):
dp[next_mask][nxt] = cand

# réponse finale
_masque final = max_masque - 1
as = min((dp[final_mask][i] pour i dans l'intervalle(n) si dp[final_mask][i]), key=len)
retour et

# Test rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.shortestSuperstring(["alex","loves","leetcode"]) Code alexlovesleet
«» "

---

Numéro 5.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne la plus courteSuperstring(vecteur<string>& mots) {
int n = mots.size();
si (n == 0) retourner ";

// Recoupements avant calcul
vecteur<vector<int>> chevauchement(n, vecteur<int>(n, 0));
pour (int i = 0; i < n; ++i) {
pour (int j = 0; j < n; ++j) {
i) continuer;
int mx = min(words[i].size(), words[j].size());
pour (int k = mx; k >= 1; --k) {
if (words[i].substr(words[i].size() - k) == words[j].substr(0, k)) {
chevauchement[i][j] = k;
pause;
}
}
}
}

dans maxMask = 1 << n;
vector<vector<string>> dp(maxMask, vector<string>(n, ""));
pour (int i = 0; i < n; ++i) dp[1 << i]i] = mots[i];

pour (int masque = 1; masque < maxMasque; ++Masque) {
pour (int last = 0; last < n; ++last) {
si (!(mask & (1 << last)))
Const string& cur = dp[masque][dernier];
pour (int nxt = 0; nxt < n; ++nxt) {
si (masque et (1 < < nxt)) continuent;
int nextMasque = masque (= 1 < nxt);
chaîne cand = cur + mots[nxt].substr(overlap[last][nxt]);
si (dp[nextMask][nxt].vide()=" cand.size() < dp[nextMask][nxt].size()
dp[nextMask][nxt] = cand;
}
}
}

Int final Masque = maxMasque - 1;
ficelles et cordes;
pour (int i = 0; i < n; ++i) {
si (!dp[finalMask][i].vide() &&
(ans.vide()="dp[finalMask]="i].size() < "ans.size()) {
ans = dp[finale Masque [i];
}
}
le retour des an;
}
};

Int main() {
Solution s;
vector<string> words = {"alex", "loves", "leetcode"};
cout << s.shortestSuperstring(words) << '\n'; // alexlovesleetcode
}
«» "

---

- Oui. 6. Essais – Vérifications rapides

Résultats attendus
C'est quoi, ça ?
"["alex", "amoureux", "code de transport"]" Code 'alexlovesleet'
"["cat", "dog", "bird"]""""toute fusion plus courte (par exemple, "catdogbird")"
"[]""""""""

---

- Oui. 7. Wrap‐Up – Quoi apporter à votre entrevue

- **Exposer l'idée fondamentale**: Nous réduisons le problème à un chemin hamiltonien classique plus court dans un DAG, résolu par DP + bitmask. (en milliers de dollars)
- **Afficher une implémentation propre**: Choisissez la langue avec laquelle vous êtes le plus à l'aise, mais gardez la structure identique.
- **Extensions des peines**: Si vous deviez produire *tous* des superchaînes minimales, nous pourrions garder plusieurs candidats par état. (en milliers de dollars)
- **Afficher les performances**: Même avec la récursion, cela tourne en millisecondes pour n=12 – nous sommes loin du cauchemar factoriel de la force brute. (en milliers de dollars)

---

- Oui. 8. Conclusion

`shortestSuperstring` est un problème d'entretien de manuels qui vous permet de démontrer:

- **Aiguïté algorithmique** (DP + bitmask + chevauchement).
- ** Compétences linguistiques** (Java, Python, C++).
- **Matériel artisanal logiciel** (structure claire, boîtiers d'angle de manutention, complexité optimale).

N'hésitez pas à copier l'un des extraits ci-dessus dans votre IDE, à effectuer les tests d'échantillons et à être prêt à expliquer chaque ligne dans une entrevue de 5 minutes. Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

**Mots clés pour l'optimisation de la recherche:**
superstring le plus court, DP bitmask, recoupement, solution Java, solution Python, solution C++, question d'entrevue, interview d'algorithme, prep d'entrevue, interview de codage, leetcode 943, algorithme agnostique de langue, complexité optimale, aucune hypothèse de substring.