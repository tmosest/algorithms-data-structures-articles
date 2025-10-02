---
titre: LeetCode 91. Décoder les voies -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Décoder Ways – 91 – Solution pleine pile (Java-Python)
> **Problème #91 – Moyen**
> https://leetcode.com/problèmes/decode-ways/

> **Objectif** – Compter le nombre de façons de décoder une chaîne numérique (1 → A, 2 → B, ..., 26 → Z).
> **Constraint** – 1 ≤ s.longueur ≤ 100, la réponse correspond à un int signé 32 bits.

Ci-dessous vous trouverez trois implémentations prêtes à la production que vous pouvez coller directement dans votre pipeline IDE ou CI. Après cela, un court et convivial article de blog de référencement qui explique le bon, le mauvais et le mauvais de ce puzzle DP classique – parfait pour LinkedIn, Medium ou un blog personnel pour mettre en évidence vos problèmes de résolution de problèmes aux recruteurs.

---

1. Mise en œuvre Java (DP itérative)

"Java
Importation de java.util.*;

solution de classe publique {
***
* Renvoie le nombre de façons de décoder la chaîne s.
* Utilise O(n) temps et O(1) espace supplémentaire.
*/
int public int numDecodings(String s) {
int n = s.longueur();
Si (n=0) s.charAt(0) == '0') retour 0;

Int prev = 1; // dp[i-2]
= 1; // dp[i-1]
pour (int i = 1; i < n; i++) {
température int = 0;

// décodage à un chiffre (car seul)
si (s.charAt(i) != '0') {
température += courbure;
}

// décodeur à deux chiffres (précédent + courant)
int deux = (s.charAt(i-1) - '0') * 10 + (s.charAt(i) - '0');
si (deux >= 10 && deux <= 26) {
température += prév;
}

// Fenêtre de diapositive
prev = curr;
curr = température;
}
le curr de retour;
}
}
«» "

Pourquoi O(1) espace ?

La récurrence dépend uniquement des deux valeurs DP précédentes (`dp[i-1]` et `dp[i-2]`).
Garder deux variables entières (`prev`, `curr`) élimine le tableau O(n).

---

2. Mise en œuvre du Python (PDD de base)

'`python
Solution de classe:
def numDécodings(self, s: str) -> Int:
n = len(s)
si n == 0 ou s[0] «0»:
retour 0

# dp[i] = façons de décoder s[:i]
dp = [0] * (n + 1)
dp[0], dp[1] = 1, 1

pour i dans la plage(2, n + 1):
# un chiffre (s[i-1])
si s[i-1] != «0»:
dp[i] += dp[i-1]

# deux chiffres (s[i-2:i])
2 = int(s[i-2:i])
si 10 <= deux <= 26:
dp[i] += dp[i-2]

retour dp[n]
«» "

> **Astuce** – tranche de Python `s[i-2:i]` est déjà un entier lorsqu'il est passé à `int()`, ce qui maintient le code concis.

---

3. Mise en œuvre C++ (PDD itérative avec espace O(1))

'`cpp
solution de classe {
public:
int numDécodings(chaîne s) {
int n = s.size();
si (n) [0]] '0') retour 0;

longue longueur prev = 1; // dp[i-2]
longue courbure longue = 1; // dp[i-1]

pour (int i = 1; i < n; ++i) {
durée longue = 0;

// Un chiffre
si (s[i] != '0')
température += courbure;

// Deux chiffres
int deux = (s[i-1] - '0') * 10 + (s[i] - '0');
si (deux >= 10 && deux <= 26)
température += prév;

prev = curr;
curr = température;
}
retourner static_cast<int>(curr);
}
};
«» "

> **Pourquoi "long"?**
> Bien que la réponse corresponde à `int`, les valeurs intermédiaires peuvent temporairement dépasser 32 bits lorsque `s` est long et que toutes les combinaisons sont valides. L'utilisation de "long long" est un filet de sécurité.

---

4. Article du blog – Le bon, le mauvais, et l'atroce des façons de décoder

> **Titre :** *Décoder les voies : les bons, les mauvais et les mauvais – Un défi de DP classique pour votre trousse d'entrevue*
> **Méta—description:** Master Leetcode #91 Décoder Ways avec les solutions Java, Python et C++. Apprenez la récurrence du PDD, les pièges de la base et comment en parler aux recruteurs.

---

Introduction

Quand j'ai trébuché sur Leetcode 91, j'ai pensé que c'était un puzzle simple. Il s'avère qu'il s'agit d'une occasion d'or** de présenter vos côtelettes de programmation dynamique, de gérer des cas de bord, et même votre capacité de parler aux recruteurs au sujet du *pourquoi* derrière votre code.

Dans ce post, I.ll disséque la solution en trois parties que chaque candidat à l'ingénierie logicielle doit maîtriser:

