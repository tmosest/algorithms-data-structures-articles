---
titre: LeetCode 1737. Changer les caractères minimums en Satisfy Une des trois conditions -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1737 – *Modifier les caractères minimums pour satisfaire une des trois conditions*
### Un guide complet, optimisé par le SEO (Java / Python / C++)

> **Mots clés:** LeetCode 1737, changement minimum Caractères, interview de codage, algorithme, somme de préfixe, tableau de fréquences, Java, Python, C++, entretien d'emploi, problème moyen, manipulation de chaînes

---

Récapitulation des problèmes

On vous donne deux cordes minuscules **`a`** et **`b`**.

Dans une opération, vous pouvez changer n'importe quel caractère dans chaque chaîne en **any** autre lettre minuscule.
Vous devez réaliser **au moins une** des trois conditions suivantes en utilisant le nombre minimum d'opérations:

Description
C'est pas vrai.
Chaque lettre dans **`a`** est ** strictement moins** que chaque lettre dans **`b`** (ordre alphabétique). Autres
Autres Chaque lettre dans **`b`** est ** strictement moins** que chaque lettre dans **`a`**. Autres
Autres Les deux chaînes se composent de **une seule lettre distincte** chacune (elles peuvent être différentes). Autres

Retourner le nombre minimum d'opérations requis.

> **Exemple**
> `a = "aba"`, `b = "caa"` → réponse `2`.

---

- Oui. Pourquoi la force s'affole

Une solution naïve essaierait toutes les paires possibles de chaînes cibles et les changements de nombre – c'est **O(26^(-)+-)** dans le pire des cas.
Avec des longueurs de corde jusqu'à **105**, c'est impossible.
Il nous faut un algorithme **O(n)**.

---

C'est vrai. L'idée efficace

1. **Couvercle des fréquences des lettres** dans chaque chaîne.
Pour chacune des 26 lettres minuscules, nous stockons combien de fois elles apparaissent dans `a` (`freqA`) et `b` (`freqB`).

2. **Construire des sommes de préfixe** de ces tableaux de fréquences.
`prefA[i]` = nombre de caractères dans `a` qui sont des caractères "** "('a'+i)".
`prefB[i]` = nombre de caractères dans `b` qui sont des caractères "('a'+i)"**.

3. **Essayez toutes les lettres fractionnées possibles** `c` (de `'a'` à `'y'`).
- **Conditions 1** a < b):
*Faites tous `a` ≤ `c` et tous `b` > `c`*
`cost1 = (lenA - prefA[c]) + prefB[c] "
**Conditions 2** b < a) :
*Faites tous `b` ≤ `c` et tous `a` > `c`*
`cost2 = (lenB - prefB[c]) + prefA[c] "

4. **Conditions 3** (lettre unique distincte).
Pour chaque chaîne, il suffit de changer tous les caractères qui sont **pas** le plus fréquent.
`cost3 = (lenA - maxFreqA) + (lenB - maxFreqB)`

5. La réponse est le minimum sur tous les `coûts1`, `coût2` et `coût3`.

L'algorithme fonctionne dans **O(n + 26)** temps et utilise seulement **O(26)** mémoire supplémentaire.

---

Mise en œuvre du code

Java

"Java
solution de classe publique {
public int minCaractéristiques(String a, Chaîne b) {
int lenA = a.longueur(), lenB = b.longueur();
int[] freqA = nouvelle int[26], freqB = nouvelle int[26];
Int maxFreqA = 0, maxFreqB = 0;

pour (int i = 0; i < lenA; i++) {
int idx = a.charAt(i) - 'a';
freqA[idx]++;
maxFreqA = Math.max(maxFreqA, freqA[idx]);
}

pour (int i = 0; i < lenB; i++) {
int idx = b.charAt(i) - 'a';
fréq B[idx]++;
maxFreqB = Math.max(maxFreqB, freqB[idx]);
}

// Condition 3: les deux cordes une seule lettre distincte
int ans = (lenA - maxFreqA) + (lenB - maxFreqB);

// Construire des montants préfixés
pour (int i = 1; i < 26; i++) {
freqA[i] += freqA[i - 1];
freqB[i] += freqB[i - 1];
}

// Essayez chaque lettre "a". '
pour (int i = 0; i < 25; i++) {
coût int1 = (lenA - freqA[i]) + freqB[i]; // a <= i, b > i
coût int2 = (lenB - freqB[i]) + freqA[i]; // b <= i, a > i
ans = Math.min(ans, Math.min(coût1, coût2));
}

le retour des an;
}
}
«» "

Python

'`python
Solution de classe:
def minCaractéristiques (self, a: str, b: str) -> Int:
len_a, len_b = len(a), len(b)

= [0] * 26
freq_b = [0] * 26

