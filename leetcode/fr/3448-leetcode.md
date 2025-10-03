---
titre: LeetCode 3448. Sous-chaînes de comptage Divisible par le dernier chiffre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Cracking LeetCode 3448: Sous-chaînes de comptage Divisible par le dernier chiffre
*O(n) Solutions en Java, Python et C++ – une interview complète Guide prêt*

---

TL;DR

- **Problème** – Compter toutes les sous-chaînes d'une chaîne à chiffres divisibles par leur dernier chiffre **non-zéro**.
- **Hardness** – «Hard» sur LeetCode.
- ** Solution optimale** – Une passe ('O(n)'), en utilisant des restes de préfixe et une petite table de fréquence pour chaque règle de division du chiffre.
- **Langues** – Java, Python, C++.
- **Mots-clés de référence** – *LeetCode 3448*, *sous-chaînes de comptes divisibles par le dernier chiffre*, *solution O(n)*, *Java, Python, C++*, *algorithme d'entrevue*, *programmation dynamique*, *règles de division*.

---

- Oui. 1. Aperçu du problème

> **Input**: Une chaîne `s` (`1 ≤=1 ≤=105`) ne contenant que des chiffres décimaux.
> **Output**: Le nombre de sous-chaînes `s[i...j]` de telle sorte que:
> * `s[j] != «0» (le dernier chiffre est non-zéro)
> * l'entier représenté par la sous-chaîne est divisible par la valeur de son dernier chiffre.

> **Exemple**
> `s = "12936"` → `11` sous-chaînes satisfont à la condition.

La clé est que *leading zéros sont autorisés*, de sorte que `"01"` est une sous-chaîne valide, mais une sous-chaîne se terminant par `'0'` est ignorée.

---

- Oui. 2. Contraintes et causes de bord

C'est vrai.
C'est le cas.
Jusqu'à 100 000 $ doivent être linéaires.
"0" ne forme jamais un dernier chiffre valide
Le résultat de débordement peut être jusqu'à 5 × 109. Autres

---

- Oui. 3. Approches naïves et leurs pièges

L'approche La complexité Pourquoi il échoue
C'est le cas.
Énumérer toutes les sous-chaînes et vérifier la disvisibilité à la volée.
Précalculer les valeurs entières de toutes les sous-chaînes
Une programmation dynamique avec l'état `(endIndex, reste)''''O(n·10·10)''' Encore trop grande; nous pouvons faire mieux

Parce que chaque dernier chiffre a une règle de division *spécifique* (par exemple `4` dépend uniquement des deux derniers chiffres, `8` sur les trois derniers, `3` sur la somme des chiffres), nous pouvons en profiter et éviter tout comportement quadratique.

---

- Oui. 4. Stratégie O(n) optimisée

4.1 Règles de divisibilité par dernier chiffre

Règle Mise en œuvre
-- -- -- -- -- -- -- -- --
Chaque nombre se terminant par ces chiffres est divisible par `d`. Autres
Un nombre est divisible par `3` (ou `9`) si la somme de ses chiffres est. Conserver le reste du modulo `3`/`9` et compter les correspondances. Autres
Autres **4**= Divisible si les derniers **deux** chiffres forment un nombre divisible par 4=Cochez `(10*prevDigit + d) % 4'=
Autres **8**= Divisible if les derniers **trois** chiffres (ou les deux derniers pour `j==1′) forment un nombre divisible par 8=Cochez `(100*d3 + 10*d2 + d) % 8=
Autres **7**= Il faut un peu plus de maths: `n % 7=0`=1 `n = 100·a + 101·b + ...` → nous utilisons le préfixe restant modulo 7 et une petite table à 6 cycles. Précalculer les inverses de `10^k mod 7` (`k=0,5`) et rechercher les fréquences. Autres
Autres ****************************************************************************************************************************************************************************************************************************************************************

4.2 Préfixer les restes

Pour les chiffres qui se basent sur *toute la sous-chaîne* (`3,6,9,7"), nous maintenons le reste courant:

Texte
préfixe[i] = (valeur de s[0...i]) % 7
«» "

Utiliser le reste au **end** d'une sous-chaîne est suffisant parce que pour une sous-chaîne `s[l...r] "

