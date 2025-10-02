---
titre: LeetCode 3461. Vérifier si les chiffres sont égaux dans la chaîne après les opérations I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3461 – Vérifiez si les chiffres sont égaux dans la chaîne après les opérations I
**Solvez-le en Java, Python et C++**
> Un parcours détaillé, un billet de blog SEO qui explique le **bon**, le **mauvais** et le **ugly** de ce problème – parfait pour votre prochain entretien de codage ou CV.

---

- Oui. 1. Récapitulation des problèmes

Vous recevez une chaîne numérique `s` (`3 ≤ s.longueur ≤ 100`).
Répétez ce qui suit jusqu'à ce que `s` ait exactement deux chiffres:

«» "
pour chaque paire adjacente (s[i], s[i+1])
nouveauDigit = (int(s[i]) + int(s[i+1]) % 10
annexe nouvelle Chiffre à la chaîne suivante
«» "

Retour **true** si les deux derniers chiffres sont identiques, sinon **faux**.

> Exemple
> `s = "3902"`
> `3902 → 292 → 11` → **true**

---

- Oui. 2. Stratégie de la force brute (simulation)

La façon la plus naturelle est de simuler littéralement le processus.

Texte
pendant que len(s) > 2 :
nouvelle_s = ""
pour i dans la plage(len(s)-1):
nouvelles_s += str(int(s[i]) + int(s[i+1]) % 10)
s = nouvelles_s
retour s[0] == s[1]
«» "

*Time*: `O(n2)` – parce que chaque itération rétrécit la chaîne par 1, de sorte que nous faisons ~n/2 + n/3 + ...
*Espace*: `O(n)` – nous construisons une nouvelle chaîne à chaque fois.

C'est assez rapide pour les contraintes données, mais laissez-les creuser dans les **bon**, **bad**, et **ugly** aspects.

---

- Oui. 3. Les bonnes

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Simplicité**La simulation modélise directement l'énoncé du problème. Pas de tours ou de maths cachés. Autres
**Readability** Autres
**Maintenabilité**= Si l'opération change (par exemple, `% 9` au lieu de `% 10`), vous n'ajustez qu'une ligne. Autres
**Language-agnostic**Le même algorithme fonctionne en Java, Python, C++, JavaScript, etc. Autres

---

- Oui. 4. Les mauvais

Question Conséquences Correction
- Oui.
**Création des résultats** ('char -> int') )?Création de performances mineures. Autres
**Concaténation de chaînes inutiles**=Crée de nombreux objets intermédiaires `StringBuilder`/`String`.=Utiliser un `StringBuilder` (Java), la compréhension de la liste (Python), ou `std::string` avec `Reserve` (C++). Autres
Pour le pire des cas (100 chiffres), il est encore bon, mais pas optimal. Explorer la réduction mathématique (voir ci-dessous). Autres

---

- Oui. 5. L'Ugly

* **Les solutions récursives** qui construisent de nouvelles chaînes pour chaque appel peuvent frapper les limites de profondeur de récursion en Python (`RuntimeError: maximum de récursion profondeur dépassée`) et les débordements de pile en C++.
* **M mutations en place** de la chaîne alors que l'itération peut produire des bogues logiques si les indices changent.
* **HashSet approach** (vérifier d'abord les chiffres uniques) peut donner une mauvaise réponse pour les chaînes comme `"1110"` (les chiffres uniques sont 1 et 0, mais après réduction ils deviennent égaux).

---

- Oui. 6. Optimisation possible (pas nécessaire mais frais)

Si vous remarquez que l'opération est linéaire et que chaque étape ne dépend que de chiffres adjacents, vous pouvez précalculer le coefficient pour chaque chiffre original en utilisant une programmation dynamique.
Cependant, la simulation naïve est déjà **< 0.1 ms** sur le matériel moderne pour 100 chiffres, donc nous allons y rester.

---

- Oui. 7. Mise en œuvre complète du code

Voici des versions propres et conviviales pour **Java**, **Python** et **C++**.
Les trois utilisent un `StringBuilder` / list / `std::string` pour éviter le coût quadratique de la concaténation répétée.

---

#### 7.1 Java (Java 17)

"Java
// Fichier: Solution.java
solution de classe publique {
public booléen aSameDigits(String s) {
// Alors que plus de deux chiffres restent
pendant que (longueur() > 2) {
// Construire la chaîne suivante en un seul passage
StringBuilder suivant = nouveau StringBuilder(s.longueur() - 1);
pour (int i = 0; i < s.longueur() - 1; i++) {
int a = s.charAt(i) - '0';
b = s.charAt(i + 1) - '0';
Annexe suivante(a + b) % 10);
}
s = suivant.àString(); // Préparez-vous pour la prochaine itération
}
// Deux derniers chiffres
retour s.charAt(0) == s.charAt(1);
}

// harnais d'essai simple
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.hasSameDigits("3902")); // true
Système.out.println(sol.hasSameDigits("34789")); // faux
}
}
«» "

---

#### 7.2 Python (Python 3,11)

'`python
# Fichier : solution. py
def has_same_digets(s): str -> C'est vrai.
# Réduire jusqu'à ce que la longueur soit 2
pendant que len(s) > 2 :
# Construire la chaîne suivante avec la compréhension de la liste (rapide)
s = ''.join(str(int(s[i]) + int(s[i+1])) % 10) pour i dans la plage(len(s)-1)
retour s[0] == s[1]


♪ Démo
si __nom__ == "__main__" :
print(has_meme_digits("3902")) # True
print(has_me_digits("34789")) # Faux
«» "

---

### 7.3 C++ (C++17)

