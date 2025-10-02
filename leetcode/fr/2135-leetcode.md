---
titre: LeetCode 2135. Compter les mots obtenus après avoir ajouté une lettre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

## Code de Leet 2135 – Tailler les mots obtenus après l'ajout d'une lettre

> **Tag**: "Moyen" , "Hashing" , "Bitmask" , "Interview"

> **Complexité**:
> *Temps*: **O(n + m + 26 · maxLen)** → pratiquement **O(n + m)**
> *Espace*: **O(n)** pour le jeu de hachages des masques de mots de départ.

---

Récapitulation des problèmes

Vous recevez deux tableaux :

"startWords" "cibleWords" Autres
- C'est quoi ?
"["ant", "act", "tack"]`"["tack", "act", "acti"]` Autres

Pour chaque mot cible, vous pouvez :

1. **Ajouter** *une* nouvelle lettre minuscule **non déjà présente** dans le mot.
2. **Réorganiser** les lettres arbitrairement.

Vous devez décider combien de mots cibles peuvent être produits à partir de *any* start word en utilisant les deux étapes ci-dessus.

**Note :** Les mots de départ ne sont ** jamais modifiés** – ils ne servent que de sources.

---

C'est vrai. Aperçu clé: Bit-Masking

Tous les mots se composent de * lettres minuscules distinctes*.
Nous pouvons représenter chaque mot comme un entier de 26 bits:

«» "
bit 0 → lettre 'a'
bit 1 → lettre 'b'
...
bit 25 → lettre 'z '
«» "

* Exemple: `"acte"` → bits 0 (a), 2 (c), 19 (t) → masque `1<<0=1<<2=1<<19`.

Avec cette représentation :

* Un mot **start** devient un masque que nous stockons dans un `HashSet<Intégrer>`.
* Pour un mot **cible** nous calculons son masque "tMask".
Supprimer un caractère `c` équivaut à basculer le bit de `c` off:
"Java
int prevMask = tMask ^ (1 << (c - 'a'));
«» "
Si `prevMask` existe dans le jeu de mots de départ, le mot cible est accessible.

Parce que chaque mot contient au plus 26 lettres, la boucle intérieure (enlevant chaque lettre) tourne au plus 26 fois – négligeable.

---

C'est vrai. Les bonnes

Pourquoi il brille
- Oui.
**O(1) lookup** – `HashSet` donne un test d'adhésion à temps constant. Autres
Autres **Pas de tri** – le bit-masking est plus rapide que le tri de chaque chaîne. Autres
**Simplicité** – un entier par mot, arithmétique trivial. Autres
**Scalable** – fonctionne pour les tailles d'entrée maximales ('5·104' mots). Autres

---

C'est pas vrai. Les mauvais

Caveats
- Oui.
** Suppose des lettres distinctes** – le problème garantit cela, mais en général vous devez vérifier. Autres
**Débordement de masque** – en Java un `int` détient 32 bits, donc 26 bits sont sûrs. Dans les langues avec des ints plus petits, vous devez assurer la capacité. Autres
**Memory** – `HashSet<Integer>` des entrées de 50k est minuscule (~2 Mo), mais si la taille des entrées augmente considérablement, elle pourrait devenir une préoccupation. Autres

---

C'est vrai. L'Ugly

Pièges si vous n'êtes pas prudent
-- --------------------------------------------------
** Erreurs de conversion de caractères à bits** – erreurs hors-par-un (`'a'` → 0, pas 1). Autres
**Togging mauvais bit** – oubliant **unset** le bit (utiliser XOR, pas OR). Autres
**Double-compte** – casser après le premier match est crucial ; sinon vous gonflerez le compte. Autres
**Ignorer la règle de la lettre doit ajouter une lettre** – vous ne pouvez pas assortir un mot cible d'un mot de départ qui est déjà un anagramme (par exemple, "act" vs "act""). L'astuce d'enlèvement de masques garantit exactement qu'une lettre est retirée. Autres

---

Code complet

Ci-dessous sont **trois** solutions complètes, prêtes à compiler – Java, Python, C++.

> *Tous les trois utilisent la même idée de bit-masking et ont des caractéristiques de temps/espace identiques. *

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int wordCount(String[] startWords, String[] cibleWords) {
// 1/ 1/ Rédiger un ensemble de masques de début
Définir <integer> startSet = nouveau HashSet<>();
pour (String s : startWords) {
set.add(toMask(s));
}

nombre int = 0;
Pour chaque mot cible essayez de supprimer chaque lettre
pour (String t : cibleWords) {
tMask = toMask(t);
booléen ok = faux;
pour [charc : t.toCharArray()] {
Int enlevé Masque = tMask ^ (1 << (c - 'a'));
i (startSet.contient(suppriméMasque)) {
ok = vrai;
pause; // arrêt après le premier succès
}
}
si (ok) count++;
}
le nombre de retours;
}

// Aide : convertir la chaîne en masque 26 bits
int privé toMask (mot d'ordre) {
masque int = 0;
pour (char ch : word.toCharArray()) {
masque= 1 << (ch - 'a');
}
masque de retour;
}

// Pilote pour les tests rapides
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.wordCount(
nouvelle chaîne[]{"ant","act","tack"},
nouvelle chaîne[]{"tack","act","acti"}); // → 2
}
}
«» "

6.2 Python

'`python
Solution de classe:
Def mot Count(self, startwords: Liste[str], cible Mots: Liste[str]) -> Int:
# Construire un ensemble de masques entiers pour les mots de départ
start_set = {self.to_mask(s) pour s dans startWords}
nombre = 0

