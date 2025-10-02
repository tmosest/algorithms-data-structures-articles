---
Titre: LeetCode 3517. Réarrangement palindromique le plus petit Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – **Java, Python et C++**

Voici des implémentations propres et prêtes à la production pour LeetCode 3517 – Le plus petit réarrangement palindromique I.
Tous les trois résolvent le problème en **O(n log n)** temps (en utilisant `Arrays.sort`) et **O(n)** espace.
N'hésitez pas à remplacer l'étape de tri par un tri pour une solution de temps *O(n*) si vous voulez repousser la limite de performance.

---

### Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public String plus petitPalindrome(String s) {
int n = s.longueur();
si (n <= 1) retourner s; // cas triviaux

// première moitié de la chaîne (floor(n/2))
idemLen = n / 2;
d'abord Demi = nouveau char[demiLen];
pour (int i = 0; i < halfLen; ++i) {
d'abord Half[i] = s.charAt(i);
}

// Tri ascendant → lexicographiquement plus petite moitié
Tableau 3.

// construire le palindrome
StringBuilder sb = nouveau StringBuilder();
sb.append(première moitié); // côté gauche

si (n % 2 == 1) { // longueur impair → garder l'omble moyen
sb.append(s.charAt(demiLen));
}

// côté droit est le revers du côté gauche trié
sb.append(new StringBuilder(new String(firstHalf)).reverse());

retour sb.toString();
}
}
«» "

---

Python

'`python
Solution de classe:
def le plus petit Palindrome (self, s: str) -> str:
n = len(s)
si n <= 1:
retour s

moitié = n // 2
premier_demi = trié(s)[:demi]) # liste des caractères triés
gauche = ''.join(première moitié)

milieu = s[moitié] si n % 2 autres ' '
droite = gauche[::-1] # arrière de gauche

retour gauche + milieu + droite
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne la plus petite Palindrome(chaîne s) {
int n = s.size();
si (n <= 1) retourner s;

la moitié int = n / 2;
chaîne gauche = s.substr(0, moitié); // première moitié
tri(left.begin(), left.end()); // lexicographiquement plus petit

chaîne moyenne = (n % 2) ? string(1, s[moitié]) : ";
chaîne droite = gauche;
inverse(right.begin(), right.end());

retour gauche + milieu + droite;
}
};
«» "

---

- Oui. 2. Article du blog – *Le bon, le mauvais et le mauvais* de LeetCode 3517

> **Référence géographique* *
> *LeetCode 3517 – Réarrangement palindromique le plus petit I.Java, Python, C++ Solutions – Obtenez le travail*

> **Description détaillée**
> Maître LeetCode 3517 en secondes. Apprenez l'algorithme gourmand, comprenez les cas de bord et voyez le code Java, Python & C++. Imprimez les gestionnaires d'embauche avec un code propre et efficace.

---

2.1 Introduction

Lorsque les recruteurs demandent : Pouvez-vous construire le palindrome lexicographiquement le plus petit à partir d'une corde palindromique ?

1. **Comprendre les palindromes et la symétrie**
2. ** Pensée grêle – choisir le plus petit côté gauche possible* *
3. **Clean, code prêt à la production dans une langue qu'ils utilisent**

LeetCode 3517, *Réarrangement palindromique le plus petit I*, est le problème d'entrevue parfait pour présenter les trois. Laissons tomber : le bon*, le mauvais* et le mauvais*.

---

2.2 Récapitulation du problème

> **Don** une chaîne de palindrome `s` de longueur `n` (`1 ≤ n ≤ 105`),
> **Retour** le palindrome lexicographiquement le plus petit qui peut être formé en réorganisant les caractères de `s`.

