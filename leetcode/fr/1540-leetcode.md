---
Titre: LeetCode 1540. Peut convertir Chaîne en K Déplace -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solution 3-Way Code pour LeetCode 1540 – *Can Convert String in K Moves*

Langue Nom du fichier Complexité
- C'est quoi ?
**Java**
**Python**
**C++**

> **Important:**
> `k` peut être aussi grand que `10^9`, nous avons donc besoin de 64 bits entiers (`long` / `long`) pour la sécurité.

---

#### 1.1 Java

"Java
// 1540. Peut convertir la chaîne en K bouge
// Heure: O(n)
// Espace: O(1)
solution de classe publique {
publique booléenne canConvertString(String s, String t, int k) {
// Les cordes doivent avoir la même longueur
si (s.length() != t.length()) retourne faux;

// Compter combien de fois chaque valeur de déplacement (1..25) est nécessaire
int[] need = new int[26]; // need[d] = nombre d'indices avec déplacement d

pour (int i = 0; i < s.longueur(); i++) {
int diff = (t.charAt(i) - s.charAt(i) + 26) % 26;
Si (diff) 0) continuer; // déjà égal
// L'occurrence i-th du poste `diff' nécessite
// (besoins[diff] * 26 + diff) se déplace au total jusqu'à présent.
si ((long)need[diff] * 26 + diff > k) retourner faux;
besoin[diff]++;
}
retour vrai;
}
}
«» "

---

#### 1.2 Python 3

'`python
# 1540. Peut convertir la chaîne en K Déplacements
♪ Heure: O(n)
♪ Espace: O(1)

def canConvertString(s): str, t: str, k: int) -> C'est vrai.
si len(s) != len(t):
Retour Faux

besoin = [0] * 26 # besoin[d] = nombre d'indices besoin changement d

pour sc, tc en zip(s, t):
diff = (ord(tc) - ord(sc)) % 26
si diff == 0:
poursuivre
si nécessaire[diff] * 26 + diff > k:
Retour Faux
besoin[diff] += 1
retour Vrai
«» "

---

*## 1.3 C++

'`cpp
// 1540. Peut convertir la chaîne en K bouge
// Heure: O(n)
// Espace: O(1)

solution de classe {
public:
bool canConvertString(chaîne s, chaîne t, int k) {
si (s.size() != t.size()) retourne false;

vectorielle <long> besoin(26, 0); // besoin[d] = nombre d'indices nécessitant un changement de direction d

pour (size_t i = 0; i < s.size(); ++i) {
int diff = (t[i] - s[i] + 26) % 26;
Si (diff) 0) poursuivre;
si (need[diff] * 26 + diff > k) retourner faux;
++besoins[diff];
}
retour vrai;
}
};
«» "

---

- Oui. 2. Article de blog – Code Leet 1540: Les bons, les mauvais et les méchants

> **Titre:**
> *LeetCode 1540 – Can Converting String in K Moves: A Deep Dive (Java, Python, C++)*
> **Méta—description:**
> Comprendre l'algorithme derrière LeetCode 1540, voir les solutions Java/Python/C++ propres, apprendre les pièges, et maîtriser l'astuce d'interview qui pourrait vous atterrir votre travail de technologie de rêve.

---

2.1 Aperçu du problème

> **Objectif** – Convertissez la chaîne `s` en chaîne `t` dans **au plus `k` moves**.
> Un mouvement : choisissez un indice non utilisé `j`, déplacez le caractère à cet indice `i` fois (enlevant de `z` à `a`), ou sautez un mouvement.
> Chaque indice peut être utilisé **une fois**.

**Contrôles* *
- "1 ≤ , s = , t ≤ 105 "
- `0 ≤ k ≤ 109`
- Seulement des lettres minuscules.

---

#### 2.2 Le bien – La perspective directe

