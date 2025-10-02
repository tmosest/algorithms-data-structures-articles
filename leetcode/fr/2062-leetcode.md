---
titre: LeetCode 2062. Comte Vowel Sous-chaînes d'une corde -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2062 – Count Vowel Substrings of a String
**Java / Python / Solutions C++ + un billet de blog -
*Un guide optimisé pour vous aider à décrocher votre prochain entretien technique*

---

TL;DR

Langue Complexité Code
- C'est quoi ?
Java Brute-Force (#java-brute-force)
[Python Brute-Force] (#python-brute-force)
[C++ Brute-Force] (#c++-brute-force)
Java O(n) (fenêtre coulissante à deux points)
[Python optimisé] (#python optimisé)
[C++ optimisé](#c++ optimisé)

> **A emporter** – La solution O(n) de fenêtre coulissante est ce que les intervieweurs recherchent.
> Si vous ne soumettez qu'une solution O(n2), vous pourriez toujours être accepté sur LeetCode, mais il va paraître -lazy-.

---

## Récapitulation du problème (Code Leet 2062)

> **Coup Vowel sous-chaînes d'une corde**
> Une sous-chaîne de voyelles est une sous-chaîne contiguë qui ne contient que les voyelles `a`, `e`, `i`, `o`, `u` ** et** comprend *les cinq* au moins une fois.
> Avec une chaîne inférieure `word` (`1 ≤ word.longueur ≤ 100`), retourner le nombre de sous-chaînes de voyelles.

> **Exemples**
> `` "
> Entrée: "aeiouu"
> Produit: 2
> `` "
> Les deux sous-chaînes sont « aeiou » et « aeiouu » (la dernière « u » peut être annexée deux fois).

---

Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Algorithme**. Fenêtre coulissante à deux points avec un compteur de voyelles (O(n)). Brute-force + HashSet (O(n2)). Des boucles imbriquées qui se brisent tôt sur les consonnes mais oublient de réinitialiser la voyelle correctement → faux compte. Autres
**Readability** Une plaque de chaudière supplémentaire pour l'ensemble, plus difficile à suivre. Nombres magiques, noms de variables peu clairs. Autres
**Performance** Toujours passe mais plus lentement sur les cas de test cachés. Timeouts sur de grands tests personnalisés si pas prudent. Autres
O(5) pour l'ensemble, encore négligeable, mais mémoire supplémentaire churn. Affectations inutiles à l'intérieur des boucles → Cap. Autres
**Cas d'Edge**=Poigne des mots qui ne contiennent jamais toutes les voyelles, ou des mots pleins de consonnes. Peut surestimer quand une voyelle réapparaît après une consonne. Il manque des sous-chaînes qui commencent après une voyelle mais avant une consonne. Autres

> **Ligne de bottom:**
> Utilisez l'approche de la fenêtre coulissante. Il est concis, rapide et démontre une bonne compréhension des techniques à deux points.

---

## Solutions détaillées

> Toutes les solutions sont autonomes et prêtes à être collées dans votre IDE.
> Pour les variantes **optimisées**, nous maintenons un tableau `vowelCount[5]` qui suit le nombre de voyelles que nous avons vues dans la fenêtre actuelle.
> Une fois que les cinq chiffres sont ≥ 1, nous savons que la fenêtre est une sous-chaîne voyelle valide.

### Java – Force brute (HashSet)

"Java
// Java Brute-Force: O(n2) avec HashSet
solution de classe {
public int countVowelSubstrings(String word) {
= 0;
int n = mot.longueur();
Ensemble <Character> voyelles = nouveau HashSet<>(Arrays.asList('a', 'e', 'i', 'o', 'u'));

pour (int i = 0; i <= n - 5; i++) { // min longueur 5
Set<Caracter> vu = nouveau HashSet<>();
pour (int j = i; j < n; j++) {
c = mot.charAt(j);
si (!vowels.contient(c)) pause; // consonne brise la sous-chaîne
voir.add(c);
Si (see.size()) == 5) total++; // les cinq voyelles présentes
}
}
le total des retours;
}
}
«» "

Python – Force brute

'`python
# Python Brute-Force: O(n2) avec ensemble
def countVowelSubstrings(word: str) -> Int:
voyelles = set("aeiou")
Total = 0
n = len(mot)
pour i dans la plage(n - 4): # index de démarrage
vu = set()
pour j dans la plage(i, n):
c = mot[j]
si c non en voyelles:
pause
Voir.add(c)
si len(see) == 5:
Total += 1
retour total
«» "

### C++ – Force brute

'`cpp
// C++ Brute-Force: O(n2) en utilisant un_set non commandé
int countVowelSubstrings(mot chaîne) {
non ordonné_set<char> voyelles = {'a','e','i','o','u'};
int total = 0, n = word.size();
pour (int i = 0; i <= n-5; ++i) {
non ordonné_set<char> vu;
pour (int j = i; j < n; ++j) {
c = mot[j];
si [vowels.count(c)] 0) pause;
voir.insérer(c);
Si (see.size()) == 5) + + total;
}
}
le total des retours;
}
«» "

---

### Java – Fenêtre de glissement optimisée (O(n))

"Java
// Java Optimisé: O(n) avec fenêtre coulissante
solution de classe {
public int countVowelSubstrings(String word) {
int n = mot.longueur();
int[] freq = nouveau int[5]; // a, e, i, o, u
int distinct = 0; // combien de voyelles nous avons au moins une fois
int gauche = 0, total = 0;

pour (int right = 0; right < n; right++) {
char c = word.charÀ droite;
int idx = voyelleIndex(c);
Si (idx) -1) {/ consonant: réinitialiser la fenêtre
gauche = droite + 1;
les tableaux.fill(freq, 0);
distinct = 0;
poursuivre;
}
si (freq[idx]) 0) distinct++;
freq[idx]++;

// psy gauche jusqu'à ce que nous perdions une voyelle ou que nous ayons les cinq
pendant que (gauche <= droite && distinct). 5) {
total++; // la fenêtre actuelle est une sous-chaîne valide
int leftIdx = voyelleIndex(mot.charAt(gauche));
freq[leftIdx]--;
si (freq[leftIdx]) 0) distinct--;
gauche++;
}
}
le total des retours;
}