pour t dans la cible Mots:
t_mask = auto.to_mask(t)
# Essayez de supprimer chaque personnage une fois
pour ch in t:
supprimé = t_mask ^ (1 << (ord(ch) - ord('a')))
si supprimé dans start_set :
nombre += 1
Break # besoin d'un seul match

Nombre de retours

@staticmethod
def to_mask(mot: str) -> Int:
masque = 0
pour ch en mot:
masque= 1 << (ord(ch) - ord('a'))
masque de retour
«» "

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int wordCount(vector<string>& startWords, vector<string>& cibleWords) {
désordonné_set<int> démarrage Jeu;
pour (const string &s : startWords)
startSet.insert(toMask(s));

Int ans = 0;
pour (const string &t : cible Mots) {
tMask = toMask(t);
bool ok = faux;
pour (charc : t) {
int enlevé = tMask ^ (1 << (c - 'a'));
si (startSet.count(supprimé)) { ok = true; break; }
}
si (ok) ++ans;
}
le retour des an;
}

particulier:
int statique toMask(const string &w) {
masque int = 0;
pour (charc : w) masque= 1 << (c - 'a');
masque de retour;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et le mauvais de résoudre le leetCode 2135

> **Titre**: *=Cracking LeetCode 2135: Le bon, le mauvais, et le mauvais d'une solution bit-masque
> **Méta-Description**: Apprenez à résoudre le LeetCode 2135 -Couvercle de mots obtenus après l'ajout d'une lettre dans le temps O(n + m). Découvrez les pièges, les compromis et les secrets d'entrevue qui vous aideront à réussir votre prochaine entrevue de codage.

---

Introduction

Les entrevues aiment les problèmes qui testent *votre* capacité à **penser avec des ensembles** et **compresser des données**. LeetCode 2135 est l'un de ces puzzles de type "hash-set + bit-mask" qui apparaissent dans de nombreux pipelines de location, en particulier pour les entreprises qui apprécient la clarté algorithmique (par exemple, Google, Amazon, Microsoft).

Ci-dessous, nous traversons le processus de pensée **complète** – ce qui fonctionne, ce qui pourrait vous faire trébucher, et les erreurs subtiles qui pourraient vous coûter l'entrevue.

---

Aperçu du problème

> **Don** deux listes de mots, pouvez-vous générer chaque mot cible en *ajoutant* une nouvelle lettre et *scrambling* les lettres?
> **Objectif** : Comptez le nombre de mots cibles possibles à partir de tout mot de départ.

Les contraintes (= 50 000 mots, lettres distinctes) indiquent qu'une structure de recherche *fast* (comme un hachage) est l'outil approprié.

---

L'idée fondamentale – Bit-Masking

Pourquoi un masque ? *
- Chaque lettre minuscule à un peu.
- Distinct → un mot = un entier unique de 26 bits.
- Set adhésion est **O(1)**.

**Algorithme**
1. Convertir chaque mot de départ → `mask`, stocker dans `HashSet`.
2. Pour chaque mot cible :
- Calculez son masque "tMask".
- Pour chaque caractère "c" dans le mot:
«prevMask = tMask ^ (1 << (c - 'a'))».
Si `prevMask` existe → ce mot cible est accessible.

L'astuce XOR garantit *exactement une* lettre est supprimée – précisément ce que le problème exige.

---

Les bonnes

- **Recherches à temps constant**: 50 k opérations *microsecondes*.
- **Pas de tri ou de manipulation des cordes** après la création du masque.
- ** Sémantique claire** : un entier par mot = débogage plus facile.
- **Scales**: 5 × 104 mots → < 2 Mo de mémoire, < 0,1 s d'exécution dans la plupart des langues.

---

Les mauvais

- ** Suppose des lettres distinctes** – si jamais vous réutilisez ce modèle sur des chaînes générales, vous devez vérifier l'unicité.
- **Limites linguistiques** – un entier de 26 bits est sûr en Java's 32-bit `int`, mais vous devez confirmer la largeur du type de données en C++/Rust/Go.
- **Hash au-dessus** – `HashSet` est un peu plus lourd qu'un tableau simple; pas un problème ici mais attention pour 106 ensembles de données de taille.

---

La moche

- ** Erreurs hors-par-un** lors de la cartographie `'a` → bit 0.
- **Contrôler l'utilisation de XOR** – basculer un peu sur (`=`) au lieu de s'éteindre (`^=`).
- **Double comptage** – ne pas « casser » après le premier succès gonfle la réponse.
- **Missinterpréter la règle « Add one letter »** – un anagramme d'un mot de départ est *not* autorisé; l'enlèvement du masque vous garantit de toujours enlever une lettre.

---

Conseils de mise en oeuvre pour votre entrevue

1. **Écrire un petit assistant** `toMask()` – garder la logique de base propre.
2. **Tester les cas de bordure** localement :
Texte
début = ["a", "ab", "abc"]
cible = ["abc", "abcd", "abcdx"]
«» "
Seuls les "abcd" et "abcdx" doivent être comptés.
3. ** Expliquez l'astuce XOR** à l'intervieweur ; c'est un excellent point de conversation.
4. **Afficher la complexité** à l'avant : temps O(n + m), espace O(n).
5. **Mention alternative** (trier les cordes, trier), puis argumenter pourquoi bit-masking gagne.

---

Faits saillants du SEO

- **Mots-clés**: *Code 2135, Nombre de mots obtenus après l'ajout d'une lettre, Bitmask, HashSet, Préparation d'entrevues, Structures de données*
- **Balises d'en-tête**: `h1` pour le titre, `h2` pour les sous-sections, `h3` pour les plongées plus profondes.
- **Rich Snippets**: Fournissez un extrait de code court, une table de complexité et une section "test rapide".
- **Backlinks**: Encouragez le lien à partir des pages de Structures de données à cet article.

---

La pensée finale

Résoudre le LeetCode 2135 avec bit-masking n'est pas seulement écrire du code rapide – c'est un **micro-cosme des meilleures pratiques d'entrevue**:

- **Utilisez la bonne structure de données** (`HashSet` pour l'adhésion).
- ** Contraintes de domaine de levier** (lettres distinctes, taille de l'alphabet).
- **Conservez le code propre** – fonctions d'aide, sorties précoces et noms de variables clairs.

En maîtrisant ce problème, vous démontrez :

- Compétence dans la manipulation par bits** – une compétence précieuse dans les entrevues de conception de systèmes.
- Capacité de **transférer les contraintes de problèmes en avantages algorithmiques**.
- L'état de préparation pour les "gotchas" qui voyagent souvent les candidats juniors.

**Takeaway:** Gâchez l'astuce bit-mask, articulez le bon/mauvais/mauvais, et vous brillez dans toute entrevue de codage qui comporte des questions de style LeetCode.

---