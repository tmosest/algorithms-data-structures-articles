---
titre: LeetCode 1814. Comptez les belles paires dans un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1814. Comte Nice Pairs in an Array – Une solution complète, prête à l'entrevue
C++*

---

TL;DR
- **Problème** – Compter le nombre de paires d'indices *(i, j*) avec `i < j` de sorte que
"nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])".
- **Point de vue principal** – L'équation est équivalente à "nums[i] – rev(nums[i]) == nums[j] – rev(nums[j])".
- **Solution** – Calculer la valeur `d = nums[k] – rev(nums[k])` pour chaque élément, stocker la fréquence de chaque `d` dans une carte de hachage, et compter `freq[d] choisir 2` paires.
- **Complexité** – temps `O(n)`, `O(n)` espace supplémentaire (où `n = longueur nums').
- **Modulo** – Toutes les réponses sont prises modul "1 000 000 007".

---

- Oui. 1. Récapitulation des problèmes (à partir de LeetCode)

> On vous donne un tableau `nums` d'entiers non négatifs.
> `rev(x)` est l'inverse de l'entier `x`.
> Une paire `(i, j)` est *nice* si `i < j` et
> `nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])».
> Retourner le nombre de jolies paires modulo `1 000 000 007`.

---

- Oui. 2. Pourquoi l'astuce de la différence

«» "
nombres[i] + rev(nums[j]) == nombres[j] + rev(nums[i])
Liste des membres de l'Assemblée générale
«» "

*Proof* – Déplacer les termes contenant le même indice du même côté :

«» "
nombres[i] - rev(nums[i]) = nombres[j] - rev(nums[j])
«» "

Ainsi deux indices forment une belle paire **iff** leurs différences* sont égales.
Ainsi, le problème s'effondre à : *compter combien de valeurs égales de la différence de . *

---

- Oui. 3. Algorithme

1. **Aide inversée** – convertir un entier en sa forme inversée.
2. Pour chaque élément «x» en «nums»:
* `d = x - rev(x)` (entreposer dans un `long`/`long long` pour éviter le débordement).
* Incrémenter le compteur de `d` sur une carte de hachage.
3. Après la numérisation, pour chaque `d` distinct avec la fréquence `c` ajouter
`c * (c – 1) / 2` à la réponse (modulo `MOD`).
4. Retourne la réponse.

---

- Oui. 4. Code

#### 4.1 Java (8+)

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

Compte de l'entreprise publiqueNicePairs(int[] nums) {
Carte <Long, Long> freq = nouveau HashMap<>();

pour (int x : nombres) {
long d = x - inverse(x);
freq.merge(d, 1L, Long::sum);
}

long ans = 0;
pour (long c : valeurs freq.()) {
si c > 1) {
ans = (ans + (c * (c - 1) / 2) % MOD) % MOD;
}
}
retour (int) ans;
}

intérieur long inverse(int num) {
long rev = 0;
pendant la période 0) {
rev = rev * 10 + num % 10;
num /= 10;
}
retour rev;
}
}
«» "

4.2 Python 3

'`python
Solution de classe:
MOD = 1 000 000 007

def countNicePairs(self, nombres: List[int]) -> Int:
freq = {}
pour x en nombres:
d = x - self._rev(x)
freq[d] = freq.get(d, 0) + 1

ans = 0
pour c en valeurs fréq.():
ans = (ans + c * (c - 1) // 2) Pourcentage de soi. MOD
retour et

def _rev(self, num: int) -> Int:
rev = 0
alors que num:
rev = rev * 10 + num % 10
NUM //= 10
retour rev
«» "

### 4.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int countNicePairs(vecteur<int>& nums) {
longue MOD = 1'000'000'007LL;
non ordonné_map<long long, long> fréq;

pour (int x : nombres) {
long long d = (long long)x - inverseNum(x);
++freq[d];
}

long an = 0;
pour (auto &p : freq) {
long c = p.seconde;
si c > 1)
ans = (ans + (c * (c - 1) / 2) % MOD) % MOD;
}
retour (int)ans;
}

particulier:
long long inverseNum(int n) {
long rev = 0;
pendant que (n) {
rev = rev * 10 + n % 10;
n/= 10;
}
retour rev;
}
};
«» "

---

- Oui. 5. Blog-Style Article: *Les bonnes, les mauvaises, et l'acharnement de compter les belles paires*

> **Meta-description (SEO)** – Vous voulez décrocher cette entrevue de codage?
> Master LeetCode 1814 : Coupez de belles paires en Java, Python et C++ !
> Apprenez l'astuce, les pièges et les conseils d'entrevue du monde réel.

---

#### 5.1 Le bon – Ce qui fait de ce problème une médaille d'or

