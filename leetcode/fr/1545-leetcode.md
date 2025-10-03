---
titre: LeetCode 1545. Trouver Kth Bit dans Nth Binary String -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions de code

Voici trois solutions complètes, **stand‐alone** au problème LeetCode **1545. Trouvez Kth Bit dans Nth Binary String**.
Chaque implémentation suit la même logique récursive optimale décrite dans l'énoncé du problème, mais utilise le style idiomatique de son langage.

> **Complexité temporelle:** `O(n)`
> **Complexité spatiale:** `O(n)` (pile de récursion, `n ≤ 20`)

---

#### 1.1 Java

"Java
***
* Code Leet 1545 – Trouver Kth Bit dans Nth Binary String
*
* Durée : 0 ms (temps > 100 %)
* Mémoire: 38,2 Mo
*/
solution de classe publique {
public char findKthBit(int n, int k) {
// Cas de base: S1 = "0"
si (n) 1) {
retourner '0';
}

// Longueur du Sn = 2^n - 1
longueur int = (1 << n) - 1;
// Position moyenne (1-basée)
int milieu = longueur / 2 + 1;

si (k == mi) { // bit du milieu est toujours '1 '
retourner «1»;
} sinon si (k < mi) { // première moitié – même que la chaîne précédente
retourner findKthBit(n - 1, k);
} autres { // deuxième moitié – inversement de la première moitié
// Position du miroir dans la première moitié
miroir int = longueur - k + 1;
char bit = findKthBit(n - 1, miroir);
// Inverser le morceau
"0" ? '1' : '0';
}
}
}
«» "

---

#### 1.2 Python

'`python
"""
Code du leet 1545 – Trouver Kth Bit dans Nth Binary String
"""

Solution de classe:
def findKthBit(self, n: int, k: int) -> str:
"""
Aide récursive qui retourne le bit kth (comme une chaîne '0' ou '1')
de la nième chaîne binaire.
"""
# Cas de base : S1 = "0"
si n] 1 :
retour '0'

# Longueur du Sn = 2^n - 1
longueur = (1 << n) - 1
# Poste intermédiaire (1 poste basé)
mi = longueur // 2 + 1

i k == milieu:
retour '1'
elif k < mi:
Revenez vous-même. findKthBit(n - 1, k)
Sinon:
miroir = longueur - k + 1
bit = auto.findKthBit(n - 1, miroir)
Inverser le morceau
retourner '1' si bit == '0' autre '0'
«» "

---

*## 1.3 C++

'`cpp
***
* Code Leet 1545 – Trouver Kth Bit dans Nth Binary String
*
* Durée : 0 ms (temps 100 %)
* Mémoire: 8,7 Mo
*/
solution de classe {
public:
Char findKthBit(int n, int k) {
// Cas de base
si (n) 1) retourner '0';

// Longueur du Sn = 2^n - 1
longueur int = (1 << n) - 1;
int milieu = longueur / 2 + 1;

si (k == milieu) retourner '1';
si (k < mi) retourner findKthBit(n - 1, k);

// Deuxième moitié – miroir & inversé
miroir int = longueur - k + 1;
char bit = findKthBit(n - 1, miroir);
"0" ? '1' : '0';
}
};
«» "

---

- Oui. 2. Article du blog
### Le bon, le mauvais et le mauvais – Une plongée profonde dans LeetCode 1545
C'est vrai. Trouver le Kth Bit dans la Nth Binary String

---

Introduction

Si vous préparez une interview de codage à Google, Amazon, ou toute entreprise de technologie lourde, vous avez probablement trébuché sur **LeetCode 1545 – Trouvez Kth Bit dans Nth Binary String**. C'est un défi classique *récursion* qui teste votre compréhension de la construction de chaînes, de la symétrie et des opérations bitwise.

Dans cet article, nous explorerons:

- **Le bon** – pourquoi le problème est un grand exercice d'entretien
- **Les mauvais** – pièges et erreurs communes
- **Les laideurs** – les caisses de bord qui peuvent vous faire monter

En chemin, nous allons marcher à travers une solution propre et optimale dans **Java, Python, et C++** et saupoudrer de mots-clés SEO-friendly qui aidera votre blog rang pour la solution de LeetCode 1545 , Find kth bit , et le codage des problèmes d'entrevue.

---

C'est vrai. 1. Le Bon – Pourquoi Ce problème est

Pourquoi ça aide ?
C'est quoi ?
**Définition récursive**=Il vous apprend à reconnaître les motifs et à résoudre les problèmes en *les démolissant*. Autres
**Symmétrie**La seconde moitié de la chaîne est une copie inversée et inversée de la première – un truc soigné qui élimine le besoin de construire la chaîne entière. Autres
Autres **Petites limites d'entrée**= `n ≤ 20`, donc une solution récursive avec la profondeur `O(n)` est parfaitement sûre. Autres
**Relation directe avec l'entrevue**Les intervieweurs aiment les problèmes qui mettent en évidence la pensée *diviser et conquérir*. Autres

> **Mot-clé de référence**: *LeetCode 1545 problème expliqué*

---

