---
titre: LeetCode 715. Module de portée - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 715 – ** Module de portée**
**Traitement 104 opérations *
**LeetCode**: <https://leetcode.com/problems/range-module/>

> Un `RangeModule` suit un ensemble d'intervalles demi-ouverts \([l,r)\).
>
> * `addRange(l,r)` – ajouter un intervalle, fusionner avec n'importe quel intervalle existant.
> * `queryRange(l,r)` – retourner `true` si l'intervalle entier est actuellement couvert.
> * `removeRange(l,r)` – supprimer l'intervalle de l'ensemble suivi.

Ci-dessous vous trouverez trois solutions propres et prêtes à la production – **Java (TreeMap)**, **Python (biect + liste triée)**, **C++ (std::map)** – chacun avec le temps O(log n) par opération.
Après le code, lisez l'article de blog SEO-friendly qui explique *le bon, le mauvais, et le laid* de ce problème, comment il est souvent utilisé dans les interviews techniques, et pourquoi maîtriser peut stimuler vos perspectives d'emploi.

---

- Oui. 1. Java – TreeMap (Faible, facile à comprendre)

"Java
Importation de java.util.*;

classe publique RangeModule {
/** clé = début, valeur = fin (exclusive) */
la version finale privée TreeMap<Integer, Integer> gammes = nouvelle TreeMap<>();

public RangeModule() {}

*** Ajouter [l, r) */
public vide addRange(int l, int r) {
// Trouver l'intervalle de chevauchement le plus à gauche
Carte.Entrée<entier,entier> gauche = ranges.floorEntrée(l);
if (gauche != null && left.getValue() >= l) l = left.getKey();

// Trouver l'intervalle de chevauchement le plus droit
Carte.Entrée<entier,entier> droite = ranges.floorEntrée(r);
si (droite != null && right.getValue() > r) r = right.getValue();

// Supprimer toutes les plages complètement recoupées
ranges.subMap(l, r).clear();

// Insérer l'intervalle fusionné
gammes.put(l, r);
}

*** Retour vrai si [l, r) est entièrement couvert */
requête publique booléenneRange(int l, int r) {
Carte.Entrée<entier,entier> gauche = ranges.floorEntrée(l);
retour à gauche != null && left.getValue() >= r;
}

/** Supprimer [l, r) */
suppression du vide public Gamme(int l, int r) {
Carte.Entrée<entier,entier> gauche = ranges.floorEntrée(l);
if (gauche != null && left.getValue() > l) {
ranges.put(left.getKey(), l); // garder le côté gauche
}

Carte.Entrée<entier,entier> droite = ranges.floorEntrée(r);
si (droite != null && right.getValue() > r) {
ranges.put(r, right.getValue()); // garder le côté droit
}

// Effacer toutes les plages qui tombent à l'intérieur [l, r)
ranges.subMap(l, r).clear();
}
}
«» "

**Pourquoi TreeMap?**
- Conserve les intervalles triés par point de départ.
- `floorEntry` donne la plus grande clé ≤ cible, faisant des contrôles de chevauchement O(log n).
- `subMap` permet d'enlever en vrac tous les intervalles complètement recoupés.

---

- Oui. 2. Python – Liste triée + bisect

'`python
bisect d'importation
de taper l'importation Liste

classe RangeModule:
def _init_(self):
self.starts: List[int] = [] # points de départ
self.ends: Liste[int] = [] # points d'extrémité (exclusif)

def _find_left(self, x: int) -> Int:
"""Le plus grand indice est tel que commence[i] <= x"""
i = bisect.bisect_right(self.starts, x) - 1
retour

def addRange(self, gauche: int, droite: int) -> Aucun:
i = self._find_left(gauche)
i >= 0 et self.ends[i] >= gauche:
gauche = self.starts[i]
j = self._find_left(droite)
i j >= 0 et self.ends[j] > droite:
droite = self.ends[j]

# Supprimer les intervalles de chevauchement
del self.starts[max(0, i+1):j+1]
del self.ends[max(0, i+1):j+1]

# Insérer l'intervalle fusionné
pos = bisect.bisect_left(self.starts, gauche)
self.starts.insert(pos, gauche)
auto.ends.insert(pos, droit)

