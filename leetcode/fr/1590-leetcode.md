---
titre: LeetCode 1590. Rendre la somme divisible par P -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1590 – Faire de la somme divisible par P
> **Objectif** – Enlever le sous-parcours le plus petit* contigu de sorte que la somme des nombres restants soit divisible par `p`.
> **Constraint** – Le tableau entier ne peut pas être supprimé.

---

Récapitulation des problèmes (anglais + chinois)

**Anglais**
«» "
Entrée: nombres = [3,1,4,2], p = 6
Produit : 1 (supprimer [4])
«» "

**Chinois *
> "P"
> C'est pas vrai.

---

Aperçu de la solution

1. ** Calculer la somme totale** `S`.
*Si* `S % p == 0`, nous sommes déjà bons → retourner `0`.
2. **Objectif du sous-appel**
La sous-tribu que nous supprimons doit avoir une somme dont le reste modulo `p` est égal à
«rem = S % p».
3. **Préfixer les montants + HashMap**
* Itérer une fois à travers le tableau en maintenant un préfixe courant sum modulo `p`.
* Conservez l'index *dernier* auquel chaque valeur modulo apparaît sur une carte de hachage.
* Pour chaque index `i` avec le préfixe `cur` actuel, nous voulons un préfixe précédent
"prévu" de telle sorte que
`cur – prev ↓ rem (mod p)` → `prev ↓ (cur – rem) mod p`.
Si une telle "prev` existe, la sous-tribu `(prev+1 ... i)" est un candidat.
4. **Tirer la longueur minimale**.
5. **Si aucun candidat** → retourner `-1`.
6. **Important** – ne **pas** permettre à la longueur du candidat d'être l'ensemble du tableau.

Cela donne **O(n)** temps et **O(n)** espace auxiliaire.
Tous les calculs utilisent des entiers 64 bits pour éviter les débordements.

---

Mise en œuvre du code

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Chaque dossier est autonome et suit la même logique.

- Oui. 1. Java 17

"Java
Importer java.util. HashMap;

solution de classe publique {
***
* Trouvez la longueur du plus petit sous-arraché à enlever
* pour que la somme des éléments restants soit divisible par p.
*
* @param nombres tableau d'entiers positifs
* @param p diviseur
* @retour longueur minimale subarray ou -1 si impossible
*/
public int minSubarray(int[] nums, int p) {
long total = 0;
pour (int x : nombres) total += x;

int rem = (int) (total % p);
si (rem) 0) retour 0; // déjà divisible

HashMap<entier, entier> pref = nouveau HashMap<>();
pref.put(0, -1); // poignée préfixe qui commence à 0
préfixe long = 0;
int best = nombres.longueur; // initialiser avec le pire des cas

pour (int i = 0; i < nombres de longueur; i++) {
préfixe += nombres[i];
int cur = (int) (préfixe % p);
besoin d'int = (cur - rem + p) % p; // réglage modulo

Integer prevIdx = pref.get(besoins);
si (prevIdx != null) {
best = Math.min (best, i - prevIdx);
}
pref.put(cur, i); // conserver le dernier index
}

retour meilleur == nums.longueur ? -1 : meilleur;
}
}
«» "

- Oui. 2. Python 3

'`python
de taper l'importation Liste

Solution de classe:
def minSubarray(self, nombres: List[int], p: int) -> Int:
total = somme(s)
rem = total % p
si rem == 0:
retour 0

pref = {0: -1} # prefix_mod -> dernier_index
préfixe = 0
best = len(nums)

pour i, v in énumérate(nums):
préfixe += v
cur = préfixe % p
besoin = (cur - rem) % p
si nécessaire en préf:
best = min(meilleur, i - besoin])
pref[cur] = i

retour -1 si le meilleur == len(nums) autre meilleur
«» "

- Oui. 3. C++17

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
#incluez <algorithme>

solution de classe {
public:
Int minSubarray(std:vector<int>& nums, int p) {
long total = 0;
pour (int x : nombres) total += x;

int rem = static_cast<int>(total % p);
Si (rem) 0) retour 0;

std::unordered_map<int, int> pref; // mod -> dernier indice
pref[0] = -1;
préfixe long = 0;
int best = static_cast<int>(nums.size());

pour (int i = 0; i < (int)nums.size(); ++i) {
préfixe += nombres[i];
int cur = static_cast<int>(préfixe % p);
besoin d'int = (cur - rem + p) % p;

auto it = pref.find(besoins);
si (it != pref.end())
best = md::min(best, i - it->seconde);

pref[cur] = i; // conserver la position la plus récente
}

Return best == nums.size() ? -1 : meilleur;
}
};
«» "