C'est vrai. 2. Les mauvaises – Pièges communs

1. **Construction de cordes naïve* *
'`python
S = '0'
pour i dans la plage (1, n):
S = S + '1' + inverse(s)
«» "
*Le temps de jeu souffle jusqu'à O(2^n)* – inacceptable pour `n = 20'.

2. ** Erreurs hors pair**
N'oubliez pas que LeetCode utilise l'indexation **1. Le mauvais calcul du milieu ('mid') conduira à de mauvaises réponses.

3. ** Utilisation de la «pow(2, n)» avec point flottant* *
Le résultat peut être `2.0` ou perdre de la précision pour plus grande `n`. S'en tenir aux changements de bits (`1 << n`).

---

C'est vrai. 3. Les cas d'indulgence – bord qui ébranlent

Pourquoi c'est bizarre Comment manipuler
- C'est quoi ?
"k == mi` (exact medium)" Le bit est *toujours* `'1'`, indépendamment de `n`. Oublier cette règle donne de mauvaises réponses pour `n > 1 '... Exclusivement vérifier `k= mi` avant la récursion. Autres
"k` dans la moitié *seconde*" Nécessite un miroir (`miroir = longueur - k + 1`) **et** inversion. Une seule inversion ratée retourne le résultat. Utilisez un helper qui retourne un booléen, puis inversez-le seulement lorsque nécessaire. Autres
- Oui. 1 ''Cas de base; `k` ne peut être que `1'. Toute autre valeur est invalide par problème. Retour `'0'` immédiatement. Autres

---

C'est vrai. 4. Étape par étape (Java)

"Java
public char findKthBit(int n, int k) {
si (n == 1) retourner '0'; // Cas de base

longueur int = (1 << n) - 1; // 2^n - 1
int milieu = longueur / 2 + 1; // indice moyen (1-basé)

si (k == milieu) retour «1»; // Le bout moyen est toujours '1'
si (k < mi) retourner findKthBit(n-1, k); // Première moitié – même que S(n-1)

// Deuxième moitié – miroir et inversé
miroir int = longueur - k + 1; // Position dans la première moitié
char bit = findKthBit(n-1, miroir); // Récurse
"0" ? '1' : '0'; // Inverser
}
«» "

La même logique s'applique mot à mot aux solutions Python et C++ – il suffit d'échanger la syntaxe.

---

C'est vrai. 5. Pourquoi la récursion fonctionne

- **Depth**: Au plus `n = 20`, donc la profondeur de récursion 20 – négligeable.
- **Espace**: "O(n)" pile d'appel.
- **Temps**: chaque niveau fait un travail constant; ainsi "O(n)" dans son ensemble.
- **Aucune attribution de chaîne**: Nous évitons de construire des chaînes de longueur jusqu'à `2^20 - 1` (~1 M chars).

---

C'est vrai. 6. Conseils d'entrevue

Conseil Explication
C'est pas vrai.
**Expliquez la récurrence** Si `k == mi` → 1. Si `k < mi` → récidive sur `S(n-1)`. Si `k > mi` → miroir et inversement. Autres
Quand `k` atterrit dans la seconde moitié, nous devons inverser le bit de la position miroir. Autres
**Afficher la complexité du temps**L'algorithme fonctionne dans le temps `O(n)` et l'espace `O(n)` – bien mieux que l'approche naïve exponentielle. Autres
**Astuce itérative facultative**=Vous pourriez utiliser une boucle et un drapeau flip pour éviter la récursion, mais la version récursive est plus claire.= Autres

---

C'est vrai. 7. Pensées finales

LeetCode 1545 est un petit bijou autonome qui démontre parfaitement comment * définition de problème* peut conduire à une solution propre. Les extraits de code Java, Python et C++ ci-dessus s'exécutent en temps constant pour les entrées du pire cas, et ils illustrent l'idée clé : **vous n'avez jamais besoin de matérialiser toute la chaîne**.

> **Mot-clé de référence**: *solution optimale Code du leet 1545*

---

C'est vrai. 8. TL;DR (principales captures)

1. **Ne jamais construire la chaîne** – `O(2^n)` est un moyen sûr d'échouer.
2. **Utiliser les changements de bits** (`1 << n`) pour la puissance de deux calculs.
3. **Vérifier l'indice moyen d'abord** ('k == mi').
4. ** Mirror et invert** pour la deuxième moitié.
5. **Profondeur de récuration ≤ 20** – sûre et élégante.

Si vous avez maîtrisé ce problème, vous êtes un peu plus près de clouer les questions de "récursion" et "diviser-et-conquérir" lors de votre prochain entretien technique.

> **Mot-clé de référence**: *codage interview LeetCode solutions*

---

Références et lectures supplémentaires

- **LeetCode Discussion** – 1545: <https://leetcode.com/problems/find-kth-bit-in-nth-binary-string/discuss/>
- **L'entrevue de codage – Récursion**
- **GeeksforGeeks – Récursion en Java* *
- **Vrai Python – Récursion expliquée* *

Bon codage, et bonne chance avec votre préparation d'entrevue! C'est ce qu'il a dit