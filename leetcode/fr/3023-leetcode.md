---
titre: LeetCode 3023. Trouver le modèle dans le flux infini Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – 3 langues

Vous trouverez ci-dessous les implémentations **ready‐to‐copy** qui résolvent le problème LeetCode 3023. Trouver le modèle dans le flux infini En utilisant la stratégie **rolling-hash (Rabin–Karp)**.
Le code est écrit en **Java, Python et C++** – tous commentés et prêts pour des tests unitaires ou une interview en direct.

> **Pourquoi Rolling-Hash? **
> Le cours d'eau est *infini*, mais le motif est court (=100).
> Un hachage roulant permet de comparer la fenêtre actuelle du flux avec le hachage du motif en **O(1)** par caractère, après une pré-computation **O(p)**, ce qui donne une complexité temporelle globale de **O(n)** où *n* est le premier indice qui contient le motif (garanti ≤ 105).
> Une simple fenêtre coulissante ou une comparaison naïve nécessiterait des opérations **O(p × n)**, ce qui est 107 dans le pire des cas – encore très bien, mais le roller-hash est plus propre et plus rapide.

---

#### 1.1 Java

"Java
***
* LeetCode 3023 – Trouver le modèle dans le flux infini I
*
* Auteur: ChatGPT
* Date: 2025‐09‐24
*
* La solution utilise un hachage roulant (Rabin–Karp) sur un flux binaire.
*/
solution de classe {

public int findPattern(InfiniStream infiniStream, int[] pattern) {
base finale int = 2; // alphabet binaire
Mod longue finale = 1_000_000_007L; // Grande prime pour éviter les collisions

- Oui. 1. Calculer le hachage du modèle --------- */
modèle long Hash = 0;
longue basePow = 1; // base^(p-1) modulo mod
pour (int i = 0; i < motif longueur; i++) {
modèle Hash = (patternHash * base + motif[i]) % mod;
i (i < pattern.longueur - 1) basePow = (basePow * base) % mod;
}

- Oui. 2. Initialiser la première fenêtre du flux --------- */
longue fenêtre Hash = 0;
int[] window = nouveau int[pattern.longueur];
pour (int i = 0; i < motif longueur; i++) {
bit int = infiniStream.next();
window[i] = bit;
fenêtre Hash = (windowHash * base + bit) % mod;
}

- Oui. 3. Fenêtre coulissante ----------------------------------- */
int idx = 0; // Indice de départ actuel de la fenêtre
alors que (vrai) {
if (windowHash == patternHash && matches(window, pattern)) {
retourner idx;
}

// Fenêtre de diapositive par une
int oldBit = window[idx % pattern.longueur];
Int nouveau Bit = infiniStream.next();

// Enlever l'ancien Contribution bit
fenêtre Hash = (windowHash - (oldBit * basePow) % mod + mod) % mod;
// Annexe Un peu
fenêtre Hash = (windowHash * base + newBit) % mod;

// Gardez le tableau de fenêtres coulissantes à jour
window[(idx + 1) % pattern.longueur] = nouveau Bit;
idx++;
}
}

*** Aide : comparaison exacte octet-by-octet avec la protection contre les collisions de hachage. */
matches booléens privés(int[] fenêtre, int[] motif) {
pour (int i = 0; i < motif longueur; i++) {
si (window[i] != pattern[i]) retourner faux;
}
retour vrai;
}
}
«» "

> **Notes**
> * Nous utilisons un module (`1_000_000_007`) pour éviter le débordement entier et minimiser les collisions de hachage.
> * La méthode `matches` n'est invoquée que lorsque les haches s'entendent – les collisions sont pratiquement impossibles pour les contraintes données, mais cela garantit la justesse.

---

#### 1.2 Python

'`python
"""
LeetCode 3023 – Trouver le modèle dans le flux infini I
Auteur: ChatGPT
"""

Solution de classe:
def findPattern(self, infiniStream: 'InfiniteStream', pattern: List[int]) -> Int:
base = 2
Le montant de l'aide est calculé comme suit:

# 1. La tête du modèle
_Hash = 0
base_pow = 1 # base^(p-1) % mod
pour i, bit in énumérate(pattern):
pat_hash = (pat_hash * base + bit) % mod
si i < len(pattern) - 1 :
base_pow = (base_pow * base) % mod

# 2. Première fenêtre
fenêtre = []
win_hash = 0
pour _ dans la plage(len(pattern)):
bit = infiniStream.next()
window.append(bit)
win_hash = (win_hash * base + bit) % mod

idx = 0
alors que Vrai:
if win_hash == pat_hash et window == motif :
retourner idx

old_bit = fenêtre[idx % len(pattern)]
new_bit = infiniStream.next()

# Supprimer la contribution de old_bit
win_hash = (win_hash - (old_bit * base_pow) % mod + mod) % mod
# Ajouter un nouveau_bit
win_hash = (win_hash * base + new_bit) % mod

fenêtre[(idx + 1) % len(pattern)] = nouveau_bit
idx += 1
«» "

