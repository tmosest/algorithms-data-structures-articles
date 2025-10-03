---
titre: LeetCode 2868. Le jeu de mots -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque geste, nous avons un mot qui a déjà été prononcé.
Le prochain joueur peut parler seulement

* un mot qui est **lexicographiquement plus grand** que le dernier mot et
* un mot qui commence avec la même première lettre** ou avec la suivante**
lettre dans l'alphabet.

Si le joueur qui doit parler ensuite n'a pas un tel mot, il perd immédiatement.

La tâche est de décider si Alice (le propriétaire du tableau `a`) peut gagner
quand elle parle le premier mot `a[0]`.

-----------------------------------------------------------------------------------

C'est vrai. 1. Observations

* Les deux tableaux `a` et `b` sont déjà triés.
* Tout le jeu ne dépend que de l'ordre relatif des mots,
Pas sur quel tableau ils appartiennent.
* Pour un dernier mot donné, il suffit de regarder des mots qui sont ** strictement
plus grande**.
Si nous traitons les mots dans **ordre lexicographique inverse** tous
les candidats au prochain déménagement sont déjà évalués – parfait pour
programmation dynamique.

-----------------------------------------------------------------------------------

C'est vrai. 2. État mondial

«» "
propriétaire : 0 → Alice, 1 → Bob
idx : index du mot dans son tableau propriétaire
dp[o][i] : vrai → le propriétaire `o` vient de parler ` Les "
et l'autre joueur finira par perdre
(le propriétaire peut gagner tout le jeu)
false → le propriétaire perdra
«» "

Le jeu se termine lorsque le joueur qui doit parler ensuite ne peut pas trouver un
mot valide – c'est exactement la situation décrite par la définition
de "dp".

-----------------------------------------------------------------------------------

C'est vrai. 3. Structures des données

Objectif
- Oui.
Autres Tous les mots ont été triés ensemble. Autres
Recherche binaire sur le propriétaire
Mots de cartographie → index (Java `HashMap`, Python `dict`) Autres

Le nombre total de mots est au plus `2·105`, donc toutes les structures facilement
S'intégrer dans la mémoire.

-----------------------------------------------------------------------------------

C'est vrai. 4. Répétition du PDD

Pour un mot "w" prononcé par le propriétaire "o" :

«» "
op = 1 - o // opposant

candidats = mots du propriétaire
• commencer par w[0] ou
• commencer par nextLetter(w[0])
• sont lexicographiquesment plus grandes que w
«» "

*S'il y a **non** candidat*, l'adversaire ne peut pas bouger →
«dp[o][idx] = true».

*S'il y a au moins un candidat*, le propriétaire gagne
iff **some** candidat conduit à la perte de l'adversaire:

«» "
dp[o][idx] = true // supposons d'abord que nous pouvons gagner
pour chaque candidat suivant Idx :
si dp[op][nextIdx] faux: // l'adversaire perdra
break // le propriétaire gagne
Autre
dp[o][idx] = faux // tous les candidats mènent à la victoire de l'adversaire
«» "

Parce qu'on rit sur les mots en **descendant** lexicographique
ordre, `dp[op][nextIdx]` est déjà connu.

-----------------------------------------------------------------------------------

C'est vrai. 5. Algorithme

«» "
1. Lire a[ ], b[ ] // déjà triés
2. Construire une liste globale ALL = { (mot, propriétaire, indexInOwnerArray) } pour
chaque mot de a et b. Tri tous lexicographiquement.
3. Créer dp[2][len(a)] et dp[2][len(b)] // initialement tous faux
4. pour chaque entrée de TOUS de la dernière à la première:
propriétaire = propriétaire d'entrée
idx = entrée.idx
dernier Mot = entrée.
Adversaire = 1 - propriétaire
trouvéCandidate = faux
win = true // gagnera si l'adversaire n'a pas de mouvement

pour la lettre dans [lastWord[0], nextLetter(lastWord[0]):
// recherche binaire dans le tableau adversaire pour le premier mot > dernier Mots
suivant Idx = premier indice dans l'adversaire Arrayez où
mot > dernier Le mot et le mot commencent par la lettre
si suivant Idx existe:
trouvéCandidate = true
si dp[opposant][nextIdx] faux:
win = true // adversaire perdra
pause
Autre
gagnant = faux // adversaire gagnera
s'il n'est pas trouvé Candidat :
win = vrai
dp[propriétaire][idx] = gain

5. La réponse est dp[0][0] // après qu'Alice parle a[0], c'est Bob.
«» "

-----------------------------------------------------------------------------------

C'est vrai. 6. Preuve d'exactitude

Nous prouvons que l'algorithme retourne **true** si Alice peut forcer une victoire.

---

Lemma 1
Pour tout mot `w` parlé par son propriétaire `o`, après l'algorithme traité
Nous avons

«» "
dp[o][idx] = true = à partir de l'état
(dernier mot = w, à côté de jouer = 1-o)
le propriétaire `o` peut forcer une victoire.
«» "

**Prof.**

Nous traitons les mots dans un ordre lexicographique décroissant.
Par conséquent, quand `w` est traité tous les mots lexicographiquement plus grand
(et donc tous les candidats au prochain déménagement) ont déjà leur
Valeurs «dp» calculées.

*Si l'opposant n'a pas de candidat*:
«dp[o][idx]» reste "vrai".
L'adversaire ne peut pas bouger, donc `o` gagne immédiatement – la déclaration tient.

*Si l'adversaire a au moins un candidat*:
«dp[o][idx]» est défini à "true" seulement s'il existe un candidat `c`
tel que "dp[1-o][c] == false".
`dp[1-o][c] == false` signifie le propriétaire de `c` (l'opposant)
finira par perdre, donc 'o' gagne – la déclaration tient.

*Si tous les candidats mènent à une victoire pour l'adversaire*:
«dp[o][idx]» devient «faux».
Dans ce cas `o` perd – la déclaration tient.

*



Lemma 2
Après Alice joue le premier mot `a[0]` le jeu est gagné par Alice
iff `dp[0][0]` est `true`.

**Prof.**

L'état après Alice est *exactement* l'état utilisé dans le
définition de «dp[0][0]»:

* La dernière parole est `a[0]` (propriété d'Alice, indice '0').
* À côté de jouer Bob.

Par conséquent, par Lemma 1, «dp[0][0]» dit si Alice peut forcer un
gagner de cette position.

*



C'est vrai. Théorème
L'algorithme sort **true** iff Alice peut gagner le jeu.

**Prof.**

Par Lemma 2 l'algorithme produit `dp[0][0]`.
Par Lemma 1 cette valeur est exacte quand Alice peut forcer une victoire.
L'algorithme est donc correct.

*



-----------------------------------------------------------------------------------

C'est vrai. 7. Analyse de la complexité

Laissez

«» "
n = longueur (1 ≤ n ≤ 105)
m = longueur b (1 ≤ m ≤ 105)
«» "

*Trier la liste globale*: `O(n+m) log(n+m) "
*Processus de chaque mot*: deux recherches binaires → `O(log n)` ou `O(log m)`
*Total*: "O(n+m) log (n+m)" temps, "O(n+m)" mémoire.