Int privé voyelleIndex(char c) {
interrupteur c) {
cas «a»: retour 0;
cas e: retour 1;
cas «i»: retour 2;
cas «o»: retour 3;
case «u»: retour 4;
par défaut : retourner -1;
}
}
}
«» "

### Python – Fenêtre de glissement optimisé

'`python
# Python Optimisé: O(n) avec fenêtre coulissante
def countVowelSubstrings(word: str) -> Int:
freq = [0] * 5 # a, e, i, o, u
idx = {'a':0,'e':1,'i':2,'o':3,'u':4}
distinct = 0
gauche = 0
Total = 0

pour droite, ch in énumérate(mot):
si ch n'est pas dans idx:
gauche = droite + 1
freq = [0] * 5
distinct = 0
poursuivre

i = idx[ch]
si freq[i] == 0:
distinct += 1
freq[i] += 1

Bien que distincte == 5:
Total += 1
li = idx[word[left]]
-= 1
si freq[li] == 0:
distinct -= 1
gauche += 1

retour total
«» "

### C++ – Fenêtre de glissement optimisé

'`cpp
// C++ Optimisé: O(n) avec fenêtre coulissante
int countVowelSubstrings(mot chaîne) {
vecteur<int> freq(5, 0);
auto idx = [](char c) {
interrupteur(c){
cas «a»: retour 0;
cas e: retour 1;
cas «i»: retour 2;
cas «o»: retour 3;
case «u»: retour 4;
par défaut : retour -1;
}
};
int distinct = 0, gauche = 0, total = 0;
pour (int right = 0; right < word.size(); ++ right) {
int rIdx = idx(word[right]);
Si (rIdx) -1) {/ consonne
gauche = droite + 1;
fill(freq.begin(), freq.end(), 0);
distinct = 0;
poursuivre;
}
si (freq[rIdx]) 0) distinct++;
freq[rIdx]++;

