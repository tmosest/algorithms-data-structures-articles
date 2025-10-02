---
titre: LeetCode 2594. Temps minimum pour réparer des voitures -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – Temps minimum pour réparer les voitures

**LeetCode 2594 – Temps minimum de réparation des voitures* *
> *Moyenne

On vous donne `ranks[]`, le rang de chaque mécanicien, et un entier `cars` qui indique combien de voitures doivent être réparées.
Un mécanicien avec rang `r` a besoin de `r × n2` minutes pour réparer `n` voitures.
Tous les mécaniciens peuvent fonctionner ** simultanément** et nous voulons le temps **minimum** requis pour terminer toutes les "voitures".

Exemple
C'est pas vrai.
Le temps minimum est de 16 minutes.
"Ranks = [5,1,8]", "cars = 6"

Contraintes
- "1 ≤ grades.longueur ≤ 105 "
- `1 ≤ grades[i] ≤ 100`
- "1 ≤ voitures ≤ 106 "

La limite de temps est serrée – une simulation **brute-force** ne se terminera pas à temps.

---

- Oui. 2. Idée de solution – Recherche binaire dans le temps

Le problème est un modèle classique de recherche binaire.

* Pour une durée fixe `t` nous pouvons demander: ** Combien de voitures peuvent tous réparer ensemble? * *
*Un mécanicien avec rang `r` peut réparer `n` voitures sif `r × n2 ≤ t`.
Ainsi, `n = <<t/r>`. *

* Si la somme sur toutes les mécaniques est **≥ voitures**, alors le temps `t` est possible.
* Sinon, nous avons besoin de plus de temps. *

Parce que la réponse est un entier et la fonction de faisabilité est **monotonique** (si un temps fonctionne, chaque plus grand temps fonctionne), nous pouvons binaire-recherche sur `t`:

«» "
faible = 0 // 0 minutes est toujours trop petite
haute = min_rank * voitures2 // mécanicien seul le plus rapide

alors que faible < élevé:
milieu = (faible + élevé) // 2
si can_repair_all(mid): // test de faisabilité
haute = milieu // mi suffit – essayez plus petit
Sinon:
faible = milieu + 1 // milieu ne suffit pas – besoin plus
retour faible
«» "

La complexité est
- **Heure:** `O(m log (min_rank · cars2)" où `m = grades.longueur`.
- **Espace:** "O(1)" – seulement quelques variables.

Le logarithme est minuscule (30 pour les contraintes maximales), de sorte que la solution correspond facilement aux limites.

---

- Oui. 3. Mise en œuvre des références

Voici des solutions propres, prêtes à coller dans **Java, Python et C++**.
Les trois utilisent la même stratégie de recherche binaire et fonctionnent dans le temps `O(m log...)`.

#### 3.1 Java (Long Arithmétique)

"Java
Importation de java.util.*;

solution de classe publique {
réparation publique longueCars(int[] grades, int voitures) {
long minRank = Arrays.stream(ranks).min().getAsInt();
longue gauche = 0;
long droit = minRank * (long) voitures * voitures; // pire cas

pendant que (à gauche < à droite) {
long milieu = gauche + (droite - gauche) / 2;
Si (peuxréparer(ranks, voitures, milieu)) {
droite = milieu; // milieu de travail – essayer plus petit
} autre {
gauche = milieu + 1; // milieu trop petit
}
}
retour à gauche;
}

booléen privé canRepair(int[] grades, int voitures, long temps) {
long total = 0;
pour (int r : grades) {
long maxCars = (long) Math.floor(Math.sqrt((double) temps / r));
total += maxCars;
si (total >= voitures) retourner vrai; // arrêt précoce
}
total de retour >= les voitures;
}
}
«» "

3.2 Python

'`python
importer des maths
de taper l'importation Liste

Solution de classe:
réparation Voitures (self, grades: List[int], voitures: int) -> Int:
min_rank = min(ranks)
lo, salut = 0, min_rank * voitures * voitures

alors que:
milieu = (lo + hi) // 2
if self._can_repair(ranches, voitures, mi):
hi = milieu # faisable, essayer plus petit
Sinon:
lo = milieu + 1 # impossible, besoin de plus de temps
retour lo

def _can_repair(self, grades: List[int], voitures: int, time: int) -> C'est vrai.
Total = 0
pour r dans les rangs:
Total += int(math.isqrt(temps // r))
si total >= véhicules:
retour Vrai
Retour Faux
«» "

### 3.3 C++ (64-bit)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue réparationCars(vecteur<int>& rang, voitures int) {
long minRank = *min_element(ranks.begin(), Classs.end());
long long bas = 0, élevé = minRank * 1LL * voitures * voitures;

pendant que (faible < haut) {
long moyen = faible + (élevé - faible) / 2;
Si (peuxréparer(ranks, voitures, milieu))
haute = milieu; // milieu des travaux – recherche gauche
Autre
faible = milieu + 1; // milieu trop petit
}
retour faible;
}

particulier:
bool canRepair(vecteur const<int>& rang, voitures int, long temps) {
long total = 0;
pour (int r : grades) {
total += static_cast<long long>(sqrt((double)time / r));
si (total >= voitures) retourner vrai; // sortie anticipée
}
total de retour >= les voitures;
}
};
«» "

> ** Pourquoi le shrt ? * *
> La condition `r * n2 ≤ t` se réarrange pour `n ≤ sqrt(t / r)`.
> Prendre la parole donne le maximum entier `n` qui peut être réparé par ce mécanicien dans le temps `t`.

---

