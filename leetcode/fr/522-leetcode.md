---
titre: LeetCode 522. Subséquence la plus longue peu fréquente II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le code 522 – ** Subséquence la plus longue peu fréquente II**
Les bons, les mauvais et les affreux
> *Une plongée profonde dans trois solutions éprouvées (Java, Python, C++) qui vous aideront à aser l'interview, ainsi qu'un billet de blog SEO-friendly que les recruteurs aimeront. *

---

Récapitulation des problèmes

> **Input**: "String[] strs" (2 ≤ ≤ ≤ ≤ 50, 1 ≤ ≤ ≤ 10)
> **Output**: longueur de la plus longue chaîne qui est une sous-séquence de **exactement un** élément de tableau, ou **-1** si aucune telle chaîne n'existe.

> On peut obtenir un *séquence ultérieure* d'une chaîne `s` en supprimant zéro ou plus de caractères sans modifier l'ordre des caractères restants.

---

Pourquoi ce problème se trouve-t-il

- **Interview Goldmine**: La plupart des entreprises le demandent pendant la conception du système ou les tours d'algorithme.
- **Breadth conceptuel**: Touche sur la manipulation des chaînes, la logique de subséquence et la théorie des ensembles.
- **Optimisation** : Facile à passer d'O(n2) à O(n) avec une simple observation – idéal pour démontrer l'efficacité du codage.

---

Trois solutions gagnantes

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**. Chacun suit la même stratégie optimale:

1. **Comparer la fréquence de chaque chaîne**.
2. Si une chaîne est unique (fréquence = 1), sa longueur est un candidat pour la réponse.
3. La réponse est la longueur de la plus longue chaîne unique; sinon `-1`.

Parce qu'une chaîne qui apparaît plus d'une fois ne peut jamais être une subséquence peu commune (c'est une subséquence de lui-même et au moins une autre chaîne identique), il suffit d'examiner des chaînes uniques.

- Oui. 1. Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
public int findLUSlength(String[] strs) {
// Nombre d'occurrences
Carte<String, entier> freq = nouveau HashMap<>();
pour (String s : strs) {
freq.put(s), freq.getOrDefault(s), 0) + 1);
}

int best = -1;
pour (String s : strs) {
si (freq.get(s)) == 1) { // chaîne unique
best = Math.max(best, s.longueur());
}
}
le meilleur retour;
}

// Pour des tests locaux rapides
public statique vide principal(String[] args) {
var sol = nouvelle solution();
Système.out.println(sol.findLUSlongueur(nouvelle chaîne[]{"aba","cdc","eae"}); // 3
Système.out.println(sol.findLUSlongueur(nouvelle chaîne[]{"aaa","aa","aa"}); // -1
}
}
«» "

**Points clés* *
- Utilise `HashMap` pour les recherches O(1).
- Scan linéaire ('O(n)') au-dessus de l'entrée; pas de boucles imbriquées, donc il fonctionne dans **O(n)** temps et **O(n)** espace.

---

- Oui. 2. Python 3

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def findLUSlength(self, strs: List[str]) -> Int:
freq = Contre(strs) # fréquence de chaque chaîne
# trouver la plus longue chaîne qui apparaît exactement une fois
retour max((len(s) pour s dans strs si freq[s] == 1), par défaut=-1)

# Test local rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.findLUSlongueur(["aba", "cdc", "eae"]) # 3
print(sol.findLUSlongueur(["aaa", "aaa", "aa"]) Numéro 1
«» "

** Faits saillants* *
- "Counter" donne le nombre d'O(n).
- L'expression du générateur maintient l'utilisation de la mémoire faible.
- `default=-1` dans `max` s`occupe de l`étui de chaîne unique.

---

- Oui. 3. C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int findLUSlongueur(vecteur<string>& strs) {
non ordonné_map<string, int> freq;
pour (cont string & s : strs) ++freq[s]; // Compte

int best = -1;
pour (cost string & s : strs)
si (freq[s]) 1) // Unique
best = max(best, (int)s.s.size());

le meilleur retour;
}
};

// Main simple pour les essais
Int main() {
Solution sol;
la durée de l'essai est << sol.findLUSlength({"aba","cdc","eae"}) << endl; // 3
<< sol.findLUSlongueur({"aaa","aa","aa"}) << endl; // -1
retour 0;
}
«» "

**Pourquoi c'est slick* *
- `unordered_map` offre des inserts et des recherches à temps constant.
- Utilise la gamme pour les boucles pour la lisibilité.
- Compile en **O(n)** temps et utilise **O(n)** espace auxiliaire.

---

Résumé de la complexité

Langue Heure Espace
- C'est quoi ?
*Java* O(n)* O(n)*
Python O(n)
C++= O(n)= O(n)=

