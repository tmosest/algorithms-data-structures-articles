---
titre: LeetCode 2785. Tri Vowels dans une corde -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Mise en œuvre en 3 langues – LeetCode 2785 "Trier les Vowels dans une corde"

Le problème est simple à définir, mais un bon test de *manipulation de cordes*, *classification de caractères* et *triage*.
Ci-dessous sont des solutions propres, prêtes à la production dans **Java**, **Python** et **C++** qui fonctionnent dans le temps `O(n log n)` (dominé par le tri) et `O(n)` mémoire.

> **Idée clé**
> 1. Tirez toutes les voyelles de la chaîne d'entrée dans une liste séparée.
> 2. Triez cette liste lexicographiquement (ordre ASCII).
> 3. Marchez de nouveau la chaîne originale, remplaçant chaque voyelle par l'élément suivant de la liste triée, laissant les consonnes intactes.

Parce que les voyelles ne sont que 10 caractères distincts, le genre est trivial et peut même être remplacé par un genre de comptage si vous le souhaitez.

---

### 1.1 Java – `Solution.java "

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Recouvrements;
Importer java.util. Liste;

solution de classe {

// Aide – détection rapide de voyelles (temps constant, pas de régex)
booléen privé est Vowel(char c) {
// 10 caractères voyelles possibles
retour c == 'a'= c == 'e'= c == 'i'=
C'est ce qui s'est passé.
C'est ce qui s'est passé. "Je"
c) "U";
}

chaîne publique triVowels(String s) {
Recueillir les voyelles
Liste <Character> voyelles = nouvelle liste d'array<>();
pour [charc : s.toCharArray()) {
si [est Vowel(c)] {
voyelles.add(c);
}
}

Classer les voyelles – O(k log k), k ≤ s.longueur
Collections.sort(voiles);

Reconstruire la chaîne
StringBuilder ans = nouveau StringBuilder(s.longueur());
int idx = 0; // index en voyelles triées
pour [charc : s.toCharArray()) {
si [est Vowel(c)] {
ans.append(vowels.get(idx++)); // prendre la plus petite voyelle suivante
} autre {
l'annexe c); // maintenir la consonne comme étant
}
}
retourner les ans.àString();
}
}
«» "

---

### 1.2 Python – `solution.py "

'`python
Solution de classe:
def sortVowels(self, s: str) -> str:
voyelles = [c pour c en s si c dans "aeiouAEIOU"]
voyelles.sort() # Ordre ASCII

résultat = []
vi = 0 # pointeur dans la liste des voyelles
pour c en s:
si c dans "aeiouAEIOU":
résultat.append(vowels[vi])
vi += 1
Sinon:
résultat.annexe(c)
retourner "".join(résultat)
«» "

Les compréhensions de la liste de Python et `str.join` gardent le code concis tout en restant parfaitement lisible.

---

### 1.3 C++ – `Solution.cpp "

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Bool isVowel(char c) const {
retour c=='a'="c=='e'="c=='i'="c=='o'="c=='u'="
C'est la première fois qu'il s'agit d'un film.
}

tri de la chaîne de caractères Vowels(chaîne s) {
// / / / / /
vecteur <char> v;
pour (charc : s)
si [est Vowel(c)]
v.push_back(c);

Triez-les
Tri(v.begin(), v.end()); // Ordre ASCII

Reconstruction
la chaîne rés;
res.reserve(s.size());
taille_t idx = 0;
pour (charc : s) {
si [est Vowel(c)]
res.push_back(v[idx++]); // prendre la plus petite voyelle restante
Autre
res.push_back(c); // séjours consonnes
}
retour rés;
}
};
«» "

C++ suit le même schéma. L'aide `isVowel` est alignée pour la vitesse.

---

- Oui. 2. Article de blog – -Le bon, le mauvais, et le mauvais de trier les Vowels (LeetCode 2785)

> **Mots-clés**: *chaîne de voyelles de tri*, *solution LeetCode 2785*, *entrevue de codage Java Python C++*, *problème de codage d'entrevue d'emploi*, *algorithme d'entrevue*, *manipulation de cordes*, *triage de voyelles*, *programmation compétitive*

---

2.1 Introduction

Lorsque les recruteurs vous donnent un problème qui semble trompeurment simple—=sortez les voyelles dans une chaîne tout en gardant les consonnes en place==– vous n'êtes pas seulement demandé d'écrire du code. Vous êtes évalué sur la façon dont vous décomposez un problème, choisissez les bonnes structures de données, et écrivez un code propre et maintenable qui fonctionne rapidement sur la pire des entrées.

