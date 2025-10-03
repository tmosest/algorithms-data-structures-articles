---
titre: LeetCode 1952. Trois diviseurs - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Trois diviseurs – 1952 (Code Leet)
**Objectif**: Retour `true` si un entier `n` a exactement trois diviseurs positifs, sinon `faux`.
**Contraintes**: "1 ≤ n ≤ 104"

---

Trois façons de le résoudre
Ci-dessous vous trouverez des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.
La mise en œuvre utilise le fait mathématique:

> Un nombre a exactement trois diviseurs **iff** c'est un carré parfait d'un nombre premier.

---

### # Java (Efficace et lisible)

"Java
solution de classe publique {
// O( √n) temps, espace O(1)
booléen public estTrois(int n) {
si (n < 4) retourner faux; // 1,2,3 ne peut pas avoir 3 diviseurs

racine int = (int) Math.sqrt(n);
si (root * root != n) retourner false; // pas un carré parfait

retour isPrime(root); // vérifier si sqrt(n) est prime
}

booléen privé estPrime(int x) {
si (x < 2) retourner faux;
si (x % 2] 0) retour x == 2;
pour (int i = 3; i * i <= x; i += 2) {
si (x % i) 0) retourner faux;
}
retour vrai;
}
}
«» "

> **Pourquoi ça marche* *
> * Les carrés parfaits sont les seuls candidats qui peuvent avoir un nombre impair de diviseurs.
> * Si la racine carrée est une prime, ses diviseurs sont `1`, `p`, `p2` → exactement trois.

---

Python (Elégant monoligneur)

'`python
Solution de classe:
def isThree(self, n: int) -> C'est vrai.
# Chèque carré parfait
racine = int(n ** 0,5)
si racine * racine != n:
Retour Faux

# Premier contrôle pour la racine
si racine < 2:
Retour Faux
si racine % 2 == 0:
retour de racine == 2
pour i dans la plage(3, int(root ** 0,5) + 1, 2):
si racine % i] 0:
Retour Faux
retour Vrai
«» "

> ** Touches pyroniques* *
> * `int(n ** 0.5)` donne le sol de la racine carrée.
> * La boucle n'intervient que sur des nombres impairs pour la vitesse.

---

C++ (Sans Fast & STL)

'`cpp
solution de classe {
public:
Bool isThree(int n) {
si (n < 4) retourner faux;

Int root = static_cast<int>(sqrt(n));
si (root * root != n) retourner faux;

retour estPrime(root);
}

particulier:
L'eau de roche est Prime(int x) {
si (x < 2) retourner faux;
si (x % 2] 0) retour x == 2;
pour (int i = 3; i * i <= x; i += 2)
si (x % i) 0) retourner faux;
retour vrai;
}
};
«» "

> **Pourquoi c'est optimal**
> * `sqrt()` de `<cmath>` est O(1).
> * Boucles d'essai primaires jusqu'à ` √root`, qui est ≤ 100 pour les contraintes données.

---

Article du blog – Le bon, le mauvais, et l'acharnement de résoudre trois divisions

Titre
La maîtrise du LeetCode 1952 – Trois diviseurs : un guide de préparation à l'emploi (Java, Python, C++)* *

Description de la méta
Débloquez votre prochain entretien avec notre parcours approfondi de LeetCode 1952 (Trois Diviseurs). Apprenez les maths, codez en Java/Python/C++ et comprenez les pièges bons, mauvais et laids. Idéal pour les ingénieurs logiciels ciblant les emplois de haute technologie.

---

Introduction
Lorsque vous frappez **LeetCode 1952 – Trois Diviseurs**, vous êtes en train de regarder un problème facile qui peut être une opportunité *golden* dans une interview technique. Il teste votre capacité à:

1. Spot raccourcis mathématiques.
2. Écrire un code propre et efficace.
3. Traduire un algorithme simple en plusieurs langues.

