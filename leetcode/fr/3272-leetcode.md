---
titre: LeetCode 3272. Trouvez le compte de bons entiers -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 3272 – Trouver le compte de bons entiers

> **Problème**
> On vous donne deux entiers `n` (1 ≤ n ≤ 10) et `k` (1 ≤ k ≤ 9).
>
> *Un entier k-palindromique* est un palindrome divisible par `k`.
> *Un bon entier* est un nombre à chiffres `n` dont les chiffres peuvent être réaménagés en un entier palindrimique k (sans diriger de zéros).
> **Objectif:** Retourner le nombre de bons entiers `n`.

Les contraintes sont minuscules, donc une solution combinatoire exacte est possible. Ci-dessous vous trouverez:

Langue Solution Temps Espace
- C'est quoi ?
*Java** * O(10<sup>n/2</sup>) * O(1)
*Python *(10<sup>n/2</sup>)
*C++*** O(10<sup>n/2</sup>)

> **Pourquoi vous devriez vous soucier** – Ce problème est une vitrine parfaite pour les intervieweurs : il teste le rétro-tracking, la combinatoire, la mémorisation factorielle et la manipulation des cas de bord (leading zéros). La maîtrise vous aidera à décrocher votre prochain poste de chef de file technologique ou de chef de file en développement.

---

Défaillance du problème

1. **Génération du Palindrome**
Le nombre de palindromes `n` à chiffres est au plus `10^(ceil(n/2)', soit au plus 10 000 lorsque `n=10`. Nous pouvons tous les forcer.

2. **Check k-palindromic**
Convertir chaque palindrome en un entier et tester la disvisibilité par `k`.

3. **Comptage des bons nombres**
Pour chaque palindrome k-palindromic, nous devons savoir combien de permutations distinctes de ses chiffres produisent un entier valide `n` (pas de zéro de tête).
* Permutations totales = `n! / (freq[0]! * ... * freq[9]!)`.
* Permutations non valides (premier chiffre = 0) = `(n‐1)! / ((freq[0]-1)! * ... * freq[9]!)».
* Permutations valides = total – invalide.

4. **Dupliquer**
Deux palindromes différents peuvent partager le même multiset de chiffres; nous ne devrions compter chaque multiset de chiffres uniques qu'une seule fois.

---

Algorithme en anglais clair

«» "
réponse = 0
visité = ensemble vide de cartes de fréquence à chiffres

pour chaque palindrome à chiffres n P:
si P % k == 0:
freq = carte de fréquence des chiffres en P
si freq n'est pas visité:
Total = n! / prod(freq[d]!)
zéroRem = si freq[0] > 0 alors (n‐1)! / prod(freq[d]! avec freq[0] réduit de 1) autre 0
réponse += total - zéro Rem
visité.add(freq)
réponse de retour
«» "

Parce que `n ≤ 10`, nous pouvons pré-calculer des facteurs jusqu'à 10 une fois et les réutiliser.

---

Code

Voici des implémentations idiomatiques propres dans **Java**, **Python** et **C++**.

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
privé statique final long[] FACT = nouveau long[11];
statique {
FACT[0] = 1;
pour (int i = 1; i <= 10; i++) FACT[i] = FACT[i - 1] * i;
}

permCount(int[] freq, int total) {
long res = FACT[total];
pour (int f : freq) res /= FACT[f];
retour rés;
}

longue privée permCountZero(int[] freq, int total) {
si (freq[0]] 0) retour 0;
freq[0]--; // réserver le zéro de départ
longue rés = FACT[total - 1];
pour (int f : freq) res /= FACT[f];
freq[0]++; // restauration
retour rés;
}

compte public longGoodIntegers(int n, int k) {
réponse longue = 0;
Set<String> visité = nouveau HashSet<>();

int[] moitié = nouvelle int[(n + 1) / 2];
générer(0, moitié, n, k, visité, réponseHolder -> réponse += réponseHolder);
réponse de retour;
}

