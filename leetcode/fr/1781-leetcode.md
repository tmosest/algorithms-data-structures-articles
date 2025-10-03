---
Titre: LeetCode 1781. Somme de la beauté de toutes les sous-chaînes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1781. Somme de la beauté de toutes les sous-chaînes – Solution Full-Stack

> **Mots clés:** LeetCode 1781, Somme de beauté, Cordes, Java, Python, C++, Algorithme Interview, complexité temporelle, complexité spatiale

---

- Oui. 1. Récapitulation des problèmes

> **Beauté d'une chaîne** = (fréquence du caractère le plus commun) – (fréquence du caractère le moins commun qui apparaît réellement).
> **Tâche:** Pour une chaîne donnée `s` (1 ≤ ≤ ≤ 500, lettres minuscules seulement), retourner la somme des valeurs de beauté pour **all** sous-chaînes possibles.

---

- Oui. 2. Pourquoi ce problème est un excellent exercice d'entrevue

C'est bien, c'est mal.
C'est pas vrai.
**Clarity** – input & output bien défini. **Les boucles nestées** peuvent être déroutantes pour les débutants.
**Scalabilité** – 500 longueur → ~125 000 sous-chaînes → < 1 M opérations.
**Multi-langue** – Java, Python, C++ → montre la pensée multiplateforme.

---

- Oui. 3. Intuition de la force brute

La façon la plus simple est d'énumérer chaque sous-chaîne, compter la fréquence de chaque lettre, puis calculer `max - min`.

Texte
pour i dans 0 .. n-1: // index de démarrage
pour j in i .. n-1: // indice de fin
calcule freq[26] de s[i..j]
beauté = max(freq) - min(freq>0)
Total += beauté
«» "

*Complexité:* `O(n3)` – parce que nous recalculons les mêmes caractères plusieurs fois.
*Espace:* "O(1)" – seulement un tableau fixe 26-int.

Ceci est *acceptable* pour `n ≤ 20`, mais pour `n = 500` il devient trop lent.

---

- Oui. 4. Solution optimale O(n2 · 26)

Nous pouvons **réutiliser le tableau de fréquences** tout en élargissant la sous-chaîne un caractère à la fois.

Texte
pour commencer par 0 .. n-1:
freq[26] = {0}
pour la fin au début .. n-1:
freq[s[end]]++ // O(1) mise à jour
maxFreq = 0
minFreq = INF
pour k dans 0 .. 25: // scan 26 lettres
si freq[k] > 0:
maxFreq = max(maxFreq, freq[k])
minFreq = min(minFreq, freq[k])
Total += maxFreq - minFreq
«» "

* Pourquoi ça marche : *
- Oui. En réinitialisant « freq » à chaque nouvel indice de départ, nous nous assurons de ne considérer que la sous-chaîne actuelle.
- Oui. Le balayage interne de 26 lettres est à temps constant, de sorte que la complexité globale devient "O(n2)".

*Complexité:*
- **Temps:** `O(n2)` (- 125 000 × 26 - 3,2 M ops pour `n = 500`) – confortablement rapide.
- **Espace:** `O(1)` – tableau fixe 26-int.

---

- Oui. 5. Mise en œuvre du code

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.
Tous les trois suivent la même logique et atteignent la même complexité optimale.

---

##### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int beauté Somme(s) {
int n = s.longueur();
= 0;

pour (int start = 0; start < n; start++) {
int[] freq = nouveau int[26]; // réinitialiser pour chaque démarrage
pour (int fin = début; fin < n; fin++) {
freq[s.charAt(end) - 'a']++; // fréquence de mise à jour

int maxFreq = 0;
int minFreq = entier.MAX_VALUE;
pour (int f : freq) {
si (f > 0) {
si (f > maxFreq) maxFreq = f;
si (f < minFreq) minFreq = f;
}
}
Total += maxFreq - minFreq;
}
}
le total des retours;
}

public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.beautySum("aabcb")); // 5
Système.out.println(sol.beautySum("aabcbaa")); // 17
}
}
«» "

---

5.2 Python

'`python
Solution de classe:
def beautySum(self, s: str) -> Int:
n = len(s)
Total = 0

pour commencer dans la plage(n):
freq = [0] * 26 # réinitialiser pour chaque démarrage
pour la fin dans la plage (démarrage, n):
freq[ord(s[end]) - 97] += 1

max_f = 0
min_f = flotteur('inf')
pour f en freq:
Si f > 0:
si f > max_f:
max_f = f
si f < min_f:
min_f = f
Total += max_f - min_f

retour total


♪ Démo
si __nom__ == "__main__" :
sol = Solution()
print(sol.beautySum("aabcb")) # 5
print(sol.beautySum("aabcbaa")) # 17
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int beauté Somme(chaîne s) {
int n = s.size();
long total = 0; // utiliser long pour la sécurité

pour (int start = 0; start < n; ++start) {
int freq[26] = {0}; // réinitialiser
pour (int fin = début; fin < n; ++ fin) {
freq[s[end] - 'a']++;

Int maxF = 0, minF = INT_MAX;
pour (int f : freq) {
si (f > 0) {
si (f > maxF) maxF = f;
si (f < minF) minF = f;
}
}
Total += maxF - minF;
}
}
retour (int)total;
}
};

// Démo
Int main() {
Solution sol;
Cout << sol.beautySum("aabcb") << enl; // 5
Cout << sol.beautySum("aabcbaa") << enl; // 17
}
«» "

---

- Oui. 6. Répartition par complexité

Étape Opération Complexité
- C'est quoi ?
Autres Boucle extérieure (`démarrage`)
La boucle intérieure (`end`)
Mise à jour de la fréquence
Numériser 26 lettres
**Total**
Autres Espace supplémentaire

---

- Oui. 7. Pièges courants et comment les éviter

Pourquoi ça arrive
- Oui.
**Montant des fréquences nulles comme min.**= Certaines personnes utilisent par erreur `minFreq = 0` initialement====================================================================================================================================================================================================================================== 0' lors de la mise à jour min/max
**Off‐by‐one dans les boucles**. Autres
À l'exception de 500, mais `int` pourrait déborder pour de plus grandes contraintes.
**Re-alterner le freq à chaque fois**

---

- Oui. 8. Conseils d'entrevue

1. ** Expliquez votre raisonnement** – Expliquez pourquoi la numérisation de 26 lettres est bon marché et comment l'algorithme reste `O(n2)`.
2. **Mentionner le boîtier de bord** – Quand tous les personnages sont les mêmes, la beauté est toujours 0 ; notre algorithme la gère naturellement.
3. **Discuss alternatives** – Mentionnez des montants ou des fenêtres coulissantes, mais expliquez pourquoi elles sont inutiles ici.
4. **Afficher votre code rapidement** – Même si vous écrivez un pseudocode sur papier, soyez prêt à le traduire dans la langue demandée.

---

- Oui. 9. Conclusion

> **Sum of Beauty of All Substrings** est un problème fallacieux qui met en valeur un truc soigné : **utiliser une petite table de fréquence tout en élargissant les sous-chaînes**.
> La solution optimale fonctionne dans le temps `O(n2)` et l'espace `O(1)`, ce qui le rend parfait pour les juges en ligne (LeetCode, HackerRank) et les entretiens de codage en direct.

Bonne chance – et rappelez-vous : la *beauté* de votre solution réside dans sa **simplicité, efficacité et clarté croisée** 