*`n` = nombre de chaînes (= 50). *

---

La plongée profonde : pourquoi le comptoir simple fonctionne

1. **Si une chaîne apparaît plus d'une fois**
- C'est une subséquence de lui-même et au moins une autre chaîne identique → ne peut pas être rare.

2. **Si une chaîne apparaît exactement une fois**
- Aucune autre corde ne peut être identique.
- Parce que toutes les autres chaînes sont * plus courtes ou égales* en longueur (max 10), la chaîne unique ne peut être une subséquence d'aucune autre chaîne (une subséquence doit préserver l'ordre relatif, mais vous ne pouvez pas intégrer une chaîne plus longue dans une chaîne plus courte).
- Ainsi, toute chaîne unique est automatiquement une séquence peu commune.

3. **Choisir le plus long* *
- Parmi toutes les cordes uniques, la plus longue est la réponse.
- Si aucune chaîne unique n'existe, la réponse est `-1`.

---

Cas de bord & Gotchas

Cas de bord Qu'est-ce que regarder ?
- C'est quoi ?
Autres Toutes les chaînes sont identiques.
Longueurs mélangées
Tableau de chaînes vide (non autorisé par les contraintes)
Des longueurs jusqu`à 10° Aucun risque de débordement entier
Autres Très petit tableau (`n = 2`)

---

Conseils d'entrevue

1. ** Expliquer l'observation tôt**: Si une chaîne se répète, elle ne peut pas être rare. Par conséquent, nous avons seulement besoin de regarder des chaînes uniques. (en milliers de dollars)
2. **Complexité de la concentration**: temps O(n), espace O(n), rapidité et efficacité de la mémoire.
3. **Afficher les exemples de cas d'essai**: Inclure les deux exemples de Leetcode et un cas personnalisé comme `["a","b","ab"]`.
4. **Discussion alternative (force brute)**: Nous pourrions générer tous les subséquences et tester chacun, mais ce serait exponentiel et inutile. (en milliers de dollars)

---

Article du blog: ♫Master Leetcode 522 – Subséquence la plus longue peu fréquente II (Java, Python, C++)

---

Titre
**Crack Leetcode 522: Subséquence la plus longue peu fréquente II – 3 solutions gagnantes (Java, Python, C++)* *

Description de la méta
Apprenez la stratégie optimale pour Leetcode 522 avec le code Java, Python et C++ propre. Comprendre le problème, algorithme, cas de bord, et comment impressionner les recruteurs. Parfait pour coder la préparation d'entrevue.

Mots clés
- Leetcode 522
- Succès le plus long peu fréquent II
- Solution Java
- Solution Python
- Solution C++
- Entretien de codage
- Entretien de l'ingénieur logiciel
- Entretien avec l'algorithme
- Peu fréquent

Aperçu

1. **Introduction** – pourquoi ce problème est important.
2. **Énoncé du problème** – récapitulation claire et concise.
3. **Observations** – le point de vue clé qui réduit le problème à un comptage de fréquence.
4. **Algorithme** – description étape par étape.
5. ** Analyse de complexité** – temps et espace.
6. **Java Implementation** – code + commentaire.
7. **Python Implementation** – code + commentaire.
8. **C++ Mise en œuvre** – code + commentaire.
9. **Cas et pièges d'Edge** – comment éviter les erreurs courantes.
10. **Conseils d'entrevue** – comment présenter la solution lors d'une entrevue.
11. **Conclusion** – message à emporter et prochaines étapes.

---

- Oui. 1. Présentation

Si vous vous préparez à une entrevue d'ingénierie logicielle, vous allez inévitablement frapper des problèmes de chaîne lourde. Leetcode 522, *Longest Unlowful Subsequence II*, est un défi populaire car il teste à la fois votre pensée conceptuelle et votre capacité à écrire un code propre et efficace. Dans ce post, nous allons parcourir le problème, révéler l'observation secrète qui transforme un cauchemar O(n2) en une solution O(n), puis présenter des implémentations polies dans **Java**, **Python** et **C++**.

---

- Oui. 2. Exposé des problèmes

> **Given** un tableau de chaînes `strs`, trouver la longueur de la plus longue chaîne qui est un subséquence de **exactement un** élément de tableau.
> **Retour** `-1` si aucune telle chaîne n'existe.

*Subséquence* signifie que vous pouvez supprimer n'importe quel nombre de caractères tout en gardant l'ordre des autres.

---

- Oui. 3. Observations

- Une chaîne qui apparaît **plus d'une fois** ne peut jamais être une subséquence peu commune (c'est une subséquence de lui-même et au moins une autre chaîne identique).
- Toute chaîne **unique** ne peut pas être une séquence d'une autre chaîne dans le tableau si elle est plus longue que les autres chaînes, car vous ne pouvez pas intégrer une chaîne plus longue dans une chaîne plus courte.
- Oui. Par conséquent, le problème se réduit à : *Trouver la plus longue chaîne unique dans le tableau. *

Cette seule ligne de perspicacité effondre le problème d'une recherche exponentielle de tous les subséquences à un simple comptage de fréquence.

---

- Oui. 4. Algorithme

1. **Couvercle des fréquences** de chaque chaîne dans "strs".
2. **Itérer** sur la liste originale; pour chaque chaîne ayant une fréquence = 1, considérer sa longueur.
3. Retourner la longueur **maximum** parmi ces chaînes uniques; si aucune n'existe, retourner `-1`.

---

- Oui. 5. Analyse de la complexité

Opération Complexité
C'est quoi ?
Fréquences de comptage **O(n)** Autres
Analyse pour max. **O(n)** Autres
Total **O(n)** temps, **O(n)** espace

Avec `n ≤ 50` et des longueurs de cordes ≤ 10, c'est confortablement rapide pour tout environnement d'entretien.

---

- Oui. 6. Mise en œuvre Java

"Java
Importation de java.util.*;

solution de classe publique {
public int findLUSlength(String[] strs) {
Carte<String, entier> freq = nouveau HashMap<>();
pour (String s : strs) {
freq.put(s), freq.getOrDefault(s), 0) + 1);
}

int best = -1;
pour (String s : strs) {
si (freq.get(s)) == 1) {/ unique
best = Math.max(best, s.longueur());
}
}
le meilleur retour;
}
}
«» "

*Pourquoi il brille :* `HashMap` donne des recherches à temps constant; nous ne générons jamais de sous-séquences.

---

- Oui. 7. Mise en œuvre de Python

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def findLUSlength(self, strs: List[str]) -> Int:
freq = compteur(s)
retour max((len(s) pour s dans strs si freq[s] == 1), par défaut=-1)
«» "

*Pourquoi il brille :* `Counter' et une expression de générateur maintiennent le code concis et convivial pour la mémoire.