le vide privé génère(int pos, int[] moitié, int n, int k,
Set<String> visité, java.util.fonction.LongConsumer add) {
si (pos=mi-longueur) {
int[] chiffres = buildPalindrome(demi, n);
valeur longue = 0;
pour (int d : chiffres) valeur = valeur * 10 + d;
si (valeur % k) 0) {
int[] freq = nouvelle int[10];
pour (int d : chiffres) freq[d]++;
Clé de chaîne = Arrays.toString(freq);
si (!visited.contient(clé)) {
visité.add(clé);
add.accept(permCount(freq, chiffres.longueur) -
permCountZero(freq, chiffres.longueur);
}
}
retour;
}
pour (int d = (pos == 0 ? 1 : 0); d <= 9; d++) {
demi[pos] = d;
générer(pos + 1, moitié, n, k, visité, ajouter);
}
}

privée int[] buildPalindrome(int[] half, int n) {
int[] p = nouvelle int[n];
pour (int i = 0; i < demi-longueur; i++) {
p[i] = p[n - 1 - i] = moitié[i];
}
si (n % 2 == 1) { // chiffre médian
int milieu = demi-longueur - 1;
p[demi-longueur - 1] = milieu;
}
retour p;
}
}
«» "

> **Explication des éléments clés**
> * `permCount` / `permCountZero` utilisent des facteurs précalculés.
> * `visited` stocke une représentation en chaîne du tableau de fréquence pour dédoubler.
> * Back-tracking `generate` construit toutes les moitiés possibles du palindrome, en les miroir pour obtenir le nombre complet.

---

- Oui. 2. Python

'`python
importer des maths
Importations provenant des collections Compteur

def countGoodIntegers(n: int, k: int) -> Int:
fait = [1] * 11
pour i à portée(1, 11):
fait[i] = fait[i - 1] * i

def total_perm(freq, tot):
res = fait[tot]
pour f dans les valeurs freq.():
Res //= fait[f]
retour res

def zero_perm(freq, tot):
si freq.get(0, 0) == 0:
retour 0
[0] -= 1
res = fait[tot - 1]
pour f dans les valeurs freq.():
Res //= fait[f]
freq[0] += 1
retour res

visité = set()
ans = 0

mi_len = (n + 1) // 2

def backtrack(pos, half):
non locaux
si c'est le cas. _mi-len :
Construire le palindrome
chiffres = moitié + moitié[:-1] si n % 2 == 0 autre moitié + moitié[-2::-1]
valeur = int('.join(carte(str, chiffres)))
si valeur % k == 0:
freq = Contre(chiffres)
key = tuple(sorted(freq.items())) Découpe
si la clé n'est pas visitée:
visité.add(clé)
freq_arr = [freq.get(i, 0) pour i dans l'intervalle(10)]
total = total_perm(freq_arr, n)
0 = zéro_perm(freq_arr, n)
ans += total - zéro
retour

début = 1 si pos == 0 autre 0
pour d dans la plage (démarrage, 10):
moitié[pos] = d
retour (pos + 1, moitié)

backtrack(0, [0] * half_len)
retour et
«» "

---

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
Constexpr statique long long FACT[11] = {
1,12,6,24,120,720,5040,40320,3628,828800
};

long total long Perm(tableau Const<int,10>& freq, int tot) {
long res = FACT[tot];
pour (int f : freq) res /= FACT[f];
retour rés;
}

long long zéroPerm(array<int,10> freq, int t) {
si (freq[0]] 0) retour 0;
freq[0]--; // réserve en tête zéro
longue rés = FACT[tot-1];
pour (int f : freq) res /= FACT[f];
freq[0]++; // restauration
retour rés;
}

public:
long compte long Bons entiers(int n, int k) {
long an = 0;
unordered_set<string> vu; // chaîne de fréquence pour dedupe

vecteur<int> moitié(n + 1)/2);
fonction<vit(int)> dfs = [&](int pos) {
si [pos] (int)demi.taille() {
vecteur<int> chiffres(n);
pour (int i=0;i<demi.size();++i) {
chiffres[i] = moitié[i];
chiffres[n-1-i] = moitié[i];
}
long vall=0;
pour (int d:digits) val=val*10+d;
si (val%k==0) {
tableau <int,10> freq{}; freq.fill(0);
pour (int d:digits) freq[d]++;
clé de chaîne;
pour (int i=0;i<10;i++) key+=to_string(freq[i])+'#';
si (see.insert(key).second) {
ans += totalPerm(freq,n) - zéroPerm(freq,n);
}
}
retour;
}
pour (int d=(pos==0?1:0); d<=9; ++d) {
moitié [pos]=d;
dfs(pos+1);
}
};

dfs(0);
le retour des an;
}
};
«» "

