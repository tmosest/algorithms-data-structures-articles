---
titre: LeetCode 774. Minimiser la distance maximale jusqu'à la station-service -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. Minimiser la distance maximale jusqu'à la station-service
- Oui. C++ – Solutions complètes
### SEO-Optimized Blog Post: -Le bon, le mauvais, et le mauvais de LeetCode 774

---

Résumé du problème
On vous donne un **array de coordonnées des stations-service** sur l'axe des x ('stations', en augmentation stricte) et un entier `k' – le nombre de nouvelles stations que vous pouvez ajouter n'importe où (pas nécessairement à des positions entières).
Votre objectif est de minimiser la distance **maximum** entre deux stations consécutives après avoir ajouté exactement les nouvelles `k`.

Retourner la distance maximale minimale possible (`pénale`). Les réponses dans la colonne `10−6` sont acceptées.

> *Exemples*
> - « stations = [1,2,3,4,5,6,7,8,9,10], k = 9 → 0,5 '
> - `stations = [23,24,36,39,46,56,57,65,84,98], k = 1 → 14,0`

**Contrôles* *

Explication
C'est pas vrai.
1=10 <= stations.longueur <= 2000== Assez petite pour O(n log)=
2-0 <= stations[i] <= 108-
Jusqu'à un million de nouvelles stations

---

# # # Une perspective fondamentale

Nous pouvons **binaire-recherche** sur la réponse.
Pour un `mid` deviné (durée maximale autorisée), vérifiez si nous pouvons combler chaque écart initial avec au plus `k` de nouvelles stations de sorte que chaque sous‐gap ≤ `mid`.

*Si nous pouvons*, essayez un plus petit "mid".
* Si nous pouvons * nous avons besoin d'un "mid" plus grand.

Cela nous donne du temps `O(n log(maxGap)`, `O(1)` espace supplémentaire.

### Aide: `stationsNeeded(gap, mi)`
Nombre de nouvelles stations nécessaires pour diviser un écart de longueur en segments de taille ≤ mi:

«» "
requis = ceil(gap / mi) - 1
«» "

Le `-1` vient du fait qu'un écart de longueur `mid` a déjà besoin de 0 nouvelles stations.

---

Mise en œuvre du code

Voici des solutions propres et bien commentées dans **Java, Python et C++**. Chaque solution suit la même logique et a la même complexité temporelle et spatiale.

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
publique double minmax Stations GasDist(int[], int k) {
// Limite supérieure : le plus grand écart initial
double maxGap = 0;
pour (int i = 1; i < stations.longueur; i++) {
maxGap = Math.max(maxGap, stations[i] - stations[i-1]);
}

double gauche = 0, droite = maxGap;
Double EPS final = 1e-6; // tolérance de précision

pendant que (droite - gauche > EPS) {
double milieu = (gauche + droite) / 2,0;
si (canAchieve(stations, k, milieu)) {
droite = milieu; // essayer un écart maximum plus petit
} autre {
gauche = milieu; // besoin d'un écart plus grand
}
}
retour à gauche;
}

*** Contrôle de l'avidité: est-il possible de garder toutes les lacunes <= pénalité? */
booléen privé canAchieve(int[] stations, int k, double pénalité) {
int nécessaire = 0;
pour (int i = 1; i < stations.longueur; i++) {
écart double = stations[i] - stations [i-1];
// ceil(gap / pénalité) - 1 stations nécessaires
nécessaire += (int) Math.ceil(gap / pénalité) - 1;
si (nécessaire > k) retourner false; // sortie anticipée
}
retour vrai;
}
}
«» "

---

# # # # # #

'`python
de taper l'importation Liste
importer des maths

