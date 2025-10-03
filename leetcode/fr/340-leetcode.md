---
titre: LeetCode 340. Substring le plus long avec au plus K caractères distincts - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 340 – Substring le plus long avec au plus K Distinct Personnages
> **Mots clés**: LeetCode 340, Fenêtre coulissante, HashMap, solution O(n), Java, Python, C++, Préparation d'entrevue, Algorithme, Structures de données

---

Aperçu du problème

- **Titre**: Substring le plus long avec au plus K Distinct Personnages
- **Difficulté**: Moyenne
- **Input**:
- `s`: une chaîne de longueur `1 ≤=2 ≤5·104`
- `k`: un entier `0 ≤ k ≤ 50`
- **Output**: Longueur de la plus longue sous-chaîne contiguë qui contient **pas plus de** `k` caractères distincts.

> **Exemple**
> `s = "eceba", k = 2 3` * (sous-chaîne = "ece")*

---

Pourquoi ce problème est important

- **Interview Gold-Mine**: Cette question teste votre capacité à penser en temps *O(n*), à utiliser des techniques à deux pointeurs et à gérer efficacement le nombre de fréquences.
- **Piège commun**: les solutions Brute-force O(n2) ou O(n3) obtiennent TLE sur les grandes entrées.
- **Compétences transferables**: Fenêtre coulissante, utilisation de la carte de hachage, manipulation de pointeur – tous les éléments essentiels de la conception du système et du codage réel.

---

L'approche classique du vent

Idée

Maintenez une fenêtre `[gauche, droite]` telle que la sous-chaîne `s[gauche..droite]` contient au plus des caractères distincts `k`.
- Étendre le "droit" une étape à la fois.
- Lorsque l'ajout d'un nouveau caractère fait que le nombre de caractères distincts dépasse `k`, réduire la fenêtre de gauche jusqu'à ce que l'état soit rétabli.

- Oui. Structure des données

Une carte de fréquence (`HashMap` / `unordered_map` / `collections. Counter`) suit combien de fois chaque caractère apparaît dans la fenêtre actuelle.

C'est vrai. Étapes

Étape Action Complexité
C'est quoi, ça ?
Autres Initialiser `gauche = 0`, `maxLen = 0`, carte vide.
Autres 2=Iterate `right` de 0 à n‐1.= O(n)=
Autres Engourdissement du "s[right]".
Autres Alors que la taille de la carte > k: décrément freq de `s[left]`, supprimer si zéro, `left++`.
Mise à jour "maxLen = maxLen, droite - gauche + 1)".
Retour `maxLen`.

Temps total `O(n)`, espace `O(k)` (faible cas lorsque tous les caractères sont distincts et `k = 50`).

---

## La force de Brute Naïve

- Énumérer toutes les sous-chaînes: temps `O(n2)`, espace `O(1)` pour le comptage avec un `Set`.
- Oui. Ou utilisez une boucle imbriquée et maintenez un tableau de fréquence pour chaque sous-chaîne: toujours `O(n2)`.

**Résultat**: Fails sur 5·104 chaînes de longueur – 2,5 milliards de sous-chaînes → TLE.

---

Le mess des bords

Cas de bord Qu'est-ce qui peut mal tourner ? Correction
-- -- -- -- -- -- -- -- -- -- -- -- --
- Oui. 0'- Aucune sous-chaîne autorisée → réponse Poignée tôt. Autres
Une chaîne vide devrait revenir Retour précoce. Autres
Autres Tous les caractères sont identiques. Fonctionne bien, mais regarde la taille de la carte jamais > k. Autres
`k >= nombre de caractères uniques dans s`= La chaîne entière est valide. Autres Fonctionne automatiquement, mais il est toujours bon de vérifier le retour anticipé si désiré. Autres

---

Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

---

### Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
durée de vie publique DeLongestSubstringKDistinct(String s, int k) {
si (k=0=0=0=0=0=0=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=2=1=1=1=1=1=1=1=

Int gauche = 0, maxLen = 0;
Carte<Caractère, entier> freq = nouvelle HashMap<>();

pour (int droite = 0; droite < s.longueur(); droite++) {
char r = s.charAt(à droite);
freq.put(r, freq.getOrDefault(r, 0) + 1);

pendant que (freq.size() > k) {
char l = s.charAt(gauche++);
nombre int = freq.get(l) - 1;
si (compter) 0) supprimer(l);
autres freq.put(l, nombre);
}

maxLen = Math.max(maxLen, droite - gauche + 1);
}
retour maxLen;
}
}
«» "

---

Python 3

'`python
de collections importer par défautdict

Solution de classe:
def length OfLongestSubstringKDistinct(self, s: str, k: int) -> Int:
Si k == 0 ou non s:
retour 0

gauche = 0
max_len = 0
freq = defaultdict(int)

pour droite, omble dans le ou les énuméré(s):
[char] += 1

pendant que len(freq) > k:
freq[s[gauche]] -= 1
si freq[s[gauche]] 0:
del freq[s[gauche]]
gauche += 1

max_len = max(max_len, droite - gauche + 1)

