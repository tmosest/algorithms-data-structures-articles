---
titre: LeetCode 1948. Supprimer les dossiers dupliqués dans le système -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1948. Supprimer les dossiers dupliqués dans le système
**Hard – LeetCode 1948**
> **Délai :** 2 s
> ** Limite de mémoire :** 256 Mo

---

Récapitulation des problèmes

Vous recevez une liste de chemins de dossiers absolus.
Une structure de dossier est *Identique* si l'ensemble des dossiers enfants **et la structure imbriquée** de ces enfants sont les mêmes (les noms de dossier eux-mêmes ne doivent pas être égaux).

Si deux (ou plus) dossiers sont identiques, *deux* dossiers ** et tous leurs sous-dossiers** sont marqués pour suppression.
Le système de fichiers supprime tous les dossiers marqués **une fois** – tous les nouveaux dossiers identiques qui apparaissent *après* la suppression ne sont pas supprimés.

Retournez la liste des chemins qui survivent après le passage de suppression unique.

> **Input** – <Liste<Liste<String>> chemins "
> **Output** – «Liste<Liste<String>>» (ordre n'a pas d'importance)

---

Stratégie de haut niveau

1. **Construire un arbre** (une *trie* des noms de dossiers) à partir des chemins d'entrée.
2. **DFS après l'ordre** pour calculer une *signature* pour chaque noeud qui décrit son sous-arbre.
3. Compter les cas de chaque signature.
4. **Deuxième DFS** – marchez à nouveau l'arbre; si une signature de nœud survient plus d'une fois, sautez ce nœud (et tous ses enfants).
5. Recueillir les chemins survivants.

L'astuce est la *signature* – une chaîne déterministe qui peut être comparée dans le temps `O(1)`.
Nous trions les signatures des enfants avant de concaténer pour rendre l'ordre non pertinent (la structure est un ensemble, pas une séquence).

---

Pourquoi ça marche ?

