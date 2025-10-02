---
Titre: LeetCode 1551. Opérations minimales pour rendre la répartition égale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code – Opérations minimales pour assurer l'égalité
Le tableau est toujours
«arr[i] = 2*i + 1 (0 ≤ i < n)»

L'objectif est de rendre chaque élément égal au nombre minimum d'opérations** où une opération soustrait 1 d'un élément et ajoute 1 à un autre.
La solution mathématique est simplement

\[
\text{minOps}(n) = \left\lfloor \frac{n^2}{4} \right\rfloor
\]

car chaque paire d'éléments symétriques a besoin de \((\text{difference})/2\) et la somme de toutes les paires s'effondre à la formule ci-dessus.

---

#### Java 17

"Java
// 1551. Opérations minimales pour assurer l'égalité
// O(1) temps, O(1) espace
solution de classe publique {
Activités publiques(int n) {
// la division entière plane automatiquement le résultat
retour n * n / 4;
}
}
«» "

---

Python 3

'`python
# 1551. Opérations minimales pour assurer l'égalité
Temps O(1), espace O(1)

Solution de classe:
def minOpérations(self, n: int) -> Int:
retour n * n // 4
«» "

---

C++17

'`cpp
// 1551. Opérations minimales pour assurer l'égalité
// O(1) temps, O(1) espace

solution de classe {
public:
int minOpérations(int n) {
retour n * n / 4; // la division entière tronque vers zéro
}
};
«» "

---

Article du blog – Le bon, le mauvais et le mauvais de LeetCode 1551

> **Titre**
> **Le bon, le mauvais et le mauvais de LeetCode 1551 – Opérations minimales pour assurer l'égalité* *

> **Méta—Description* *
> Débloquez les secrets de LeetCode 1551 avec une plongée profonde dans les maths, les pièges et les tours d'interview du monde réel. Obtenez la solution O(1) la plus rapide, apprenez pourquoi un seul liner fonctionne, et découvrez les hacks d'entrevue qui font que les recruteurs vous remarquent.

---

Introduction

Code du leet 1551 – *Opérations minimales pour rendre Array Equal* – semble trompeurment simple: vous êtes donné un tableau construit à partir d'une simple progression arithmétique, et vous pouvez des unités de swap de deux positions. Le défi est de décider ** combien de swaps** il faut pour faire de chaque élément le même.