«» "
valeur(l,r) % d == 0 φ préfix[r] % d == préfix[l-1] * (10^(r-l+1) mod d) % d
«» "

- Pour `3,6,9` le multiplicateur est toujours `1` (le reste est indépendant de la longueur de la sous-chaîne).
- Pour `7` le multiplicateur change toutes les 6 positions parce que `10^k mod 7` répète avec la période 6.

4.3 Tableaux de fréquence

Pour chaque règle, nous maintenons un petit éventail de comptes :

Texte
freq3[0,2] // nombre de restes préfixés modulo 3
freq9[0..8] // nombre de restes préfixés modulo 9
freq7[0,5][0,6] // pour le 6-cycle de 7
«» "

Au cours du seul scan, nous:

1. **Count** la contribution actuelle en utilisant la règle appropriée.
2. **Mise à jour** du tableau de fréquence correspondant pour les postes ultérieurs.

Parce que nous utilisons toujours les valeurs préfixes *déjà traitées*, l'algorithme reste linéaire.

---

- Oui. 5. Mise en œuvre

> **Conseil** – Les trois implémentations utilisent la même idée de base.
> Les seules différences sont la syntaxe, la gestion des tableaux et la prise en charge intégrée des grands entiers.

#### 5.1 Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe publique {
// Inverses précalculées de 10^k mod 7 pour k = 0,5
int final statique privé[] INV7 = {1, 5, 2, 3, 6, 4};

compte public longSubstrings(String s) {
int n = s.longueur();
long[] pref3 = nouveau long[n];
long[] pref9 = nouveau long[n];
long[] pref7 = nouveau long[n];
long[] prefAll = nouveau long[n]; // préfixe mod 3 (même que pref3)
long[] freq3 = nouveau long[3];
long[] freq9 = nouveau long[9];
long[]] freq7 = nouveau long[6][7]; // 6-cycle × 7 restes

résultat long = 0;
pour (int j = 0; j < n; ++j) {
int d = s.charAt(j) - '0';
si (d == 0) { // sauter les sous-chaînes se terminant par 0
poursuivre;
}

// -------- Règle pour les chiffres 1,2,5 ---------
si (d) d) d) 5) {
résultat += j + 1; // toutes les sous-chaînes se terminent à j
}

// -------- Règle pour les chiffres 3,6,9 ---------
Sinon, si (d) 6) {
long rem = pref3[j];
résultat += freq3[rem] + (rem == 0 ? 1 : 0);
} sinon si (d) 9) {
long rem = pref9[j];
résultat += freq9[rem] + (rem == 0 ? 1 : 0);
}

// -------- Règle pour le chiffre 4 ---------
Sinon si (d) 4) {
Si (j) 0) {
résultat += 1; // seul le seul chiffre
} autre {
int dernier Deux = (s.charAt(j - 1) - '0') * 10 + d;
résultat += (dernier % 4 == 0 ? (j + 1) : 1);
}
}

// -------- Règle pour le chiffre 8 --------
Sinon si (d) 8) {
Si (j) 0) {
résultat += 1;
} sinon si (j) 1) {
int dernier Deux = (s.charAt(0) - '0') * 10 + 8;
résultat += (dernier % 8 == 0 ? 2 : 1);
} autre {
int last3 = (s.charAt(j - 2) - '0') * 100
+ (s.charAt(j - 1) - '0') * 10 + 8;
int last2 = (s.charAt(j - 1) - '0') * 10 + 8;
si (dernier 3 % 8) 0) résultat += j - 1;
si (dernier 2 % 8) 0) résultat += 1;
résultat += 1; // la sous-chaîne à un chiffre
}
}

// -------- Règle pour le chiffre 7 ---------
Sinon si (d) 7) {
long rem = pref7[j];
résultat += (rem == 0 ? 1 : 0);
// Analyser les 6 exposants possibles k (0...5)
pour (int k = 0; k < 6; ++k) {
int idx = (j % 6 - k + 6) % 6;
int nécessaire = (int)((rem * INV7[k]) % 7);
résultat += freq7[idx][nécessaire];
}
}

