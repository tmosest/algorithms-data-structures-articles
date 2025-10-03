---
titre: LeetCode 2243. Calculer la somme numérique d'une chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2243. Calculer la somme numérique d'une chaîne
**LeetCode – Facile** ** Limite de mémoire :** 256 Mo

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Idée de force brute] (#idée de force brute)
3. [Algorithme optimal] (#algorithme optimal)
4. [Mise en œuvre] (#Mise en œuvre)
- Java
- Python
- C++
5. [Analyse de la complexité] (#analyse de la complexité)
6. [Calendrier des cas d'urgence](#Calendrier des cas d'urgence)
7. **Les bons, les mauvais et les méchants**
8. [Interview-Ready Tips](#interview-ready-tips)
9. [Conclusion] (#conclusion)

---

## Aperçu du problème <a name="problem-overview"></a>

Avec une chaîne `s` composée de chiffres (`0`‐`9`) et un entier `k`, plusieurs fois **group** la chaîne en blocs de longueur `k` (le bloc final peut être plus court).
Pour chaque bloc, calculez la somme de ses chiffres et remplacez le bloc par cette somme (convertie en chaîne).
Concaténer les sommes de tous les blocs pour former une nouvelle chaîne.
Répétez ce processus jusqu'à ce que la longueur de la chaîne devienne **= k**; retournez la chaîne finale.

**Exemple**

«» "
s = "1111222223", k = 3
1er tour → "3465"
Ronde 2 → "135" (longueur ≤ k, arrêt)
«» "

Contraintes
- "1 ≤ s.longueur ≤ 100"
- "2 ≤ k ≤ 100"
- `s` ne contient que des chiffres

---

C'est pas vrai. Idée de force <a name="force-idea"></a>

Une solution naïve :

1. Pars chaque personnage dans un tableau entier.
2. Dans chaque tour, marchez le tableau, en additionnant des nombres consécutifs `k`, en poussant la somme dans une nouvelle liste.
3. Convertir la liste en une chaîne et répéter.

Bien que correcte, cette approche utilise des tableaux temporaires inutiles et beaucoup de conversions de chaînes.
Il rend également le code plus difficile à lire et à maintenir.

---

## Algorithme optimal <un nom="algorithme optimal"></a>

L'observation clé : **Le processus est purement séquentiel** – chaque tour ne dépend que de la chaîne actuelle, pas de l'histoire.
Par conséquent, nous pouvons le simuler en place en utilisant un `StringBuilder` (Java), une liste mutable (Python), ou un `stringstream` (C++).

**Étapes**

1. Tandis que `s.longueur() > k`:
- Créez un constructeur vide.
- Pour chaque indice `i` de `0` à `s.length()` passage par «k»:
- Calculer la somme des chiffres de `i` à `min(i + k, s.longueur()`.
- Ajouter la somme numérique (convertie en chaîne) au constructeur.
- Remplacer `s` par `builder.toString()`.
2. Retour « s ».

La boucle interne traite chaque personnage exactement une fois par tour, et chaque tour raccourcit considérablement la chaîne, de sorte que le coût total est linéaire dans la longueur initiale.

---

## Mise en oeuvre <un nom></a>

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

Code de la langue
C'est quoi, ça ?
**Java** Cliquez pour agrandir</résumé>

"Java
***
* LeetCode 2243 – Calculer Somme numérique d'une chaîne
* Auteur: Votre nom (Linkedin) GitHub
*/
solution de classe publique {
chaîne publiqueSum (chaîne s, int k) {
// Continuer jusqu'à ce que la longueur de la chaîne soit ≤ k
pendant que (longueur() > k) {
StringBuilder suivant = nouveau StringBuilder();

// Marchez à travers la chaîne en marche de k
pour (int i = 0; i < s.longueur(); i += k) {
= 0;
// Somme des chiffres du bloc actuel
pour (int j = i; j < Math.min(i + k, s.longueur()); j++) {
somme += s.charAt(j) - '0';
}
// Ajouter la somme comme une chaîne
suivant.append(sum);
}

s = suivant.àString(); // Préparez-vous à la prochaine ronde
}
retour s;
}
}
«» "

</détails>
**Python**=Détails><résumé>Cliquez pour agrandir</résumé>

'`python
"""
LeetCode 2243 – Calculer Somme numérique d'une chaîne
Auteur: Votre nom (Linkedin GitHub)
"""

Solution de classe:
def digitSum(self, s: str, k: int) -> str:
Continuer à réduire pendant que la longueur dépasse k
pendant que len(s) > k:
next_str = []
pour i dans la plage(0, len(s), k):
bloc = s[i:i + k]
digit_sum = sum(int(ch) pour ch en bloc)
next_str.append(str(digit_sum))
s = "".join(next_str)
retour s
«» "

</détails>
**C++** Cliquez pour agrandir</résumé>

'`cpp
***
* LeetCode 2243 – Calculer Somme numérique d'une chaîne
* Auteur: Votre nom (Linkedin) GitHub
*/
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chiffre de chaîne Somme(chaîne s, int k) {
pendant que ((int)s.size() > k) {
chaîne suivante;
pour (int i = 0; i < (int)s.size(); i += k) {
= 0;
pour (int j = i; j < min(i + k, (int)s.size()); ++j) {
somme += s[j] - '0';
}
suivant += to_string(sum);
}
s.swap(suivant); // éviter la copie
}
retour s;
}
};
«» "

</détails>

---

## Analyse de complexité <un nom="analyse de complexité"></a>

Opération Temps Espace
- C'est quoi ?
Chaque tour (constructeur)
Autres Nombre total de tours ≤ `log_k (longueur initiale)'
Exclusivité globale **O(n)** où `n` ≤ 100.

Avec `n` ≤ 100, la solution fonctionne confortablement dans les limites.

---

Surmonter Liste de vérification des cas <un nom> Liste de vérification des cas de référence></a>

Cas de bord Ce qu'il faut tester Pourquoi ça compte
- C'est quoi ?
`k` égale la longueur de la chaîne de caractères `s = "123", k = 3`
`k` plus grande que la chaîne de caractères `s = "12", k = 5`
Autres Tous les zéros `s = "0000", k = 2 ''Le résultat garde les zéros (`"00"`), les zéros de tête d'essai
= "7", k = 3"
Longueur maximale (100) , Chaîne aléatoire à 100 chiffres, `k = 10` , Test de stress

---

## Le Bon, le Mauvais, et l'Ugly <un nom, le bon, le mauvais et le mauvais"></a>

Aspect du bien
- C'est quoi ?
**L'élégance algorithmique**= Simulation directe; pas de trucs cachés== Nécessite des limites de boucle soigneuses pour éviter de se tromper== certaines solutions naïves convertissent chaque personnage en int à plusieurs reprises, blessant les performances==
**Readability**== Effacer les boucles `for`, les noms de variables descriptives=== Les boucles sur-nestées peuvent confondre===L'utilisation du régex ou des compréhensions de listes complexes peut masquer l'intention===
Autres **Edge‐Manipulation de cas**= Explicit `min(i + k, len)` gère le dernier bloc== L'oubli de gérer le dernier bloc conduit à des erreurs== Utiliser la division entière sans vérifier le reste → bugs silencieux==
Autres **Utilisation de l'espace**=Reuse builder or stringstream==L'attribution d'une nouvelle chaîne chaque tour peut être gaspillée==Enregistrement de chaque chaîne intermédiaire dans un vecteur → Mémoire O(n2)=
Le manque de tests négatifs peut masquer les bugs.

> ** Conseil professionnel :** Lorsque vous expliquez votre solution dans une entrevue, commencez par l'intuition (= groupe, somme, remplacement==) avant de plonger dans le code. Ceci démontre un état d'esprit clair de résolution de problèmes.

---

## Conseils de préparation à l'entrevue <un nom></a>

1. ** Expliquez l'invariant**: Après chaque tour, la longueur de la chaîne est au plus `précédent_longueur / k + 2`.
2. **Discuse pourquoi `alors que ` (len > k)` est exact**: Parce que le processus s'arrête exactement quand la longueur ≤ k.
3. **Afficher comment gérer le dernier bloc**: Utiliser `min(i + k, len)` ou `substring(i, min(...))`.
4. **Complexité des peines**: Temps linéaire, espace auxiliaire linéaire.
5. **Demander des éclaircissements** : l'entrée est-elle garantie non vide ? (Oui par contrainte.)
6. **Partager un test d'unité rapide**: `assert solution.digitSum("00000000", 3) == "000"`.

Ces points donnent confiance aux intervieweurs que vous comprenez à la fois l'algorithme et ses cas de bord.

---

## Conclusion <un nom="conclusion"></a>

LeetCode 2243 est un exemple de manuel de **string manipulation + simulation**.
L'astuce consiste à regrouper correctement et à résumer des chiffres sans frais généraux inutiles.
Les implémentations Java, Python et C++ fournies sont concises, efficaces et prêtes à la production.

Si vous pouvez expliquer cette solution dans une entrevue – couvrant l'intuition, les cas de bord et la complexité – vous impressionnerez les recruteurs et vous rapprocherez de cette offre d'emploi. Bonne chance ! C'est ce qu'il a dit.

---

**Mots clés:**
`LeetCode 2243`, `numer sum`, `string grouping`, `simulation algorithme`, `Java solution`, `Python solution`, `C++ solution`, `interview prep`, `time complexity O(n)`, `edge case handling`, `coding interview tips`.
---

* Sentez-vous libre de fourche cette repo et ajoutez vos propres tests ou optimisations! Bon codage ! *