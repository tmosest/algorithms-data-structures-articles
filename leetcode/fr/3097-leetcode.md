---
titre: LeetCode 3097. Subarray le plus court avec OU au moins K II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La plus courte des sous-tables avec OU au moins K (Code de débit 3097)

**Mots-clés** – LeetCode 3097, le plus court subarray OR, bitwise OR, fenêtre coulissante, solution Java, solution Python, solution C++, algorithme d'entretien, interview de codage

---

Récapitulation des problèmes

Compte tenu d'un tableau « nombres » d'entiers non négatifs et d'un entier « k », trouvez la longueur du sous-array non vide le plus court* dont **OR** est **≥ k**.
Retour `-1` s'il n'existe pas de subarray.

*Contrôles*

- Oui.
-- -- -- -- -- --
1 ≤ longueur nums ≤ 2 × 105 '
0 ≤ k ≤ 109

Le problème apparaît à première vue, mais les contraintes rendent impossible une solution naïve O(n2).

---

C'est vrai. Pourquoi l'approche naïve fait défaut

L'idée simple est :

«» "
pour chaque indice de départ i
ou = 0
pour chaque indice de fin j ≥ i
(j)
si ou >= k: enregistrer j-i+1 et casser
«» "

complexité temporelle : **O(n2)** → 4 × 1010 opérations pour le pire cas.
L'utilisation de la mémoire est bonne, mais l'exécution est beaucoup trop élevée pour 2 × 105 éléments.

---

C'est vrai. La stratégie gagnante – Fenêtre coulissante + Compte bit

Intuition

Lorsque nous étendons la fenêtre à droite, la OU de la fenêtre ne peut que **augmenter** (les bits ne peuvent tourner que de 0 → 1).
Lorsque nous rétrécissons de la gauche, les bits ne peuvent disparaître que si le bits était unique à l'élément que nous supprimons.

Parce que les nombres s'inscrivent en 32 bits (`= 109 < 231`), nous pouvons maintenir un tableau `cnt[32]` où
`cnt[i]` = combien de nombres dans la fenêtre courante ont le paramètre `i`-th bit.

De `cnt` nous pouvons reconstruire le courant OR en O(32) en réglant un peu si `cnt[i] > 0`.

Algorithme

«» "
gauche = 0
ans = INF
cnt[32] = {0}

pour droite dans 0 .. n-1
ajouter des morceaux de nums[right] à cnt

alors que gauche <= droite et courant_OR(cnt) >= k
ans = min(ans, droite-gauche+1)
enlever les bits de nums[left] de cnt
gauche++

Retour et retour == INF ? -1 : ans
«» "

*Ajouter / supprimer des bits* est simplement augmenter / décrémenter les nombres pour chaque bits qui est défini dans le nombre.

Complexité

- Chaque élément est ajouté une fois et supprimé une fois → **O(n)** mises à jour.
- Chaque mise à jour touche au plus 32 bits → **O(32 · n) ↓ O(n)**.
- Reconstruction de la RUP dans la boucle « while » est O(32), temps constant.

Utilisation de la mémoire: **O(32)** → trivial.

---

C'est pas vrai. Tranche Liste de contrôle des cas

Autres Décision Pourquoi ça marche Remarques
- C'est quoi ?
- Oui. 0''' OU de tout élément unique est ≥ 0'' Le plus court est toujours longueur 1'''
Autres Aucun subarray n`atteint les séjours `k`- Ans` `INF`- Retour `-1`-
"nums" tous les zéros
Longueur Un seul élément vérifié une fois Fonctionne naturellement

---

C'est vrai. Mise en œuvre du code

> **Conseil:** Les extraits de code ci-dessous sont prêts à la production. Ils utilisent les mêmes fonctions d'aide claires pour ajouter/enlever des bits et reconstruire le bloc.

##### 5.1 Java

"Java
Importation de java.util.*;

solution de classe {
Int minimumSubarrayLength(int[] nums, int k) {
int[] cnt = nouveau int[32];
int gauche = 0, ans = entier. MAX_VALEUR;

pour (int droite = 0; droite < nums.longueur; droite++) {
AddBits(cnt, nums[right], 1);

pendant que (gauche <= droite && courantOr(cnt) >= k) {
ans = Math.min(ans, droite - gauche + 1);
AddBits(cnt, nums[left], -1);
gauche++;
}
}
Integer. MAX_VALUE ? -1 : ans;
}

vide privé addBits(int[] cnt, int num, int delta) {
pour (int i = 0; i < 32; i++) {
si (((num >> i) et 1) == 1) cnt[i] += delta;
}
}

courant int privéOr(int[] cnt) {
Int val = 0;
pour (int i = 0; i < 32; i++) {
si (cnt[i] > 0) valeur= (1 << i);
}
valeur de retour;
}
}
«» "

