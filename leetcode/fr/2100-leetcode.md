---
titre: LeetCode 2100. Trouver de bons jours pour Rob the Bank -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Solution 3-Langue – Trouver de bons jours pour voler la banque (Code de débit 2100)

Ci-dessous vous trouverez un algorithme propre **O(n)** dans **Java**, **Python** et **C++**.
Les trois implémentations utilisent la même technique de préfixe à deux passages :

1. **decr[i]** – nombre de jours consécutifs non croissants se terminant à *i* (regardez à gauche → à droite).
2. **incr[i]** – nombre de jours consécutifs non décroissants à partir de *i* (voir à droite → à gauche).

Un jour *i* est "good" si les deux compteurs sont ≥ "time".

Autres **Pourquoi est-ce la meilleure approche? **
> La fenêtre coulissante de force brute serait **O(n·time)**, qui peut exploser lorsque "temps -105".
> La méthode préfixe-suffix donne un balayage linéaire et est donc optimale.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<entier> goodDaysTobBank(int[] security, int time) {
int n = sécurité. longueur;
int[] décr = nouveau int[n]; // préfixe non croissant
int[] incr = nouveau int[n]; // suffixe non décroissant

// à gauche → à droite : compter des jours consécutifs non croissants
pour (int i = 1; i < n; i++) {
si (sécurité[i] <= sécurité[i - 1]) {
decr[i] = decr[i - 1] + 1;
} autre {
decr[i] = 0;
}
}

// droite → gauche : nombre de jours consécutifs non déclenchants
pour (int i = n - 2; i >= 0; i--) {
si (sécurité[i] <= sécurité[i + 1]) {
incr[i] = incr[i + 1] + 1;
} autre {
incr[i] = 0;
}
}

Liste du résultat <entier> = nouvelle liste de distribution<>();
pour (int i = temps; i < n - temps; i++) {
si (décr[i] >= temps && incr[i] >= temps) {
résultat.add(i);
}
}
le résultat du retour;
}
}
«» "

---

Python

'`python
de taper l'importation Liste

Solution de classe:
def goodDaysTobBank(self, security: List[int], time: int) -> Liste[int]:
n = len(sécurité)
decr = [0] * n # préfixe non croissant
encr = [0] * n # suffixe non décroissant

# gauche → droite
pour i dans la plage (1, n):
decr[i] = decr[i-1] + 1 si security[i] <= security[i-1] autre 0

# droite → gauche
pour i dans la plage(n-2, -1, -1):
incr[i] = incr[i+1] + 1 si security[i] <= security[i+1] autre 0

retour [i pour i dans l'intervalle (temps, n-temps)
si décr[i] >= temps et incr[i] >= durée]
«» "

---

C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> goodDaysTobBank(vector<int>& security, int time) {
int n = security.size();
vecteur <int> décr(n, 0), incr(n, 0);

// gauche → droite : préfixe non croissant
pour (int i = 1; i < n; ++i)
decr[i] = (security[i] <= security[i-1]) ? decr[i-1] + 1 : 0;

// droite → gauche : suffixe non décroissant
pour (int i = n-2; i >= 0; --i)
incr[i] = (security[i] <= security[i+1]) ? incr[i+1] + 1 : 0;

vecteur <int> ans;
pour (int i = temps; i < n - temps; ++i)
si (décr[i] >= temps && incr[i] >= temps)
le nom de l'autorité compétente;

le retour des an;
}
};
«» "

---

Article du blog – Le bon, le mauvais et le mauvais: Mastering LeetCode 2100

Introduction

> **Problème :** *Trouvez de bons jours pour Rob the Bank* – un défi de niveau moyen qui teste votre capacité à raisonner sur les préfixes, les suffixes et les fenêtres coulissantes.
> **Objectif:** Fournir une solution concise, **O(n)** qui passe tous les cas de bord.

Dans ce post nous allons explorer:

1. Le problème est la mécanique du noyau.
2. Une stratégie linéaire *bonne*.
3. Pièges communs (*les mauvais*).
4. Le tour subtil qui rend l'algorithme robuste (*la moche*).

Et nous poivrons l'article avec **mots-clés de référence** tels que *LeetCode 2100*, *array prefix*, *dynamic programming*, *interview coding*, *Java Python C++ solutions* afin que vous puissiez trouver sur Google et atterrir ce travail!

---

C'est pas vrai. Comprendre le bien

Une *bonne journée* nécessite **deux motifs symétriques**:

- **Non-augmentation** gardes pendant "temps" jours avant "i".
- **Non-diminution** gardes pendant les «temps» jours suivant «i».

La solution la plus naïve vérifierait chaque jour avec deux boucles, coûtant **O(n·time)**. Lorsque le "temps" est aussi grand que le "105", cela devient impossible.

**Connaissance clé:** Les deux modèles peuvent être précalculés avec deux passes linéaires :

Ce que nous calculons Pourquoi ça marche
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
La plus longue stries non croissantes se terminant à "i" Si la longueur de stries ≥ `temps`, nous savons déjà que la partie "avant" est bonne. Autres
"incr[i]": la plus longue série non décroissante commençant par "i" Autres

Une fois que les deux tableaux existent, un simple scan détermine tous les bons jours en **O(n)** temps.

---

- Oui. Les mauvaises – erreurs courantes

