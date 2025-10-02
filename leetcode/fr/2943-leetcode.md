---
titre: LeetCode 2943. Maximiser la zone du trou carré en grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Le bon, le mauvais et le mauvais de **LeetCode 2943 – Maximiser la zone du trou carré* *
*Un guide concis et prêt à servir de référence pour aider les recruteurs à vous voir comme un candidat de premier plan. *

---

- Oui. 1. Récapitulation des problèmes

On vous donne une grille de lignes `n` et de colonnes `m`.
Les barres horizontales sont placées entre les lignes et les barres verticales entre les colonnes.
Une barre peut être **supprimée** seulement si elle se trouve à côté d'une autre barre enlevée; sinon la barre reste intacte.

Lorsqu'un bloc de barres horizontales consécutives est enlevé, les rangées adjacentes de cellules fusionnent et vous obtenez **une rangée supplémentaire de cellules** pour chaque barre enlevée.
La même logique s'applique aux barres verticales.

**Objectif:**
Trouvez le plus grand *carré* qui peut être formé après avoir enlevé le bloc optimal de barres, et retourner sa zone.

> **Numéro de code de débit**: 2943
> **Tags**: Arrayage, tri, deux points, question d'entrevue

---

- Oui. 2. Intuition (Le Bien)

1. **Désolé**
Le tri de chaque liste de barres rend les barres consécutives faciles à repérer.

2. **Compte de poursuite**
Une séquence de barres amovibles `k` donne des cellules `k + 1` dans cette direction.
*Exemple*: `[2,3]` → deux barres consécutives → hauteur = 3 cellules.

3. **Longueur du côté**
Un carré ne peut croître que jusqu'à la plus petite des deux dimensions.
Texte
côté = min(maxConsécutive(barres horizontales),
maxConsecutive(barres verticales)) + 1
«» "

4. **Zone**
"zone = côté * côté".

Parce que l'entrée garantit au moins une barre dans chaque liste, la longueur minimale consécutive est toujours **≥ 1**, donc la formule fonctionne pour tous les cas de bord.

---

- Oui. 3. Les pièges (les mauvais)

Pourquoi ça arrive Comment l'éviter
-- -- -- -- -- -- -- --
**Ignorer le nombre de Les gens pensent que la zone est simplement `min(maxConsecutive)`2. Autres
La vérification de tous les intervalles conduit à un temps quadratique. Trier une fois et scanner linéairement – O(n log n). Autres
**Les erreurs hors-par-un dans le scan**=Le démarrage `cur` à 0 ou 2 peut faire erreur. Initialiser `cur = 1` et mettre à jour `max_len` quand une pause se produit. Autres
**Ne pas gérer la dernière série**La boucle pourrait oublier la séquence finale. Mettre à jour `max_len` après la fin de la boucle. Autres

---

- Oui. 4. L'Ugly (Trick d'optimisation)

La solution la plus simple bat déjà 99 % des soumissions en pratique.
Si vous voulez raser quelques millisecondes sur des cas de test massifs, utilisez un **pass unique lambda** (C++/Python) ou une fonction **inner helper** (Java) qui fonctionne directement sur le vecteur/référence au lieu de copier.
Cela élimine la copie de tableau supplémentaire qu'un «vecteur<int> copie = arr» naïve créerait.

---

- Oui. 5. Complexité algorithmique

Étape Temps Espace
C'est pas vrai.
Classer `hBars`.
Numérisation `hBars`
Trie `vBars`.
Numérisation "vBars"
* Total******O(h log h + v log v)**

(« h » = « hBars », « v » = « vBars »)

---

- Oui. 6. Mises en œuvre en plusieurs langues

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
Tous suivent la même logique: trier, trouver la plus longue série consécutive, calculer le côté, zone de retour.

---

#### 6.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
l'intérêt public Zones carrées (int n, int m, int[] hBars, int[] vBars) {
int maxH = maxConsécutive(hBars);
int maxV = maxConsécutive(vBars);
côté int = Math.min(maxH, maxV) + 1;
côté retour * côté;
}