-----------------------------------------------------------------------------------

C'est vrai. 7. Mise en œuvre des références

Java 17

"Java
importation java.io.*;
Importation de java.util.*;

classe publique {

- Oui. Structure des données pour un mot global ---------- */
classe statique privée WordEntry {
La chaîne de mots;
propriétaire de l'infrastructure; // 0 – Alice, 1 – Bob
int idx; // index dans son tableau propriétaire

WordEntry(String w, int o, int i) {
mot = w;
propriétaire = o;
idx = i;
}
}

/* --------------- aide : prochaine lettre alphabétique --------- */
char statique privé suivantLettre(char c) {
retour (char) (c + 1); // 'a' -> 'b', ..., 'z' -> '{ '
}

Recherche binaire : premier mot > clé et commençant par la lettre --------- */
Int statique privé premierGreaterWithPrefix(Liste<String> arr, Clé de chaîne, préfixe de char) {
int lo = 0, hi = arr.size();
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
Chaîne cur = arr.get(mid);
si (cur.compareTo(key) <= 0) {
lo = milieu + 1;
} autre {
hi = milieu;
}
}
// lo est le premier index avec arr[lo] > clé
si (lo < arr.size() && arr.get(lo).charAt(0) == préfixe) {
retour lo;
}
retour -1;
}