'`cpp
// Fichier: solution.cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool haveSameDigits(string s) {
pendant que (s.size() > 2) {
chaîne suivante;
suivant.reserve(s.size() - 1);
pour (size_t i = 0; i + 1 < s.size(); ++i) {
int a = s[i] - '0';
int b = s[i+1] - '0';
next.push_back('0' + (a + b) % 10);
}
s.swap(suivant); // Réutiliser la mémoire, aucune attribution
}
retour s[0] == s[1];
}
};

Int main() {
Solution sol;
cout << boolalpha; // imprimer true/false au lieu de 1/0
<< sol.hasSameDigits("3902") << '\n'; // true
<< sol.hasSameDigits("34789") << '\n'; // false
}
«» "

---

- Oui. 8. Analyse de la complexité

Langue Heure Espace
- C'est quoi ?
*Java** * O(n2) * 5 000 opérations pour < < n = 100 > > * O(n) * Autres
**Python** Autres
* C++** , O(n2) , O(n) Autres

> **Pourquoi il passe encore:**
> La longueur de la boucle se rétrécit de 1 par passe, de sorte que le nombre total d'opérations est d'environ `n(n‐1)/2`.
> Avec `n ≤ 100`, cela est bien en dessous du budget temps de la suite de test LeetCode.

---

- Oui. 9. SEO-Friendly Blog Post

> **Titre**: *LeetCode 3461 – Algorithme de réduction des cordes (Java, Python, C++) – Explication de préparation à l'entrevue*
> **Description détaillée**: *Découvrez comment résoudre le LeetCode 3461 avec le code Java, Python et C++. Comprendre l'algorithme, la complexité et les conseils d'entrevue. Préparez-vous à votre prochaine entrevue de codage.

### 9.1 Introduction

```markdown
- Oui. Qu'y a-t-il dans ce billet ?
- Répartition des problèmes
- L'approche de simulation & pourquoi elle est une grande base d'entrevue
- La critique du bien/du mal/du mal – pièges du monde réel
- Trois extraits de code prêts à la production (Java, Python, C++)
- Explication de style d'entrevue vous pouvez déposer dans votre CV
- Mots clés SEO-heavy pour stimuler votre marque personnelle
«» "

### 9.2 Résumé du problème

> **Vérifier si les chiffres sont égaux dans les chaînes après les opérations I** – LeetCode #3461
> Réduire une chaîne numérique par paire avec le modulo 10 et comparer les deux derniers chiffres.

Pourquoi ça compte ?

- **La manipulation de la chaîne** est un élément essentiel dans le codage des entrevues.
- **Modulo arithmétique** présente votre état d'esprit mathématique.
- Oui. Le problème teste **simulation** compétences, qui sont fréquentes dans la chasse aux insectes du monde réel.

9.4 La solution Brute-Force (simulation)

> L'idée centrale : construire la chaîne suivante en un seul scan linéaire, répéter jusqu'à ce que deux chiffres restent, puis comparer.

'`python
pendant que len(s) > 2 :
s = ''.join(str(int(s[i]) + int(s[i+1])) % 10) pour i dans la plage(len(s)-1)
retour s[0] == s[1]
«» "

- **Heure**: `O(n2)` – acceptable pour `n ≤ 100`.
- **Espace**: `O(n)` – une chaîne auxiliaire par itération.

Code pour toutes les langues

(Insérer Java, Python, extraits C++ de la section 7)

### 9.6 Bonne / mauvaise / Récapitulatif

(Insérer le tableau de la section 3–5)

### 9.7 Conseils d'entrevue

Comment la solution montre Quoi mettre en avant
-- -- -- -- -- -- -- -- -- -- -- -- -- --
**La pensée algorithmique**=Modèler le processus exactement comme décrit===J'ai d'abord construit une simulation pour refléter l'énoncé; il a rendu l'analyse de cas de bord trivial.== Autres
**Travaux entre l'espace et l'heure**= Connaissance des solutions `O(n2)` et `O(n)`== J'ai utilisé `StringBuilder` pour maintenir les allocations linéaires.= Autres
**Readability**= Code propre dans toutes les langues==J'ai choisi l'approche la plus simple pour que les évaluateurs puissent se concentrer sur la logique. Autres
**Adaptabilité**=Le même algorithme fonctionne dans n'importe quelle langue==Je peux le porter à Go, Rust ou JavaScript si nécessaire. Autres

> *Tip*: Lors d'une entrevue, narrez les *bons* et *mauvais* pendant que vous codez. Les intervieweurs adorent vous voir raisonner à propos des compromis.

9.8 Pensées de clôture

- **LeetCode 3461** est un grand problème de vitrine : il vous oblige à penser à **simulation**, ** manipulation de chaînes** et **arithmétique modulaire**.
- Oui. La solution **simulation** est rapide, claire et linguistique-agnostique.
- Rappelez-vous : **code propre > code intelligent** dans la plupart des scénarios d'entrevue.

---

10 ans. Appel à l'action

- **Ajoutez ce problème à votre portfolio** – il montre votre capacité à traduire un énoncé de problème en code de travail.
- **Partagez la solution sur GitHub** – attachez un `README.md` qui passe par l'algorithme (comme nous l'avons fait ici).
- **Pratiquez l'analyse de "bien/mauvais/puce** – les intervieweurs adorent vous voir critiquer vos propres solutions.

---

Mots clés pour référencement

«» "
LeetCode 3461, Vérifiez si les chiffres sont égaux, interview de codage, solution Java, solution Python, solution C++,
manipulation de chaîne, opération modulo, préparation d'entretien, problème algorithmique,
entretien d'emploi, entretien technique, structures de données, algorithme, entretien de programmation, conseils d'entrevue
«» "

---

Bon codage, et que cette solution vous débarque que prochaine offre d'emploi! *