1. **Le Bon** – Ce qui fait de ce problème une base d'entrevue parfaite.
2. **Le mauvais** – Des pièges communs qui tuent un candidat.
3. **L'Ugly** – Complications du monde réel que vous frapperez lorsque vous passerez d'un test de jouet à la production.

---

### Les bons – Pourquoi Décoder les chemins

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Déclaration de problème claire**=Une chaîne numérique → de nombreuses interprétations alphabétiques – facile à raisonner. Autres
Autres La récurrence `dp[i] = dp[i-1] + dp[i-2]` est un exemple de sous-problèmes qui se chevauchent. Autres
**O(n) Solution**= Le temps et l'espace peuvent être linéaires et s'adapter confortablement aux contraintes du Leetcode. Autres
**Modèle réutilisable**Le tour de "Look-back-one-and-two" apparaît dans de nombreux problèmes de DP basés sur des cordes (p. ex., "Climbing Stairs" et "Unique Paths"). Autres
**Great for Interviews**= Les recruteurs aiment voir une solution PD propre et itérative qui fonctionne dans le temps `O(n)` avec l'espace `O(1)`. Autres

> *Pro Tip:* Lors d'une entrevue en direct, commencer par décrire les cas de base (`dp[0] = 1`, `dp[1] = 1` sauf si le premier char est '0'). Cela montre que vous comprenez les conditions de bord du problème tout de suite.

---

Les mauvaises – erreurs courantes que les candidats plagues

Une erreur Pourquoi ça fait mal Comment l'éviter
- C'est quoi ?
**Ignorer Un « 0 » ne peut pas correspondre à une lettre, mais peut faire partie d'un numéro valide à deux chiffres (« 10 »– « 26 »). Oublier de gérer cela renvoie 0 ou sur-comptes. Ajouter un garde: `si (s[0]] '0') retour 0;''
Le mélange de `dp[i]` et `dp[i-1]` conduit à des combinaisons erronées. Utiliser un DP basé sur 1 (`dp[0] = 1`) ou un document explicite qui `dp[i]` fait référence aux premiers caractères *i*. Autres
**Ne pas vérifier les Bounds à deux digits** Certaines solutions utilisent par erreur `< 27` sans la vérification `>=10`, en comptant `05` comme étant valide à deux chiffres. Essai explicite `si (deux >= 10 && deux <= 26)` Autres
**Array vs. Rolling Variables**.La mise en œuvre de DP avec un tableau est bonne pour les petites entrées, mais une chaîne de 100 caractères peut encore être faite avec seulement deux entiers. L'utilisation du tableau rend la solution sur-ingénierie. Conserver deux variables (`prev`, `curr`) et glisser la fenêtre. Autres
**Edge-Case = chaîne vide**= Beaucoup de gens retournent 0 pour `s="`, mais la spécification LeetCode garantit `longueur >= 1'. Ajouter un garde est toujours sûr pour les bibliothèques réutilisables. 0) retourner 0;»

---

### ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. ** Grandes entrées dans différents environnements* *
* Leetcode limite `s.longueur <= 100`, mais les services internes peuvent alimenter des chaînes plus longues.
* Les valeurs intermédiaires peuvent déborder `int`. Utilisez `longe` ou `long` pour la sécurité.

2. **Langue mixte Bases de codes* *
* Vous pouvez avoir besoin d'une bibliothèque Java, d'un service Python et d'un micro-service C++ qui résolvent le même puzzle.
* Gardez l'interface identique: `int numDecodings(String)` / `int numDecodings(String s)` / `int numDecodings(string s)`.

3. **Thread‐Safety & Immutability**
* Dans un service multithreaded, vous ne pouvez pas utiliser les tableaux DP statiques de niveau classe.
* Les solutions itératives ci-dessus sont naturellement sans fil car elles n'utilisent que des variables locales.

4. **Unit-Testing & Mocking**
* Éviter les cas de calage dur dans les tests; générer plutôt des chaînes aléatoires et recouper avec un validateur de force brute naïf pour `n <= 10`.
* Exemple de harnais de test Python :

'`python
def brute(s):
si non s: retour 1
si s[0] == '0': retour 0
Voies = 0
si s[0] != '0': voies += brute(s)[1:])
si len(s) >= 2 et 10 <= int(s):2) <= 26:
Voies += brute(s[2:])
retour
«» "

5. **Performance dans un service à haute charge**
* Même si `O(n)` est trivial pour `n <= 100`, un micro-service pourrait appeler cette méthode 106 fois par seconde.
* Cache les résultats pour les entrées répétées ou pré-calculer pour toutes les chaînes possibles de longueur ≤ 100 si votre trafic est principalement répété.

---

5. Comment partager cela sur votre blog

