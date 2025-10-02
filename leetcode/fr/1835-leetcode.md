---
titre: LeetCode 1835. Trouver la somme XOR de toutes les paires Bitwise ET -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 1835 – Trouvez la somme XOR de toutes les paires
* Python : solutions C++ + billet de blog In-Depth**

> *Un guide complet qui montre la solution mathématique la plus propre, prouve pourquoi elle fonctionne et transforme le problème en une histoire d'entrevue gagnante. *

---

Table des matières
1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Approche Naïve Brute-Force] (#approche naïve)
3. [La solution O(n+m) élégante] (#solution efficace)
4. [Proof mathématique] (#proof)
5. [Complexité temporelle et spatiale](#complexité)
6. [Justices et pièges] (#cas de référence)
7. (#code)
- Java
- Python
- C++
8. [Conseils d'entrevue et astuces](#tips)
9. [SEO-Optimized Closing & CTA](#seo)

---

## <a id="problème-recap"></a>1.

> **LeetCode 1835 – Trouvez la somme XOR de toutes les paires Bitwise ET**
> *Tarde*

On vous donne deux tableaux entiers `arr1` et `arr2`.
Pour chaque paire `(i, j)` vous calculez `arr1[i] & arr2[j]`.
Tous ces résultats forment une liste; vous devez retourner la somme XOR de cette liste.

Contraintes
- `1 ≤ arr1.longueur, arr2.longueur ≤ 105 "
- `0 ≤ arr1[i], arr2[j] ≤ 109`

---

## <une approche naïve></a>2. Approche de la force

Texte
pour chaque a en arr1:
pour chaque b en arr2:
(a et b)
«» "

* **Heure**: `O(n*m)` – 105 * 105 = 1010 ops → impossible.
* **Espace**: `O(1)` en dehors de l'entrée.

Bien que facile à coder, cette approche *time-out* sur les grandes entrées.
C'est un écueil classique de la paire – n'oubliez pas de chercher des simplifications algébriques.

---

L'élégant O(n+m) Solution

La principale observation est la loi distributive de XOR sur ET:

> **(a & b) (a & c) = a & (b / c)**

Appliquer cette propriété à plusieurs reprises nous obtenons:

«» "
XOR sur toutes les paires = (XOR d'arr1) et (XOR d'arr2)
«» "

Il nous faut donc deux scans :

1. `xor1 = a0 , , , ... , a_{m-1} "
2. `xor2 = b0 . "
3. Retour `xor1 & xor2 "

C'est ça – **O(n+m) temps, O(1) espace**.

---

La preuve mathématique

Laissez

«» "
S = {arr1[i] et arr2[j]=0 ≤ i < m, 0 ≤ j < n}
X = * * * * * (la somme XOR de toutes les paires)
«» "

Fixer un élément `arr1[i] = a`.
Tous les termes contenant "a" sont:

«» "
a & arr2[0], a & arr2[1], ..., a & arr2[n-1]
«» "

XOR de ces termes:

«» "
A & arr2[0]
= a & (arr2[0] -irr2[1] -irr2[n-1]) (par distribution)
= a & xor2
«» "

Maintenant XOR sur tous les `i`:

«» "
X = (arr1[0] & xor2)
= (arr1[0] -) arr1[1] -) et xor2
= xor1 & xor2
«» "

Ainsi toute la somme XOR s'effondre à un seul ET de deux XOR.

---

## <a id="complexité"></a>5.

L'approche La complexité temporelle La complexité spatiale Autres
Il s'agit d'un projet pilote.
*(n · m)
Optimisé (XOR + ET)

Avec `n, m ≤ 105`, la méthode optimisée fonctionne en < 0,01 s dans la plupart des langues.

---

## <a id="edge-cases"></a>6.

Scénario Que regarder
C'est pas vrai.
Le problème garantit la longueur ≥ 1, donc pas besoin de traiter vide. Autres
Des nombres allant jusqu'à 109 (32 bits) sont en sécurité; XOR/AND vous maintiennent dans une plage de 32 bits. Autres
Conservez les boucles serrées ; évitez de créer des tableaux intermédiaires. Autres
Autres Pour les concours, lisez avec des E/S rapides. Autres
Les nombres négatifs sont absents par contrainte; s'ils étaient, XOR fonctionne mais ET peut avoir besoin de manipulation non signée. Autres

---

## <un code id="></a>7.

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.

> **Astuce:** La même logique fonctionne pour n'importe quelle langue avec arithmétique entière 32 bits.

#### 7.1 Java

"Java
// LeetCode 1835 – Trouvez la somme XOR de toutes les paires Bitwise ET
solution de classe {
Int public getXORSum(int[] arr1, int[] arr2) {
xor1 = 0;
xor2 = 0;

pour (int a : arr1) xor1 ^= a;
pour (int b : arr2) xor2 ^= b;

retourner xor1 & xor2;
}
}
«» "

7.2 Python

'`python
# LeetCode 1835 – Trouvez la somme XOR de toutes les paires
Solution de classe:
def getXORSum(self, arr1: List[int], arr2: List[int]) -> Int:
xor1 = 0
xor2 = 0

pour a en arr1:
xor1 ^= a
pour b en arr2:
xor2 ^= b

retour xor1 & xor2
«» "

> *Les entiers de Python sont débordés, mais le résultat s'adapte en 32 bits selon les contraintes. *

### 7.3 C++

'`cpp
// LeetCode 1835 – Trouvez la somme XOR de toutes les paires Bitwise ET
solution de classe {
public:
int getXORSum(vector<int>& arr1, vector<int>& arr2) {
xor1 = 0, xor2 = 0;
pour (int a : arr1) xor1 ^= a;
pour (int b : arr2) xor2 ^= b;
retourner xor1 & xor2;
}
};
«» "

Les trois snippets fonctionnent dans **O(n+m)** temps et **O(1)** espace supplémentaire.

---

## <a id="tips"></a>8. Conseils et astuces d'entrevue

Pourquoi ça aide ?
C'est pas vrai.
**Afficher les maths d'abord** – demander si le candidat peut repérer une propriété avant de coder. Démontre une compréhension profonde des opérateurs bitwise. Autres
**Demander pour les cas de bord** – tester les nombres négatifs, les zéros, les grandes valeurs. Révèle la robustesse. Autres
**Débat sur la complexité du temps** – confirmer O(n+m) contre O(n*m). Montre la conscience algorithmique. Autres
**Le droit distributif explicite** – «(a&b) ─ (a&c) = a & (b ─ c)». C'est pourquoi la solution est correcte. Autres
**Demander des solutions alternatives** – par exemple, en utilisant le comptage des bits. Teste la créativité. Autres

> **Interview Highlight**: Mentionnez que ce problème est un exemple de manuel de *= chercher pour la simplification algébrique. Les intervieweurs aiment les candidats qui transforment une tâche O(n2) apparemment difficile en un tour O(n) propre.

---

## <a id="seo"></a>9. SEO-Optimized Closing & Call‐to‐Action

Si vous êtes à la recherche de *boost your coded interview game*, mastering LeetCode 1835 met en évidence votre capacité à:

- Réfléchissez.
- Appliquer *les identités mathématiques*
- Ecrire le code *O(n+m)* en **Java, Python et C++**

Ajoutez ce problème à votre portfolio, partagez l'élégante preuve et marquez vos messages avec `#LeetCode1835`, `#BitwiseOperations`, `#CodingInterview` et `#AlgorithmDesign`. Les recruteurs aiment voir des solutions concises et mathématiques.

> ** Prêt à faire l'interview suivante ? * *
Voir [LeetCode](https://leetcode.com) → Recherche -1835 → Résolvez → Soumettre → Partagez votre solution sur LinkedIn avec une brève écriture.
> Cliquez sur LinkedIn pour obtenir plus de guides et d'aide à la recherche d'emploi.

Bon codage ! C'est ce qu'il a dit.

---