/* --------- principal --------- */
public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));

Chaîne[] a = br.readLine().trim().split("\\s+");
Chaîne[] b = br.readLine().trim().split("\\s+");

int n = longueur;
int m = longueur b;

// Liste globale
Liste<WordEntry> tous = nouvelle liste de distribution<>(n + m);
pour (int i = 0; i < n; ++i) all.add(new WordEntry(a[i], 0, i));
pour (int i = 0; i < m; ++i) all.add(new WordEntry(b[i], 1, i));

tous.sort(Comparator.comparing(e -> e.word));

// tableaux dp
booléen[], dp = nouveau booléen[2],
dp[0] = nouveau booléen[n];
dp[1] = nouveau booléen[m];

// Processus en ordre inverse
pour (int pos = all.size() - 1; pos >= 0; --pos) {
WordEntry e = all.get(pos);
Int propriétaire = e. propriétaire;
int idx = e.idx;
Chaîne dernière = e.word;
char first = last.charAt(0);
char nextLettre(premier);

Booléen trouvé Candidat = faux;
boolean win = true; // par défaut: nous gagnons si l'adversaire ne peut pas bouger

int op = 1 - propriétaire;
Liste <String> oppArray = (op) 0) ? Arrays.asList(a) : Arrays.asList(b);

// Essayez les deux premières lettres possibles
pour (lettre char : nouveau char[]{premier, suivant}) {
int suivant Idx = premierGreatWithPrefix(oppArray, dernier, lettre);
si (suivantIdx != -1) {
foundCandidate = true;
si (!dp[op][nextIdx]) { // l'adversaire perd
win = vrai;
pause;
} sinon { // l'adversaire gagnera
gain = faux;
}
}
}
si (!foundCandidate) gagnant = vrai;
dp[propriétaire][idx] = gain;
}

Système.out.println(dp[0][0] ? "vrai" : "faux");
}
}
«» "

Python 3

'`python
importations
bisect d'importation

df résoudre(a, b):
n, m = len(a), len(b)

# liste globale de tous les mots
all_words = []
pour i, w dans l'énumérationa:
all_words.append((w, 0, i))
pour i, w dans l'énumération(b):
all_words.append((w, 1, i))
all_words.sort(key=lambda x: x[0]) # ordre lexicographique

dp_a = [Faux] * n
dp_b = [Faux] * m

# helper: premier index dans arr qui est > clé et commence par la lettre
def first_greater_with_prefix(arr, clé, lettre):
idx = bisect.bisect_right(arr, clé)
alors que idx < len(arr) et arr[idx][0] != Lettre:
idx += 1
retourner idx si idx < len(arr) sinon -1

pour mot, propriétaire, idx in inversed(all_words):
opp = 1 - propriétaire
trouvé = Faux
win = Vrai # gagnera si l'adversaire n'a pas de mouvement

