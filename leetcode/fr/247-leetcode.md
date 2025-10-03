---
titre: LeetCode 247. Numéro strobographique II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
247. Numéro strobographique II
**Java / Python / C++ – Solutions complètes + Interview‐ Prêt Blog Post**

> *LeetCode 247 – Numéro strobographique II*
> *Difficulté: moyenne*
> *Time‐Limit: 1 s (soit 5 × 105 appels récursifs max)*
> *Space‐Limit: 256 Mo*

---

Table des matières
1. [Énoncé du problème] (#Énoncé du problème)
2. [Qu'est-ce qu'un numéro strobographique?](#qu'est-ce-est-un-numéro strobographique)
3. [Stratégie de haut niveau] (#stratégie de haut niveau)
4. [Bonne – L'approche de la récursion simple] (#Bonne)
5. [Bad – Edge Cases & Leading Zeros](#bad)
6. [Ugly – Manipulation extrêmement grande `n`] (#ugly)
7. [Mise en œuvre de Java] (#Mise en œuvre de Java)
8. [Python implementation] (#python implementation)
9. [Mise en œuvre C++](#c++-mise en œuvre)
10. [Analyse de la complexité] (#analyse de la complexité)
11. [Approches alternatives] (#approches alternatives)
12. [Conseils d'entrevue et erreurs courantes](#conseils d'entrevue)
13. [Résumé optimisé du SEO](#seo-summary)
14. [Conclusion] (#conclusion)

---

- Oui. 1. Énoncé du problème <un nom="problème-statement"></a>

> **Avec un nombre entier `n`, retournez *tous* numéros stratobographiques de longueur `n`.**
> Un nombre strobographique est un nombre qui apparaît le même après la rotation 180° (à l'envers).

**Exemples**

Produit
- Oui.
"["11", "69", "88", "96"]" Autres
"["0", "1", "8"]" Autres

**Contrôles* *

* "1 ≤ n ≤ 14"

---

- Oui. 2. Qu'est-ce qu'un numéro strobographique? <un nom "qu'est-ce-est-un-numéro strobographique"></a>

Chiffres rotatifs (180°)
- C'est quoi ?
0 – 0
D'après les résultats de l'enquête
6 – 9
8 – 8
9 – 6

Un nombre est strobographique si le *i*-ième chiffre de la gauche est égal au *i*-ième chiffre de la droite après application de la cartographie ci-dessus.

---

- Oui. 3. Stratégie de haut niveau

* **Recursive Backtracking** – Construisez le numéro depuis l'extérieur.
* **Dossiers de base** –
- Oui. 0` → chaîne vide (utilisée pour construire des numéros de longueur uniforme).
* `n == 1` → `["0","1","8"]` (le chiffre moyen des nombres impairs).
* **Étape récursive** – Pour chaque chaîne `inner` de `helper(n-2, m)` prepend/append chaque paire valide.
* **Éviter les zéros principaux** – Sauter `"0" + intérieur + "0"` quand `n == m` (couche extérieure).

Cela donne toutes les combinaisons dans le temps et l'espace `O(5^(n/2).

---

- Oui. 4. Bon – L'approche de récursion simple <un nom="bon"></a>

* **Readability** – Une fonction, une boucle claire.
* **Natural Fit** – Le problème est littéralement de construire à partir des bords dedans. (en milliers de dollars)
* **Extension** – Facile à ajouter de nouvelles paires de chiffres si la définition change.
* **Aucune structure de données supplémentaires** – Utilise uniquement des listes/vecteurs de chaînes.

---

- Oui. 5. Mauvais – Cas de bord et zéros de tête <a name="bad"></a>

* Oublier d'exclure `"0...0"` au niveau extrême génère des nombres comme `"00"`, `"000"`, qui sont **invalides** parce qu'ils ont des zéros de tête.
* Une implémentation naïve qui ajoute toujours la paire zéro produira des chaînes `4` supplémentaires pour chaque couche externe, gonfleant le jeu de résultats.
* Lorsque `n` est bizarre, la couche centrale ne doit contenir que `"0"`, `"1"`, `"8"`. Ajouter `"0"` sur les côtés créerait des nombres de longueur `n+2` – un bug classique hors-par-un.

---

- Oui. 6. Ugly – Manipulation extrêmement grande `n` <a name="ugly"></a>

* **Dépassement de la masse** – La profondeur de la récursion augmente avec `n`. Pour `n = 14` la profondeur est seulement `7`, donc il est sûr, mais pour la généralisation (par exemple, `n = 104`) vous avez frappé les limites de la pile.
* ** Empreinte mémoire** – Le nombre de résultats est "5^(n/2)"; pour "n = 14", il est "5^7 = 78 125".
* Chaque chaîne est longue 14 → ~1 KB par résultat → ~78 Mo total.
* Si l'intervieweur ne demande que *compte*, vous pouvez éviter de matérialiser toutes les chaînes.

---

- Oui. 7. Mise en œuvre Java <a name="java-implémentation"></a>

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<String> trouverStrobogramme(int n) {
aide au retour(n, n);
}

liste privée<String> aide(int n, int m) {
// Cas de base
si (n) 0) retourner la nouvelle Liste d'Array<>(Collections.singletonList("");
si (n == 1) retourner une nouvelle liste d'array<>(Arrays.asList("0", "1", "8");

Liste<String> res = nouvelle liste de distribution<>();
// Récursé pour la partie intérieure
Liste <String> intérieur = assistant(n - 2, m);

pour (String s : intérieur) {
si (n != m) res.add("0" + s + "0"); // sauter en tête zéro au niveau extrême
"1" + s + "1");
rés.add("6" + s + "9");
"8" + s + "8";
"9" + s + "6");
}
retour rés;
}
}
«» "

> **Pourquoi c'est propre** – L'aide reçoit la paire *originale* `m` pour savoir quand éviter `"0"`.
> **Heure** – O(5^(n/2))
> **Espace** – O(5^(n/2))

---

- Oui. 8. Mise en oeuvre de Python <a name="python-implémentation"></a>

'`python
de taper l'importation Liste

Solution de classe:
def findStrobogrammatic(self, n: int) -> Liste[str]:
retourner soi-même._helper(n, n)

def _helper(self, n: int, m: int) -> Liste[str]:
si n] 0:
retour ["""]
si n] 1 :
retourner ["0", "1", "8"]

res = []
pour l'intérieur en soi._helper(n - 2, m):
si n != m: # éviter les zéros
res.append("0" + intérieur + "0")
res.append("1" + intérieur + "1")
Annexe("6" + intérieur + "9")
res.append("8" + intérieur + "8")
res.append("9" + intérieur + "6")
retour res
«» "

> **Note pyronique** – L'utilisation de la récursion maintient le code court; si vous préférez un BFS itératif, remplacez simplement l'aide par une boucle de queue.

---

- Oui. 9. Mise en œuvre C++ <a name="c++-implémentation"></a>

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<string> findStrobogrammematic(int n) {
aide au retour(n, n);
}
particulier:
vector<string> helper(int n, int m) {
si (n == 0) retourner {""};
si (n == 1) retourner {"0", "1", "8"};

vecteur <string> rés;
vecteur<chaîne> intérieur = aide(n - 2, m);

pour (const string &s : inner) {
si (n != m) res.push_back("0" + s + "0"); // éviter les zéros en tête
res.push_back("1" + s + "1");
res.push_back("6" + s + "9");
res.push_back("8" + s + "8");
res.push_back("9" + s + "6");
}
retour rés;
}
};
«» "

> **Pourquoi C++?** – La même logique de récursion; la seule différence est la gestion manuelle de la mémoire via `std::vector`.

---

- Oui. 10. Analyse de la complexité <un nom="analyse de la complexité"></a>

Opération Temps Espace
- C'est quoi ?
Profondeur de l'arbre de récursion (pile d'appel)
Nombre de chaînes générées (liste des résultats)
Total "O(5^(n/2))"""O(5^(n/2)" Autres

*Reason*: A chaque niveau, nous générons 5 fois plus de chaînes que le niveau intérieur précédent (à l'exception du niveau extérieur où nous sautons la paire -00, donnant 4 * 5^(k-1) pour même `n`).

---

11. Approches alternatives <un nom d'approche alternative></a>

Méthode
- C'est quoi ?
**Itérative BFS (queue)**
**DP / Memoization** Autres
**Count-only**. O(1) espace si seul le nombre de solutions est nécessaire.

> **Quand choisir BFS?** Si votre panel d'entrevue préfère des solutions itératives ou si vous craignez le débordement de pile pour plus grand `n`.

---

- Oui. 12. Conseils d'entrevue et erreurs courantes <un nom></a>

1. **Clarifier la définition** – Confirmer que les chiffres 6 et 9 sont autorisés et que 0 peut apparaître au milieu seulement pour les longueurs impaires.
2. **Demandez au sujet de zéros de tête** – Mention que les nombres comme -00 , sont invalides sauf si `n == 1`.
3. **Énoncer la complexité** – Mention `O(5^(n/2))` temps/espace; si `n` étaient énormes, discuter de la façon de modifier l'algorithme.
4. **Edge cases first** – Discutez des cas de base explicitement avant de plonger dans la récursion.
5. **Test** – Après avoir écrit le code, testez pour `n=1,2,3,4,5` afin d'assurer une manipulation correcte des longueurs impairs/even.
6. **Éviter le codage dur 4 ou 5** – Utilisez une structure de données de paires pour garder le code flexible.

---

# 13. SEO-Optimized Summary <a name="seo-summary"></a>

> Ce guide fournit la solution **LeetCode -Strobogramme Numéro II** dans **Java**, **Python** et **C++**.
> L'algorithme récursif concis construit tous les nombres stratogrammatiques de longueur `n` (1 ≤ n ≤ 14) dans le temps `O(5^(n/2)")`.
> Points clés : cas de base (`n==0` → `"`, `n==1` → `["0","1","8"]`), évitez de diriger des zéros au niveau extérieur et sautez les récursions inutiles.
> Complexité: exponentielle "5^(n/2)".
> Les versions alternatives BFS/itatives ont des performances identiques.
> Les intervieweurs recherchent souvent la capacité de gérer les cas de bord et de discuter de la complexité ; évitez les sorties de sortie et les débordements de pile.

---

- Oui. 13. Conclusion <un nom="conclusion"></a>

La solution de recul récursif est la façon la plus **naturelle** et **readable** de générer tous les nombres stratobographiques. Il gère les longueurs impairs/even, saute les zéros de tête et fonctionne confortablement dans les contraintes du problème. Pour les intervieweurs qui préfèrent la logique itérative, un BFS basé sur la file d'attente donne le même résultat sans récursion.

> **Astuce Pro** – Demandez toujours si l'intervieweur veut le *count* ou la *list*; si seul le compte compte compte, vous pouvez retourner `4 * 5^(n/2-1)` pour même `n` et `4 * 5^(n-1-2)` pour impair `n`, sauvant la mémoire.

Bonne chance cracking Numéro Strobogramme II de votre prochaine interview de codage! C'est ce qu'il a dit.

---

Références

* Problème de LeetCode: https://leetcode.com/problèmes/strobogrammematic-number-ii/
* Solutions discutées sur GitHub (Java, Python, C++)

---

**Mots clés pour le référencement**: Strobogrammatic Number II, solution LeetCode, backtracking récursif, solution Java, solution Python, solution C++, conseils d'entretien, complexité temporelle, complexité spatiale, alternative BFS.