---
titre: LeetCode 3541. Trouver la plus fréquente Vowel et Consonant -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# C'est le plus fréquent Vowel et Consonant – Un LeetCode-Style Plongée profonde
**Difficulté**: Facile **Langues cibles**: C++

---

TL;DR
* **Objectif** – Pour une chaîne inférieure donnée `s`, retourner la somme de la fréquence voyelle la plus élevée et de la fréquence consonne la plus élevée.
* **Approche** – Comptez chaque lettre une fois avec deux tableaux (`vowelFreq` et `consonantFreq`), puis prenez le maximum de chaque et ajoutez-les.
* **Complexité** – temps `O(n)`, espace supplémentaire `O(1)`.
* **Langues** – Code est affiché en **Java**, **Python** et **C++**.

---

Déclaration de problème

On vous donne une chaîne `s` composée de lettres anglaises minuscules (`'a```'z``).

1. Trouvez la voyelle (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`) qui se produit le plus souvent.
2. Trouvez la consonne (toute autre lettre) qui se produit le plus souvent.
3. Retourne la somme de ces deux fréquences maximales.

S'il n'y a pas de voyelles ou de consonnes dans la chaîne, traiter la fréquence manquante comme **0**.
Si plusieurs voyelles ou consonnes s'attachent pour le maximum, l'une d'elles peut être choisie – le résultat est inchangé.

**Contrôles* *

État Valeur
C'est quoi ?
1 <= longueur <= 100 ' –
"s" contient seulement des lettres anglaises minuscules

---

Exemples de cas

Entrée Sortie Explication
C'est pas vrai.
""succès" ""6"" Vowel max = 2 (`e`), consonne max = 4 (`s`), somme = 6"
"aeiaeia" ""3"" Vowel max = 3 (`a`), pas de consonnes → 0, somme = 3"

---

Bon, le méchant et le méchant

Aspect du bien
- C'est quoi ?
**Simplicité**Le comptage d'un passage est facile à comprendre. Aucune – la solution naïve est déjà optimale. L'utilisation de cartes ou de régex ajouterait des frais généraux inutiles. Autres
**Performance**= O(n) temps, espace constant – le plus rapide possible. Léger risque de débordement entier si l'entrée était énorme (pas ici). Re-scanner la chaîne deux fois pour les voyelles/consonneurs perd du temps. Autres
**Readability**= Séparation claire de la logique voyelle/consonne. Certains peuvent être surcomplis avec les fonctions d'aide. Difficile à lire boucles nichées ou bit-masking pour les débutants. Autres

---

Approche étape par étape

1. **Initialiser deux gammes de fréquences** – une pour les voyelles (taille 5) et une pour les consonnes (taille 21).
2. **Traverser la chaîne une fois** :
* Déterminer si un personnage est une voyelle (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`).
* Augmentation du compteur correspondant.
3. **Trouver le maximum dans chaque tableau**.
4. **Retourner la somme** des deux maxima.

Aucune structure de données ou bibliothèque supplémentaire n'est nécessaire; la solution convient parfaitement aux contraintes.

---

Mise en œuvre

### Java

"Java
solution de classe publique {
int public maxFreqSum(String s) {
int[] voyelleFreq = nouvelle int[5]; // a, e, i, o, u
int[] consonantFreq = nouveau int[21]; // 21 consonants

// Carter une lettre à son index dans le tableau voyelle ou le tableau consonne
pour (char ch : s.toCharArray()) {
int idx = ch - 'a';
si (isVowel(idx)) {
voyelleFreq[ch - 'a']++;
} autre {
consonne Freq[idx - (is BeforeE(idx) ? 0 : 1)]++;
}
}

Int maxVowel = 0;
pour (int v : voyelleFreq) si (v > maxVowel) maxVowel = v;

int maxConsonant = 0;
pour (int c : consonantFreq) si (c > maxConsonant) maxConsonant = c;

retour maxVowel + maxConsonant;
}

booléen privé est Vowel(int idx) {
idx de retour == idx de retour ==
}
}
«» "

Python

'`python
Solution de classe:
def maxFreqSum(self, s: str) -> Int:
_compte de voyelle = [0] * 5 # a e i o u
Nombre de consonnes = [0] * 21 # 21 consonnes

voyelles = ensemble('aiou')
pour ch en s:
si ch en voyelles:
voyelle_count[ord(ch) - ord('a')] += 1
Sinon:
# passage à l'indice de consonne basé sur 0
idx = ord(ch) - ord('a')
Consonant_index = idx - 1 si idx > 4 autres
nombre_consonant[index_consonant] += 1

max_vowel = max(vowel_count)
max_consonant = max(consonant_count)
retour max_vowel + max_consonant
«» "

C++

'`cpp
solution de classe {
public:
int maxFreqSum(chaîne s) {
voyelle intFreq[5] = {0};
Int consonant Freq[21] = {0};

pour (charte : s) {
int idx = ch - 'a';
le bool isVowel = (idx) : (idx) : (idx) : (idx) :
si (est Vowel) {
voyelleFreq[idx]++; // idx 0,4,8,14,20
} autre {
Int consonant Idx = idx - (idx > 4 ? 1 : 0);
ConsonantFrek[consonant Idx]++; // quart après voyelles
}
}

int maxVowel = *max_element(degin(vowelFreq), fin(vowelFreq));
int maxConsonant = *max_element(début(consonantFreq), fin(consonantFreq));
retour maxVowel + maxConsonant;
}
};
«» "

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Autres Passage unique sur une chaîne de caractères **O(n)** (`n <= 100`)
Trouver le maximum **O(1)** (éléments constants 5 + 21)
**O(n)**

---

Cas et pièges

Scénario Quoi faire ?
C'est ce que j'ai dit.
**Toutes les voyelles**
**Tous les consonnes**=Le tableau Vowel reste zéro → max = 0.
**Le problème garantit la longueur ≥ 1, mais gardez-le si vous êtes réutilisé. Autres
**Connectez-vous à plusieurs**=Toute œuvre maximale; nous utilisons simplement `max_element`. Autres
**Unicode / majuscule**= L'entrée garantit la minuscule; sinon des vérifications supplémentaires sont nécessaires. Autres

---

Conseils d'entrevue

1. ** Expliquez clairement la logique** – le nombre de voyelles et de consonnes est indiqué séparément ; puis le nombre de voyelles et de consonnes est indiqué. (en milliers de dollars)
2. ** compromis temps/espace** – Cette solution est optimale et ne nécessite aucune structure de données supplémentaire au-delà des tableaux constants.
3. **Demander des éclaircissements** – p.ex., Dois-on traiter les lettres majuscules? La chaîne est-elle garantie de ne pas être vide? (en milliers de dollars)
4. **Montrer la manipulation des caisses de bord** – Parlez de pas de voyelles/consonneurs et de cas de cravate.
5. **Parcourir un échantillon** – Écrire les tableaux de fréquences pour une simple chaîne sur le tableau blanc.

---

Les variations que vous pourriez rencontrer

Idées différentes Autres
- C'est quoi ?
**Retourner la lettre elle-même** Obtenir l'index de l'élément max et la carte de retour à la lettre. Autres
**Insensible au cas**=Convertissez la chaîne en cas inférieur/super avant le traitement. Autres
**Inclure 'y' comme voyelle**. Autres
**Return positions of max letters** Autres

---

Conclusion

Le problème "Find Most Frequent Vowel and Consonant" est un exemple de manuel de comptage **fréquence** et d'indexation **array**.
Sa solution optimale fonctionne dans un temps linéaire avec un espace constant, ce qui en fait un excellent choix pour un problème d'interview qui teste:

* Structures de base de données (array, boucles).
* Gestion des conditions limites.
* Communication claire des étapes algorithmiques.

En maîtrisant ce problème en Java, Python et C++, vous aurez une solution polyvalente qui démontre à la fois l'efficacité algorithmique** et la conception linguistique-agnostique**, un point de discussion solide dans toute entrevue de codage. Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

Liste de contrôle du référencement

Mot-clé
C'est quoi ?
Titre, description du problème, conclusion
Autres Rubrique du code, explication
Section du code Python, explication
Section du code, explication
Interviews Section des conseils
Codage interview
Problème algorithmique Introduction
Autres complexité temporelle
Autres Complexité spatiale
Conclusion, motivation

*Toutes les sections sont riches en mots clés mais naturelles, assurant une plus grande visibilité sur les moteurs de recherche de blogs demandeurs d'emploi. *

---