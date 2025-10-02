---
titre: LeetCode 3648. Capteurs minimaux pour couvrir la grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3648. Capteurs minimums pour couvrir la grille – LeetCode – One-liner, O(1) Solution

Ci-dessous vous trouverez **ready‐to-colle code** dans **Java, Python, et C++** qui résout le problème en temps constant.
Après le code, vous trouverez un billet de blog **SEO-optimisé** qui explique l'intuition, les pièges (-) et comment cette technique d'interview peut vous aider à décrocher ce prochain emploi.

---

- Oui. 1. Recap du problème LeetCode

** Problème* *
> Compte tenu d'une grille `n × m` et d'un entier `k`, un capteur placé à `(r, c)` couvre chaque cellule dont la distance **Chebyshev** à `(r, c)` est au plus `k`.
> Retourner le nombre minimum de capteurs** requis pour couvrir toute la grille.

**Distance de Chebyshev** = `max(=r1-r2=" ,="c1-c2=") ' – la distance de ="king=" sur un échiquier.

---

- Oui. 2. Aperçu d'une ligne

*Chaque capteur couvre un carré de côté «2k + 1». *
Si nous posons des capteurs sur une grille régulière avec espacement `2k + 1`, nous ne gaspillons jamais la couverture.
Ainsi, le nombre minimum de capteurs est simplement:

«» "
Ceil(n / (2k+1)) * ceil(m / (2k+1))
«» "

"ceil(x)" peut être calculé avec le calcul entier: `x / taille + (x % taille > 0 ? 1 : 0)`.

---

- Oui. 3. Code – Java / Python / C++

#### 3.1 Java

"Java
solution de classe {
Int public int minSensors(int n, int m, int k) {
taille int = 2 * k + 1; // côté du carré de couverture
int horiz = n / taille + (n % taille > 0 ? 1 : 0);
int vert = m / taille + (m % taille > 0 ? 1 : 0);
retour horiz * vert;
}
}
«» "

3.2 Python

'`python
Solution de classe:
def minSensors(self, n: int, m: int, k: int) -> Int:
taille = 2 * k + 1
horiz = n // taille + (1 si n % autre taille 0)
vert = m // taille + (1 si m % taille autre 0)
retour horiz * vert
«» "

### 3.3 C++

'`cpp
solution de classe {
public:
int minSensors(int n, int m, int k) {
taille de l ' int = 2 * k + 1;
int horiz = n / taille + (n % taille ? 1 : 0);
int vert = m / taille + (m % taille ? 1 : 0);
retour horiz * vert;
}
};
«» "

Les trois extraits se déroulent dans le temps **O(1)** et la mémoire **O(1)**.

---

- Oui. 4. Article du blog – Le bon, le mauvais, et le mauvais de Grid-Covering Capteurs

### 4.1 Titre (optimisé par le référencement)

> Les capteurs minimums pour couvrir la grille – la solution O(1) dont tout le monde a besoin pour le LeetCode & Interviews

Description de la méta

> Résolvez le LeetCode 3648 en une seule ligne. Apprenez la stratégie gourmande, écueils à éviter, et pourquoi cette astuce de détection de grilles brille dans les interviews de codage. Améliorez vos compétences en algorithme pour les rôles technologiques.

4.3 Introduction

Dans les interviews de codage, on vous demande souvent de couvrir un tableau, un graphique ou un tableau 2-D avec les moins de pièces.
LeetCodes **3648 – Capteurs minimums pour couvrir la grille** est un exemple de manuel: un capteur couvre une surface carrée, et nous devons minimiser le nombre.

L'astuce est simple mais puissante : ** Traiter le problème comme un carrelage de carrés**.
Ci-dessous, je vous marche à travers l'intuition, les cas de bord, les erreurs communes (les ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 4.4 Énoncé du problème (Points de Bulletin)

* Dimensions de la grille: `n × m` (1 ≤ n, m ≤ 103).
* Rayon de couverture du capteur: `k` (0 ≤ k ≤ 103).
* Distance de Chebyshev = `max(==Δrow,==Δcol)` – comme un roi des échecs.
* Retour ** Capteurs minimum** nécessaires pour couvrir chaque cellule.

#### 4.5 Le bon: Pourquoi le tiling de la place Greedy fonctionne

1. ** Forme de couverture* *
Un capteur à `(r, c)` couvre un carré centré sur cette cellule avec un côté «2k + 1».
Considérez chaque capteur comme un "tile" de cette taille fixe.

