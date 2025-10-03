---
titre: LeetCode 519. Matrice de glissement aléatoire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
519. Matrice de glissement aléatoire – Mise en œuvre intégrale (Java, Python, C++)

Ci-dessous vous trouverez une solution **ready‐to‐copy** pour chaque langue prise en charge par LeetCode, ainsi qu'un billet de blog **step‐by‐step** qui passe par les parties de ce problème d'entrevue classique.
N'hésitez pas à déposer les extraits dans votre IDE, à exécuter les tests fournis ou à les coller directement dans l'éditeur LeetCode.

---

## Code – rapide, efficace en mémoire et aléatoire

> **Idée clé** – Carte d'un indice linéaire *virtuel* à l'indice réel de la matrice.
> Chaque `flip` dessine un nombre aléatoire `k` dans `[0, reste‐1]`.
> Si cet index a déjà été retourné, nous stockons un *swap* dans une carte de hachage.
> Cela transforme le problème en un simple échantillon de réservoir avec le temps `O(1)` et `O(#flips)` espace.

Code de la langue
C'est quoi, ça ?
**Java** Afficher Java</résumé>``java
Importation de java.util.*;

solution de classe {
final privé int m, n;
Int privé restant; // cellules qui sont toujours 0
carte finale privée <entier, entier> carte; // virtuel -> cartographie réelle
Finale privée Rand aléatoire;

solution publique(int m, int n) {
ce.m = m;
n = n;
Ça. restant = m * n;
ce.map = nouveau HashMap<>();
ce.rand = nouveau Random();
}

/** @return [row, col] d'une cellule retournée */
Int[] flip() {
int r = rand.next Int(remaining); // choisir une cellule libre aléatoire
// l'indice réel peut avoir été échangé plus tôt
int real = map.getOrDefault(r, r);

// choisir la dernière cellule libre pour remplir le trou laissé par r
int last = restant - 1;
int lastReal = map.getOrDefault(dernier, dernier);

// carte r à la fin Real (la prochaine fois que r donnera la dernière Real)
map.put(r, lastReal);
// nous n'avons plus besoin de durer dans la piscine
si (r) la dernière) map.supprimer(r);

restant--; // une cellule moins libre
retourner une nouvelle int[]{real / n, real % n};
}

vide public réinitialisation() {
cart.clear();
restant = m * n;
}
}
```</details> Autres
*Python *Détails *<résumé > Afficher Python</résumé>``python
importation aléatoire
de taper l'importation Liste

Solution de classe:
def __init_(self, m: int, n: int):
m, m = m, n
self.rem = m * n # autres zéros
auto.mapping = {} # virtuel -> indice réel

def flip(self) -> Liste[int]:
r = aléatoire.randint(0, self.rem - 1)
réel = auto.mapping.get(r, r)

dernier = self.rem - 1
last_real = self.mapping.get (dernier, dernier)

# map l'index choisi vers la dernière cellule libre
self.mapping[r] = last_real
si r == dernier:
Self.mapping.pop(r, Aucun)

Self.rem -= 1
retour [réel // self.n, réel % self.n]

def reset(self) -> Aucun:
Self.mapping.clear()
self.rem = self.m * self.n
```</details> Autres
**C++** Affichage C++</résumé>``cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
int m, n, restant;
unordered_map<int,int> mp; // virtual -> cartographie réelle
mt19937 rng; // moteur moderne au hasard

public:
Solution(int m, int n) : m(m), n(n), restant(m*n) {
ng.seed(random_device{}());
}

vecteur<int> flip() {
uniform_int_distribution<int> dist(0, restant - 1);
int r = dist(rng); // choisir une cellule virtuelle libre
int real = mp.count(r) ? mp[r] : r; // traduire à l'index réel

int last = restant - 1;
int lastReal = mp.count(last) ? mp[last] : le dernier;

// remplir le trou laissé par r avec la dernière cellule libre
mp[r] = dernièreréalité;
si (r ==dernière) mp.erase(r);

--rester;
retour { réel / n, réel % n };
}

