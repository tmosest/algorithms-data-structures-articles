---
titre: LeetCode 3625. Nombre de trapézoïdes II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour deux points différents `A(x1 , y1)` et `B(x2 , y2)` nous regardons le droit
segment «AB».
Tous les segments qui ont la même pente appartiennent au même **groupe de pente**.
À l'intérieur d'un groupe de pente, nous pouvons choisir deux segments – si les deux segments sont

* sur différentes lignes (non collinéaires)
* n'ont pas de critère d'évaluation commun

puis les quatre paramètres forment un trapèze
(le parallélogramme est un cas particulier de trapèze).

-----------------------------------------------------------------------------------

C'est vrai. 1. Représentation d ' une ligne

Pour un segment `AB`

«» "
dx = x2 – x1
dy = y2 – y1
«» "

`dx , dy` sont réduits de `g = gcd(-)dx,-)`
(les signaux sont normalisés de sorte que `dx > 0`, ou `dx==0` et le signe est en `dy`).

«» "
pente : (dy , dx) – Inf. pour une ligne verticale
intercepté : (num , den) – valeur de b en y = mx + b
(pour une ligne verticale : x = const)
«» "

Toutes les fractions sont maintenues sous forme entière réduite – aucun point flottant arithmétique n'est
utilisé.

Une clé pour une *line* est la concaténation de la clé de pente et de la clé d'interception.



-----------------------------------------------------------------------------------

C'est vrai. 2. Compter toutes les paires avec la même pente

Pour une clé de pente `s`

«» "
cntPente(s) – nombre de segments ayant cette pente
cntLine(s,l) – nombre de segments situés sur la même ligne l
«» "

Toutes les paires de segments avec pente `s` sont `C(cntSlope(s), 2)`.
Les paires situées sur la même ligne doivent être enlevées – elles ne peuvent pas construire un quadrilatère.

«» "
trapèzes_from_slope_s = C(cntSlope(s), 2) – lignes C (cntLine, 2)
«» "

La somme sur toutes les pentes donne le nombre de trapèzes * et *
parallélogrammes comptés **deux fois** (une fois pour chacun de leurs deux côtés parallèles)
des paires).

-----------------------------------------------------------------------------------

C'est vrai. 3. Comptage des parallélogrammes

Les diagonales d'un parallélogramme s'entrecoupent.
Par conséquent, deux segments avec le même point médian sont les diagonales d'un
parallélogramme.

Pour chaque paire de points, nous stockons la somme `(x1+x2 , y1+y2)` – c'est deux fois la somme
mi-point et peut être utilisé comme une clé.

«» "
cntMidpoint(m) – nombre de segments ayant ce point médian
Parallélogrammes = points C(cntMidpoint, 2)
«» "

Chaque parallélogramme est compté exactement une fois.



-----------------------------------------------------------------------------------

C'est vrai. 4. Formule finale

«» "
réponse =
C(cntSlope,2) – Lignes C(cntLine,2) ) // trapèzes + 2×parallélogrammes
– parallélogrammes // supprimer le double comptage
«» "

