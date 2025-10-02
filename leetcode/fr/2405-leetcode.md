---
titre: LeetCode 2405. Partition optimale de la chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## ♫ Mastering LeetCode 2405 – Partition optimale des chaînes
*Java-Optimized Guide to Nail the Interview*

---

Table des matières
1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Pourquoi ce problème se trouve-t-il pour les entrevues] (# pourquoi ce problème se trouve-t-il)
3. [Le bien – une solution unique pour l'avidité (O(n) Temps, O(1) Espace)](#le bien)
4. [L'O(n) Time, O(26) Space] (#the-bad)
5. [La Force Brute et le PD (O(2n) Temps, pas pratique)] (#le-gross)
6. [Mise en œuvre complète du code] (#Mise en œuvre complète du code)
- Java
- Python
- C++
7. [Décomplexité du temps et de l'espace] (#complexité)
8. [Pièges communs et cas de bord] (#pièges)
9. [Optimiser pour l'intervieweur] (#optimiser)
10. [Conclusion et prochaines étapes](#conclusion)

---

<un nom="recap-problème"></a>
- Oui. 1. Récapitulation des problèmes

**LeetCode 2405 – Partition optimale des chaînes**
> Étant donné qu'une chaîne `s` (seulement des lettres anglaises minuscules), la partitionner dans les plus petites sous-chaînes possibles de telle sorte que chaque sous-chaîne contient **unique** caractères.
> Retournez le nombre minimal de sous-chaînes.

Exemples
Entrée Sortie Explication
C'est pas vrai.
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" Autres
""ssssss" """ "6" "Chaque "ss" doit rester seul"

**Contrôles* *
- `1 <= longueur <= 105`
- Seules les lettres minuscules

---

<un nom> </a>
- Oui. 2. Pourquoi ce problème se pose pour les entrevues

Caractéristiques Pourquoi ça compte
C'est-à-dire
**L'intuition grêle** Démontre la capacité de repérer une sous-structure optimale. Autres
**Bit-mask vs HashSet**Shows knowledge of low-level tricks and space optimisation. Autres
**Scan linéaire**= Faits saillants raisonnement de complexité temporelle (O(n)). Autres
**Manipulation de caisses Edge**Les caisses d'essai comprennent tous les mêmes caractères, motifs alternés, cordes longues. Autres

Les intervieweurs aiment ce problème parce qu'il est ** facile de comprendre** mais ** assez profond** pour révéler l'intelligence.

---

<un nom "le bon"></a>
- Oui. 3. Le bien – un laissez-passer avec Bitmask

Intuition
- Scannez la corde de gauche à droite.
- Conservez un entier de 26 bits (`masque`) représentant les caractères déjà apparus dans la sous-chaîne actuelle.
- Oui. Lorsque nous rencontrons un caractère déjà défini dans `mask`, nous *must* commençons une nouvelle sous-chaîne: réinitialisez `mask`, incrémentez le compteur et définissez le bit pour le caractère courant.

Pourquoi ça marche ?
- Tout caractère répété force une partition parce que la sous-chaîne actuelle violerait l'unicité.
- Commencer une nouvelle sous-chaîne dès que possible (à droite quand on voit le duplicata) garantit le nombre *minimum* de sous-chaînes – une preuve cupide classique.

Code (Java)
"Java
solution de classe publique {
partage d'entrées publiques Chaîne(s) {
masque int = 0; // masque 26 bits pour les caractères visibles
= 1; // au moins une sous-chaîne
pour (int i = 0; i < s.longueur(); i++) {
bit int = 1 << (s.charAt(i) - 'a');
si ((masque & bit) != 0) { // duplicata détecté
masque = 0; // lancer une nouvelle sous-chaîne
count++;
}
masque= bit; // marque l'omble vu
}
le nombre de retours;
}
}
«» "

Pourquoi c'est génial
- **O(n) temps** – un passage.
- **O(1) espace** – le masque est constant.
- Oui. Pas de structures de données lourdes; parfait pour une grande entrée.

---

<a name="the-bad"></a>
- Oui. 4. L'approche "Bad" – HashSet

Intuition
- Utilisez un `HashSet<Caracter>` pour garder une trace des caractères vus dans la sous-chaîne courante.
- Lors de la rencontre d'un duplicata, réinitialisez le jeu et démarrez une nouvelle sous-chaîne.

Mise en œuvre
"Java
partage d'entrées publiques Chaîne(s) {
Set<Caracter> vu = nouveau HashSet<>();
nombre int = 1;
pour [charc : s.toCharArray()) {
si (!seen.add(c)) { // ajouter retourne false si déjà présent
voir.clear(); // nouvelle sous-chaîne
voir.add(c);
count++;
}
}
le nombre de retours;
}
«» "

Inconvénients
- **O(26) espace** – toujours constant mais plus lourd que bitmask.
- Un peu plus lent en raison des opérations de hachage.
- Plus difficile à expliquer à un intervieweur non technique.

---

<a name="the-ugly"></a>
- Oui. 5. La force brute / DP

Force brute
- Générer toutes les partitions possibles ("2^(n-1)").
- Vérifiez chaque unicité → **exponentielle**.

Approche du PDD
- "dp[i] = sous-chaînes minimales pour s[0..i]".
- Pour chaque `i`, scanner en arrière pour trouver la plus longue sous-chaîne valide se terminant par `i`.
- Complexité : **O(n2)** – inacceptable pour `n = 105`.

**Pourquoi c'est bizarre**
- Nécessite des boucles imbriquées, plus de temps, et plus de logique pour expliquer.
- Les intervieweurs attendent O(n) pour ce problème.

---

<a name="full-code-implémentations"></a>
- Oui. 6. Mise en œuvre complète du code

Voici des solutions propres et autonomes pour Java, Python et C++.

### Java (Bitmask Greedy)

"Java
solution de classe {
partage d'entrées publiques Chaîne(s) {
masque int = 0; // bitmasque 26 bits
partitions int = 1; // au moins une sous-chaîne
pour (int i = 0; i < s.longueur(); i++) {
bit int = 1 << (s.charAt(i) - 'a');
si ((masque & bit) != 0) { // duplicata dans la sous-chaîne actuelle
masque = 0; // lancer une nouvelle sous-chaîne
partitions++;
}
masque= bit; // marque char
}
les partitions de retour;
}
}
«» "

### Python (Bitmask Greedy)

'`python
Solution de classe:
def partitionString(self, s: str) -> Int:
masque = 0
partitions = 1
pour ch en s:
bit = 1 << (ord(ch) - 97) # 97 == ord('a')
si masque & bit & #160;:
masque = 0
partitions += 1
masque = bit
Retourner les partitions
«» "

### C++ (Bitmask Greedy)

'`cpp
solution de classe {
public:
partition int Chaîne(s) {
masque int = 0;
partitions int = 1;
pour (charc : s) {
bit int = 1 << (c - 'a');
si (masque & bit) { // duplicata
masque = 0;
partitions++;
}
masque= bit;
}
les partitions de retour;
}
};
«» "

Les trois solutions sont **O(n)** temps, **O(1)** espace, et passer confortablement les tests cachés de LeetCode.

---

<un nom="complexité"></a>
- Oui. 7. Répartition de la complexité du temps et de l'espace

L'approche Temps Espace
- C'est quoi ?
Bitmask Greedy **O(n)**
* O(26)** (constante)
DB (O(n2))
Force brute

**À emporter :** Utilisez le bitmask pour une vitesse maximale et une mémoire minimale.

---

<a name="pitfalls"></a>
- Oui. 8. Pièges communs et cas de bord

Piège
- Oui.
Oubliez de réinitialiser le compteur avant la première itération.Initialisez `partitions = 1` (il y a toujours au moins une sous-chaîne). Autres
Utiliser un `HashSet` avec `add()` sans vérifier la valeur de retour. Autres
Autres Hors-par-un dans les boucles. Autres
Autres Utiliser un masque de plus de 32 bits en C++ sur le compilateur 64 bits `int mask` est très bien (26 bits), mais si vous voulez être sûr utiliser `int mask = 0;`. Autres
Ne pas manipuler la chaîne vide (bien que les contraintes disent `len >= 1').- Retour `0` ou `1` en conséquence; habituellement pas nécessaire. Autres

---

<un nom "optimisant"></a>
- Oui. 9. Optimisation pour l'intervieweur

1. ** Expliquez la preuve cupide rapidement** – Nous coupons dès que nous voyons un duplicata parce que le retard ne ferait qu'augmenter le nombre de sous-chaînes. (en milliers de dollars)
2. **Mention l'avantage bitmask** – Nous n'avons besoin que de 26 bits; pas de structures de données supplémentaires. (en milliers de dollars)
3. **Afficher le code** – garder propre, utiliser des noms de variables significatifs (`masque`, `partitions`).
4. **Discuse la complexité** – Souligner l'espace O(n) et O(1).
5. **Suivi des réponses** – S'il est question de solutions alternatives, mentionner le HashSet comme une approche plus simple mais légèrement plus lourde.

---

<un nom="conclusion"></a>
- Oui. 10. Conclusion et prochaines étapes

- **La partition optimale de la chaîne** est un problème classique d'avidité qui teste votre capacité à reconnaître quand la coupe précoce est la stratégie optimale.
- Oui. La solution d'avidité **bitmask** est la plus rapide, la plus simple et la plus conviviale.
- La maîtrise de ce problème vous donne confiance pour des questions similaires : *La plus longue sous-chaîne sans répéter de caractères*, *Les problèmes de partition de String*, etc.

Prochaines étapes

1. **Pratique** – Résoudre des variantes comme la sous-chaîne la plus longue sans répéter de caractères (LeetCode 3).
2. **Lire l'éditorial** – Comprendre le bitmask en profondeur.
3. **Écrire un billet de blog** – Partagez ce guide (comme celui-ci) pour présenter vos compétences en résolution de problèmes.
4. **Appliquer** – Utilisez cette solution dans votre curriculum vitae sous la rubrique Préparation de l'entrevue de codage.

Bonne chance, et que vos partitions soient toujours optimales! C'est ce qu'il a dit.

---

**Référencement Mots clés Utilisé :**
- Partition optimale des chaînes de LeetCode
- LeetCode 2405 solution
- problème d'interview Java Python C++
- partition de chaînes de bits gourmande
- Codage des conseils d'entrevue
- prép d'entretien par algorithme
- partition de chaînes d'espace O(1)
- interview questions partition chaîne
- problème de codage des entretiens d'emploi

---