---

Article du blog : Le bon, le mauvais et l'atroce de LeetCode 1590

> *Make Sum Divisible by P. – une question d'entrevue trompeusement simple qui cache des pièges subtils. Laissez tomber, explorez les cas de bord, et apprenez à le clouer dans votre prochain entretien de codage. *

C'est pas vrai. Bon – Ce qui fait Ce problème est amical

Aspect Pourquoi ça aide
C'est pas vrai.
Un scan linéaire avec un hashmap donne du temps à O(n). Autres
**Reste déterministe**Le reste de l'objectif est simplement « % total p ». Autres
**Claright Mathematical Insight** Autres
Autres **Wide Test Coverage**= LeetCode=2 tests cachés cocher les cas bord: suppression vide, cas impossibles, grands nombres. Autres

- Oui. Mauvais – Les coins tricky

Pourquoi ça casse
C'est quoi ?
**Excédent total** peut être > 2^31‐1. Utilisez 64 bits (long'/long'). Autres
**Modulo avec nombres négatifs**. En Java/C++ `-1 % p` est négatif. Utiliser `(cur - rem + p) % p`. Autres
**Remplacement de l'ensemble du tableau** La déclaration l'interdit. Un "minimum de n" ne retournera pas `n` au lieu de `-1`. Autres
**Initialisation de HashMap**= Oublier d'insérer `0 → -1` manque les candidats qui commencent à index `0`. Autres
**L'utilisation de la première occurrence de la première occurrence de la seule occurrence**. Conservez l'occurrence la plus tardive pour chaque module. Autres
**O(n2) Brute-Force** Autres

Quand l'intervieweur t'engueule

> L'intervieweur pourrait vous demander d'adapter la solution pour **mises à jour dynamiques** ou pour ** gérer plusieurs requêtes**. Le principe sous-jacent tient encore, mais vous devrez :

* **Pré-calculer les sommes du préfixe** et les stocker dans un tableau.
* Utilisez **prefix sum difference** pour répondre aux requêtes en O(1).
* Pour les mises à jour, reconstruire le hashmap ou utiliser un arbre de segment si de nombreuses mises à jour sont nécessaires.

C'est pas vrai. Liste de vérification de l'entrevue-réalisation

- **Lisez l'énoncé attentivement** – notez que la clause "R" ne peut pas supprimer l'ensemble du tableau.
- **Utilisez l'arithmétique 64 bits** partout.
- **Normalisez les résultats modulo** pour être non-négatif avant de regarder le plan de hash.
- **Initialiser le hashmap avec `{0: -1}`** – ceci gère les sous-réseaux qui commencent à l'index 0.
- **Retourner `-1` si la meilleure longueur correspond à la taille du tableau**.
- ** Expliquez votre algorithme en anglais clair** avant de plonger dans le code.

> **Astuce :** Pratiquez le modèle --préfixe-sum + hashmap sur d'autres problèmes (p. ex., *la plus longue des sous-arraies avec Sum Zero*, *la taille maximale des sous-arrachages équivaut à k*, *la division des sous-arras*). Une fois que vous le maîtrisez, vous allez voir que beaucoup de problèmes difficiles se résument à un modèle similaire.

Mots-clefs

* LeetCode 1590
* Rendre la somme divisible par P
* Problème de codage de l'entrevue
* Solution Java
* Solution Python
* Solution C++
* Préfixe la somme
* Technique HashMap
* complexité de l'algorithme
* Données Entretien des structures

- Oui. Prise finale Loin

> **Le cœur de ce problème est un beau mélange d'arithmétique et de structure de données. **
> - *Bien*: Temps linéaire, objectif clair restant.
> - *Bad*: Attention au débordement, au modulo négatif et à la restriction de la gamme complète.
> - *Ugly*: Lorsque vous oubliez le hashmap ou essayez une force de brute quadratique, le harnais d'essai vous indiquera immédiatement.

Si vous pouvez articuler ce raisonnement lors d'une entrevue et remettre l'un des trois extraits de code propres et prêts à la production ci-dessus, vous serez un candidat fort pour tout rôle algorithmique. Bon codage !

---

**Sentez libre de copier les extraits de code dans votre IDE et exécutez les cas de test fournis. Bonne chance avec votre entretien ! * *