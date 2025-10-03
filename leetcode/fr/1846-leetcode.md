---
titre: LeetCode 1846. Élément maximum après la diminution et la réorganisation -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La maîtrise du LeetCode 1846
**Élément maximal après la diminution et la réorganisation** – *Les bons, les mauvais et les méchants*

---

### TL;DR
* **Problème** – Vous pouvez réorganiser un tableau et diminuer n'importe quel élément à n'importe quel entier positif plus petit.
* **Objectif** – Après toutes les opérations, le premier élément doit être `1` et les éléments consécutifs doivent différer au plus `1`. Retournez la valeur **maximum possible** dans le tableau.
* **Réponse** – Tri, puis marcher une fois et augmenter un maximum de course chaque fois que vous voyez un nombre plus grand que lui.
* **Complexité** – temps « O(n log n) », espace supplémentaire « O(1) » (en ignorant le tri des frais généraux).

---

Rétablissement des problèmes

Texte
Entrée: arr = [2,2,1,2,1]
Produit: 2

Entrée: arr = [100,1 1000]
Produit : 3
«» "

Vous pouvez **toute fois**:
1. ** Diminuer** une valeur à un entier positif plus petit.
2. **Réorganiser** le tableau dans tout ordre.

Après tous les changements:
- "arr[0]". 1'
- `abs(arr[i] - arr[i-1]) ≤ 1` pour tous `i > 0'

Retourne l'élément le plus important qui peut exister dans un tel tableau valide.

> **Constraints**
> `1 ≤ longueur d'arrondi ≤ 105 "
> `1 ≤ arr[i] ≤ 109 "

---

## 2--Intuition & --Bien – Pourquoi trier + fonctionne avidement

Autres Ce que nous pouvons faire
-- -- -- -- -- --
Diminuer tout élément
Nous devons garder le **premier élément** comme `1`

Parce qu'on ne peut pas augmenter les nombres, la stratégie «Best» est d'utiliser les plus petites valeurs pour ensemencer la séquence**.
Triez le tableau ascendant: les plus petits nombres viennent en premier, afin que nous puissions les assigner en toute sécurité aux positions dont nous avons besoin.
Une fois le tableau trié, nous n'avons qu'à décider ** combien d'entiers consécutifs** nous pouvons construire à partir de `1`.

Laissez `maxVal` être le plus grand entier que nous ayons déjà sécurisé.
Lorsque nous regardons l'élément suivant `x` dans le tableau trié:
- Si `x` > `maxVal`, nous pouvons *diminuer* `x` en `maxVal + 1`.
→ augmenter `maxVal` par `1`.
- Sinon `x` n'est pas assez grand pour étendre la chaîne; sautez-la.

Cette règle avide garantit la plus longue chaîne possible car:
- Oui. L'ordre trié garantit que nous considérons toujours la valeur **la plus petite possible** qui pourrait étendre la chaîne suivante.
- La diminution d'un plus grand nombre ne fait jamais de mal à une partie antérieure de la chaîne – nous sommes tout simplement en train de sauver un plus grand nombre pour plus tard.

---

- Oui. "Bad" – Pièges potentiels que vous pourriez rencontrer

Pourquoi il échoue
- C'est quoi ?
Autres **Démarrer `maxVal` à `0`**=Le premier élément doit être `1`. Si vous commencez à `0`, vous compterez mal un supplément "1". Autres
**Le premier élément après tri pourrait ne pas être `1`. Cependant, nous *force* `1` comme premier élément, donc nous ignorons la valeur réelle à l'indice `0`. Utiliser `maxVal = 1` *avant* la boucle. Autres
**Utiliser `pour (int x : arr)`**=Vous comparerez `x` avec `maxVal` avant de vous définir la chaîne actuelle; cela peut sur-compter. * de l'indice 1** vers l'avant, car l'indice 0 est toujours « 1 ». Autres
**O(n2) simulation naïve**.La diminution de tous les éléments individuellement est impossible pour `n = 105`. Autres

---

N° 4 : Où le problème devient difficile

1. **Tous les nombres sont égaux** – par exemple, «[1, 2, 2, 2]».
L'algorithme avide saute automatiquement des `2` supplémentaires parce qu'ils ne peuvent pas être réduits à un nouveau entier.

2. **Très grands nombres** – par exemple, «[109, 109, 109]».
Après tri, nous n'ajoutons toujours qu'un entier de plus par élément parce que nous sommes obligés de diminuer.

3. **Petits tableaux** – par exemple, «[1]».
La boucle ne tourne jamais, mais nous devons quand même retourner `1`.

Manipulation de ces cas d'angle est trivial avec l'algorithme avide – assurez-vous que la boucle ne fonctionne que lorsque `arr.longueur > 1`.

---

Code de solution

Voici des solutions propres et idiomatiques pour **Python 3**, **Java 17** et **C++17**.
Tous les trois partagent le même temps O(n log n) et l'espace O(1) (à l'exception du tri des frais généraux).

5.1 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def maximumElementAfterDecrementingAndRearranging(self, arr: List[int]) -> Int:
"""
:type arr: Liste[int]
:rtype : int
"""
arr.sort() # O(n log n)
max_val = 1 # nous avons déjà sécurisé 1

# passer par le tableau trié à partir de l'index 1
pour x dans arr[1:]:
si x > max_val: # peut étendre la chaîne
max_val += 1

_retour maxval
«» "

#### 5.2 Java 17

"Java
Importer java.util. Les tableaux;

solution de classe {
public int maximumÉlémentAprèsdécretetréaménagement(int[] arr) {
Tableaux.sort(arr); // O(n log n)
int maxVal = 1; // nous avons déjà 1

pour (int i = 1; i < arr.longueur; i++) {
si (arr[i] > maxVal) {
maxVal++; // étendre la chaîne
}
}
retour maxVal;
}
}
«» "

Numéro 5.3 C++17

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
Int maximumÉlémentAprèsDécretetRéaménagement(std::vector<int>& arr) {
À l'exclusion de: // O(n log n)
int maxVal = 1; // nous avons déjà 1

pour (size_t i = 1; i < arr.size(); ++i) {
si (arr[i] > maxVal) {
++maxVal; // étendre la chaîne
}
}
retour maxVal;
}
};
«» "

Les trois solutions effectuent un **passe linéaire unique** après tri, et elles sont O(1) espace supplémentaire (en ignorant la pile de récursion utilisée par la routine de tri intégrée).

---

Analyse de complexité

Opération Complexité
C'est quoi ?
Classer le temps `O(n log n)`, `O(1)` (ou `O(n)` si vous comptez le tas utilisé par le groupe rapide)
Une seule analyse linéaire du temps `O(n)`, `O(1)` espace
**Total**** **«O(n log n)» temps, «O(1)» espace auxiliaire**

> **Pourquoi pas "O(n)"? **
> Les seules opérations sous‐`O(n)` disponibles sont des scans linéaires.
> Le tri est inévitable parce que vous devez savoir *qui* valeurs sont assez grandes pour étendre la chaîne; sans tri, vous pourriez sauter un nombre qui aurait pu être réduit à une valeur utile.

---

# # 7- Liste de contrôle des cas

Pourquoi ?
- C'est quoi ?
Seul le premier élément existe. Autres
"[5, 5, 5] "" `2`" Trié → `[5,5]". Le premier `5` peut devenir `2`. Autres
Chaque nombre énorme peut être réduit à 2, 3, ..., n`.
"[1, 100, 100, 100] "" `4`" `1` → `2` → `3` → `4`. Autres

Toujours tester avec un mélange de petits, égaux, et des nombres énormes.

---

- Oui. Exemple de code de conducteur et tests unitaires

Voici un moyen rapide de vérifier l'implémentation dans n'importe quelle langue.

'`python
def run_tests():
essais = [
([2,2,1,2,1], 2),
([100,1 000], 3),
[1,2,2,2], 2),
([10**9, 10**9, 10**9], 3),
([1], 1),
- Oui.

