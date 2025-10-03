---
titre: LeetCode 2416. Somme des scores préfixes des cordes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2416 – Somme des scores préfixes des cordes
**Python de Java**C++**

---

- Oui. 1. Résumé du problème

Étant donné qu'un tableau `words` (1 ≤ n ≤ 1 000, chaque longueur de mot ≤ 1 000) composé de lettres anglaises minuscules, définit le *score* d'une chaîne `term` comme le nombre de mots dans `words` qui ont `term` comme préfixe (y compris lui-même).

Pour chaque "mots [i]" nous avons besoin de la somme des scores de ** chaque préfixe non vide** de ce mot.

Retourner un tableau `réponse` où `réponse[i]` est cette somme.

---

- Oui. 2. Pourquoi un essai?
La structure de données classique pour les problèmes liés au préfixe est le **Trie (arbre de préfixe)**.
* Chaque noeud représente un préfixe.
* Un noeud peut stocker le nombre de mots qui passent par lui → directement la partition de ce préfixe.
* L'insertion et la requête sont à la fois 'O(L)' où `L` est la longueur du mot.

Avec les contraintes, cela est optimal ('O(caractères totaux)' 1 000 × 1 000 = 106 opérations).

---

- Oui. 3. Idées fondamentales

1. **Construire la trie**
Pour chaque mot, marchez le Trie, créant des nœuds d'enfants manquants, et incrémentez un champ `compte` sur chaque noeud que nous visitons.
Après insertion, `node.count` est égal au nombre de mots ayant le préfixe représenté par ce nœud.

2. ** Calculer la réponse**
Pour chaque mot, marchez à nouveau, additionnant le `compte` de chaque nœud visité.
Cette somme est exactement la somme de préfixe requise.

---

- Oui. 4. Détails de la mise en œuvre

Langue Structure des nœuds
C'est-à-dire...
**Java**= `int count; Node[] child = new Node[26];`= Après avoir créé / récupéré l'enfant, `child.count++`.== `O(total characters)` Autres
*Python *Python *Python *Python *Python *Python *Python *Python *Python *Python 1 '.. Autres
**C++**= < < nombre d'ints; node* enfant[26]=>; "enfant->compte++". Autres

Les trois utilisent la même logique – juste des différences syntaxiques.

---

- Oui. 5. Code

##### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
// - Oui. Trie Node...
Nœud statique privé {
nombre int = 0;
Node[] enfant = nouveau Node[26];

booléen contient(char ch) { retour enfant[ch - 'a'] != nul; }
Noeud get(char ch) { retour enfant[ch - 'a']; }
vide put(char ch, Node n) { child[ch - 'a'] = n; }
vide inc() { count++; }
}

// - Oui. Noyau - Oui.
finale privée racine du nœud = nouveau nœud();

// Insérer un mot dans le trie, incrémenter les nombres le long du chemin
vide privé insert(mot d'ordre) {
Noeud cur = racine;
pour (char ch : word.toCharArray()) {
si (!cur.contient(ch)) cur.put(ch, nouveau nœud();
cur = cur.get(ch);
cur.inc(); // le nombre de ce préfixe augmente
}
}

// Résumez les comptes de tous les préfixes de mots
préfixe privé intScoreSum (mot de connexion) {
Noeud cur = racine;
= 0;
pour (char ch : word.toCharArray()) {
cur = cur.get(ch);
somme += Cur.count;
}
la somme de retour;
}

// -------- API LeetCode ----------
public int[] sumPrefixScores(String[] mots) {
// 1. Construction trie
pour (String w : mots) insérer(w);

// 2. Réponses aux questions
int n = longueur de mots;
int[] ans = nouvelle int[n];
pour (int i = 0; i < n; i++) ans[i] = préfixeScoreSum(words[i]);
le retour des an;
}
}
«» "

5.2 Python

'`python
Solution de classe:
C'est... Trie Node...
Numéro de classe:
__slots__ = ('cnt', 'enfant')
def _init_(self):
auto.cnt = 0
soi-même.enfant = [Aucun] * 26

def _init_(self):
self.root = self.Node()

C'est... Noyau - Oui.
def insert(self, mot: str) -> Aucun:
noeud = self.root
pour ch en mot:
idx = ord(ch) - 97
si noeud.child[idx] n'est pas:
Node.child[idx] = soi-même.Node()
noeud = noeud.child[idx]
noeud.cnt += 1