5.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def minimumSubarrayLength(self, nombres: Liste[int], k: int) -> Int:
cnt = [0] * 32
gauche, ans = 0, flotteur('inf')

pour droite, num in énumérate(nums):
Auto._add_bits(cnt, num, 1)

alors que gauche <= droite et soi-même._current_or(cnt) >= k:
ans = min(ans, droite - gauche + 1)
self._add_bits(cnt, nums[left], -1)
gauche += 1

retour -1 si ans == flotter('inf') sinon ans

@staticmethod
def _add_bits(cnt: List[int], num: int, delta: int) -> Aucun:
pour i dans la fourchette(32):
si (num >> i) & 1:
cnt[i] += delta

@staticmethod
def _current_or(cnt: List[int]) -> Int:
Valeur = 0
pour i, c dans l'énumération(cnt):
si c:
Valeur = (1 < < i)
retour val
«» "

C++

'`cpp
solution de classe {
public:
Length(vecteur <int>& nums, int k) {
tableau<int, 32> cnt{}; // tous les zéros initialement
int gauche = 0, ans = INT_MAX;

pour (int right = 0; right < (int)nums.size(); ++right) {
AddBits(cnt, nums[right], 1);

pendant que (gauche <= droite && courantOr(cnt) >= k) {
ans = min(ans, droite - gauche + 1);
AddBits(cnt, nums[left], -1);
+ + gauche;
}
}
retour (ans == INT_MAX) ? -1 : ans;
}

particulier:
La Commission a décidé de ne pas modifier le règlement (CEE) n° 1408/71. {
pour (int i = 0; i < 32; ++i) {
si ((num >> i) et 1)
cnt[i] += delta;
}
}

Int courant Ou (tableau const<int, 32>& cnt) {
Int val = 0;
pour (int i = 0; i < 32; ++i)
si (cnt[i] > 0)
la valeur = (1 < < i);
valeur de retour;
}
};
«» "

---

- Oui. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
Autres **Complexité du temps**= O(n) → passe facilement== Naïve O(n2) utiliserait des opérations bitwise (p. ex., reconstruction OU avec une boucle de 64 bits) pourrait encore être **lent**=
**L'espace **= Constante (32 ints)== Un tableau `ou` supplémentaire n'est pas nécessaire== L'oubli de réinitialiser les nombres mène à **incorrecte OU**==
**Mise en oeuvre**= Aides claires (`addBits`, `currentOr`) → lisibilité======================================================================================================================================================================================================================================
**Portabilité**= Fonctionne en Java, Python, C++=Certains langages ont besoin d'entiers 64 bits=En Java, `1 << 31` est négatif mais toujours correct – peut confondre les nouveaux arrivants=
**Maintenabilité**= Logique du compte de bits réutilisable== Aucun=L'utilisation de `unordered_map<int,int>` par bits serait **overkill** Autres

---

- Oui. Comment atterrir cette entrevue

1. **Afficher le processus de pensée** – Commencez par expliquer pourquoi une double boucle naïve est trop lente.
2. **Explain OU Monotonicity** – Les intervieweurs aiment voir que vous comprenez la propriété centrale qui rend une fenêtre coulissante viable.
3. **Highlight Constant‐Time Bit Operations** – Mention que 32 bits → constante, de sorte que la boucle «Inner» est toujours O(1).
4. **Test Edge Cases** – Demandez à l'intervieweur de penser à `k == 0`, tous les zéros, etc.
5. **Mention Space** – 32 compteurs sont négligeables; vous pouvez même les compresser en entier 32 bits si vous voulez être fantaisiste.
6. **Écrire un code propre** – Comme indiqué ci-dessus, utilisez des fonctions d'aide et évitez les nombres magiques.

> Pourquoi ajoutez-vous et supprimez-vous des bits ? Est-ce que OU associé?
> Réponse : C'est associatif, mais parce que nous avons besoin de détecter quand le OR tombe sous k tout en rétrécissant, nous suivons combien d'éléments contribuent à chaque bit. Ça nous dit quand un peu disparaît. (en milliers de dollars)

---

- Oui. Dernier départ

- **LeetCode 3097** est un exemple de manuel de la façon dont une simple observation (le OU grandit seulement) vous permet de convertir une force brute O(n2) en un algorithme de fenêtre coulissante O(n).
- Oui. Le point de vue clé est de garder un tableau **fréquence de bits** au lieu de recalculer le OU de zéro.
- Oui. La solution est *language‐agnostic* : elle fonctionne en Java, Python, C++ et toute autre langue avec des entiers 32 bits.

> **Tip pour recruteurs**: Mentionnez que votre solution utilise des opérations bit *constante-time*, ce qui la rend *super rapide* même sur les limites supérieures des contraintes. C'est exactement le genre de "performance-aware" que les intervieweurs de pensée recherchent.

Bon codage ! C'est ce qu'il a dit