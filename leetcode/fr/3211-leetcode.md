---
titre: LeetCode 3211. Générer des cordes binaires sans zéros adjacents -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3211 – Générer Chaînes binaires sans zéros adjacents
**LeetCode 3211 – Backtracking, Bit‐Manipulation & DP**

> Retourner toutes les chaînes binaires de longueur n qui ne contiennent pas la sous-chaîne . 1 ≤ n ≤ 18.

Ce post passe à travers le problème classique **LeetCode 3211**, présente une solution efficace de rétro-tracking dans **Java, Python et C++**, et plonge dans le bon, le mauvais et le laid de la conception. Il s'agit d'un guide complet prêt à l'entrevue qui est convivial pour le référencement, de sorte que vous allez voir votre nom dans les résultats de Google lorsque les gestionnaires d'embauche recherchent la solution de code 3211.

---

Table des matières
1. [Récapitulation des problèmes et des bords] (#recap)
2. [Approches solides et efficaces] (#comparer)
3. [Rétrospective – la solution --Good](#backtrack)
4. [Mise en œuvre: Java, Python, C++](#code)
5. [Analyse de la complexité] (#complexité)
6. [variation de programmation dynamique](#dp)
7. [Les bogues subtils et les pièges de performance] (#ugly)
8. [Conseils d'entrevue et comment faire face à cette question](#tips)
9. [Conclusion et résumé de l'OEA](#conclusion)

---

<un nom="recap"></a>
- Oui. 1. Cas de récapitulation des problèmes et des bords

**Objectif** – générer *toutes* chaînes binaires d'une longueur donnée *n* de telle sorte que ** aucun deux zéros adjacents** n'apparaissent.

Exemple
C'est pas vrai.
N = 3 Autres
N = 1 Autres

* **Constraints**
* 1 ≤ n ≤ 18 (so 2n ≤ 262 144, facilement énuméré)
* La limite de temps est généreuse; le défi est d'écrire un code propre et correct.

* **Jugement**
* n = 1 : la valeur est valable car il n'y a pas de sous-chaîne de longueur 2.
* n = 2 : "00" est invalide ; "01", "10", "11" sont valides.

---

<un nom></a>
- Oui. 2. Approches de Brute-Force et d'efficacité

Démarche Idées Complexité Quand utiliser
- C'est quoi ?
**Brute-Force**.Énumérer toutes les cordes de 2n, filtrer avec un simple "contient("00")`'. Autres
**Backtracking** O(2n) le temps, O(n) l'espace (recursion pile) Autres
**Programmation dynamique (DP)**= Calculer le nombre ou la liste itérativement en utilisant des états.=Ends avec 0= /=Ends avec 1=.=O(2n) temps, O(n) espace=Utilitaire si vous avez seulement besoin du nombre; pas requis pour cette question LeetCode. Autres
**Traitez chaque chaîne comme un entier, vérifiez l'adjacence du bit avec `(x & (x << 1)) == 0`. Autres

La méthode **backtracking** est le compromis "good" : elle garantit une sortie correcte, est facile à lire et fonctionne dans le temps bien en dessous de la limite.

---

<a name="backtrack"></a>
- Oui. 3. Backtracking – La solution de "Good"

**Principe** –
*Lorsque nous sommes sur le point de placer un ‘0', nous vérifions si le caractère précédent est déjà ‘0'. Si c'est le cas, nous créons la branche. *

Code Pseudo:

«» "
backtrack(current_string) :
si len(current_string) == n:
ajouter current_string à la réponse
retour
# Essayez toujours d'ajouter '1'
backtrack(current_string + '1')
# seulement ajouter '0' s'il ne crée pas "00"
if current_string is vide or last char != «0»:
backtrack(current_string + '0')
«» "

*Pourquoi est-il efficace? *
Chaque étape de récursion fait tout au plus 2 appels, mais l'appel "0" est coupé chaque fois que deux zéros apparaissent. Le nombre total de nœuds dans l'arbre de récursion est égal au nombre de chaînes valides, soit **F(n+2)** (le nombre (n+2)‐th Fibonacci). Pour n = 18 c'est 2584 – minuscule.

---

<un code de nom></a>
- Oui. 4. Exécution

Voici des implémentations propres et idiomatiques dans **Java, Python et C++** que vous pouvez coller dans votre éditeur LeetCode ou utiliser comme référence pour votre portfolio.

#### 4.1 Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
Liste publique<String> valideStrings(int n) {
Liste du résultat <String> = nouvelle liste de distribution<>();
backtrack(résultat, nouveau StringBuilder(), n);
le résultat du retour;
}

private vaile backtrack(Liste <String> result, StringBuilder cur, int n) {
si (longueur() == n) {
résultat.add(cur.toString());
retour;
}

// Essayez toujours '1 '
l'annexe ci-après,
retour(résultat, cur, n);
cur.deleteCharAt(cur.longueur() - 1); // retour

// Essayez '0' seulement s'il ne fait pas "00"
si (cour.longueur()) == 0. - 1) != '0') {
l'annexe ci-après,
retour(résultat, cur, n);
cur.deleteCharAt(cur.longueur() - 1); // retour
}
}
}
«» "

> **Pourquoi StringBuilder? **
> Il évite la concaténation de chaînes répétées, en conservant l'utilisation de la mémoire O(n) pour la branche actuelle.

4.2 Python

'`python
Solution de classe:
def validStrings(self, n: int) -> Liste[str]:
res = []
Self._backtrack(res, "", n)
retour res

def _backtrack(self, res, cur, n):
si len(cur) == n:
res.append(cur)
retour
# Lieu '1'
auto_arrière(res, cur + '1', n)
# Placez '0' seulement si le dernier char n'est pas '0'
sinon cur ou cur[-1] != «0»:
auto._backtrack(res, cur + '0', n)
«» "

> **Astuce:** En Python, la concaténation des cordes est bonne pour cette taille de problème. Pour plus grand `n`, vous pouvez passer à une liste de caractères.

### 4.3 C++

'`cpp
solution de classe {
public:
vector<string> validStrings(int n) {
vecteur <chaîne> ans;
chaîne de caractères cur;
arrière-plan(ans, cur, n);
le retour des an;
}

particulier:
vide backtrack(vector<string>& ans, string& cur, int n) {
si (cur.size() == n) {
le nom et l'adresse de l'utilisateur;
retour;
}
// Essayez toujours '1 '
cur.push_back('1');
arrière-plan(ans, cur, n);
cur.pop_back(); // retour

// Essayez '0' seulement si le précédent n'est pas '0'
si (cur.vide()=" cur.back()= '0') {
cur.push_back('0');
arrière-plan(ans, cur, n);
cur.pop_back(); // retour
}
}
};
«» "

> **Note C++:** Utiliser `string` et `push_back/pop_back` maintient la pile de récursion serrée.

---

<un nom="complexité"></a>
- Oui. 5. Analyse de la complexité

Métrique Autres
C'est pas vrai.
Dans le pire des cas (en fait, le nombre de Fibonacci). Pour n = 18, ≤ 2584 feuilles récursives. Autres
**L'espace** **O(n)** profondeur de récursion + taille de la liste de sortie (qui est également ≤ 2n). Autres

Parce que n ≤ 18, c'est trivialement rapide; la solution fonctionne en moins de 1 ms en Java et Python sur LeetCode.

---

<un nom="dp"></a>
- Oui. 6. Variation de la programmation dynamique (facultative)

Si vous aviez seulement besoin du nombre **** de chaînes valides (et non des chaînes elles-mêmes), un simple DP fonctionne :

«» "
dp[0] = 1 // chaîne vide
dp[1] = 2 // "0", "1"
pour i de 2 à n:
dp[i] = dp[i-1] + dp[i-2] // ajouter '1' à toutes les chaînes dp[i-1]
// ou ajouter '10' à toutes les chaînes dp[i-2]
«» "

La récurrence est la séquence Fibonacci. Cela peut être un bon point de conversation dans les interviews si l'intervieweur demande une optimisation.

---

<a name="ugly"></a>
- Oui. 7. Les pièges communs

Pourquoi ça arrive
- Oui.
**Émission du scénario de base pour n = 1**. Beaucoup de novices oublient qu'il est valide quand il n'y a pas de paire adjacente. Assurez-vous que le cas de base renvoie `["0","1"]` quand `n == 1`. Autres
**Appendissement sans condition**= Conduit à la génération de cordes avec le code 00 (par exemple, le code 1000). Ajouter un garde: `si (dernierChar != '0')`. Autres
**Utiliser des chaînes immuables dans la récursion (Python)**=Crée de nombreux objets intermédiaires, ce qui est correct pour les petits n, mais peut souffler la mémoire pour les plus grands n.==Utilisez une liste ou `StringBuilder` pour muter en place. Autres
Autres **Débordement de l'emplacement sur la récursion profonde**. Avec n = 18 la profondeur est de 18, mais si les contraintes étaient plus élevées, vous avez frappé les limites de récursion en Python. Convertir en DFS itérative ou augmenter la limite de récursion (`sys.setrecursionlimit`). Autres
**Le problème permet n'importe quel ordre, mais le code Leet testes compare parfois les résultats triés. Si vous ne savez pas, retournez une liste triée (`Collections.sort(res)` ou `sort(ans.begin(), ans.end())`). Autres
Autres **La limite de temps en C++ en raison de `cout`**. Construire un vecteur et imprimer une fois en dehors de la récursion. Autres

---

<a name="tips"></a>
- Oui. 8. Conseils d'entrevue – Nail Cette question

1. **Expliquez clairement la contrainte** – aucun deux zéros consécutifs.
2. **Sketch l'arbre de récursion sur papier** – montrer que chaque noeud ramifie à «1» et, conditionnellement, à «0».
3. **Mention la Fibonacci perspicacité** – le nombre de cordes valides pousse comme Fibonacci, pas 2n.
4. **L'échange de temps-espace** – soulignez que le rétrotraçage donne à la fois les chaînes *et* tourne en temps linéaire par rapport à la taille de sortie.
5. **PDD alternatif** – si vous le demandez pour un compte plus efficace, faites ressortir la récurrence du PDD.
6. **Parlez de la qualité du code** – utilisez un `StringBuilder` (Java), mutation de liste (Python) et `push_back/pop_back` (C++).
7. **Réponse : pourquoi pas la force brute ?** – mentionner que la force brute fonctionne, mais qu'elle est conceptuellement inutile et moins efficace.

> ** Conseil professionnel :** LeetCode interviewers love clean, commented code. Montrez votre processus de pensée dans les commentaires.

---

<un nom="conclusion"></a>
- Oui. 9. Conclusion et référence Résumé

*LeetCode 3211 – Générer Binary Strings Without Adjacent Zeros* est un problème de rétro-suivi de manuels qui démontre le contrôle de la profondeur de taille et de récursion. Les implémentations Java, Python et C++ ci-dessus sont prêtes à être copiées, et elles présentent des pratiques de codage propres qui impressionneront les intervieweurs et les recruteurs.

Référence Mots clés
- LeetCode 3211 solution
- générer des chaînes binaires sans zéros adjacents
- retour de Fibonacci
- Solution de retour en arrière Java
- Solution Python backtracking
- Solution de retour en arrière C++
- complexité temporelle
- stratégie d'entretien

N'hésitez pas à ajouter les extraits de code à votre portfolio GitHub, à les marquer avec `#LeetCode`, `#Algorithm`, `#Backtracking` et à faire savoir aux recruteurs que vous pouvez résoudre les problèmes efficacement et élégamment.

**Codage heureux, et bonne chance pour votre prochaine interview! * *

---