def prefix_score(self, mot: str) -> Int:
noeud = self.root
s = 0
pour ch en mot:
noeud = noeud.enfant[ord(ch) - 97]
s += noeud.cnt
retour s

C'est... API LeetCode ----------
def sumPrefixScores(self, words: list[str]) -> list[int]:
pour w en mots:
auto.insérer(w)
retourner [self.prefix_score(w) pour w en mots]
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
Numéro de structure {
cnt = 0;
Noeud* enfant[26] = {nullptr};
};
Noeud* racine = nouveau Noeud();

vide insert(const string& word) {
Noeud* cur = racine;
pour (char ch : mot) {
int id = ch - 'a';
si (!cur->child[id]) cur->child[id] = nouveau nœud();
cur = cur->child[id];
++cur->cnt; // ce préfixe apparaît encore une fois
}
}

Int score(const string & word) {
Noeud* cur = racine;
int s = 0;
pour (char ch : mot) {
cur = cur->child[ch - 'a'];
s += cur->cnt;
}
retour s;
}

public:
vector<int> sumPrefixScores(vecteur<string>& mots) {
pour (const string& w : mots) insérer(w);
vecteur <int> ans;
as.reserve(words.size());
pour (const string& w : mots) ans.push_back(score(w));
le retour des an;
}
};
«» "

---

- Oui. 6. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Construisez trie. Autres
Autres Interroger chaque mot
*Total * Total * O(total_chars) * O(total_chars) * Autres

Avec `n ≤ 1000` et chaque mot ≤ 1000, les caractères totaux les plus défavorables sont `106`, qui s'inscrivent facilement dans les délais.

---

- Oui. 7. Cas de bord et pièges communs

Numéro
C'est quoi ?
**Couvercle du nœud racine**La racine représente un préfixe vide – nous ne le faisons pas**. L'augmentation ne compte qu'après avoir déménagé vers un enfant. Autres
**Plusieurs mots identiques**La trie accumule automatiquement les nombres; les mots identiques sont manipulés sans code spécial. Autres
**Utilisation de la mémoire**= Pour le pire des cas (tous les caractères distincts), nous créons au maximum des nœuds `total_chars` – amende pour 1 000 × 1 000. Autres
**Profondeur de la récursion** Autres
**Validation d'entrée**LeetCode garantit les lettres minuscules – pas besoin de vérification. Autres

---

- Oui. 8. Bon, mauvais, mauvais dans les entrevues

Ce que l'intervieweur attend de vous
- Oui.
Un tri propre et itératif qui met à jour compte à la volée. Autres
J'ai fait en sorte d'ignorer le préfixe vide et de ne s'accumuler qu'après avoir visité un enfant. Autres
En utilisant une carte de hachage pour chaque noeud (dépassement excessif) ou récursion DFS qui souffle la pile. J'ai utilisé un tableau fixe de 26 pour la vitesse et la traversée itérative pour la sécurité. Autres

---

- Oui. 8. Variations que vous pourriez voir dans les entrevues

1. **Retourner la somme préfixe-score la plus élevée** – vous pouvez simplement garder un maximum global tout en interrogeant.
2. **Prefix‐score pour une chaîne cible seulement** – build the trie once, puis requête juste cette cible.
3. **Requêtes en ligne** – garder la trie persistante et manipuler insert/query entrelacé.

---

8.1 Discuter Dans l'interview