Int privé maxConsecutive(int[] arr) {
Tableau 3.
l'ent maxLen = 1, cur = 1;
pour (int i = 1; i < arr.longueur; i++) {
si (arr[i]) [i - 1] + 1) {
cur++;
} autre {
maxLen = Math.max(maxLen, cur);
cur = 1;
}
}
maxLen = Math.max(maxLen, cur);
retour maxLen;
}
}
«» "

---

#### 6.2 Python 3

'`python
def maximumSquareHoleZone(n: int, m: int, hBars: list[int], vBars: list[int]) -> Int:
def max_consecutive(arr: list[int]) -> Int:
arr.sort()
max_len = cur = 1
pour i dans la plage (1, len(arr)):
si arr[i] == [i - 1] + 1:
pour 1
Sinon:
max_len = max(max_len, cur)
cur = 1
retour max(max_len, cur)

côté = min(max_consecutive(hBars), max_consecutive(vBars)) + 1
côté retour * côté
«» "

---

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maximum Zone carrée (int n, int m, vecteur<int>& hBars, vecteur <int>& vBars) {
Auto maxConsecutive = [](vecteur<int>& arr) {
tri(arr.begin(), arr.end());
Int max_len = 1, cur = 1;
pour (size_t i = 1; i < arr.size(); ++i) {
si (arr[i]) [i - 1] + 1) {
++cur;
} autre {
max_len = max(max_len, cur);
cur = 1;
}
}
retour max(max_len, cur);
};

côté int = min(maxConsécutive(hBars), maxConsécutive(vBars)) + 1;
côté retour * côté;
}
};
«» "

---

- Oui. 7. Pourquoi cela gagne dans les entrevues

- **Simplicité** – Tri + passe simple est immédiatement compréhensible.
- **Time‐Efficace** – O(n log n) bat l'approche quadratique de la force brute.
- **Langue Agnostique** – Vous pouvez écrire la même logique en Java, Python ou C++, démontrant ainsi sa capacité d'adaptation.
- **Connaissance des cas** – Manipulation correcte des barres non consécutives.
- **Scalable** – Fonctionne pour les tailles d'entrée maximales autorisées par LeetCode.

---

- Oui. 8. SEO et renforcement du recrutement

- **Mots-clés cibles**:
*La zone maximale du trou carré* *LeetCode 2943*, *les barres de grille*, *l'algorithme à deux points*, *l'entrevue de codage*, *les solutions Java Python C++*, *les questions d'entrevue technique*, *les conseils d'entrevue de l'ingénieur logiciel*.

- **Description de la Meta (155 caractères)* *
*Découvrez comment résoudre LeetCode 2943 – Maximiser la zone du trou carré – en Java, Python et C++. Un guide étape par étape qui couvre le bon, le mauvais et laid de l'algorithme, parfait pour votre prochaine entrevue de codage. *

- **En-têtes**
- "# Maximiser la zone du trou carré (Code Leet 2943) – Java / Python / Solutions C++ "
- Oui. Le bon : tri simple + balayage linéaire "
- Oui. Les mauvaises: les pièges communs et comment les éviter "
- Oui. L'horrible : Traces de cas et erreurs hors-par-un "

- **Appels à l'action**
- *Si cette solution a aidé, donnez-lui un pouce! *
- Besoin d'un autre entretien ? Abonnez-vous à notre newsletter! *
- *Show recruteurs vous pouvez résoudre 2943 en plusieurs langues – ajoutez ceci à votre portfolio. *

---

- Oui. 9. Réflexions finales

Mastering LeetCode 2943 est plus qu'un simple exercice de codage ; c'est une vitrine de votre état d'esprit de résolution de problèmes. En présentant une solution propre et multilingue, vous prouvez que vous pouvez :

1. **Lisez attentivement le problème** – comprendre la géométrie de la grille.
2. **Identifiez l'invariant du noyau** – barres amovibles consécutives.
3. **Mise en oeuvre d'un algorithme optimal** – O(n log n) avec un seul passage.
4. **Communiquer clairement** – essentiel pour les entrevues techniques.

Déposez cette solution dans votre GitHub, ajoutez les extraits de code à votre portfolio de codage, et référez-vous au problème dans votre prochaine interview – les recruteurs adorent voir la maîtrise concrète de LeetCode. Bon codage !