// - Oui. Mettre à jour les tableaux de préfixes ---------
// Calculer de nouvelles valeurs préfixes pour la prochaine itération
pref3[j] = (j == 0 ? d : (pref3[j - 1] * 10 + d) % 3);
pref9[j] = (j == 0 ? d : (pref9[j - 1] * 10 + d) % 9);
pref7[j] = (j == 0 ? d : (pref7[j - 1] * 10 + d) % 7);

// Mettre à jour les fréquences pour les positions futures
freq3[pref3[j]]++;
freq9[pref9[j]]++;
freq7[j % 6][pref7[j]]++;
}
le résultat du retour;
}
}
«» "

> **Pourquoi cela fonctionne** –
> * Chaque `d` est traité en temps constant.
> * Les tables de fréquence (`freq3`, `freq9`, `freq7`) contenir seulement **peu** entrées, donc l'utilisation de la mémoire est minuscule.
> * La seule passe garantit le temps "O(n)".

---

5.2 Python

'`python
Solution de classe:
INV7 = [1, 5, 2, 3, 6, 4]

def countSubstrings(self, s: str) -> Int:
n = len(s)
pref3 = [0] * n
pref9 = [0] * n
pref7 = [0] * n

freq3 = [0] * 3
freq9 = [0] * 9
freq7 = [[0] * 7 pour _ dans la plage(6)]

ans = 0
pour j dans la plage(n):
d = int(s[j])

Si d] 0: # jamais un dernier chiffre valide
poursuivre

# 1, 2, 5 – toujours divisible
si d en (1, 2, 5):
ans += j + 1

# 3, 6, 9 – règle de la somme des chiffres
elif d in (3, 6, 9):
rem = pref3[j] si d dans (3, 6) sinon pref9[j]
si d en (3, 6):
ans += freq3[rem] + (1 si rem == 0 autre 0)
Sinon : # d == 9
ans += freq9[rem] + (1 si rem == 0 autre 0)

# 4 – deux derniers chiffres
élif d == 4:
Si j == 0:
+= 1
Sinon:
last_two = int(s[j-1:]) # deux chiffres se terminant à j
si last_deux % 4 == 0 & #160;:
ans += j + 1
Sinon:
+= 1

# 8 – les trois derniers chiffres (ou deux pour j) 1 )
élif d == 8:
Si j == 0:
+= 1
Il n'y a pas d'autre solution.
last_two = int(s[0:2])
ans += 2 si last_deux % 8 == 0 autre 1
Sinon:
Last_three = int(s[j-2:j+1])
Last_two = int(s[j-1:j+1])
si last_trois % 8 == 0 & #160;:
ans += j - 1
si last_deux % 8 == 0 & #160;:
+= 1
+= 1

# 7 – besoin du multiplicateur de 6 cycles
élif d == 7:
rem = pref7[j]
+= 1 si rem == 0 autre 0
pour k dans la plage(6):
idx = (j % 6 - k + 6) % 6
nécessaire = (rem * self.INV7[k]) % 7
ans += freq7[idx][nécessaire]

# calculez les restes du préfixe
Si j == 0:
pref3[j] = d % 3
pref9[j] = d % 9
pref7[j] = d % 7
Sinon:
pref3[j] = (pref3[j-1] * 10 + d) % 3
pref9[j] = (pref9[j-1] * 10 + d) % 9
pref7[j] = (pref7[j-1] * 10 + d) % 7

# les fréquences de mise à jour
freq3[pref3[j]] += 1
freq9[pref9[j]] += 1
[j % 6][pref7[j]] += 1

retour et
«» "

> **Spécifications du python** –
> * Utilise `int(s[a:b])` pour l'extraction rapide des derniers 2 ou 3 chiffres.
> * `INV7` est une liste globale, empêchant la recréation dans la boucle.

---

### 5.3 C++ (GCC 17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
constexpr statique int INV7[6] = {1, 5, 2, 3, 6, 4};

