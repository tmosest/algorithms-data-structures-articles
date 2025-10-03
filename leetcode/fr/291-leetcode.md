---
titre: LeetCode 291. Mot modèle II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Mot modèle II – Leetcode 291
C++** – Retraçage + Bijection
**SEO-optimized guide** pour vous aider à résoudre ce problème d'entrevue et de poser votre travail de rêve

---

Aperçu du blog (mots de référence)

- **Leetcode 291 Word Pattern II** – défi à cordes classiques
- **Solution de recul de Java** – code propre et prêt à la production
- **Python Word Pattern II** – récursion lisible avec des ensembles/dictes
- **C++** – STL non ordonné_map / non ordonné_set
- ** Bijection assortie de carton** – pourquoi l'unicité compte
- **Stratégie d'entretien d'emploi** – comment parler de ce problème dans un entretien technique
- **Complexité temporelle et spatiale** – O(n^m) dans le pire des cas, mais *pratiquement* rapide
- **Pièges communs** – Dupliquer la cartographie

> *Meta Description: *
> Maître Leetcode 291 – Mot modèle II. Préparez-vous avec les solutions de backtracking Java, Python et C++, l'analyse de complexité, les astuces et les points d'entretien. Parfaitez vos compétences en algorithme et impressionnez les gestionnaires d'embauche.

---

Récapitulation des problèmes

> **Modèle II**
> Compte tenu d'une chaîne de motif `pattern` et d'une chaîne `s`, déterminer si `s` peut être segmenté en une séquence de sous-chaînes non vides de telle sorte que chaque caractère de cartes `pattern` **bijectivement** (un à un) à une sous-chaîne.
> Contraintes : `1 <= pattern.longueur, s.longueur <= 20`, seulement lettres minuscules.

---

Une idée de haut niveau

1. **Backtracking** – Essayez chaque sous-chaîne possible pour chaque caractère de motif.
2. **Mapping (`HashMap / dict / unordered_map`)** – stocker la sous-chaîne choisie pour chaque caractère.
3. ** Set utilisé (`HashSet / set / unordered_set`)** – s'assurer **bijectivity**: pas deux caractères de motif partagent la même sous-chaîne.
4. **Élagage** – si le mapping actuel ne correspond pas au préfixe de `s`, backtrack immédiatement.

L'algorithme explore un arbre de possibilités; parce que la taille de l'entrée est minuscule (20), le pire cas exponentiel est acceptable.

---

Mise en œuvre du code

C'est pas vrai. Java (Suivi + ensembles)

"Java
Importer java.util. HashMap;
Importer java.util. HashSet;
Importer java.util. Carte;
Importer java.util. Jeu;

solution de classe publique {
mot public booléen PatternMatch(String pattern, String s) {
retour(s), 0, motif, 0, nouveau HashMap<>(), nouveau HashSet<>();
}

retour booléen privé(String s, int i, String pattern, int j,
Carte<Caracter, String> carte, Set<String> utilisée) {
// Base: les deux cordes entièrement consommées
si (i == s.length() && j == pattern.length()) retourne true;
// Mismatch: l'un consommé, l'autre non
i (i) s.length() ; j) pattern.length() ;

char c = pattern.charAt(j);

// La cartographie existante → doit correspondre exactement
si (map.contientKey(c)) {
Chaîne val = map.get(c);
si (!s.startsWith(val, i)) retourner faux;
retour(s, i + val.length(), motif, j + 1, carte, utilisé);
}

// Essayez chaque sous-chaîne possible pour ce personnage
pour (int k = i; k < s.longueur(); k++) {
Candidat à la chaîne = s.substring(i, k + 1);
si (utilisé.contient(candidate)) continue; // vérification de bijection

map.put(c, candidat);
utilisé.add(candidate);

si (piste(s), k + 1, motif, j + 1, carte utilisée) retourner true;

// Retour
carte.supprimer(c);
utilisé.remove(candidate);
}
retourner faux;
}
}
«» "

> **Pourquoi ça marche** – La profondeur de récursion est égale à "pattern.longueur()" (- 20). Chaque appel tente toutes les sous-chaînes possibles; le jeu `used` garantit qu'aucune carte de deux caractères de motif n'est utilisée pour la même sous-chaîne.

---

Python (récursion élégante)

'`python
def wordPatternMatch(pattern: str, s: str) -> C'est vrai.
def dfs(i: int, j: int, mapping: dict, used: set) -> C'est vrai.
# Conditions finales
Si i == len(s) et j == len(pattern):
retour Vrai
Si i == len(s) ou j == len(pattern):
Retour Faux

c = modèle[j]

# Déjà carte
si c dans la cartographie:
val = cartographie[c]
si ce n'est pas s.commence avec(val, i):
Retour Faux
retour dfs(i + len(val), j + 1, cartographie, utilisé)

Essayez chaque sous-chaîne possible
pour k (i, len(s)):
cand = s[i:k + 1]
si la cand est utilisée:
poursuivre
mapping[c] = cand
utilisé.add(cand)
si dfs(k + 1, j + 1, cartographie utilisée):
retour Vrai
del mapping[c]
utilisé.supprimer(cand)
Retour Faux

retour dfs(0, 0, {}, set())
«» "

> **Pythonic Highlights** – `s.startswith(val, i)` est un préfixe rapide; `set` assure la bijectivité en O(1).

---

