---
titre: LeetCode 68. Justification du texte - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
No 68 – Justification du texte
**Temps O(n)**

---

Table des matières

Ce que vous apprendrez
- Oui.
Problème L'état exact du LeetCode
Les idées clés L'emballage de graisse, la distribution de l'espace, la gauche-justifiée dernière ligne
Algorithme Explication étape par étape
Code de Java, Python, implémentations C++ Autres
Les lignes à un mot, l'espace inégal divisé, la manipulation de la dernière ligne
Pourquoi la solution est optimale
Comment en parler sur un entretien technique
Comment cet article vous aide à trouver un emploi

---

Déclaration de problème

> **Avec** un tableau de mots `words` et une largeur maximale de ligne `maxWidth`, formater le texte de telle sorte que chaque ligne ait **exactement** `maxWidth` caractères et est entièrement (gauche et droite) justifié.
> Emballez des mots avidement : mettez autant de mots que possible dans chaque ligne.
> Insérez des espaces pour que chaque ligne atteigne la largeur requise.
> Pour une ligne avec *k* mots (`k > 1`), il y a des lacunes `k‐1`. Distribuez les espaces supplémentaires de manière uniforme : si les espaces ne peuvent pas être divisés de façon uniforme, les espaces **leftmost obtiennent un espace de plus**.
> La **dernière ligne** est justifiée à gauche et n'a pas d'espacement interne supplémentaire.
> **Contraintes**:
> - `1 ≤ longueur de mots ≤ 300`
> - `1 ≤ mots[i].longueur ≤ 20`
> - `1 ≤ maxLargeur ≤ 100`
> - Chaque longueur de mot ≤ `maxWidth "

---

Les idées clés

Idée Pourquoi c'est important
-- -- -- -- -- --
**Emballage grêle** Nous n'avons qu'à regarder la ligne actuelle; une fois qu'elle est pleine, nous passons à autre chose. Autres
Autres **Enregistrement de l'espace** Autres
Autres **Même la distribution** Autres
**Manipulation spéciale**= Dernière ligne (justifiée à gauche), lignes avec un seul mot (également justifiée à gauche). Autres

---

Algorithme

1. **Initialiser** `idx = 0` – pointeur au premier mot non encore placé.
2. Alors que `idx < words.longueur`:
1. **Déterminer la ligne** :
- `lineLen = mots[idx].longueur() "
- "dernier = idx + 1"
- Alors que `dernier < words.length` et `lineLen + 1 + words[last].length() ≤ maxWidth "
* `lineLen += 1 + mots[dernier].longueur() "
* `dernier++`
2. **Construire la ligne** :
"numWords = dernier - idx "
- `numSpaces = maxWidth - (lineLen - (numWords - 1))` (les espaces nécessaires pour atteindre la largeur)
- **Si** "dernier == mots.longueur" **ou** "numWords". 1' → *gauche-justifier*
* Ajoutez des mots avec un seul espace.
* Pad la fin avec des espaces.
- **Autres** → *justification complète*
* `espacesPerGap = numSpaces / (numWords - 1)`
* `extra = numSpaces % (numWords - 1)`
* Pour chaque mot (sauf le dernier) ajouter `espacesPerGap + (i < extra ? 1 : 0)` espaces.
3. **Avant** "idx = dernier".

3. Retournez la liste des lignes construites.

---

Code

Voici des solutions idiomatiques propres pour **Java 17**, **Python 3.10+** et **C++17**.

### Java

"Java
Importation de java.util.*;

