---
titre: LeetCode 1703. Swaps adjacents minimum pour K Consécutifs -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1703 – Swaps adjacents minimums pour K consécutif Les
**Un guide complet et optimisé pour les développeurs d'emplois**

> * Lien du problème : * <https://leetcode.com/problèmes/minimum-adjacent-swaps-for-k-consecutive-ones/>
> *Tags:* Deux-Pointeurs:

---

Déclaration du problème

Compte tenu d'un tableau binaire `nums` (`0` / `1`) et d'un entier `k`, vous pouvez échanger deux **éléments adjacents** en un seul mouvement.
Retourner le nombre de mouvements *minimum* requis pour que le tableau contienne **`k` consécutif `1`s**.

**Contrôles* *

Variable Limites
C'est pas vrai.
"nums.longueur" "1 ... 10^5" Autres
Nombres "0" ou "1"
< < k > > 1 ... somme(s) > > Autres

---

Pourquoi ce problème se pose

* Sujet d'interview classique : ** manipulation dearray + fenêtre coulissante**.
* Souligne votre capacité à optimiser *temps* et *espace* – un grand plus sur le radar d'embauche.
* Vous donne une chance de pratiquer **préfixer les sommes**, **la logique médiane** et **le raisonnement de bonne humeur** – tous les concepts favorables à l'entrevue.

---

Les bons, les mauvais, les affreux

Catégorie Ce que vous allez apprendre Complexité de mise en œuvre
C'est ce que j'ai dit.
**Bon*** *O(n)* solution utilisant la médiane des positions + les montants préfixes. **Fast, clean, scalable** – idéal pour les interviews de codage. Autres
**Modalités d'approche de Brute-force O(nk) ou O(n2) (doubles boucles, montants de distance répétés). **Horaires** sur les grandes entrées. Autres
**Les structures de données lourdes (segments d'arbres, arbres indexés binaires) ou les maths trop intelligents qui obscurcissent l'intention. Autres

Nous allons parcourir la solution **good** en détail, montrer pourquoi les mauvais échouent, et vous donner le code prêt-à-coller dans **Java, Python, et C++**.

---

Le point de vue central

1. **Collectez les indices de tous les «1»** – «pos».
2. Toute fenêtre de `k` peut être déplacée pour devenir consécutive.
3. La cible *optimale* est de centrer le bloc autour du **médiane** de la fenêtre.
4. Distance pour un `1` = `abs( pos[i] - pos[mid] - (i - mi) '.
5. Cela simplifie les mots `abs( (pos[i] - i) - (pos[mid] - mi)'.

Ainsi, si nous précalculons `arr[i] = pos[i] - i`, le coût d'une fenêtre est la somme des différences absolues à sa médiane.

---

## O(1) Coût par fenêtre (après O(n) Prétraitement)

Que `préf[i]` soit la somme préfixe de `arr`.

Pour la fenêtre `[l ... r]` (`k = r-l+1`), indice médian `m = l + k/2` (division entière).

Coût =

«» "
(côté gauche) = arr[m] * (m-l) - (pref[m-1] - pref[l-1])
(côté droit) = (préf[r] - pref[m]) - arr[m] * (r-m)
«» "

Total = côté gauche + côté droit

Toutes les opérations sont O(1), donc l'algorithme entier tourne dans le temps O(n) et dans l'espace O(n).

---

Mise en œuvre du code

Ci-dessous vous trouverez des implémentations propres et commentées dans **Java, Python et C++**.

> **Astuce:** Pour le code Java, n'oubliez pas d'utiliser `long` pour calculer les sommes pour éviter les débordements (bien que la réponse corresponde à `int` pour les contraintes données).

---

Java (O(n) Fenêtre coulissante + Préfixe Sum)

"Java
Importation de java.util.*;

solution de classe publique {
int public minMoves(int[] nums, int k) {
// 1. Recueillir les postes de tous les
Liste <Integer> pos = nouvelle liste de distribution<>();
pour (int i = 0; i < nombres de longueur; i++) {
si (nombres [i]] 1) pos.add(i);
}

int m = pos.size(); // nombre total de 1's
si (k == m) retourne 0; // déjà consécutif

// 2. Construire arr[i] = pos[i] - i
long[] arr = nouveau long[m];
pour (int i = 0; i < m; i++) arr[i] = pos.get(i) - i;

// 3. Préfixer les sommes d'arr
long[] pref = nouveau long[m];
pref[0] = arr[0];
pour (int i = 1; i < m; i++) pref[i] = pref[i-1] + arr[i];

int ans = entier. MAX_VALEUR;
pour (int l = 0; l + k - 1 < m; l++) {
t r = l + k - 1;
int milieu = l + k / 2; // indice médian
long médian = arr[mid];

longue gauche = médiane * (milieu - l) - (milieu > l ? - préf[l-1] : 0);
longue droite = (préf[r] - préf[mid]) - médiane * (r - milieu);

ans = (int)Math.min(ans, (int)(gauche + droite));
}
le retour des an;
}
}
«» "

---

Python (O(n) Fenêtre coulissante + Préfixe Sum)

'`python
Solution de classe:
def minMoves(self, nombres: List[int], k: int) -> Int:
1. Positions de 1's
pos = [i pour i, v dans le dénombrement(nums) si v]. 1]
m = len(pos)
Si k == m:
retour 0