> **Conseil** – Les trois solutions partagent la même idée de base. Vous pouvez copier-coller les fonctions d'aide combinatoire entre les langues avec des changements minimes.

---

Analyse de complexité

Métrique
- C'est quoi ?
**Heure** – au plus 10 000 itérations
**Espace** (à l'exception de l'ensemble visité qui détient au plus 10 cartes à chiffres distincts) Autres

La pré-computation factorielle est négligeable (« O(10) »).

---

Article de blog optimisé par le SEO

Voici un article prêt à publier qui utilise les mots-clés que vous avez demandés. N'hésitez pas à le copier dans votre blog personnel, Medium, Dev.to ou un article LinkedIn pour améliorer votre visibilité en ligne.

---

♪ Trouvez le compte de bons entiers – LeetCode 3272 (Java, Python, C++)

**Mots clés:** *LeetCode 3272, trouver le nombre de bons entiers, k‐palindromic, algorithme d'entretien, solution Java, solution Python, solution C++, entretien de codage, entretien d'embauche, entretien de développement logiciel, entretien de direction, entretien de direction, conception d'algorithme, code prêt à l'emploi, défi de codage, résolution de problèmes algorithmique. *

---

Présentation

Si vous vous préparez à une entrevue d'ingénierie logicielle, vous vous retrouverez bientôt à regarder des problèmes qui combinent **back-tracking** et **combinatorics**. LeetCode 3272 – Trouver le comte des bons entiers – est un tel défi. Il vous demande :

- Générer tous les palindromes `n` à chiffres (n ≤ 10).
- Filtrer ceux qui sont divisibles par un petit entier `k` (1 ≤ k ≤ 9).
- Compter combien de permutations uniques de chaque palindrome de qualification les chiffres créent un nombre `n`-numérique valide (pas de zéro de tête).

Alors que les contraintes semblent minuscules, la solution est une grande démonstration de:

- Recherche en profondeur (DFS) sur la moitié des chiffres.
- Pré-computation des facteurs pour les permutations exactes.
- Dédoublement à l'aide d'une carte de fréquence.
- Manipulation de cas pour les zéros de tête.

**Pourquoi est-ce une nécessité pour les recruteurs? * *
Les intervieweurs aiment les problèmes qui testent *exact* compte plutôt que les approximations. Il montre que vous pouvez penser à la combinatoire, à la mémorisation et à la manipulation de chaînes de caractères – toutes les compétences qui se traduisent directement en code de production.

---

## 2-Écrit

> **Input**:
> `int n` – le nombre de chiffres (1 ≤ n ≤ 10).
> `int k` – le diviseur (1 ≤ k ≤ 9).
>
> **Résultat**:
> `long` – le nombre de bons nombres entiers `n`.

Un nombre **k-palindromic** est un palindrome divisible par `k`.
Un **bon entier** est un nombre `n` à chiffres qui peut être permuté (sans ramener de zéros) dans un entier k palindromique.

