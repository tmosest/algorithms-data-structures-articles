---
titre: LeetCode 3668. Restaurer l'ordre de finition -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3668. Restaurer l'ordre de finition
**Facile**=https://leetcode.com/problèmes/restore-finishing-order/>

> On vous donne un tableau entier `ordre` de longueur *n* et un tableau entier `amis`.
> `order` contient chaque entier de 1 à *n* exactement une fois, représentant les ID des participants d'une course dans leur ordre d'arrivée.
> `friends` contient les ID de vos amis dans la course triée dans l'ordre strictement croissant.
> Chaque ID dans `friends` est garanti pour apparaître dans le tableau `order`.
> **Retourner un tableau contenant vos amis Les pièces d'identité dans leur ordre de finition. **

---

- Oui. 1. Brute-Force vs Optimal

Stratégie Temps Espace Pourquoi ça marche
- C'est quoi ?
**Brute-Force** – pour chaque ami, scannez `commande` jusqu'à ce que vous le trouviez.
**HashSet + Single Pass** – mettre tous les amis dans un ensemble de hachage, itérer au-dessus de "order" **O(n + m)**

L'approche de hachage est la solution canonique sur LeetCode (vitesse à 100%).

---

- Oui. 2. Mise en œuvre des références

> **Note** – toutes les implémentations partagent la même logique :
> 1. Construisez un `Set` (ou `unordered_set` / `HashSet`) à partir de `friends`.
> 2. Scanner `commande`; chaque fois qu'un élément est dans l'ensemble, l'ajouter à la réponse.

### 2.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe {
public int[] récupérerOrdre(int[] ordre, int[] amis) {
Set<integer> friendSet = nouveau HashSet<>();
pour (int f : amis) amiSet.add(f);

int[] res = nouveau int[friends.longueur];
Int idx = 0;
pour (int id : ordre) {
si (friendSet.contient(id)) {
res[idx++] = id;
}
}
retour rés;
}
}
«» "

#### 2.2 Python (Python 3,11)

