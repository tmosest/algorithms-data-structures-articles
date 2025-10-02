---
Titre: LeetCode 1869. Segments plus longs et plus contigués que les zéros -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1869 – Segments plus longs et plus contigus que les zéros
### Le bon, le mauvais et le mauvais – Un guide d'entrevue complet
*(Java / Python / C++ solutions + SEO-friendly blog post)*

---

Récapitulation des problèmes
**LeetCode #1869 – Segments plus longs et plus contigus que les zéros**

> **Donné** d'une chaîne binaire `s`, retourner `true` si le segment contigu le plus long de `1`-S est ** strictement** plus long que le segment contigu le plus long de `0`-S; sinon retourner `false`.
>
> **Exemples**
> ```texte
> s = "1101" → true (max.1-run = 2, max 0-run = 1)
> s = "111000" → faux (max.1-run = 3, max 0-run = 3)
> s = "110100010" → faux (max. 1-run = 2, max 0-run = 3)
> `` "
> **Règles d'âge** – Si la chaîne ne contient pas de `0`s, le max 0‐run est considéré comme `0` (et vice-versa).

---

- Oui. Pourquoi ce problème est-il à l'origine de votre entrevue?

**Aspect**
- C'est quoi ?
**Temps-Optimal**= O(n) col simple, qui est la norme de l'or pour les questions d'entrevue. Autres
**Space‐Optimal**= O(1) mémoire supplémentaire – démontre l'utilisation consciente des ressources. Autres
**Manipulation d'attache**= Compétence de base pour tout rôle logiciel; montre que vous pouvez traiter les caractères efficacement. Autres
Autres **Edge-Case Awareness** Extrêmement capable de penser aux runs vides et aux chaînes de longueur. Autres

---

- Oui. Le bien – la solution propre et idiomatique

L'idée principale : ** suivre deux compteurs pendant l'itération** – un pour la séquence courante de `1`s, un pour la séquence courante de `0`s.
Lorsque la stries est cassée, mettez à jour le maximum correspondant et réinitialisez le compteur.

Java

"Java
// Java 17 – temps O(n), espace O(1)
solution de classe publique {
boolean public checkZeroOnes(String s) {
l'inté maxOne = 0, maxZero = 0;
Int curOne = 0, curZero = 0;

pour (int i = 0; i < s.longueur(); i++) {
c = s.charAt(i);
si (c) «1») {
curOne++; // continuer 1-run
curZero = 0; // réinitialiser 0-run
si (curOne > maxOne) maxOne = cur Un;
} autre { // c == '0'
curZero++;
curOne = 0;
si (curZero > maxZero) maxZero = cur Zéro;
}
}
retour maxOne > max Zéro;
}

// harnais d'essai simple
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
System.out.println(sol.checkZeroOnes("1101")); // true
System.out.println(sol.checkZeroOnes("111000")); // faux
Système.out.println(sol.checkZeroOnes("110100010")); // faux
}
}
«» "

Python

'`python
# Python 3 – temps O(n), espace O(1)
Solution de classe:
Contrôle ZéroOnes(self, s: str) -> C'est vrai.
max_one = max_zero = 0
cur_one = cur_zero = 0

pour ch en s:
si ch == '1':
_une 1
_zéro = 0
si _couron > _une max :
max_one = cur_one
Sinon : # ch == '0'
_zéro 1
_une = 0
si cur_zero > _zéro max :
max_zero = cur_zero

retourner max_one > max_zero


♪ Démo
si __nom__ == "__main__" :
sol = Solution()
print(sol.checkZeroOnes("1101")) # True
print(sol.checkZeroOnes("111000") # Faux
print(sol.checkZeroOnes("110100010")) # Faux
«» "

C++

'`cpp
// C++17 – temps O(n), espace O(1)
solution de classe {
public:
Chèque de boolZeroOnes(chaîne s) {
l'inté maxOne = 0, maxZero = 0;
Int curOne = 0, curZero = 0;

pour (charc : s) {
si (c) «1») {
++curOne;
curZero = 0;
maxOne = max(maxOne, curOne);
} autre { // c == '0'
++curZero;
curOne = 0;
maxZero = max(maxZero, curZero);
}
}
retour maxOne > max Zéro;
}
};

