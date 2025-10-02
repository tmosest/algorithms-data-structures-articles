---
titre: LeetCode 1124. Intervalle le plus long et le plus performant -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de maîtrise du leet 1124 – *Intervalle le plus long et le plus performant*
*(Java-Python-C++) – Bon, le mauvais et le mauvais – Votre chemin vers un travail de rêve*

---

Récapitulatif du problème (présenté par le SEO)

> **LeetCode 1124 – Intervalle le plus long et le plus performant**
> *Difficulté*: Moyenne
> *Tag*: `Array`, `HashMap`, `Prefix Sum`, `Deux Pointeurs "

Vous êtes donné un tableau entier `heures[]` où chaque élément est le nombre d'heures travaillées sur un jour donné.
- Un jour de repos** = "heures [i] > 8".
- Un intervalle **performant** = sous-tarif où **jours d'attente >jours d'attente**.

**Objectif**: Retourner la longueur de l'intervalle le plus long et le plus performant.

> **Pourquoi cela est important pour les entrevues d'emploi* *
> 1. Démontre la maîtrise de *les montants préfixés* et *les cartes hash*.
> 2. Montre comment transformer un problème en un problème plus simple d'équilibre (latent = +1, non-latent = –1).
> 3. Faits saillants O(n) temps et O(n) espace – les intervieweurs aiment les solutions linéaires.

---

- Oui. La bonne solution O(n) HashMap

L'astuce classique est de cartographier chaque jour à **+1** (latent) ou **–1** (non fatigant) et de garder une somme de préfixe en cours d'exécution.
Si à tout moment la somme du préfixe est positive, nous avons déjà vu un intervalle qui commence à l'index 0.
Si la somme du préfixe n'est pas positive, nous cherchons le premier indice où la somme était **(currentSum‐1)**.
La distance entre ces indices donne l'intervalle le plus long se terminant au jour actuel.

Concept Code
- Oui.
"Somme préfixe (tring→+1, pas fatiguante→–1)" "somme += heures[i] > 8 ? 1 : -1;"
Carte de la première occurrence
Autres Mettre à jour la réponse «ans = Math.max(ans, i - firstIdx.get(sum-1));» Autres

Mise en œuvre Java (HashMap O(n))

"Java
Importation de java.util.*;

solution de classe {
le plus long IWP(int[] heures) {
si (durée des heures) 0) retour 0;

Int maxLen = 0;
Carte <entier, entier> premierIdx = nouveau HashMap<>();
= 0; // solde de fonctionnement

pour (int i = 0; i < durée des heures; i++) {
somme += heures[i] > 8 ? 1 : -1;

// Enregistrez la première fois que nous voyons cette somme
premierIdx.putIfAbsent(sum, i);

// Si la somme > 0, l'intervalle commence à 0
si (somme > 0) {
maxLen = i + 1;
} autre {
// Recherchez un indice antérieur où la somme était (somme-1)
Total j = premierIdx.get(sum - 1);
si (j != null) {
maxLen = Math.max(maxLen, i - j);
}
}
}
retour maxLen;
}
}
«» "

**Complexités* *
- **Time**: `O(n)` – une passe, hashmap temps constant ops.
- **Espace**: `O(n)` – stockage des premières occurrences de chaque somme.

---

- Oui. Le Python – rapide et lisible

'`python
Solution de classe:
def le plus long IPT(self, hours: List[int]) -> Int:
premier = {} # somme -> premier indice
s = 0
ans = 0

pour i, h en nombre d'heures:
s += 1 si h > 8 autres

si n'est pas en premier:
premier[s] = i

si s > 0:
ans = i + 1
Sinon:
j = premier.get(s) - 1)
si j n'est pas None:
ans = max(ans, i - j)
retour et
«» "

*Pourquoi Python est génial pour la préparation de l'entrevue :*
- Effacer la syntaxe (`s += 1 si h > 8 autres -1`).
- Le dictionnaire intégré rend la logique du hashmap trivial.

---

## 4-C++- Speedy et Idiomatic