Toutes les valeurs intermédiaires correspondent à des entiers signés 64 bits
(C(124750, 2)

-----------------------------------------------------------------------------------

C'est vrai. 5. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le nombre de trapèzes **distincts**
peut être formé à partir des points donnés.

---

Lemma 1
Pour tous les segments `AB` et `CD`

* parallèle,
* pas collinéaire,
* ne partagent aucun paramètre,

le quadrilatère formé par les quatre points distincts est convexe et a exactement
une paire de côtés parallèles.

**Prof.**

Des segments parallèles et non collinéaires se trouvent sur deux lignes parallèles distinctes.
Les quatre paramètres sont distincts, donc les lignes se croisent uniquement à la
les points médians des segments, jamais à l'intérieur d'un segment.
Connecter les paramètres dans l'ordre `A – B – C – D` (ou tout déplacement cyclique)
produit un quadrilatère convexe dont les deux côtés opposés sont "AB" et "CD".



Lemma 2
Pour une pente fixe `s` la valeur

«» "
C(cntSlope(s), 2) – Lignes C(cntLine, 2)
«» "

égale le nombre de paires non ordonnées de segments disjoints, non collinéaires qui
ont la pente `s`.

**Prof.**

`C(cntSlope(s), 2)` compte toutes les paires non ordonnées de segments avec pente `s`,
y compris ceux sur la même ligne.
Pour chaque ligne `l` avec pente `s` la valeur `C(cntLine(l), 2)` compte les paires
sur cette ligne – exactement les cas invalides qui doivent être exclus.
La soustraction enlève toutes les paires collinéaires et laisse précisément les paires qui
satisfaire aux conditions de Lemma 1.



Lemma 3
La somme sur toutes les pentes de l'expression de Lemma 2
est égal au nombre de trapèzes **plus** au nombre de parallélogrammes
(comptés deux fois).

**Prof.**

Chaque trapèze a au moins une paire de côtés parallèles.
*S'il a exactement une paire de côtés parallèles*
les deux segments de cette paire appartiennent à un groupe de pente unique et sont comptés
Une fois dans la somme.

*Si c'est un parallélogramme*
il a deux paires distinctes de côtés parallèles, donc il est compté une fois dans
chacun des deux groupes de pentes correspondants, soit deux fois.

Aucun autre chiffre n'est compté par l'algorithme, car toutes les paires comptées sont
parallèle et non collinéaire (Lemma 2). *



Lemma 4
`parallélogrammes = point C(cntMidpoint, 2)`
compte chaque parallélogramme exactement une fois.

**Prof.**

Dans un parallélogramme, les deux diagonales se croisent, d'où leur
Les points médians coïncident.
Inversement, si deux segments partagent le même point médian, les quatre paramètres
former un parallélogramme (les diagonales se croisent).
Ainsi, chaque paire non ordonnée de segments avec un point médian commun correspond à un
Parallélogramme unique, et chaque parallélogramme produit exactement une telle paire.
Par conséquent, la somme `C(cntMidpoint,2)` sur tous les points médians compte chaque
parallélogramme une fois.



Lemma 5
La formule finale

«» "
Total = C(cntSlope,2) – ↓_lignes C(cntLine,2) ) – parallélogrammes
«» "

égale le nombre de trapèzes **distincts** qui peuvent être formés.

**Prof.**

De Lemma 3 la première somme compte chaque trapèze une fois,
et chaque parallélogramme deux fois.
Lemma 4 montre que les `parallélogrammes` sont le nombre de
parallélogrammes dans l'entrée.
La soustraction supprime le deuxième comptage de chaque parallélogramme,
laissant exactement une occurrence de chaque trapèze (parallélogramme inclus). *



C'est vrai. Théorème
L'algorithme décrit ci-dessus renvoie le nombre de
trapèzes qui peuvent être construits à partir de l'ensemble de points donné.

**Prof.**

L'algorithme implémente les trois étapes de comptage prouvées correctes par
Lemmas 1–5 et finalement évalue la formule de Lemma 5.
Par conséquent, le nombre produit est précisément celui souhaité. *



-----------------------------------------------------------------------------------

C'est vrai. 6. Analyse de la complexité

«» "
N = nombre de points (N ≤ 500)

Nombre de paires de points: M = N·(N–1)/2 ≤ 124 750
«» "

* Construire les dictionnaires* – "O(M)"
* Calcul des sommes* – linéaire dans le nombre de clés distinctes
('O(nombre_de_lopes + nombre_de_lignes + nombre_de_points)'), tous des
ils sont liés par `M`.

«» "
Temps : O(N2) (= 1,25·10^5 opérations dans le cas le plus défavorable)
Mémoire : O(N2) (trois tables de hachage, chacune au maximum des entrées M)
«» "

Les deux limites sont facilement à l'intérieur des limites de la tâche.



-----------------------------------------------------------------------------------

C'est vrai. 7. Mise en œuvre des références (Python 3)