_retourner maxlen
«» "

---

C++

'`cpp
#inclut <non-ordonné_map>
#incluez <string>
#incluez <algorithme>

solution de classe {
public:
longueur intOfLongestSubstringKDistinct(suite std::string& s, int k) {
si (k) 0.vide() retourne 0;

std::unordered_map<char, int> freq;
Int gauche = 0, maxLen = 0;

pour (int right = 0; right < static_cast<int>(s.size()); ++right) {
freq[s[right]]++;

pendant que (freq.size() > static_cast<size_t>(k)) {
si (--freq[s[gauche]]] 0)
freq.erase(s[gauche]);
+ + gauche;
}

maxLen = md:maxLen, droite - gauche + 1;
}
retour maxLen;
}
};
«» "

---

Le fonctionnement du code (étape par étape)

1. **Initialisation** – `left` pointe au début de la fenêtre actuelle, `maxLen` enregistre la meilleure longueur trouvée, `freq` stocke le nombre de caractères.
2. **Extend** – Pour chaque `droit`, ajouter le caractère à `freq`.
3. **Contract** – Bien que nous ayons trop de caractères distincts, rétrécir la fenêtre de la gauche : diminuer le nombre, supprimer si zéro et déplacer `gauche`.
4. **Mise à jour** – Après chaque extension, la fenêtre est valide. Mettre à jour `maxLen` si la fenêtre actuelle est plus grande.
5. **Retour** – Après la boucle, `maxLen` tient la longueur de la plus longue sous-chaîne.

---

Analyse de complexité

Métrique
- C'est quoi ?
Temps **O(n)**
Espace **O(k)**
*n* ===================================================

*Pourquoi O(k) espace? *
La carte de fréquence ne contient jamais plus de touches `k+1` (une fois qu'elle dépasse `k`, nous rétrécissons).

---

Erreurs courantes et comment éviter Eux

Erreurs dans les résultats
- C'est quoi ?
Oubliez de manipuler `k == 0`.. Retourne une mauvaise longueur non nulle.
Utiliser `HashSet` au lieu de la carte de fréquence
Mise à jour `maxLen` avant la passation de contrat
Erreurs hors-par-un dans la taille de la fenêtre

---

Autres optimisations

Quand utiliser l'effet
C'est pas vrai.
**Two-Pointer (déjà utilisé)**
**Pré-allocate Array pour ASCII**= Les cordes sont ASCII== Accès à temps constant plus rapide que HashMap=
**Éviter `HashMap.getOrDefault` en Java 8+**=Critical de performance== Utiliser `compute` ou `merge` pour un code concis==

> *Astuce* : Pour les intervieweurs qui apprécient **clarité sur les micro-optimisations**, l'approche HashMap/Counter est idéale. Pour les systèmes de production, un tableau (taille 256) peut raser quelques microsecondes.

---

Suite d'essais (Python)

'`python
test unitaire d'importation

classe TestLongestSubstring(unittest). Cas d'essai:
def setUp(self):
Self.sol = Solution()

def test_examples(self):
Self.assertEqual(self.sol.longueurDeLongestSubstringKDistinct("eceba", 2), 3)
Self.assertEqual(self.sol.longueurDeLongestSubstringKDistinct("aa", 1), 2)

def test_edge_cases(self):
Self.assertEqual(self.sol.longueurDeLongestSubstringKDistinct("", 0), 0)
Self.assertEqual(self.sol.longueurDeLongestSubstringKDistinct("abc", 0), 0)
Self.assertEqual(self.sol.longueurDeLongestSubstringKDistinct("abc", 5)
Self.assertEqual(self.sol.length OfLongestSubstringKDistinct("a", 1), 1)

def test_large(self):
s = "a" * 50000
Self.assertEqual(self.sol.longueurDeLongestSubstringKDistinct(s, 1), 50000)

si __nom__ == "__main__" :
unitétest.main()
«» "

Exécuter `python3 test.py` pour assurer une couverture de 100%.

---

À emporter – Ce que les recruteurs recherchent

1. **Correctness** – Poignée tous les cas de bord.
2. **Efficacité du temps et de l'espace** – temps O(n), espace O(k).
3. **Clean Code** – Noms de variables clairs, gardes précoces, plaque minimale de chaudière.
4. **Problème–Solving Mindset** – Reconnaître la fenêtre coulissante comme l'ajustement naturel.

> *Conseil de préparation à l'emploi* : Pratique expliquant votre solution à haute voix. Les intervieweurs adorent des explications concises et bien structurées qui mettent en lumière la perspicacité algorithmique et les compromis.

---

Mot final

Levet Le code 340 est un problème classique de fenêtre coulissante qui peut être résolu en temps linéaire. En maîtrisant ce modèle, vous êtes non seulement préparé pour cette question spécifique, mais également équipé pour une foule de problèmes d'entrevue impliquant des sous-chaînes, des sous-arrays et des contraintes de fréquence.

Bon codage, et que votre prochaine interview appelle la classe `Solution` que vous venez d'écrire! C'est ce qu'il a dit