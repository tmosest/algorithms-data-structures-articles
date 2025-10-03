---
Titre: LeetCode 527. Abréviation de mot - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 527. Abréviation de mots – LeetCode dur
### Une solution complète et multilingue (Java-Python C++) + SEO-Optimized Blog Post

---

TL;DR
- **Objectif** : Retournez l'abréviation unique la plus courte pour chaque mot dans une liste de mots distincts.
- **Idée clé**: Grouper les mots par leur abréviation *initiale*, puis construire une trie **préfixe** pour chaque groupe pour trouver la longueur minimale de préfixe unique.
- **Complexités**:
- Temps – **O(--)word)** (linéaire dans le nombre total de caractères).
- L'espace – **O(... ..word)** pour les nœuds triés.

Les sections suivantes donnent une explication étape par étape et fournissent un code prêt à la copie en **Java**, **Python** et **C++**. Après le code, un court article de style blog explique le problème, les compromis et les idées favorables à l'entrevue.

---

Récapitulation des problèmes (Code de bord 527)

Étant donné un tableau de chaînes distinctes `words`, pour chaque mot nous devons produire son abréviation minimale suivant ces règles:

1. **Abréviation initiale**:
`first_lettre + (len - 2) + last_lettre "
(si l'abréviation n'est pas plus courte que le mot, garder le mot inchangé).

2. **Résolution de validation** :
Si deux mots partagent la même abréviation, **extendez le préfixe** de chacun par un seul caractère et recalculez l'abréviation.
Répétez jusqu'à ce que chaque abréviation soit unique.

Exemple
Texte
mots = ["comme", "dieu", "interne", "moi", "internet", "intervalle", "intensité", "face", "intrusion"]

Sortie = ["l2e", "dieu", "interne", "moi", "i6t", "intervalle", "inte4n", "f2e", "intr4n"]
«» "

---

Algorithme de haut niveau

1. ** Calculez l'abréviation initiale** pour chaque mot.
2. **Les mots de groupe qui entrent en conflit** (c.-à-d. qui partagent la même abréviation).
3. Pour chaque groupe:
1. Construisez une trie **préfixe** à partir de la partie suffixe de chaque mot (à partir du deuxième caractère).
2. Pour chaque mot du groupe, marchez le trie jusqu'à ce que nous atteignions un noeud avec le "compte == 1".
3. La profondeur de ce nœud nous indique combien de caractères nous devons garder dans le préfixe.
4. Recalculer l'abréviation avec cette nouvelle longueur de préfixe.
4. Retournez les abréviations finales dans l'ordre original.

---

Mise en œuvre du code

Ci-dessous sont trois solutions idiomatiques pour le même problème, une en **Java**, **Python** et **C++**.

> **Astuce** : Toutes les implémentations partagent la même logique de base : *groupe → trie → longueur de préfixe unique*.

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
// Trie noeud utilisé pour chaque groupe
classe statique privée TrieNode {
TrieNode[] enfants = nouveau TrieNode[26];
int count = 0; // combien de mots passent par ce nœud
}

// Aide à construire l'abréviation
chaîne statique privée abbrev (mot de chaîne, préfixe intLen) {
int n = mot.longueur();
si (n - prefixLen <= 3) retourner mot; // abréviation pas plus courte
retour word.substring(0, prefixLen + 1) + (n - prefixLen - 2) + word.char À (n-1);
}

liste publique<String> motsAbréviation(liste<String> mots) {
int n = mots.size();
Chaîne[] ans = nouvelle chaîne[n];

// Étape 1: groupe par abréviation initiale
Carte<String, liste<int[]>> groupes = nouvelle HashMap<>(); // valeur: {index, prefixLen}
pour (int i = 0; i < n; i++) {
Chaîne w = words.get(i);
Chaîne abbr = abbrev(w, 0);
groups.computeIfAbsent(abbr, k -> new ArrayList<>())add(new int[]{i, 0});
}

// Étape 2: traiter chaque groupe séparément
pour (Liste <int[]> groupe : groupes.valeurs() {
si [groupe.size()] 1) { // unique déjà
int idx = groupe.get(0)[0];
[idx] = abbrev(words.get(idx), 0);
poursuivre;
}

// Construire la trie à partir du deuxième caractère vers l'avant
TrieNode root = nouveau TrieNode();
pour (int[] paire : groupe) {
Chaîne w = words.get(pair[0]);
TrieNode cur = racine;
pour (int pos = 1; pos < w.length() - 1; pos++) { // exclure le dernier char
int c = w.charAt(pos) - 'a';
si (cur.children[c] == nul) cur.children[c] = nouveau TrieNode();
cur = enfants[c];
le nombre ++;
}
}

// Trouver un préfixe unique minimal pour chaque mot
pour (int[] paire : groupe) {
Chaîne w = words.get(pair[0]);
TrieNode cur = racine;
préfixe int = 1; // commencer par le premier caractère
pour (int pos = 1; pos < w.longueur() - 1; pos++) {
Si (cur. compter) 1) pause; // unique
int c = w.charAt(pos) - 'a';
cur = enfants[c];
préfixe++;
}
ans[pair[0]] = abbrev(w, préfixe - 1);
}
}

retour Arrays.asList(ans);
}
}
«» "

# # # # # #

'`python
de collections importer par défautdict
de taper l'importation Liste