public:
int countSubstrings(string s) {
int n = s.size();
vecteur <int> pref3(n), pref9(n), pref7(n);
vecteur <long long> freq3(3), freq9(9);
vecteur <array<long long,7>> freq7(6); // 6-cycle × 7

long an = 0;
pour (int j = 0; j < n; ++j) {
l'élément d = s[j]-'0';
si (d == 0) continuer;

// 1, 2, 5
si (d) d) d) 5) {
ans += j + 1;
}
// 3, 6, 9
Sinon, si (d) 6) {
int rem = pref3[j];
as += freq3[rem] + (rem==0);
} sinon si (d) 9) {
int rem = pref9[j];
ans += freq9[rem] + (rem==0);
}
// 4
Sinon si (d) 4) {
i (j == 0) ans += 1;
autres {
int dernier Deux = (s[j-1]-'0')*10 + d;
ans += (dernier 2 % 4 == 0 ? j+1 : 1);
}
}
// 8
Sinon si (d) 8) {
i (j == 0) ans += 1;
Sinon si (j) 1) {
int dernier Deux = (s[0]-'0')*10 + 8;
ans += (dernier 2 % 8 == 0 ? 2 : 1);
} autre {
int last3 = (s[j-2]-'0')*100 + (s[j-1]-'0')*10 + 8;
int last2 = (s[j-1]-'0')*10 + 8;
si (dernier 3 % 8) 0) ans += j-1;
si (dernier 2 % 8) 0) ans += 1;
+= 1;
}
}
// 7
Sinon si (d) 7) {
int rem = pref7[j];
ans += (rem==0);
pour (int k=0;k<6;k++) {
int idx = (j%6 - k + 6)%6;
besoin int = (rem * INV7[k]) % 7;
ans += freq7[idx][besoins];
}
}

// mettre à jour préfixe les restes pour la prochaine ronde
pref3[j] = (j==0? d : (pref3[j-1]*10 + d)%3);
pref9[j] = (j==0? d : (pref9[j-1]*10 + d)%9);
pref7[j] = (j==0? d : (pref7[j-1]*10 + d)%7);

// mises à jour freq
freq3[pref3[j]]++;
freq9[pref9[j]]++;
freq7[j%6][pref7[j]]++;
}
le retour des an;
}
};
«» "

> ** Notes C++** –
> * Utilise `vector` pour les tableaux dynamiques.
> * `array<long long,7>` pour la table intérieure fixe, qui est légèrement plus rapide que `vecteur`.

---

- Oui. 6. Résumé de la complexité

Langue
- C'est quoi ?
Java (n) ~50 octets
Python O(n)
O(n)=50 octets

> **Pourquoi `O(1)` par poste** –
> Chaque `d` déclenche au plus une poignée d'accès au réseau et d'opérations arithmétiques.

---

- Oui. 7. Essais et validation

- **Tests unitaires** – Vérifiez manuellement les petites chaînes (`"12345"`, `"9876543210"`, `"1111111"`).
- **Tests de résistance** – Chaînes aléatoires jusqu'à 10^5" chiffres; comparer avec un algorithme de force brute sur un ensemble de données réduit (`n ≤ 2000`) pour valider la justesse.
- **Cas d'urgence** –
- Tous les chiffres sont les mêmes (`"1111"`, `"2222"`, `"4444"`, `"7777"`).
- Cordes se terminant par « 0 » (support d'assurances).
- Longueur maximale de la chaîne aléatoire (chiffres `1e5`).

---

- Oui. 8. Conclusion

> **Takeaway** – Un problème apparemment lourd de comptage sur toutes les sous-chaînes d'un nombre décimal peut être résolu en temps linéaire par :
>
> 1. Grouper les chiffres par *propriétés de division mathématique*.
> 2. Utiliser **préfixer les restes** et les tables de fréquences courtes.
> 3. Numériser une fois, calculer chaque contribution en temps constant.
>
> Cette approche s'applique aussi bien aux autres contrôles de divisibilité (par exemple, «n % 11», «n % 13») – seulement la période de cycle et la modification inverse du tableau.

> **Pourquoi tu devrais te souvenir de ça** –
> Le même schéma apparaît dans de nombreux problèmes d'entrevue:
> *Réduire le problème dans un petit espace (préfixer le reste + la position) et utiliser une carte de fréquence pour accumuler les comptes. *

---

> ** Bon codage !**
> Si vous avez aimé cette solution, donnez-lui un -- sur GitHub ou déposez un -- sur le dépôt.
> *Codage heureux – et que vos numéros soient toujours divisibles! *