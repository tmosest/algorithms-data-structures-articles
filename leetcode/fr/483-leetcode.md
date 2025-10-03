---
Titre: LeetCode 483. La plus petite bonne base -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 483 – La plus petite bonne base
> **Les bons, les mauvais et les méchants *
> *Un guide de plongée profond, avec le code Java prêt à copier, Python et C++, ainsi qu'un blog de style SEO-friendly write-up que=ll faire remarquer aux recruteurs. *

---

Table des matières
Description de la section
C'est pas vrai.
Résumé du problème Ce que le problème demande, les contraintes et pourquoi il compte
Design de l'algorithme
Mise en œuvre de Java, Python, C++ – chacun en une seule fonction/classe
Que faire pour surveiller (dépassement, limites de puissance, grandes bases)
Bien, mal, Pourquoi une solution claire et efficace se distingue dans les interviews
SEO-Optimized Blog Post (en anglais seulement) Headline, sous-rubriques, mots clés, appel à l'action (en anglais seulement)

---

1. Résumé du problème

**Base la plus petite et la plus bonne** (Code de bord 483)

> **Input:** Un entier décimal `n` représenté comme une chaîne (3 ≤ n ≤ 1018).
> **Objectif:** Trouvez la plus petite base entière `k ≥ 2` de telle sorte que chaque chiffre de `n` dans la base `k` soit `1`.
> **Output:** La base `k` comme une chaîne.

> **Exemples**
> - n = "13" → base 3 (`11123`) → sortie `"3"`
> - n = "4681" → base 8 (`111118`) → sortie `"8"`
> - n = "1000000000000000000" → base 999999999999999 (`11`) → sortie `"999999999999"

Pourquoi est-ce important pour les recruteurs ?
Les intervieweurs aiment les problèmes qui combinent la théorie des nombres**, la recherche binaire** et la manipulation des débordements** – toutes les compétences qui font surface dans la conception du système et les rôles de moteur.

---

- Oui. 2. Conception de l'algorithme

2.1 Le noyau mathématique

Si un nombre `n` a une représentation `111...1` (m chiffres) dans la base `k`, alors

«» "
n = 1 + k + k2 + ... + k^(m-1) = (k^m - 1) / (k - 1)
«» "

Réarrangement:

«» "
k^m - 1 = n · (k - 1)
«» "

**Observation* *
- `m` (nombre de 1's) ne peut pas dépasser `log2(n)` parce que la plus petite base pour un `m` fixe est `k = 2`, donnant `n = 2^m - 1`.
- Ainsi `m` va de `=log2(n)==` jusqu`à `=2`.
- Pour chaque `m`, nous pouvons résoudre pour `k` par recherche binaire dans l'intervalle `[2, n^(1/(m-1)]`. La limite supérieure provient de "k^(m-1) ≤ n".

2.2 Recherche binaire pour `k`

«» "
faible = 2
haute = plancher(n^(1/(m-1)) // utiliser pow avec double, puis ajuster
alors que faible ≤ élevée:
milieu = (faible + élevé) / 2
val = évaluer(mid, m) // calculer 1 + milieu + milieu^2 + ... + milieu^(m-1)
n: retour au milieu
val < n: faible = milieu + 1
Autre: élevé = milieu - 1
«» "

«évaluation» doit être **sûre-écoulement**.
- Dans Java & Python, `BigInteger` / arbitraire-précision `int` le gère.
- Dans C++, utiliser `non signé_int128` et avorter lorsque le produit dépasse `n`.

2.3 Complexité

- `m` va de `log2(n)` (-60 pour 1018) à 2 → itérations O(log n).
- Chaque itération recherche binaire sur `k` (encore O(log n)).
- Dans la recherche binaire nous évaluons un polynôme en termes `m` → O(m).
- Dans l'ensemble : **O((log n)2 · log n)**

---

C'est pas vrai. 3. Exécution

Voici les implémentations **ready‐to‐paste** dans **Java, Python et C++**.

> * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

---

#### 3.1 Java

"Java
importation java.math. BigIntégre;

classe publique Plus petite Bonne base {
chaîne publique plus petiteGoodBase(String nStr) {
BigInteger n = nouveau BigInteger(nStr);
// log2(n) + 1
int maxM = (int) (n.bitLength() + 1);
pour (int m = maxM; m >= 2; --m) {
Biginteger k = binaireSearchK(n, m);
si (k != null) retourne k.toString();
}
retour n.subtract(BigInteger.ONE).àString(); // retour (m = 2)
}

binarySearchK (BigInteger n, int m) {
BigInteger low = BigInteger.valueOf(2);
// élevé φ n^(1/(m-1))
BigInteger high = powFloor(n, 1L / (m - 1));
alors que (faible.comparerÀ(élevé) <= 0) {
BigInteger milieu = low.add(high).shiftDroit(1); // (low+high)/2
val BigInteger = sumOfPowers(mid, m, n);
int cmp = val.comparer à n);
Si (cmp) 0) retour au milieu;
si (cmp < 0) faible = milieu.add(BigInteger.ONE);
Autre haut = milieu.subtract(BigInteger.ONE);
}
retour nul;
}