# 2. arr[i] = pos[i] - i
arr = [pos[i] - i pour i dans l ' intervalle(m)]

3. Préfixer les sommes
pref = [0] * m
ff[0] = arr[0]
pour i à portée (1, m):
pref[i] = pref[i-1] + arr[i]

ans = 10**9
pour l dans la plage (0, m - k + 1):
r = l + k - 1
milieu = l + k // 2
médiane = arr[mid]

gauche = médiane * (milieu - l) - (préf[milieu-1] - pref[l-1] si mi > l autres 0)
droite = (préf[r] - préf[mid]) - médiane * (r - milieu)

ans = min(ans, gauche + droite)

retour et
«» "

---

### C++ (O(n) Fenêtre coulissante + Préfixe Sum)

'`cpp
solution de classe {
public:
int minMoves(vecteur<int>& nums, int k) {
vecteur <int> pos;
pour (int i = 0; i < nums.size(); ++i)
si (nums[i]] 1) pos.push_back(i);

int m = pos.size();
si k == m) retourne 0;

vecteur <long> arr(m);
pour (int i = 0; i < m; ++i) arr[i] = (long)pos[i] - i;

vecteur <long> pref(m);
pref[0] = arr[0];
pour (int i = 1; i < m; ++i) pref[i] = pref[i-1] + arr[i];

long an = LLONG_MAX;
pour (int l = 0; l + k - 1 < m; ++l) {
t r = l + k - 1;
int milieu = l + k / 2;
long long médian = arr[mid];

longue gauche = médiane * (milieu - l) - (milieu > l ? - préf[l-1] : 0);
longue droite = (préf[r] - préf[mid]) - médiane * (r - milieu);

ans = min(ans, gauche + droite);
}
retour (int)ans;
}
};
«» "

