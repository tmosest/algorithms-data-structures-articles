---
titre: LeetCode 2071. Nombre maximum de tâches que vous pouvez attribuer -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2071 – **Nombre maximum de tâches que vous pouvez attribuer**
> **Difficulté**: dur
> **Tags**: Greedy, Recherche binaire, Deux-Pointeurs, Tri

### TL;DR
- Trier les "tâches" (ascendant) et les "travailleurs" (ascendant).
- Recherche binaire de la réponse (`mid` = nombre de tâches que vous essayez de satisfaire).
- Pour chaque "mid" faire un contrôle avide *can-assign* :
1. Essayez de satisfaire la tâche la plus difficile avec le travailleur le plus fort non entraîné.
2. Si le travailleur n'est pas assez fort, voir si un travailleur plus faible peut être boosté avec une pilule (et nous avons encore des pilules).
3. Si aucun travailleur (avec ou sans pilule) peut gérer la tâche → `mid` est impossible.
- La plus grande réponse possible est la "mid".

L'algorithme fonctionne dans le temps `O(n+m) log(min(n,m)) + n log n + m log m)` et `O(n+m)` espace supplémentaire.



---

Code idiomatique complet

Java (Java 17)

"Java
Importation de java.util.*;

solution de classe {
int public maxTaskAssign(int[] tâches, int[] travailleurs, pilules int, force int) {
int n = tâches.longueur, m = travailleurs.longueur;
lo = 0, hi = Math.min(n, m);

Tableaux.sort(tâches); // ascendant
Arrays.sort(travailleurs); // ascendant

pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi + 1) >>> 1; // nombre de tâches du candidat
i (peut-être attribuer (tâches, travailleurs, milieu, pilules, force)) {
lo = mi; // mi est faisable → rechercher plus haut
} autre {
hi = milieu - 1; // milieu trop haut → recherche inférieure
}
}
retour lo;
}

Le booléen privé peut assigner(int[] les tâches, int[] les travailleurs,
taskCoupe, pilules int, force int) {
tw = travailleurs.longueur - 1; // indice du travailleur libre le plus fort
int freePills = pilules; // pilules restantes

// Travailler de la tâche la plus difficile à la plus simple
pour (int t = taskCount - 1; t >= 0; --t) {
difficulté int = tâches[t];

Préférez un travailleur sans pilule
si (w >= 0 && travailleurs[w] >= difficulté) {
w--; // consommer ce travailleur
poursuivre;
}

(Si nous avons encore des pilules)
// Nous cherchons le travailleur le plus faible* qui peut être augmenté pour satisfaire
// la tâche actuelle. Parce que les deux tableaux sont triés ascendants,
// tout travailleur satisfaisant `travailleur + force >= difficulté "
// doit être *pas plus fort* que le travailleur actuel que nous balayons.
// Donc nous balayons à l'envers jusqu'à ce qu'on frappe un travailleur qui, après boost,
// rencontre la difficulté.
pendant que (w >= 0 && travailleurs[w] + force >= difficulté) {
// Poussez ce travailleur dans une file d'attente de travailleurs "boostés"
// (ils seront sautés plus tard si nous manquons de pilules)
// Nous utiliserons une structure semblable à une pile pour garder l'ordre.
// Utiliser un tableau d'entrée simple comme pile ici est suffisant.
si (freePills) 0) {
// Aucune pilule restant → impossible
retourner faux;
}
// Utilisez une pilule sur ce travailleur
"pills libres";
// Ce travailleur peut maintenant gérer la tâche, donc la consommer
W--;
pause;
}

// Si nous atteignons ici, la tâche actuelle ne peut être satisfaite
// avec toute autre combinaison travail/pill
si (w < 0 & & freePills) 0) {
retourner faux;
}
}

retour vrai;
}
}
«» "

> **Pourquoi cette version Java fonctionne-t-elle? * *
> 1. La routine `canAssign` est **O(taskCount)** parce que nous marchons une fois sur les travailleurs les plus forts et utiliser un guichet simple pour les pilules.
> 2. La recherche binaire externe exécute des temps `log(min(n,m)`, donnant la complexité globale.

---

Python (Python 3.10+)

'`python
Solution de classe:
def maxTaskAssign(self, tâches: List[int], workers: List[int],
pilules: int, force: int) -> Int:
tâches.sort()
travailleurs.sort()

lo, hi = 0, min(tâches), len(travailleurs)

alors que:
milieu = (lo + hi + 1) // 2
si self._can(tâches, travailleurs, pilules, force, milieu):
lo = mi # les tâches mi sont réalisables
Sinon:
hi = milieu - 1 # milieu trop ambitieux
retour lo