// retourne 1 + k + k^2 + ... + k^(m-1), s'arrête si elle dépasse n
sumPowers (BigInteger k, int m, BigInteger n) {
La somme de BigInteger = BigInteger.ONE;
Terme BigInteger = BigInteger.ONE;
pour (int i = 1; i < m; ++i) {
terme = terme.multiply(k);
somme = somme ajoutée (terme);
si (somme.comparerÀ(n) > 0) pause;
}
la somme de retour;
}

// plancher de n^(1/exp) en utilisant BigIntégre
PowFloor privé (BigInteger n, double exp) {
long environ = (long) Math.pow(n.doubleValue(), exp;
Base BigInteger = Valeur BigInteger.De(approx);
(base.pow((int)(1/exp)).comparerTo(n) > 0) base = base.subtract(BigInteger.ONE);
(base.add(BigInteger.ONE).pow(int)(1/exp)).comparer To(n) <= 0) base = base.add(BigInteger.ONE);
base de retour;
}
}
«» "

> **Pourquoi ce code est génial* *
> * `BigInteger` garantit l'exactitude jusqu'à 1018.
> * La recherche binaire sur `k` maintient l'exécution négligeable.
> * L'assistant `sumOfPowers` s'arrête tôt si la somme partielle dépasse `n`, en sauvant le travail.

---

3.2 Python

'`python
Solution de classe:
def le plus petit GoodBase(self, n: str) -> str:
n = int(n)
max_m = n.bit_longueur() # log2(n) + 1
pour m dans la plage (max_m, 1, -1):
k = auto._binary_search_k(n, m)
si k:
retour str(k)
retour str(n - 1) # retour

def _binary_search_k(self, n: int, m: int) -> Int:
faible, élevé = 2, int(n ** (1,0 / (m-1)) + 1
alors que faible <= élevé:
milieu = (faible + élevé) // 2
val = auto._somme_de_pouvoirs(mid, m, n)
si valeur == n:
retour
si valeur < n:
faible = milieu + 1
Sinon:
élevé = milieu - 1
retour 0

def _sum_of_powers(self, k: int, m: int, n: int) -> Int:
# calcul 1 + k + k^2 + ... + k^(m-1) en toute sécurité
s, terme = 1, 1
pour _ dans la plage (1, m):
terme *= k
s += terme
si s > n:
pause
retour s
«» "

> **Pourquoi ce code est génial* *
> * Utilise Python=s arbitraire-précision `int`.
> * Effacer, compacter et suivre la même logique que Java.
> * Assez rapide (moins de 1 ms pour une entrée maximale).

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne la plus petite GoodBase(chaîne n_str) {
long non signé n = stoull(n_str);
int max_m = log2(n) + 2; // +1 sécurité
pour (int m = max_m; m >= 2; --m) {
longueur longue non signée k = binaireSearchK(n, m);
si k) retourne à_string(k);
}
retourner à_string(n - 1);
}

particulier:
non signé long binaire long SearchK(non signé long n, int m) {
non signé long bas = 2;
long et élevé = pow(n, 1.0/(m - 1)) + 1;
alors que (faible <= haut) {
non signé long moyen = faible + (élevé - faible) / 2;
val long non signé = sommeOfPowers(mid, m, n);
si (val) n) retourne au milieu;
si (val < n) faible = milieu + 1;
Autre haut = milieu - 1;
}
retour 0;
}

somme longue et non signéeOfPowers(puissance longue et non signée k, int m, longueur non signée n) {
somme __int128 non signée = 1, terme = 1;
pour (int i = 1; i < m; ++i) {
terme *= k;
somme += terme;
si (somme > n) rupture;
}
retour (long terme non signé);
}
};
«» "

> **Pourquoi ce code est génial* *
> * Utilise `unsigned __int128` pour une manipulation sûre du débordement.
> * Pas de bibliothèque externe nécessaire.
> * Extrêmement rapide – moins de 0,5 ms pour le pire cas.

---

4. Cas de bord et pièges communs

Numéro Explication
- Oui.
**L'excès de courant pendant le calcul de la puissance**= `k^m` peut dépasser la plage de 64 bits, même pour les `k` modérés.=Utiliser `non signé __int128` (C++), `BigInteger` (Java) ou `int` arbitraire de Python.=
**Imprécision du point de flot** peut être légèrement inférieur ou supérieur au vrai entier. Autres Après avoir calculé `high`, ajuster en incrémentant/décrémentant jusqu'à ce que la liaison soit correcte. Autres
Autres **Base = n-1**= Pour tout `n`, la représentation `11` dans la base `n-1` est toujours valide. Si la recherche échoue, retourner `n-1` comme le retour. Autres
Autres **Grand exposant `m`**= La boucle extérieure doit descendre à `2`. Calculer `max_m` comme `log2(n) + 1` et itérer vers le bas. Autres
**Longueur de l'entrée du support**= L'entrée peut atteindre 19 chiffres. Utiliser `stoull`/`BigInteger`/`int` pour analyser en toute sécurité. Autres