'`python
Solution de classe:
def recoverOrdonnance(self, commander: List[int], amis: List[int]) -> Liste[int]:
friend_set = set(friends)
retourner [id_ pour id_ dans l'ordre si id_ dans friend_set]
«» "

N° 2.3 C++ (C++17)

'`cpp
solution de classe {
public:
vector<int> recoverOrdonnance(vecteur<int> et ordre, vector<int> et amis) {
unordered_set<int> amiSet(friends.begin(), friends.end());
vecteur<int> rés;
res.reserve(friends.size());
pour (int id : ordre) {
si (friendSet.count(id)) res.push_back(id);
}
retour rés;
}
};
«» "

---

- Oui. 3. Analyse de la complexité

Formule métrique Valeur pour les contraintes
- C'est quoi ?
**Temps**= O(n + m)= `n ≤ 100`, `m ≤ 8` → < 120 ops
L'espace 8 ' entiers

L'analyse linéaire garantit que la solution se terminera en temps constant pour les limites données, ce qui la rendra idéale pour les questions d'entrevue et le code de production.

---

- Oui. 4. Le bon, le mauvais et le mauvais

Qu'aimer Qu'est-ce qu'un piège commun Qu'éviter
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bon**• Code minimal – juste un jeu + boucle.<br>• Fonctionne pour n'importe quel `n` (= 105 en théorie).<br>• LeetCode-friendly: O(1) memory & time.
**Bad** Si vous triez accidentellement `order` à nouveau, vous perdez l'ordre d'arrivée original. Autres
• Utilisation d'un tableau ou `boolean[]` de taille *n* pour les vérifications d'adhésion peut gaspiller de l'espace si *n* est énorme. Autres

> **Ligne de bottom:** Le hash‐set + un seul passage est le modèle *canonical* LeetCode pour le filtre un problème de subséquence. La maîtrise vous donne une victoire rapide pour de nombreuses questions d'entrevue.

---

- Oui. 5. Article de blog optimisé par le SEO

> **Titre**
> **=Ordre de finition de la restauration (Code de débit 3668): Guide rapide – Code bon, mauvais, mauvais et prêt à l'emploi**

---

5.1 Introduction

- Oui. Quel est le problème *Restaurer la commande*?
- Oui. Pourquoi cela compte pour les ingénieurs en logiciels (manipulation d'arrachage, opérations fixes).
- Mots-clés: LeetCode 3668, Restore finding order, Hash set interview, O(n) array filtrant.

5.2 Ventilation des problèmes

- Contraintes d'entrée (1 ≤ n ≤ 100, m ≤ 8).
- Clarifier l'ordre de finishing de la liste des amis.
- Afficher les entrées/sorties de l'échantillon.

5.3 Aperçu de la solution

- **Bien**: Construisez un ensemble d'amis → un seul scan → O(n + m).
- **Bad**: Tri inutile, O(n log n).
- **Ugly**: Utilisation de la recherche linéaire à l'intérieur de la boucle → O(n × m).

Utilisez des extraits de code pour Java, Python, C++.

5.4 Code détaillé

- Expliquez chaque ligne de l'implémentation Java.
- Afficher la version Python list-comprehension.
- Expliquer l'utilisation de C++ sans ordre.
- Mettre en évidence les compromis temps/espace.

5.5 Complexité et performance

- Tableau temps/espace.
- Discuter de l'évolutivité au-delà des contraintes (par exemple, n = 106).
- Soulignez pourquoi O(n + m) bat d'autres approches naïve.

5.6 Cas de bord et essais

- Des amis vides ? (Non autorisé par les contraintes mais les bonnes pratiques).
- Tous amis ?
- Un seul ami.
- Un mélange aléatoire d'ordre.

Montrer harnais de test rapide dans chaque langue.

5.7 Pièges communs d'entrevue

- Oublier que les amis sont déjà triés.
- Utilisation d'un vecteur/array au lieu d'un jeu de hachage, conduisant à des contrôles O(m).
- Suringénierie (par exemple trier à nouveau des "amis").

####5.8 Prise- Conseils pour les entrevues d'emploi

- Mentionnez l'astuce de set comme filtrant de Hash – un motif qui réapparaît souvent.
- Expliquez pourquoi l'adhésion à O(1) compte.
- Montrez comment s'adapter à des entrées plus grandes (unordered_map, bitset, etc.).

### 5.9 Fermeture

- Récapitulez, c'est mauvais.
- Encourager les lecteurs à pratiquer des problèmes similaires de sous-ensemble.
- CTA: "Essayez d'autres problèmes de LeetCode: 1467, 1466, 1692. (en milliers de dollars)

---

Liste de contrôle du référencement

Objet
- Oui.
Le titre comprend le code Leet 3668
Les titres H1/H2 utilisent des mots-clés
Nombre de mots 1500 à 2000 (profondeur adéquate)
Blocs de code formatés (Java, Python, C++) Autres
Description de la meta : Solve LeetCode 3668 en Java, Python et C++... Autres
Texte Alt pour images (le cas échéant)
Liens internes vers des tutoriels liés au LeetCode
Lien externe vers la page de problème LeetCode
Densité de mots-clés ~1% pour l'ordre de finition de la restauration, leetCode 3668

> ** Pensée finale :** La maîtrise de ce simple problème démontre votre capacité à traduire une exigence de haut niveau en une mise en œuvre propre et optimale – une compétence recherchée par chaque gestionnaire d'embauche.

---

- Oui. 6. Prêt à publier

Vous pouvez coller l'article dans une plateforme de blogging (Medium, dev.to, LinkedIn), ajouter les extraits de code, et le message sera à la fois *informatif* pour les lecteurs et *SEO-friendly* pour vous aider à débarquer ce travail d'ingénierie logicielle. Bon codage !