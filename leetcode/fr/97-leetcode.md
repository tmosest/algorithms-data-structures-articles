---
titre: LeetCode 97. Chaînes
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Chaîne d'interconnexion – LeetCode 97
**Le bon, le mauvais et le mauvais – un guide complet pour votre prochaine entrevue de codage* *

> **SEO Titre**: Interleaving String LeetCode 97 – Solution de programmation dynamique, 1D DP, Récursion, Conseils d'entrevue
> **Meta Description**: Master LeetCode 97 -Interleaving String avec une solution de programmation dynamique 1-D. Apprenez les avantages et les inconvénients, les pièges communs et l'explication prête à l'entrevue. Boostez vos compétences d'entretien de codage!

---

Table des matières

Lien
- Oui.
Aperçu du problème
Autres Bon : le DP optimum #good
Mauvais : Récursion naïve
Ugly: Sur-ingénierie
Suivi: O(min(m,n)) L'espace #suivi
#interview-stratégie
Code Extraits de code
Conseils d'essai
À emporter

---

## Aperçu du problème

**LeetCode #97 – Chaîne d'interconnexion**
> **Donné** trois chaînes `s1`, `s2` et `s3`, déterminer si `s3` peut être formé par *interleaving* `s1` et `s2`.
> *Interleaving* signifie que vous pouvez fusionner les deux chaînes tout en préservant l'ordre relatif des caractères de chaque chaîne originale.

> **Exemples**
> ```texte
> s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac" → true
> s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbacc" → faux
> `` "

**Pourquoi cela compte dans les entrevues* *
- Problème classique de programmation dynamique (DP).
- Démontre la capacité de raisonner sur les transitions d'état et les compromis espace/temps.
- apparaît fréquemment dans le codage des questions d'entrevue pour les postes qui valorisent la pensée algorithmique (ingénieur de backend, Data Scientist, etc.).

---

## La bonne – Solution optimale 1-D DP

Pourquoi 1-D DP ?

- **Complexité temporelle**: `O(m · n)` où `m = len(s1)`, `n = len(s2)` – le meilleur possible pour ce problème.
- **Complexité spatiale**: `O(min(m, n))` – nous ne conservons qu'une ligne de la table DP.
- **Simplicité** : Plus facile à expliquer et à implémenter correctement.

Définition de l'État

«» "
dp[j] = true = le préfixe s3[0 ... i + j - 1] peut être formé
par entrelacement s1[0 ... i - 1] et s2[0 ... j - 1]
«» "

`i` itrate sur les caractères de `s1`, `j` sur `s2`.

Transition

«» "
dp[j] = (dp[j] et s1[i-1] == s3[i+j-1]) // prendre de s1
OU (dp[j-1] et s2[j-1] == s3[i+j-1]) // prendre de s2
«» "

Code Pseudo

«» "
si m + n != len(s3): retourner Faux
si m < n: swap s1 et s2 // garder la plus petite chaîne dans s2
dp[0] = Vrai
pour j en 1 ... n:
dp[j] = dp[j-1] et s2[j-1] == s3[j-1]
pour i dans 1 ... m:
dp[0] = dp[0] et s1[i-1] == s3[i-1]
pour j en 1 ... n:
dp[j] = (dp[j] et s1[i-1] == s3[i+j-1]) ou
(dp[j-1] et s2[j-1] == s3[i+j-1])
retour dp[n]
«» "

---

## Les mauvaises – Récursion naïve (TLE)

Une approche récursive directe qui tente les deux possibilités à chaque étape peut explorer jusqu'à des états `2^(m+n)`.
Alors qu'il est conceptuellement simple, il dépasse facilement les limites de temps sur les grandes entrées.

**Pièges clés* *
- Temps exponentiel ("O(2^(m+n)")".
- Débordement pour les longues ficelles.
- Oui. Pas de mémoisation → travail répété.

---

- Oui. L'Ugly – Sur-ingénierie (Multiple HashMaps, Classes Personnalisées)

Certains candidats créent des objets personnalisés `State`, utilisent des tables de hachage avec des clés composites, ou tentent de comprimer la table DP en utilisant des opérations bit.
Bien que techniquement correct, ceci souvent:

- Obscure l'idée algorithmique.
- C'est plus dur pour les intervieweurs.
- Augmente le risque de bugs (erreurs hors-par-un, hachage incorrect des clés).

---

## Suivi : O(min(m, n)) Espace

Le PDD 1‐D réalise déjà l'espace «O(min(m, n)»)».
Si vous voulez être très concis, vous pouvez toujours stocker la plus petite des deux chaînes dans le tableau DP pour enregistrer encore plus de mémoire.

---

## Stratégie d'entrevue

1. **Demander des éclaircissements**
- Confirmer si l'entrelacement est *strictement* préservant l'ordre relatif.
- Préciser si `s1` et `s2` peuvent être vides.

2. ** Sortie précoce**
'`python
si len(s1) + len(s2) != len(s3):
Retour Faux
«» "

3. **Exposer les dimensions du tableau DP**
- «dp[i][j]» ou «dp[j]» unidimensionnels.
- Visualiser comme une grille où chaque cellule dépend des voisins supérieurs et gauches.

4. **Complexité**
- Heure: 'O(m · n) "
- Espace: "O(min(m, n)" (optimal)

