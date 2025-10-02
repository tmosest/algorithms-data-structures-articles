---
Titre: LeetCode 1228. Numéro manquant en progression arithmétique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Numéro manquant dans la progression arithmétique – LeetCode 1228
** Solutions Java, Python & C++ + guide prêt à l'interview**

---

- Oui. 1. Présentation

> **LeetCode 1228 – Numéro manquant dans la progression arithmétique**
> *Un seul nombre a été retiré d'une progression arithmétique (AP) qui a strictement augmenté ou diminué. Trouvez l'élément manquant. *

Le problème est une question d'entrevue classique qui teste votre compréhension des séquences arithmétiques, de la manipulation des cas de bord et de la logique à temps constant. La maîtrise vous donne une solution propre à montrer sur votre CV, une réponse solide pour les entretiens techniques, et la confiance dans la résolution de problèmes plus difficiles.

---

- Oui. 2. Exposé des problèmes

Texte
Avec un tableau entier arr qui contient tous les éléments d'une progression arithmétique strictement monotone de longueur n+1
sauf un élément qui a été enlevé (pas le premier ou le dernier élément), trouver le nombre manquant.

Rends le numéro manquant.
«» "

Description du champ
C'est pas vrai.
Tableau de la taille `n` (n ≥ 3)
Longueur du tableau d`entrée
Taille originale de la PA avant le retrait

> **Exemples**
> • «arr = [5, 7, 11, 13]» → sortie `9`
> • `arr = [15, 13, 12]` → sortie `14`

---

- Oui. 3. Contraintes

Paramètre minimum Remarques maximum
- C'est quoi ?
La taille d'entrée peut être grande; O(n) est nécessaire. Autres
`arr[i]`= -109=109=199 nombre entiers signés 32 bits. Autres
Autres La progression est ** strictement monotonique** (augmentation ou diminution). Autres
Autres L'élément manquant est **jamais le premier ou le dernier** de la séquence originale. Autres

---

- Oui. 4. Comprendre le problème

Une progression arithmétique (AP) présente une différence constante «d».
Si nous supprimons un élément d'une progression de la longueur `k+1`, le tableau résultant a `k` éléments, et **exactement une paire adjacente aura un espace de `2·d`** – l'endroit où la suppression s'est produite.

Pourquoi une seule de ces paires ? *
Parce que toutes les autres paires adjacentes dans le reste du tableau sont toujours consécutives dans l'AP originale et diffèrent donc exactement par `d`.

La tâche se réduit à :
1. **Déterminer la vraie différence "d".**
Dans un tableau de ≥ 4 éléments, nous pouvons regarder les trois premières différences et choisir celle qui apparaît au moins deux fois.
2. **Localiser la paire anormale** où la différence est `2·d` et calculer le nombre manquant comme `précédent + d`.

Cas de bord:
- **`n = 3`** – la règle "majorité" ne peut pas être appliquée parce que nous n'avons que deux différences. La plus petite différence de magnitude est la "d" réelle.
- **Négatif `d`** – l'AP peut diminuer; l'algorithme gère les signes naturellement.

---

- Oui. 5. Approche (temps O(n), espace O(1))

1. ** Calculer les trois premières différences** (`diff1`, `diff2`, `diff3`).
2. **Identifiez la bonne différence «d»** :
*Si `diff1 == diff2` ou `diff1 == diff3` → `d = diff1`; sinon `d = diff2`.*
3. **Scan une fois** du deuxième élément au deuxième au dernier:
*Quand `arr[i] - arr[i-1] != d`, le nombre manquant est `arr[i-1] + d`.
La boucle se termine immédiatement – pas besoin de vérifier le dernier élément parce que l'élément manquant ne peut pas être à la fin du tableau. *
4. ** Cas spécial «n = 3»**:
*Les deux différences disponibles donnent `d` comme celle avec une valeur absolue plus petite.
Si la première différence est égale à "2·d", le nombre manquant se situe après le premier élément; sinon, il se situe après le second. *

L'algorithme ne modifie jamais le tableau d'entrée et fonctionne en une seule passe linéaire.

---

- Oui. 6. Mise en œuvre

Ci-dessous sont propres, des implémentations prêtes à l'interview dans **Java, Python et C++**.

---

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe {
public int manquantNumber(int[] arr) {
int n = longueur de l'arrond;
si (n) 3) {
int diff1 = arr[1] - arr[0];
int diff2 = arr[2] - arr[1];
int d = Math.abs(diff1) < Math.abs(diff2) ? diff1 : diff2;
si (diff1 == 2 * d) {
retour arr[0] + d; // manquant après arr[0]
} autre {
retour arr[1] + d; // manquant après arr[1]
}
}

int diff1 = arr[1] - arr[0];
int diff2 = arr[2] - arr[1];
int diff3 = arr[3] - arr[2];

int d = (diff1 == diff2="diff1 == diff3) ? diff1 : diff2;

pour (int i = 1; i < n - 1; i++) {
Si (arr[i] - arr[i - 1] != d) {
retour arr[i - 1] + d;
}
}
retour -1; // ne devrait jamais atteindre ici
}
}
«» "

---

6.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def manquantNumber(self, arr: List[int]) -> Int:
n = len(arr)
Si n == 3:
diff1 = arr[1] - arr[0]
diff2 = arr[2] - arr[1]
d = diff1 si abs(diff1) < abs(diff2) sinon diff2
retourner arr[0] + d si diff1 == 2 * d autre arr[1] + d

diff1 = arr[1] - arr[0]
diff2 = arr[2] - arr[1]
diff3 = arr[3] - arr[2]
d = diff1 si diff1 == Diff2 ou Diff1 == diff3 autres diff2

pour i dans la fourchette(1, n - 1):
si arr[i] - arr[i - 1] != d:
retour arr[i - 1] + d
retour -1 # jamais atteint
«» "

---

*### 6.3 C++

'`cpp
#incluez <vecteur>
#incluez <cmath>