Classe TrieNode:
__slots__ = ("enfants", "compte")
def _init_(self):
l'enfant = [Aucun] * 26
total = 0

Solution de classe:
def _abbrev(self, mot: str, prefix_len: int) -> str:
n = len(mot)
si n - prefix_len <= 3:
retour du mot
retourner mot[:prefix_len + 1] + str(n - prefix_len - 2) + mot[-1]

def wordsAbréviation(self, words: List[str]) -> List[str]:
n = len(mots)
ans = [Aucun] * n

# Indices de groupe par abréviation initiale
groupes = defaultdict(list)
pour idx, w en énumération(mots):
groupes[self._abbrev(w, 0)].append(idx)

pour groupe en groupes.valeurs():
si len(groupe)] 1 :
idx = groupe[0]
ans[idx] = self._abbrev(words[idx], 0)
poursuivre

# Construire le tri
racine = TrieNode()
pour idx dans le groupe:
w = mots[idx]
noeud = racine
pour ch in w[1:-1]: # Sauter le premier et le dernier char
c = ord(ch) - 97
si le noeud.enfants[c] n'est pas:
enfants[c] = TrieNode()
noeud = noeud.enfants[c]
nombre de nœuds += 1

# Trouver une longueur de préfixe unique
pour idx dans le groupe:
w = mots[idx]
noeud = racine
préfixe = 1
pour ch in w[1:-1]:
en cas de nœud. Nombre de personnes 1 :
pause
noeud = noeud.enfants[ord(ch) - 97]
préfixe += 1
[idx] = auto._abbrev(w, préfixe - 1)

retour et
«» "

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct TrieNode {
tableau <TrieNode*, 26> enfant{};
cnt = 0;
TrieNode() { enfant.fill(nullptr); }
};

solution de classe {
public:
chaîne abbrev(const string& w, int prefixLen) {
int n = w.size();
si (n - préfixeLen <= 3) retour w;
retour w.substr(0, prefixLen + 1) + to_string(n - préfixeLen - 2) + w.back();
}

vecteur<string> motsAbréviation(vecteur<string>& mots) {
int n = mots.size();
vecteur<chaîne> ans(n);

// Indices de groupe par abréviation initiale
non ordonné_map<string, vector<int>> les groupes;
pour (int i = 0; i < n; ++i) {
groupes[abbrev(words[i], 0)].push_back(i);
}

pour (auto &kv : groupes) {
&grp = kv.seconde;
Si [grp.size()] 1) {
[grp[0]] = abbrev(mots[grp[0]], 0);
poursuivre;
}

// Construire un trie pour ce groupe
TrieNode *root = nouveau TrieNode();
pour (int idx : grp) {
TrieNode *node = racine;
const chaîne &w = mots[idx];
pour (size_t pos = 1; pos + 1 < w.size(); ++pos) { // exclure le dernier char
c = w[pos] - 'a';
si (!node->child[c]) node->child[c] = nouveau TrieNode();
noeud = noeud->enfant[c];
++noeud->cnt;
}
}

// Trouver un préfixe unique minimal pour chaque mot
pour (int idx : grp) {
TrieNode *node = racine;
const chaîne &w = mots[idx];
préfixe int = 1; // premier caractère
pour (size_t pos = 1; pos + 1 < w.size(); ++pos) {
si (noeud->cnt) 1) pause; // unique
noeud = noeud->enfant[w[pos] - 'a'];
++préfixe;
}
ans[idx] = abbrev(w, préfixe - 1);
}
// (Dans le code de production, nous supprimerions tous les nœuds attribués.)
}

le retour des an;
}
};
«» "

> **Note**: Dans la version C++, vous pouvez réutiliser un pool global de trie ou utiliser des pointeurs intelligents pour éviter les fuites de mémoire dans une interview du monde réel.

---

Analyse de complexité

Langue Heure Espace
- C'est quoi ?
* * * * * * * * * * * *
"Python" **O(=)Mot****
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