5. **Juge**
- Des cordes vides.
- Tous les caractères sont égaux dans les deux cordes.

6. **Tests**
- Fournir des essais unitaires ou une petite méthode "main" qui exécute des cas d'échantillonnage.

---

Extraits de code complet

Voici des implémentations propres et prêtes à la production dans trois langues populaires.
N'hésitez pas à copier, coller et courir.

### Python 3 – DP 1-D

'`python
Solution de classe:
def isInterleave(self, s1: str, s2: str, s3: str) -> C'est vrai.
m, n, l = len(s1), len(s2), len(s3)
Si m + n != l:
Retour Faux

# S'assurer que s2 est la chaîne plus courte pour garder le tableau DP minimal
si m < n:
retour self.isInterleave(s2, s1, s3)

dp = [Faux] * (n + 1)
dp[0] = Vrai

# Initialiser la première ligne (i = 0)
pour j dans la plage(1, n + 1):
dp[j] = dp[j - 1] et s2[j - 1] == s3[j - 1]

# C'est au-dessus de s1
pour i à portée (1, m + 1):
dp[0] = dp[0] et s1[i - 1] == s3[i - 1]
pour j dans la plage(1, n + 1):
dp[j] = (dp[j] et s1[i - 1] == s3[i + j - 1]) ou \
(dp[j - 1] et s2[j - 1] == s3[i + j - 1])

retour dp[n]
«» "

### Java – DP 1-D

"Java
solution de classe publique {
booléen public estInterleave(String s1, String s2, String s3) {
int m = s1.longueur(), n = s2.longueur(), l = s3.longueur();
si (m + n != l) retourner faux;

// Gardez la chaîne plus petite dans s2 pour un tableau DP minimal
si (m < n) retour est Interleave(s2, s1, s3);

booléen[] dp = nouveau booléen[n + 1];
dp[0] = vrai;

// Initialiser la première ligne
pour (int j = 1; j <= n; j++) {
dp[j] = dp[j - 1] && s2.char (j - 1) == s3.charAt(j - 1);
}

// Déterminer au-dessus de s1
pour (int i = 1; i <= m; i++) {
dp[0] = dp[0] && s1.charAt(i - 1) == s3.charAt(i - 1);
pour (int j = 1; j <= n; j++) {
Dp[j] = (dp[j] && s1.charAt(i - 1) == s3.charAt(i + j - 1))
(dp[j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1));
}
}
retour dp[n];
}
}
«» "

### C++ – 1‐D DP (GNU‐C++17)

'`cpp
solution de classe {
public:
bool isInterleave(chaîne s1, chaîne s2, chaîne s3) {
int m = s1.size(), n = s2.size(), l = s3.size();
si (m + n != l) retourner faux;

// Gardez s2 plus court
si (m < n) retour est Interleave(s2, s1, s3);

vecteur<bool> dp(n + 1, false);
dp[0] = vrai;

// Première ligne
pour (int j = 1; j <= n; ++j) {
dp[j] = dp[j - 1] && (s2[j - 1] == s3[j - 1]);
}

pour (int i = 1; i <= m; ++i) {
dp[0] = dp[0] && (s1[i - 1] == s3[i - 1]);
pour (int j = 1; j <= n; ++j) {
Dp[j] = (dp[j] && (s1[i - 1] == s3[i + j - 1])
(dp[j - 1] && (s2[j - 1] == s3[i + j - 1]);
}
}
retour dp[n];
}
};
«» "

---

## Conseils pour les tests

1. **Essais d'écriture* *
"Java
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
System.out.println(sol.isInterleave("aabcc", "dbbca", "aadbbcbcac")); // true
System.out.println(sol.isInterleave("aabcc", "dbbca", "aadbbbacc")); // false
}
«» "

2. **Scénarios d'Edge**
- `s1 = ""`, `s2 = ""`, `s3 = ""` → `true`
- `s1 = "abc"`, `s2 = ""`, `s3 = "abc"` → `true "
- `s1 = "abc"`, `s2 = "def", `s3 = "abdcef"` → `true "

3. ** Essai de résistance**
'`python
importer au hasard, chaîne
s1 = ''.join(random.choice('abc') pour _ dans l'intervalle(2000))
s2 = ''.join(random.choice('abc') pour _ dans l'intervalle(2000))
# Construisez un s3 valide par shuffling s1 et s2 tout en préservant l'ordre
s3 = ''.join(random.sample(s1 + s2, len(s1)+len(s2))
«» "

Exécutez la solution pour la confirmer se termine en millisecondes.

---

À emporter

- **Utilisez le DP 1-D** : rapide, efficace en mémoire et convivial pour l'entrevue.
- **Éviter la récursion pure** à moins d'ajouter une mémoisation (temps « O(m·n) »).
- **Je n'ai jamais trop d'ingénieur**: La simplicité vous aide, vous et votre intervieweur.
- **Connais le suivi**: Être capable d'expliquer l'espace `O(min(m,n)' montre que vous comprenez l'optimisation.

La maîtrise de ce problème vous donne une base solide pour *toute* entrevue qui teste les compétences DP – que vous postuliez à un ingénieur de backend, un ingénieur de données ou un rôle d'apprentissage automatique.

Bon codage et bonne chance pour votre prochaine interview! C'est ce qu'il a dit