solution de classe {
public:
nombre(std::vector<int>& arr) {
int n = arr.size();
si (n) 3) {
int diff1 = arr[1] - arr[0];
int diff2 = arr[2] - arr[1];
int d = std::abs(diff1) < std::abs(diff2) ? diff1 : diff2;
si (diff1 == 2 * d) retour arr[0] + d;
sinon retourner arr[1] + d;
}

int diff1 = arr[1] - arr[0];
int diff2 = arr[2] - arr[1];
int diff3 = arr[3] - arr[2];
int d = (diff1 == diff2="diff1 == diff3) ? diff1 : diff2;

pour (int i = 1; i < n - 1; ++i) {
Si (arr[i] - arr[i - 1] != d) retour arr[i - 1] + d;
}
retour -1; // inaccessible
}
};
«» "

---

- Oui. 7. Alternative (Brute-Force) – pourquoi pas?

Une solution naïve tente tous les nombres possibles entre `arr[0]` et `arr[n-1]` et vérifie si elle correspond à une AP.
Il est **O(n2)** et sera TLE sur les grandes entrées. Il est utile pour la pratique, mais ** jamais** pour la production ou une entrevue.

---

- Oui. 8. Cas de bord d'essai

Pourquoi ça marche ?
C'est pas vrai.
"[1, 4, 7, 10]""" "13"" d = 3; écart après le dernier élément, mais la règle garantit que nous l'attraperons avant la fin. Autres
"[10, 8, 6, 4]"" "2"" Diminution de la PA; d = ‐2, la paire anormale est `10-4 = 6" (2·d). Autres
Augmenter la PA avec d = 10; la paire moyenne est 10. Autres
"[2, 1, 0]"" "-1"" Diminution de la PA avec d = ‐1; manquant après le premier élément. Autres
La longueur du tableau doit être ≥ 3 (le problème le garantit). Autres

---

- Oui. 9. Pourquoi cette solution est-elle utile pour les entrevues

1. **Zéro-mémoire** – Espace supplémentaire constant.
2. **Scan unique** – Temps linéaire, qui correspond à la complexité requise.
3. **Poignées augmentant et diminuant les AP** – Le signe `d` est conservé.
4. ** Logique claire** – Vous pouvez expliquer la différence de majorité et l'écart anomalous en quelques phrases.
5. **Extensible** – Le même motif résout ..... ..... .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. .. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .

---

- Oui. 10. Variations et extensions

Comment s'adapter
C'est quoi ?
**Trouver deux nombres manquants** Détectez les deux et calculez les deux éléments manquants. Autres
**Progression non-monotonique**= Calculer la différence moyenne `d = (arr[-1] - arr[0]) / n` (division entière). Puis procéder au scan. Autres
**Grands entiers (64 bits)**= Utiliser `long` en Java/C++ ou `int` en Python (Python='s int n'est pas lié). Autres

---

11. Réflexions finales

*Missing Number in Arithmetic Progression* est un problème trompeur simple qui cache un motif subtil.
Maîtriser ce modèle :
- Construit une base **solide** pour résoudre les problèmes de gap (p. ex. subséquence manquante, élément manquant dans un tableau trié).
- Démontre la clarté algorithmique** aux gestionnaires d'embauche.
- Vous donne un extrait réutilisable pour toute entrevue impliquant des séquences arithmétiques ou des scans linéaires.

Bon codage et bonne chance pour votre prochaine interview! C'est ce qu'il a dit