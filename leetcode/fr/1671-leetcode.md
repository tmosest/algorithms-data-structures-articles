---
titre: LeetCode 1671. Nombre minimum d'enlèvements pour effectuer une représentation en montagne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1671 – Nombre minimum d'enlèvements pour faire une représentation des montagnes
- Oui. La solution complète, bonne, mauvaise et mauvaise
C++*

> **TL;DR** –
> 1. Trouver la séquence la plus longue en augmentation (LIS) se terminant à chaque indice.
> 2. Trouvez la séquence de diminution la plus longue (LDS) à partir de chaque indice.
> 3. Pour chaque indice pouvant être un pic ('LIS[i] > 1 && LDS[i] > 1') calculer
> `montagneLen = LIS[i] + LDS[i] - 1`.
> 4. `réponse = n - max(mountainLen)` – les suppressions minimales.
>
> Complexité: **O(n2)** temps, **O(n)** espace (n ≤ 1000).

---

- Oui. Pourquoi ce problème compte pour les entrevues

- **Mountain Array** – un modèle d'entrevue classique: -en augmentant strictement puis en diminuant strictement.
- Nécessite une programmation dynamique* (LIS/LDS) et une compréhension claire des problèmes de subséquence.
- Teste votre capacité à gérer les cas de bord (`n = 3`, tous nombres égaux, etc.).
- Parfait pour montrer votre style de codage et votre approche de résolution de problèmes lors d'une entrevue d'embauche.

---

## -Détails

Définition d'un tableau de montagne

Une chaîne de montagnes "arr" satisfait:

1. `longueur normale >= 3'
2. Indice `i` (`0 < i < n-1`) tel que
«arr[0] < ... < arr[i]» **et** "arr[i] > ... > arr[n-1] "

Le pic est unique car les deux côtés sont strictement monotoniques.

- Oui. Observation

Si nous savons pour chaque indice:
- Combien de temps une subséquence en pleine augmentation se termine à cet indice (`LIS[i]`).
- Combien de temps commence une subséquence strictement décroissante à cet indice ('LDS[i]').

Un indice peut alors être un pic **iff** `LIS[i] > 1 && LDS[i] > 1`.
La longueur totale de la montagne qui utilise `i` comme le pic est `LIS[i] + LDS[i] - 1` (le pic est compté deux fois).

#### #############

Parce que `n <= 1000`, un `O(n2)` DP est parfait.

- **LIS**
«» "
LIS[i] = 1
pour j < i:
si nombres[i] > nombres[j]: LIS[i] = max(LIS[i], LIS[j] + 1)
«» "

- **LDS** – itérer à l'envers
«» "
LDS[i] = 1
pour j > i:
si nombres[i] > nombres[j]: LDS[i] = max(LDS[i], LDS[j] + 1)
«» "

C'est pas vrai. Trouvez la montagne la plus longue

«» "
maxLen = 0
pour i en 1 ... n-2:
si LIS[i] > 1 et LDS[i] > 1:
maxLen = maxLen, LIS[i] + LDS[i] - 1)
«» "

C'est vrai. Réponse finale

«» "
retour n - maxLen
«» "

---

Numéro de code

### Java (friendly Code Leet)

"Java
solution de classe {
Int minimumMountainRemoveals(int[] nums) {
int n = longueur nums;
int[] lis = nouvelle int[n];
int[] lds = nouvelle int[n];

// LIS (avant)
pour (int i = 0; i < n; i++) {
lis[i] = 1;
pour (int j = 0; j < i; j++) {
si (nombres[i] > nombres[j]) {
lis[i] = Math.max(lis[i], lis[j] + 1);
}
}
}

// SLD (en arrière)
pour (int i = n - 1; i >= 0; i--) {
lds[i] = 1;
pour (int j = n - 1; j > i; j--) {
si (nombres[i] > nombres[j]) {
lds[i] = Math.max(lds[i], lds[j] + 1);
}
}
}

int best = 0;
pour (int i = 1; i < n - 1; i++) {
si (lis[i] > 1 && lds[i] > 1) {
best = Math.max(best, lis[i] + lds[i] - 1);
}
}
retour n - meilleur;
}
}
«» "

Python 3

'`python
Solution de classe:
def minimumMountainRemoveals(self, nombres: List[int]) -> Int:
n = len(nums)
lis = [1] * n
lds = [1] * n

LIS
pour i dans la plage(n):
pour j dans la plage i:
si nombres[i] > nombres[j]:
lis[i] = max(lis[i], lis[j] + 1)

# LDS
pour i dans la fourchette(n - 1, -1, -1):
pour j dans la plage(n - 1, i, -1):
si nombres[i] > nombres[j]:
lds[i] = max(lds[i], lds[j] + 1)

meilleur = 0
pour i dans la fourchette(1, n - 1):
si lis[i] > 1 et lds[i] > 1 :
best = max(best, lis[i] + lds[i] - 1)

retour n - meilleur
«» "

### C++ (GNU‐C++17)

'`cpp
solution de classe {
public:
Int minimumMountainRemoveals(vecteur<int>& nums) {
int n = nombres.size();
vecteur<int> lis(n, 1), lds(n, 1);

// LIS
pour (int i = 0; i < n; ++i) {
pour (int j = 0; j < i; ++j)
si (nombres[i] > nombres[j])
lis[i] = max(lis[i], lis[j] + 1);
}

// LDS
pour (int i = n - 1; i >= 0; --i) {
pour (int j = n - 1; j > i; --j)
si (nombres[i] > nombres[j])
lds[i] = max(lds[i], lds[j] + 1);
}

int best = 0;
pour (int i = 1; i < n - 1; ++i) {
si (lis[i] > 1 && lds[i] > 1 )
best = max(best, lis[i] + lds[i] - 1);
}

retour n - meilleur;
}
};
«» "