'`python
importer des maths
de taper l'importation Liste, Tuple

♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

def comb2(x: int) -> Int:
"""Retour C(x,2) = x*(x-1)/2, mais pour x<2, le résultat est 0.""
retour x * (x - 1) // 2 si x >= 2 autres 0

♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
♪ Résolveur principal

def count_trapézoïdes(points: Liste[Tuple[int, int]]) -> Int:
pente_cnt = {}
ligne_cnt = {}
mi_cnt = {}

pour i dans la plage(len(points)):
x1, y1 = points[i]
pour j dans la plage(i + 1, len(points)):
x2, y2 = points[j]

dx = x2 - x1
dy = y2 - y1

# ---------- pente --------------------------------
Si dx == 0: # verticale
g = abs(dy)
slope_key = ("inf", dy // g)
interception_clé = (x1, 0) # x = const
Sinon:
g = maths.gcd(dx, dy)
dx //= g
dy/= g
si dx < 0:
dx, dy = -dx, -dy
slope_key = (dy, dx)

# pente m = dy/dx
num = y1 * dx - x1 * dy # b * dx
den = dx
g2 = maths.gcd(num, den)
num //= g2
den //= g2
interception_clé = (num, den)

La clé de la ligne - Oui.
line_key = (slope_key, interception_key)

C'est... Mettre à jour les dictionnaires ------------------
slope_cnt[slope_key] = slope_cnt.get(slope_key, 0) + 1
line_cnt[line_key] = line_cnt.get(line_key, 0) + 1

La clé du milieu -----------
mi_clé = (x1 + x2, y1 + y2)
mi_cnt[mid_key] = mi_cnt.get(mid_key, 0) + 1

C'est... trapèzes + 2×parallélogrammes - Oui.
Total = 0
pour s, c en pente_cnt.items():
Total += peigne2c)

pour c dans line_cnt.values():
Total -= peigne2c)

C'est... parallélogrammes - Oui.
Par = 0
pour c dans les valeurs milieu_cnt.():
par += peigne2c)

retour int(total - par)

♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
♪ Exemple d'utilisation

si __nom__ == "__main__" :
Exemple 1
points = [(0, 0), (1, 1), (1, 2), (2, 1), (2, 2), (3, 3)
print(count_trapézoïdes(points)) # → 4
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus
et conforme à la signature de la fonction requise `count_trapezoïdes`.

-----------------------------------------------------------------------------------

C'est vrai. 8. Mise en œuvre des références (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

en utilisant ll = long;

ll comb2(ll x){ retour x < 2 ? 0 : x*(x-1)/2; }
ll gcdll(ll a, ll b){ retourner std::gcd(a,b); }

Int main(){
ios::sync_with_stdio(faux);
cin.tie (nullptr);
nombre de points
si(!(cin >> n)) retourner 0;
vecteur<pair<ll,ll>> p(n);
pour(int i=0;i<n;i++) cin >> p[i].premier >> p[i].seconde;

sans ordre_map<string,ll> pente Cnt, ligneCnt, milieuCnt;

Pour(int i=0;i<n;i++){
ll x1=p[i].premier, y1=p[i].seconde;
pour(int j=i+1;j<n;j++){
ll x2=p[j].premier, y2=p[j].seconde;
ll dx=x2-x1, dy=y2-y1;

// --------- pente ---------
pente de la chaîne Clé;
if(dx=0){
ill g=gcdll(abs(dy),1);
dy/=g; // garder le signe dans dy
la penteKey"inf"+to_string(dy);
}else {
ill g=gcdll(abs(dx),abs(dy));
dx/=g; dy/=g;
if(dx<0){ dx=-dx; dy=-dy; }
slopeKey=to_string(dy)+"_"+to_string(dx);
}

// -------- Intercepter - Oui.
chaîne interceptée Clé;
if(dx=0){
interceptionKey=to_string(x1)+"_0"; // x = const
}else {
// pente m = dy/dx, donc b = y1 - m*x1 = (y1*dx - x1*dy)/dx
ll num=y1*dx - x1*dy;
ll den=dx;
ill g2=gcdll(abs(num),den);
num/=g2; den/=g2;
intercepterKey=to_string(num)+"_"+to_string(den);
}

// --------- touche de ligne --------
chaîne de caractères ligneKey = penteKey+"""+intercept Clé;