`==word== nombre total de caractères dans la liste des entrées.
Parce que chaque caractère est visité un nombre constant de fois, l'algorithme est effectivement linéaire.

---

Cas et pièges

Scénario Que regarder
-- -- -- -- -- -- -- -- --
La boucle suffixe ('pour ch in w[1:-1]') exécute zéro fois – trie reste vide. L'algorithme fonctionne toujours parce que la taille du groupe sera `1`. Autres
Autres Les mots très courts (`len <= 3`) Autres
Autres Tous les mots partagent la même abréviation.La profondeur de trie sera la longueur du mot – chaque mot finit inchangé. Autres
Autres Mots avec des caractères médians répétés. Autres

---

D'après une perspective d'entrevue

Aspect du bien
- C'est quoi ?
**Le choix de la structure des données**= Trie donne *exact* longueur minimale du préfixe en O(1) par mot. L'utilisation d'une comparaison naïve par paire serait O(k2=word=) – inacceptable pour 100 + mots. Oublier de supprimer les nœuds trie (fuite mémoire C++) ou utiliser trop de profondeur de récursion peut planter le programme. Autres
**Temps et espace linéaires – bien dans les limites de LeetCode. Si vous deviez construire un trie pour *tous* mots à l'échelle mondiale, vous avez gaspillé de l'espace; le regroupement garde d'abord le trie petit. Autres Si vous stockez l'ensemble de la chaîne suffixe au lieu de construire un trie, vous allez perdre le temps. Autres
**Readability**=Javas classes internes statiques et `calculer SiAbsent` faire le code compact. Le python `_slots__` réduit les frais de mémoire mais est facultatif. C++ pointer gymnastique peut être difficile à lire; envisager d'utiliser `unique_ptr` ou un vecteur de nœuds. Autres
**Take-away d'interview**= Montrez que vous pouvez *grouper* d'abord, puis *localiser* la logique de résolution de collision à un tri. Éviter un tri monolithique pour tous les mots – il sera difficile de déboguer et pourrait faire sauter la pile. N'oubliez pas de gérer la règle "pas plus court" tôt ; sinon vous générerez des chaînes plus longues que nécessaire. Autres

---

## Đ Blog-Style Write-up

> **Titre**: *Code de cap 527 – Abréviation de mots: Une approche trié en Java, Python et C++ *
> **Mots clés**: LeetCode Word Abréviation, Leetcode 527 solution, Java Python C++ algorithme, interview, trie, abréviation de chaîne

---

### Code Leet 527 – Abréviation verbale : Une plongée profonde de style Blog

C'est vrai. 1. Contexte problématique
Le défi **Word Abréviation** vous demande de compresser une liste de mots distincts dans leurs abréviations uniques les plus courtes. Il combine la manipulation de chaîne** avec la résolution de collision**, un thème d'interview commun. La maîtrise de ce problème montre que vous pouvez :

- Oui. Pensez à *identifications uniques minimales*.
- Utilisez un préfixe ** pour découvrir le plus petit préfixe distinctif.
- Mettre en oeuvre un algorithme qui soit à la fois efficace dans le temps** et conscient de la mémoire**.

C'est vrai. 2. Aperçu général
Commencez par l'abréviation *naïve* («premier + len‐2 + dernier»). Si deux mots s'opposent, la seule façon de les différencier est de **extendre le préfixe** jusqu'à ce que les préfixes divergent. Un trie construit sur le suffixe (caractères 2...n‐1) est parfait pour cela: chaque noeud garde un compteur de combien de mots passent par lui, donc le premier noeud avec "compte". 1` nous indique la longueur minimale de préfixe requise.

C'est vrai. 3. Pourquoi une trie?
Autres Pourquoi des alternatives
C'est pas vrai.
**Longueur exacte du préfixe** dans *O(profondeur)*. Autres
**Space‐efficace** lorsque les tailles de groupe sont petites. Tableau plat de mots → O(k2 n). Autres
**Natural pour la logique du préfixe de l'extend** – chaque étape correspond à un déplacement vers le bas. Comparaison récursive des cordes → O(k2 n). Autres

C'est vrai. 4. Conseils de mise en oeuvre pour les entrevues

Motif
- Oui.
**Grouper par abréviation initiale d'abord** Autres
**Utilisez un `TrieNode` avec un tableau de 26 pointeurs** Autres
**Poignez la règle de "pas plus court" tôt** Autres
Autres **Nettoyez la trie après chaque groupe** (C++)= Prévient les fuites de mémoire; en Java/Python GC s'en occupe. Autres
**Return results in original order** Autres

C'est vrai. 5. Prolongation possible des entrevues

- ** Optimisation de l'espace**: Au lieu d'un tri complet, gardez un tableau de compteur par groupe et recherchez binaire la longueur minimale du préfixe.
- **Grand alphabet** : Remplacer `char‐to‐index` par `unordered_map` ou `unordered_set` si les caractères peuvent être un point de code Unicode.
- **Groupes parallèles**: Traiter chaque groupe en parallèle (Java Streams, Python `concurrent.futures`, C++ `std::async`) pour réduire le temps d'exécution sur les machines multicore.

---

À emporter

La stratégie *group → trie → prefix* unique donne une solution linéaire propre au LeetCode 527. Il présente :

- **Une meilleure compréhension des cordes et des suffixes**.
- **Utilisation efficace de la structure des données de Trie** pour préfixer la discrimination.
- ** Séparation nette des préoccupations** (aide à l'abréviation, regroupement, construction de trie, recherche préfixe).

Copiez-collez les extraits de code ci-dessus dans votre IDE, exécutez les tests d'échantillon, et vous serez prêt à accepter ce problème lors de toute entrevue de codage. Bon codage ! *