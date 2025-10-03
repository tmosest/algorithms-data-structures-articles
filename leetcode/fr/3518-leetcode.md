---
Titre: LeetCode 3518. La plus petite réorganisation palindromique II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
N° 3518. La plus petite réorganisation palindromique II
### Un facile à lire Java / Python / Solution C++ + un billet de blog prêt à travailler

---

### TL;DR

* ** Objectif :** Retourner le *k*-th palindrome lexicographiquement le plus petit qui peut être formé en permutant une chaîne palindromique donnée *s*.
* **Constraint:**
* < 1 ≤ α ≤ 104 > >
* `1 ≤ k ≤ 106`
* `s` ne contient que des lettres anglaises minuscules et est garanti être un palindrome.
* **Idée de base :**
* Un palindrome est entièrement déterminé par sa première moitié* (et peut-être un personnage du milieu).
* Compter le nombre de permutations possibles pour chaque préfixe de la première moitié en utilisant un coefficient multiple*.
* Choisissez avec plaisir la plus petite lettre qui conserve le nombre de permutations restantes ≥ k.

Les sections suivantes passent par l'intuition, l'algorithme, la complexité et l'implémentation dans **Java, Python et C++**.
Après le code, nous incluons un article de blog SEO poli et convivial que vous pouvez copier-coller dans votre portfolio ou LinkedIn pour présenter votre pensée prête à l'entrevue.

---

- Oui. 1. Récapitulation des problèmes (en anglais clair)

> Vous êtes donné une corde qui est déjà un palindrome.
> Réorganiser ses lettres (toute permutation) aussi longtemps que le résultat reste un palindrome.
> Parmi toutes les permutations palindromiques distinctes, affichez le **k‐th** dans l'ordre lexicographique.
> S'il y a moins de permutations *k*, affichez une chaîne vide.