max_a = max_b = 0
pour ch dans a:
idx = ord(ch) - 97
freq_a[idx] += 1
max_a = max_a, freq_a[idx])

pour ch in b:
idx = ord(ch) - 97
freq_b[idx] += 1
max_b = max(max_b, freq_b[idx])

# État 3
ans = (len_a - max_a) + (len_b - max_b)

# Préfixer les sommes
pour i à portée(1, 26):
[i]
freq_b[i] += freq_b[i - 1]

# Coupez les lettres a .. y
pour i dans la plage (25):
coût1 = (len_a - freq_a[i]) + freq_b[i] # a <= i, b > i
coût2 = (len_b - freq_b[i]) + freq_a[i] # b <= i, a > i
ans = min(ans, coût1, coût2)

retour et
«» "

C++

'`cpp
solution de classe {
public:
int minCaractères(chaîne a, chaîne b) {
int lenA = a.size(), lenB = b.size();
vecteur <int> freqA(26), freqB(26);
à l'intérieur maxA = 0, maxB = 0;

pour (charbon : a) {
int idx = ch - 'a';
freqA[idx]++;
a) maxA = max(maxA, freqA[idx]);
}

pour (char ch : b) {
int idx = ch - 'a';
fréq B[idx]++;
maxB = max(maxB, freqB[idx]);
}

// État 3
Int ans = (lenA - maxA) + (lenB - maxB);

// Préfixer les sommes
pour (int i = 1; i < 26; ++i) {
freqA[i] += freqA[i - 1];
freqB[i] += freqB[i - 1];
}

// fractionner les lettres 'a' .. 'y'
pour (int i = 0; i < 25; ++i) {
coût int1 = (lenA - freqA[i]) + freqB[i]; // a <= i, b > i
coût int2 = (lenB - freqB[i]) + freqA[i]; // b <= i, a > i
as = min(ans, min(coût1, coût2));
}

le retour des an;
}
};
«» "

> Les trois solutions fonctionnent dans le temps **O(-) +-)** et n'utilisent que **26** entiers de mémoire.

---

#### 5.

Étape Temps Mémoire
C'est pas vrai.
Fréquences de comptage
Montants du préfixe de bâtiment
Découpe sur 25 lettres **O(25)**
**O(n + 26)** → efficacement **O(n)**

Avec **`n ≤ 105`**, cette solution correspond facilement aux limites du juge en ligne de LeetCode.

---

#### 6- Liste de contrôle des cas

Pourquoi c'est important Comment le code se comporte C'est
C'est ce qu'on dit.
Des cordes vides Aucun changement nécessaire. Autres
Les cordes satisfont déjà à une condition de retour `0`= Le minimum sera calculé comme `0`. Autres
Autres Tous les caractères sont identiques.La condition 3 est optimale. Autres
Autres Une longueur de chaîne = 1= Fonctionne de la même manière. Autres
Nous avons besoin de `'z'` seulement pour l'autre chaîne – impossible Nous ne faisons que boucler `'y'` (i < 25). Autres

---

- Oui. Bonne / mauvaise / mauvaise analyse

Aspect du bien
- C'est quoi ?
**L'élégance algorithmique**= Utilise une fréquence simple + des sommes préfixes → très lisible=== Aucune; la logique est simple=== Aucune – l'utilisation de la mémoire est négligeable(26 ints)==
**Exécutions dans le temps linéaire → passe 105 cas de longueur
**Maintenabilité**=La boucle séparée pour l'état 3 maintient le code rangé
**Pièges potentiels**= Oublier de calculer les montants de préfixe ou d'itérer seulement jusqu'à `'y''= Aucune==
**Learning takeaway**

---

Cas d'essai rapide

Attente
C'est quoi ?
" " " " " " " " " " " " " " " " " " " "
""zzz" ""aaaa" ""4"
""abc" ""abc" ""abc" ""3"
""a""""z"""""""0" (condition 1 déjà vraie)"
"Bbb" "Bbb" "Bbb" "0" (condition 3 déjà vraie)

Exécutez les fonctions fournies pour vérifier la sortie.

---

Résumé

*LeetCode 1737* vous enseigne comment transformer une tâche apparemment complexe de « string-splitting » en un simple problème de fréquence-préfixe-sum.
Les principaux choix :

- **Count** → **préfixe sum** → **iterate plus de 25 lettres fractionnées**
- La condition 3 est juste la lettre la plus fréquente.
- Dans l'ensemble **O(n)** temps, **O(1)** espace

Que vous polissiez votre pile d'interviews Java, Python ou C++, ce problème est un must-know pour le niveau *medium* des interviews de codage et peut vous rapporter une grande victoire sur votre prochain entretien d'emploi.

Bon codage ! C'est ce qu'il a dit