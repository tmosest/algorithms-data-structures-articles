---
titre: LeetCode 424.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Remplacement de caractères répétitifs le plus long – LeetCode 424
*Java • Python • C++ Solutions + In-Depth Blog Post*

---

Déclaration de problème

> **Grâce à une chaîne de caractères `s` composée uniquement de lettres anglaises majuscules et d'un entier `k`, vous pouvez changer au maximum de caractères `k` dans `s` à toute autre lettre majuscule. Retournez la longueur de la plus longue sous-chaîne qui peut contenir la même lettre après les remplacements. **

> **Exemple**
> `s = "ABAB", k = 2` → **4** (changer les deux `A`=" en `B`=" ou vice-versa)
> `s = "AABABBA", k = 1` → **4** (modifier le milieu `A` en `B` → `"AABBBBA"` → `"BBBB"`)

**Contrôles* *

- Oui.
-- -- -- -- -- --
1 <= s.longueur <= 10^5`= 0 <= k <= s.longueur` Autres
"s" contient seulement des lettres majuscules Autres

---

Pourquoi ce problème est-il un savoir-faire pour les entrevues

* **Fenêtre de glissement classique** – démontre la maîtrise de la technique à deux points.
* **Composition de fréquence** – montre du confort avec des cartes de hachage / tableaux de taille fixe.
* **Le temps optimal contre l'espace** – parfait pour discuter des compromis asymptotiques.
* **Analogie du monde réel** – problèmes de nettoyage et de normalisation des données.

---

## ♫ Idées de base – Fenêtre coulissante +

Quand on regarde n'importe quelle sous-chaîne, la seule chose qui compte est :

1. La longueur de la fenêtre
2. Le compte du caractère ** le plus fréquent** à l'intérieur de cette fenêtre

Si la longueur de la fenêtre moins le nombre de caractères le plus fréquent est **= k**, nous pouvons changer les caractères restants en caractères fréquents, rendant l'ensemble de la fenêtre uniforme.
Sinon la fenêtre est invalide et nous devons la réduire de la gauche.

L'astuce est que la valeur la plus fréquente est **monotonique** – elle ne diminue jamais à mesure que la fenêtre grandit, de sorte que nous pouvons garder une variable `maxFreq` unique et la mettre à jour seulement lorsque le nombre d'un nouveau caractère devient plus grand.

---

La complexité temporelle et spatiale

- Oui.
-- -- -- -- -- --
**Heure**="O(n)" – chaque index est ajouté et supprimé au plus une fois. Autres
**Espace** – tableau fixe de taille 26 (ou dictionnaire de taille ≤ 26). Autres

---

Cas de bord et pièges communs

Pièges
C'est pas vrai.
Autres 1= Oublier de soustraire la fréquence sortante du char=s lors du rétrécissement de la fenêtre. Toujours décrémenter `freq[s[left] - 'A']` avant de déplacer `gauche`. Autres
En utilisant `int` pour `maxFreq` mais pas en le mettant à jour quand il diminue. **Ne recalculez pas "maxFreq" sur le rétrécissement – gardez-le monotonique ; il n'augmente que *. Autres
Utiliser `<= k` vs `< k` dans la vérification de validité. L'état correct est `windowLen - maxFreq <= k`.
Autres Le calcul de la longueur de la fenêtre (fin - gauche + 1). Utiliser `end - gauche + 1` ou `end + 1 - gauche '. Autres

---

Code – Java

"Java
solution de classe publique {
***
* Le remplacement le plus long des caractères répétés (LeetCode 424)
*
* @param s La chaîne d'entrée des lettres majuscules.
* @param k Le nombre maximal de remplacements autorisés.
* @retour La longueur de la plus longue sous-chaîne qui peut être faite tout de même.
*/
caractère int publicRemplacement(String s, int k) {
int gauche = 0; // démarrage de la fenêtre
int maxFreq = 0; // fréquence la plus élevée dans la fenêtre actuelle
int[] freq = nouvelle int[26]; // fréquence de chaque lettre

int best = 0; // meilleure longueur de fenêtre vue

pour (int droite = 0; droite < s.longueur(); droite++) {
int idx = s.charÀ droite - 'A';
freq[idx]++; // inclure un nouveau char

maxFreq = Math.max(maxFreq, freq[idx]);

// Si nous avons besoin de plus de k changements, rétrécir de gauche
si (droite - gauche + 1 - maxFreq > k) {
int leftIdx = s.charAt(gauche) - 'A';
freq[leftIdx]--; // supprimer char laissant la fenêtre
gauche++; // Déplacer la fenêtre
}

best = Math.max (meilleur, droit - gauche + 1);
}

le meilleur retour;
}
}
«» "

---

Code – Python

'`python
Solution de classe:
def characterReplacement(self, s: str, k: int) -> Int:
"""
Fenêtre coulissante avec tableau de fréquences fixes (taille 26).
"""
gauche = 0
max_freq = 0
freq = [0] * 26
meilleur = 0

pour droite, ch en énumération(s):
idx = ord(ch) - ord('A')
freq[idx] += 1
max_freq = max(max_freq, freq[idx])

si droite - gauche + 1 - max_freq > k:
freq[ord(s[left]) - ord('A')] -= 1
gauche += 1

best = max (meilleur, droit - gauche + 1)

le meilleur retour
«» "

---

Code – C++