pour la lettre en [mot[0], chr(ord(mot[0]) + 1):
si opp == 0:
arr = a
dp_opp = dp_a
Sinon:
arr = b
dp_opp = dp_b

# recherche binaire pour le premier mot > mot qui commence par 'lettre '
# arr est une liste de cordes
lo = bisect.bisect_right(arr, mot)
# s'assurer que les premiers caractères correspondent
alors que lo < len(arr) et arr[lo][0] != Lettre:
lo += 1

si lo < len(arr):
trouvé = Vrai
si pas dp_opp[lo]:
= Vrai
pause
Sinon:
gain = faux

s'il n'est pas trouvé:
= Vrai

si propriétaire == 0:
dp_a[idx] = gain
Sinon:
dp_b[idx] = gain

Après qu'Alice ait parlé, c'est le tour de Bob
retourner dp_a[0]


si __nom__ == "__main__" :
a = sys.stdin.readline().split()
b = sys.stdin.readline().split()
print("true" si solid(a, b) autre "faux")
«» "

-----------------------------------------------------------------------------------

C'est vrai. 7. Mise en œuvre des références – C++ (pour être complète)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct Entrée {
chaîne w;
Int propriétaire; // 0: Alice, 1: Bob
int idx; // index dans son propre tableau
};

Int main(){
ios::sync_with_stdio(faux);
cin.tie (nullptr);
ligne de chaîne;
// lire la ligne entière, divisée par espace blanc
vecteur<chaîne> a, b;
getline(cin, ligne);
chaîne de caractères ss(ligne);
tok à cordes;
pendant (ss >> tok) a.push_back(tok);
getline(cin, ligne);
chaîne de caractères ss2(ligne);
pendant (ss2 >> tok) b.push_back(tok);

int n = a.size(), m = b.size();

vecteur <Entrée> tous;
toutes les réserves (n+m);
pour(int i=0;i<n;i++) all.push_back({a[i],0,i});
pour(int i=0;i<m;i++) all.push_back({b[i],1,i});

Tri(all.begin(), all.end(), [](const Entrée et x, const Entrée et y){
retour x.w < y.w;
});

vecteur<vecteur<char>> dp(2);
dp[0].assign(n,0);
dp[1].assign(m,0);

auto firstGreater = [&](vecteur Const<string>& arr, chaîne Const& clé, lettre char) {
l=0,r=arr.size();
pendant que(l<r){
Int mi=(l+r)/2;
i(arr[mid] <= clé) l=mid+1;
autres r=mid;
}
if(l< arr.size() && arr[l][0]==lettre] retourner l;
retour -1;
};

pour(int pos=(int)all.size()-1;pos>=0;--pos){
Const auto &e = all[pos];
int owner=e.owner, idx=e.idx;
Const string &last=e.w;
propriétaire int opp=1;
bool win=true; // gagnera si l'adversaire n'a pas de mouvement
bool found=false;

lettres de char[2] = { last[0], (char)(last[0]+1) };

pour (lettre char: lettres) {
int suivant Idx;
if(opp=0){
nextIdx = premierGrand(a, dernier, lettre);
}else {
nextIdx = premierGrand(b, dernier, lettre);
}
if(nextIdx!=-1){
found=true;
if(opp=0){
if(!dp[0][nextIdx]){ win=true; break;}
autres gains = faux;
}else {
if(!dp[1][nextIdx]){ win=true; break;}
autres gains = faux;
}
}
}
if(!found) win=true;
if(owner==0) dp[0][idx]=win;
autres dp[1][idx]=win;
}
cout << (dp[0]]?"true":"faux") << '\n';
}
«» "

-----------------------------------------------------------------------------------

- Oui. 8. Conclusion

Le problème se réduit à vérifier si le dernier mot traité peut être battu par l'adversaire dans un jeu déterministe.
En explorant le jeu en arrière (à partir du mot lexicographiquement le plus grand) et en appliquant un DP simple avec des recherches binaires, nous pouvons déterminer le gagnant dans le temps `O(n+m) log(n+m)`.
Toutes les implémentations de référence ci-dessus adhèrent aux contraintes de problème et sont entièrement compatibles avec Java 17, Python 3 et (pour être complètes) C++17.