def _can(self, tâches, travailleurs, pilules, force, tâche_cnt):
"""Retourne Vrai si nous pouvons terminer les tâches `task_cnt`."""
w = len(travailleurs) - 1 # travailleur le plus fort disponible
_pills gratuits = pilules

# Itérer du plus dur au plus facile des tâches sélectionnées
pour t dans l'intervalle(task_cnt - 1, -1, -1):
requis = tâches[t]

# 1. Utilisez un travailleur non entraîné si nous en avons un
si w >= 0 et travailleurs[w] >= requis:
-= 1
poursuivre

2. Essayez de trouver un travailleur plus faible que nous pouvons stimuler
# (scane à l'envers alors que le travailleur stimulé satisfait encore la tâche)
pendant que w >= 0 et travailleurs[w] + force >= requis:
-= 1
_pills libres -= 1
si _pills libres < 0:
Retour Faux

# Si nous manquons de travailleurs ou de pilules, mission impossible
si w < 0 et free_pills < 0:
Retour Faux

retour Vrai
«» "

> **Pourquoi cette version Python est élégante* *
> *Pas de multiset ou de tas explicite – nous marchons juste les deux tableaux triés une fois. *

---

C++ (C++20)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxTaskAssign(vecteur<int>&tâches, vecteur<int>&travailleurs,
pilules int, force int) {
tri(tasks.begin(), tasks.end());
tri(workers.degin(), workers.end());

int lo = 0, hi = min(tasks.size(), workers.size());

pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi + 1) / 2;
i (peut-être attribuer (tâches, travailleurs, milieu, pilules, force)) {
lo = milieu;
} autre {
hé = milieu - 1;
}
}
retour lo;
}

particulier:
bool canAssign(vecteur const<int>& les tâches, le vecteur const<int> et les travailleurs,
int taskCnt, pilules int, force int) {
int w = (int)workers.size() - 1; // indice du travailleur le plus fort
int freePills = pilules;

// Il faut passer de la tâche la plus difficile à la tâche la plus facile parmi les "taskCnt" sélectionnés
pour (int t = taskCnt - 1; t >= 0; --t) {
int requis = tâches[t];

// Utilisez un travailleur sans pilule si assez fort
si (w >= 0 && travailleurs[w] >= requis) {
--w;
poursuivre;
}

// Sinon nous devons utiliser une pilule sur un travailleur plus faible
// Trouvez le travailleur *faible* qui, après avoir augmenté, peut faire la tâche.
// Puisque les travailleurs sont triés ascendants, le prochain candidat est les travailleurs[w].
// Nous cherchons un tel travailleur.
pendant que (w >= 0 && travailleurs[w] + force < requise) {
--w; // ce travailleur ne peut même pas être augmenté
}
si (p < 0.) 0) retourner faux; // aucun travailleur n'est parti

// Boostez ce travailleur et consommez une pilule
--w;
--piles libres;
}
retour vrai;
}
};
«» "

> **Pourquoi cette version C++ est rapide* *
> La vérification cupide se déroule dans `O(taskCnt)` et les boucles de recherche binaire `O(log(min(n,m))` times – parfaitement acceptable pour `n,m ≤ 2·105`.

---

Article du blog – Des pilules à la productivité : Mastering LeetCode 2071

> **Cible auprès du public**: Ingénieurs logiciels, passionnés de préparation d'entretien, recruteurs
> **Mots clés**: LeetCode 2071, attribution de tâches, recherche binaire, algorithme gourmand, préparation d'entrevue, entretien de codage, résolution de problèmes, entretien d'emploi, ingénieur logiciel

---

C'est pas vrai. Le problème en coque

> *Vous êtes donné `tasks` (niveaux difficiles) et `workers` (force).
> Un travailleur peut faire une tâche si sa force ≥ difficulté.
> Vous avez également un nombre limité de pilules (`pills`) qui ajoutent temporairement `force` à un travailleur.
> Quel est le nombre maximum de tâches que vous pouvez accomplir? *

---

- Oui. Pourquoi ce problème est - il difficile?

Aspect Pourquoi il est difficile
C'est-à-dire
Vous devez jongler avec trois variables : tâches, travailleurs, pilules. Une simple cupidité, assigner le travailleur le plus fort à la tâche la plus difficile, peut échouer parce que vous pourriez gaspiller une pilule sur un travailleur faible quand un travailleur plus fort aurait pu faire le travail sans boosté. Autres
**Décisions non-monotoniques**= Une décision qui semble bonne localement (démarrer le travailleur le plus faible) pourrait bloquer une meilleure affectation mondiale. Autres
**Grande entrée** Les approches Brute-force qui tentent tous les sous-ensembles sont impossibles. Autres

---

C'est vrai. La bonne vieille approche naïve

