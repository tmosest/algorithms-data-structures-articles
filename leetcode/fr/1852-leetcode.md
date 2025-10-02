---
titre: LeetCode 1852. Nombres distincts dans chaque sous-arrachage - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1852 – Distinct Nombres dans chaque sous-aire
**Java / Python / Implémentations C++ + un blog d'interviews de bonne qualité* *

> **Mots clés**: LeetCode 1852, nombres distincts, sous-array, fenêtre coulissante, Java, Python, C++, interview prep, algorithme, complexité temporelle, complexité spatiale, interview de codage, entretien d'emploi, structure de données, hashmap, dictionnaire, vecteur.

---

- Oui. 1. Récapitulation des problèmes

> **Donné** d'un nombre entier (longueur `n`) et d'un nombre entier `k` (`1 ≤ k ≤ n`).
> **Tâche** : Pour chaque fenêtre contiguë de taille `k`, affichez le nombre d'éléments **distincts**.

«» "
Entrée : nombres = [1,2,3,2,1,3], k = 3
Produit : [3,2,2,2,3]
«» "

La longueur du tableau peut être jusqu'à `10^5`, de sorte qu'une solution de force brute `O(n·k)' sera temps-out.

---

- Oui. 2. Stratégie de solution – Fenêtre coulissante + carte Hash

1. **Window**: Gardez une fenêtre `[gauche, droite)` de la taille `k`.
2. **Carte de bord** : Conservez chaque fréquence de nombre dans la fenêtre.
3. **Déplacer**:
* Ajouter `nums[right]` à la carte (augmenter son nombre).
* Si la taille de la fenêtre atteint `k`, enregistrer `map.size()` (nombre de clés).
* Faites glisser la fenêtre: supprimer `nums[left]` (diminuer son nombre, effacer si zéro).
4. **Répéter** jusqu'à ce que `droit` atteigne `n`.

Cela fonctionne dans le temps `O(n)` et utilise `O(k)` (au plus `k` nombres distincts) espace.

---

- Oui. 3. Mise en œuvre du code

> Toutes les implémentations suivent la même logique, mais utilisent des constructions spécifiques au langage.

#### 3.1 Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
nombres(int[] nombres, int k) {
si (nums) null=0 nums.longueur < k) retournent la nouvelle int[0];

int n = longueur nums;
int[] ans = nouvelle int[n - k + 1];
Carte<integer, integer> freq = nouveau HashMap<>();

int gauche = 0, droite = 0, idx = 0;

pendant que (droite < n) {
freq.put(nums[right], freq.getOrDefault(nums[right], 0) + 1);
droite++;

si (à droite - à gauche) k) {
ans[idx++] = freq.size();

Int gauche Val = nombres[left++];
si (--freq.get(leftVal)) 0) freq.remove(leftVal);
}
}
le retour des an;
}
}
«» "

> **Complexités** – Temps `O(n)`, Espace `O(k)`.

---

3.2 Python

'`python
de taper l'importation Liste
de collections importer par défautdict

Solution de classe:
def distinctNumbers(self, nombres: List[int], k: int) -> Liste[int]:
à moins de nombres ou de nombres < k:
retour []

n = len(nums)
ans = []
freq = defaultdict(int)

gauche = 0
pour droite, val in énumérate(nums):
freq[val] += 1

Si droite - gauche + 1 == k:
(en français)
gauche_val = nombres[gauche]
freq[left_val] -= 1
si freq[left_val] == 0:
del freq[left_val]
gauche += 1
retour et
«» "

> **Complexités** – Temps `O(n)`, Espace `O(k)`.

---

### 3.3 C++

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> distinctNombres(vecteur<int>& nums, int k) {
si (nums.vide()="nums.size() < k) retourne {};

int n = nombres.size();
vecteur <int> ans;
unordered_map<int, int> freq;

Int gauche = 0;
pour (int droite = 0; droite < n; ++ droite) {
++freq[nums[right]];

si (droite - gauche + 1 == k) {
as.push_back(freq.size());

Int gauche Val = nombres[left++];
Si (--freq[leftVal]] 0) freq.erase (leftVal);
}
}
le retour des an;
}
};
«» "

> **Complexités** – Temps `O(n)`, Espace `O(k)`.

---

- Oui. 4. Bon, mauvais, mauvais Entretien

