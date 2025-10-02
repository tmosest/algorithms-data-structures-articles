---
titre: LeetCode 3491. Numéro de téléphone Préfixe -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Numéro de téléphone Préfixe – Un code leet complet (Java / Python / C++)

> **Objectif**:
> • Résoudre le problème de LeetCode
> • Livraison de code prêt à la production en **Java**, **Python** et **C++**.
> • Ecrivez un billet de blog SEO optimisé qui couvre *le bon, le mauvais et le laid* du problème et met en valeur votre état d'esprit prêt à l'entrevue.

---

- Oui. 1. Aperçu du problème

**LeetCode 3491 – Préfixe du numéro de téléphone**
*Difficulté: Facile*

> **Input**: `String[] numbers` – un tableau de numéros de téléphone (seulement des chiffres, longueur ≤ 50).
> **Output**: `boolean` – `true` si **no** le numéro de téléphone est un préfixe d'un autre; sinon `false`.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
"["1", "2", "4", "3"]""""true" Aucun nombre n'est un préfixe d'aucun autre. Autres
"["001", "007", "15", "00153"] ""false"" "001" est un préfixe de "00153". Autres

**Contrôles* *

Valeur des contraintes
C'est pas vrai.
"2 <= nombres.longueur <= 50"
1 <= nombres[i].longueur <= 50 '
Autres Seuls les chiffres (`'0'``'9'`)

---

- Oui. 2. Pourquoi cela compte dans les entrevues

* Le préfixe vérifie la surface des problèmes réels : arbres de répertoires, autocomplet, annuaire téléphonique, tables de routeurs, etc.
* Démontre la compréhension de **la manipulation des chaînes**, **le tri** et éventuellement une structure de données **Trie**.
* Le problème est assez court pour être résolu en 10-15 min – parfait pour une vitrine rapide lors d'un appel de sélection.

---

- Oui. 3. Le bien

1. **Simplicité** – Une seule étape de tri + balayage linéaire.
2. **Déterministe** – Pas de randomisation ou de forte récursion.
3. **Scales** – Même pour les contraintes maximales, l'algorithme est instantané.
4. **Language-agnostique** – La même idée fonctionne dans n'importe quelle langue.

---

- Oui. 4. Le mal

Mauvaise explication
C'est pas vrai.
** Nécessite O(N log N)** temps Le tri domine – bien que trivial pour N ≤ 50. Acceptable; pour les ensembles de données énormes, une Trie est O (longueur totale). Autres
Autres **L'utilisation de l'espace**Le tri en place utilise un minimum d'espace supplémentaire, mais certaines langues (Python) copient la liste pendant `sort()`. Le tri en place ou l'utilisation d'une Trie en streaming élimine la copie. Autres
**Cas d'Edge**=Les chaînes vides ou les numéros dupliqués (non autorisés par les contraintes mais possibles dans un système réel). Pré-vérifier ou utiliser un `Set` pour dédoubler si nécessaire. Autres

---

- Oui. 5. L'Ugly

1. **Trie Implementation Bugs** – Oublier de vérifier les drapeaux en fin de mot ou mal gérer le nœud racine.
2. **Miss‐interpréter -préfixe** – Un écueil commun est de penser -substring - au lieu de -préfixe. (en milliers de dollars)
3. **Ignorer les contraintes** – Suringénierie avec des structures de données lourdes lorsque le problème est trivial.

> *Astuce*: Commencez par la solution de travail la plus simple; seulement si l'entrevue demande une structure de données plus efficace.

---

- Oui. 6. La solution gagnante (Démarrage + "démarrage avec")

L'observation :
Si un nombre est un préfixe d'un autre, cette paire sera adjacente après tri lexicographiquement.
Il suffit donc de comparer chaque élément avec le suivant.

**Complexité* *

Opération Temps Espace
- C'est quoi ?
Classer "O(N log N)" "O(1)" (en place)
Détecteur `O(N)` Autres
Total "O(N log N)" "O(1)" Autres

---

- Oui. 7. Mise en œuvre des références

#### 7.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe {
téléphone public booléenPréfixe(numéros String[]) {
// 1. Trier le tableau en place
Tableaux.sort(nombres);

// 2. Comparer chaque paire adjacente
pour (int i = 0; i < nombres.longueur - 1; i++) {
Chaîne cur = nombres[i];
Chaîne suivante = nombres[i + 1];
si (next.startsWith(cur)) {
retourner faux;
}
}
retour vrai;
}
}
«» "

*Pourquoi c'est prêt pour la production? *
* `Arrays.sort` est hautement optimisé.
* Utilise seulement le nombre minimal de variables.
* Pas de structures de données supplémentaires – faible empreinte mémoire.

---

7.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def phonePrefix(self, numbers: List[str]) -> bool:
nombres.sort() # O(N log N) en place
pour i dans la plage(len(nombres) - 1 :
si nombres[i + 1].commence avec(nombres[i]):
Retour Faux
retour Vrai
«» "

*Notes spécifiques au python*:
* La méthode `sort()` est en place.
* `startswith` est une routine C hautement optimisée.

---

### 7.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Téléphone de boolPrefix(vecteur<string>& numéros) {
tri(numbers.begin(), numbers.end()); // O(N log N)
pour (size_t i = 0; i + 1 < numbers.size(); ++i) {
const chaîne &cur = nombres[i];
const chaîne &next = nombres[i + 1];
si (next.compare(0, cur.size(), cur) == 0) // vérification préfixe
retourner faux;
}
retour vrai;
}
};
«» "

*Pourquoi "comparer"? *
* Il évite de créer une sous-chaîne et effectue un memcmp direct, qui est rapide.

---

- Oui. 8. Option facultative – Trie (Java)

Si vous êtes demandé de démontrer une structure de données plus avancée, une Trie est un ajustement parfait.

"Java
classe TrieNode {
TrieNode[] suivante = nouveau TrieNode[10];
booléen isEnd = faux;
}

solution de classe {
téléphone public booléenPréfixe(numéros String[]) {
TrieNode root = nouveau TrieNode();
pour (Num : chiffres) {
TrieNode cur = racine;
pour (charc : num.toCharArray()) {
int idx = c - '0';
si (cur.next[idx] == null) {
cur.next[idx] = nouveau TrieNode();
}
cur = cur.next[idx];
si (cur.isEnd) retourne false; // numéro existant est un préfixe
}
Si (cur.next[0] != NULLARYC cur.next[1] != NULLARY
cur.next[2] != null.
cur.next[4] != NULLARYC cur.next[5] != NULLARY
cur.next[6] != null.
cur.next[8] != null.
retourner false; // nouveau numéro est un préfixe de l'existant
cur.isEnd = vrai;
}
retour vrai;
}
}
«» "

*Traitement*: temps O(longueur totale) et espace O(longueur totale) par rapport à la solution de tri "temps O(N log N)" et espace O(1)".
Pour `N <= 50` et la longueur `<= 50`, l'approche de tri est généralement préférable.

---

- Oui. 9. Comment montrer ceci sur votre CV / Portfolio

1. **Résumé des problèmes**
* LeetCode 3491 – Préfixe du numéro de téléphone (Easy) en utilisant un algorithme de tri en deux étapes + balayage linéaire. (en milliers de dollars)

2. ** Faits marquants* *
* Solution optimisée: temps "O(N log N)", espace auxiliaire "O(1)". (en milliers de dollars)
* Implémenté en Java, Python et C++ démontrant la polyvalence du langage. (en milliers de dollars)

3. **Traitements clés**
* Illustré compréhension des préfixes de chaîne, propriétés de tri, et algorithmique temps-espace compromis. (en milliers de dollars)
* Préparé pour les questions d'entrevue de suivi sur les essais, l'analyse de la complexité et le traitement des cas de bord. (en milliers de dollars)

---

10. SEO-Optimized Blog Post

> **Titre**: *=Cracking LeetCode 3491 – Préfixe du numéro de téléphone: Java, Python, & C++ Solutions + Conseils d'entrevue
> **Meta Description**: *Master LeetCodeS Problème de préfixe du numéro de téléphone avec le code clair, prêt à la production en Java, Python et C++. Apprenez l'algorithme, la complexité et les stratégies de préparation des entrevues. *

---

#### 10.1 Introduction

Dans le paysage technologique concurrentiel d'aujourd'hui, les problèmes *LeetCode* sont un élément essentiel de la préparation des interviews. L'un de ces problèmes, le préfixe du numéro de téléphone** (ID 3491), teste votre compréhension de la manipulation de chaîne et de la pensée algorithmique. Dans cet article, nous traversons la **meilleure solution**, nous discutons des compromis **performance**, nous fournissons **clean code** en **Java**, **Python** et **C++**, et nous vous donnons des conseils pratiques **interview** pour impressionner les gestionnaires d'embauche.

---

### 10.2 Récapitulation des problèmes

*Avec un tableau de chaînes numériques, retourner `true` si aucune chaîne n'est un préfixe d'une autre. *
- **Exemples**
- "["1", "2", "4", "3"]" → `true`
- "["001", "007", "15", "00153"]` → `faux`

- **Constraints**
- 2 ≤ "nombres.longueur" ≤ 50
- 1 ≤ "numéros[i].longueur" ≤ 50
- Seuls les chiffres `'0'`–`'9'`

---

#### 10.3 La bonne, la mauvaise, la mauvaise, la marche

C'est vrai. Les bonnes
- **Straightforward**: Tri + comparer les paires adjacentes.
- **Fast**: Même pour la plus grande entrée, fonctionne en millisecondes.
- **Mémoire efficace**: O(1) espace supplémentaire.

C'est vrai. Les mauvais
- **Coût de récupération**: temps O(N log N) - négligeable ici, mais une préoccupation pour les listes énormes.
- **Connaissance des cas**: Il faut gérer les duplicates ou les chaînes vides si la spécification change.

C'est vrai. L'Ugly
- **Pièges communs**: Utiliser `substring` au lieu de `starts Avec ', mal gérer la racine dans les implémentations de Trie, ou oublier que le tableau trié garantit des relations de préfixe adjacentes.

---

#### 10.4 Le code gagnant

C'est vrai. Java

"Java
Importation de java.util.*;

solution de classe {
téléphone public booléenPréfixe(numéros String[]) {
Tableaux.sort(nombres);
pour (int i = 0; i < nombres.longueur - 1; i++) {
si (numbers[i + 1].startsWith(numbers[i]) retourne false;
}
retour vrai;
}
}
«» "

Python

'`python
Solution de classe:
def phonePrefix(self, numbers: List[str]) -> bool:
nombres.sort()
pour i dans la plage(len(nombres) - 1 :
si nombres[i + 1].commence avec(nombres[i]):
Retour Faux
retour Vrai
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Téléphone de boolPrefix(vecteur<string>& numéros) {
tri(numbers.begin(), numbers.end());
pour (size_t i = 0; i + 1 < numbers.size(); ++i) {
Si (nombres[i + 1].comparer(0, nombres[i].size(), nombres[i]) == 0)
retourner faux;
}
retour vrai;
}
};
«» "

---

### 10.5 Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Tri de `O(N log N) ́ ́ ́ ́ ́ ` ́ ́ ́ ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` Autres
Détecteur `O(N)` Autres
**Total****«O(N log N)»****«O(1)»** Autres

Avec `N ≤ 50`, cette solution est effectivement instantanée.

---

10.6 Quand utiliser un essai

Si l'entrevue demande spécifiquement un *Trie* (ou si vous avez affaire à des millions de numéros de téléphone), une Trie vous propose :

- **O(longueur totale)** temps – linéaire dans la somme de toutes les longueurs de chaîne.
- **Espace** proportionnel au nombre total de caractères.

Le compromis est ajouté à la complexité du code. Pour ce problème LeetCode, l'approche de tri reste la plus simple victoire.

---

### 10.7 Conseils d'entrevue

1. **Exposer les principaux points de vue**: Après tri, toute paire de préfixes sera adjacente. (en milliers de dollars)
2. **Discuse la complexité** à l'avant.
3. **Afficher la clarté du code** – utiliser des fonctions langagières et idiomatiques (`startsWith`, `compare`).
4. **Cas de bord d'adresse** : duplicata, chaînes vides (si la spécification se développe).
5. **Mention solutions alternatives** (Trie) et pourquoi vous avez choisi le plus simple.

---

10.8 Réflexions finales

La résolution du préfixe du numéro de téléphone démontre :

- Maîtrise des opérations à chaîne* *
- Utilisation efficace du tri**
- Capacité d'écrire **propre, code prêt à la production** en plusieurs langues

Ces compétences se traduisent directement par des tâches dans le monde réel – penser à des tables de routage, à l'authentification des utilisateurs ou à la conception d'index de base de données. Continuez à pratiquer, ajoutez cette solution à votre portefeuille, et vous serez prêt à aborder des énigmes d'entretien similaires avec confiance.

---

** Bon codage !**

---

11 ans. SEO Mots clés (pour méta tags et rubriques)

- LeetCode Numéro de téléphone Préfixe
- Solution de préfixe du numéro de téléphone
- Java LeetCode 3491
- Python LeetCode 3491
- C++ LeetCode 3491
- algorithme d'entretien pour les numéros de téléphone
- algorithme de vérification préfixe
- tri et début Avec
- Trie question d'entrevue
- Codage de la préparation des entretiens
- complexité de l'algorithme
- comparaison efficace des chaînes

Utilisez-les dans vos titres d'article, rubriques, et tout au long du poste pour attirer les demandeurs d'emploi et les gestionnaires d'embauche à la recherche d'exemples d'entrevues concrètes.