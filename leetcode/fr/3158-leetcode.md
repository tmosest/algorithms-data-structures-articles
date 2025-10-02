---
titre: LeetCode 3158. Trouvez le XOR des nombres qui apparaissent deux fois -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# # 3158. Trouvez le XOR des nombres qui apparaissent deux fois
** Difficulté :** Facile **Tags:** Array, Hash Table, Manipulation bit

> **Problème**
> On vous donne un tableau entier `nums`. Chaque numéro du tableau apparaît **une ou deux fois**.
> Retournez le XOR bitwise de **tous les nombres qui apparaissent deux fois**. Si aucun nombre n'apparaît deux fois, retourner `0`.

Exemple
Entrée Sortie Explication
C'est pas vrai.
"[1,2,1,3]"" "1"" "1" "1" apparaît seulement deux fois. Autres
"[1,2,3]"" "0"" Pas de duplicata. Autres
1 XOR 2 = 3

Obstacles
"1 ≤ longueur nominale ≤ 50"
- `1 ≤ nombres[i] ≤ 50'
- Chaque élément apparaît une ou deux fois.

---

Solution courte et efficace (temps O(n), espace O(n)

Nous comptons la fréquence de chaque nombre avec un `HashMap` (ou un tableau de taille 51 parce que les valeurs sont limitées).
Au cours d'une deuxième passe, nous XOR toutes les clés qui ont une fréquence de `2`.
Comme XOR est associatif, le résultat final est le XOR de tous les numéros dupliqués.

### Java
"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe {
public int duplicateNumbersXOR(int[] nums) {
Carte<integer, integer> freq = nouveau HashMap<>();
pour (int n : nombres) {
freq.put(n, freq.getOrDefault(n, 0) + 1);
}

xor = 0;
pour (Map.Entry<Integer, Integer> e : freq.entrySet() {
si [e.getValue()] 2) xor ^= e.getKey();
}
retour xor;
}
}
«» "

Python
'`python
Importations provenant des collections Compteur

Solution de classe:
def duplicateNumbersXOR(self, nombres: List[int]) -> Int:
freq = compteur(s)
résultat = 0
pour num, cnt en fréq.item():
Si cnt == 2:
résultat ^= num
résultat du retour
«» "

C++
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombresXOR(vecteur<int>& nombres) {
unordered_map<int, int> freq;
pour (int n : nombres) freq[n]++;

Int xor Val = 0;
pour (auto &p : freq)
si (p.second) 2) xorVal ^= p.first;
retour xor Val;
}
};
«» "

---

Article du blog – Le bon, le mauvais et l'hommage de LeetCodes *Trouver le XOR des nombres qui apparaissent deux fois*

