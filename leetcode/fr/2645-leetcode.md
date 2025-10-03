---
titre: LeetCode 2645. Ajouts minimums pour faire une chaîne valide -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2645 – Ajouts minimums pour rendre la chaîne valide
**Java.Python.C++** – Des solutions de travail complètes + un court billet de blog qui vous aidera à décrocher votre prochain entretien technique.

---

Récapitulation des problèmes
* **Objectif:** Insérez les lettres les plus rares (`a`, `b`, ou `c`) dans une chaîne `word` afin que la chaîne résultante puisse être divisée en un ou plusieurs blocs consécutifs `"abc"`.
* **Input:** `1 ≤ word.longueur ≤ 50`, `word` ne contient que `a`, `b`, `c`.
* ** Sortie:** Nombre minimum d'insertions requises.

---

3 Solutions linguistiques spécifiques

> Toutes les solutions fonctionnent dans **O(n)** temps, **O(1)** espace supplémentaire.

---

#### Java 17

"Java
solution de classe {
int public addMinimum (mot de la chaîne) {
int k = 0; // nombre de blocs nécessaires
char prev = 'z'; // sentinelle plus grande que n'importe lequel des a,b,c

pour (int i = 0; i < word.longueur(); i++) {
char cur = mot.charAt(i);
si (cur <= prev) { // démarrer un nouveau bloc
k++;
}
prev = cur; // garder le dernier caractère vu
}
retour k * 3 - word.length(); // total des caractères en blocs moins ceux existants
}
}
«» "

**Pourquoi ça marche* *
La chaîne `"abc"` augmente strictement (`a < b < c`).
Chaque fois que le caractère actuel est **pas** plus grand que le précédent, nous devons démarrer un nouveau bloc `"abc"`.
`k` est le nombre total de blocs; chaque bloc contribue à 3 caractères, donc `k*3` est la longueur de la chaîne valide finale.
Soustrayez la longueur d'origine pour obtenir les insertions nécessaires.

---

### Python 3.10+

'`python
Solution de classe:
def addMinimum(self, mot: str) -> Int:
k, prev = 0, 'z'
pour ch en mot:
si ch <= prev: # nouveau bloc requis
k += 1
prev = ch
retour k * 3 - len(mot)
«» "

La version Python est un 1-liner à l'intérieur de la boucle – logique identique à Java.

---

C++17

'`cpp
solution de classe {
public:
int addMinimum(string word) {
int k = 0; // blocs
char prev = 'z'; // sentinelle

pour (char ch : mot) {
si (ch <= prev) { // commencer un nouveau bloc
++k;
}
prev = ch;
}
retourner k * 3 - static_cast<int>(word.size());
}
};
«» "

---

Article du blog : *Les bons, les mauvais, et les affreux de LeetCode 2645*

> **Mots clés:** LeetCode 2645, Minimum d'ajouts pour faire une chaîne valide, solution Java, solution Python, solution C++, algorithme gourmand, préparation d'entrevue, entretien d'emploi, conception d'algorithme.

---

Description de la méta
Master LeetCode 2645 – Ajouts minimums pour faire une chaîne valide – apprenez l'astuce gourmande, voyez les solutions Java/Python/C++, et comprenez les nuances de « good‐bad‐ugly» pour recevoir votre prochaine interview de codage.

---

C'est pas vrai. Le bien: pourquoi ce problème est une question d'entrevue dorée
- **Simplicité + profondeur** – À première vue, il ressemble à un problème de jouet, mais la logique cupide sous-jacente est un microcosme de problèmes de subséquence classiques.
- **Échelle** – La solution fonctionne en temps linéaire, ce qui est un must pour les personnes interrogées.
- **Language-agnostique** – Vous pouvez le résoudre dans n'importe quelle langue (Java, Python, C++), ce qui le rend parfait pour montrer des forces spécifiques à la langue.

C'est vrai. Les mauvaises : des pièges communs qui coûtent aux intervieweurs
Pourquoi ça arrive ?
- Oui.
**Misinterpréter "croissant"**" Penser `b <= a` signifie "nouveau bloc" au lieu de `b > a`. Autres
Autres **L'utilisation d'une pile ou d'une file d'attente. Garder seulement un caractère `prev` et un compteur `k`. Autres
**Oublier la sentinelle**. Initialiser `prev` à un caractère plus grand que `c` (`'z`` œuvres). Autres

C'est vrai. L'Ugly : des approches alternatives Les choses Messy
- **Two-Pointer simulation**: Itération sur un cycle virtuel `"abc"` et incrémentation d'un compteur d'insertion chaque fois que le caractère actuel se confond. Il fonctionne mais introduit une logique supplémentaire (`(j + 1) % 3`) qui est facile de se tromper.
- ** Programmation dynamique** : La construction d'une table DP pour tous les préfixes est surqualifiée pour `n ≤ 50`. C'est un exemple de manuel de bloat algorithmique.
- **Regex + Remplacement**: Certaines solutions en ligne utilisent regex pour supprimer des modèles comme `abc`. Alors que rapide dans la pratique, il est fragile et pas auto-explication.

C'est pas vrai. Comment utiliser ce problème dans votre recherche d'emploi
1. **Afficher la perspicacité gourmande** – les intervieweurs aiment vous voir reconnaître les modèles.
2. **Afficher le temps O(n) et l'espace O(1)** – ces paramètres sont fréquemment demandés.
3. ** Démontrer la polyvalence du langage** – présenter la solution en Java, Python et C++ (comme nous l'avons fait plus haut).
4. ** Expliquez les pièges** – être capable de souligner ce que *pas* faire indique une compréhension profonde.

---

À emporter

- **Greedy Insight:** Démarrer un nouveau bloc ""abc"` chaque fois que le caractère actuel n'est pas plus grand que le précédent.
- **Formule finale:** "insertions = blocs * 3 - mot.longueur()".
- ** Mise en œuvre :** Une boucle simple avec deux variables – « k » (blocks) et « prev » (dernier caractère vu).

Avec cette solution propre et 5 lignes dans n'importe quelle langue supérieure, vous allez non seulement passer LeetCode 2645 mais aussi impressionner les intervieweurs en transformant un problème apparemment trivial en une vitrine de maturité algorithmique. Bon codage – et bonne chance pour ce prochain travail!