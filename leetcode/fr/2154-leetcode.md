---
titre: LeetCode 2154. Continuer à multiplier Valeurs trouvées par deux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2154 – Continuez à multiplier Valeurs trouvées par deux

*Le bon, le mauvais, et le laid d'un problème simple mais convivial d'interview.

---

- Oui. 1. Résumé du problème (facile)

Vous êtes donné un tableau entier `nums` et un entier `original`.
Alors que `original` est présent dans `nums`, vous le doublez (`original *= 2`).
Retourner la première valeur qui est **not** trouvée dans `nums`.

> **Input** – «nums = [5,3,6,1,12]», «original = 3»
> ** Sortie** – 24 '
> **Explication**
> 3 → 6 → 12 → 24 (24 n'est pas dans le tableau, donc nous arrêtons)

**Contrôles* *

- "1 ≤ longueur nominale ≤ 1000"
- `1 ≤ nums[i], origine ≤ 1000`

---

- Oui. 2. Pourquoi ce problème est une bonne question d'entrevue

C'est bien, c'est mal.
C'est pas vrai.
**Simplicité** – Il teste la pensée algorithmique de base sans vous noyer dans la plaque de chaudière. **Pièges d'urgence** – Oublier de s'arrêter lorsque la valeur est absente, ou mal gérer le débordement entier si les contraintes étaient plus grandes. Autres
**Soutien linguistique multiple** – Vous pouvez démontrer la même logique en Java, Python, C++ – idéal pour un portfolio. Autres
**Échange de temps** – Vous apprenez pourquoi une structure basée sur le hachage est l'ajustement naturel.

---

- Oui. 3. Algorithme – Recherche rapide avec un HashSet

1. ** Convertir les «nums» en «HashSet»** – donne une moyenne des vérifications d'adhésion O(1).
2. **Loop** alors que `original` est contenu dans l'ensemble:
`original *= 2'
3. Retourner `original` lorsque la boucle sort.

**Pourquoi ça marche* *

- Oui. Chaque itération garantit que la valeur actuelle est présente, donc nous sommes autorisés à la doubler.
- Oui. Dès que la valeur est manquante, aucun doublement supplémentaire n'est possible – nous renvoyons le premier nombre de "missing".
- Parce que nous ne balayons l'ensemble qu'une seule fois par itération et que chaque itération augmente exponentiellement `original`, la boucle se termine rapidement (au plus ~10 étapes pour les contraintes données).

---

- Oui. 4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Bâtiment HashSet ("O(n)") Autres
Chaque itération de la boucle (recherche « O(1) » + « O(1) » multiplier) Autres
**O(n + réponse au journal)**

Avec "nums.longueur ≤ 1000", cela est bien en dessous de toute limite de temps pratique.

---

- Oui. 5. Code – 3 langues

Voici des solutions propres et idiomatiques pour **Java, Python et C++**. N'hésitez pas à les copier, à les coller et à les exécuter dans votre éditeur préféré.

##### 5.1 Java (style LeetCode)

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe {
public int findFinalValue(int[] nums, int original) {
Définir<integer> set = nouveau HashSet<>();
pour (int num : nums) set.add(num);

pendant que (set.contient(original)) {
original <<= 1; // original *= 2
}
l'original du retour;
}
}
«» "

5.2 Python

'`python
def find_final_value(nums: list[int], original: int) -> Int:
nums_set = set(nums) # O(n) time, espace O(n)

alors que original dans nums_set: # O(1) recherche moyenne
originale <<= 1 # multiplier par 2

retour original
«» "

C++

'`cpp
#inclut <unordered_set>
#incluez <vecteur>

solution de classe {
public:
int findFinalValue(std::vector<int>& nums, int original) {
std::unordered_set<int> st(nums.begin(), nums.end());
pendant que (premier compte(original)) {
originale <<= 1; // multiplier par 2
}
l'original du retour;
}
};
«» "

---

- Oui. 6. Erreurs courantes et comment les éviter

Erreurs dans les résultats
- C'est quoi ?
En utilisant une `Liste` et `list.contient()` à l'intérieur du temps de boucle O(n2), peut TLE sur des contraintes plus grandes. Autres
Autres Oublier l'état de la boucle** (pendant que (set.contient(original))) Toujours garder la boucle avec le contrôle de l'existence.
Utiliser `originale * 2` au lieu de `originale <<= 1` en Java/C++. 1' est un tour de changement qui est un peu plus rapide en boucles serrées
Dans ce problème, les contraintes l'empêchent, mais pour les plus grandes entrées, il s'agit d'un risque.

---

- Oui. 7. Stratégie d ' essai

Texte
1. Cas de base:
- nombres = [1,2,4,8], original = 1 -> 16
- nombres = [2,7,9], original = 4 -> 4
2. Cas de bord:
- tableau d'élément unique, correspondances originales / ne correspond pas
- contraintes maximales (1000 éléments, tous 1000)
3. Essais randomisés :
- Générer des tableaux aléatoires et des originaux, comparer la force brute par rapport à l'implémentation du jeu de hachage
«» "

---

- Oui. 8. Pourquoi ce blog aide votre travail de chasse

- **Mots-clés compatibles avec le référencement**: LeetCode 2154, Keep Multiplying Found Values by Two, Solution Java, Solution Python, Solution C++, Ensemble Hash, Interview Algorithme.
- **Showcases**: compétence multilingue, compréhension claire des structures de données, analyse du temps et de l'espace, traitement des cas de bord – tous essentiels pour une entrevue d'ingénierie logicielle.
- **Portfolio**: Ajoutez les extraits de code à votre blog personnel ou GitHub README; les recruteurs aiment voir des solutions propres et commentées.

---

- Oui. 9. A emporter

Ce problème est un puzzle classique qui teste si vous pouvez choisir la bonne structure de données et écrire un code concis et correct. En le maîtrisant, vous démontrez :

- Analyse rapide des problèmes
- Sélection efficace de la structure des données
- Implémentation propre et idiomatique dans votre langue préférée
- Sensibilisation aux pièges communs

Bonne chance pour écraser votre prochain entretien de codage ! C'est ce qu'il a dit