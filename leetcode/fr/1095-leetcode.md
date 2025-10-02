---
titre: LeetCode 1095. Trouver dans Mountain Array -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 1095 – Trouver dans la station de montagne
**Traitement**

> Si vous êtes à la recherche d'une solution d'interview solide dans **Python, Java ou C++**, vous êtes au bon endroit.
> Ci-dessous vous trouverez:
> * Une explication claire et pas à pas qui s'attaque au bon, au mauvais et au mauvais*.
> * Extraits de code en plein fonctionnement dans **Python, Java et C++** qui respectent la limite d'appel de 100‐`get()‘.
> * Un mini-blog optimisé pour le référencement (mots clés, titres, méta-style copie) qui peut doubler en tant que poste de portefeuille sur LinkedIn ou Medium.

> **TL;DR** – Trouvez d'abord le pic, puis la recherche binaire la partie croissante (retourner tôt si trouvé), sinon la recherche binaire la partie décroissante.

---

- Oui. 1. Récapitulation des problèmes

> Un tableau *montagne* est une séquence qui augmente strictement à un seul pic, puis diminue strictement.
> Vous n'êtes autorisé à lire le tableau que via l'interface `MountainArray`:
> ```texte
> int get(index d'int);
> longueur int();
> `` "
> Le but : **retourner le plus petit indice `i` de telle sorte que `get(i) == cible`, ou `-1` si la cible est manquante. **
> **Important:** Ne **pas** faire plus de **100** appels à `get`.

Contraintes:
* `3 ≤ montagne ≤ 104 "
* `0 ≤ cible, montagneArr.get(i) ≤ 106 "

---

- Oui. 2. Le bon, le mauvais et le mauvais des recherches d'images de montagne

**Quoi faire**
Il n'y a pas de lien entre les deux.
Utiliser une recherche binaire qui compare `mid` et `mid+1`. Effectuer un balayage linéaire ou appeler à plusieurs reprises `get` dans une boucle sans tailler. Autres
**Augmentation de la recherche en partie** Val → gauche = milieu + 1 '). Autres
*Décreasing-Part Search**= Inverser les mouvements de pointeur (`cible > miVal → droite = mi-1`).= Oubliez que `mid` est déjà `-1` ou `0` et gardez toujours `gauche ≤ droite`. Autres
*Compte d'appel** au minimum en réutilisant la longueur du tableau et en appelant `get` seulement deux fois par comparaison. Appeler `get` sur le même index plusieurs fois ou appeler un helper qui boucle le tableau. Autres
**Edge-Cases**= Vérifiez que la « cible » peut être au sommet. Supposons que le tableau augmente ou diminue toujours. Autres
**Tests**=Vérifier avec les parties ascendantes et descendantes. Passer l'indice le plus petit* requis – retourner le premier trouvé au lieu du plus bas. Autres

---

- Oui. 2. Aperçu de l'algorithme

1. **Obtenez la longueur du tableau** une fois: `n = montagneArr.longueur()`.
2. **Trouver l'index pic (`p`)** – recherche binaire avec la règle `get(mid) < get(mid+1)` → déplacer à droite; sinon → déplacer à gauche.
3. **Rechercher la partie ascendante `[0 ... p]`** avec recherche binaire normale.
* Si trouvé → retourner l'index immédiatement (garanti plus petit).
4. **Rechercher la partie descendante `[p+1 ... n-1]`** avec une recherche binaire inversée.
5. Retourner le résultat (ou `-1` si non trouvé).

Le budget de l'appel est bien inférieur à 100:
* `peak` a besoin au plus `log2(104) 14` itérations → environ `28` appels (`get(mid)` et `get(mid+1)` chaque itération).
* Chaque recherche binaire nécessite au plus des appels `14` → deux autres recherches vous maintiennent toujours dans la limite de 100 appels.

---

- Oui. 3. Analyse de la complexité

**Métrique**
C'est quoi, ça ?
Temps **O(log n)** – une recherche de pointe + au plus deux recherches binaires. Autres
Espace **O(1)** – pas de structures de données supplémentaires, juste quelques variables entières. Autres

---

- Oui. 4. Échantillons de codes complets

> Les extraits suivants sont prêts à être collés dans l'éditeur LeetCode (il suffit de remplacer la `solution de classe` existante).
> Chacun honore la restriction d'appel 100‐`get()‘ et utilise l'interface exactement comme LeetCode s'y attend.