'`cpp
solution de classe {
public:
caractère intRemplacement(chaîne s, int k) {
vecteur <int> freq(26, 0);
int gauche = 0, maxFreq = 0, meilleur = 0;

pour (int droite = 0; right < (int)s.size(); ++right) {
int idx = s[right] - 'A';
freq[idx]++;
maxFreq = max(maxFreq, freq[idx]);

si (droite - gauche + 1 - maxFreq > k) {
[à gauche] - 'A']--;
+ + gauche;
}

best = max (meilleur, droit - gauche + 1);
}
le meilleur retour;
}
};
«» "

---

Le bon, le mauvais et le mauvais

Introduction

> **Remplacement de caractères le plus long** (LeetCode 424) est un problème apparemment simple qui cache un aperçu profond de *l'optimisation par fenêtre* et *la comptabilité par fréquence*. C'est une base dans les portefeuilles d'entrevues pour une bonne raison: il teste la capacité d'un candidat à:
>
> 1. Formuler un invariant de fenêtre coulissante
> 2. Maintenir efficacement l'état auxiliaire
> 3. Raison des limites les plus défavorables
> 4. Communiquer clairement leur approche
>
> Dans cet article, nous allons marcher à travers le "good" (pourquoi l'algorithme est élégant), le "bad" (pièges communs et idées fausses), et le "ugly" (des approches moins optimistes qui fonctionnent encore, mais vous obtiendrez rejeté dans une interview chronométrée).

### La bonne – Une solution élégante pour le vent

1. **Invariant**
*La fenêtre est valide si `windowLen - maxFreq <= k`.*
Ce simple contrôle garantit que nous n'avons jamais besoin de scanner toute la fenêtre pour des modifications.

2. **Monotonique `maxFreq`**
*Pourquoi on peut sauter la recomposition*
`maxFreq` augmente seulement à mesure que nous élargissons la fenêtre. Même si nous laissons tomber le char le plus fréquent, le précédent `maxFreq` est toujours un *bound inférieur* sur le vrai maximum pour la fenêtre réduite. Cette subtilité nous permet de garder l'algorithme linéaire sans passes supplémentaires.

3. **O(1) Espace**
Un tableau fixe de 26 int est trivial comparé à la longueur potentielle de 10^5 de la chaîne.

- Oui. Le mauvais – ce qui rompt habituellement les candidats

Problème Symptômes Correction
C'est le cas.
**Recomputing frequence on srrink**
**Formule de la longueur de la fenêtre de Wong**
**Utiliser `<= k` de manière incorrecte**= Cas d'échec d'essai== Valider l'état avec des exemples simples (`"AB", k=1` → 2)=
**État mutable après la boucle**

### L'Ugly – Alternatives qui passent toujours mais pas l'échelle

L'approche de la complexité Pourquoi c'est bizarre
C'est le cas.
**Binary Recherche sur la longueur de la réponse + contrôle**
**Force-brute avec boucles imbriquées** Dépasse les délais pour 105
Autres **Utiliser une `Carte<Caracter, Deque<Intégrer>>`**

Bien que ces approches puissent gagner sur de petits cas de test, les intervieweurs recherchent des solutions * propres et optimales*.

Comment parler Dans une interview

1. **Énoncez le problème dans vos propres mots** – vous assure de comprendre le but.
2. **Expliquez l'invariant de la fenêtre coulissante** – montrez-vous en termes de fenêtres *valides/invalides*.
3. **Discuss `maxFreq` monotonicité** – c'est le crux qui le maintient linéaire.
4. **Cas de bord de Mention** – par exemple, `k = 0`, `s` de longueur 1, tous les caractères identiques.
5. **Parlez de la complexité** – les intervieweurs aiment voir une justification claire "O(n)"/ "O(1)".

Résumé

- **Bien**: Temps linéaire, espace constant, élégant invariant.
- **Bad**: Commun off-by-one, recomputation, mauvais état.
- **Ugly**: Variantes de recherche quadratique ou binaire qui perdent du temps.

Maîtriser ce problème indique que vous pouvez gérer *les contraintes dynamiques* et *les optimisations basées sur la fréquence* – compétences très prisées par les entreprises de haute technologie.

---

## -Référencement optimisé

> Vous cherchez à décrocher un rôle d'ingénierie logicielle? Maîtrise **LeetCode 424 – Remplacement de caractères répétitifs le plus long** montre votre compétence dans la fenêtre de glissement**, la manipulation de chaînes** et la conception d'algorithmes optimaux**.
> Plongez dans nos solutions Java, Python et C++, lisez le blog détaillé pour le **bon, mauvais et laid** de cette question d'interview classique, et augmentez votre confiance en interview aujourd'hui!

---

Bonus – Harnais d'essai rapide (facultatif)

"Java
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.caractèreRemplacement("ABAB", 2)); // 4
Système.out.println(sol.caractèreRemplacement("AABABBA", 1)); // 4
}
«» "

'`python
si __nom__ == "__main__" :
sol = Solution()
print(sol.caractèreRemplacement("ABAB", 2)) # 4
print(sol.caractèreRemplacement("AABABBA", 1)) # 4
«» "

'`cpp
Int main() {
Solution s;
Cout << s.caracterRemplacement("ABAB", 2) << enl; // 4
Cout << s.caracterRemplacement("AABABBA", 1) << enl; // 4
}
«» "

Bon codage et bonne chance pour votre prochaine interview!