> **Exemples**
> ```texte
> n = 3, k = 1 → 27 (Tous les nombres à 3 chiffres sont bons parce que chaque nombre peut être réaménagé dans un palindrome divisible par 1)
> n = 3, k = 3 → 4 (seulement les nombres à 3 chiffres comme 121, 232, 343, 454 sont bons)
> `` "

---

- Oui. Brute- Stratégie de la force

Comme `n` est au plus 10, le nombre de palindromes possibles est au plus `10^(ceil(n/2)'.
Même pour `n = 10`, ce n'est que 10 000 palindromes – parfaitement traitables.

1. ** Générer tous les palindromes `n` en choisissant récursivement les premiers chiffres `ceil(n/2)`.
2. **Mirreur** la moitié choisie pour créer le palindrome complet.
3. ** Vérifier la disvisibilité**: `pal % k == 0`.
4. **Comparer les permutations** des chiffres du palindrome de qualification qui ne sont pas **** ont un zéro de tête.

---

Nombre de permutations valides

Les lettres indiquent la fréquence de chaque chiffre dans un palindrome comme étant `freq[0...9]`.
Le nombre total de permutations distinctes des chiffres `n` est:

> `` "
> n! / (freq[0]! * freq[1]! * ... * freq[9]!)
> `` "

Nous précalculons les facteurs jusqu'à 10! une fois et les réutiliser.

**Mais nous devons exclure les permutations qui commencent par zéro. **
Si le palindrome contient au moins un zéro, nous:

- Réduire le nombre de zéros de 1.
- Calculer les permutations des chiffres `n-1` restants.
- Restaurer le nombre zéro après.

Le nombre de permutations de type "bad" (qui mène à zéro) est:

> `` "
> (n-1)! / (freq[0]-1)! * (freq[1]! * ... * freq[9]!)
> `` "

La soustraction du mauvais compte du total donne le nombre de permutations *valides* pour ce palindrome.

---

# # # 4-

Plusieurs palindromes peuvent partager les mêmes fréquences numériques.
Par exemple, `121` et `212` ont le même `freq = {1:2, 2:1}`.
Nous n'avons besoin de compter chaque configuration de fréquence distincte qu'une seule fois.

Nous stockons une représentation en chaîne du tableau de fréquences dans un `set`/`unordered_set` et ignorons les duplications.

---

Mise en œuvre complète

#### 5.1 Java

"Java
solution de classe {
longueur finale statique[] FACT = {1,1,2,6,24,120,720,5040,40320,362880,3628800};

total privé longPerm(int[] freq, int n) {
long res = FACT[n];
pour (int f : freq) res /= FACT[f];
retour rés;
}

privé long zéroPerm(int[] freq, int n) {
si (freq[0]] 0) retour 0;
[0] --;
long res = FACT[n-1];
pour (int f : freq) res /= FACT[f];
freq[0]++;
retour rés;
}

compte public longGoodIntegers(int n, int k) {
Set<String> vu = nouveau HashSet<>();
long ans = 0;
la moitié int = (n+1)/2;

int[] halfDigits = nouvelle int[ half];
backtrack(0, halfDigits, n, k, vu, ansRef -> {
ans += ansRef;
});

le retour des an;
}

vide privé retour(int pos, int[] moitié, int n, int k, Set<String> vu, consommateur<Long> consommateur) {
si (pos=mi-longueur) {
// Construire un palindrome complet
int[] chiffres = nouvelle int[n];
pour (int i=0;i<mi-longueur;i++) {
chiffres[i] = chiffres[n-1-i] = moitié[i];
}
longue valeur = 0;
pour (int d:digits) val = val*10 + d;
si (val % k) 0) {
int[] freq = nouvelle int[10];
pour (int d:digits) freq[d]++;
Clé de chaîne = Arrays.toString(freq);
si (voir.add(clé)) {
consommation.accept(total Perm(freq, n) - zéroPerm(freq, n));
}
}
retour;
}
pour (int d=(pos==0?1:0); d<=9; ++d) {
demi[pos] = d;
backtrack(pos+1, moitié, n, k, vu, consommateur);
}
}
}
«» "

> *Le code ci-dessus utilise `Consommer<Long>` pour accumuler la réponse, mais vous pouvez facilement la remplacer par un simple champ de classe. *

5.2 Python

'`python
importer des maths
Importations provenant des collections Compteur

def countGoodIntegers(n: int, k: int) -> Int:
fait = [1]*11
pour i dans l'intervalle(1,11): fait[i] = fait[i-1]*i

def total_perm(freq, n):
res = fait[n]
pour v dans freq.values(): res //= fact[v]
retour res

def zero_perm(freq, n):
si freq.get(0,0)==0: retourner 0
[0]-=1
res = fait[n-1]
pour v dans freq.values(): res //= fact[v]
freq[0]+=1
retour res

moitié = (n+1)//2
visité = set()
ans=0

