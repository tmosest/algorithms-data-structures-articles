---
titre: LeetCode 2506. Nombre de paires de cordes similaires -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2506 – Nombre de paires de cordes similaires
> **Un guide complet avec des solutions Java, Python & C++ + un article de blog qui vous aidera à décrocher votre prochain emploi technologique* *

---

TL;DR
- **Problème** : Comptez les paires de mots qui se composent du même ensemble de caractères (fréquence d'ignorage et ordre).
- **Key Insight**: Chaque mot peut être représenté par un masque de 26 bits – un bit par lettre alphabétique.
- ** Solution optimale** : Construisez le masque, stockez la fréquence de chaque masque dans une carte de hachage, et pour chaque nouveau mot, ajoutez la fréquence actuelle à la réponse.
- **Complexité**:
- **Heure** O(n · m) (où *n* = nombre de mots, *m* = longueur maximale du mot)
- **Espace** O(n) (carte de cache pour masques)

"Java
int similarPairs(String[] mots) // Java
«» "

'`python
def similarPairs(mots: List[str]) -> Int # Python
«» "

'`cpp
int similarPairs(vector<string>& words) // C++
«» "

> **Pourquoi cela importe** – Le modèle bitmask + hash‐map est un astuce *stand‐out* qui apparaît fréquemment dans la préparation de l'entrevue, en particulier pour les rôles supérieurs.

---

Article de blog (optimisé par le référencement)

> **Titre**
> **Pairs de montage de cordes similaires (LeetCode 2506) – Un guide complet, un code et des conseils d'entrevue* *

> **Description détaillée**
> Master LeetCode 2506: Nombre de paires de cordes similaires. Obtenez une solution étape par étape, un code Java/Python/C++, une analyse de l'espace temporel et des astuces d'entrevue pour impressionner les gestionnaires d'embauche.

> **Mots clés**
> LeetCode 2506, Count Pairs of Similar Strings, Bitmask, HashMap, Java, Python, C++, Algorithm, Data Structures, Coding Interview, Technical Interview, Job Interview, Senior Software Engineer

---

Récapitulation des problèmes

> **Input**: `words[0 ... n-1]` – une liste de chaînes minuscules.
> **Objectif**: Compter le nombre de paires d'index `(i, j)` avec `i < j` de sorte que le *set* de caractères dans `words[i]` est égal à l'ensemble «words[j]».

> **Exemple**
> `` "
> mots = ["aba", "aabb", "abcd", "bac", "aabc"]
> → 2 paires (0,1) et (3,4)
> `` "

---

C'est vrai. Le Bon: Pourquoi Bitmask fonctionne

Raison
- Oui.
**Vérifier si deux cordes sont similaires est *O(1)* une fois que nous avons le masque. Autres
**Mémoire-efficace** , 26 bits → un seul `int`. Autres
**Simple pour implémenter**.Pas besoin de trier, utiliser des ensembles ou hacher tous les caractères. Autres
**Scales**= Fonctionne pour jusqu'à 10^5 mots, 100 caractères chacun – bien dans les limites. Autres

C'est vrai. Construction de masques

Texte
bit 0 → 'a'
bit 1 → 'b '
...
bit 25 → 'z '
«» "

Pour chaque caractère `c` dans un mot, définir `mask= 1 << (c - 'a')`.
Parce que nous ne nous soucions que de la *présence* d'un personnage, les duplicatas sont automatiquement ignorés.

---

C'est vrai. Les mauvais : les cas et les pièges

Numéro
C'est quoi ?
Dupliquer les mots Dupliquer Traiter chaque instance séparément – chaque paire compte. Utilisez une carte de fréquence, pas un ensemble. Autres
Des chaînes vides (pas dans les contraintes) Pas besoin de manipulation spéciale. Autres
Autres De très longs mots Encore O(m) par mot, amende pour ≤100. Autres

---

C'est pas vrai. L'Ugly : une approche forte

> **Que ne pas faire**
> ``python
> ans = 0
> pour i dans la plage(n):
> pour j dans la plage(i+1, n):
> si set(words[i]) == set(words[j]):
> ans += 1
> `` "
> Cette solution O(n2·m) sera TLE pour les grandes "n". Il utilise aussi `set()` pour chaque paire, en doublant la mémoire.

> **A emporter** – Toujours chercher un *signature* (bitmask, hasch) pour réduire les comparaisons par paires.

---

Code complet – trois langues

#### Java (Code Leet 2506)

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe {
public int similarPairs(String[] words) {
Int ans = 0;
Carte<integer, integer> freq = nouveau HashMap<>();

pour (Mot d'ordre : mots) {
masque int = 0;
pour (char ch : word.toCharArray()) {
masque= 1 << (ch - 'a');
}
ans += freq.getOrDefault(masque, 0);
freq.merge(masque, 1, entier::sum);
}
le retour des an;
}
}
«» "

Python 3

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def similarPairs(self, mots: List[str]) -> Int:
ans = 0
freq = defaultdict(int)

pour mot en mots:
masque = 0
pour ch in word: # duplicata auto-ignoré
masque= 1 << (ord(ch) - 97)
ans += freq[masque]
freq[masque] += 1

retour et
«» "

#### C++ (GNU‐C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int similarPairs(vector<string>& words) {
Int ans = 0;
unordered_map<int, int> freq;

pour (auto& w : mots) {
masque int = 0;
pour (charc : w) {
masque = 1 << (c - 'a');
}
as += freq[masque];
freq[mask]++; // stocker une nouvelle occurrence
}
le retour des an;
}
};
«» "

---

Analyse de complexité

Explication
C'est pas vrai.
**Heure**="O(n * m)" – chaque mot scanne ses caractères une fois; `m ≤ 100`. Autres
**L'espace**="O(n)" – la carte de fréquence peut contenir jusqu'à `n` différents masques. Autres

---

### 7--Des conseils d'entrevue

1. **Mentionnez l'idée de bitmask immédiatement** – les intervieweurs aiment les tours de bas niveau.
2. ** Expliquez pourquoi les duplicatas ne comptent pas** – le masque capture seulement *présence*.
3. **Parlez du rôle de la carte de hachage** – accumulation à temps constant de paires.
4. **Montrer la manipulation des cas** – chaîne vide, mots très longs, lettres répétées.
5. **Comparez avec une solution O(n2) naïve** – pourquoi elle échouerait.

---

TL;DR Feuille de chaleur

Étape de l'extrait de code (Java)
-- -- -- -- -- -- -- -- -- --
Construisez un masque, "masque=1 << (ch - "a");" Autres
Autres Nombre de paires de nombres `ans += freq.getOrDefault(masque, 0);`=
Autres Conserver le masque « freq.merge (masque, 1, entier::sum);»

---

Pourquoi ce blog vous aide à trouver un emploi

1. **Référencement favorable** – L'article est structuré pour les moteurs de recherche (en-têtes, mots-clés).
2. **Hands‐On Code** – Des solutions réelles et testées en trois langues.
3. **Interview-Centric** – Marche à travers des scénarios bons, mauvais, laids.
4. **Showcases Meilleures Pratiques** – Bitmask + hash carte pattern est un outil d'entrevue convoité.

> **Prochaine étape**: Copiez le code, lancez-le sur la plateforme LeetCode, et ajoutez l'article à votre portfolio GitHub. Lié Dans les lecteurs, vous verrez l'énoncé du problème, votre solution et les idées – exactement ce que les recruteurs recherchent.

Bon codage, et bonne chance pour l'entrevue! C'est ce qu'il a dit