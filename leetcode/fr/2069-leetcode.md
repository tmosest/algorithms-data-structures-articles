---
titre: LeetCode 2069. Simulation robot de marche II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes (LeetCode 2069 – *Walking Robot Simulation II*)

* Une grille `largeur × hauteur` est sur le plan XY.
Cellule inférieure gauche = `(0, 0)`, cellule supérieure droite = `(largeur‐1, hauteur‐1)`.
Le robot peut faire face à l'une des quatre directions cardinales – le nord, l'est, le sud, l'ouest.
* Le robot commence à "(0, 0)" face à **Est**.
* `step(num)` – le robot doit prendre `num` les étapes d'une cellule.
Pour chaque étape:
1. Essayez de faire avancer une cellule dans la direction actuelle.
2. Si cette cellule se trouvait à l'extérieur de la grille, ** tourner 90° dans le sens contraire des aiguilles d'une montre** au lieu de se déplacer.
3. Après le tour, réessayez la même étape (ainsi un tour compte * comme* une seule étape).
* `getPos()` – retour `[x, y]`.
* `getDir()` – retourne la chaîne de direction actuelle.

**Contrôles* *

«» "
2 ≤ largeur, hauteur ≤ 100
1 ≤ num ≤ 10^5
≤ 10^4 nombre total d'appels vers step/getPos/getDir
«» "

---

- Oui. 2. Idée de base – réduire le nombre d'étapes simulées

La trajectoire du robot est *périodique*: après avoir parcouru le périmètre de la grille, il sera de retour à la même position avec la même direction.

Longueur du périmètre
«» "
P = 2 * (largeur + hauteur) – 4 // nombre de cellules dans l'anneau extérieur
«» "
Par exemple, une grille 6×3 → `P = 2*(6+3)-4 = 14`.

Si nous prenons `step(num)`, seulement `num % P` φreal=' les étapes comptent - le reste juste répéter le même cycle.

Parce que "largeur, hauteur ≤ 100", le périmètre "P ≤ 396".
Donc, après l'opération modulo, nous pouvons simuler en toute sécurité les 395 étapes restantes en boucle – c'est O(1) par appel et jamais dépasser quelques centaines d'itérations.

---

- Oui. 3. Solutions de référence

#### 3.1 Java (style LeetCode)

"Java
// Java 17 (compatible avec LeetCode)
Robot public {
intérieur final int w, h; // taille de la grille
int privé x, y; // position actuelle
Int dir privé; // 0:E, 1:N, 2:W, 3:S

finale statique privée Chaîne[] DIRS = {"Est", "Nord", "Ouest", "Sud"};
// vecteurs de mouvement pour E, N, W, S
DX = {1, 0, -1, 0};
int final statique privé[] DY = {0, 1, -1};

Robot public (largeur de l'int, hauteur de l'int) {
w = largeur;
h = hauteur;
ce.x = 0;
ce.y = 0;
ce.dir = 0; // Est
}

Pas de vide public(int num) {
Si (nombre) 0) retour;

périmètre int = 2 * (w + h) - 4;
num %= périmètre; // seulement les autres questions
Si (nombre) 0) retour; // cycle complet → rien ne change

pour (int i = 0; i < num; i++) {
Int nx = x + DX[dir];
int ny = y + DY[dir];

si (nx < 0) nx >= w) ny < 0) ny >= h) {
// Compteur de virage dans le sens des aiguilles d'une montre
dir = (dir + 1) et 3; // +1 mod 4
} autre {
x = nx;
y = ny;
}
}
}

public int[] getPos() {
retourner une nouvelle int[] {x, y};
}

chaîne publique getDir() {
retourner DIRS[dir];
}
}
«» "

> **Pourquoi ça marche* *
> * "num % P" garanties au plus 395 itérations.
> * Le modulo élimine la partie lourde de l'appel.
> * Le virage n'est qu'un changement d'index ; le déplacement est un simple ajout de coordonnées.

3.2 Python 3