Solution de classe:
def minmax GasDist(self, stations: List[int], k: int) -> flotteur:
# Limite supérieure: espace maximum existant
max_gap = max(stations[i] - stations[i-1] pour i dans la plage(1, len(stations))

gauche, droite = 0,0, flotteur(max_gap)
eps = 1e-6

alors que droite - gauche > eps:
milieu = (gauche + droite) / 2,0
si self.can_achieve(stations, k, mi):
droite = milieu
Sinon:
gauche = milieu
retour à gauche

def can_achieve(self, stations: List[int], k: int, penalty: float) -> C'est vrai.
nécessaire = 0
pour i dans la plage (1, len(stations)):
écart = stations[i] - stations [i-1]
nécessaire += maths.ceil(gap / penalty) - 1
si nécessaire > k:
Retour Faux
retour Vrai
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
double minmax GazDist(vecteur<int>& stations, int k) {
double maxGap = 0;
pour (size_t i = 1; i < stations.size(); ++i)
maxGap = max(maxGap, static_cast<double>(stations[i] - stations[i-1]);

double gauche = 0, droite = maxGap;
Const double EPS = 1e-6;

pendant que (droite - gauche > EPS) {
double milieu = (gauche + droite) / 2,0;
si (canAchieve(stations, k, milieu))
droite = milieu; // essayer plus petit
Autre
gauche = milieu; // besoin plus grand
}
retour à gauche;
}

particulier:
bool canAchieve(vecteur const<int>& stations, int k, double pénalité) {
longue durée nécessaire = 0;
pour (size_t i = 1; i < stations.size(); ++i) {
écart double = stations[i] - stations [i-1];
nécessaire += static_cast<long long>(ceil(gap / penalty)) - 1;
si (nécessaire > k) retourner false; // sortie anticipée
}
retour vrai;
}
};
«» "

---

La complexité temporelle et spatiale

Langue Heure Espace
- C'est quoi ?
Java (O(n log(maxGap))"""O(1)" Autres
Python "O(n log(maxGap)") "O(1)" Autres
* C++ * O(n log(maxGap) * O(1) * Autres

*`n = stations.longueur`, `maxGap` ≤ 108. *

---

Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 774

Description de la méta
> Master LeetCode 774 – * Minimiser la distance maximale de la station-service*. Apprenez l'astuce de recherche binaire, voyez les solutions Java/Python/C++ propres, et comprenez les nuances algorithmiques que les intervieweurs aiment. Perfect your coded interview prep!

---

Introduction

Si vous préparez une entrevue d'ingénierie logicielle, vous avez probablement trébuché sur **LeetCode 774**: * Minimiser la distance maximale jusqu'à la station-service*.
C'est un problème classique **greedy + recherche binaire** qui teste:

- **Recherche binaire sur la réponse** (une technique puissante pour les domaines continus).
- **Dénombrement de la graisse** des stations insérées.
- Manipulation soigneuse de la précision du point flottant**.

Ci-dessous, nous disséquons le problème, traversons la solution optimale et montrons les implémentations en Java, Python et C++. Enfin, nous réfléchissons sur les aspects bons, mauvais, laids qui vous aideront à as interviews et à terre ce travail de rêve.

---

Récapitulation des problèmes

Vous avez reçu :

- `stations[]` – triées, augmentant strictement les positions sur l'axe des x.
- `k` – nombre de nouvelles stations que vous pouvez ajouter (toute coordination réelle).

**Objectif:** Ajouter exactement les nouvelles stations `k` de sorte que la distance maximale entre deux stations consécutives soit aussi petite que possible.
Retournez cette distance maximale minimale.

---

Pourquoi la recherche binaire sur la réponse fonctionne

La réponse (distance maximale) se situe entre `0` et l'écart initial le plus important.
Si un écart particulier est possible, un écart plus important sera également possible.
Cette **monotonicité** permet la recherche binaire:

Texte
faible = 0
haute = max (écart initial)

alors que haut - bas > EPS:
milieu = (faible + élevé) / 2
si possible (milieu): élevé = milieu
sinon: faible = milieu
«» "

Le seuil de précision `EPS = 1e-6` satisfait aux exigences du problème.

---

Contrôle de faisabilité – Le noyau de la graisse

Pour un candidat «mid»:

1. Pour chaque paire adjacente `(a, b)` calculer `gap = b - a`.
2. Nombre de nouvelles stations nécessaires à cet écart:
\[
nécessaire = \lceil \frac{gap}{mid} \rceil - 1
\]
Pourquoi ? *
Si on divise l'écart en sous-segments `x` de taille ≤ `mid`, on a besoin de nouvelles stations `x-1`.
`ceil(gap / mi)` donne le nombre minimal de segments nécessaires.

3. Somme «nécessaire» pour toutes les lacunes.
- Si < < Needed ≤ k > > , < < mi > > est faisable.
- Sinon, ça ne l'est pas.

La vérification se déroule dans **O(n)**, où `n` = `stations.longueur`.

---

Faits saillants de la mise en oeuvre

Mots clés Autres
C'est pas vrai.
**Java**=Utilise `Math.ceil` et le casting de type prudent à `double`. `canAchieve` sort tôt si `nécessaire > k`. Autres
**Python**"math.ceil" avec flotteurs; le retour précoce évite le travail inutile. Autres
**C++**="ceil(gap / penalty)" – les deux opérandes `double`. Utiliser `long` pour `nécessaire` pour éviter les débordements (bien que `k ≤ 1e6`). Autres

Les trois solutions partagent la même structure : boucle externe de recherche binaire + boucle intérieure gourmande.

---

Temps et espace

- **Heure**: "O(n log(maxGap)") " – trivial pour les contraintes d'entrevue.
- **Espace**: "O(1)" – mémoire supplémentaire constante.

---

Les bons – Ce que les intervieweurs aiment

1. **Elegant Binary Search on Answer** – vous montre comment réduire les espaces de recherche continue.
2. **Comptage de la graisse** – démontre que vous pouvez calculer les insertions minimales efficacement.
3. ** Manipulation de précision** – l'utilisation de la tolérance `1e-6` montre une attention aux nuances de point flottant.
4. **Clean Code** – des fonctions d'aide claires (« canAchieve ») et des commentaires aident les évaluateurs à lire votre logique.

---

Les mauvaises – Pièges communs

Piège
- Oui.
**Utilisation de la division entière** dans `ceil(gap / mi)` → mauvais résultat. Conversion des opérandes en "double". Autres
**Faux retour (si nécessaire > k); → gaspillé du temps pour le grand `k`. Autres
**Le seuil de précision de Wong** → peut afficher 0,499999 au lieu de 0,5. EPS. Autres
Autres **Calcul de l'écart** ('gap = stations[i] - stations[i-1]' mais oublier de lancer). S ' assurer que l ' écart est un double. Autres

---

## -- Les affreux – les cas de bord et les gotchas

1. **Large `k` (jusqu'à 1e6)** – convient toujours facilement parce que nous ne calculons qu'un nombre simple par écart.
2. **Très petites lacunes** – «ceil(gap / mi)» peut retourner 1, donc «nécessaire = 0».
3. **L'arrondi des points flottants** – `mid` peut être légèrement supérieur à l'optimum vrai; la recherche binaire s'arrête à `EPS', donc le résultat est dans la tolérance requise.
4. **Débordement entier** – pas un problème dans les contraintes données, mais être attentif dans les variantes où `k` ou `n` pourrait être plus grand.
5. **Toutes les stations sont déjà à la même distance** – le résultat sera 0, géré naturellement par la recherche binaire.

---

## -Envelopper – Comment se tenir dehors

- **Exposer la monotonicité** avant de plonger dans le code.
- **Afficher le raisonnement mathématique** pour "ceil(gap / mi) - 1".
- ** Mettre en évidence la précision** et pourquoi `1e-6` suffit.
- **Mention approches alternatives** (par exemple, programmation dynamique, file d'attente prioritaire) mais justifier pourquoi la recherche binaire + cupidité est optimale.

Ces points de discussion illustrent la profondeur de la compréhension et des compétences en communication – exactement ce que les recruteurs recherchent.

---

Les pensées finales

LeetCode 774 peut sembler intimidant à première vue, mais une fois que vous maîtrisez la recherche *binaire sur le modèle de réponse*, la solution tombe en place.
La mettre en œuvre dans votre langue de choix (Java, Python, C++) et expliquer les compromis algorithmiques vous montre que vous êtes prêt pour les problèmes *real-world* que testent les intervieweurs.

Bon codage, et bonne chance pour votre prochaine entrevue – votre rôle d'ingénierie logicielle de rêve est juste une recherche binaire loin! C'est ce qu'il a dit.

---

Liste de contrôle à emporter

- La boucle externe de recherche binaire avec `EPS = 1e-6`.
- Nombre d'avidités par écart ('ceil (gap / mi) - 1').
- Sortie anticipée lorsque « nécessaire > k ».
- C'est correct.
- Fonctions d'aide claires et commentées.

Vérifiez tout, et vous impressionnerez n'importe quel gestionnaire d'embauche.

---

Joyeux entretien !

---

**Auteur:** *[Votre nom]* – Coding interview coach, passionné de Java/Python/C++, et ancien interviewé qui a transformé le laideur en offres d'emploi.

---

* Fin de l'article. *



---

** Prêt pour votre prochain entretien? **
Téléchargez les extraits de code propres ci-dessus, passez à travers les cas de test, et se sentent confiants. Bonne chance !