> *Inclure les étiquettes suivantes:*
> `#DynamicProgramming`, `#Leetcode91`, `#DecodeWays`, `#CodingInterview`, `#Java`, `#Python`, `#C++`, `#InterviewPrep`, `#Recrutement "

```markdown
♪ Décoder les voies : le bon, le mauvais et le mauvais

Lorsque vous débarquez une entrevue dans une entreprise technologique, votre recruteur vous demandera souvent de résoudre **Decode Ways** (#91 sur LeetCode).
Voici pourquoi il s'agit d'un problème *must-know* et comment vous pouvez y répondre dans n'importe quelle langue.

Les bons
* Temps linéaire et espace constant* – parfait pour les contraintes du JO.
*Récurrence nette*: `dp[i] = dp[i-1]` (un chiffre) + `dp[i-2]` (deux chiffres).
*Dessin réutilisable* pour beaucoup de cordes Questions du DP.

- Oui. Les mauvais
*La manipulation de zéro* – un seul « 0» ou un « 0 » qui ne fait pas partie d'un nombre valide à deux chiffres tue immédiatement le résultat.
*Les erreurs hors-par-un* sont fréquentes; rappelez-vous que `dp[0] = 1` (chaîne vide) et `dp[1] = 1` à moins que le premier char soit ‘0=.

- Oui. L'Ugly
*Les déploiements à grande échelle* peuvent accidentellement utiliser un tableau `int` où la somme déborde temporairement de 32 bits.
*Sécurité des fils* : les réseaux DP mutables partagés sont un cauchemar dans des environnements concomitants.

Code (Java)

*Java:*

"Java
int public numDecodings(String s) { ... }
«» "

*Python:*

'`python
Solution de classe:
def numDécodings(self, s: str) -> Int: ...
«» "

*C++:*

'`cpp
solution de classe {
public:
int numDécodings(chaîne s) { ... }
};
«» "

Les pensées finales

Le problème Decode Ways est un microtest de programmation dynamique* qui met en valeur :

- Compréhension des caisses de base et manipulation des caisses de bord.
- Capacité de comprimer la mémoire de `O(n)` à `O(1)`.
- Communication claire de votre raisonnement (bon pour les notes d'entrevue).

Bonne chance dans votre prochaine entrevue de codage – vous aurez maintenant une solution prête à copier et un billet de blog poli que les recruteurs peuvent trouver avec un rapide Recherche Google pour la solution de chemins de code Java ou de chemins de code Python.

*Bon code ! *
«» "

> ** Astuce de référence** – Le message inclut le mot-clé « Decode Ways » plusieurs fois, et il se termine par un appel à l'action pour que les recruteurs voient la solution sur LeetCode. Les moteurs de recherche adorent ces signaux.

---

6. Exécution locale du code

Langue
C'est pas vrai.
Java (avec un `main` qui innove `Solution`) Autres
(ajouter un script `unittest` qui appelle `Solution(.numDecodings()`) Autres
C++ -std=c++17 solution.cpp -o décodage`<br>`./décode`

---

Bonus : écueils de test unitaire

"Java
Importation d'org. junit.jupiter.api.*;
Importer l'org. junit.jupiter.api.Assertions.*;

Solution de classe Essai {
solution finale privée s = nouvelle solution();

@Test
test de videSimple() {
assertionEquals(2, s.numDécodings("12")); // AB, L
}

@Test
vide testZero() {
assertionEquals(0, s.numDécodings("0");
affermEquals(0, s.numDécodings("10");
}

@Test
Essai de videGrand() {
assertionEquals(1, s.numDécodings("1111111")); // tous les A
}
}
«» "

'`python
test unitaire d'importation
de solution d'importation

classe TestDecodeWays(unittest. Cas d'essai:
def setUp(self):
Self.s = Solution()

def test_basic(self):
Self.assertEqual(2, self.s.numDécodings("12"))

def test_with_zero(self):
Self.assertEqual(0, self.s.numDécodings("0")
Self.assertEqual(0, self.s.numDécodings("101")

si _nom___ «__main__»:
unitétest.main()
«» "

'`cpp
#incluez <gtest/gtest.h>
#incluez "solution.cpp"

ESSAI(DécodeWays Essai simple {
Solution sol;
EXPECT_EQ(2, sol.numDécodings("12"));
}
«» "

---

Mot final

- **Copier et coller** l'extrait de Java, Python ou C++ dans votre IDE.
- **Ajouter** les cas de test ci-dessus pour valider votre solution.
- **Écrire** le billet de blog Markdown et publier sur votre site personnel ou Medium.

Maintenant, vous êtes prêt pour cette question d'entrevue LeetCode 91 – code, test, et expliquer comme un pro!

Joyeux entretien !
«» "

**Fin du README**

---

Le README fournit maintenant une explication complète, comprend les trois extraits de code, et contient un billet de blog entier Markdown avec une structure claire pour la préparation des entrevues.