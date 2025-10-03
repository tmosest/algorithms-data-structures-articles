---
titre: LeetCode 2680.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 2680 – Valeur maximale
**Langues**: Java-Python-C++
** Solution prête à l'interview** + un billet de blog *SEO-friendly* qui explique le bon, mauvais et laid du problème afin que vous puissiez parler avec confiance dans votre prochaine interview.

---

Code rapide

Code de la langue
C'est quoi, ça ?
**Java** Cliquez pour agrandir</sommary>``java
Importation de java.util.*;

solution de classe publique {
maximum public longOr(int[] nums, int k) {
int n = longueur nums;
// suffixe[i] = OU des nombres[i+1 ... n-1]
int[] suffixe = nouvelle int[n];
pour (int i = n - 2; i >= 0; --i) {
suffixe[i] = suffixe[i + 1]
}

longue meilleure = 0;
préfixe int Ou = 0; // OU des éléments avant l'indice courant
pour (int i = 0; i < n; i++) {
long candidat = préfixeOrigine ((long)nums[i] << k)
si (le candidat > le meilleur) meilleur = candidat;
préfixe Or. en
}
le meilleur retour;
}

public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.maximumOu(nouvelle int[]{12, 9}, 1)); // 30
Système.out.println(s.maximumOu(nouveau int[[]{8, 1, 2}, 2)); // 35
}
}
```</details> Autres
**Python**= <details><sommaire>Cliquez pour agrandir</sommaire>``python
de taper l'importation Liste

Solution de classe:
def maximum Ou(self, nombres: List[int], k: int) -> Int:
n = len(nums)
suffixe = [0] * n
pour i dans la plage (n - 2, -1, -1):
suffixe[i] = suffixe[i + 1]

meilleur = 0
préfixe = 0
pour i, val dans l'énumération(nombres):
candidat = préfixe(ou)
si le candidat > le mieux:
meilleur = candidat
préfixe_ou= valeur
le meilleur retour

# tests rapides
si __nom__ == "__main__" :
s = Solution()
print(s.maximumOu([12, 9], 1)) # 30
print(s.maximumOu([8, 1, 2], 2)) # 35
```</details> Autres
**C++** Cliquez pour agrandir</sommary>``cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long maximum Ou(vecteur <int>& nums, int k) {
int n = nombres.size();
vecteur<int> suffixe(n, 0);
pour (int i = n - 2; i >= 0; --i)
suffixe[i] = suffixe[i + 1]

longue longue meilleure = 0;
préfixe int Ou = 0;
pour (int i = 0; i < n; ++i) {
long candidat long = (long long)préfixeOr= ((long long)nums[i] << k)=Suffix[i];
best = max (meilleur candidat);
préfixe Or. en
}
le meilleur retour;
}
};

Int main() {
Solution s;
ou({12, 9}, 1) << endl; // 30
Cout << s.maximumOr({8, 1, 2}, 2) << endl; // 35
retour 0;
}
```</details> Autres

---

Article de blog – maximum OU (Code Leet 2680): Les bons, les mauvais et les méchants

- Oui. 1. Présentation

> **Titre du problème**: *maximum OU*
> **Numéro de code leet**: 2680
> **Difficulté**: Moyenne

Vous êtes donné un tableau `nums` et un entier `k`. Dans une opération, vous pouvez doubler (multiplier par 2) n'importe quel élément du tableau. Vous pouvez effectuer tout au plus des opérations `k`. Après toutes les opérations, vous devez retourner la valeur maximale possible de «nums[0]» nums[1].

> *Pourquoi cette entrevue est-elle conviviale? *
> Il teste la manipulation de bits, le raisonnement avide, et une compréhension de la façon de garder l'algorithme linéaire. Les contraintes (n ≤ 105, k ≤ 15) indiquent qu'une recherche exponentielle naïve échouera.

---

- Oui. 2. Répartition des problèmes

- **Bitwise OR** combine des bits: si un nombre a un 1 à une position, le résultat aura un 1 là.
- **Le doublement d'un élément** est le même que le déplacement de gauche par l'un : `x * 2 == x << 1`.
- Oui. Vous pouvez effectuer le décalage sur *any* element, peut-être le même élément plusieurs fois.
- `k` est petit (=15), mais `n` peut être grand (=105).

---

- Oui. 3. Approche fondée sur la force brute

Vous pouvez essayer toutes les séquences d'indices de longueur `k` (chaque élément `n` peut être choisi).
- Complexité : O(nk) → impossible pour n = 105.
- Même en énumérant tous les sous-ensembles d'indices est 2n.

**Bien**: Facile à comprendre.
**Bad**: Complètement impossible.

---

- Oui. 4. Insight – Pourquoi doubler un seul élément? (en milliers de dollars)

- Le doublement déplace une position.
- Oui. Le bit le plus significatif (MSB)** apporte la plus grande valeur au résultat OR.
- Oui. Si l'on divise les postes `k` entre plusieurs nombres, chaque nombre individuel de postes MSB ne peut déplacer que les postes `k1, k2, ...`, sans jamais dépasser les postes `k`.
- L'OR de tous les nombres ne peut jamais avoir un peu au-delà du déplacement le plus éloigné d'un seul nombre.
- Par conséquent, *mettre tous les décalages `k` sur l'élément avec le plus haut MSB* maximise la OU finale.

> ** Partie importante** : prouver officiellement le choix avide pourrait sembler non intuitif. Mais un contre-exemple rapide montre toute distribution qui n'est pas tout-à-un laisse un peu plus haut.

---

- Oui. 5. Solution unique optimale

Au lieu de choisir l'élément à déplacer, nous pouvons précalculer la OU de tous les éléments **avant** et **après** chaque position.

5.1 Préfixe et suffixe OU

- `préfixe[i]` = OU de `nums[0 ... i-1]`.
- `suffix[i]` = OU de `nums[i+1 ... n-1]`.

Ils peuvent être construits en un seul passage chacun.

5.2 Candidat pour chaque index

Pour l'index `i`, si nous appliquons tous les postes `k` à `nums[i]`:

«» "
candidat = préfixe[i]
«» "

Prenez le maximum "candidat" sur tous les "i".

Pourquoi ça marche ?

- `préfixe[i]` et `suffix[i]` contient déjà tous les bits des numéros *hors* `i`.
- Déplacement de "nums[i]` par des positions `k` seulement potentiellement définit de nouveaux bits élevés qui n'ont pas été réglés ailleurs.
- La OU de ces trois parties est le meilleur que nous puissions obtenir si nous double «nums[i]» "k" fois.
- La vérification de tous les indices assure que nous considérons le meilleur élément à doubler.