Pourquoi il échoue
- C'est quoi ?
**Utilisation `>=` * Certaines implémentations comparent `security[i] < security[i-1]` au lieu de `<=`. Cela élimine les comptes de garde égaux, qui sont permis par le problème. Utiliser `<=` pour la passe de gauche à droite et `<=` pour la passe de droite à gauche. Autres
* Erreurs budgétaires * Oublier d'exclure les jours qui n'ont pas "temps" jours avant ou après ( "i < temps" ou "i > n-1-temps").
**O(n2) approche** Précalculer les tableaux préfixe et suffixe au lieu de recalculer. Autres
**Great memory gaspillage**.Utiliser un tableau séparé pour chaque tendance de garde, mais ne pas les réutiliser. Seulement deux «int» de longueur «n» sont nécessaires; gardez-les locaux. Autres
**Ignorer le temps = 0**= Retourner une liste vide parce que `time` n'est jamais cochée.= Si `time == 0`, tous les indices sont valides – la boucle s'en occupe naturellement. Autres

---

C'est vrai. Les cas de bord que vous devez gérer

1. **Toutes valeurs égales**
«» "
sécurité = [5,5,5], temps = 1
«» "
Les deux "décr" et "incr" deviennent "0,1,2,...". Notre logique (`>= time`) fonctionne toujours.

2. **Très petits tableaux**
«» "
sécurité = [1], heure = 0
«» "
L'algorithme retourne gracieusement `[0]` parce que la boucle tourne de `i=0` à `i < 1-0`.

3. **Large 'temps' approche de la longueur du tableau* *
«» "
sécurité = [1,2,3,4], temps = 4
«» "
Aucun jour ne satisfait à la condition; les limites de la boucle («i < n - time») empêchent tout indice d'être pris en considération.

4. **Le nombre de gardes négatifs? **
Le problème garantit des nombres entiers non négatifs, mais notre algorithme fonctionnerait encore parce que les comparaisons ne reposent que sur l'ordre et non sur la valeur absolue.

---

####=4==Mettant tout en place – une mise en œuvre robuste

Voici la finale, prête à la production Code Java (vous pouvez copier-coller dans un éditeur LeetCode):

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<entier> goodDaysTobBank(int[] security, int time) {
int n = sécurité. longueur;
int[] décr = nouveau int[n]; // le plus long préfixe non croissant se terminant à i
int[] incr = nouveau int[n]; // suffixe non décroissant le plus long à partir de i

pour (int i = 1; i < n; i++) {
decr[i] = security[i] <= security[i-1] ? decr[i-1] + 1 : 0;
}

pour (int i = n-2; i >= 0; i--) {
incr[i] = security[i] <= security[i+1] ? incr[i+1] + 1 : 0;
}

Liste <Integer> res = nouvelle liste de distribution<>();
pour (int i = temps; i < n - temps; i++) {
si (décr[i] >= temps && incr[i] >= temps) {
l'alinéa i est remplacé par le texte suivant:
}
}
retour rés;
}
}
«» "

Le même motif se traduit par Python (compréhension de la liste) et C++ (`vector<int>`), comme montré précédemment.

---

C'est pas vrai. Pourquoi cela compte pour votre entrevue

Compétence Comment il apparaît dans la solution
-- -- -- -- -- -- ----------------------------------
**Manipulation de l'image** Autres
Autres **Le temps et la complexité de l'espace****La maîtrise de **O(n)** vs **O(n2)** les compromis. Autres
**La pensée d'Edge-case** ∙ La manipulation du temps == 0`, des tableaux très courts, de grandes stries. Autres
**Lisibilité du code**= Effacer les noms de variables (`decr`, `incr`), les commentaires et aucun nombre magique. Autres
**La polyvalence de la langue**=La présentation d'une logique identique en Java, Python et C++ démontre la capacité d'adaptation—un trait d'interview clé. Autres

---

### # Comment se faire trouver

- **Titre:** LeetCode 2100 – Trouver de bons jours pour voler la Banque (Java / Python / C++ O(n) Solution)
- **Meta Description:** Apprenez une solution propre et linéaire à LeetCode 2100. Comprendre les préfixes, les suffixes, les pièges communs et les cas de bord. Augmentez vos compétences d'entrevue de codage. (en milliers de dollars)
- **Phrases clés:** *Solution LeetCode 2100*, *programmation dynamique préfixée*, *problème d'entrevue bancaire*, *Algorithme Java O(n)*, *Python suffix array*, *C++ prefix-suffix trick*, *stratégie de codage d'entrevue*.

Ajoutez ces phrases naturellement à vos titres et tout au long du post. Si vous hébergez l'article sur une plateforme de blog, ajoutez-les aux **tags** et **catégories**.

---

Dernier départ

- **Bien:** Technique de préfixe linéaire.
- **Bad:** Erreurs communes d'indexation et de comparaison.
- **Ugly:** Cas rares mais critiques (temps proche de la longueur du tableau, toutes valeurs égales).

Avec les trois extraits de code, vous pouvez déposer cette solution dans n'importe quel test d'entrevue ou de codage. Ajouter l'article à votre portfolio, le partager sur LinkedIn, ou même l'inclure dans votre GitHub README. La combinaison de **code de haute qualité** et **contenu convivial pour le référencement** vous aidera à vous démarquer des recruteurs à la recherche de côtelettes de résolution de problèmes.

Bon codage, et que votre prochaine interview se sente comme un *heist avec zéro victime*! C'est ce qu'il a dit