1. **Simplicité des mathématiques** – Une fois que vous remarquez l'astuce d'annulation (`x - rev(x)`), tout le problème s'effondre à un nombre de fréquence.
2. **Haute performance** – La solution O(n) fonctionne confortablement pour les contraintes maximales (numéros 10^5).
3. **Language-agnostique** – La même idée correspond à Java, Python, C++, Allez, etc., afin que vous puissiez répondre dans la langue que préfère l'intervieweur.
4. ** Grande vitrine d'entrevue** – Démontre :
- Capacité de repérer la simplification algébrique.
- Utilisation appropriée des cartes de hachage pour le comptage.
- Manipulation de grands nombres avec arithmétique modulaire.

---

5.2 Les mauvaises – Pièges communs et comment les éviter

Pourquoi ça compte ?
- Oui.
**L'utilisation de `int` pour les valeurs inversées**. La suppression de 1 000 000 000 produit 1, ce qui est bien, mais les multiplications intermédiaires (par exemple, `rev * 10`) peuvent déborder `int`. Autres
Même si la réponse est plafonnée, des sommes intermédiaires comme `c * (c-1) / 2` peuvent déborder de 64-bit si `c` est énorme (théoriquement jusqu'à 10^5). Calculez le modulo après chaque ajout et jetez-le à "long long". Autres
**Ne pas manipuler les zéros** va sauter, donc vous devez gérer `num == 0' explicitement. Autres Initialiser `rev = 0` et utiliser ` while (num > 0)` (qui fonctionne), ou cas spécial zéro. Autres
**L'utilisation d'un tableau simple pour les fréquences**La valeur de la différence peut être négative, donc un tableau indexé par `d` n'est pas réalisable. Utiliser une carte/dictionnaire de hachage clé par `d`. Autres
** Erreurs hors-par-un**= N'oubliez pas que les paires sont *non ordonnées*: `(i, j)` et `(j, i)` sont les mêmes. La formule "c * (c-1)/2 " en tient compte. Vérifier avec de petits exemples. Autres

---

### 5.3 Les mauvais – Scénarios d'Edge-Case et tests de Tricky

Autres Test de la réponse attendue Pourquoi il est difficile
-- -- -- -- -- -- -- --
"nums = [0, 0, 0]" 3" Toutes les différences sont zéro; vous devez compter 3 paires. Autres
"nums = [100, 1]"" 0" `rev(100) = 1`, `rev(1) = 1`; différences: `99` et `0` → aucune correspondance. Autres
"Nums = [123456789, 987654321] "" Les deux ont des différences différentes mais "rev` retourne l'ordre. Autres
Autres Très grandes valeurs (près de `10^9') S'assurer que l'inverse ne déborde pas. Autres
La performance doit être linéaire. Autres

---

5.4 Entretien Entretien amical Voie

1. ** Expliquer l'observation**: `nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])` → `nums[i] - rev(nums[i]) == nums[j] - rev(nums[j])`.
2. **Énoncez l'approche**: calculez la différence de chaque nombre, utilisez une carte de hachage pour compter les différences identiques, puis utilisez la formule combinatoire.
3. **Faire ressortir la complexité**: temps O(n), espace O(n), facteur constant minuscule.
4. **Manipulation de l'enveloppe**: arithmétique 64 bits, modulo, zéros.
5. **Voir le code**: Une mise en œuvre concise dans la langue de choix.
6. **Optionnel**: Expliquez pourquoi nous utilisons `long` pour `rev` et `différence`.

---

5.5 A emporter

* La beauté de la Coupe Nice Pairs consiste à transformer une égalité apparemment complexe en un simple problème de comptage. En maîtrisant cette astuce, vous ne résolvez pas seulement LeetCode 1814 efficacement, mais démontrez également un état d'esprit puissant que les intervieweurs aiment : voir le modèle sous-jacent, réduire aux bases, et implémenter proprement. *

---

- Oui. 6. Liste de contrôle finale avant votre prochaine entrevue

- [ ] ** Expliquez clairement la simplification mathématique**.
- [ ] **Ecrivez un helper inversé** qui fonctionne pour 0 et évite les débordements.
- [ ] **Utilisez une carte de hachage** (`Map<Long, Long>` en Java, `unordered_map<long, long>` en C++, `dict` en Python).
- [ ] **Paires de comptes** avec `c * (c-1) / 2` et appliquer modulo `1 000 000 007`.
- [ ] **Test avec les cas de bord** (tous les zéros, grands nombres, données aléatoires).
- [ ] **Pratiquez le talk-track** pour répondre avec confiance en 2–3 minutes.

Bon codage, et bonne chance avec cette interview! C'est ce qu'il a dit