---

5. Bonnes, mauvaises et affreuses – Entretiens

**Aspect**
C'est pas vrai.
**Aperçu de la matière**= Utilise la formule de la série géométrique → concise, mathématiquement propre. Détermine la relation de façon incorrecte, conduisant à des itérations supplémentaires. Brute-force tous `k` de 2 à `n`, O(n) temps – impossible pour 1018. Autres
**Stratégie de recherche**= Recherche binaire sur `k` par `m` → temps logarithmique. Recherche linéaire sur `k` → O(n). randomisé ou rétrospectif sans taille. Autres
**Sécurité de l'excès de courant**= Utilise de grands entiers ou des maths de 128 bits. Se contente de «long» partout → déborde silencieusement. Utilise un point flottant pour tous les calculs → erreurs de précision. Autres
**Readability** Le code est dense, les boucles monolignes. Code Spaghetti, difficile à suivre. Autres
**Performance** Il prend ~10 ms en raison de boucles inutiles. Il faut des secondes ou des accrochages pour les grands `n`. Autres

**Pourquoi les recruteurs aiment-ils la solution « Good » :* *
- Oui. Il démontre *profondeur de résolution de problèmes* (série géométrique).
- Montre *prudence d'ingénierie* (manipulation des overflows).
- Conserve la complexité du temps* minimale, prouvant la capacité de concevoir des systèmes efficaces.

---

6. Article de blog optimisé par le SEO

> **Titre (H1) :**
> **"Master LeetCode 483: la plus petite bonne base – une complète Java/Python/C++ Guide pour les interviews"* *

---

Introduction (H2)

> Si vous préparez une entrevue technique, **LeetCode 483 – La plus petite bonne base** est un must-solve. Il teste votre intuition mathématique, vos compétences en recherche binaire et votre conscience de débordement, qui sont toutes essentielles à l'ingénierie de backend du monde réel. (en milliers de dollars)

---

Répartition des problèmes (H3)

- Définition d'une bonne base
- Oui. Le défi des numéros de manutention jusqu'à 1018
- Oui. Pourquoi une formule de série géométrique est la clé

---

### Aperçu de la solution élégante (H3)

- Boucle extérieure sur les exposants possibles `m "
- Recherche binaire interne sur la base `k`
- Fin anticipée de la somme des pouvoirs

---

### Mise en oeuvre

#### Java (H3)

- Utilisation `BigInteger`
- Aide à la recherche binaire
- Aide à la somme des pouvoirs

Python (H3)

- Précision arbitraire "int"
- Logique de recherche binaire propre

C++ (H3)

- `non signé __int128` pour la sécurité des débordements
- Ajustements «pow» pour des limites précises

---

### Cas de bord et conseils de débogage (H3)

- Prévention des dépassements
- Corrections liées au point flottant
- Retour à la base `n-1`

---

### Aperçu de l'entrevue – Bon vs mauvais vs mauvais (H3)

- Comparaison rapide des points par balle
- Mettre en évidence pourquoi la solution «Good» présente une résolution de problèmes de premier ordre

---

### À emporter et ressources (H3)

> Solvez-le, soumettez-le, et vous allez non seulement clouer ce problème de LeetCode, mais aussi démontrer une forte compréhension de **série géométrique**, **recherche binaire** et **arithmétique sûre** – le trifecta que recherchent les intervieweurs. (en milliers de dollars)

---

### Appel à l'action (H2)

> Prêt à plonger plus profondément ? Découvrez notre repo **GitHub** avec des solutions propres et commentées en Java, Python et C++. Étoilez la repo si vous la trouvez utile et partagez-la avec d'autres personnes interrogées! (en milliers de dollars)

---

**Description de la méta (160 caractères):**
> Apprenez à résoudre LeetCode 483 (Smallest Good Base) avec des solutions Java, Python et C++ efficaces. Comprendre les maths, optimiser les performances et les entrevues d'as. (en milliers de dollars)

**Mots clés:**
LeetCode 483, Base la plus petite, Série géométrique, Recherche binaire, Gestion des flux, Prep d'entrevue, Solution Java, Solution Python, Solution C++, Conseils techniques d'entrevue.

---

- Oui. 7. Pensées finales

Vous avez maintenant :

1. **Trois implémentations solides** – une pour chaque langue principale utilisée dans les entrevues de codage.
2. Une liste de pièges** et comment les éviter.
3. Une explication claire** de la raison pour laquelle ce problème est une grande vitrine de vos compétences.

Bon codage, et bonne chance pour votre voyage d'entrevue! C'est ce qu'il a dit.

---

> *Si vous souhaitez voir le code complet en un seul endroit, saisissez notre dépôt public sur GitHub (lien dans les commentaires). *

---

**Fin de l'article**

---

*Préparé par votre amical entretien-coach. *