---

- Oui. 8. Mise en œuvre C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int findLUSlongueur(vecteur<string>& strs) {
non ordonné_map<string, int> freq;
pour (cont string & s : strs) ++freq[s];
int best = -1;
pour (cost string & s : strs)
si (freq[s]) 1 )
best = max(best, (int)s.s.size());
le meilleur retour;
}
};
«» "

*Pourquoi il brille:* `unordered_map` offre les mêmes avantages à temps constant, et la gamme basée pour les boucles lues naturellement.

---

- Oui. 9. Cas de bord et pièges

Réparer les bords
- C'est quoi ?
Autres Toutes les chaînes sont identiques.La boucle ne trouvera jamais de fréquence = 1; retourner `-1`. Autres
L'algorithme le choisit automatiquement. Autres
Les contraintes garantissent au moins deux chaînes. Autres
Autres Les cordes très courtes (`""`) Autres

---

10 ans. Conseils d'entrevue

1. **Décrivez d'abord la principale observation**: Si une chaîne apparaît plus d'une fois, elle ne peut pas être rare. (en milliers de dollars)
2. **Parler à travers l'algorithme** tout en esquissant la carte de fréquence sur un tableau blanc.
3. **Complexité de l'intervention** pour rassurer l'intervieweur.
4. **Afficher un test rapide**: `["a","b","ab"] → 2` (la chaîne `"ab"` est unique).
5. **Discuse alternative** (force brute) seulement si l'intervieweur demande, pour vous montrer comprendre pourquoi l'approche optimisée est supérieure.

---

11 ans. Conclusion

Leetcode 522 est un problème trompeurment simple une fois que vous remarquez l'astuce: la plus longue séquence peu commune est simplement la plus longue chaîne **unique**. Cela réduit la tâche à un compte de fréquence à un passage et à un scan max-longueur, donnant du temps et de l'espace à O(n). Les solutions Java, Python et C++ ci-dessus sont prêtes à copier-coller dans votre boîte à outils d'entretien de codage.

**Étape suivante:** Pratique expliquant la perspicacité à haute voix, et essayez de résoudre le Leetcode 521, *La plus longue subséquence peu commune*, où les cordes ne sont pas nécessairement uniques et l'approche de la force brute devient inévitable.

---

Bon codage, et bonne chance écraser votre prochaine interview! C'est ce qu'il a dit.

---

Article de fin de blog

---

Ces notes devraient vous aider à préparer non seulement le code, mais le narratif qui rend les intervieweurs cliquez sur "impressionnant". Bonne chance !