> **Note:** Nous utilisons `long' pour les calculs préfixes et intermédiaires – la réponse finale correspond confortablement à un `int`.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Recueillir les indices
Construisez "arr"
Construire des montants préfixés **O(m)**
Analyse de la fenêtre coulissante
**O(n)**

Parce que `m ≤ n`, la complexité globale est linéaire et efficace pour la mémoire.

---

Pièges et correctifs communs

Piège
- Oui.
**Débordement entier** lors du cumul des distances. Autres
Erreurs hors-par-un sur les montants préfixés («pref[l-1]») "Garde avec "si (mid > l)" ou utiliser des valeurs sentinelles. Autres
La mauvaise médiane pour les fenêtres de longueur égale.La division entière (`k/2`) fonctionne parce que le coût est symétrique. Autres
Autres Oubliant de soustraire l'index offset (`i-mid`) Autres

---

Comment faire pour faire ça sur une entrevue en direct

1. ** Expliquez les positions de la collection → idée de décalage médian** avant de coder.
2. Afficher les maths pour `arr[i] = pos[i] - i` pour convaincre l'intervieweur que vous savez pourquoi la formule fonctionne.
3. Écrire le code dans **O(n)**, le tester avec les exemples donnés, et **vérifier** les cas de bord (`k=m`, tous les zéros, tous les).
4. Enfin, demandez s'ils aimeraient une version **Java / Python / C++** – c'est un signal subtil que vous êtes prêt à distribuer le code de travail.

---

Bonus : Pourquoi les solutions Bad et Ugly sont mauvaises

Une approche de la mise en œuvre typique Pourquoi il fait défaut
- C'est quoi ?
**O(nk)**"pour i dans l'intervalle(n): pour j dans l'intervalle(i,i+k): sum(abs(pos[j] - pos[i] - (j-i))"" Pour `n = 10^5` et `k = 10^4`, vous touchez ~10^9 opérations → **Délai dépassé**. Autres
**O(n2)**= Doubles boucles imbriquées sur toutes les distances `1` pour calculer les distances.= Même avec les petits `k`, le pire cas explose encore. Autres
Autres **Segment Tree / BIT**.Maintien de nombres de `1`s pour les requêtes de gamme dynamique. Autres

---

Comment cela vous stimule

Compétences
C'est pas vrai.
Autres **Greedy + Médiane**=Il montre que vous pouvez trouver un centre optimal dans une liste de positions. Autres
**Prefix Sum**= Indique la familiarité avec l'un des plus puissants tours de requête O(1). Autres
**Two-Pointer Sliding Window**= Une base de nombreuses entrevues de codage – les recruteurs adorent. Autres
**La sensibilisation à la complexité du temps** Autres

Lorsque vous présentez cette solution à un gestionnaire d'embauche, parlez comme ceci :

> J'ai résolu LeetCode 1703 en **O(n)** temps en glissant une fenêtre sur les indices de `1`s, en centrant chaque bloc sur la médiane, et en utilisant des montants préfixes pour calculer le coût en temps constant. (en milliers de dollars)

Cette seule phrase est un bon point de discussion dans toute interview.

---

## Résumé à emporter

1. **Collecter les indices** → `pos`.
2. Transformer chaque indice: `arr[i] = pos[i] - i`.
3. Préfixer les sommes d'arr.
4. Pour chaque fenêtre de taille `k`, calculer le coût en O(1) en utilisant la logique médiane.
5. Résultat dans **O(n)** temps, **O(n)** espace.

Vous avez maintenant *prêt à utiliser* code dans trois langues populaires et une explication complète qui impressionnera les recruteurs.

---

Étapes suivantes – Construisez votre portefeuille

Pourquoi ça compte ?
-- -- -- -- -- --
Autres **Ajouter cette solution à votre GitHub** avec un README qui inclut l'explication ci-dessus. Démontrer des compétences en résolution de problèmes et en documentation dans le monde réel. Autres
**Écrire un article de blog** ou un tweet sur cette solution. Montrez vos côtes de communication. Autres
**Préparer des questions de suivi** comme : Montre la profondeur de la pensée et de la curiosité. Autres

---

Dernier appel à l'action

> **Si vous préparez une entrevue d'ingénierie logicielle,** faites du LeetCode 1703 une partie de votre liste d'entretien Warm-Up.
> Clone la repo ci-dessous, exécutez les tests, et vous serez prêt à ** déposer la réponse O(n)** dans tout défi de codage ou session de tableau blanc.

"""
clone git https://github.com/votre-nom d'utilisateur/codeleet-1703-min-swaps
cd leetcode-1703-min-swaps
♪ Lancez le harnais de test de votre choix
«» "

Bon codage, et bonne chance d'atterrissage ce rôle de rêve! *

---