vide réinitialisé() {
mp.clear();
restant = m * n;
}
};
```</details> Autres

> **Pourquoi ça marche* *
> 1. Chaque appel tire un numéro aléatoire de la réserve *current* de cellules libres.
> 2. Nous conservons une bijection entre les indices virtuels `[0, restant-1]` et les indices réels `[0, m*n-1]`.
> 3. Après le basculement, nous remplaçons l'index utilisé par le dernier libre, garantissant que les futurs tirages ne voient plus jamais le même index.
> 4. `reset()` efface simplement la carte et restaure la taille originale de la piscine.

---

Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 519

> **Audience cible :** Ingénieurs de front / back-end, passionnés de data-structure, et quiconque se prépare à des entrevues par algorithme.
> **Mots-clés du référencement:** *Code de leet 519*, *Matrice de flip de random*, *Java interview questions*, *Python interview problems*, *C++ interview algorithmes*, *O(1) flip matrix*, *algorithme design*, *coding interview conseils*.

---

Titre
**Le bon, le mauvais, et le mauvais de LeetCode 519: Maîtriser la matrice de glissement aléatoire en Java, Python et C++* *

### TL;DR
- **Bien**: Temps linéaire, mémoire O(#flips), pas de grille supplémentaire, accès aléatoire à temps constant.
- **Bad**: Les approches naïves sont *O(m*n) et *O(m*n) par flip – inévoluables.
- **Ugly**: Le mauvais traitement de la graine aléatoire ou la logique d'échange conduit à des bugs subtils et biais dans le hasard.

---

C'est vrai. 1. Aperçu du problème

> *On vous donne une matrice binaire `m × n` initialement remplie de zéros.
> Chaque appel à `flip()` doit renvoyer un index aléatoire uniforme `(i, j)` où la cellule est `0`, retourner cette cellule à `1`, et garantir que chaque `0` restant a une chance égale d'être sélectionné.
> L'opération `reset()` restaure la matrice à tous les zéros. *

Les contraintes sont généreuses (`m, n ≤ 104`), mais seulement jusqu'à **1000** opérations `flip`/`reset`. Nous avons donc besoin d'un algorithme qui fonctionne bien même pour les matrices massives.

---

C'est vrai. 2. L ' approche négative

Méthode Temps Espace Commentaires
- C'est quoi ?
Tableau 2-D + liste des cellules libres Enregistre toute la matrice – impossible pour 108 cellules. Autres
Scan aléatoire jusqu'à ce qu'une cellule libre soit trouvée. Autres

La solution naïve **fails** parce qu'elle viole les contraintes d'entretien:
- Vous devez garder un tableau ou une liste de *chaque cellule* pour garantir l'uniformité, faire exploser la mémoire.
- Re-scanner la matrice pour chaque tour devient un goulot d'étranglement de performance.

> **Pourquoi c'est mauvais? **
> La complexité de l'algorithme est une fonction de la taille de la grille *entre* et non du travail *réel* que vous faites.
> Pour une matrice de 104 × 104 qui signifierait stocker 108 int – tout simplement impossible sur la plupart des machines d'entrevue.

---

C'est vrai. 3. L'élégant (bon) Cartographie

1. **Flatte la matrice**
Traitez la matrice 2-D comme un tableau 1-D de longueur `N = m * n`.
Un indice linéaire `x` à `(x / n, x % n)`.

2. **Maintenir un comptoir de maintien**
«rester = N» initialement.
Chaque flip réduit le « maintien » par un seul.

3. **Utilisez une carte Hash pour l'échange**
Texte
_index virtuel _index réel
«» "
*Quand un index virtuel est utilisé, nous le mapons à la dernière cellule libre, puis supprimons cette cellule de la piscine. *

4. **Random Choice**
Choisir `k` uniformément dans `[0, restant-1]`.
Traduire `k` vers un index réel en utilisant la carte (`k` peut avoir été échangé plus tôt).
Échangez `k` avec `remaining-1` (la dernière cellule libre).

5. **Retourner les coordonnées 2-D* *
`row = real / n`, `col = real % n`.

**Pourquoi c'est bon**
- **O(1)** par «flip»/«reset».
- **O(k)** mémoire où `k` est le nombre de flips (1 000).
- Oui. Pas besoin de stocker toute la matrice.
- Le hasard est *non biaisé* car chaque tirage provient d'un sous-ensemble uniformément aléatoire des cellules libres actuelles.

> **Pseudocode (style python)* *
> ``python
> r = random.randint(0, restant-1)
> real = mapping.get(r, r)
> dernier = restant- 1
> lastReal = mapping.get(last, last)
> mapping[r] = dernierReal
> restant -= 1
> retour [réel // n, réel % n]
> `` "

---

3.1. Pièges

Correction du bug
C'est pas vrai.
**Swap incorrect quand `r=dernier=**=La carte contient toujours une clé qui n'existe plus dans le pool, brisant les futurs tirages. Supprimer la clé (`mapping.pop(r, None)`) quand `r == last`.
**L'utilisation de `randint` avec des limites inclusives**=________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________ Utiliser `randint(0, reste-1)` ou `nextInt(remaining)`. Autres
**Semences de mauvaise gestion** Utilisez une graine *fresh* (`mt19937` + `random_device` dans C++, `Random()` dans Java, RNG par défaut dans Python). Autres
**Contrôles en hash dans des langages de haut niveau**= Rares, mais pouvant dégrader les performances.= Utiliser `unordered_map` (C++), `HashMap` (Java), ou Python=s dict – tous sont amortis O(1). Autres