4.1 Python 3

'`python
# Définition pour MountainArray.
# classe MountainArray:
# def get(self, index: int) -> Int:
# def length(self) -> Int

Solution de classe:
def findInMountainArray(self, cible: int, month_arr: 'MountainArray') -> Int:
n = longueur de la montagne()

Aide : recherche binaire - Oui.
def binaire_search(gauche: int, droite: int, cible: int, ascendant: bool) -> Int:
alors que gauche <= droite:
milieu = (gauche + droite) // 2
mid_val = montagne_arr.get(mid)

if mi_val == cible & #160;:
retour

si ascendant: # logique ascendante normale
si cible > _virgule :
gauche = milieu + 1
Sinon:
droite = milieu - 1
sinon : # inversé pour la partie descendante
si cible > _virgule :
droite = milieu - 1
Sinon:
gauche = milieu + 1
retour -1

# -------- aide: trouver le pic ---------
def find_peak() -> Int:
l, r = 0, n - 1
alors que l < r:
milieu = (l + r) // 2
On n'a besoin que de deux personnes.
Si mountain_arr.get(mid) < mountain_arr.get(mid + 1):
l = milieu + 1 # pic est à droite
Sinon:
r = le pic moyen est au milieu ou à gauche
retour l

pic = find_peak()

N° 1 Rechercher la partie ascendante d'abord
idx = binaire_search(0, pic, cible, ascendant=True)
Si idx != - 1 :
retourner idx

N° 2 Si elle n'est pas trouvée, recherchez la partie descendante
retour binaire_search(peak + 1, n - 1, cible, ascendant=False)
«» "

> **Pourquoi ça marche* *
> *Le pic est le point de pivot où le tableau change de direction.
> En cherchant d'abord la partie ascendante, nous garantissons l'indice *le plus petit* si la cible apparaît avant le pic.
> La recherche binaire inversée sur le côté descendant fonctionne parce que les éléments sont strictement décroissants. *

---

#### 4.2 Java

