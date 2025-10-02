---
titre: LeetCode 1859. Tri de la peine -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1859 – Détachement de la peine
Temps O(n), espace O(n)

> **Problème**
> Une phrase reformulée est formée en ajoutant la position du mot 1 indexé à chaque mot, puis en permutant les mots.
> Étant donné qu'une phrase « s » est reformulée (pas d'espaces de guidage ou de traçage, de mots séparés par un seul espace), reconstruire la phrase originale.

> **Exemple**
> `` "
> Entrée : "is2 phrase4 Ce 1 a3"
> Sortie : "C'est une phrase"
> `` "

> **Pourquoi est-ce une bonne question d'entrevue? **
> * Logique simple d'analyse
> * Démontre la manipulation et l'indexation des chaînes
> * Pas besoin de structures de données avancées

---

Aperçu de la solution

1. **Split** la chaîne en caractères (O(n)).
2. Pour chaque mot, **extraire** le dernier caractère → la position (1-basée).
3. **Place** le mot (sans le chiffre) dans un tableau à `index‐1`.
4. **Rejoindre** le tableau dans une phrase.

> La contrainte `1 ≤ wordCount ≤ 9` garantit que le dernier caractère est toujours un seul chiffre.
> Si le problème permettait plus de mots, nous aurions besoin d'analyser tous les chiffres qui suivent.

---

Mise en œuvre du code

> Toutes les implémentations ont une logique identique ; seule la syntaxe diffère.

- Oui. 1. Java

"Java
// Java 17
Importation de java.util.*;

solution de classe publique {
public String triSentence(String s) {
Chaîne[] mots = s.split(");
Chaîne[] res = nouvelle chaîne[mots.longueur];

pour (Pièce w : mots) {
int pos = w.charAt(w.longueur() - 1) - "1"; // 0
res[pos] = w.substring(0, w.length() - 1);
}

retour String.join("", res);
}
}
«» "

> **Complexité**
> *Heure* – O(n) (chaque mot visité une fois)
> *Espace* – O(n) (tableau de résultats)

---

- Oui. 2. Python

'`python
# Python 3
Solution de classe:
def triSentence(self, s: str) -> str:
mots = s.split()
res = [Aucun] * len(mots)

pour w en mots:
pos = int(w[-1]) - 1 # 0-based index
res[pos] = w[:-1] # enlevez le chiffre

retour ''.join(res)
«» "

> **Complexité** – identique à Java

---

- Oui. 3. C++

'`cpp
// C++17
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
sort de chaîneSentence(chaîne s) {
vecteur <string> les mots;
sss de chaîne de caractères;
chaîne w;
pendant (ss >> w) words.push_back(w);

vector<string> res(words.size());
pour (const string &w : mots) {
int pos = w.back() - '1'; // 0-basé
res[pos] = w.substr(0, w.size() - 1);
}
ficelles et cordes;
pour (size_t i = 0; i < res.size(); ++i) {
i) ans += ';
et += res[i];
}
le retour des an;
}
};
«» "

> **Complexité** – temps O(n), espace O(n)

---

Comment utiliser ces solutions dans votre entrevue

1. ** Expliquez l'algorithme** avant de plonger dans le code.
2. Mentionnez la complexité **temps/espace** et pourquoi ils sont optimaux.
3. Soulignez que l'astuce est de traiter le dernier chiffre comme un index.
4. Soyez prêt à discuter de cas de bord (p. ex. phrases à mots simples, cas mixte, etc.).

---

Les bons, les mauvais et les méchants

Catégorie de la catégorie de la catégorie de la catégorie de la catégorie de la catégorie de la catégorie de la catégorie de la catégorie de la catégorie
- C'est la première fois.
**Bon**• O(n) temps et espace, aucune structure de données lourde.<br>• Fonctionne pour tout alphabet (en bas/en haut).
**Bad** Le problème est délibérément facile à mettre en évidence les compétences de base en cordes.
Si le problème était étendu à **10+ mots** (positions à plusieurs chiffres), la logique actuelle échouerait. <br>• Besoin d'une routine d'analyse plus robuste qui extrait tous les chiffres traînants, pas seulement le dernier char. Dans le monde réel, les phrases peuvent contenir des ponctuations ou des nombres en mots, nécessitant une solution régex plus propre. Autres

---

Bonus : Extension aux indices de longueur variable

Si la phrase peut avoir **10+ mots**, l'index peut se composer de plusieurs chiffres. Voici une adaptation rapide pour Python:

'`python
importations

def tri_sentence_variable(s) :
mots = s.split()
res = [Aucun] * len(mots)
pour w en mots:
m = re.search(r'(\d+)$', w)
pos = int(m.group(1)) - 1
res[pos] = w[:m.start()]
retour ''.join(res)
«» "

Ceci utilise un régex pour capturer tous les chiffres de la piste.

---

## Description du blog optimisé SEO & Meta

**Titre:**
> *Sortir la peine (LeetCode 1859) – Java, Python, & C++ Solutions + Conseils d'entrevue*

**Meta Description:**
> Master LeetCodeSupprimer le problème de la peine avec le code Java, Python et C++. Apprenez l'algorithme optimal, l'analyse de complexité et l'explication prête à l'entrevue. Parfait pour coder la préparation d'entrevue.

---

Enveloppe

Tri de la Sentence est une manipulation classique de chaîne + indexing. La solution optimale est triviale une fois que vous réalisez que le dernier chiffre est une position explicite basée sur 1.
Les implémentations en Java, Python et C++ sont concises, efficaces et prêtes à passer dans votre session LeetCode ou votre entretien de codage.

Bon codage – et que vos phrases soient toujours en ordre! C'est ce qu'il a dit