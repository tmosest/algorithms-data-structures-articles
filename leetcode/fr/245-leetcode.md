---
titre: LeetCode 245. Distance Word III la plus courte -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 245. Distance Word III la plus courte – Guide de solution complète (Java-Python-C++)

> **TL;DR** – Analysez la liste une fois, conservez deux indices (dernière vue de `word1` et `word2`), mettez à jour la distance minimale sur chaque match. Fonctionne dans l'espace *O(n*), dans l'espace *O(1)* et gère avec élégance le boîtier "Same-word".

---

Récapitulation du problème

> Avec une liste ** de chaînes** `wordsDict` et deux chaînes `word1` et `word2` (tous deux garantis pour apparaître dans la liste), retournez la distance **la plus courte** (dans les indices) entre toute occurrence de `word1` et `word2`.
> Les deux mots peuvent être identiques – dans ce cas nous voulons la plus petite distance entre **deux événements différents** de ce mot.

**Contrôles* *

Valeur
- C'est quoi ?
MotsDict.longueur1 ... 105
"MotsDict[i].longueur"
Autres Tous les mots sont en minuscules lettres anglaises.

**Exemples**

Entrée Sortie
C'est quoi ?
"["pratique", "makes", "parfait", "codage", "makes"]`, "makes"`, "codage"`
"["pratique", "makes", "parfait", "codage", "makes"]`, "makes"`, "makes"""

---

1. Approche: Scan à deux points (passe simple)

La façon la plus naturelle est un seul scan de gauche à droite tout en maintenant les ** positions les plus récentes** de chaque mot.

«» "
i1 = dernier index de word1 (initialement)
i2 = dernier indice de word2 (initialement +)
minDist = +
pour chaque index i en mots Numéro:
si mots[i] == mot1: i1 = i
si mots[i] == mot2:
i word1 == word2: i1 = i2 // nous avons besoin de l'événement précédent
i2 = i
minDist = min(minDist,=i1 -=i2=)
«» "

*Quand `word1 == word2`* nous devons **wap** les deux indices sur un succès pour nous assurer de comparer *deux positions différentes*.

**Pourquoi ça marche* *

- Oui. L'algorithme ne revient jamais plus d'une fois : chaque index est traité une fois, donc la complexité du temps est *O(n*).
- Oui. Seules les variables supplémentaires constantes sont utilisées → *O(1)* espace auxiliaire.
- Le cas de bord de la même mot est traité explicitement en échangeant les indices lorsque nous voyons le même mot.

---

2. Autres idées

L'approche La complexité Quand utiliser
C'est pas vrai.
**Pré-traiter toutes les positions dans une `Map<String, Liste<Intégrer>>'** puis calculer la différence minimale entre deux listes triées par fusion de deux points. Heure: *O(n)*; Espace : *O(n*) Quand vous devez répondre **de nombreuses requêtes** sur la même liste de mots – vous payez le coût une fois. Autres
**Fenêtre coulissante / programmation dynamique** – pas nécessaire ici.
**Recherche binaire** – aussi inutile parce que nous pouvons scanner une fois.

---

Code

Vous trouverez ci-dessous des solutions prêtes à la copie dans **Java**, **Python** et **C++**.
Chaque mise en œuvre suit la stratégie de balayage à deux points.

> **Note** – Les trois extraits sont des classes (ou des fonctions) de type LeetCode `Solution` et contiennent de brefs commentaires pour plus de clarté.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
public WordDistance(String[] wordsDict, String word1, String word2) {
// indices des dernières positions vues
int i1 = Integer.MIN_VALUE; // utiliser des valeurs extrêmes pour éviter les contrôles spéciaux
int i2 = entier.MAX_VALUE;
int minDist = entier.MAX_VALUE;

booléen même = mot1.equals(word2);

pour (int i = 0; i < mots Longueur dictée; i++) {
Chaîne w = motsDict[i];
si (w.equals(word1)) {
si (même) {
// même mot – traiter i1 comme l'événement précédent
i1 = i2;
}
i1 = i;
} sinon si (w.equals(word2)) {
i2 = i;
}

// Comparaison seulement lorsque les deux indices sont fixés
si (i1 != Integer.MIN_VALUE && i2 != Total.MAX_VALUE) {
minDist = Math.min(minDist, Math.abs(i1 - i2));
}
}
retour minDist;
}
}
«» "

> **Heure** – *O(n)*
> **Espace** – *O(1)*

---

Python

'`python
Solution de classe:
def le plus court WordDistance(
self, wordsDict: Liste[str], word1: str, word2: str
-> Int:
i1 = -10**9 # efficacement
i2 = 10**9 # efficacement
min_dist = 10**9
même = word1 == word2

pour idx, w en énumération(motsDict):
si w == mot1:
si même:
i1 = i2
i1 = idx
elif w == mot2:
i2 = idx

# Mettre à jour seulement si les deux indices ont été vus
i1 > -10**8 et i2 < 10**8:
min_dist = min(min_dist, abs(i1 - i2))

_dist de retour
«» "

> **Heure** – *O(n)*
> **Espace** – *O(1)*

---

C++

'`cpp
solution de classe {
public:
dans la plus courte WordDistance(vecteur<chaîne>& mots Dict, string word1, string word2) {
Int i1 = INT_MIN; // ---
int i2 = INT_MAX; // +-
int minDist = INT_MAX;
bool meme = word1 == word2;

pour (int i = 0; i < wordsDict.size(); ++i) {
const chaîne &w = mots Dict[i];
si (w == mot1) {
i1 = i2; // événement antérieur
i1 = i;
} sinon si (w == mot2) {
i2 = i;
}

Si (i1 != INT_MIN && i2 != INT_MAX) {
minDist = min(minDist, abs(i1 - i2));
}
}
retour minDist;
}
};
«» "

> **Heure** – *O(n)*
> **Espace** – *O(1)*

---

4. Résumé de la complexité

Pourquoi il s'agit d'une interview-Ready
- C'est quoi ?
Java (n) *O(1)*Utiliser uniquement des ints primitifs, pas de HashMap, rapidement sur une seule requête. Autres
Python () *O(n)* () *O(1)* () Même idée, plaque de chaudière minimale. Autres
*O(1)*= Fonctionne avec `vector<string>` et `std::string`. Autres

---

4. Bon / mauvais / mauvais – ce que chaque intervieweur aime

Catégorie Ce que nous évaluons Verdict
- C'est quoi ?
*Simplicité* – un passage, aucune structure de données auxiliaire, espace O(1) clair.
**Bad**= *Manipulation d'un cas* – beaucoup de gens oublient l'affaire « même mot » et finissent par avoir une réponse incorrecte (distance 0 ou indices négatifs).
**La lisibilité du code par rapport à la vitesse* – une solution naïve à deuxarraies (`i1`, `i2` stockée séparément et échangée lors d'un coup) peut sembler confuse si elle n'est pas commentée correctement.

> **À emporter :**
> - Écrire propre, le code commenté.
> - Garder toujours l'affaire « même mot » – c'est un piège d'entrevue classique.
> - Si vous avez besoin de répondre à de nombreuses questions, le pré-traitement est parfait; sinon, le mono-scan est la norme d'or.

---

5. Harnais d ' essai

Code de l ' essai
- C'est quoi ?
Autres Les trois langues sont les suivantes :
Autres Les trois langues sont les suivantes :
Autres Les trois langues sont les suivantes :

Vous pouvez coller ces cas de test dans l'IDE LeetCode ou votre environnement local pour confirmer.

---

6. Pourquoi les intervieweurs aiment cette question

- ** Fondamental**: Tests de compréhension de la traversée du réseau et de l'arithmétique de l'indice.
- **Connaissance des cas**: La situation du même mot est une pierre d'achoppement d'entrevue commune.
- **Versatile**: Les solutions en plusieurs langues montrent la résolution de problèmes langue-agnostiques.
La solution O(n) est efficace même pour la taille maximale d'entrée.

Si vous réussissez ce problème dans votre entrevue, vous démontrez :

- Maîtrise des compromis temps/espace**.
- Capacité d'écrire **code de bust** qui traite des cas spéciaux.
- Confort avec les signatures de classe/fonction **LeetCode-style**.

---

7. Performance et compromis

Valeur métrique Pourquoi ça compte
- C'est quoi ?
**Temps** **O(n)* (= 105 ops)= Assez rapide pour les pipelines de données de qualité de production. Autres
**L'espace**= *O(1)*=Tenir l'empreinte mémoire minuscule – critique pour les appareils limités. Autres
**Readability** Autres
**Pre-processing Map**= Extra *O(n)* memory== Bon pour les scénarios de requête par lots, mais pas pour une seule requête. Autres

---

8. Résumé du SEO

- **Mots clés**: *Distance de mot la plus courte III LeetCode*, *solution de Java*, *solution de Python*, *solution de C++*, *deux pointeurs*, *question d'entrevue*, *prep d'entrevue d'emploi*, *entrevue de structure de données*, *solution de O(n)*.
- **Titre**: 245. Distance Word III la plus courte – Java / Python / C++ Solutions & Guide d'entrevue
- **Description de la méta** (=160 caractères): LeetCode245 – Distance de Word III la plus courte avec code optimum O(n) Java, Python et C++. Apprenez l'astuce à deux pointeurs, la manipulation des cas de bord et les conseils d'entrevue. (en milliers de dollars)

Utilisez ces extraits dans votre CV ou GitHub pour mettre en valeur votre capacité à résoudre efficacement les problèmes d'entrevue classiques.

---

9. Pensées finales

Le balayage à deux points est la réponse **canonique** pour ce problème de LeetCode.
Si vous préparez des entrevues de codage, assurez-vous de pouvoir :

1. ** Expliquez l'algorithme** en anglais clair.
2. **Mise en œuvre dans votre langue préférée** (Java, Python, C++).
3. **Discute le cas de bord** où les deux mots sont identiques.
4. **Comparer les compromis** avec une carte de prétraitement lorsque de nombreuses requêtes sont attendues.

La maîtrise de ce problème simple et subtil va renforcer votre confiance pour d'autres questions d'entrevue de distance/paire la plus proche, comme *Shortest Unlowful Subsequence*, *First Missing Positive* et bien d'autres encore.

Bon codage – et bonne chance pour votre prochaine entrevue! C'est ce qu'il a dit