> **Exemples**
> * `"abba"`, k = 2 → `"baab"`
> * `"aa"`, k = 2 → `""` (uniquement `"aa"` existe)
> * `"bacab"`, k = 1 → `"abcba"` (en premier dans l'ordre)

---

- Oui. 2. Intuition: La moitié du Palindrome est tout ce dont nous avons besoin

Un palindrome lit les mêmes avant et arrière.
Si nous connaissons les caractères qui occupent les **premières positions `=n/2=='**, toute la chaîne est corrigée:

«» "
premier Demi + (charnier intermédiaire, le cas échéant) + inverse(première moitié)
«» "

Ainsi le *problème* se réduit à:

1. **Trouvez le personnage du milieu** (il y en a au plus un, car la chaîne d'entrée est un palindrome).
2. **Construire la première moitié** de la longueur « halfLen = n / 2 ».
3. Le *k*-th palindrome n'est que la première moitié que nous construisons, suivi par l'omble moyen (le cas échéant) et son inverse.

Le défi est de *comment construire efficacement la première moitié* tout en sachant combien de permutations sont encore possibles après chaque choix provisoire.

---

- Oui. 2. Compter les permutations restantes – Coefficient multinomial

Si la fréquence d'un caractère *c* dans la première moitié est `cnt[c]`, alors le nombre de façons distinctes d'organiser le reste multiset de lettres est

«» "
multinôme(cnt) = (cnt[0] + ... + cnt[25])
«» "

Parce que les valeurs factorielles croissent extrêmement vite, nous ** n'avons jamais besoin de calculer le nombre exact** – nous avons seulement besoin de savoir si c'est **≥ k** ou **< k**.
Donc nous plafonnons le résultat à `MAX = 1_000_001` (un de plus que le plus grand "k" possible) et avorter le calcul dès que nous franchissons ce seuil.

Le coefficient binôme `C(n, k)` est utilisé en interne:

«» "
C(n, k) = n! / (k! · (n-k)!)
«» "

Tant `multinomial()` que `binom()` sont implémentés avec *début-termination* pour garder l'exécution minuscule.

---

- Oui. 3. Construction de la première moitié

Pour chaque position `pos` dans la première moitié (de gauche à droite):

«» "
pour chaque caractère c en 'a'..'z' (par ordre croissant):
Si cnt[c] == 0: continuer

Essaie de mettre c à cette position
Cnt[c]...
restant = multinôme(cnt) Nombre de permutations pour le suffixe

si restant >= k: # nous pouvons garder c ici
annexe c au résultat
Break # aller à la position suivante
Sinon:
k -= restant # sauter toutes les permutations commençant par c
cnt[c]++ # restaurer le nombre
«» "

Parce que la chaîne est un palindrome, **chaque** permutation valide de la première moitié correspond à un palindrome entier unique – il n'y a pas de duplication entre les deux moitiés.

---

- Oui. 4. Analyse de la complexité

Étape Temps Raison
C'est pas vrai.
Nombre de fréquences
Trouver le char du milieu `O(26)`.
Calculer le premier semestre `O(demi-Len · 26 · B) ́ ́ ́ ́ Pour chacune des positions `demi-Len ≤ 5 000`, nous essayons au plus 26 lettres. `B` est le nombre de multiplications à l'intérieur de `binom()`, qui est limité par ~20 parce que la valeur explose `1 000 001` passé après une poignée de multiplications. Autres
Unité finale Chaîne et concaténation inversées
**Total******«O(n · 26 · 26 · 20» → Pratiquement `O(n)`**= Les facteurs constants sont minuscules. Autres

L'utilisation de la mémoire est `O(26)` (tableaux de fréquences) + `O(n)` pour la chaîne de sortie – bien en dessous des limites.

---

- Oui. 5. Mise en œuvre – Trois langues

> **Note :**
> Toutes les implémentations gardent la valeur combinatoire *cappée* à `MAX = 1_000_001`.
> `k` est basé sur **1** – le premier palindrome est à `k = 1`.

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
MAX_K = 1_000_001L;

chaîne publique plus petitePalindrome(String s, int k) {
int[] freq = nouveau int[26];
pour (char ch : s.toCharArray()) freq[ch - 'a']++;

// Char moyen (le cas échéant)
mid = 0;
pour (int i = 0; i < 26; i++) {
si ((freq[i] & 1)) 1) { // nombre impair
milieu = (char) ('a' + i);
freq[i]-; // supprimer le milieu
pause;
}
}

// demi fréquences
int[] moitié = nouvelle int[26];
idemLen = 0;
pour (int i = 0; i < 26; i++) {
moitié[i] = freq[i] / 2;
moitiéLen += moitié[i];
}

long total = multinôme(moitié);
si (k > total) retourner "; // pas assez de permutations

StringBuilder d'abord = nouveau StringBuilder();
pour (int pos = 0; pos < halfLen; pos++) {
pour (int c = 0; c < 26; c++) {
si (demi-[c]]] 0) poursuivre;
demi[c]--; // Utilisation provisoire c
longues voies = multinôme(moitié);
si (ways >= k) { // garder c
premier appendice(char) («a» + c);
pause;
} autre { // sauter toutes ces permutations
k -= voies;
demi[c]++; // restaurer
}
}
}

String rev = nouveau StringBuilder(first).reverse().toString();
retour au milieu de == 0 ? premier + rev : premier + milieu + rev;
}

multinôme(int[] cnt) privé long {
la valeur de l'élément est égale à 0;
pour (int c : cnt) t += c;
longue rés = 1;
pour (int i = 0; i < 26; i++) {
c = cnt[i];
si (c) 0) poursuivre;
res = res * binom(tot, c);
si (res >= MAX_K) retourne MAX_K;
-= c;
}
retour rés;
}

binom(int n, int k) {
si (k > n) retourne 0;
si (k > n - k) k = n - k;
longue r = 1;
pour (int i = 1; i <= k; i++) {
r = r * (n - i + 1) / i;
si (r >= MAX_K) retourne MAX_K;
}
retour r;
}
}
«» "

---

5.2 Python

'`python
de taper l'importation Liste

MAX_K = 1_000_001

Solution de classe:
def le plus petit Palindrome (self, s: str, k: int) -> str:
freq = [0] * 26
pour ch en s:
freq[ord(ch) - 97] += 1

# Char moyen (le cas échéant)
moyenne = ' '
pour i dans la fourchette(26):
si freq[i] & 1:
milieu = chr(97 + i)
[i] 1
pause