C'est un exemple classique de la façon dont un problème qui ressemble à une simulation de force brute cache une formule **fermée**. Dans ce post, nous disséquerons le **bon** (pourquoi c'est un beau puzzle de maths), le **mauvais** (des idées erronées communes qui perdent du temps), et le **ugly** (cas de pointe et pièges d'entrevue). Nous terminerons avec la solution *one-liner* et une feuille de triche prête à l'entrevue rapide.

> **Mots clés**: LeetCode 1551, Opérations minimales pour rendre Array égal, problèmes de codage d'entrevue, solution O(1), maths algorithmiques, équilibre de tableau, préparation d'entrevue, entrevue technique, conseils d'entrevue de codage, codage d'entrevue d'emploi.

---

La bonne – une dérivée mathématique propre

Étape Description Résultat
C'est quoi ?
**Comprendre le tableau** – `arr[i] = 2*i + 1` donne une séquence de nombres impairs qui augmente strictement. Autres Drôle de progression arithmétique
Autres **Identifiez la valeur cible** – Tous les nombres finissent par égaler l'élément intermédiaire lorsque `n` est impair, ou la moyenne des deux éléments intermédiaires lorsque `n` est pair. Médiane = `(n-1)`—ième nombre impair ou `(n/2)`—ième nombre impair
**Paire les extrêmes** – Déplacer 1 de l'extrémité droite à l'extrémité gauche se déplace à la fois vers le centre. Pour les indices `i` et `n-1-i`, la différence est `2*(n-1-2*i)`.
Autres **Somme les opérations** – Somme d'une série arithmétique de la forme `1+2+...+k` donne `k(k+1)/2`. La somme se transforme en un simple quadratique.
**Simplifier** – Après la manipulation algébrique, vous obtenez `=n2/4=‘. Formule finale

**Pourquoi ça marche* *
Chaque opération réduit la distance totale à la cible de 2 (une unité enlevée d'un côté, l'une ajoutée à l'autre). La somme de toutes les distances est un nombre de triangle, qui est exactement la moitié du carré de `n`.

---

Les mauvaises – pièges communs

1. ** Penser à la simulation**
* Idée naïve* : itérer sur tous les indices, effectuer des opérations un par un.
*Réalité*: Même pour `n = 104`, le nombre d'opérations peut être d'environ 25 millions – trop lent pour une interview.

2. ** Manipulation même « n »**
Certaines solutions ajoutent par erreur `n/2` après avoir calculé la somme triangulaire. La formule correcte (`n2/4`) explique déjà le cas uniforme.

3. **Débordement entier dans d'autres langues* *
Pour les `int` 32 bits en C/C++, `n * n` peut déborder quand `n = 104`? En fait, `1042 = 108` qui s'inscrit dans l'int signé 32-bit (-2.1×109). Toujours utiliser 64 bits («long long») dans les langues où «int» est 32 bits pour être sûr.

4. ** Erreurs hors pair**
La médiane est «arr[n/2]» lorsque `n` est étrange, et `arr[(n/2)-1]` ou `arr[n/2]` quand même. La confusion peut conduire à la mauvaise formule.

---

### -Le mauvais – Les pièges d'entrevue et les cas de bord

Qu'est-ce qu'il faut regarder ?
-- -- -- -- -- -- -- ------------------
Quand `n = 1` la réponse est 0 (trivial). Autres
**Large `n`**) Bien que la formule soit O(1), assurez-vous que votre code gère `n = 104` sans débordement. Autres
**Différente génération de tableau** La requête de problème garantit que le tableau est exactement `2*i+1`. Certains intervieweurs pourraient changer le générateur en `2*i` ou `2*i+2` – revérifiez les contraintes. Autres
Autres En Java, `/` sur entiers effectue la division entière (étage). En Python, `//` est nécessaire; `/` retourne un flotteur. Autres
**L'intervieweur pourrait vous demander de sortir le tableau intermédiaire après chaque opération (la version de Simulate). Vous devriez poser des questions claires pour éviter le temps perdu. Autres

---

La solution d'un liner – prête pour les entrevues

Code de la langue
C'est quoi, ça ?
**Java**
**Python** C'est ce qu'on a dit.
**C++**

> **Pourquoi il passe**
> Toutes les langues effectuent la division entière qui aplanit le résultat. L'expression `n * n / 4` est mathématiquement équivalente à `=n2/4=". Pas de boucles, pas de conditions – temps O(1), espace O(1).

---

Entretien rapide Feuille de chaleur

Concept Remarque rapide
C'est pas vrai.
**Type de problème**
**Symmétrie + distance à la médiane
Formulaire
**Complexité**
Autres **Cadre d ' égalisation**
**Excédent**= Utiliser 64-bit en cas de doute
Question commune Quelle est la valeur cible ? – médiane / moyenne de deux moyennes
**Suivez-vous**

---

### -Take final- Loin

Code du leet 1551 est une vitrine parfaite** de la façon dont un objectif mathématique clair peut réduire un problème apparemment itératif à un liner unique. Comprendre la dérivation vous montre comment raisonner à propos de *distance* et *symétrie* – compétences qui font surface dans de nombreux problèmes d'entrevue (p. ex., *Balanced Binary Tree*, *Minimum Swap to Make Strings Equal*, *Longest Prefix Suffix*).

Soyez prudent avec le boîtier de taille uniforme, évitez les débordements et demandez toujours des éclaircissements avant de plonger dans la simulation. Si vous pouvez frapper l'intervieweur avec la formule en forme fermée lors du premier essai, vous passerez *non* temps à écrire des boucles et impressionnerez l'intervieweur avec vitesse et élégance.

---

> ** Prêt à décrocher ce poste de technicien ? * *
> Pratiquez ce problème, partagez le seul liner dans votre prochaine entrevue de codage, et regardez les recruteurs ajouter *LeetCode 1551* à votre liste de compétences.

Bon codage ! C'est ce qu'il a dit