pour arr, attendu dans les essais:
sol = Solution()
res = sol.maximumÉlémentAprèsDécretetRéaménagement(arr.copy())
affermissez res == attendu, f"FAIL: {arr} → {res} (attendu {attendu})"
print("Tous les tests sont passés!")

si __nom__ == "__main__" :
run_tests()
«» "

Ajouter le même harnais de test en Java et C++ (utiliser JUnit / Google Testez si vous vous préparez aux entrevues).

---

## 9=1 Conseils d'entrevue

Conseil Pourquoi c'est important
-- -- -- -- --
** Expliquez l'invariant gourmand** – Le plus grand entier que nous ayons déjà garanti montre que vous comprenez l'état de l'algorithme. Autres
**Mention l'impossibilité d'augmenter les nombres** Autres
**Afficher la preuve O(n log n)** – le tri domine. Autres
**Discuss corner Cases** – un seul élément, tous égaux, des valeurs énormes. Autres
Autres **Parler des compromis spatiaux** – `Arrays.sort` en Java utilise `O(log n)` espace de la pile; `std::sort` utilise `O(log n)` profondeur de récursion. Autres

---

Mots clés utiles pour la recherche d'emploi

- **LeetCode 1846**
- **Élément maximal après diminution et réaménagement* *
- **Questions sur l'entrevue de LeetCode* *
- **Algorithme de Java**
- **Algorithme Python**
- Algorithme **C++**
- **Sortie + Greedy**
- **O(n log n) complexité du temps* *
- **Entretien de l'ingénieur logiciel prép**
- **Structures de données et algorithmes**

*Ajouter ces balises à votre blog, Linked Dans l'article, ou GitHub README pour attirer les recruteurs à la recherche de la maîtrise LeetCode. *

---

Conclusion

La partie "good" de LeetCode 1846 est son élégance : **on trie +on passe** donne la réponse optimale.
La partie «bad» est la tentation de surpenser – certaines personnes essaient de simuler les opérations, entraînant des explosions quadratiques.
La partie "gugly" gère le boîtier d'angle subtil lorsque l'élément trié est *pas* assez grand pour prolonger la chaîne – vous le sautez simplement.

Avec cette solution propre dans **Python, Java et C++**, vous pouvez résoudre le problème avec confiance dans n'importe quel réglage d'entretien.

> **Pro‐tip** – Lorsque vous êtes coincé sur un problème de LeetCode qui permet de diminuer ou de réorganiser, demandez-vous: *Puis-je trier le tableau d'abord? * Souvent la réponse est oui, et un passage gourmand suivra.

Bonne chance sur votre interview, et n'hésitez pas à **partager ce post** sur Linked Dans ou Twitter pour montrer aux recruteurs que vous maîtrisez déjà les solutions les plus efficaces! C'est ce qu'il a dit.

---

**#LeetCode #Interview Préparation #Java #Python #C++ #Algorithme #Greedy #LogicielEngineer #JobInterview* *