Ci-dessous, nous disséquons le problème, nous vous montrons la solution *bonne* efficace, nous découvrons les pièges *mauvais* naïfs, et nous vous avertissons au sujet des anti-patterns *puces*. Tout en gardant les extraits de code prêts pour Java, Python et C++.

---

Récapitulation des problèmes
> **Don** un entier `n` (1 ≤ n ≤ 104).
> **Retour** `true` si `n` a exactement trois diviseurs positifs, sinon `faux`.

---

Les mathématiques derrière la solution

1. **Diviseurs en paires** – Pour un nombre `n`, chaque diviseur `d` a un partenaire `n/d`.
2. **Parfaits carrés** – Seuls des carrés parfaits brisent cette paire, laissant un diviseur non pairé (' √n').
3. ** Trois diviseurs** – Pour un carré parfait `p2`, ses diviseurs sont `1`, `p`, `p2`.
*Par conséquent, `p` doit être le premier pour garder le compte à trois. *

**Key Insight**: *Vérifiez si `n` est un carré parfait; si oui, testez si sa racine carrée est une prime. *

---

Le bon – Code efficace et élégant

*Pourquoi c'est génial*:
- **Complexité temporelle**: O( √n) – bien en dessous de la limite de contrainte.
- **Complexité spatiale**: O(1).
- **Readability**: Petite fonction d'aide (isPrime).
- **Langue Agnostique**: Fonctionne en Java, Python, C++ avec des modifications de syntaxe mineures.

Voir les extraits de code ci-dessus.

---

La mauvaise – Naïve Brute Force

"Java
nombre int = 0;
pour (int i = 1; i <= n; i++) {
Si (n % i] 0) nombre++;
}
3;
«» "

* Problèmes*
- **O(n) Time** – Même avec n = 104, c'est gaspillé dans un contexte d'entrevue.
- **Inefficient pour les limites plus grandes** – Si les contraintes étaient assouplies, cela serait temps.
- **Poor Utilisation des mathématiques** – Ignore la propriété d'appariement de diviseur.

**Quand elle est acceptable**: Pour les problèmes de jouets ou très petites plages d'entrée. Mais pour de vrais entretiens, c'est un drapeau rouge.

---

### -------------

Motif: Pourquoi c'est ugly: Correction
C'est pas vrai.
**Limites codées à l'aide d'un code à l'arrêt** Autres
**Repeated sqrt**= Appeler `sqrt(n)` dans une boucle= Calculer une fois et réutiliser. Autres
** Division d'essai complète**= Vérification de tous les nombres jusqu'à `n`= Vérifier seulement jusqu'à `=root`. Autres
**Ne pas manipuler les cas de bord** Autres
**Les noms de variables Verbose**= `isTree` vs `hasTreeDivisors`=Utilisez des noms descriptifs clairs. Autres

---

À emporter pour les entrevues de travail

1. **Parlez des maths** avant de coder.
2. **Mention la stratégie O( √n)** – les intervieweurs aiment voir la conscience algorithmique.
3. **Show clean code** – petites fonctions d'aide, noms clairs et commentaires.
4. **Soyez prêts à traduire** dans n'importe quelle langue – on vous demandera probablement de réécrire dans une autre langue.

---

Mots clés et référencement

- Trois Diviseurs problème
- Solution LeetCode 1952
- Code de trois diviseurs Java
- Python premier contrôle
- Algorithme carré parfait C++
- Pratique de l'algorithme d'entrevue
- Questions sur l'algorithme d'entretien d'emploi
- Entretien avec l'ingénieur logiciel
- Défi de codage basé sur les mathématiques

---

Réflexions finales

- **Bien**: Élégante logique du premier carré, temps O( √n).
- **Bad**: Compte du diviseur de la force brute.
- **Ugly**: boucles inefficaces, cas de bord non manipulés, mauvais nom.

En maîtrisant ce problème, vous démontrerez votre capacité à combiner la perspicacité mathématique et le code propre – une compétence clé que les employeurs recherchent. Bon codage, et bonne chance pour votre prochaine interview!