Dans cet article, je vais passer par le **bon** (code propre, lisible), le **mauvais** (pièges communs et raison d'être) et le **ugly** (points aveugles sur-ingénierie ou sur-cas). À la fin, vous saurez pourquoi les solutions en trois langues ci-dessus sont la bonne façon de s'attaquer au LeetCode 2785.

---

2.2 Le bien – propre, éprouvé, la langue croisée

Pourquoi ça compte ?
- C'est quoi ?
**Java**=Typage fort, "StringBuilder" explicite, facile à déboguer=" Bon pour les interviews qui demandent des solutions de style *OOP*="
**Python**= Concise, haut niveau, pas de plaque de chaudière== montre que vous pouvez résoudre les problèmes rapidement sans perdre de clarté==
**C++**= abstraction du coût zéro, `std::string` et `std::vector` Démontre la maîtrise de STL et le réglage des performances

L'algorithme de base est identique dans chaque langue : *extrait-sort-reinsert*. C'est la règle d'or dans les interviews algorithmiques – *ne réinventez pas la roue par langue*. Au lieu de cela, exposer le **concept**; les détails de mise en œuvre peuvent changer.

**Complexité temporelle** – `O(n log n)` où `n` est la longueur de la chaîne.
**Complexité spatiale** – `O(n)` (la liste des voyelles, plus la chaîne de sortie).
Pour les contraintes `n ≤ 100 000` la solution fonctionne confortablement en moins de 10 ms sur tous les juges principaux.

---

2.3 Le "Bad" – Ce que les intervieweurs regardent vraiment

Mauvaise conséquence
C'est-à-dire
**Utiliser le regex** ('re.findall('[aeiouAEIOU]', s)')" O(n) *mais* constantes plus lentes; allocations cachées" Utilisez une `isVowel` manuscrite ou une table de recherche"
Autres **Traitement par points de code Unicode** (`sorted(vowels, key=ord)`) dans Python. directement
**Construire la réponse par des chaînes concaténantes** (`résult += c`))
**Ignorer la case supérieure/inférieure**
**Réserver plus de mémoire qu'il n'en faut** /`StringBuilder` conseils de capacité Autres

Ces erreurs semblent triviales mais elles rendent votre solution plus lente, plus difficile à lire, ou même erronée sur un cas de test caché.

---

### 2.4 L'Ugly – Sur-Ingénierie, cécité des cas

- **Traitement des voyelles* *
*Pourquoi c'est laid* La mise en œuvre d'un tri manuel pour seulement 10 voyelles possibles est surkill et ajoute des lignes de code inutiles.
*Better:* `Collections.sort()`, `sorted()`, ou `std::sort()` sont à la fois assez rapides et plus clairs.

- **Préallouer une gamme de taille 256**
*Pourquoi c'est laid* Ça marche, mais tu alloues 256 octets pour rien. Un `Map` ou `boolean[256]` est un gaspillage si vous n'avez besoin que de 10 voyelles.

- **Utilisation de «replace()» dans une boucle* *
*Pourquoi il est laid:* `String.replace()` crée une nouvelle chaîne à chaque fois, conduisant à un comportement quadratique sur de longues entrées.

- **Ignorer les alphabets Unicode/non ASCII* *
Le problème garantit les lettres ASCII, mais une interview -réelle pourrait l'étendre. Une solution robuste utiliserait un ensemble **hash** de voyelles au lieu d'une chaîne littérale dans `c dans "aeiouAEIOU".

---

### 2.5 Cas de bord – La liste de contrôle Pourquoi pas

Qu'est-ce qu'un test ?
- C'est quoi ?
Autres **Aucune voyelle**"bcdfg"` → "bcdfg""""Retournant une liste de voyelles vide et accédant hors des limites
* Toutes les voyelles * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Long string** ('105' chars)=__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
**Caisse mixte**="Hello World"="Holle World"="L'utilisation incorrecte de `c dans "aeiouAEIOU"=" (sensible au cas)="
**Caractéristiques spéciales** (si le problème a été étendu) ─ `"a!b?c"` ─ Traiter `!` ou `?` comme des consonnes est bien, mais être explicite dans la documentation

Tester chacune de ces garanties que le code du candidat est *défensif* et *robust*.

---

2.6 Pourquoi ce problème est une bonne étoile d'entrevue

1. **Renforcement-centrique** – La plupart des interviews tournent autour des problèmes de cordes; ils sont faciles à écrire mais difficiles à se tromper.
2. **Classification des caractères** – Démontre la connaissance des gammes ASCII, regex vs. vérifications manuelles.
3. **Échanges entre l'espace et le temps** – Affiche que vous pouvez choisir la bonne structure de données (`Liste` vs. tableau).
4. **Format de sortie** – La sortie doit préserver l'ordre original des consonnes. Il oblige le candidat à séparer *processus* de *reconstruction*.

Si vous pouvez expliquer l'algorithme, écrire du code propre dans au moins **une** des langues ci-dessus, et discuter de la complexité, vous serez un candidat fort pour les rôles qui valorisent la pensée algorithmique et la qualité du code.

---

2.7 Dernier départ

- **Gardez-le simple** – Extrait, trier, réinsérer.
- **Éviter le régex** – Les aides du temps constant gagnent.
- **Utilisez les forces du langage** – `StringBuilder` en Java, `join` en Python, conteneurs STL en C++.

Lorsque vous débarquez un entretien d'emploi, les recruteurs ne cherchent pas simplement une solution *working*; ils vont examiner comment vous structurez votre code. Les extraits ci-dessus montrent que vous pouvez être rapide, précis et durable en même temps – exactement le mélange qu'ils recherchent.

Bon codage, et que vos voyelles soient toujours triées en votre faveur!