1. ** Calculer le décalage nécessaire par indice**
```diff = (t[i] - s[i] + 26) % 26``
Si `diff=0`, aucune action n'est nécessaire.

2. **Chaque valeur de déplacement `d` peut apparaître plusieurs fois* *
Le *premier* déplacement du poste `d` coûte `d`.
L'occurrence *seconde* du même "d" doit utiliser un cycle complet supplémentaire de 26 mouvements parce que nous ne pouvons pas déplacer à nouveau le même indice.
En général, l'événement *j-th* coûte "26*(j-1) + d".

3. **Vérification du sperme**
Pour chaque valeur de déplacement, conservez le nombre de fois qu'elle est apparue jusqu'à présent (`cnt[d]`).
Avant de traiter la prochaine occurrence, nous vérifions :
* 26 + d <= k```
Si l'inégalité échoue, le coût total dépassera "k" et nous pourrons arrêter tôt.

La beauté : un seul passage sur les cordes, un espace auxiliaire constant, et **O(n)** temps.

---

#### 2.3 L'erreur – Pièges communs

Pourquoi il échoue
- C'est quoi ?
**L'utilisation de `int` pour `k`**" `k` peut être de 1 milliard; les sommes intermédiaires `cnt[d] * 26` peuvent déborder. Autres
**Soustraire les caractères sans le mod**
**Ignorer les indices qui correspondent déjà à**. Pas de problème.
**Tréer chaque indice de façon indépendante** , Nous avons oublié que chaque cycle de travail (26) coûte des déplacements supplémentaires pour répéter `diff` , Utilisez `cnt[d] * 26` pour tenir compte des cycles ,
**Missing de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état de l'état

---

2.4 L'Ingénierie excessive

- **Cartes de vol** pour compter les équipes (travaille mais ajoute des frais généraux).
- **Trier** les valeurs de décalage et effectuer la recherche binaire.
- **DP** sur tous les mouvements possibles (exponentielle).
- ** Simulation** de chaque mouvement.

Ces approches sont inutiles. Le problème se résume à compter les fréquences des déplacements et à appliquer la formule du coût du cycle. Garde ça simple, fais vite.

---

### 2.5 Pourquoi cette solution est-elle utile pour les entrevues

Caractéristiques Prestations
C'est pas vrai.
**Temps linéaire**=Poigne la longueur maximale `105` confortablement. Autres
**L'espace continu** Autres
**Poignées grandes `k`**= L'arithmétique 64-bit montre l'attention portée aux cas de bord. Autres
**Readable**= Peu de lignes, noms de variables clairs, pas de tours obscurs. Autres
**Extensible**= Peut être modifié pour les variantes (p. ex., permettre des déplacements multiples par index). Autres

---

2.6 Extraits de code complets (Java, Python, C++)

*(Voir la section 1 pour les implémentations complètes.) *

---

2.7 A emporter et conseils d'entrevue

1. **Demander des éclaircissements** – Le problème a-t-il dit "à la plupart des déplacements "k" ou "à la fois" exactement "k" ?
2. **Exposer le cycle de travail** – Souligner pourquoi chaque poste répété coûte 26 déplacements supplémentaires.
3. **Va à travers un contre-exemple** – Montrez ce qui se passe lorsque vous ignorez le coût du cycle.
4. **Déclarer la complexité à l'avance** – Les intervieweurs aiment les résumés concis.
5. **Cas de bord Mention** – Chaînes vides, `k = 0`, chaînes déjà égales.

> **Bonus:** La même technique résout de nombreuses questions d'entrevues de transformation de chaîne. Maîtrisez-le, et vous aurez un outil solide dans votre boîte à outils algorithme.

---

2.8 Pensée finale

LeetCode 1540 est un exemple classique où une observation attentive (le cycle de 26 mois) transforme un problème de transformation apparemment complexe en une solution linéaire à temps constant. En comprenant le **bon**, en évitant le **mauvais**, et en ignorant le **ugly**, vous pouvez attraper le problème et impressionner les intervieweurs – potentiellement atterrissant ce travail de technologie convoité. Bon codage !