C++ (STL, récursif)

'`cpp
solution de classe {
public:
bool wordPatternMatch(string pattern, string s) {
unordered_map<char, string> mp;
unordered_set<string> utilisé;
retour(s, 0, motif, 0, mp, utilisé);
}

particulier:
bool backtrack(const string& s, int i, const string& pattern, int j,
unordered_map<char, string>& mp, unordered_set<string>& used) {
si (i == s.size() && j == pattern.size() retourne true;
i (i) s.size() ;

char c = motif[j];
auto it = mp.find(c);

// Cartographie existante
si (it != mp.end()) {
const string& val = it->seconde;
si (s.compare(i, val.size(), val) != 0) retourner faux;
retour arrière(s, i + val.size(), motif, j + 1, mp, utilisé);
}

// Nouvelle cartographie : essayez toutes les sous-chaînes
pour (int k = i; k < s.size(); ++k) {
chaîne cand = s.substr(i, k - i + 1);
si (utilisé.count(cand)) continue;

mp[c] = cand;
utilisé.insérer(cand);

si (backtrack(s, k + 1, pattern, j + 1, mp, utilisé)) retourne true;

(c)
utilisé.erase(cand);
}
retourner faux;
}
};
«» "

> **C++ Efficience** – `s.compare(i, len, val)` effectue une comparaison rapide de sous-chaîne; `unordered_map / unordered_set` donne une recherche moyenne O(1).

---

La complexité temporelle et spatiale

- **Case la plus importante**:
- Chaque caractère de motif peut se mapper à l'une des sous-chaînes restantes.
- L'espace de recherche "O(n^m)" où `n = s.length()` et `m = pattern.length()`.
- Avec `n, m ≤ 20`, c'est pratiquement rapide (la plupart des branches sont taillées tôt).
- **Espace**:
- Pile de récursion `O(m)` + `O(m)` pour la cartographie + `O(m)` pour le jeu utilisé.
- Total: **O(m)** espace supplémentaire, négligeable pour les contraintes.

---

## -Cas de bord (Conseils d'entrevue)

Numéro
C'est quoi ?
**Cartographie en double** (`"abba"` → `"xyz"` pour `a` et `b`) Utiliser un ensemble *used* pour bloquer la réutilisation. Autres
**Substr(i, k-i+1)** N'oubliez pas l'index de fin inclusive `k`. Autres
La boucle commence à `i` et s'arrête à `len(s)-1`; `k-i+1 >= 1'.
**Déploiement de la pile**= Profondeur ≤ 20 → sûre en Java/Python/C++; si vous tombez dans des motifs plus profonds, convertissez-vous à une pile explicite. Autres
**Early tailler**= Si la cartographie ne correspond pas à la partie suivante de `s`, sautez le reste de la boucle. Autres

---

Points d'entrevue prêts à parler

1. ** Clarifier l'exigence de bijection* *
Chaque lettre doit correspondre à une sous-chaîne unique; aucune lettre ne peut partager le même bloc.

2. ** Expliquez votre stratégie de retour* *
J'assiste récursivement des sous-chaînes à des caractères, stockant l'assignation dans un dictionnaire, et immédiatement backtrack si le préfixe de la chaîne d'entrée ne correspond pas.

3. **Montrer comment vous manipulez la taille* *
En utilisant `startsWith`/`s.compare`, je peux détecter une inadéquation en temps constant, coupant des branches entières.

4. ** Débat sur la complexité**
*Le cas le plus intéressant est exponentiel, mais les contraintes de longueur le rendent extensible. Dans la pratique, l'algorithme fonctionne en millisecondes.

5. ** Optimisations facultatives**
- Mémoriser les paires `(i, j)` (programmation dynamique par rapport à l ' état).
- Pré-calculer les montants pour couper les branches plus rapidement.

---

## Résumé rapide des références

Langue de référence Structures de données clés Profondeur de récursion Vérification de la bijectivité
-- -- -- -- -- -- -- -- -- -- -- -- -- --
*Java *HashMap <Caracter,String>` + `HashSet<String>`" ≤ 20" `served.contains(candidate)` Autres
**Python**="dict" + `set"=" ≤ 20="cand in used` Autres
*C++**== `unordered_map<char,string>== + `unordered_set<string>=== ≤ 20==`used.count(cand)===

---

Le dernier Verdict

- **Correctness:** Chaque algorithme garantit une cartographie unique et couvre toutes les possibilités de partition.
- **Efficacité :** Pour les contraintes données, fonctionne confortablement dans les limites du temps.
- **Readability:** Le code Java est prêt à la production; le code Python est concis; le code C++ est compatible avec STL.
- **Interviewabilité :** Le problème est une grande vitrine de la récursion, du retour et de la gestion prudente de l'état, parfait pour une entrevue de haut niveau.

---

Prochaines étapes pour votre préparation d'entrevue

1. **Mettre en œuvre chaque version vous-même** – copie-colle n'a pas gagné de points.
2. **Donnez les cas d'essai fournis** plus *votre propre* cas de bord (par exemple, "pattern"a", "s"abcd").
3. **Exposer la contrainte de bijection** – une partie clé de l'énoncé du problème.
4. **Pratiquez une promenade** – narrez l'arbre de récursion, comment vous taillez les branches, et quand vous reculez.

Bon codage et bonne chance pour votre prochain entretien technique! C'est ce qu'il a dit