**Aspect**
C'est pas vrai.
**Concept**=Fenêtre coulissante + carte de fréquence – classique, facile à interviewer.= Aucune (facile à mettre en œuvre). Aucun.
**Complexité temporelle**= `O(n)` – optimum pour `n = 10^5`.=== Brute-force `O(n·k)` échoue sur une grande entrée.==== Recomptage de comptes distincts de zéro pour chaque fenêtre. Autres
Autres **Complexité spatiale**= `O(k)` – il suffit de compter pour la fenêtre actuelle.== = Stocker toutes les sommes préfixes ou les ensembles distincts précalculés consomme `= `O(n·k)`.== = Utiliser un tableau de taille `max(nums)+1` (`10^5`) lorsque seul `k` distinct nécessaire - mémoire gaspillée. Autres
**Edge Cases**=Poignées `k = 1`, `k = n`, nombres répétés.=== Éviter de supprimer la clé lorsque le nombre passe à zéro → = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = Autres
**Nuances de langue**=Java=s `HashMap.getOrDefault`, Python=s `defaultdict`, C++=s `unordered_map`.=____________________________________________________________________________________________________________________________________________________________________________________________________________ Autres

> **Key Take‐away**: Utilisez une structure de hachage *non ordonnée*, mettez à jour les comptes en `O(1)` par étape et supprimez toujours les entrées lorsque le nombre atteint zéro pour garder la taille de la carte exacte.

---

- Oui. 5. Essais et bords Liste de contrôle des cas

Autres Description du test
- C'est quoi ?
"nums = [1,1,1], k = 1`. Autres
Nombres = [1,2,3,4], k = 4 '
"nums = [5], k = 1"
Tous les duplicata
Nombres = [1,2,1,2,1,2], k = 2 ' Exclusion Autres

Exécuter le code fourni avec un harnais d'essai unitaire ou une méthode `main` pour valider.

---

- Oui. 6. Conseils de performance

1. **Éviter la création d'objets inutiles** – réutiliser la même carte/dicte; effacer seulement lorsque nécessaire.
2. **Préférence `unordered_map` sur `map` en C++** pour les recherches moyennes `O(1)`.
3. **En Java, utiliser `HashMap` avec la capacité initiale** `k` pour réduire la remise en état (`new HashMap<>(k)`).
4. **Retour rapide** pour les cas de bord (`k > n`, `nums == null`) pour gagner du temps.

---

- Oui. 7. Histoire d'entrevue – La fenêtre coulissante Saga

Une fois, j'ai fait face à une question de leetcode demandant des comptes distincts dans chaque sous-arrachage. Mon premier instinct a été une boucle imbriquée; après quelques minutes de débordement de la pile, je me suis souvenu du tour de la fenêtre coulissante. J'ai codé une carte de hachage pour garder les fréquences et glisser la fenêtre dans le temps linéaire. L'intervieweur a été impressionné par la complexité `O(n)` et la suppression nette des clés lorsque les nombres sont tombés à zéro. Ce petit détail sur la suppression des touches zéro nombre a sauvé ma solution d'être mal sur les cas de test avec de nombreuses répétitions.

---

- Oui. 8. Pensées finales

- **Pourquoi cela compte pour un entretien d'embauche**:
* Démontre la maîtrise de deux structures de données de base : les tables de hachage et les fenêtres coulissantes.
* Affiche la sensibilisation aux compromis entre l'espace temporel.
* Indique la manipulation soigneuse des cas de bord et la gestion de la mémoire.

- ** Prochaines étapes** :
* Variantes de la pratique – Coudre des valeurs distinctes dans une plage de valeurs (interrogations hors ligne).
* Explorer des structures de données plus avancées: `Fenwick Tree` ou `Segment Tree` pour les mises à jour dynamiques.
* Construisez une repo personnelle de solutions de fenêtre coulissante pour un rappel rapide lors des entrevues.

---

Référence Méta Description

> Code du leet 1852 – Distinct Nombres dans chaque sous-aire. Apprenez les solutions Java, Python et C++ pour la fenêtre coulissante, l'analyse du temps et de l'espace et les conseils prêts à l'entrevue. Boostez votre codage interview prep et atterrissez votre travail de rêve. (en milliers de dollars)

---

Joyeux codage, et que le compte distinct soit toujours en votre faveur!