1. **Énoncez votre approche**: -I-ll construire une Trie où chaque noeud stocke le nombre de mots qui partagent ce préfixe. (en milliers de dollars)
2. **Expliquer les deux passes**: insertion → nombre incrément; requête → somme des nombres.
3. **Complexité des phrases**: temps et espace `O(caractères totaux).
4. **Parler de cas de bord**: mots identiques, préfixes vides.
5. **Optionnel**: Mention vous pouvez aussi le résoudre avec un tableau trié + recherche binaire, mais ce serait `O(n log n)` par requête – pas aussi élégant qu'une Trie.

---

Pourquoi les intervieweurs Aimez la trie

* **Savoirs sur la structure des données** – Affiche que vous pouvez choisir la bonne structure pour le problème.
* **Échange de temps de l'espace** – Vous équilibrez la mémoire avec la performance.
* **Scalabilité** – Votre solution fonctionne même si les contraintes doublent.
* **Détail de mise en œuvre** – L'attention portée aux nombres de nœuds, aux boucles itératives et à l'hygiène de la mémoire démontre la discipline du codage.

---

8.3 Comment faire tourner l'entrevue

Étape Recommandation Autres
-- -- -- -- -- --
**Commencez avec l'intuition** -Nous traitons avec les préfixes, donc une Trie est naturelle. Autres
**Venez à travers votre code** Autres
**Time/Space**=État `O(total_chars)` explicitement. Autres
**Mentions d'écueils**** Afficher la sensibilisation au nombre de racines par rapport au nombre d'enfants. Autres
**Parler d'extensions**=Si nous n'avions besoin que du score maximum, nous l'avons suivi pendant l'insertion.= Autres
**Praticien**) Résolvez 2416 sur LeetCode et écrivez une brève explication – les intervieweurs apprécient une solution bien articulée. Autres

---

Article sur le blog – Résumé des préfixes : une classe de maîtres trie-drive

Titre
**Sum of Prefix Scores of Strings – Mastering the Trie for LeetCode Hard* *

Description de la méta
Découvrez comment résoudre LeetCode 2416 avec une implémentation propre Trie en Java, Python et C++. Découvrez les conseils d'entrevue, la gestion des cas et pourquoi ce problème est un must-savoir pour toute entrevue d'ingénierie logicielle. (en milliers de dollars)

---

- Oui. 1. Le problème en coque
(Insérer l'énoncé du problème – comme ci-dessus)

> *Pourquoi ce problème est important*: Il teste votre capacité à transformer une définition théorique (= score préfixe=) en solution concrète de structure de données. C'est une question **hard** LeetCode qui apparaît souvent dans les pipelines d'entrevue de niveau supérieur.

- Oui. 2. Bon – Pourquoi la Trie est parfaite
* Poignée les longueurs de préfixe arbitraires.
* Compter par noeud = score préfixe → *O(1)* accès.
* Échelles linéaires avec taille d'entrée.

- Oui. 3. Mauvais – Pourquoi une Brute-Force ou une approche Hash-Map
* Double boucle naïve → `O(n2·L)` (plus mauvais cas 1010 opérations).
* Les cartes hash par mot auraient encore besoin d'un balayage linéaire par requête → frais généraux inutiles.
* Tri + recherche binaire est `O(n log n)` par requête – pas optimal pour `L = 1 000`.

- Oui. 4. Laid – Pièges cachés
* Oublier que le *root* est le préfixe vide – entraîne des erreurs off-by-one.
* Incrémentation compte **avant** passer à l'enfant au lieu d'après.
* Utilisation de la récursion sur une trie profonde (la profondeur peut être 1 000) → débordement de la pile sur certains juges.

- Oui. 5. Démarche de mise en œuvre (Java, Python, C++)
(Insérer des extraits de code de la section 5 avec de brefs commentaires.)

- Oui. 6. Répartition par complexité
(Insérer le tableau de complexité.)

- Oui. 7. Ce que recherchent les intervieweurs
* Reconnaissance de la Trie comme solution canonique.
* Traitement correct des mots identiques et du préfixe vide.
* Discussion des compromis temps/espace.
* Capacité d'expliquer la logique des deux passages en anglais simple.

- Oui. 8. Variations que vous devriez connaître
* Et si nous n'avons besoin que de la somme de préfixe maximale? (en milliers de dollars)
* Et si les mots viennent dans un flux en ligne? (en milliers de dollars)
* Peut-on le résoudre avec un tableau trié + recherche binaire?

- Oui. 9. Mots clés du SEO
* **LeetCode 2416**
* **Somme des scores préfixes* *
* ** Trie préfixe**
* **Problèmes de code de leet *
* **Entretien avec un ingénieur logiciel**
* **Questions d'entrevue sur la structure des données**
* **Préparation de l'entrevue d'embauche**

Incorporer ces mots clés naturellement dans les rubriques, les paragraphes et la méta description.

10 ans. Réflexions finales
La maîtrise de ce problème met en évidence votre intuition *structure des données*, *codage propre* et *efficacité algorithmique* – qualités de chaque gestionnaire d'embauche. En étant capable d'articuler l'approche, les détails de mise en œuvre et les pièges subtils, vous vous démarquerez dans une interview technique.

> **Prochaine étape** – pratiquez le problème sur LeetCode, puis ajoutez une courte écriture (comme ce billet de blog) à votre portfolio ou GitHub README. Les recruteurs aiment les candidats qui peuvent expliquer leurs solutions, pas seulement les coder.

Bon codage et bonne chance d'atterrissage ce rôle d'ingénierie logicielle de rêve! C'est ce qu'il a dit.

---