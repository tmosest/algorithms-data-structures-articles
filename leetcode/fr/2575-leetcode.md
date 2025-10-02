---
titre: LeetCode 2575. Trouver la disvisibilité d'une chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2575. Trouver la disvisibilité d'une chaîne
** Difficulté :** Moyenne **Temps:**

---

Récapitulation des problèmes

Avec une chaîne décimal `word` (longueur `n` jusqu`à `105`) et un entier `m` (`1 ≤ m ≤ 109`), retourner un tableau `div` de longueur `n` où

«» "
div[i] = 1 si l'entier représenté par mot[0 ... i] est divisible par m
div[i] = 0 autrement
«» "

L'analyse directe du préfixe dans un entier de 64 bits peut déborder, nous devons donc compter sur l'arithmétique modulaire.

---

## Idée de la solution – "Gardez le reste"

* Traitez la chaîne de gauche à droite.
* Maintenez le reste du préfixe actuel modulo `m`.
* `rem = (rem * 10 + chiffre) % m "
* Si "rem". 0` le préfixe actuel est divisible par `m`.
* Stocker `1` ou `0` dans le tableau de réponses.

Parce que `rem < m` en tout temps, nous ne débordons jamais, même si le nombre réel est astronomiquement grand.

---

Code

Voici des solutions propres et prêtes à la production pour **Java**, **Python** et **C++**.

---

### Java

"Java
solution de classe publique {
Int[] divisibilité publique Tableau (mot d'ordre, int m) {
char[] ch = word.toCharArray();
int[] ans = nouvelle int[ch.longueur];
long rem = 0; // long pour éviter un débordement accidentel
pour (int i = 0; i < ch.longueur; i++) {
digit int = ch[i] - '0'; // plus rapide que Character.getNumericValue()
rem = (rem * 10 + chiffre) % m; // ne conserver que le reste
ans[i] = (rem) 0) ? 1 : 0; // préfixe divisible?
}
le retour des an;
}
}
«» "

---

Python 3

'`python
Solution de classe:
def divisibilité Array(self, mot: str, m: int) -> liste[int]:
ans = []
rem = 0
pour ch en mot:
rem = (rem * 10 + int(ch)) % m
l'annexe (1 si rem == 0 autre 0)
retour et
«» "

---

### C++ (C++17)

'`cpp
solution de classe {
public:
vecteur<int> divisibilité Tableau (mot chaîne, int m) {
vecteur <int> ans;
as.reserve(word.size());
long rem = 0;
pour (char ch : mot) {
chiffre int = ch - '0';
rem = (rem * 10 + chiffre) % m;
as.push_back(rem == 0 ? 1 : 0);
}
le retour des an;
}
};
«» "

---

Résultats

Langue Heure Espace
- C'est quoi ?
*Java* O(n)* O(n)*
Python O(n)
C++= O(n)= O(n)=

La seule opération lourde par itération est une multiplication/addition modulaire, qui est le temps constant.

---

Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Excédent**= Utilise seulement les restes → sûrs== Aucun==
**Complexité**
Il faut comprendre l'arithmétique modulaire.
Autres **Cas d'escroquerie**
**Mémoire Empreinte de l'empreinte de l'empreinte de l'empreinte de l'empreinte de l'empreinte de l'empreinte de l'empreinte de l'empreinte de l'empreinte de l'empreinte de l'information
**Tests**= Préfixes faciles à tester Autres

Pourquoi c'est génial pour les entrevues

1. **Il montre que vous comprenez l'arithmétique modulaire** – un piège d'entrevue commun.
2. ** Démontre l'efficacité O(n)** – répond aux contraintes de LeetCode.
3. **Code simple** – moins de place pour les bugs, plus facile à expliquer.

Pièges potentiels

- L'oubli de mod après chaque multiplication peut causer un débordement.
- Conversion incorrecte des caractères (par exemple, `int digit = ch - 48;` est bien, mais `int digit = Character.getNumericValue(ch);` est plus lent).
- Retour d'un mauvais type (`Liste<Integer>` vs `int[]` en Java).

---

## Conseils pour transformer cette pièce en une pièce de portefeuille gagnante

1. **Ajouter une suite d'essais**
'`python
def test():
sol = Solution()
d'affirmer la sol.divisibilitéArray("998244353", 3) == [1,1,0,0,0,1,0,0]
d'affirmer la sol.divisibilitéArray("1010", 10) == [0,1,0,1]
«» "
2. **Documenter votre code** – ajouter de brefs commentaires expliquant les étapes modulaires.
3. ** Expliquez l'algorithme dans votre mémoire** – Arithmétique modulaire utilisé pour résoudre un grand nombre de disvisibilité en temps O(n). (en milliers de dollars)
4. **Contexte d'entrevue de Mention** – -Adapté cette solution pour LeetCode 2575; prêt à discuter des cas de bord et de l'optimisation. (en milliers de dollars)

---

## SEO-Optimized Blog Titre & Meta Description

**Titre:**
*LeetCode 2575: Divisibility Array – The Good, The Bad, and The Ugly (Java, Python, C++)*

**Meta Description:**
"Master LeetCode 2575 avec des solutions Java, Python et C++ propres. Apprenez l'astuce arithmétique modulaire, l'analyse du temps et de l'espace, et des conseils d'entrevue pour décrocher votre prochain emploi."

---

Les pensées finales

Le motif "Keep the Rebyder" est un agrafe pour les problèmes de chaîne à entier où le nombre peut dépasser les types intégrés.
- **Bien**: O(n) temps, pas de débordement, facile à raisonner.
- **Bad**: Aucun si vous vous souvenez de modéliser chaque étape.
- **Ugly**: Aucune – la solution est élégante.

Montrez ceci dans votre portfolio, et vous aurez un point fort pour les entretiens techniques. Bonne chance ! C'est ce qu'il a dit