def requêteRange(self, gauche: int, droite: int) -> C'est vrai.
i = self._find_left(gauche)
retour i >= 0 et self.ends[i] >= droite

def supprimer Gamme (auto, gauche: int, droite: int) -> Aucun:
i = self._find_left(gauche)
i >= 0 et self.ends[i] > gauche:
self.ends[i] = gauche # tronquer la partie gauche

j = self._find_left(droite)
i j >= 0 et self.ends[j] > droite:
# Insérer un nouvel intervalle pour la partie droite
pos = bisect.bisect_left(self.starts, droite)
self.starts.insert(pos, droit)
(pos, self.ends[j])
self.ends[j] = droite

# Supprimer les intervalles complètement recoupés
del self.starts[max(0, i+1):j+1]
del self.ends[max(0, i+1):j+1]
«» "

**Pourquoi bisect + listes? * *
- Le "bisect" de Python donne la recherche O(log n).
- Deux listes parallèles maintiennent des paires start/end, ce qui réduit l'empreinte mémoire.
- Toutes les modifications restent O(log n) plus O(k) pour supprimer les intervalles de chevauchement `k` (k ≤ n).

---

- Oui. 3. C++ – `std::map` (contenant associatif commandé)

'`cpp
#incluez <map>

classe RangeModule {
std::map<int, int> mp; // clé = début, valeur = fin (exclusive)

public:
GammeModule() {}

vide addRange(int gauche, int droite) {
auto it = mp.lower_bound(gauche);
si (it != mp.degin()) {
auto prev = std::prev(it);
si (prev->seconde >= gauche) gauche = prev->première;
}
pendant que (it != mp.end() && it->first <= right) {
droite = md::max(droite, it->seconde);
il = mp.erase(it);
}
mp.emplace(gauche, droite);
}

requête boolRange(int gauche, int droite) {
auto it = mp.upper_bound(gauche);
si (it) == mp.begin() retourne false;
--it;
retourner it->seconde >= droit;
}

vide supprimer Gamme(int gauche, int droite) {
auto it = mp.lower_bound(gauche);
si (it != mp.degin()) {
auto prev = std::prev(it);
si (prév->seconde > gauche) {
int old_end = prev->seconde;
prev->seconde = gauche;
si (vieille_fin > droite) {
mp.emplace(droite, old_end);
}
}
}
pendant que (it != mp.end() && it->first < right) {
si (it->seconde > droite) {
mp.emplace(à droite, it->seconde);
}
il = mp.erase(it);
}
}
};
«» "

**Pourquoi `std::map`?**
- Insertion logarithmique, suppression et recherche.
- Effacer la syntaxe pour la logique de division/fusion.
- Fonctionne bien dans des environnements de programmation compétitifs.

---

- Oui. 4. Le Bon, le Mauvais, et l'Ugly

Qu'est-ce qu'un bien?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Structure des données**= Les cartes commandées conservent les intervalles triés → Opérations O(log n)= Si vous utilisez une *list* ou *vector*, les opérations deviennent O(n)-- Éviter les balayages linéaires naïfs après chaque mise à jour.
**Logique de fusion**= L'approche simple d'expansion gauche/droite combine toutes les plages de chevauchement en une seule passe== Oublier de gérer les intervalles * adjacents* (par exemple, `[1,3]` et `[3,5)`) → peut laisser des lacunes
**Délétion**=Séparez les parties gauche/droite si elles existent → aucune donnée perdue==Supprimer ou oublier de garder le fragment droit==Tenir la trace de l'intervalle initial=s se termine avant d'effacer==
**Mémoire**=Les cartes ne sont stockées que *disjointes* Intervalles==Les ajouts/suppressions répétés peuvent fragmenter la carte → de nombreuses petites gammes==Passer agressivement dans `addRange` pour garder la taille minimale==
Chaque opération est *logarithmique Dans le pire des cas, enlevant de nombreux petits intervalles → O(k log n)
**Language quirks**

- Oui. Le côté "Ugly"