Exemples
Entrée Sortie Explication
C'est pas vrai.
Un seul caractère – déjà minime. Autres
""bab" ""abbba" ""abbba" "" Triant la première moitié donne `ab`, inverse est `ba`. Autres
""daccad" ""acddca" """"" Trié moitié `acd` → inverser `dca`. Autres

**Insight clé:**
Un palindrome est complètement défini par sa première moitié (et le caractère moyen, si `n` est étrange). Si nous faisons la première moitié aussi petite que possible lexicographiquement, tout le palindrome devient le plus petit possible.

---

### 2.3 La bonne – Gâterie simple + Tri

**Pourquoi ça marche* *

* `s` est déjà un palindrome → le multiset des premiers caractères `=n/2=" est égal à celui des derniers caractères `=n/2=".
* En triant la première moitié ascendante, nous organisons les plus petits personnages à l'avant.
* Le miroir de cette moitié triée nous donne automatiquement un palindrome valide.
* Le personnage du milieu (si la longueur est étrange) est forcé – nous ne pouvons pas le changer.

**Étapes d'algorithme**

1. `moitié = n / 2`
2. Première moitié = s[0 ... moitié-1] "
3. Tri en premier A moitié ascendant.
4. Si `n` est impair, `mid = s[moitié]` sinon `mid = "".
5. `rightHalf = inverse(premierHalf)`
6. Résultat = "première Moyenne + droite moitié "

Complexités
* **Heure:** `O(n log n)` – en raison du tri.
* **Espace:** `O(n)` – pour la chaîne de sortie et le tableau trié.

**Pourquoi c'est bon* *

* **Readable** – une boucle, une sorte, une inversion.
* ** Prédictible** – le tri garantit le minimum du côté gauche.
* **Évoluable** – fonctionne pour la longueur maximale `105`.

---

2.4 Les mauvaises – approches naïves qui échouent

Problème
C'est pas vrai.
**Permutations de la force brute** temps – impossible pour `n > 10`. Autres
**Greedy sans trier**) Prendre le personnage le plus petit à gauche cupide peut conduire à une moitié droite impossible. Autres
**Réarranger entièrement Chaîne aléatoirement** Autres
**Sort Full String, puis build**.Le tri de la chaîne entière donne une chaîne triée, mais il se peut que ce ne soit pas un palindrome. Autres

Ces méthodes violent les délais ou produisent des résultats erronés. Ils sont un classique de toutes les possibilités.

---

#### 2.5 L'horrible – Cas et pièges

Qu'est-ce qui se passe ?
Il n'y a pas de lien entre les deux.
"n = 1" "moitié = 0"; tri des chaînes vides. Retournez tôt (si n <= 1 retour s). Autres
"n = 2"" Même longueur – le milieu n'existe pas. Traiter comme une longueur égale (demi = 1). Autres
**Tous les caractères Même**= `s = "aaa"` → sortie inchangée. Toujours fonctionne – le tri ne fait rien. Autres
**Large `n` (105)** Toutes les opérations sont linéaires ou « O(n log n) »; bien dans les limites. Autres
Le problème garantit les lettres minuscules. Pas besoin de manipulation supplémentaire. Autres

Souvenez-vous toujours de gérer le caractère intermédiaire de longueur bizarre séparément. En l'oubliant, il produira une chaîne qui s'éteint par un seul personnage.

---

2.6 Faits saillants de la mise en œuvre

Voici les implémentations en 3 langues que nous avons fournies précédemment. Ils suivent tous le même algorithme :

Texte
1. Extraire la moitié gauche
2. Tri ascendant
3. (facultatif) Ajouter le caractère intermédiaire si impair
4. Ajouter le revers de la moitié gauche triée
«» "

**Pourquoi ils sont prêts à la production* *

* **Aucune dépendance externe** – seule bibliothèque standard.
* **Noms de variables clairs** – `demiLen`, `mid`, `left`, `right`.
* **Responsabilité unique** – la méthode fait exactement une chose.
* **Test prêt** – test facile avec les exemples ci-dessus.

---

2.7 Résumé de la complexité

Heure de mise en œuvre
- Oui.
"O(n log n)" Autres
Python "O(n log n)" Autres
"O(n log n)" Autres

Si vous avez besoin de la vitesse ultime, remplacez `Arrays.sort` / `sorted()` par un tri de comptage basé sur la fréquence** (26 lettres). Cela transforme l'algorithme en 'O(n)' l'espace "O(n)".

---

2.8 Cas d'essai (liste de contrôle rapide)

Texte
s = "z" → "z"
s = "aa" → "aa"
s = "bab" → "abba"
s = "daccad" → "acddca"
s = "cbaabc" → "aabccb"
s = "abccba" → "abccba"
s = "aaaaabaaaa" → "aaaaabaaaa"
«» "

Exécutez chacun dans les trois langues pour confirmer les sorties identiques.

---

2.9 Réflexions finales – Comment cela vous aide à trouver un emploi

* **Afficher la clarté algorithmique** – vous avez réduit le problème à une simple opération gourmande.
* ** Démontre l'artisanat du code** – propre, concis et commenté.
* **Illustre les compromis temps/espace** – vous pouvez discuter de la raison pour laquelle vous avez choisi trier vs trier.
* **Fait ressortir la compréhension des problèmes** – vous savez pourquoi le tri de la première moitié est suffisant pour un palindrome.

Lorsque les intervieweurs voient cela, ils reconnaissent instantanément que vous pouvez transformer un problème de permutation apparemment complexe en une solution linéaire. C'est exactement le genre de compétence qu'ils recherchent.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

**Mots clés:** Petite réarrangement palindromique, LeetCode 3517, Lexicographiquement plus petit palindrome, solution Java, solution Python, solution C++, problème de codage d'entretien, interview d'algorithme, codage d'entretien d'emploi, algorithme avide, réarrangement palindromique.