#incluez <iostream>
Int main() {
Solution sol;
ms::tout << ms::boolalpha;
std::cout << sol.checkZeroOnes("1101") << '\n'; // true
std::tout << sol.checkZeroOnes("111000") << '\n'; // faux
std::coupe << sol.checkZeroOnes("110100010") << '\n'; // faux
}
«» "

---

- Oui. Les pièges communs

Pourquoi il fait défaut
Ce n'est pas le cas.
**Off‐by‐one dans les compteurs**= Oublier de réinitialiser le compteur opposé après une course. Toujours réinitialiser le compteur *other* à `0` sur chaque caractère. Autres
**Ignorer la série finale**= Mise à jour du maximum seulement quand une série se brise. Mettre à jour le maximum à la fin de la boucle ou après chaque incrément. Autres
**Comparaison des erreurs**==` en utilisant `>=` au lieu de `>` pour la période plus longue. Autres Le problème dit explicitement *strictement*, ainsi utilisez `>` seulement. Autres
**Logique complexe** Stick à une seule passe, deux compteurs. Autres
**Données erronées**= Utiliser `int[]` ou `StringBuilder` lorsque `int` est suffisant. Pour rester simple – les compteurs `int` suffisent. Autres

---

C'est pas vrai. Le «Ugly» – Sur-ingénierie

Parfois, les intervieweurs testent si vous pouvez garder votre solution *simple*:

- **Regex hack**: `s.split("0")` et `s.split("1")` pour obtenir des longueurs d'exécution.
*Ugly car* il alloue de nombreux tableaux et est O(n) *mais* plus lent et plus difficile à lire.
- ** Approche à deux passages** : Première analyse pour max 1-run, seconde pour max 0-run.
*Parce que* il double le travail quand un seul passe suffit.

**Ligne de bottom:** Visez un code *propre, concis et déterministe*.

---

Analyse de complexité

Langue Heure Espace
- C'est quoi ?
Java **O(n)** (passe unique)
Python **O(n)**
* * * * * * * * *

`n` = longueur de la chaîne (`1 ≤ n ≤ 100` par contrainte).

---

## 7=1 Interview-Ready Points de discussion

1. **Re-statement du problème** – Clarify plus longtemps par rapport à plus grand ou égal.
2. **Edge Cases** – Tester les chaînes de toutes les `1`s, toutes les `0`s, longueur‐1, en alternance.
3. **Exposer l'approche à deux counter** – C'est la solution O(n) la plus simple.
4. **Pourquoi O(1) L'espace compte** – Démontre une utilisation prudente des ressources.
5. **Demander des éclaircissements** – par exemple, la comparaison devrait-elle être stricte?

---

Variations et extensions

- **La plus longue sous-chaîne d'égale longueur** → retourner `true` si la plus longue 1-run *égale* la plus longue 0-run.
- **Plus de deux symboles** – généraliser à plus long terme de n'importe quel personnage.
- **Fenêtre coulissante** – pas nécessaire ici, mais bonne pour la diversité des interviews.

---

Description de la méta optimisée (pour le blog)

> Code maître de leet 1869 – Segments plus longs et contigus que les zéros. Lisez un guide complet avec les solutions Java, Python et C++, l'analyse de cas de bord, des conseils d'entrevue et comment asses ce problème dans toute entrevue de codage. (en milliers de dollars)

---

À emporter

- **Soyez simple**: Une passe, deux compteurs, comparaison directe.
- **Testez attentivement**: Inclure des cas bord qui brisent des solutions naïves.
- **Exposer avec confiance**: Faites passer l'intervieweur à travers la logique, l'espace et le temps.

Avec ces extraits et idées, vous êtes prêt à affronter LeetCode 1869, impressionner les gestionnaires d'embauche, et vous rapprocher de votre rôle d'ingénierie logicielle de rêve. C'est ce qu'il a dit.

---