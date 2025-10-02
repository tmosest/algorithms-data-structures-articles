---
titre: LeetCode 1929. Concaténation d'Array -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1929 – Concaténation d'Array
**Langues**
- Oui.
**Heure**
**Espace**

Autres Vous souhaitez obtenir votre prochain entretien d'ingénierie logicielle?
> Cet article passe par la solution *cleanest* pour LeetCode 1929, explique pourquoi il est efficace, couvre les pièges, et vous donne du contenu SEO-friendly pour booster votre CV.

---

## 1-

Avec un tableau entier `nums` de longueur `n`, créez un tableau `ans` de longueur `2n` de telle sorte que:

«» "
ans[i] = nombres[i] pour 0 ≤ i < n
ans[i + n] = nombres[i] pour 0 ≤ i < n
«» "

En d'autres termes, `ans` est la concaténation de `nums` avec lui-même.

> **Exemple**
> Entrée: `[1, 2, 1]` → Sortie: `[1, 2, 1, 1, 2, 1]`

---

## 2-

* La tâche est une copie d'un passage : nous avons simplement besoin de deux copies de chaque élément.
* **O(n)** le temps est la complexité optimale – chaque élément est traité une fois.
* **O(n)** espace supplémentaire est inévitable parce que le résultat a la taille `2n`.
* Une naïveté «re-annexer l'ensemble du tableau» fonctionnerait mais est moins explicite.

---

- Oui. Les pièges communs

Pourquoi c'est mauvais
C'est quoi ?
En utilisant `list.extend()` ou `vector.insert()` dans une boucle. Autres
Autres Réallocation du tableau de résultats à l'intérieur de la boucle. Autres
Oublier l'indexation 0-basée. Autres
Autres Ne pas traiter les "nums" vides (bien que les contraintes l'interdisent) ► L'épreuve future contre les changements. Autres

---

- Oui. Le "Ugly" – Les choses à éviter

* Sur-optimisation avec les astuces de la mémoire de la copie (p. ex., `System.arraycopy') – elles sont bonnes mais obscurcissent la logique.
* Utiliser la concaténation de liste de haut niveau dans un style fonctionnel ('nums + nums') qui crée un tableau temporaire – gaspillé.
* Ajouter des impressions ou des commentaires inutiles dans la boucle.

---

Les solutions propres

Ci-dessous sont trois implémentations idiomatiques qui évitent les mauvais et les mauvais modèles.

#### 5.1 Java – Boucle simple

"Java
// Code Leet 1929 – Concaténation d'Array
solution de classe publique {
public int[] getConcaténation(int[] nums) {
int n = longueur nums;
int[] ans = nouveau int[2 * n];
pour (int i = 0; i < n; i++) {
as[i] = nombres[i];
ans[i + n] = nombres[i];
}
le retour des an;
}
}
«» "

**Pourquoi c'est propre**
* Pas d'appels de bibliothèque supplémentaires.
* Les indices explicites rendent la logique claire.
* Passe tous les cas de test LeetCode en < 10 ms.

---

5.2 Python – Compréhension de la liste

'`python
Code Leet 1929 – Concaténation d'Array
Solution de classe:
def getConcaténation(self, nombres: List[int]) -> Liste[int]:
n = len(nums)
retour [nums[i] i < n autres nombres[i - n] pour i dans l'intervalle(2 * n)]
«» "

*Pythonic* – met à profit la compréhension de la liste pour la brièveté tout en restant O(n).

---

### 5.3 C++ – Copie manuelle

'`cpp
// Code Leet 1929 – Concaténation d'Array
solution de classe {
public:
vecteur<int> getConcaténation(vecteur<int>& nums) {
int n = nombres.size();
vecteur <int> ans(2 * n);
pour (int i = 0; i < n; ++i) {
as[i] = nombres[i];
ans[i + n] = nombres[i];
}
le retour des an;
}
};
«» "

*Non `std::copie` ou `std::vecteur::insert` – maintient l'utilisation de la mémoire linéaire et prévisible. *

---

Analyse de complexité

Métrique
- C'est quoi ?
**Heure**
* Espace * O(n)

*Parce que nous attribuons un nouveau tableau de la taille `2n`, l'espace aérien est inévitable. *

---

## 7-

Autres Essai prévu
C'est pas vrai.
[5] Autres
[1,2,3,4] Autres
"n = 1000" (constriction maximale)

*Vérifiez toujours que la longueur du tableau retourné est exactement "2 * len(nums)". *

---

- Oui. Réflexions finales

* **Keep it simple** – le problème est trivial; une boucle propre gagne l'entrevue.
* **Éviter les micro-optimisations** qui masquent l'intention.
* **Commentaire seulement lorsque nécessaire** – votre code devrait lire comme une histoire.

---

Résumé optimisé du SEO

> **LeetCode 1929 Concaténation des solutions Array – Java, Python, C++**
> Maîtrisez la question d'entrevue facile avec des implémentations propres, O(n). Apprenez les pièges, les pratiques exemplaires et la façon de codifier les entrevues. Boostez votre CV avec ce guide définitif.

---

Tu en veux plus ?
Consultez notre série sur **LeetCode Easy Problems** – des tours de tableau à la manipulation de chaînes – avec des explications étape par étape et des extraits de code en Java, Python et C++.

Bon codage et bonne chance pour votre prochaine interview!