> **Python spécifique**
> * Le modulo est maintenu tout au long pour éviter le débordement sur de très longs cours d'eau (bien que les ints de Python ne soient pas liés).
> * `window` est un tampon circulaire (liste) pour tenir des mises à jour O(1).

---

*## 1.3 C++

'`cpp
***
* LeetCode 3023 – Trouver le modèle dans le flux infini I
* Auteur: ChatGPT
* Date: 2025-09-24
*
* L'implémentation utilise un hachage roulant (Rabin–Karp) sur un flux binaire.
*/

solution de classe {
public:
int findPattern(InfiniteStream& stream, vecteur const<int>& pattern) {
base longue = 2;
Const longue mod = 1'000'000'007LL;

int pLen = pattern.size();

- Oui. 1. Hash & base du modèle^(pLen-1) --------- */
longue patHash longue = 0;
longue basePow = 1; // base^(pLen-1) % mod
pour (int i = 0; i < pLen; ++i) {
PatHash = (patHash * base + motif[i]) % mod;
i (i < pLen - 1) basePow = (basePow * base) % mod;
}

- Oui. 2. Première fenêtre du flux --------- */
vector<int> window(pLen);
longue victoireHash = 0;
pour (int i = 0; i < pLen; ++i) {
bit int = stream.next();
window[i] = bit;
winHash = (winHash * base + bit) % mod;
}

int idx = 0; // index de départ de la fenêtre actuelle
alors que (vrai) {
si (winHash == patHash && egal(window.begin(), window.end(), pattern.begin()) {
retourner idx;
}

// Fenêtre de diapositives
int oldBit = fenêtre[idx % pLen];
Int nouveau Bit = stream.next();

// Supprimer la contribution de oldBit
winHash = (winHash - (oldBit * basePow) % mod + mod) % mod;
// Annexe Un peu
winHash = (winHash * base + newBit) % mod;

window[(idx + 1) % pLen] = nouveauBit;
++idx;
}
}
};
«» "

> **C++ Spécifiques**
> * `egal` de `<algorithme>` effectue une comparaison par octet pour exclure les collisions de hachage.
> * `InfiniteStream` est supposé fournir une méthode `int next()`; vous pouvez écrire un simple wrapper pour les tests unitaires.

---

- Oui. 2. Article du blog – Le bon, le mauvais, et le mauvais de trouver des modèles dans un flux infini

> **Mots-clés cibles* *
> `leetcode find pattern in infinith stream`, `rolling hash`, `kmp algorithme`, `binary stream`, `coding interview`, `job interview coding`, `Python rolling hash`, `Java KMP`, `C++ stream pattern`.

---

2.1 Introduction

> Je vais chercher un flux infini pour un modèle minuscule. (en milliers de dollars)
> C'est le cœur de **LeetCode 3023**. Alors que le problème semble simple, la torsion des données *infinies* nous force à repenser les stratégies de recherche de sous-chaînes typiques.
> Dans cet article nous allons marcher à travers les **naïve**, **rolling-hash**, et **KMP** approche, analyser leurs pros/cons, et vous donner une liste de contrôle pour as l'entrevue.

---

### 2.2 Énoncé du problème (réécrit)

- On vous donne un modèle **binaire** (pour une longueur de 0/1, ≤ 100).
- Oui. Vous avez accès à un objet `InfiniteStream` qui expose `int next()`; chaque appel vous donne le prochain morceau d'une séquence infinie 0/1.
- Retournez le **premier index de départ** où le motif apparaît dans le flux.
- Oui. Il est garanti qu'une correspondance existe dans les premiers bits `105`.

---

2.3 Fenêtre coulissante naïve

Idées Complexité Inconvénients
- C'est quoi ?
Autres Conservez une deque des derniers bits `p`; après chaque deque `next()` comparer avec le modèle====================================================================================================================================================================================================================================
Autres Pas de structures de données auxiliaires au-delà d'une petite file d'attente

**Pourquoi il échoue dans les interviews** – Les intervieweurs s'attendent à ce que vous pensiez aux solutions *temps-optimal*. Un scan linéaire est bien adapté à certains problèmes, mais avec la garantie `n=105` ils s'attendent à *O(n*) avec un travail de peritération minimal.

---

#### 2.4 Casse à roulettes (Rabin–Karp) – Le bon

Caractéristique Explication Raisonnement
C'est pas vrai.
Autres Traitez les bits comme des chiffres dans la base 2, calculez le hachage sur une fenêtre coulissante.
Module `1 000 000 007` (ou `2^63-1` avec long non signé) pour éviter les débordements
Vérifier la correspondance exacte lorsque les hachages coïncident.
**Circulaire tampon** pour la fenêtre

** À emporter** – Le hachage roulant est *la réponse attendue* pour un flux binaire avec `p` jusqu'à 100. Il est élégant, rapide, et met en valeur la connaissance de la chaîne de hachage*.

---

2.5 KMP – L'alternative

Idée Complexité
- C'est quoi ?
Autres Construisez la fonction d'échec du modèle; tandis que la lecture du flux avance le temps `O(n)` de l'état, `O(p)` espace. Autres
Autres Fonctionne pour n'importe quel alphabet.

**Quand choisir KMP**
- Oui. Si vous êtes codant dans **Java** ou **C++** et préférez rester dans le royaume de l'algorithme classique.
- Oui. Dans un entretien *emploi*, les intervieweurs peuvent explicitement demander : "Pouvez-vous résoudre cela avec KMP ? " pour tester votre ampleur algorithmique.

**Pourquoi on choisit habituellement de rouler le hachage sur KMP** –
- Le hachage en roulis correspond à la nature *stream* : vous n'avez jamais la chaîne complète en mémoire ; vous ne gardez que la fenêtre actuelle.
- Modulus arithmétique est bon marché en binaire et les échelles à n'importe quelle taille de l'alphabet (juste changer `base`).
- KMP nécessite un tableau *additionnel* (`pi`) mais nécessite toujours le même `next()` appels – les deux sont linéaires.

---

#### 2.6 Les collisions avec l'hash

Même si l'alphabet est binaire, les collisions de hash** sont théoriquement possibles (différentes fenêtres produisent le même hash).
**Attention* *
- Utiliser un *prime module* (`1 000 000 007` ou `2^61-1`).
- Effectuer une comparaison exacte lorsque le hachage correspond.
- Oui. Dans les entrevues, indiquez explicitement que nous nous préservons contre les collisions avec un contrôle; les collisions sont astronomiquement improbables. (en milliers de dollars)

---

2.7 Liste de contrôle pour la mise en œuvre

Il n'y a pas de problème.
- Oui.
**Expliquer clairement le problème** – Redire les contraintes
**Décrivez le modèle à flux infini** – vous pouvez stocker toute la chaîne.
**Choisir O(n)** temps – hachage enroulé ou KMP
**Afficher le temps constant par itération** – quelques opérations entières, sans boucles
**Guard contre les collisions de hachage** – vérifier le modèle quand le hachage correspond.
**Manipulation des modules et des débordements** – crucial pour Java & C++
**Mention le lien garanti (= 105)** – cela justifie O(n) mais aussi des indices d'optimisations possibles.

---

### 2.8 Exemple d'entrevue Pseudo-Code

Texte
1. Modèle de calcul Profil de Hash = [i] * base^(p-1-i) (mod M)
2. Construire la première fenêtre de taille p à partir du flux.
3. Pour chaque nouveau bit:
a. Shift hash: supprimer la contribution de bits le plus à gauche.
b. Ajouter un nouveau morceau.
c. Si le hachage correspond, comparez les bits pour la sécurité des collisions.
d. Indice de retour lorsqu'il est assorti.
«» "

---

####2.9 Pourquoi Rolling Hash gagne dans les scénarios d'entrevue

- **Minimal per-iteration work** – seulement deux opérations arithmétiques modulaires et une attribution de tableau.
- ** Séparation claire des préoccupations** – Le hachage est une composante autonome que vous pouvez tester indépendamment.
- **Language-agnostic** – la même idée fonctionne en Python, Java ou C++.
- **Handles flux infinis naturellement** – vous n'avez jamais besoin de rembobiner; vous continuez à glisser.

---

2.10 Pensées de clôture

- **LeetCode 3023** est un *substring-search* déguisé en problème de streaming.
- Le **good** est la clarté et l'efficacité de la solution de laminage-hash.
- Le **bad** est l'approche naïve qui ignore l'exigence de temps constant.
- Le **ugly** est le risque de collisions ou de débordement si vous n'utilisez pas un module ou une étape de vérification.

> **Takeaway** – Montrez à l'intervieweur que vous connaissez *tous les deux* les techniques rolling-hash et KMP, expliquez pourquoi vous avez choisi le premier pour un flux binaire infini, et confirmez l'exactitude par une comparaison rapide octet-by-octet. Ce niveau de rigueur transforme une recherche sous-chaîne simple en une réponse *d'entrevue stellaire*.

---

### 2.11 TL;DR (résumé d'une ligne)

> Pour LeetCode 3023, utilisez un hachage binaire **rolling** avec un module et un tampon circulaire ; l'algorithme fonctionne dans le temps O(n) et garantit la justesse même avec un flux infini. (en milliers de dollars)

---

Note finale

> Gardez cet article bookmarked et référez-vous chaque fois que vous êtes invité à rechercher des modèles dans les données de streaming – qu'il s'agisse de journaux binaires, de paquets réseau, ou de données de capteur.
> Bonne chance, et rappelez-vous : *L'entrevue n'est qu'un autre flux ; trouvez le modèle et partez. *

---

> **ENDE DE L'ARTICLE**
> (Nombre de mots : ~1 350 mots, sur mesure pour un blog LinkedIn/Coding‐Interview.)

---

- Oui. 3. Pensées finales

> Qu'il s'agisse du codage Java, Python ou C++, l'approche rolling-hash est une source unique de vérité** pour LeetCode 3023.
> Combinez-le avec un contrôle de collision et vous aurez une solution anti-balles qui fonctionne confortablement sous la limite `105` bit.
> Et si vous préparez des interviews de codage, gardez à l'esprit le cadre ** bon, mauvais, laid** – il vous aidera à présenter une solution concise et optimisée à chaque fois.