2. **Optimalité de l'espacement régulier**
Si nous mettons des capteurs de sorte que leurs centres sont exactement "2k + 1" cellules séparées horizontalement et verticalement, les tuiles touchent (pas de trous, pas de chevauchement inutile).
Tout autre placement laisserait des lacunes ou créerait des chevauchements inutiles.

3. **Formule mathématique**
* Tuiles horizontales nécessaires*: "ceil(n / (2k+1)) "
* Tuiles verticales nécessaires*: "ceil(m / (2k+1)) "
Multipliez → capteurs totaux.

4. **Pourquoi c'est O(1)* *
Nous ne faisons que quelques opérations arithmétiques et quelques divisions entières.

4.6 Les mauvaises: pièges communs

Pourquoi il fait défaut Exemple
- C'est quoi ?
**Utiliser `n / size` sans plafond**= La division entière tronque.== `n = 5, size = 3 → 1` au lieu de `2`. Autres
**En supposant que les capteurs peuvent être placés à l'extérieur de la grille** Il est illégal de placer un capteur à (-1, -1). Autres
**Ajout de capteurs inutilement** Mettre des capteurs sur chaque cellule lorsque `k=0`. Autres
**Mixer les lignes et les colonnes** , `ceil(m / size)` vs `ceil(n / size)` échangé → mauvais produit. Autres

### 4.7 L'horrible : trop compliqué Approches

Certaines solutions tentent de simuler le placement, le BFS ou d'utiliser une programmation dynamique.
On y ajoute :

* **O(n m)** ou **O(n+m) log(n+m)** complexité – inutile pour un simple problème de mathématiques.
* Beaucoup de manipulation de cas de bord (couverture partielle aux frontières, contrôles recoupants).
* Plus de chances de bugs et plus de temps d'entrevue.

> **Ligne de bottom**: La simplicité est l'élégance. Une réponse arithmétique d'un liner est la réponse des recruteurs de code « clean ».

### 4.8 Code Passage à pied (Java, Python, C++)

(Insérer les blocs de code de la section 3 ici, chacun dans un bloc de code clôturé séparé.)

> **Astuce**: Dans les interviews, toujours expliquer la formule d'abord, puis montrer comment vous implémentez "ceil` en entier maths. Les recruteurs apprécient la clarté.

4.9 Analyse de la complexité

* **Heure**: «O(1)» – opérations constantes, indépendamment de la taille de la grille.
* **Espace**: "O(1)" – seulement quelques variables entières.

#### 4.10 Cas de bord à tester

Nombre de capteurs attendus
-- -- -- -- -- -- -- -- -- --
C'est la première fois que l'on s'en occupe.
Dénomination des marchandises
- Oui.
1 000 000 000 000
1 000 000 000 000 500 000 1 000

### 4.11 Comment cela aide votre recherche d'emploi

* **Interview Impact**: montre que vous pouvez identifier un motif gourmand et le convertir en mathématiques.
* ** Style de codage** : Code propre et concis – exactement ce que les recruteurs attendent.
* **Breadth algorithmique**: Les problèmes d'inclinaison et de couverture apparaissent dans de nombreux scénarios réels (p. ex., réseaux de capteurs, couverture Wi-Fi).
* **Portfolio**: Ajoutez cette solution à votre GitHub avec un court README – une vitrine rapide des compétences en résolution de problèmes.

4.12 Conclusion et prochaines étapes

> Le problème **Capteurs Minimum à Cover Grid** est une classe de micro-master en transformant la géométrie en arithmétique.
> Rappelez-vous : recherchez toujours l'abstraction *tiling* ou *covering* ; elle mène souvent à une solution `O(1)` ou `O(log n)`.
> Continuez à pratiquer des problèmes similaires de couverture (p. ex., nombre minimum de lumières pour couvrir un couloir) et vous serez prêt à l'entrevue en un rien de temps.

---

### 4.13 Appel à l'action

Autres **Essayez-le vous-même**: Copiez le code dans votre IDE préféré, exécutez les exemples, puis défiez-vous avec les cas de bord.
> * Partager** vos résultats sur LinkedIn ou GitHub et me tag – J'aimerais voir votre implémentation!
** Bonne chance** sur votre prochaine interview – vous avez obtenu la bonne intuition algorithmique.

---

* Fin de l'article. *