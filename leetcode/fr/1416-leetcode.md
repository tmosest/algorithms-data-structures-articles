---
titre: LeetCode 1416. Restauration Le tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Restaurer le tableau (Code de bord 1416) – Un guide complet
> * Programmation dynamique, Java, Python, C++ – L'un des puzzles d'interview les plus courants. *

---

Table des matières

Secteur
- Oui.
Autres Déclaration de problème
Autres Pourquoi ce problème est-il une question d'entrevue?
Autres 3-- Brute-Force Insight (et pourquoi elle échoue)
Autres Approche optimale – Programmation dynamique Autres
Autres Mise en oeuvre
Autres Les cas des bords & des gotchas
Autres 7: Complexité temporelle et spatiale
Code – Java / Python / C++
FAQ / Variantes d'entrevue courantes
Comment utiliser ce blog pour la chasse à l'emploi
TL;DR

---

- Oui. 1. Exposé des problèmes

Vous recevez:

* une chaîne `s` contenant seulement des chiffres décimals, **pas de zéros en tête**.
* un entier `k` (`1 ≤ k ≤ 109`).

La chaîne `s` est la concaténation d'un tableau inconnu d'entiers positifs `A = [a1, a2, ..., a_m]` avec chaque `a_i` dans la gamme inclusive `[1, k]`.
Votre tâche est de **compter le nombre de différents tableaux** qui pourraient produire la chaîne `s`.
Retourner la réponse modulo `1 000 000 007`.

> **Exemples**
> * `s = "1000"`, `k = 10000` → `1` (arraché `[1000]`)
> * `s = "1000"`, `k = 10` → `0` (pas de partage valide)
> * `s = "1317"`, `k = 2000` → `8` (liste des tableaux affichés dans l'instruction)

---

- Oui. 2. Pourquoi ce problème est une question d'entrevue

Raison
- Oui.
** Programmation dynamique** La solution est un DP classique sur les positions de cordes. Autres
Autres **Edge-Case Handling**= Vous devez éviter de diriger des zéros, de gérer de grands `k` et de surveiller les débordements entiers. Autres
**L'évolutivité peut être de 105. Autres
**Scénarios du monde réel**= Pensez à analyser les fichiers journaux, décoder les messages ou reconstruire les charges utiles des paquets. Autres
**Les intervieweurs l'aiment** Il teste votre capacité à combiner la perspicacité algorithmique et le codage propre. Autres

---

- Oui. 3. Brute-Force Insight (et pourquoi elle échoue)

Une approche naïve tenterait chaque point partagé:

«» "
pour chaque position i en s:
pour chaque point de partage j après i:
si s[i:j] est un nombre valide <= k:
Récursé sur s[j:]
«» "

C'est essentiellement exponentiel ('O(2^n)') et va exploser même pour les petites cordes.
Il nous faut un algorithme polynôme.

---

- Oui. 4. Approche optimale – Programmation dynamique

### 4.1 Idée

Traitez la chaîne de **de droite à gauche** (ou de gauche à droite).
Laissez `dp[i]` = nombre de façons de diviser le suffixe `s[i ... n-1]` en nombres valides.

- `dp[n] = 1` – le suffixe vide est une fraction valide.
- Pour chaque position "i" 0 ≤ i < n:
- Si `s[i] == `0'` → `dp[i] = 0` (les zéros ne sont pas autorisés).
- Dans le cas contraire, étendre un nombre jusqu'à 10 chiffres maximum (depuis "k ≤ 109").
- Pour chaque `j` de `i` à `min(i+9, n-1):
- Construisez le nombre `num = s[i ... j]` progressivement.
- Si `num > k` → pause (plus valide).
- Autrement `dp[i] = (dp[i] + dp[j+1]) mod M`.

Enfin, réponse = `dp[0]`.

4.2 Pourquoi au plus 10 chiffres ?

`k ≤ 109` → tout nombre supérieur à `109` est automatiquement invalide, de sorte que toute sous-chaîne de plus de 10 chiffres ne peut pas être ≤ k.

### 4.3 Croquis d'exactitude

*Cas de base*: Le suffixe vide (`dp[n]`) a exactement une façon d'être divisé: ne choisissez rien.
*Étape inductive*: Pour toute position `i`, chaque fraction valide du suffixe doit commencer par un nombre valide formé de `s[i ... j]`.
Toutes les autres fractions du reste sont comptées en «dp[j+1]».
Le total de tous les «j» valides donne le nombre total de «dp[i]».
Ainsi, par induction, le DP compte correctement tous les tableaux.

---

- Oui. 5. Démarche de mise en oeuvre

Ci-dessous se trouve un DP** (itatif) de base – préféré pour Java/Python en raison des limites de profondeur de récursion.
Vous pouvez aussi l'implémenter de façon récursive avec la mémoisation; les deux sont O(n × 10).

Principaux détails de la mise en œuvre:

Numéro
C'est quoi ?
**Integer Overflow** Autres
**Modulo Constant** Autres
** Longueur de la boucle Utiliser `int[]` pour DP; `O(n)` mémoire. Autres
**Reporter Zéro** "0". Autres
Autres **Découvrez rapidement**= Quand `num > k`, arrêtez d'étendre la sous-chaîne – d'autres chiffres ne font que la agrandir. Autres

---

- Oui. 6. Edge Cases et Gotchas

1. **La clé commence par `0`** – réponse `0`.
2. **k < 10** – beaucoup de sous-chaînes sont invalides, DP fonctionne encore.
3. **Longueur maximale sous-chaîne** – il suffit de regarder 10 caractères devant.
4. **Large `k` (par exemple, 109)** – tout va bien parce que nous comparons `num` à `k` en utilisant `long`.
5. **Python Recursion Limit** – évitez la récursion; utilisez le DP itératif.

---

- Oui. 7. Complexité temporelle et spatiale

* **Heure**: `O(n · L)` où `L = 10` (maximum des chiffres).
Pour `n = 105`, il s'agit d'environ `1 million' d'opérations – confortablement rapides.
* **Espace**: `O(n)` pour le tableau DP.

---

- Oui. 8. Code – Java / Python / C++

> **Toutes les solutions renvoient la réponse modulo `1 000 000 007`. **

#### 8.1 Java

"Java
Importation de java.util.*;

solution de classe {
int final statique privé MOD = 1_000_000_007;

Nombre d'entrées publiques Dénomination des marchandises
int n = s.longueur();
int[] dp = nouvelle int[n + 1];
dp[n] = 1; // suffixe vide

pour (int i = n - 1; i >= 0; i--) {
si (s.charAt(i) == '0') { // tête zéro non autorisée
dp[i] = 0;
poursuivre;
}

long num = 0;
pour (int j = i; j < n && j - i < 10; j++) { // au plus 10 chiffres
num = num * 10 + (s.charAt(j) - '0');
si (num > k) pause; // ne peut pas être valide
dp[i] = (int)((dp[i] + dp[j + 1]) % MOD);
}
}
retour dp[0];
}
}
«» "