- Oui. 4. Article du blog – Le bon, le mauvais, et le laid de *temps minimum pour réparer des voitures*

4.1 Introduction

Si vous vous préparez à une entrevue d'ingénierie logicielle, vous trouverez *Minimum Time to Repair Cars* (LeetCode 2594) sur de nombreuses listes. C'est un problème de moyenne difficulté qui teste votre capacité à :

- Reconnaître un problème de faisabilité **monotonique**.
- Appliquer ** recherche binaire** sur un espace de réponse.
- Travailler avec **entier math** et éviter le débordement.

Dans cet article, nous disséquons le problème, nous traversons une solution propre, nous discutons d'écueils et nous partageons des mots-clés favorables au SEO qui aideront votre blog à poser des questions.

---

4.2 Compréhension des problèmes

La vitesse d'un mécanicien est régie par un coût quadratique: `temps = rang × n2`.
- Classement = 1 est le plus rapide, rang = 100 est le plus lent.
- `n` est le nombre de voitures une seule réparation mécanique.

Toutes les machines fonctionnent **en parallèle**. La question : **Quel est le temps total minimal pour terminer les voitures `cars`? **

L'approche naïve simulerait chaque mécanicien ajoutant des voitures un par un. Ce serait "O(ranks × voitures)", bien trop lent pour "voitures = 106".

---

4.3 Approches naïves et optimales

Démarche Complexité Pratique
- C'est quoi ?
Simulation de la force brute Effraction aux contraintes élevées
**Recherche binaire dans le temps** Rapide, propre, s'adapte aux limites
Autres Horaires d'avidités incorrects – le coût quadratique rompt simple cupidité

La méthode de recherche binaire est un manuel de recherche de la réponse: ** trouver le plus petit temps qui satisfait une condition de faisabilité**.

---

4.4 Vérification de faisabilité

Compte tenu de l'heure du candidat « non » :

«» "
pour chaque mécanicien ayant rang r:
maxCars = plancher( sqrt(t / r) )
Total += Voitures max
total de retour >= voitures
«» "

Pourquoi `sqrt`?
«r × n2 ≤ t» ─ «n2 ≤ t / r» ─ «n ≤ sqrt(t / r)».
Nous prenons la parole parce que `n` doit être un entier.

---

4.5 Choisir les limites de la recherche

- **Côté inférieur (faible)**: 0 minutes – toujours trop petite.
- **Côté supérieur (haut)**:
Le mécanicien le plus rapide seul aurait besoin `minRank × cars2` minutes.
Aucun emploi du temps ne peut être pire que cela, donc c'est une limite supérieure sûre.

Avec des entiers 64 bits (Java `long`, Python `int`, C++ `long`) Il n'y a pas de risque de débordement.

---

4.6 Complexité temporelle et spatiale

- **Heure**: "O(m log(minRank × voitures2)")".
*Pour les valeurs maximales, il s'agit d'environ 30 itérations × 105 mécanique = 3 millions d'opérations. *
- **Espace**: "O(1)" – seulement quelques compteurs et indices.

---

### 4.7 Surmonter Cas Gotchas

1. **Overflow** – utiliser l'arithmétique 64 bits pour `t = r × n2`.
2. **Floating-point sqrt** – utiliser la racine carrée entière (`Math.isqrt` dans Python, `sqrt` moulé à long en Java/C++).
3. **Arrêt précoce** – dès que les voitures cumulées atteignent la cible, arrêtez de résumer pour gagner du temps.
4. **Boîte d'angle zéro** – "faible" commence à 0; la première fois possible est toujours ≥ 1.

---

Pourquoi cette solution s'écarte

- **Simplicité** : Quelques lignes de code, pas de structures de données supplémentaires.
- **Scalabilité**: Poignée les plus grandes tailles d'entrée confortablement.
- **Générabilité**: Le même cadre de recherche binaire s'applique à de nombreux problèmes d'entrevue avec des contraintes de réponse minimale/maximum réalisable (p. ex. *Nombre minimal de sauts*, *Recherche binaire dans une matrice triée*).

---

### 4.9 SEO & Mots-clés

Pour aider les gestionnaires et les personnes interrogées à trouver votre contenu :

Mots clés primaires Mots clés secondaires Autres
- Oui.
LeetCode 2594, entretien de recherche binaire, problème de coût quadratique
Réparer les voitures Solution LeetCode , Recherche binaire sur la réponse, faisabilité monotonique, dépassement de maths
Entretien problème réparation voitures de temps quadratique complexité, planification optimale entretien

Ajoutez ces étiquettes, incluez un bloc de code rapide, et vous vous classez bien pour la solution de réparation de voitures de LeetCode.

---

###4.9 Conclusion

*Temps minimum pour réparer des voitures* est un problème trompeur simple qui révèle la puissance de la recherche binaire sur un espace de réponse numérique.
La maîtrise de ce modèle vous permettra non seulement de décrocher le travail que vous voulez, mais aussi de renforcer un ensemble de compétences d'entretien de base : **les contraintes de modélisation, la conception d'un test de faisabilité et l'application de la recherche binaire**.

Bon codage, et bonne chance pour votre prochaine interview!

---

- Oui. 5. Pensées finales

Nous avons tout couvert de la stratégie de haut niveau au code prêt à la production en trois langues principales. La solution de recherche binaire est la norme d'or pour *Minimum Time to Repair Cars* – elle est **rapide, robuste et facile à expliquer dans une interview**.

N'hésitez pas à adapter les extraits à votre style ou à agrandir l'article avec des diagrammes visuels et des cas de test plus étendus. Bonne chance, et que votre entretien se déroule bien!