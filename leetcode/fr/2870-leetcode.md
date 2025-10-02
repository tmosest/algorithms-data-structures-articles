---
titre: LeetCode 2870. Nombre minimum d'opérations pour rendre la répartition vide -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2870 – Nombre minimum d'opérations pour rendre la répartition vide
### Medium=Java=Python=C++=99,63 %+ Beat

> **Problème**
> On vous donne un tableau 0 indexé `nums` d'entiers positifs.
> Dans une opération, vous pouvez supprimer **deux** éléments égaux ou **trois** éléments égaux.
> Trouvez le nombre minimum d'opérations nécessaires pour supprimer le tableau entier.
> Si c'est impossible, retourner **-1**.

> **Constraints**
> * < 2 ≤ longueur nominale ≤ 105 "
> * `1 ≤ nombres[i] ≤ 106`

---

## Aperçu de la solution

La seule chose qui compte est la fréquence **** de chaque valeur distincte.
Toutes les suppressions sont effectuées sur des éléments égaux, donc une fois que nous savons combien de copies d'une valeur existent, nous pouvons décider combien de suppressions de 2 ou 3 groupes sont nécessaires.

Stratégie de suppression de l'avidité
1. **Coup** la fréquence `cnt` de chaque nombre distinct en utilisant une carte de hachage / dictionnaire.
2. **Cas impossible** – si une fréquence est `1`, nous ne pouvons jamais supprimer cet élément (ni 2 ni 3). Retour `-1`.
3. Pour une fréquence `cnt`:
* Utilisez autant de suppressions de 3 groupes que possible: `cnt / 3`.
* Si un solde (`cnt % 3`) existe:
* Si le reste est `2`, nous pouvons le supprimer dans une autre opération (un 2-groupe).
* Si le reste est "1", nous devons d'abord transformer l'un des 3 groupes précédents en deux groupes (ou un groupe 2 + 1 restant).
Le nombre optimal est toujours `cnt / 3 + 1` parce que `cnt % 3 == Une opération supplémentaire.
4. Résumez les opérations pour tous les chiffres.

Cette stratégie gourmande est optimale car:
- Supprimer 3 à la fois est toujours mieux (ou égal) que supprimer 2 parce qu'il supprime plus d'éléments par opération.
- Chaque fois qu'un reste reste reste, la seule façon de consommer le reste 1 ou 2 est exactement une opération de plus.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Fréquences de comptage **O(n)**** **O(k)** (k = nombres distincts) Autres
Totalisation finale
**O(k)**

Le temps et l'espace sont linéaires, répondant facilement aux contraintes.

---

Mise en œuvre du code

Voici des solutions propres et prêtes à la production pour **Java**, **Python** et **C++**.

---

### Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
Services d'information
Carte<integer, integer> freq = nouveau HashMap<>();
pour (int x : nombres) {
freq.put(x, freq.getOrDefault(x, 0) + 1);
}

Int ops = 0;
pour (int count : freq.values()) {
si (compter) 1) retour -1; // impossible
ops += nombre / 3; // Suppressions de 3 groupes
si (comptez % 3 != 0) ops++; // une autre op pour le reste
}
les opérations de retour;
}
}
«» "

---

Python

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def minOperations(self, nombres: List[int]) -> Int:
freq = compteur(s)
ops = 0
pour cnt en valeurs fréq.():
si cnt == 1:
retour -1
cnt // 3
si cnt % 3:
Opérations += 1
retour ops
«» "

---

C++

'`cpp
#inclut <non-ordonné_map>
#incluez <vecteur>

solution de classe {
public:
int minOpérations(std:vector<int>& nums) {
std::unordered_map<int, int> freq;
pour (int x : nombres) ++freq[x];

Int ops = 0;
pour (const auto& [val, cnt] : freq) {
Si (cnt) 1) retour -1;
les opérations += cnt / 3;
si (cnt % 3) ++ops;
}
les opérations de retour;
}
};
«» "

---

## -D'une promenade détaillée (bon, mauvais, moche)

Catégorie: Ce qui a fonctionné: Ce qui est devenu court: Comment le réparer?
- C'est quoi ?
**Bon** - Compte de fréquence monopass. <br>- Mathématiques entiers simples (`/3`, `%3`). <br>- Poigne tous les cas de bord (`cnt == 1`, `cnt % 3`).
**Bad** - L'utilisation d'une carte non ordonnée pour jusqu'à 106` clés distinctes pourrait consommer ~8 Mo de RAM. <br>- En Java, les frais généraux `HashMap` peuvent pousser l'utilisation de la mémoire à un niveau élevé. Autres
**Éviter de gérer le "cnt" == 1" cas se traduit par "-1" manqué. <br>- Suringénierie en essayant des solutions complexes DP ou BFS. Gardez l'approche gourmande ; elle est à la fois optimale et succincte. Autres

Pièges communs

1. **Faire disparaître le "cnt". 1` check** → Certaines solutions retournent un nombre positif incorrectement.
2. ** Erreurs hors-par-un dans la manipulation du reste** – Rappelez-vous qu'un reste de `1` ajoute encore **une** opération supplémentaire.
3. **L'utilisation de la suppression de 2 groupes d'abord** peut conduire à des dénombrements sous-optimaux; toujours maximiser les 3 groupes d'abord.

---

## -Référencement optimalisé à emporter

- **Mots-clés**: *LeetCode 2870*, *Nombre minimum d'opérations pour faire Array Empty*, *solution Java*, *solution Python*, *solution C++*, *algorithme de la corde*, *carte de fréquence*, *entrevue de codage*, *entrevue de génie logiciel*, *structures de données*, *complexité du temps*, *complexité de l'espace*, *problème de codage de l'entrevue d'emploi*.
- **Suggestion de titre**: *=LeetCode 2870 – Nombre minimum d'opérations pour rendre Array vide – Java/Python/C++ Solution pour l'avidité
- **Meta Description**: Solve LeetCode 2870 en 5 minutes. Apprenez la stratégie cupide basée sur la fréquence, Java, Python, et C++ code, et compétences d'entretien maître. (en milliers de dollars)

---

La pensée finale

Le nombre minimal d'opérations pour rendre Array vide est une illustration classique qui ** observations simples donnent souvent les solutions les plus élégantes**. Compter les fréquences, détecter les cas impossibles, puis enlever avidement autant de 3 groupes que possible donne un algorithme linéaire, espace constant qui passe tous les cas de bord.

Maîtrisez ce modèle, et vous serez prêt à affronter de nombreux autres problèmes de LeetCode, basés sur la fréquence, lors d'entrevues. Bon codage 