classe publique TexteJustification {
Liste publique<String> completJustifier(String[] mots, int maxWidth) {
Liste<String> res = nouvelle liste de distribution<>();
int i = 0; // index de départ de la ligne actuelle
pendant que (i < mots.longueur) {
int lineLen = mots[i].longueur();
int last = i + 1;
// Trouvez le dernier mot qui correspond à la ligne
pendant que (dernier < mots.longueur &&
ligneLen + 1 + mots[dernier].longueur() <= maxWidth) {
ligneLen += 1 + mots[dernier].longueur();
dernier++;
}

StringBuilder sb = nouveau StringBuilder();
int numWords = dernier - i;
// Nombre d'espaces à distribuer
Total Espaces = maxWidth - (ligneLen - (numWords - 1));

// Dernière ligne ou ligne avec un seul mot => justifié à gauche
i (dernier) mots.longueur 1) {
pour (int j = i; j < last; j++) {
sb.append(mots[j]);
si (j < dernier - 1) sb.append('');
}
// Pad la fin avec des espaces
pour (int k = sb.longueur(); k < maxWidth; k++) sb.append(');
} autre {
// Entièrement justifié
espaces intérieurs PerGap = espace total / (numWords - 1);
int extraSpaces = totalSpaces % (numWords - 1);
pour (int j = i; j < last - 1; j++) {
sb.append(mots[j]);
// Les lacunes les plus à gauche obtiennent un espace supplémentaire
pour (int s = 0; s < espacesPerGap + (j - i < extraEspaces ? 1 : 0); s++)
sb.annexe(');
}
sb.append(words[last - 1]); // dernier mot, aucun espace de fuite
}
res.add(sb.àString());
i = dernier; // passer à la ligne suivante
}
retour rés;
}
}
«» "

**Points clés* *
- `lineLen` trace la somme des longueurs de mots **plus** un espace entre chaque mot.
Total Espaces est le nombre brut de blancs nécessaires après avoir soustrait les espaces uniques déjà présents.
- La boucle `alors que (dernier < mots.longueur &&...)` implémente l'emballage gourmand.

---

Python

'`python
de taper l'importation Liste

Solution de classe:
def fullJustify(self, mots: List[str], maxWidth: int) -> List[str]:
res = []
i = 0
alors que i < len(mots):
# Déterminer combien de mots correspondent à la ligne actuelle.
ligne_len = len(mots[i])
dernier = i + 1
pendant la dernière période < len(words) et line_len + 1 + len(words[last]) <= maxWidth:
ligne_len += 1 + len(mots[dernier])
dernier += 1

num_words = dernier - i
total_espaces = maxWidth - (ligne_len - (num_mots - 1)
ligne = ""

# Dernière ligne ou ligne avec un seul mot => à gauche.
if last == len(words) ou num_words == 1 :
ligne = ".join(mots[i:last])
ligne += < < > > * (max.
Sinon:
# Une justification complète.
espace_per_gap = total_espaces // (num_mots - 1)
extra = total_espaces % (num_mots - 1)
pour j dans la plage (i, dernier - 1):
ligne += mots[j]
Les lacunes les plus à gauche ont un espace supplémentaire.
ligne += " " * (espaces_per_gap + (j - i < extra))
ligne += mots[dernière - 1]

res.append(ligne)
i = dernier
retour res
«» "

---

C++

'`cpp
#incluez <vecteur>
#incluez <string>

solution de classe {
public:
std::vector<std::string> fullJustify(std::vector<std::string>& mots, int maxWidth) {
md::vecteur<std::chaîne> résultat;
taille_t i = 0;
pendant que (i < words.size()) {
// 1. Trouver la fin de la ligne
int lineLen = mots[i].size();
taille_t last = i + 1;
alors que (dernier < words.size() &&
ligneLen + 1 + mots[dernier].size() <= maxWidth) {
ligneLen += 1 + mots[dernier].size();
++dernier;
}

// 2. Construire la ligne
md::ligne de corde;
int numWords = dernier - i;
Total Espaces = maxWidth - (ligneLen - (numWords - 1));

if (dernier) mots.size() 1) {
// Justifié à gauche
pour (size_t j = i; j < last; ++j) {
ligne += mots[j];
si (j + 1 < dernière) ligne += ' ';
}
line.append(maxWidth - line.size(), ');
} autre {
// Justification complète
espaces intérieurs PerGap = espace total / (numWords - 1);
int extra = totalEspaces % (numWords - 1);
pour (size_t j = i; j < last - 1; ++j) {
ligne += mots[j];
espaces int = espaces (j - i < extra ? 1 : 0);
ligne.append(espaces, '');
}
ligne += mots [dernier - 1];
}

result.push_back(line);
i = dernier; // Passez à la ligne suivante
}
le résultat du retour;
}
};
«» "

---

Cas de bord et pièges communs

Autres Décision Pourquoi il importe de savoir comment la solution la gère
Il n'y a pas de lien entre les deux.
**Mot unique par ligne**=Aucun espace interne à distribuer. "numWords". 1` → chemin justifié à gauche. Autres
**Dernière ligne**= Doit être laissé-justifié indépendamment du nombre de mots.="dernier == words.size()` déclenche le chemin gauche-justifié. Autres
**Distribution inégale de l'espace**= Les lacunes les plus à gauche reçoivent un espace supplémentaire. `extra= totalSpaces % (numWords - 1)` et ajouter à gauche les espaces. Autres
**Word exactement égal à "maxWidth"** La boucle gourmande s'arrête avant d'ajouter un autre mot; la ligne devient à gauche. Autres
Autres **TrÃ ̈s longue ligne de mots courts** Calculs correctement gérer les grands "totalSpaces".

---

Analyse de complexité

Calcul métrique Résultat
- C'est quoi ?
Chaque mot est examiné une fois → "O(n)" "O(n)" où `n = mots.longueur` Autres
* Espace * Seulement quelques variables entières + liste de sortie

La solution est linéaire, la plus rapide possible car chaque mot doit être visité au moins une fois.

---

Conseils d'entrevue

1. **Exposer la décision cupide**: Nous continuons d'ajouter des mots jusqu'à ce que nous ne puissions pas rentrer dans le prochain. (en milliers de dollars)
2. **Afficher votre raisonnement pour la distribution de l'espace**: parlez de la division entière et du reste.
3. **Afficher la manipulation du boîtier**: lignes à mots simples, dernière ligne, espaces inégaux.
4. **Complexité**: Temps linéaire, espace auxiliaire constant. (en milliers de dollars)
5. **Afficher un croquis rapide** (lignes de dessin, trous, espaces) – il démontre une communication claire.

---

Bonus de référencement – Débarquer un emploi avec cet article

* ** Mots clés**: LeetCode Text Justification, Greedy Algorithm, Java Interview Question, Python Text Justification, C++ Text Justification, Full Justification, Interview Prep, Coding Interview, Technical Interview, Algorithm Design.
* **Description détaillée**: *Solve LeetCode (Hard) en Java, Python et C++. Apprenez un algorithme gourmand, la manipulation des cas de bord et des explications prêtes à l'entrevue. Déposez votre prochain travail technique !
* **En-têtes**: Utilisez H1 pour le titre, H2 pour les sections, H3 pour les sous-sections – Google aime la structure sémantique.
* ** Extraits de code**: Les blocs de code visibles aident les moteurs de recherche à reconnaître le contenu est un tutoriel.
* **Readability**: Points de balles, courts paragraphes, et le code surligné maintiennent les utilisateurs engagés → taux de rebond inférieur.

En affichant cet article, en le partageant sur des blogs de codage, ou en l'ajoutant à votre GitHub README, vous n'êtes pas seulement en train de pratiquer le codage – vous êtes aussi en train de montrer votre capacité à écrire des solutions propres et prêtes à l'entrevue en plusieurs langues.

---

** À emporter** : Un algorithme cupide concis, des maths d'espace soignés et une gestion robuste des cas de bord font de ce problème de Hard LeetCode une vitrine parfaite tant pour vos cliquets de codage que pour vos compétences en communication avec les interviews. Bon codage, et bonne chance pour le prochain entretien d'embauche!