slopeCnt[slopeKey]++;
ligne Cnt[ligne Clé]++;

// ---------point médian - Oui.
ll midKeyX=x1+x2, midKeyY=y1+y2;
chaîne midKey = to_string(midKeyX)+"_"+to_string(midKeyY);
Moyenne Clé]++;
}
}

ll total = 0;
pour (auto &kv : penteCnt) total += comb2(kv.seconde);
pour (auto &kv : lineCnt) total -= comb2(kv.seconde);

ll par = 0;
pour (auto &kv : midCnt) par += comb2(kv.seconde);

Il répond = total - par;
cout << réponse << '\n';
retour 0;
}
«» "

-----------------------------------------------------------------------------------

C'est vrai. 9. Mise en œuvre des références (Java 17)

"Java
importation java.io.*;
Importation de java.util.*;

classe publique TrapézoïdeCounter {

/* **----------------------------------------------------------------
Peigne longue statique2(long x){ retour x<2?0L:x*(x-1)/2L; }

/* **----------------------------------------------------------------
pente de chaîne statiqueKey(long dx, long dy){
if(dx==0) retourner "inf"+dy; // vertical
g = Math.abs(gcd(dx,dy));
dx/=g; dy/=g;
if(dx<0){ dx=-dx; dy=-dy; }
retourner dy+"_"+dx;
}

Intercepteur de chaînes statiques Clé(long x1,long y1,long x2,long y2,long dx,long dy) {
if(dx==0){ // verticale
retour x1+"_"+0; // x = const
}else {
long num = y1*dx - x1*dy; // 2*b
long den = dx;
g = Math.abs(gcd(num,den));
num/=g; den/=g;
retourner num+"_"+den;
}
}

/* **----------------------------------------------------------------
statique long gcd(long a, long b) {
if(b==0) retourne Math.abs(a);
retourner gcd(b, a%b);
}

/* **----------------------------------------------------------------
public statique vide main(String[] args) lance Exception{
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
long[][] p = nouveau long[n][2];
Pour(int i=0;i<n;i++){
StringTokenizer st = nouveau StringTokenizer(br.readLine());
p[i][0] = Long.parseLong(st.nextToken());
p[i][1] = Long.parseLong(st.nextToken());
}

Carte<String,Integer> penteCnt = nouveau HashMap<>();
Carte <String,Integer> lineCnt = nouveau HashMap<>();
Carte<String,Integer> milieuCnt = nouvelle HashMap<>();

Pour(int i=0;i<n;i++){
long x1=p[i][0], y1=p[i][1];
pour(int j=i+1;j<n;j++){
longueur x2=p[j][0], y2=p[j][1];
longue dx=x2-x1, dy=y2-y1;

Chaîne sKey = penteKey(dx,dy);
Chaîne iKey = interceptionKey(x1,y1,x2,y2,dx,dy);
Chaîne lKey = sKey+""+iKey;

penteCnt.merge(sKey,1,entier::sum);
lineCnt.merge(lKey,1,entier::sum);

long mx=x1+x2, my=y1+y2;
Chaîne mKey = mx+"_"+my;
midCnt.merge(mKey,1,entier::sum);
}
}

long total = 0;
pour(int c : penteValeurs Cnt.() total += peign2(c);
pour(int c : lineCnt.values() total -= comb2(c);

long par = 0;
pour(int c : midCnt.values() par += comb2(c);

réponse longue = total - par;
Système.out.printn(réponse);
}
}
«» "

Les trois programmes de référence mettent en œuvre la même logique,
compatible avec les versions linguistiques spécifiées, et
résoudre le problème dans les limites des contraintes données.