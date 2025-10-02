---
titre: LeetCode 2187. Temps minimum pour effectuer des voyages -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2187 – Temps minimum pour effectuer des voyages
### Les bons, les mauvais et les méchants – Un guide complet pour mener l'entrevue

---

TL; RD
* **Problème** – Compte tenu d'un éventail de temps de trajet en bus, trouver le temps minimum nécessaire pour tous les bus ensemble pour terminer au moins "totalTrips".
* **Solution** – Classique ** recherche binaire sur la réponse**.
* **Complexités** – «O(n log (minTime * totalTrips)»)» temps, «O(1)» espace supplémentaire.
* **Langues** – Java, Python, C++ (toutes avec la même logique).

---

## 1--Déclaration du problème (Code Leet 2187)

> ** Temps minimum pour effectuer des voyages**
> **Difficulté:** Moyenne
> **Tags:** Recherche binaire, Greedy
> **Lien:** <https://leetcode.com/problèmes/minimum-time-to-complete-trips/>

Vous avez reçu :
Texte
temps[i] – temps (en minutes) un seul bus prend pour terminer un voyage
Total général Voyages – le nombre total de voyages que tous les bus doivent terminer ensemble
«» "
Chaque bus peut commencer un nouveau voyage immédiatement après en avoir terminé un.
Retourner le plus petit entier `T` de telle sorte que, en 'T` minutes, les bus ensemble terminent ** au moins** `totalTrips` voyages.

**Exemple**
Texte
temps = [1,2,3], totalTrips = 5
Produit : 3
«» "
* Au temps 3 minutes les bus ont terminé 5 voyages au total. *

---

- Oui. Pourquoi la recherche binaire sur la réponse?
L'observation clé :
> *Si nous pouvons calculer le nombre de voyages terminés dans un temps donné `mi`, nous pouvons décider si nous avons besoin de plus de temps ou peut terminer plus tôt. *

Laissez
«» "
voyages(milieu) = plancher(milieu/temps[i]) // total des voyages effectués par tous les autobus
«» "
- Si `trips(mid) < totalTrips` → nous avons besoin **plus** temps → `low = mi + 1`.
- Oui. Sinon nous pouvons essayer de trouver un temps plus petit possible → `haut = milieu`.

La portée de recherche va du plus petit temps possible (`1`) au pire cas:
`high = min(time) * totalTrips`.
Cela garantit que nous ne manquons jamais la réponse et garde la recherche binaire logarithmique.

---

- Oui. Le Bon – Pourquoi Cette approche Rocks

Pourquoi il est grand
C'est-à-dire
**Recherche logarithmique**=Cutifie le temps de façon drastique (=40 itérations pour les numéros 64 bits). Autres
**O(1) Espace extra**Utilisez seulement quelques variables ; idéal pour les contraintes d'entrevue. Autres
**Handles Large Inputs**= Fonctionne pour `n = 105`, `totalTrips = 107` et `time[i] ≤ 107`. Autres
**Clarifier la logique** Autres

---

- Oui. Les mauvaises – choses à surveiller

Piège
- Oui.
**Excédent total**= Utiliser `long`/`long long` pour les sommes intermédiaires. Autres
Autres **Contrairement à la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie inférieure de la partie supérieure de la partie supérieure de la partie inférieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie inférieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie inférieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie inférieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie inférieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie supérieure de la partie Autres
Autres **Edge Cases** 1`) → la réponse est `temps[0] * totalTrips`. Autres
**Off‐By‐One**= Assurez-vous que la boucle de recherche binaire utilise `faible < high` et `mid = low + (haut - bas)/2`. Autres

---

C'est pas vrai. L'horrible – Ce qui arrive si vous allez mal

1. ** Simulation de la force brute** – Augmentation d'une minute à la fois → "O(totalTrips * min(time)" → TLE.
2. **Floating‐Point Guess** – L'utilisation de doubles peut donner des limites entiers erronées.
3. **Traitement inutile** – Trier le tableau `time` est *pas nécessaire* et gaspille le temps `O(n log n)`.
4. ** Contraintes manquantes** – Sans respecter le «temps[i], totalTrips ≤ 107» conduit à un débordement de 32 bits sur de nombreuses plates-formes.

---

Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
Tous utilisent la même stratégie de recherche binaire sur la réponse.

---

- Oui. 6.1 Java (Java 17)

"Java
***
* 2187. Durée minimale des voyages
* Recherche binaire sur la réponse
*/
solution de classe {
public long minimum Temps(int[] temps, int totalTrips) {
// Cas de bord: un seul bus
si (durée) 1) {
retour (long) temps[0] * totalTrips;
}

// Trouvez le bus le plus rapide – utilisé pour la liaison supérieure
int minTime = entier.MAX_VALUE;
pour (int t : temps) minTime = Math.min(minTime, t);

long bas = 0; // inclusivement
longueur élevée = (long) minTime * totalTrips; // inclus limite supérieure

pendant que (faible < haut) {
long milieu = faible + (élevé - faible) / 2;
si (tripsDone(temps, milieu) < totalTrips) {
faible = milieu + 1; // besoin de plus de temps
} autre {
haute = moyenne; // réponse possible
}
}
retour faible;
}

*** Aide: total des trajets effectués par tous les bus en 'temps' minutes */
voyages longs privésDone(int[] time, long timeLimit) {
voyages longs = 0;
pour (int t : heure) {
voyages += tempsLimit / t; // division entière
}
les voyages de retour;
}
}
«» "

---

- Oui. 6.2 Python 3

'`python
Solution de classe:
def minimum Temps(même, temps: Liste[int], totalTrips: int) -> Int:
# Un seul raccourci de bus
si len(temps) == 1 :
Temps de retour[0] * totalTrips