---

Ce qui fonctionne bien

Pourquoi c'est bien
C'est quoi ?
**Simple O(n2) DP**. Facile à comprendre, aucune structure de données avancée n'est nécessaire. Autres
**Séparation claire**LIS et LDS calculés indépendamment, rendant le débogage trivial. Autres
**Contrôle déterministe du pic** 1' garantit une montagne valide. Autres
**Évoluable**="n = 1000` → au plus 1 000 000 d'opérations → bien moins de 1 ms. Autres
**Portable** uvre en Java, Python et C++ avec des changements minimes. Autres

---

## -

Sujet Atténuation
C'est pas vrai.
**O(n2) peut se sentir lourd**= Pour `n = 105` il échouerait, mais les contraintes sont `= 1000`. Autres
**Les cas d'Edge** `LIS` et `LDS` resteront 1 → pas de pic; problème garantit solvable, mais toujours bon à gérer explicitement. Autres
**Mémorie**= Les tableaux `O(n)` sont minuscules, mais si vous avez besoin de `O(n log n)` pour des contraintes plus grandes, utilisez la recherche binaire LIS. Autres

---

## Ugly - Gotchas & Advanced Échelles

1. ** Augmenter ou diminuer de façon stricte** – Assurez-vous d'utiliser la comparaison *strict* (`>`).
2. **Peak doit avoir les deux côtés** – Ne jamais considérer `i = 0` ou `i = n-1` comme un pic.
3. **Off‐by‐One in Length Calculation** – N'oubliez pas de soustraire 1 lorsqu'on additionne LIS + LDS parce que le pic est compté deux fois.
4. **Approche alternative** – Une solution plus rapide `O(n log n)` peut être construite avec LIS+reverse‐LIS + recherche binaire, mais pour la clarté de l'entrevue le DP quadratique est préféré.
5. **Test** – Inclure des cas comme `[1, 2, 3]` (pas de côté décroissant) et `[3, 2, 1]` (pas de côté croissant) pour confirmer que l'algorithme ne choisit que des pics valides.

---

Ébauche de blog optimisée du SEO

> **Titre:**
> Code de Leet 1671 – Nombre minimum d'enlèvements pour effectuer la répartition des montagnes (Java/Python/C++)
>
> **Meta Description:**
> Découvrez comment résoudre LeetCode 1671 en Java, Python et C++ en utilisant une programmation dynamique. Comprendre LIS & LDS, la sélection des pics et l'analyse de la complexité afin d'obtenir votre prochaine entrevue de codage.

Paragraphe intro
> Si vous préparez un entretien technique, vous aurez souvent des problèmes de subséquence. L'un des plus délicats mais les plus éclairants est LeetCode 1671: *Nombre minimal d'enlèvements pour faire une représentation des montagnes*. Ce post vous guide à travers la solution complète, le cassant dans les parties de bon, mauvais et laid. Saisissez les extraits de code pour Java, Python et C++, afin que vous puissiez vous entraîner sur LeetCode ou vous préparer à votre prochaine entrevue.

Sections du corps
1. **Pourquoi les tableaux de montagne sont-ils de l'or?**
2. **Définition du problème et contraintes* *
3. **Perspective de programmation dynamique – LIS & LDS**
4. ** Mise en oeuvre étape par étape** (Java, Python, C++)
5. **Analyse de complexité et cas de bord**
6. Résumé**
7. ** Variantes avancées et lecture supplémentaire**
8. **Conseils pratiques et exemples de cas d'essai**

> **Mots clés:**
> LeetCode 1671, Enlèvement minimum de montagne, LIS, LDS, Programmation dynamique, Solution Java, solution Python, solution C++, modèles de codage d'entretien, conseils d'entretien de codage, défi de codage.

### Appel à l'action

> Vous voulez plus de solutions LeetCode ? Abonnez-vous à notre newsletter et obtenez des défis de codage hebdomadaires livrés directement à votre boîte de réception!

---

Comment utiliser cet article dans votre recherche d'emploi

1. **Afficher le code** – Coller l'extrait de langue spécifique sur votre profil GitHub ou un blog personnel.
2. **Expliquer l'approche** – Dans une interview, commencer par la définition de montagne → LIS/LDS → pic check.
3. **Discuse les parties de "Bad" & "Ugly"** – Limites de citation, pourquoi des comparaisons strictes comptent, et comment gérer les cas de bord.
4. **Mention l'alternative** – Notez brièvement l'option `O(n log n)`; vous pouvez dire que vous avez choisi le DP quadratique pour plus de clarté.
5. **Enveloppez** – Résumez la réponse et la complexité pour renforcer votre compréhension.

---

À emporter

LeetCode 1671 est une vitrine de programmation dynamique* déguisée en puzzle subséquemment. En calculant LIS et LDS et en validant les pics, vous pouvez terminer avec le nombre minimal de suppressions d'une manière propre et prête à l'entrevue. Utilisez le code ci-dessus, testez-le soigneusement, et vous impressionnerez les recruteurs avec votre profondeur technique et la clarté de la pensée.

Bon codage ! C'est ce qu'il a dit.

---

**Note:** Tous les extraits de code sont compilés sur l'environnement standard de LeetCode. N'hésitez pas à copier-coller et à tester. Joyeux entretien !