'`python
# Python 3.9
Robot de classe:
DIRS = ["Est", "Nord", "Ouest", "Sud"]
DX = [1, 0, -1, 0]
DY = [0, 1, 0, -1]

def __init__(self, largeur: int, hauteur: int):
Self.w, self.h = largeur, hauteur
Self.x, self.y = 0, 0
Dir = 0 # 0:E, 1:N, 2:W, 3:S

def step(self, num: int) -> Aucun:
si num] 0:
retour
durée = 2 * (self.w + self.h) - 4
%= durée
si num] 0:
retour

pour _ dans l'intervalle(num):
nx = self.x + self.DX[self.dir]
ny = self.y + self.DY[self.dir]
Si non (0 <= nx < self.w et 0 <= ny < self.h):
# virage dans le sens contraire des aiguilles d'une montre
auto.dir = (auto.dir + 1) % 4
Sinon:
Self.x, self.y = nx, ny

def getPos(self) -> list[int]:
retour [self.x, self.y]

def getDir(self) -> str:
Revenez vous-même. DIRS [self.dir]
«» "

### 3.3 C++ (GCC 17)

'`cpp
// C++17 (Code Leet)
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

Robot de classe {
particulier:
Const int w, h; // dimensions de la grille
int x, y; // position actuelle
dir; // 0:E 1:N 2:W 3:S

vecteur statique const <string> DIRS;
DX[4];
static const int DY[4];

public:
Robot(largeur int, hauteur int) : w(largeur), h(hauteur), x(0), y(0), dir(0) {}

pas de vide(int num) {
Si (nombre) 0) retour;

périmètre int = 2 * (w + h) - 4;
num %= périmètre;
Si (nombre) 0) retour;

pour (int i = 0; i < num; ++i) {
Int nx = x + DX[dir];
int ny = y + DY[dir];
si (nx < 0) nx >= w) ny < 0) ny >= h) {
dir = (tir + 1) et 3; // compteur de virage– dans le sens des aiguilles d'une montre
} autre {
x = nx;
y = ny;
}
}
}

vector<int> getPos() const {
retourner {x, y};
}

chaîne getDir() const {
retourner DIRS[dir];
}
};

Définition des membres statiques
vecteur const <string> Robot::DIRS = {"Est", "Nord", "Ouest", "Sud"};
Const int Robot::DX[4] = {1, 0, -1, 0};
Robot const int::DY[4] = {0, 1, 0, -1};
«» "

> **Pourquoi la boucle est sûre** – après `num %= périmètre` la boucle tourne ≤ 395 itérations (le pire cas `w=h=100` → `périmètre=396`).
> Les frais généraux du module lui-même sont négligeables, de sorte que la complexité globale est **O(1)** par appel "étape".

---

- Oui. 4. Comment parler de ce problème dans une interview

Autres **Ce que vous avez demandé**
-- -- -- -- -- ------------------------------------------------------------------
**Expliquez la périodicité** Autres
Autres **Afficher une solution rapide**= Une boucle naïve au-dessus de `num` pourrait exploser jusqu'à `10^9` opérations → time-out. Autres
** Contraintes de Mention** Le petit périmètre (396) garantit une boucle à temps constant. Autres
Autres **Parler sur les cas de bord** Autres
**Optionnel : maths directs**. Calculez la distance jusqu'au bord et sautez les tours entiers en une seule étape, mais pas nécessaire pour les limites. Autres

> **À emporter** – *Vérifiez toujours les répétitions cachées* avant de simuler aveuglément.
> Cette astuce transforme une simulation en une poignée d'opérations.

---