8.2 Python

'`python
MOD = 10**9 + 7

Solution de classe:
def numberOfArrays(self, s: str, k: int) -> Int:
n = len(s)
dp = [0] * (n + 1)
dp[n] = 1 # suffixe vide

pour i dans la fourchette(n - 1, -1, -1):
si s[i] == '0': # zéros de tête interdits
poursuivre
num = 0
pour j dans la plage(i, min(n, i + 10)): # au plus 10 chiffres
num = num * 10 + int(s[j])
si num > k:
pause
(dp[i] + dp[j + 1]) % MOD

retour dp[0]
«» "

#### 8.3 C++

'`cpp
solution de classe {
public:
static const int MOD = 1'000'000'007;
Numéro int Dénomination des marchandises
int n = s.size();
vecteur<int> dp(n + 1, 0);
dp[n] = 1; // scénario de base

pour (int i = n - 1; i >= 0; --i) {
si (s[i] == '0') continuer; // pas de zéro en tête

long num = 0;
pour (int j = i; j < n && j - i < 10; ++j) { // max 10 chiffres
num = num * 10 + (s[j] - '0');
en cas de rupture (num > k);
dp[i] = (dp[i] + dp[j + 1]) % MOD;
}
}
retour dp[0];
}
};
«» "

---

- Oui. 9. FAQ / Variantes d'entrevue courantes

Question Réponse
C'est pas vrai.
Autres **Pouvons-nous utiliser la récursion avec la mémoisation? Profondeur sera au plus `n`, mais Python peut frapper les limites de récursion; Java & C++ fine. Autres
Autres **Et si `k` était plus grand que `109`?**= L'algorithme fonctionne encore; il suffit d'augmenter la fenêtre des chiffres (`10` → `digets(k)`), mais le temps reste O(n·digets(k)). Autres
**Pourquoi ne pas utiliser BigInteger?**= `k` est ≤ 109, donc un entier de 64 bits est suffisant. Autres
Autres **Que faire si la chaîne peut contenir des zéros de tête?**.Ajustez la condition : sautez les positions où `s[i] == '0'` à moins que le nombre lui-même soit `0` et autorisé. Autres
Autres **Pouvons-nous utiliser une Trie?**= Pas nécessaire; DP est plus simple et plus rapide. Autres

---

- Oui. 10. Comment utiliser ce blog pour la chasse à l'emploi

1. **Afficher votre processus de résolution des problèmes** – Inclure le blog complet avec des extraits de code en plusieurs langues.
Les recruteurs aiment voir une solution propre et commentée, pas seulement la réponse finale.
2. **Complexité du temps de pointe** – Les intervieweurs demandent souvent, -Quelle est la pire affaire? (en milliers de dollars)
La démonstration de l'analyse "O(n10)" montre une profonde compréhension.
3. **Ajouter une section « Piège commun »** – Mention des limites de récursion, des débordements, etc.
4. **SEO Boost** – Utilisez des mots-clés comme *Java Python C++ interview problem**, et * Job interview algorithme** tout au long de l'article.
5. **Ajouter un appel à l'action** – Inviter les recruteurs à se connecter ou à planifier un appel; p. ex. Connectez-vous sur LinkedIn !

> ** Conseil professionnel :** Poster ce blog sur **Moyen**, votre site personnel, ou un GitHub Gist. Ajouter une courte vidéo de démonstration expliquant l'algorithme; le contenu vidéo se classe plus haut sur les moteurs de recherche et capture les yeux des recruteurs.

---

Conclusion

Le problème **Restaurer l'Array** (LeetCode 1416) est un défi DP classique qui mélange la logique d'analyse avec des contrôles prudents des frontières.
Avec la stratégie itérative DP ci-dessus, vous pouvez fournir une solution qui est:

- **Fast** (travaille pour 105 chaînes de longueur),
- **Correct** (manipulation des zéros et des grands "k");
- **Portable** (disponible en Java, Python et C++).

Maintenant, vous êtes prêt à accepter ce problème et impressionner les gestionnaires d'embauche. Bon codage !

---

*Si vous trouvez ce guide utile, partagez-le sur Linked Dans ou Twitter – laissez-nous aider plus de gens à casser leur prochaine interview! *