moitié = [f // 2 pour f en freq]
moitié_len = somme(moitié)

total = auto-multinôme(moitié)
si k > total:
retour '

premier = []
pour _ dans l'intervalle(demi_len):
pour c dans la plage(26):
si la moitié[c]] 0:
poursuivre
moitié[c] -= 1
Voies = auto.multinôme(moitié)
si ways >= k:
Première annexe(chr(97 + c))
pause
k -= voies
moitié[c] += 1

première moitié = ''.join(premier)
retourner la première moitié + le milieu + la première moitié[:-1]

def multinôme(self, cnt: List[int]) -> Int:
tot = somme (cnt)
Res = 1
pour c en cnt:
Res *= self.binom(tot, c)
si res >= MAX_K :
retour MAX_K
-= c
retour res

def binom(self, n: int, k: int) -> Int:
si k > n:
retour 0
si k > n - k:
k = n - k
r = 1
pour i dans la plage (1, k + 1):
r = r * (n - i + 1) // Les
si r >= MAX_K :
retour MAX_K
retour r
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
MAX_K = 1000001L;

public:
chaîne la plus petite Palindrome(chaîne s, int k) {
tableau <int,26> freq{};
pour(char ch: s) freq[ch-'a']++;

// Char moyen
mid = 0;
Pour(int i=0;i<26;i++){
Si(freq[i]&1){
milieu = char('a'+i);
[i] --;
pause;
}
}

tableau <int,26> moitié {};
idemLen = 0;
Pour(int i=0;i<26;i++){
moitié[i] = freq[i]/2;
moitiéLen += moitié[i];
}

long total = multinôme(moitié);
if(k > total) retourne ";

chaîne d'abord;
pour(int pos=0; pos<demiLen; ++pos){
Pour(int c=0;c<26;c++){
si(demi-[c]==0) continuer;
demi[c]--; // essayer c
longues voies = multinôme(moitié);
if(ways >= k) {
premier.push_back(char('a'+c));
pause;
}else {
k -= voies;
moitié[c]++; // annuler
}
}
}

chaîne rev = première;
inverse(rev.begin(), rev.end());
if(mid==0) retourner en premier + rev;
sinon retourner d'abord + mi + rev;
}

particulier:
long multinomial(const array<int,26> &cnt) const {
long tot = 0;
pour(int c: cnt) t += c;
longue rés = 1;
pour(int c: cnt){
ic==0) continuer;
res *= binom(tot, c);
if(res >= MAX_K) retourne MAX_K;
-= c;
}
retour rés;
}

long binom(long n, long k) const {
si(k>n) retourne 0;
si(k>n-k) k=n-k;
longue r=1;
pour(long i=1;i<=k;i++){
r = r * (n-i+1) / i;
if(r>=MAX_K) retourne MAX_K;
}
retour r;
}
};
«» "

---

- Oui. 6. Comment utiliser ces solutions

- **LeetCode / Interview**: copiez la classe `Solution` / méthodes dans l'éditeur de plate-forme.
- **Essais locaux**:

'`python
sol = Solution()
print(sol.smallestPalindrome("abcba", 1)) #abcba
print(sol.smallestPalindrome("abcba", 3)) # bcbab
«» "

---

- Oui. 7. Résumé – Pourquoi cela compte pour votre récit

* **Prise solide des combinatoires** – expliquant les facteurs, le binôme, le multinôme, et comment les appliquer dans la conception d'algorithmes.
* **La terminaison précoce efficace** – une astuce d'entrevue commune pour les calculs en entier.
* **La construction progressive avec la connaissance de l'état futur** – démontre une compréhension profonde de choisir la prochaine étape droite des problèmes.
* **Clean, code idiomatique en trois langues** – montre la polyvalence en tant qu'ingénieur logiciel.

Inclure ce problème dans votre portfolio ou comme un point de discussion dans les interviews techniques pour impressionner les gestionnaires d'embauche: Je peux construire un palindrome dans le temps linéaire en utilisant combinatoire, même sous des contraintes serrées. (en milliers de dollars)

Bon codage – et que votre prochain entretien d'emploi accepte votre premier palindrome avec `k = 1`!