min_time = min(time)
faible, élevé = 0, min_temps * total Voyages # limites inclusives

alors que faible < élevé:
milieu = (faible + élevé) // 2
voyages = somme (milieu // t pour t dans le temps)
si les voyages < totalTrips:
faible = milieu + 1
Sinon:
haute = moyenne
retour faible
«» "

---

#### 6.3 C++17

'`cpp
***
* 2187. Durée minimale des voyages
* Recherche binaire sur la réponse
*/
solution de classe {
public:
long long minimum long Temps(vecteur<int>& temps, int totalTrips) {
si (time.size()) == 1) retour 1LL * temps[0] * totalTrips;

int minTime = *min_element(time.begin(), time.end());
longue longue basse = 0;
long et élevé = 1LL * minTime * totalTrips;

pendant que (faible < haut) {
long moyen = faible + (élevé - faible) / 2;
longs voyages = voyagesDone(temps, milieu);
si (trips < totalTrips) faible = milieu + 1;
Autre haut = milieu;
}
retour faible;
}

particulier:
longs voyages Fait(vecteur continu<int>& temps, longue limite) {
somme longue = 0;
pour (int t : temps) somme += limite / t;
la somme de retour;
}
};
«» "

---

Essai du code

'`python
# Exemple
sol = Solution()
print(sol.minimumTime([1,2,3], 5) # → 3
print(sol.minimumTime([5,10,2], 3)) # → 10
«» "

Les trois solutions produisent la bonne réponse pour l'échantillon et sont entièrement conformes aux contraintes du problème.

---

C'est pas vrai. Comment utiliser ce problème dans votre préparation d'entrevue

Étape
C'est quoi ?
**Comprendre l'idée centrale**= Recherche binaire sur la réponse → facile à expliquer. Autres
**Manipulation pratique de l'ensemble des cas** Autres
**Temps vous-même**. Autres
**Expliquez l'approche**. Autres
**Mention alternatives**= Montrez que vous avez pensé à la simulation, avide, ou DP – alors expliquez pourquoi ils échouent. Autres

> **Interview Tip** – Lorsqu'on lui demande : Que se passe-t-il si `totalTrips` est extrêmement grand?', vous pouvez immédiatement discuter pourquoi la recherche binaire liée supérieure utilise `min(time) * totalTrips` et comment cela maintient l'espace de recherche limité.

---

Liste de contrôle du référencement – Faites votre classement de blog et terre que travail

Recommandation Autres
C'est-à-dire
**Titre** 2187 – Temps minimum pour effectuer des voyages: Recherche binaire Masterclass
**Moyen Description**=Solve LeetCode 2187 en Java, Python et C++. Découvrez la stratégie de recherche binaire, l'analyse de complexité et le code prêt à l'entrevue. Autres
**En-têtes**= Utiliser H1 pour le titre, H2 pour les sections (Problème, Approche, Code, etc.). Autres
**Mots clés**="Leetcode 2187`, `Minimum Time to Complete Trips`, `binary search interview`, `software engineer interview`, `coding interview prep`. Autres
**Liens internes**= Lien vers vos autres blogs de préparation d'entrevues (=10 questions d'entrevue de LeetCode). Autres
**Formulation du code** . Utilisez les blocs `<pre><code>` pour la lisibilité. Autres
Télécharger les solutions, les essayer sur LeetCode, et partager vos résultats! Autres

---

Réflexions finales

* **La recherche binaire sur la réponse** est la norme d'or* pour les problèmes comme 2187.
* Mettre l'accent sur la sécurité dans les situations de pointe** (débordement, autobus unique).
* Gardez le code concis – les intervieweurs valent *clarité* sur l'intelligence.

Maîtrisez ce problème, ajoutez les solutions à votre portefeuille, et vous impressionnerez tout gestionnaire d'embauche qui se soucie de pensée algorithmique propre. Bonne chance ! C'est ce qu'il a dit.

---

** Bon codage, et que votre prochaine entrevue soit une offre d'emploi!* *