- **Juges**:
- Ajout d'une gamme qui touche la fin d'une gamme existante.
- Supprimer une plage qui chevauche partiellement plusieurs intervalles.
- Interroger un ensemble ou une plage vide en dehors de tous les intervalles.

- **Off‐par‐un**:
Étant donné que les intervalles sont *demi-ouverts*, une plage «[10, 20)» comprend 10 mais exclut 20.
Le traiter comme fermé peut conduire à des bugs subtils.

- **Sécurité des fils**:
Les implémentations données sont *not* thread‐safe.
Dans un environnement multifilé, vous aurez besoin de serrures externes ou d'une carte concurrente.

---

- Oui. 5. Pourquoi le module Mastering Range aide votre carrière

1. ** Fréquence des entretiens**
- *Le module de ramification* est un élément essentiel des plateformes de recrutement technique (LeetCode, HackerRank, InterviewBit).
- Il teste votre capacité à maintenir un ensemble *dynamique* d'intervalles – un problème classique de structure des données.

2. **Feuille de cuisson conventionnelle**
- Vous allez pratiquer :
*Cartes ordonnées / BST équilibrées* → connaissances de base sur la structure des données.
*Arithmétique intermédiaire* → maths + manipulation de cas de bord.
*Set opérations (union, intersection, différence)* → fondamentale à de nombreux systèmes.

3. **Affichage des problèmes de résolution**
- Ecrivez une implémentation claire et sans bugs dans la langue avec laquelle vous êtes à l'aise.
- Expliquer les compromis dans l'espace temporel au cours d'une entrevue; il montre une compréhension approfondie.

4. ** Pertinence de la production**
- De nombreux services dans le monde réel (p. ex. moteurs de flag, systèmes de programmation, règles de pare-feu réseau) maintiennent des gammes d'horodatage ou de blocs IP.
- Connaître ce modèle vous donne confiance pour contribuer immédiatement à de tels systèmes.

---

- Oui. 5. Titre et aperçu du blog

**Titre**
> Module d'analyse – La puissance de l'entrevue : 715 LeetCode expliqué (bon, mauvais et ingénieux)

**Description détaillée**
> Plongez dans le problème du module d'extension (LeetCode #715). Apprenez trois solutions O(log n) en Java, Python et C++, ainsi que des idées d'entrevue sur la gestion des cas de bord et pourquoi maîtriser ce problème peut vous poser un rôle d'ingénierie logicielle.

** Rubriques proposées* *

1. **Qu'est-ce que le module Gamme?** – Énoncé de problème et intervalles demi-ouverts.
2. **Pourquoi ce problème se trouve-t-il pour les entrevues** – Ensemble dynamique d'intervalles, compromis temporels.
3. **Trois implémentations de production-ready** – Java, Python, C++ (blocs de code).
4. **Le bon** – Cartes ordonnées, opérations logarithmiques, logique de fusion par division claire.
5. **Le mauvais** – Cas de bord, erreurs par un, fragmentation.
6. **L'Ugly** – Intervalles adjacents, sécurité des fils, fragmentation à grande échelle.
7. ** Erreurs communes à éviter** – Liste de contrôle Pseudocode, tests de limites.
8. **Au-delà du problème** – Appliquer la logique de l'intervalle aux règles de programmation, de mise en cache, de pare-feu.
9. **Interview Success Tips** – Comment expliquer votre solution, les discussions de compromis, le traitement des questions de suivi.
10. **Conclusion et prochaines étapes** – Autres problèmes (Merge Intervalles, 315 – Compte de petits nombres, 720 – Word le plus long du dictionnaire) et ressources.

---

À emporter

Maîtrise **Le module de portée** signifie que vous pouvez :

- Écrire un code efficace, sans bug pour les problèmes d'intervalle dynamique.
- articuler les compromis entre différentes langues et structures de données.
- Résoudre un problème d'entrevue classique qui teste à la fois la connaissance de la structure des données et le raisonnement prudent sur les cas de bord.

Essayez les solutions, faites quelques tests aléatoires et ressentez la confiance qui vient d'être *pro-professionnel* à la gestion des gammes. Bon codage – et bonne chance pour votre prochaine entrevue!