def backtrack(pos, half):
non locaux
Si pos==moitié:
nombres = moitié + moitié[:-1] si n%2==0 autre moitié + moitié[-2:-1]
val = int('.join(map(str,digits)))
si val%k==0 & #160;:
freq = Contre(chiffres)
key = tuple(sorted(freq.items()))
si la clé n'est pas visitée:
visité.add(clé)
as += total_perm(freq, n) - zéro_perm(freq, n)
retour

pour d dans la plage(1 si pos==0 autre 0, 10):
retour(pos+1, demi+[d])

retour(0, [])
retour et
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
Constexpr statique long long FACT[11] = {1,1,2,6,24,120,720,5040,40320,362880,3628800};

long total long Perm(tableau Const<int,10>& freq, int n){
long res = FACT[n];
pour (int f : freq) res /= FACT[f];
retour rés;
}

long long zéroPerm(array<int,10> freq, int n){
si (freq[0]==0) retourner 0;
freq[0]--; // réserve en tête zéro
long res = FACT[n-1];
pour (int f : freq) res /= FACT[f];
freq[0]++;
retour rés;
}

public:
long compte long Bons entiers(int n, int k){
unordered_set<string> vu;
long an = 0;
vecteur<int> moitié(n+1)/2);

fonction<vit(int)> dfs=[&](int pos){
si (pos==demi.size()) {
vecteur<int> chiffres(n);
pour(int i=0;i<demi.size();++i) {
chiffres[i]=chiffres[n-1-i]=moitié[i];
}
long vall=0;
pour(int d:digits) val=val*10+d;
if(val%k==0){
tableau <int,10> freq{}; freq.fill(0);
pour(int d:chiffres) freq[d]++;
clé de chaîne;
pour(int i=0;i<10;i++) key+=to_string(freq[i])+'#';
si(seen.insert(key).second) {
ans += totalPerm(freq,n) - zéroPerm(freq,n);
}
}
retour;
}
pour(int d=(pos==0?1:0);d<=9;++d){
moitié [pos]=d;
dfs(pos+1);
}
};

dfs(0);
le retour des an;
}
};
«» "

---

- Oui. Pourquoi la solution compte

Ce que les intervieweurs attendent Comment ce problème produit
C'est ce qu'on a dit.
**Comptabilité exacte** Utiliser la pré-computation factorielle pour calculer les permutations exactement. Autres
**DFS sur la moitié** Retraçant les chiffres `(n+1)/2`. Autres
**Dédoublement**Éviter le surcompte. Enregistre la chaîne de fréquence dans un ensemble. Autres
**Cas d'escroquerie** L'aide à la permutation zéro garantit qu'aucun zéro n'est en tête. Autres

Ces modèles sont **production-grade**: vous pré-calculez des choses lourdes une fois, utilisez des boucles itératives, et gardez contre les cas de bord.

---

C'est pas vrai. A emporter pour l'entrevue

1. **Afficher votre capacité à concevoir un DFS propre** qui fonctionne sur *la moitié* des chiffres.
2. ** Expliquez pourquoi la pré-computation factorielle est importante** pour le comptage exact – elle élimine les erreurs d'arrondi.
3. **Mention l'étape de duplication** – c'est une optimisation subtile mais cruciale.
4. ** Démontrer la manipulation des zéros de tête** – une source de bug classique.

Si vous présentez cette solution dans une entrevue, vous démontrerez à la fois *perspective algorithmique* et *mise en oeuvre propre*, exactement ce que les postes de direction ou de chef de file technologique exigent.

---

C'est pas vrai. Mot final

LeetCode 3272 est une miniclasse** en comptage combinatoire.
Que vous le résolviez en Java, Python ou C++, la logique reste identique.
Votre code *propre, bien documenté* vous permettra non seulement de gagner des points d'entrevue, mais aussi d'impressionner les recruteurs qui lisent vos billets de blog.

> **Prochaines étapes**
> 1. Pratiquez le problème sur LeetCode et enregistrez l'exécution pour chaque langue.
> 2. Écrire la solution dans au moins deux langues pour renforcer la fluidité des langues.
> 3. Publiez votre solution (comme cet article) et demandez aux pairs de faire des commentaires.

Bon codage ! C'est ce qu'il a dit