Étape Ce que nous obtenons Pourquoi ça compte
-- -- -- -- -- -- --
**Construction de l'arbre**= Chaque dossier est un nœud; les bords représentent le parent → enfant. Donne une structure de données propre à traverser. Autres
**Signature**="signature = concat(sorted(childName +"(" + childSig + ")")"=" Deux sous-arbres identiques produisent des signatures identiques. Autres
**Countant**== `Map<signature, count>=== Détecte les duplications dans `O(1)` par noeud. Autres
**Ébauche**=Supprimer tout noeud dont le nombre de signatures ≥ 2=Supprime que les dossiers uniques restent. Autres

---

Mise en œuvre

Vous trouverez ci-dessous des solutions prêtes à coller dans **Java, Python et C++**.
Tous utilisent le même algorithme en trois phases décrit ci-dessus.

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe {
Définition du nœud
Nœud statique privé {
Nom de la chaîne;
Carte <String, Node> enfants = nouveau TreeMap<>(); // trié pour la signature déterministe
Chaîne sig; // signature du sous-arbre

Node(Nom de la chaîne) { this.name = name; }
}

Liste publique<Liste<String>> deleteDuplicateFolder(Liste<Liste<String>> chemins) {
Noeud root = nouveau Noeud(""); // racine factice

/* ---- 1. Construire le trie ---- */
pour (Liste <String> chemin : chemins) {
Noeud cur = racine;
pour (partie d'attache : chemin) {
cur = cur.children.computeIfAbsent(part, k -> new Node(k));
}
}

/* ---- 2. Calculer les signatures et les compter ---- */
Carte<String, nombre entier> = nouveau HashMap<>();
dfsSig(racine, nombre);

/* ---- 3. Recueillir les chemins survivants
Liste <Liste<String>> res = nouvelle liste <>();
Liste<String> curPath = nouvelle liste de distribution<>();
pour (Nœud enfant : root.children.values()) {
dfsCollect(enfant, curPath, res, nombre);
}
retour rés;
}

/* DFS post-commande – calcul de la signature et du nombre */
chaîne privée dfsSig(node, carte <String, nombre entier>) {
si (node.children.isEmpty()) { // feuille
noeud.sig = ";
count.merge(node.sig, 1, entier::sum);
noeud de retour. Sig;
}
StringBuilder sb = nouveau StringBuilder();
pour (Node enfant : node.children.values()) {
sb.append(child.name)
.append("(")
.append(dfsSig(enfant, nombre))
.append(")");
}
noeud.sig = sb.toString();
count.merge(node.sig, 1, entier::sum);
noeud de retour. Sig;
}

/* Deuxième DFS – sauter les sous-arbres dupliqués */
vide privé Recueillir (noeud, liste <String> curPath,
Liste<Liste<String>> res, carte<String, nombre entier> {
si (!node.children.isEmpty() &&count.get(node.sig) > 1) {
retour; // sauter ce nœud et ses enfants
}
curPath.add(nom du noeud);
res.add(nouvelle liste d'array<>(curPath));
pour (Node enfant : node.children.values()) {
dfsCollect(enfant, curPath, res, nombre);
}
curPath.supprimer(curPath.size() - 1);
}
}
«» "

---

- Oui. 2. Python

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
Numéro de classe:
__slots__ = ('nom', 'enfants', 'sig')
def __init_(self, nom: str):
nom propre = nom
Les enfants = {} Nom Noeud
Self.sig = ""

def deleteDuplicateFolder(self, chemins: List[List[str]]) -> Liste[Liste[str]]:
racine = se.Node("") # racine factice

# 1. Construire le tri
pour chemin dans les sentiers:
cur = racine
pour partie dans le chemin:
cur = cur.children.setdefault(part, self.Node(part))

2. Calculer les signatures et les comptes
compteur = defaultdict(int)
Self._dfs_sig(racine, compteur)

# 3. Recueillir les chemins survivants
res = []
cur = []
pour l'enfant dans root.children.values():
auto_dfs_collect(enfant, cur, rés, compteur)
retour res

def _dfs_sig(self, node: 'Solution. Noeud', compteur: code défaut:
si ce n'est pas un nœud. enfants: # feuille
noeud.sig = ""
compteur[node.sig] += 1
noeud de retour. Sig

sb = []
pour enfant dans trié(node.children.values(), key=lambda x: x.name):
child_sig = self._dfs_sig(enfant, compteur)
sb.append(f"{child.name}({child_sig})")
noeud.sig = "".join(sb)
compteur[node.sig] += 1
noeud de retour. Sig

def _dfs_collect(self, node: 'Solution. Un nœud.
cur: Liste[str], res: Liste[List[str]],
compteur: defaultdict):
si nœud.enfants et compteur[node.sig] > 1 :
retour # prune
cur.append(node.name)
res.append(cur.copy())
pour enfant dans trié(node.children.values(), key=lambda x: x.name):
auto_dfs_collect(enfant, cur, rés, compteur)
C. pop()
«» "

---

- Oui. 3. C++

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
#incluez <map>
#incluez <string>
#incluez <algorithme>

utilisant l'espace de noms std;

solution de classe {
particulier:
Numéro de structure {
le nom de la chaîne;
carte <string, noeud*> enfants; // triés
chaîne sig;
Node(const string&n) : name(n) {}
};

vide dfsSig(Node* noeud, non ordonné_map<string,int>& cnt) {
si (noeud->enfants.vide()) { // feuille
noeud->sig = ";
cnt[node->sig]++; retour;
}
chaîne sig;
pour (auto& kv : noeud->enfants) {
Noeud* enfant = kv.seconde;
dfsSig(enfant, cnt);
Sig += nom de l'enfant + (" + enfant->sig + ");
}
noeud->sig = sig;
cnt[node->sig]++; // nombre d'accroissements
}

vide dfsCollect(Node* noeud, vecteur<string>& cur,
vecteur<vector<string>&ans,
Const unordered_map<string,int>& cnt) {
si (!node->children.vide() && cnt.at(node->sig) > 1 )
retour; // prune

cur.push_back(node->name);
ans.emplace_back(cur);
pour (auto& kv : noeud->enfants) {
dfsCollect(kv.second, cur, ans, cnt);
}
cur.pop_back();
}

public:
vecteur<vecteur<chaîne>> deleteDuplicateFolder(vector<vector<string>>&paths) {
Noeud* racine = nouveau Noeud(""); // racine factice

/* construire trie */
pour (auto & chemin : chemins) {
Noeud* cur = racine;
pour (auto & partie : chemin) {
si (!cur->children.count(part))
cur->children[part] = nouveau nœud(part);
cur = cur->enfants[partie];
}
}

unordered_map<string,int> cnt;
dfsSig(racine, cnt);

vecteur <vector<string>> ans;
vecteur <string> curPath;
pour (auto& kv : root->children) {
dfsCollect(kv.seconde, curPath, ans, cnt);
}

/* mémoire libre – omise pour la brièveté, mais conseillée en code réel */
le retour des an;
}
};
«» "

---

Analyse de complexité

Autres Phase du temps Espace
C'est pas vrai.
Construire la trie. "O (nombre de nœuds)" Autres
Signature DFS (nombre de nœuds) "O (nombre de nœuds)" (chaînes de signature)
Taille DFS (nombre de nœuds)
**Total** "O (nombre de nœuds)" Autres

Tant le temps que la mémoire sont linéaires dans la taille de l'entrée – facilement dans les limites de LeetCode.

---

Pièges communs

Pourquoi il échoue
- C'est quoi ?
En utilisant `unordered_map` pour les enfants en Java/C++.
Autres Oubliant de trier les signatures d'enfants.
Autres Retourner le chemin de racine factice `""""" chemin non valide" Sauter la racine factice; recueillir seulement des enfants réels
Autres Les feuilles sont toujours uniques (signature vide) – elles ne sont jamais dupliquées.

---

Essais d'échantillons

'`python
# Python – vérification rapide de la santé mentale
sol = Solution()

print(sol.deleteFolder([["a","b"],["a","c"]])
[["a", "b"], ["a", "c"]]

print(sol.deleteDuplicateFolder([["a","b","c"],["a","b","d"],["x","y","c"],["x","y","d"],["x","z","d"])
# => [["a", "b", "d"], ["x", "z", "d"]]
«» "

N'hésitez pas à exécuter les mêmes entrées dans les implémentations Java / C++ – les ensembles de sortie doivent être identiques.

---

Article du blog

---

# -Supprimer les dossiers dupliqués dans le système – Une plongée profonde dans le LeetCode 1948 (Java, Python & C++)

> **Méta-description**: Master LeetCode 1948 – Supprimer les dossiers dupliqués dans le système. Apprenez une solution de sérialisation arborescente en Java, Python et C++. Idéal pour la préparation d'entrevue, la résolution de problèmes difficiles et la déduplication du système de fichiers.

---

Présentation

Si vous avez déjà abordé **LeetCode 1948 – Supprimer les dossiers dupliqués dans System**, vous le savez est un problème *Hard* qui teste votre compréhension des arbres, hachage, et DFS.
Cet article explique le problème, présente une solution élégante qui fonctionne dans les trois langues principales, et passe par les parties de bonne, mauvaise et laid de l'implémentation.

---

Mots clés

- Supprimer les dossiers dupliqués dans le système
- Leetcode 1948
- Problèmes de LeetCode
- Dédoublement du système de fichiers
- Sérialisation des arbres
- DSV hachage
- Solution Java
- Solution Python
- Solution C++

---

Récapitulation des problèmes

Vous recevez une liste de chemins de dossiers absolus.
Si deux ou plusieurs dossiers partagent *exactement* la même structure imbriquée (les noms ne comptent pas, seulement la structure), ils sont marqués pour la suppression.
Le système de fichiers effectue **un** pass de suppression – tout nouveau dossier identique qui apparaît *après* ce pass est laissé intact.
Retourne la liste des chemins qui survivent.

---

- Oui. Pourquoi Arbre + Signature + Compte est l'approche d'or

1. **Tree** – Un *trie* de noms de dossiers donne une façon naturelle de décrire les relations parent → enfant.
2. **Signature** – Une chaîne déterministe qui décrit un sous-arbre. Le tri des signatures d'enfants supprime la dépendance à l'ordre.
3. **Count** – `HashMap<signature, occurrences>` nous permet de décider en O(1) s'il faut tailler un noeud.

Cette stratégie en trois phases réduit un problème de comparaison potentiellement exponentiel à un simple hachage de chaînes et à des traversées linéaires.

---

## 4-

### 4.1 Construire la trie

«» "
racine
│ − c
C'est ce qui s'est passé.
«» "

- Chaque chemin crée des nœuds à partir de la racine factice.
- Les `enfants` sont stockés sur une carte triée (`TreeMap` / `map`) pour garantir une commande déterministe.

4.2 Signatures de calcul (DFS après commande)

«» "
feuille: sig = "" // chaîne vide
intérieur: sig = concat(sorted(childName + "(" + enfantSig + ")"))
«» "

Deux sous-arbres identiques génèrent des « sig » identiques.
En calculant, incrémentez un compteur mondial.

### 4.3 Recueillir les survivants (deuxième DSV)

Si une signature de nœud survient **≥ 2**, sautez ce nœud (et ses enfants).
Sinon, enregistrez le chemin et récursez.

---

## 5-Specific Implementations

#### 5.1 Java

"Java
solution de classe {
/* ... (code Java ci-dessus) ... */
}
«» "

5.2 Python

'`python
Solution de classe:
/* ... (code Python de dessus) ... */
«» "

C++

'`cpp
solution de classe {
/* ... (code C++ ci-dessus) ... */
};
«» "

Les trois extraits compilent dans leurs environnements respectifs LeetCode et s'exécutent en temps linéaire.

---

C'est pas vrai. Bon, mauvais, et humble

Autres La phase est bonne
- C'est quoi ?
**Tree Build**=L'abstraction nette des dossiers=' Nécessite une gestion attentive de la mémoire en C++='Les noeuds sur-allouants peuvent souffler la mémoire='
**Signature**= Comparaison simple `String`= La concaténation des chaînes peut être coûteuse si les sous-arbres sont énormes= Utiliser des pointeurs bruts (C++) – risque de fuite==
**Ébauche**= Un passage, déterministe== L'oubli de compter les feuilles conduit à des bogues subtils==Recursion proof risque (deep file systems)==

À emporter

- **Bien** – complexité linéaire, structures de données réutilisables.
- **Bad** – Il faut trier pour éviter les bugs de commande.
- **Ugly** – Nettoyage manuel de la mémoire (C++) et manipulation de récursions extrêmement profondes.

---

Les pensées finales

LeetCode 1948 est un problème *hard* qui fait tourner votre pensée de "comparer chaque paire" à "hash" la structure une fois, puis prune.
La technique de sérialisation des arbres est un modèle puissant qui apparaît dans d'autres problèmes difficiles comme *Binary Tree Substructure*, *Symmetric Tree*, et même dans les systèmes du monde réel pour **file system deduplication**.

Pratiquez l'algorithme en trois phases dans toutes les langues, exécutez les cas de test, et vous aurez une réponse solide prête pour n'importe quel forum d'entrevue.

Bon codage !

---

> **Auteur**: [Votre nom] – passionné d'algorithme, développeur Java & Python, gourou C++.

---

Articles connexes

- *Sous-structure de l'arbre généalogique – LeetCode 572*
* Arbre symétrique – LeetCode 101*
- *Concevoir un système de fichiers – Entrevue de codage*

---

Avec ce guide, vous avez obtenu le problème *Hard* fissuré et les outils pour expliquer votre solution avec confiance. Joyeux entretien de préparation!

---

*Fin de l'article*

---

N'hésitez pas à adapter l'article au style de votre blog ou à ajouter plus de diagrammes visuels si votre plateforme les supporte. Bonne écriture !