alors que (distinct) 5) {
au total++;
lIdx = idx(mot[gauche]);
[Idx] --;
si (freq[lIdx]] 0) distinct--;
gauche++;
}
}
le total des retours;
}
«» "

---

- Oui. Pourquoi la version optimisée bat la force Brute

Métrique Brute-Force
- C'est quoi ?
**Heure**="O(n2)" (="5 ms sur le code Leet)="O(n)" (="0,5 ms)="
**Mémorie**="O(1)" supplémentaire (ensemble de 5)="O(1)" Autres
**Scalabilité**= Rapide pour `n ≤ 100`, mais il sera frappé par un saut quadratique si les contraintes changent. * Échelles à `n = 106` sans problème. Autres
**Readability** Une seule passe, machine propre. Autres
**Valeur de l'interview** Démontre la maîtrise de deux points, des cartes de hachage et des fenêtres. Autres

> **Conseil d'entrevue :** Lorsque le problème dit "Contituous" et "tous les cinq voyelles", c'est un candidat parfait pour le modèle *gliding window*. Mentionnez que la fenêtre se rétrécit automatiquement lorsqu'un consonne apparaît, ce qui garantit un temps linéaire.

---

## Pièges communs et comment les éviter

Piège
- Oui.
Autres **L'utilisation d'un ensemble qui se déplace entre les sous-chaînes**= Effacer l'ensemble à l'intérieur de la boucle extérieure ou utiliser un ensemble frais à chaque fois. Autres
**Réinitialiser la boucle intérieure sur la première consonne, mais pas réinitialiser l'ensemble**. Autres
Autres **Compilant la même fenêtre à plusieurs reprises**.Dans la solution optimisée, après avoir rétréci le pointeur gauche, la fenêtre ne contient plus les cinq voyelles – pas de duplicata. Autres
**Off‐by‐one erreurs sur les indices**=Démarrer la boucle externe à `i <= n - 5` parce qu'une sous-chaîne valide nécessite au moins cinq caractères. Autres
**Ignorant que les voyelles peuvent réapparaître après un consonant** Autres

---

- Oui. Comment pratiquer davantage

1. **Custom Test Generator** – Écrire un script qui génère des mots aléatoirement avec des longueurs de 100 à 200 et compte le résultat attendu en utilisant la force brute. Comparer les deux solutions.
2. **Edge Case Library** – Magasinez des chaînes comme `"aeiouaeiou"` ou `"abcde"` pour vérifier les nombres.
3. ** Expliquez l'algorithme à un ami** – L'enseignement vous force à penser à la clarté et aux conditions de bord.

---

Les pensées finales

> Ce problème est une excellente façon de présenter votre jeu de compétences algorithmiques tout en gardant le code succinct.
> La solution de fenêtre coulissante est non seulement la plus rapide, mais aussi la plus propre – une réponse parfaite à poser lors d'une véritable interview.

---

Liste de contrôle à emporter

- [ ] Comprendre les contraintes : *contitueux* → fenêtre coulissante.
- [ ] Maintenir les fréquences voyelles dans un tableau pour les vérifications O(1).
- [ ] Réinitialisez la fenêtre lorsque vous rencontrez un consonne.
- [ ] Plongez à gauche tant que nous avons encore les cinq voyelles ; cela garantit que chaque sous-chaîne est comptée exactement une fois.

---

Tu en veux plus ?

- **Explorer**: *La plus longue sous-chaîne contenant les cinq voyelles*.
- **Lire**: billet de blog sur la technique à deux points.
- **Pratique**: Codewars

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---