'`cpp
solution de classe {
public:
Int le plus long IPT(vecteur<int>& heures) {
non ordonné_map<int, int> premier; // somme -> premier indice
somme int = 0, ans = 0;

pour (int i = 0; i < hours.size(); ++i) {
somme += (heures[i] > 8) ? 1 : -1;

si (!first.count(sum))
premier[sum] = i;

si (somme > 0) {
ans = i + 1;
} autre {
auto it = first.find(sum - 1);
si (it != first.end())
ans = max(ans, i - it->seconde);
}
}
le retour des an;
}
};
«» "

*Pourquoi C++ compte : *
- `unordered_map` donne la moyenne de la recherche O(1).
- La sécurité du temps compile et l'exécution rapide – utile pour les entrevues critiques.

---

C'est pas vrai. L'Éclat – Pièges communs et comment les éviter

Pourquoi il échoue
- C'est quoi ?
**O(n2) scan bi-pointer**=Temps Quadratic, TLE sur 104 array== Remplacer par préfixe-sum + hashmap==
**Utiliser `HashMap.put(sum, i)` à chaque fois**
Erreurs hors-par-un (>=8 au lieu de >8)
**Ignorer la réponse de longueur zéro**= Retourner négatif lorsqu'aucun intervalle n'est trouvé== Retourner `0` si `ans== Pas de problème.
**L'utilisation de `sum-1` incorrectement**=Fails quand `sum` n'a jamais atteint `-1`=Vérifie l'existence de la carte avant de soustraire

> **Astuce**: Exécutez toujours les cas échantillons plus les cas bord (tous fatigants, tous non latents, en alternance) avant de soumettre.

---

# # # 6 Les cas de l'Ugly – Tweaks & Edge avancés

1. **L'espace est optimisé sans HashMap**
- Utilisez une pile monotonique décroissante d'indices pour suivre les montants préfixés.
- Temps toujours `O(n)` mais `O(n)` empile de l'espace; fonctionne si vous voulez éviter le hachage.

2. ** Contraintes d'entrée importantes à la main* *
- Préfixer les sommes peut être négatif jusqu'à `-n`.
- En Java, un `int` est une amende (`n ≤ 104`).
- Pour `n` jusqu`à `106`, envisager d`utiliser `long` pour la sécurité.

3. **Parallélisation**
- Pas nécessaire pour LeetCode mais peut être utile dans les pipelines de données du monde réel.

4. **Cadre de test* *
- Construisez un harnais JUnit ou PyTest rapide pour valider automatiquement des milliers de cas de tests aléatoires.

---

Résumé du blog optimisé

Titre
> **Crack LeetCode 1124: Intervalle le plus performant – Java, Python, C++ Solutions + Conseils d'entrevue**

Description de la méta
> Master LeetCode 1124 avec notre guide complet: Solution Java HashMap O(n), implémentations Python & C++, pièges et stratégies d'entrevue.

Rubriques et mots-clés

Titre Mots clés
C'est pas vrai.
Récapitulatif des problèmes
La bonne solution de HashMap, la somme de préfixe, le temps
Version de Python Version de Python Solution de Python, Dictionnaire, Code de Leet 1124
Version C++ Solution C++, Carte non commandée, Programmation compétitive
Erreurs communes
Interview d'emploi Edge, interview de codage, questions d'entrevue d'algorithme

### Appel à l'action
> Prêt à accepter votre prochaine entrevue de codage ? Laissez un commentaire ci-dessous avec votre propre solution ou posez des questions. N'oubliez pas de frapper **Abonnez-vous** pour plus de LeetCode qui vous atterrissent le travail que vous voulez!

---

- Oui. Dernier départ

- **Bien**: O(n) hashmap + solution de somme de préfixe – simple, rapide, facile à interviewer.
- **Bad**: Surcomplication avec des scans quadratiques ou une mauvaise utilisation des cartes de hachage – évitez!
- **Ugly**: Rares cas de bord, mais avec un plan clair, vous ne voyagerez jamais sur eux.

Avec ces implémentations et conseils, vous êtes désormais équipé pour impressionner les recruteurs sur LeetCode, GitHub, ou dans votre prochaine interview. Bon codage 