> *Trier les travailleurs qui descendent, trier les tâches qui descendent, puis pour chaque tâche, choisir le premier travailleur qui peut le gérer (en boostant si nécessaire). *
> Cela échoue parce que vous pourriez consommer une pilule sur un travailleur qui pourrait autrement être jumelé à une tâche ultérieure, tandis qu'un travailleur plus fort est laissé inactif.

---

C'est pas vrai. Analogie du monde réel

Pensez à une équipe de logiciels.
Vous avez un ensemble de **caractéristiques** (tâches) et un ensemble de **développeurs** (travailleurs).
Vous avez un nombre limité de ** heures de mentorat** (`pills`) qui peuvent temporairement augmenter les connaissances d'un développeur junior (`force`).
Si vous assignez le mentorat au développeur le moins expérimenté sur une fonctionnalité qu'un senior pourrait avoir fait, vous perdez peu de temps de mentorat, potentiellement manquant sur des projets plus grands.

---

C'est pas vrai. La solution élégante : recherche binaire + vérification de la graisse

4.1 Aperçu conceptuel

1. **Trier** les deux tableaux – cela nous donne de l'ordre pour les décisions gourmandes.
2. **Recherche binaire** la réponse: Si vous pouvez terminer les tâches `mid`, essayez plus; sinon, essayez moins.
3. **Vérification de faisabilité** – pour chaque tâche (plus difficile → plus facile), choisir le travailleur le plus fort qui peut le faire. Sinon, cherchez un travailleur plus faible qui peut être stimulé.
4. **Arrêtez quand** vous touchez une tâche qui ne peut pas être satisfaite → `mid` est impossible.

##### 4.2 L'Assignation Can-Adhérent

> **Pourquoi ça marche**:
> Nous traitons les tâches en difficulté décroissante; cela garantit que lorsque nous considérons une tâche, tout travailleur qui est parti après la boucle est soit *trop faible* ou *déjà assigné*.
> En choisissant d'abord l'ouvrier *le plus fort*, nous évitons d'aller trop loin.
> Si nous devons utiliser une pilule, nous choisissons le travailleur *faible* qui peut être boosté – cela conserve les pilules pour les tâches ultérieures.

4.3 Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Tri des "tâches", des "travailleurs" Autres
Recherche binaire Autres
Contrôle de l ' avidité Autres

Total: temps `O(n+m) log(min(n,m))`, espace `O(n+m)`.

---

C'est vrai. Pièges à éviter

1. **Musreading the monotonicity** – en supposant que stimuler le travailleur le plus faible est toujours le meilleur.
2. **Utiliser un tas pour le multiset quand il n'est pas nécessaire** – augmente les facteurs constants.
3. ** Erreurs hors-par-un** – rappelez-vous que la recherche binaire utilise `(lo + hi + 1) / 2` pour éviter les boucles infinies.

---

- Oui. Tâches clés pour l'entrevue

Conseil Explication
C'est pas vrai.
**Découvrez votre intuition **Découvrez pourquoi une cupidité naïve échoue, puis expliquez comment la recherche binaire + cupidité résout le problème. Autres
**Discuse la complexité à l'avance**=Les recruteurs aiment les arguments de complexité concis. Autres
**Afficher l'équivalence**Démontrer que le contrôle avide peut être mis en œuvre en plusieurs langues (Java, Python, C++). Autres
**Relat to real-world scenarios**= Dessiner des parallèles à la gestion des produits, à l'allocation des ressources ou même à l'optimisation de la posologie des médicaments. Autres

---

Pratique, pratique, pratique

- **LeetCode**: 2071 – *Tâche avec pilules*
- **Hard** – mais solvable avec une stratégie **binaire-recherche + gourmande**.
- **Conseils**: Écris des cas bord, lance une trace à la main, puis traduit ton raisonnement en code propre.

---

- Oui. Mot final

> *LeetCode 2071 est plus qu'un défi de codage ; c'est une leçon d'optimisation des ressources.
> La maîtrise vous donne non seulement confiance pour les entrevues, mais elle aiguise également votre pensée pour les problèmes d'ingénierie réels où vous devez équilibrer les ressources limitées par rapport aux charges de travail exigeantes. *

Bonne chance, et que vos pilules soient toujours utilisées sagement! C'est ce qu'il a dit.



---



Enveloppe

* Vous disposez maintenant de trois solutions prêtes à la production (Java, Python, C++).
* L'article explique pourquoi le problème est difficile et comment articuler la solution dans un contexte d'entrevue.
* Prêt à impressionner les recruteurs? Montrez-leur l'astuce de la productivité de la pile! Les

---



---

> *Si vous voulez plus d'informations ou une plongée plus profonde dans la stratégie de recherche cupide-vers-binaire, laissez un commentaire ou DM moi. Bon codage ! *