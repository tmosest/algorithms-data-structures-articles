---
titre: LeetCode 2309. La plus grande lettre anglaise en majuscule et en minuscule -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2309 – La plus grande lettre anglaise en majuscule et en minuscule
> Une solution rapide et prête à l'interview (Java / Python / C++) + un billet de blog (SEO optimisé, le bon, le mauvais, le laid)

---

## TL;DR – Un liner pour chaque langue

Code de la langue
C'est quoi, ça ?
*Java** Lettre(String s){Set<Caracter> set=new HashSet<>();pour(char c:s.toCharArray()set.add(c);pour(char c='Z';c>='A';c--)if(set.contient(c)&&set.contient((char)('a'+c-'A')))retour "+c;retour";}`
**Python**"def bestLetter(s): retour suivant(c pour c en inversed('ABCDEFGHIJKLMNOPQRSTUVWXYZ') si c dans s et c.lower() dans s), '')"
*C++** Lettre(string s){unordered_set<char> st(s.begin(),s.end());pour(char c='Z';c>='A';--c)if(st.count(c)&&st.count(tolower(c))return string(1,c);return ");}`

Les trois solutions fonctionnent dans **O(n)** temps, **O(1)** espace supplémentaire (ignorer l'ensemble), et sont parfaites pour une entrevue de codage.

---

## Le problème (Code Leet 2309)

> **Grâce à une chaîne de lettres anglaises, retournez la lettre *la plus grande* qui apparaît dans **tous les deux** sa forme minuscule et majuscule.
> La lettre retournée doit être en majuscule; si aucune lettre n'existe, retourner une chaîne vide.

> *La grandeur* est définie par l'ordre alphabétique (`Z` > `Y` > ... > `A`).

> **Constraints**
> * `1 ≤ longueur ≤ 1000`
> * `s` ne contient que des lettres alphabétiques anglaises.

---

- Oui. Pourquoi ce problème est important

1. **Entretien amical** – Il teste deux compétences de base:
* Manipulation de caractères (mathématiques ASCII ou aides intégrées).
* Définir l'utilisation / recherche basée sur le hachage.
2. **Real‐World Pertinence** – De nombreuses applications nécessitent des vérifications sensibles aux cas (p. ex., noms d'utilisateur, clés de base de données).
3. **REO / Prime de chasse à l'emploi** – Maîtriser ce problème démontre que vous pouvez gérer les cas de korner et l'optimisation des qualités – les recruteurs aiment.

---

## Aperçu de l'approche

1. **Collecter tous les caractères** dans un jeu de hachage (`Set<Caracter>` ou `unordered_set<char>`).
*Pourquoi?* Recherches constantes pour les vérifications d'existence.

2. **Scan de «Z» jusqu'à «A»** – la plus grande lettre d'abord.
*Si* la lettre majuscule *et* son homologue minuscule existent tous les deux dans l'ensemble, c'est notre réponse.
* Pourquoi à partir de "Z"? Garanties le premier match est la plus grande lettre; nous pouvons arrêter tôt.

3. **Retourner une chaîne vide** si aucune paire n'est trouvée.

Complexité

Étape Temps Espace
C'est pas vrai.
Ensemble de bâtiments
Numériser 26 lettres
**O(n)**

---

Le bon, le mauvais, le mauvais

Aspect du bien
- C'est quoi ?
**Readability** Certains préféreront peut-être le bit-mask pour une vitesse supplémentaire. Si vous utilisez le bit-masking, le code devient opaque. Autres
**Performance**= O(n) avec petite constante; passe tous les tests LeetCode rapidement. L'utilisation de tableaux (taille 52) serait également très bien; le réglage est plus clair. Une double boucle de force brute (O(262)) est encore bonne pour n=1000, mais pas évolutive. Autres
Autres **Cas d'escroquerie**=Poignée : chaîne vide, toutes les minuscules, toutes les majuscules, mélangées. Rien de significatif. Autres
* Nuances de langue*** Java: `HashSet`, Python: générateur, C++: `unordered_set`. Autres

---

## Code Passages

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe {
publique Lettre(s) {
// Étape 1: mettre chaque personnage dans un ensemble
Set<Caracter> set = nouveau HashSet<>();
pour (char ch : s.toCharArray()) {
l'ensemble.add(ch);
}

// Étape 2: vérifier à partir de 'Z' vers le bas
pour (char ch = 'Z'; ch >= 'A'; ch--) {
si (set.contient(ch) && set.contient((char) (ch + ('a' - 'A'))) {
retour String.valueOf(ch);
}
}
// Étape 3: aucun trouvé
retour ";
}
}
«» "

**Notes**
* `ch + ('a' - 'A')' convertit les majuscules en minuscules via les mathématiques ASCII.
* Pas de tableau explicite ; set garantit des recherches à temps constant.

---

- Oui. 2. Python

'`python
def bestLetter(s): str) -> str:
# défini pour les vérifications d'adhésion O(1)
voir = ensemble(s)

# itérer de 'Z' vers le bas
pour c en marche arrière(' Objet
si c en vue et c.inférieur() en vue:
retour c
retour ""
«» "

**Notes**
* `reversed('ABCDEFGHIJKLMNOPQRSTUVWXYZ') ' donne l'ordre décroissant.
* Python est "in" sur un ensemble est amorti O(1).
* Élégant un-liner dans la boucle si vous vous sentez fantaisiste.

---

- Oui. 3. C++

'`cpp
#incluez <string>
#inclut <unordered_set>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne plus grande Lettre(chaîne s) {
_set <char> st(s.begin(), s.end() non classé;

pour (char c = «Z»; c >= «A»; --c) {
si (premier compte(c) && st.count(dernier(c))) {
retour de la chaîne(1, c);
}
}
retour ";
}
};
«» "

**Notes**
* `unordered_set<char>` donne une recherche O(1).
* Le mot `inférieur(c)' convertit les majuscules en minuscules.
* `string(1, c)` construit une chaîne à caractère unique pour la réponse.

---

## Solutions alternatives et optimisations

Description de la méthode
- C'est quoi ?
**Bitmask** (`int mass = 0`) Extrêmement rapide (pas de hachage). Moins lisible; la manipulation bit peut être excessive pour n ≤ 1000. Autres
**Tableau de taille 52**.Deux booléens par lettre: majuscule et minuscule. Pas de hachage au-dessus; mémoire constante. Un peu plus de verbe qu'un ensemble. Autres
**Trier + Deux-pointeurs** Pas de mémoire supplémentaire en plus de la chaîne triée. Temps supplémentaire O(n log n) – pas optimal pour l'entrevue. Autres

---

## Conseils aux intervieweurs

1. **Demander des précisions** – Par exemple, sommes-nous garantis que `s` ne contient que des lettres ASCII? (en milliers de dollars)
2. **Complexité de la concentration** – temps O(n), espace O(1). (en milliers de dollars)
3. **Parler des cas de bord** – chaîne vide, seulement cas inférieur / supérieur, lettres répétées.
4. **Afficher d'autres solutions** – bitmask ou tableau – pour démontrer la profondeur.

---

## SEO-Optimized Blog Post Outline

1. **Titre**
*LeetCode 2309: La plus grande lettre anglaise – Java, Python, C++ Solutions & Interview Prep

2. **Description détaillée**
*Solve LeetCode 2309 en quelques minutes. Apprenez le code Java, Python et C++, comprenez la logique, et asez votre interview de codage avec ce problème facile mais intelligent. *

3. **Traitements (H1‐H3)**
* H1: LeetCode 2309 – La plus grande lettre anglaise
* H2 : Résumé des problèmes et contraintes
* H2 : Algorithme – Réglage + Scan inverse
* H3 : Mise en œuvre Java
* H3 : Mise en œuvre de Python
* H3: Mise en œuvre C++
* H2 : Analyse de complexité
* H2 : Solutions de rechange et compromis
* H2 : Perspective de l'intervieweur – -
* H2: A emporter pour votre prochain entretien
* H2 : Foire aux questions

4. **Mots clés**
* LeetCode 2309, le plus grand anglais Lettre, entretien de codage, solution Java, solution Python, solution C++, préparation d'entretien, analyse d'algorithmes, opérations de set, manipulation de chaînes.

5. **Appel à l'action**
Vous avez une question ? Laissez un commentaire ci-dessous ou rejoignez LinkedIn – heureux de vous aider à répondre à votre prochaine interview !

---

Les pensées finales

- **Pourquoi cet article est important** – Il met en valeur votre capacité de traduire un énoncé de problème en code propre et agnostique, de discuter des compromis et d'anticiper les questions d'entrevue.
- **Avantage de la chasse à l'emploi** – En publiant une écriture claire, optimisée par le SEO, vous démontrez des compétences en communication, une passion pour les algorithmes et une disponibilité pour les entrevues techniques.
- **Prochaine étape** – Jumelez le code avec les tests unitaires et une section de démarrage rapide sur la façon de l'exécuter localement. Ensuite, partagez sur GitHub, LinkedIn et les sous-reddits pertinents (r/leetcode, r/cscareerquestions).

Bon codage – et bonne chance pour la prochaine entrevue! C'est ce qu'il a dit