- Oui. 5. Article de blog (prêt à l'emploi)

> **Titre**
> **La simulation du robot Walking II – Le bon, le mauvais et le mauvais problème d'entrevue de LeetCode* *

> **Description détaillée* *
> Apprenez à résoudre efficacement le LeetCode 2069, quel piège à éviter, et comment maîtriser ce problème peut vous aider à coder des interviews et atterrir un rôle d'ingénierie logiciel.

> **Mots clés**
> LeetCode 2069, Walking Robot Simulation II solution de codage d'entretien de simulation d'entretien d'entretien d'entretien d'entretien d'entretien de logiciel d'entretien d'entretien d'entretien d'emploi.

---

5.1 Le bon – Pourquoi ce problème est un test d'entrevue *classique*

1. ** Déclaration claire** – Les règles sont sans ambiguïté, ce qui signifie que vous pouvez vous concentrer sur l'algorithme, pas sur l'analyse du problème.
2. **Cadre de cale** – Une trajectoire périodique est un moment magnifique. Reconnaître qu'il montre des compétences de reconnaissance de modèle, une capacité d'entrevue prisée.
3. **Petites contraintes** – La grille est minuscule, ce qui vous permet de prototyper avec une simple boucle et ensuite d'optimiser seulement si nécessaire.
4. **Langues multiples** – Démonstration de la solution en Java, Python et C++ montre des compétences de conception langage-agnostique.

5.2 Les mauvaises – Pièges communs qui vous coûteront du temps

Pourquoi il échoue
C'est quoi ?
Autres Simulation de chaque étape (même après le modulo) Avec `num = 10^5` et 10^4 appels → 10^9 opérations → TLE. Autres
Autres Oublier qu'un *turn* compte comme un pas Vous pouvez sauter un pas après un tour et finir avec la mauvaise position. Autres
Autres Utiliser la mauvaise formule de périmètre compte les cellules externes *deux fois*; vous devez soustraire 4 pour éviter de doubler le compte des cellules d'angle. Autres
Autres Erreurs hors-par-un lors d'un virage aux frontières Un robot faisant face à l'Est tournera vers le Nord – vérifiez votre ordre de direction (E→N→W→S→E). Autres

5.3 L'Ugly – Quand vous écrivez une solution rapide et sale

> ** Implémentation rapide et sale**
> ``python
> def step(self, num):
> pour _ dans l'intervalle(num):
> # Logique en une seule étape
> `` "
> Cela passe avec les minuscules cas d'essai, mais les essais de contrainte cachés seront interrompus.

> Pourquoi c'est moche ?
> * La complexité O(`num`) est linéaire et sans limite.
> * Il ignore le cycle évident.
> * Il risque une durée d'exécution de 10 secondes sur LeetCode, qui apparaîtra dans votre journal d'entrevue.

> **Éviter** – Toujours chercher un cycle ou un raccourci avant de sauter dans une simulation complète.

---

- Oui. 6. Démarrage rapide – Lancer les solutions localement

#### 6.1 Java

"""
# compilez & exécutez un test rapide
Javac Robot.java
Java Robot // (LeetCode invoquera la classe Robot; utilisez un petit harnais de test si vous voulez)
«» "

6.2 Python

"""
# robot python3. py
Python3 - <<'PY'
de robot importation Robot

r = Robot(6, 3)
r.étape(10)
print(r.getPos(), r.getDir()
étape(20)
print(r.getPos(), r.getDir()
PY
«» "

*### 6.3 C++

"""
g++ -std=c++17 -O2 -pipe -statique -s robot.cpp -o robot
./robot # exécutez votre propre harnais de test
«» "

---

- Oui. 7. A emporter pour votre prochaine entrevue

1. **Spot the pattern first** – un robot de grille sur un rectangle se déplace toujours le long du périmètre.
2. **Réduire la taille du problème avec un modulo** – après cela il ne reste qu'une poignée de vraies étapes.
3. **Mise en œuvre d'une boucle O(1) propre** – simulation après le modulo est trivial et sûr.
4. **Cas de bord de test** – étape de cycle complet (`num % P=0`), tournant sur un coin, grandes valeurs `num`, etc.
5. ** Expliquez votre processus de pensée** – les intervieweurs aiment entendre *pourquoi* vous avez utilisé un modulo vs une simulation complète.

Avec les solutions ci-dessus en main (Java, Python, C++), vous serez prêt à flasher ce problème lors de toute interview de codage et montrer que vous pouvez penser à la fois rapide et profonde.

---

** Bon codage – et que votre robot trouve toujours la bonne direction!**