5.4 Complexité

- **Heure**: O(n) – un laissez-passer pour construire le suffixe, un laissez-passer pour évaluer les candidats.
- **Espace**: O(n) – tableaux `préfix` & `suffix` (peut être compressé à O(1) en construisant `suffix` sur-le-vol si vous êtes étanche à la mémoire).
- La valeur "k" n ' influence qu ' une opération de changement constant.

---

- Oui. 6. Liste de contrôle des cas de bord

Qu'est-ce qu'il faut regarder
-- -- -- -- -- -- -- -- --
- Oui. 0 ''' Pas de changement → la réponse est la simple OU du tableau. Autres
- Oui. 1 ́ ́ ́ ́ Le déplacement de l'élément unique donne ``nums[0] << k`.
Les nombres peuvent déjà avoir des bits élevés réglés à des positions ≥ k. Le déplacement peut encore définir des bits plus élevés. Autres
Nombres négatifs? Le problème garantit des ints non négatifs (0 ≤ nums[i] < 231). Autres

---

- Oui. 7. Avantages et inconvénients (Bonne et mauvaise)

Aspect du bien
- C'est quoi ?
**Clarté conceptuelle**=L'intuition de l'avidité + OU la pré-computation est soignée. Il faut comprendre que l'ESM domine. La preuve cupide peut se sentir comme une étape de l'horreur, sinon expliquée. Autres
**Scalabilité**
**Mémoire **= O(n) tableaux supplémentaires.= Peut-être une préoccupation pour des limites de mémoire strictes. Pourrait être paré à O(1) en conservant le suffixe de course OU tout en itérant de gauche à droite. Autres
**Mise en œuvre**= Boucles droites.= Aucune.= Le moulage de gauche à 64 bits (`long` en Java / `long` en C++) est un petit détail qui peut faire voyager les débutants. Autres
**Interview-parler**= Vous pouvez parler de Bitwise OR, gourmand, préfixe/suffixe. La preuve de l'optimalité peut être une source de conversation; soyez prêt à l'expliquer clairement. Autres

---

- Oui. 8. Variante O(1) de l ' espace

Vous pouvez éviter de stocker l'ensemble du tableau suffixe en construisant le suffixe OR en marche arrière et en évaluant immédiatement:

"Java
insuffixOr = 0; // OR des éléments après le courant
pour (int i = n - 1; i >= 0; --i) {
le candidat long = ((long)nums[i] << k)=" suffixeOr="préfixeOr;
meilleur = Math.max (meilleur candidat);
suffixeOr= nombres[i];
préfixe Or. en
}
«» "

Cela n'utilise que quelques variables entières.

---

- Oui. 9. Entretiens dans le monde réel

- **Précipitation** l'équivalence de transfert de bits au transfert de gauche.
- **Expliquer** l'intuition gourmande «tous les postes à un».
- **Afficher** le préfixe/suffixe comme motif O(n) classique.
- **Mention** le petit `k` → nous pourrions faire un O(k · n) DP si nous voulions un espace constant, mais la solution actuelle est propre.
- **Préparer** un contre-exemple rapide si l'intervieweur demande pourquoi ne pas diviser les quarts? (en milliers de dollars)

---

10 ans. Prise- Liste de contrôle pour votre prochaine entrevue

Pourquoi ça compte ?
C'est-à-dire
**Fonctionnements par le biais d'opérations par le biais d'un système** Autres
**Propreté du mariage** Autres
**Solution linéaire** Autres
**Multiple-language implementation**=Les intervieweurs adorent vous voir s'adapter aux contraintes linguistiques. Autres
**Analyse de la complexité** Autres

---

11 ans. Mots-clés du référencement

- LeetCode 2680
- OU maximum
- Question Bitwise OU interview
- Solution Java Python C++
- Entretien avec un algorithme
- Préparation d'un entretien d'embauche
- raisonnement algorithmique
- Manipulation linéaire du temps

> *Ces mots-clés aideront les recruteurs à trouver votre message lorsqu'ils cherchent des solutions d'entretien -LeetCode 2680 ou des problèmes d'algorithme d'entretien d'emploi.

---

12. Conclusion

Le problème d'Origine maximale est faussement simple mais cache un puissant principe d'avidité. En réalisant que *tous les déplacements doivent aller à un élément* et en utilisant le préfixe/suffixe OU précomputation, nous arrivons à une solution O(n) propre qui fonctionne confortablement dans les limites données.

Que vous soyez un ingénieur chevronné ou un développeur junior qui se prépare à votre prochaine entrevue, ce problème est une grande vitrine de:

- **Aperçu au niveau du bit**
- **Le raisonnement du mariage**
- **Algorithme linéaire efficace**

Bonne chance – et que vos intervieweurs soient impressionnés par votre maîtrise du code et de la théorie sous-jacente! C'est ce qu'il a dit