---

C'est vrai. 3. 3. Mise en œuvre pratique

Les extraits de code dans la section précédente incarnent déjà la solution **good**.
Ci-dessous sont **complet, commenté** extraits pour chaque langue – les déposer directement dans LeetCode.

> **Astuce:** En Python, évitez `numpy` ou toute bibliothèque lourde.
> Dans le C++, utiliser `mt19937` au lieu du `rand()' déprécié pour une meilleure uniformité.

---

C'est vrai. 4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
"flip()" **O(1)** (prévu)
"Reset()" **O(1)** – efface la carte
Total pour < k > flips **O(k)**

> ** Empreinte mémoire* *
> Au plus 1000 entiers sur la carte de hachage → < 10 KB même en Java (int 32 bits).
> Plus léger que le stockage de la matrice entière (jusqu'à 400 Mo pour 108 cellules).

---

C'est vrai. 5. Pourquoi le hasard compte dans les entrevues

- **Uniformité**: Les intervieweurs s'attendent à ce que vous fournissez une sélection aléatoire vraiment uniforme.
- **Bias**: Même une seule affectation déplacée peut fausser les probabilités.
- **Reproductibilité**: Certaines plateformes d'entrevue exécuteront votre solution sur la même entrée plusieurs fois. Assurez-vous que votre générateur aléatoire n'utilise pas une graine fixe à moins d'être explicitement requis.

---

C'est vrai. 6. Conseils pratiques

1. ** Effectuez vos propres tests**
'`python
s = Solution(10000, 10000)
pour _ dans l'intervalle(1000):
r = s.flip()
s.reset()
«» "
Vérifiez que `reset()` restaure la taille de la piscine.

2. **Vérifier l'homogénéité**
Simuler 1 000 flips sur une petite matrice (`m=2, n=2`) et compter la distribution des sorties. L'histogramme doit être plat.

3. **Délibérations**
- "flip()" appelé lorsque la matrice est pleine (`remaining == 0`) – devrait lancer une exception ou gérer gracieusement.
- `reset()` appelé à plusieurs reprises – devrait toujours effacer la carte.

4. **Pointeurs d'entrevue**
- Expliquez l'idée de mapping "virtuel".
- Mention de **échantillonnage de réservoir** comme analogie conceptuelle.
- Mettre en évidence les compromis entre espace/temps et méthode naïve.

---

C'est vrai. 7. Conclusion – Vous êtes prêt à accepter l'entrevue

- **Bien**: O(1) par opération, mémoire minimale, utilisation élégante d'une carte de hachage.
- **Bad**: Entreposer toute la grille est une *erreur fatale* sur une grande matrice.
- **Ugly**: Sauter les cas de bord de clé (comme l'échange du même indice) produira des résultats biaisés ou incorrects, souvent inaperçus jusqu'à ce qu'un cas de test échoue.

Déposez ce code dans votre dépôt, ajoutez une brève description de l'algorithme dans votre README, et vous aurez une référence **ready** pour les prochaines entrevues.

Bon codage ! C'est ce qu'il a dit.

---

- Oui. Vous voulez plus de code prêt à l'entrevue?
Abonnez-vous à notre bulletin d'information sur les problèmes de LeetCode hebdomadaires, les explications vidéo et les défis de préparation à l'entrevue.

---

> **Auteur:** *[Votre nom]* – *Ingénieur de l'algorithme
> **Contact:** `votre.email@example.com` "

---

**Fin du blog* *

---

Liens rapides

Section d'ancrage
C'est pas vrai.
Code Autres
Article du blog
TL,DR,#tldr Autres

---

Joyeux entretien, et rappelez-vous : **Le bon tour de la structure des données est la moitié de la bataille. **