Description de la méta
> Master LeetCodeS'il s'agit d'une solution propre, O(n) en Java, Python et C++. Apprenez les avantages, les pièges et les astuces d'entrevue pour surmonter ce problème facile et décrochez votre prochain rôle technologique.

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Pourquoi XOR?](#Why-xor)
3. [Solution à travers] (#solution à travers)
4. **Le bon** – Algorithme propre et linéaire
5. **Les mauvais** – Cas de bord et suringénierie
6. **Le Ugly** – Erreurs courantes et pièges de performance
7. [Approches alternatives] (#approches alternatives)
8. [Tests et liste de contrôle des cas](#test)
9. [Référencement et conseils d'entrevue](#seo-interview-tips)
10. [Conclusion] (#conclusion)

---

- Oui. 1. Aperçu du problème <un nom="problème-overview"></a>
LeetCodes *Trouver le XOR de nombres qui apparaissent deux fois* est un problème de tableau **facile** qui teste:

- Compte de fréquence
- Propriétés XOR bitwise
- Utilisation efficace des structures de hachage

Parce que les nombres sont petits (`- 50`) nous pouvons même remplacer une carte de hachage par un tableau de taille fixe, mais une carte de hachage conserve le code générique.

---

- Oui. 2. Pourquoi XOR? <un nom=why-xor></a>
XOR est parfaitement adapté à ce problème:

Pourquoi ça aide ?
C'est pas vrai.
**XOR de nombres identiques est 0**. Autres
**XOR est associatif et commutatif**.L'ordre n'a pas d'importance – nous pouvons accumuler des résultats dans n'importe quel passage. Autres
**XOR de `0` avec un nombre est ce nombre** Autres

Ces propriétés nous permettent de *collect* dupliquer efficacement, sans tri ni boucles imbriquées.

---

- Oui. 3. Solution Passage <un nom="solution-passage"></a>
1. ** Fréquences de comptage** – Une passe linéaire avec une carte de hachage ou un tableau de comptage.
2. **XOR duplicata** – Deuxième passe: XOR seulement les numéros dont le nombre est exactement "2".
3. **Retour** – Si aucun duplicata n'a été trouvé, `xor` reste `0` (la bonne réponse).

*Complexité temporelle :* **O(n)** – un ou deux passe au-dessus du tableau.
*Complexité spatiale:* **O(n)** – taille de la carte de hachage proportionnelle à des éléments distincts (=50).

---

- Oui. 4. Le bon <un nom="le bon"></a>
Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Simplicité** – Deux boucles claires ; aucune logique cachée. Autres
**Déterministe** – Fonctionne pour toutes les entrées dans les contraintes. Autres
**Scalable** – Si les contraintes se développent (par exemple, `nums.length = 106`), l'algorithme est toujours linéaire. Autres
**Language-agnostic** – L'implémentation existe en Java, Python, C++ avec des changements minimes. Autres
**Amis à l'entrevue** – Démontre la connaissance des tables de hachage et des opérations bitwise, deux sujets d'entrevue courants. Autres

---

- Oui. 5. Le mauvais <un nom="le mauvais"></a>
Pièges
C'est pas vrai.
**En supposant que tous les duplicatas sont exactement 2** – Problème le garantit, mais dans les données réelles, vous pouvez voir des triplicates. Valider l'entrée ou ajouter des assertions. Autres
**Utiliser des structures de données lourdes** – Une `HashMap` complète est surqualifiée pour les petits `nums`. Remplacer par un tableau fixe de 51 éléments (`int[51]`). Autres
**Pas de gestion de tableau vide** – Pas nécessaire pour LeetCode mais bonne pratique. Retourner `0` ou soulever une exception si `nums.isEmpty()`. Autres

---

- Oui. 6. L'Ugly <a name="the-ugly"></a>
Erreurs d'impact
C'est quoi ?
** Force brute double boucle** – temps "O(n2)". TLE sur les entrées plus importantes (même si les essais cachés dépassent les contraintes). Utiliser une carte de hash ou un tableau de fréquence. Autres
**Utiliser `Set` pour détecter les duplicata** – `O(n)` mais vous devez toujours XOR tous les duplicata. Il manque des doubles apparaissant deux fois si vous ne vérifiez que la présence. Le magasin compte, pas seulement la présence. Autres
**S'appuyant sur la magie bitwise sans explication** – Les intervieweurs peuvent demander *pourquoi* vous avez utilisé XOR. Risque d'être considéré comme un codeur de boîte noire. Expliquez brièvement les propriétés de XOR dans votre explication. Autres
**Ignorer le débordement entier** – XOR ne déborde pas, mais ajouter des fréquences peut si vous utilisez `int` pour les grands comptages. Rare pour les contraintes mais une bonne habitude d'utiliser "long". Autres

---

- Oui. 7. Autres approches <un nom="autres approches"></a>

1. **Tableau de calcul** (depuis valeurs ≤ 50):
"Java
int[] freq = nouveau int[51];
pour (int n : nombres) freq[n]++;
xor = 0;
pour (int i = 1; i <= 50; i++) si (freq[i]] 2) xor ^= i;
«» "

2. **Manipulation de bits sans rash**
Pour chaque position de bit `b` (0..31), compter combien de nombres ont bit `b` ensemble.
Si un peu apparaît un nombre pair de fois sur les duplicatas, il annule.
Cela est plus complexe et n'est pas nécessaire pour les contraintes données.

3. **Trier + Scan**
Triez le tableau (O(n log n)) et numérisez une fois les paires.
Pas aussi efficace que le comptage O(n), mais plus facile à coder dans les langues qui manquent de tables de hachage.

---

- Oui. 8. Liste de vérification des essais et des cas <un nom>
Autres Test d'entrée Résultats attendus
- C'est quoi ?
Autres Tous uniques
Autres Tous les duplicata (invalides par contrainte)
Autres Duplicata unique
Doublons multiples
Valeurs limites
Ordre mixte

---

- Oui. 9. SEO et conseils d'entrevue <un nom="seo-interview-tips"></a>
Pourquoi ça compte ?
- Oui.
**Mots-clés** – LeetCode XOR problem, Find XOR de nombres dupliqués, Entretien de manipulation du bit de Java Autres
Autres **Clear Code Blocks** – Séparer les sections linguistiques, ajouter des commentaires. Autres
**Interview Insight** – Discutez des compromis, de la complexité du temps et de l'espace. Autres
**Result-oriented** – Mention : « Runs in O(n) time » et « Handles ledge cases » Les recruteurs recherchent des solutions efficaces. Autres
**Appel à l'action** – Essayez cela sur LeetCode, soumettez et suivez votre évaluation. Autres

---

- Oui. 10. Conclusion <un nom="conclusion"></a>
LeetCodeS *Trouver le XOR des nombres qui apparaissent deux fois* est une vérification rapide de la santé mentale de votre capacité à combiner le comptage et les opérations bitwise.
En utilisant une carte de fréquence (ou un tableau) et en tirant parti des propriétés de XOR, vous pouvez résoudre le problème en temps linéaire avec un code minimal – exactement le genre d'intervieweurs de solutions propres et efficaces aiment.

Essayez la plateforme LeetCode, ajoutez quelques tests unitaires et n'oubliez pas de documenter votre approche dans votre portfolio. Une solution solide et prête à l'entrevue comme celle-ci peut être la différence entre l'atterrissage d'un appel d'entrevue et le fait de passer inaperçu. Bon codage !

---

Extraits de code final (Copier-Paste Ready)

C'est vrai. Java
"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
public int duplicateNumbersXOR(int[] nums) {
Carte<integer, integer> freq = nouveau HashMap<>();
pour (int n : nombres) freq.put(n, freq.getOrDefault(n, 0) + 1);

xor = 0;
pour (entrée var : freq.entrySet())
si [entry.getValue()] 2) xor ^= entry.getKey();

retour xor;
}
}
«» "

Python
'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def duplicateNumbersXOR(self, nombres: List[int]) -> Int:
freq = compteur(s)
résultat = 0
pour num, cnt en fréq.item():
Si cnt == 2:
résultat ^= num
résultat du retour
«» "

C++
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombresXOR(vecteur<int>& nombres) {
unordered_map<int,int> freq;
pour (int n : nombres) ++freq[n];

Int xor Val = 0;
pour (auto &p : freq)
si (p.second) 2) xorVal ^= p.first;

retour xor Val;
}
};
«» "

Bonne résolution, et bonne chance d'obtenir ce travail de technologie!