"Java
***
* C'est l'interface que LeetCode nous donne. Dans les
* problème que vous n'avez pas besoin de mettre en œuvre – il est fourni.
*/
interface MountainArray {
int get(index d'int);
longueur int();
}

solution de classe {

public int findInMountainArray(int cible, MountainArray mountainArr) {
int n = montagneLongueur arr.();

// --------- aide: recherche binaire - Oui.
// ascendant = true → recherche binaire normale
// ascendant = faux → inversé (partie descendante)
Java.util.fonction. BiFunction<entier, entier, entier> ascSearch =
(à gauche, à droite) -> {
int l = gauche, r = droite;
pendant que (l <= r) {
Int milieu = (l + r) >>> 1;
int midVal = montagneArr.get(mid);
si (midVal) la cible revient au milieu;
si (cible > miVal) l = milieu + 1;
r = milieu - 1;
}
retour -1;
};

Java.util.fonction. BiFunction <entier, entier, entier> descSearch =
(à gauche, à droite) -> {
int l = gauche, r = droite;
pendant que (l <= r) {
Int milieu = (l + r) >>> 1;
int midVal = montagneArr.get(mid);
si (midVal) la cible revient au milieu;
si (cible > milieu Val) r = milieu - 1; // inversé
autrement l = milieu + 1;
}
retour -1;
};

// --------- trouver le pic - Oui.
Int l = 0, r = n - 1;
pendant que (l < r) {
Int milieu = (l + r) >>> 1;
si (montagneArr.get(mid) < montagneArr.get(mid + 1)) {
l = milieu + 1; // pic est à droite
} autre {
r = milieu; // le pic est au milieu ou à gauche
}
}
pic int = l;

// -------- partie ascendante - Oui.
int idx = ascSearch.apply(0, pic);
Si (idx != -1) retourner idx;

// ---------- Recherche en partie descendante - Oui.
retour descSearch.apply(peak + 1, n - 1);
}
}
«» "

> ** Points clefs**
> * `>>> 1` est un poste droit non signé – plus rapide que `/ 2`.
> * `BiFunction` est utilisé pour la brièveté; vous pouvez également extraire des méthodes d'aide privées si vous préférez.
> * Les appels de recherche de pointe `get` deux fois par boucle (`mid` et `mid+1`), mais les appels globaux restent bien inférieurs à 100.

---

### 4.3 C++

'`cpp
***
* C'est l'interface que LeetCode nous donne. Dans les
* problème que vous n'avez pas besoin de mettre en œuvre – il est fourni.
*/
classe MountainArray {
public:
int virtuel get(int index) const = 0;
longueur int virtuelle () const = 0;
};

solution de classe {
public:
int findInMountainArray(int cible, MountainArray &mountainArr) {
int n = montagneLongueur arr.();

// ------- recherche binaire (croissante ou descendante) -------
auto binaireSearch = [&](int gauche, int droite, bool ascendant) -> Int {
pendant que (gauche <= droite) {
int milieu = gauche + (droite - gauche) >> 1);
int midVal = montagneArr.get(mid);

si (midVal) la cible revient au milieu;

si (croissant) { // ascendant normal
si (cible > milieu Val) gauche = milieu + 1;
autre droite = milieu - 1;
} autre { // inversé pour la partie descendante
si (cible > milieu Val) droite = milieu - 1;
autre gauche = milieu + 1;
}
}
retour -1;
};

// -------- trouver le pic (indice de l'élément maximal) -------
Int l = 0, r = n - 1;
pendant que (l < r) {
int milieu = l + ((r - l) >> 1);
si (montagneArr.get(mid) < montagneArr.get(mid + 1))
l = milieu + 1; // pic est à droite
Autre
r = milieu; // pic au milieu ou à gauche
}
pic int = l;

// ------- recherche la partie ascendante d'abord -------
int idx = binaireSearch(0, pic, true);
Si (idx != -1) retourner idx;

// ------- sinon trouvé, recherchez la partie descendante - Oui.
retour binaire Recherche (peak + 1, n - 1, false);
}
};
«» "

> **Notes**
> * La lambda capture `montainArr` par référence et fonctionne avec des variables `int` uniquement.
> * C++ utilise `>> 1' (déplacement) pour éviter la division.
> * La recherche de pointe utilise `get(mid)` et `get(mid+1)` – tout comme la version Java.

---

- Oui. 5. Liste de contrôle avant la soumission

- [ ] Remplacer la « solution de classe » existante par l'extrait de langue spécifique ci-dessus.
- [ ] Aucune fonction supplémentaire d'aide qui scanne le tableau entier.
- [ ] Exécutez les cas de test LeetCode fournit.
- [ ] Vérifiez que la réponse est **le plus petit** indice (pas n'importe quel événement).
- [ ] Assurez-vous que votre code est compilé dans l'environnement donné (utilisez `#include <bits/stdc++.h>` si nécessaire dans C++).

---

- Oui. 6. Conclusion

> LeetCodes **Find in Mountain Array** est un excellent exercice pour appliquer correctement la recherche binaire à une mise en page de données non triviales.
> La clé est de reconnaître le changement de direction* (en pointe) et d'inverser les mouvements des pointeurs pour la partie descendante.
> En comptant soigneusement `get()` vous appelle confortablement en dessous de la limite de 100 appels.

Bonne chance, et profitez de casser la montagne! C'est vrai.

---

*Si vous trouvez ce guide utile, s'il vous plaît donner le problème de LeetCode une note – il aide les autres à apprendre le bon modèle. *