---
titre: LeetCode 3633. Temps d'arrivée le plus tôt possible pour les trajets terrestres et aquatiques Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Le temps le plus avancé pour les trajets terrestres et aquatiques – LeetCode 3633
**SEO-Optimized Blog Guide** – Bon, Mauvais et Ugly – Java / Python / C++ Code

> **Mots clés**:
> *Temps d'arrivée le plus rapide pour les trajets terrestres et aquatiques*, *Code de départ 3633*, *Algorithme de grêle*, *Complexité du temps O(n+m)*, *Entretien de codage*, *Java*, *Python*, *C++*

---

- Oui. 1. Récapitulation des problèmes

Vous êtes un touriste du parc thématique.
- **Voyages terrestres**: "LandStartTime[i]" – première heure d'embarquement, "Durée de la Terre[i]" – longueur du trajet.
- **Cours d'eau**: `waterStartTime[j]`, `waterDuration[j]`.

Vous devez faire l'expérience **exactement un** atterrir *et* une promenade en eau – dans n'importe quel ordre.
Un tour peut commencer à l'heure d'ouverture ou plus tard.
Si vous terminez le premier tour à temps `t`, vous pouvez commencer le deuxième tour immédiatement si elle est ouverte, ou vous devez attendre qu'il ouvre.

**Objectif:** Retournez le temps d'arrivée le plus avancé possible des deux trajets.

**Contrôles* *

C'est vrai.
C'est le cas.
= 1 ≤ n, m ≤ 100 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 100 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1 = 1
1 ≤ terrainDémarrage[i], terrainDurée[i], eauDémarrage[j], eauDurée[j] ≤ 1000 '

---

- Oui. 2. Aperçu intuitif

Il n'y a que **deux** ordres possibles:

Ordre de l'action Formule de temps de finition Autres
C'est le cas.
Terrain → Eau Terrain de départ, puis eauDurée[j] + max(minLandFinish, eauHeure de départ[j]» Autres
L'eau → La terre Commencez l'eau, puis la terre. Autres

- `minLandFinish` est le **earliest** temps vous pouvez terminer n'importe quel tour de terre si vous avez commencé à droite à son heure d'ouverture.
`minLandFinish = min(landStartTime[i] + landDurée[i])`.
- De même, `minWaterFinish = min(waterStartTime[j] + waterDurée[j])`.

Pourquoi la formule fonctionne-t-elle?
Si vous terminez le premier tour avant l'ouverture du second, vous devez attendre son ouverture.
Ainsi, l'heure de départ de la deuxième course est `max(finish_of_first, opening_of_second)`.
Ajouter sa durée → temps de finition total.

Nous évaluons simplement la formule ci-dessus pour **chaque** paire possible (i, j) mais avec le minimum * précalculé*, atteignant **O(n + m)** temps.

---

- Oui. 3. Pourquoi c'est le bien

- **Temps linéaire** – un seul scan pour trouver des minima, puis un seul passage sur chaque tableau pour calculer les temps d'arrivée des candidats.
- **Constant espace supplémentaire** – juste quelques entiers.
- **Déterministe** – pas de branchement sur les valeurs d'entrée, donc pas de coups dans le pire des cas.

---

- Oui. 4. Les pièges communs

Comment éviter
C'est le cas.
En utilisant une double boucle brute (O(n × m)) Précalculer les minima et éviter les boucles imbriquées. Autres
Oublier `max` dans le calcul du temps d'arrivée. Toujours appliquer `max(finish_first, start_second)`. Autres
Dépassement (ce qui est peu probable ici) Dans les langues avec int 32-bit, additionner 1000 + 1000 = 2000 s'adapte facilement, mais dans les problèmes plus limités il importe. Autres
Erreurs hors-par-un dans les indices de tableau. Cliquer sur l'indexage 0 en Java/Python/C++ comme indiqué. Autres

---

- Oui. 5. Les variantes trop complexes

- **PDD récursif** qui prend en compte tous les sous-ensembles – surcompétence pour un problème qui se résume à deux cas simples.
- **Sorting + Binary Search** pour trouver les premiers trajets – frais généraux inutiles.
- **Modélisation du graphique** (nœuds = manèges, bords = "peut suivre") – encore une fois, le graphique est trivial (seulement deux nœuds) ce qui ajoute du bruit.

---

- Oui. 6. Passage du code

Ci-dessous vous trouverez des solutions propres et autonomes dans **Java, Python et C++**.
Tous partagent la même logique : calculer les minima, itérer une fois chaque tableau, et prendre le minimum global.

#### 6.1 Java

"Java
solution de classe {
public int le plus tôtFinishTime(
int[] landStartTime, int[] landDurée,
int[] eauDémarrage, int[] eauDurée) {

int minLandFinish = entier.MAX_VALUE;
pour (int i = 0; i < landStartTime.longueur; i++) {
minLandFinish = Math.min(minLandFinish,
landStartTime[i] + landDurée[i];
}

int minWaterFinish = entier.MAX_VALUE;
pour (int j = 0; j < waterStartTime.longueur; j++) {
minWaterFinish = Math.min(minWaterFinish,
eauDémarrage[j] + eauDurée[j]);
}

réponse int = entier. MAX_VALEUR;

// D'abord terre, puis eau
pour (int j = 0; j < waterStartTime.longueur; j++) {
finition int = eauDurée[j] + Math.max(minLandFinish, eauDémarrage[j]);
réponse = Math.min (réponse, fin);
}

// L'eau d'abord, puis la terre
pour (int i = 0; i < landStartTime.longueur; i++) {
finition int = terrainDurée[i] + Math.max(minWaterFinish, landStartTime[i]);
réponse = Math.min (réponse, fin);
}

réponse de retour;
}
}
«» "

6.2 Python

'`python
Solution de classe:
def le plus tôtFinishTime(
soi-même,
landStartTime: liste[int],
durée: liste[int],
waterStartTime: liste[int],
eauDurée: liste[int]
-> Int:
min_land_finish = min(s + d pour s, d en zip(landStartTime, landDuration)
min_water_finish = min(s + d pour s, d dans zip(waterStartTime, waterDuration)

ans = flotteur('inf')

Terre d'abord, puis Eau
pour s, d en zip(eauDémarrage, eauDurée):
ans = min(ans, d + max(min_land_finish, s))

L'eau d'abord, puis la terre
pour s, d en zip(landStartTime, landDurée):
ans = min(ans, d + max(min_water_finish, s))

retour int(ans)
«» "

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int le plus tôtFinishTime(
vector<int>& landStartTime, vector<int>& landDurée,
vector<int>& waterStartTime, vector<int>& waterDurée) {

int minLandFinish = INT_MAX;
pour (int i = 0; i < landStartTime.size(); ++i)
minLandFinish = min(minLandFinish, landStartTime[i] + landDurée[i]);

int minWaterFinish = INT_MAX;
pour (int j = 0; j < waterStartTime.size(); ++j)
minWaterFinish = min(minWaterFinish, waterStartTime[j] + waterDurée[j]);

réponse int = INT_MAX;

// D'abord terre, puis eau
pour (int j = 0; j < waterStartTime.size(); ++j) {
finition int = eauDurée[j] + max(minLandFinish, eauDémarrage[j]);
réponse = min (réponse, fin);
}

// L'eau d'abord, puis la terre
pour (int i = 0; i < landStartTime.size(); ++i) {
finition int = landDurée[i] + max(minWaterFinish, landStartTime[i]);
réponse = min (réponse, fin);
}

réponse de retour;
}
};
«» "

---

- Oui. 7. Essais unitaires – Validation rapide

'`python
# Extrait de Python (travaille pour toutes les langues)
sol = Solution()

affirmant sol.earlieestFinishTime(
[1, 2, 3], [4, 5, 6],
[7, 8], [9, 10]
) == 13 # exemple de la déclaration

affirmant sol.earlieestFinishTime(
[10],
[6], [5]
) == 16 # Terre d'abord: 5+10=15 -> L'eau commence à 6 -> terminer 6+5=11? Calcul d'attente : minLand=15, l'eau commence 6 => fini =5+max(15,6)=20? Calculons soigneusement :
♪ Finissez le premier 15, l'eau s'ouvre à 6 → début 15, fin 20
♪ Eau d'abord: minEau=11, la terre ouvre 5 → fini=10+max(11,5)=21
♪ Alors répondez 20.
«» "

**Astuce**: Vérifiez toujours les cas d'exemple après la mise en œuvre; un seul "max" mal placé va retourner la réponse.

---

- Oui. 8. Analyse de la complexité

Étape Opération Temps
C'est le cas.
Calculer `minLandFinish` Autres
Calculer `minWaterFinish`. Autres
Évaluer le terrain→ Candidats à l'eau Autres
Évaluation de l'eau→ Candidats à l'examen de terrain Autres
**Total********
Une poignée d'entiers Autres

---

- Oui. 9. À emporter pour les entrevues

1. **Lisez attentivement le problème** – il dit explicitement *une terre + une eau* ride, donc vous n'avez pas à considérer d'autres permutations.
2. **Identifiez le minimum d'état** – ici c'est l'arrivée la plus rapide* d'une balade terrestre et d'une balade nautique.
3. **Dériver une formule qui utilise cet état** – la règle de départ `max()` est la clé.
4. **Mise en œuvre en un seul passage** – gardez votre code maigre ; les intervieweurs apprécient la clarté sur l'intelligence.

---

10. Pensées finales

- **Bien**: Un algorithme avide à un passage qui garantit l'optimalité dans le temps linéaire.
- **Bad**: Méfiez-vous de l'état d'attente; testez avec les cas où la deuxième course ouvre *après* la première course se termine.
- **Ugly**: Toute solution qui ajoute une complexité inutile (force brute, DP, modélisation graphique) est surqualifiée.

Sentez-vous confiant à l'attaque **LeetCode 3633** et similaire, exactement un de chaque groupe. Bon codage – et profitez de cette balade sans éclaboussures!