---
titre: LeetCode 3324. Trouvez la séquence des chaînes apparaissant sur l'écran -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes
**LeetCode 3324 – Trouver la séquence des cordes apparaissant sur l'écran**
*Difficulté: moyenne*

Alice a un clavier spécial avec seulement deux clés

Effet de la clé
- Oui.
Autres Ajouter `'a'` à la chaîne actuelle
Autres **2**=Augmentation du caractère *dernier* de la chaîne (`'c' → 'd'`, `'z' → 'a'`) Autres

A partir d'une chaîne vide, Alice veut taper la chaîne cible dans **le nombre minimum de touches de presse**.
Votre tâche est de retourner **chaque chaîne intermédiaire** qui apparaît à l'écran dans l'ordre où elle apparaît.

---

Pourquoi ce problème est-il un problème pour les entrevues

Raison
- Oui.
**Connaissance algorithmique**=Vous devez penser à la façon d'atteindre la cible avec les presses clés les moins nombreuses. Autres
**Manipulation de la chaîne de caractères**= Toutes les langues doivent construire et modifier efficacement des chaînes de caractères. Autres
**Manipulation d'un cas d'Edge**.Signature vide → première `'a'`, wrap‐around `'z' → 'a' est trivial ici mais mérite toujours d'être mentionné. Autres
**Longueur de la cible jusqu'à 400 – O(n2) est assez rapide, mais une solution O(n) gourmande est encore plus agréable. Autres

Si vous pouvez attraper ce problème, vous allez montrer interviewers que vous savez transformer un scénario apparemment compliqué en un simple algorithme gourmand.

---

La stratégie optimale

1. **Ajouter `'a'` premier** – vous *doit* appuyer sur la touche 1 au moins une fois pour chaque nouveau caractère.
2. **Incrément à la lettre désirée** – utiliser la clé 2 jusqu'à ce que le dernier caractère corresponde au caractère cible.
3. **Enregistrez chaque chaîne intermédiaire** – chaque presse (clé 1 ou clé 2) produit une nouvelle chaîne qui doit faire partie de la réponse.

La règle gourmande : *pour chaque caractère de la cible, appuyez sur la touche 1 une fois, puis appuyez sur la touche 2 jusqu'à ce que le dernier caractère soit égal au caractère cible. *
Ceci est évidemment optimal car vous ne pouvez pas sauter la clé 1 pour un nouveau caractère et vous ne pouvez pas sauter n'importe quel incréments requis de la clé 2.

---

Code Passage

Voici des implémentations idiomatiques propres dans **Java**, **Python** et **C++**.
Tous les trois partagent la même logique et fonctionnent en temps O(n2) (worst-case 25 incréments par caractère) et en espace O(n2) pour la sortie.

C'est pas vrai. Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
public List<String> stringSequence(String cible) {
Liste du résultat <String> = nouvelle liste de distribution<>();
StringBuilder cur = nouveau StringBuilder();

pour (char ch : cible.toCharArray()) {
// Clé 1: ajouter 'a '
l'annexe ci-après,
résultat.add(cur.toString());

// Clé 2: incrémenter le dernier char jusqu'à ce qu'il corresponde à 'ch'
pendant que (cur.charAt(cur.longueur() - 1) < ch) {
char next = (char) ((cur.charAt(cur.longueur() - 1) - 'a' + 1) % 26 + 'a');
cur.setCharAt(cur.longueur() - 1, suivant);
résultat.add(cur.toString());
}
}
le résultat du retour;
}
}
«» "

> **Pourquoi `StringBuilder`?**
> Les annexes à temps constant et les modifications en place rendent cette mise en œuvre conviviale.

# # # # # #

'`python
Solution de classe:
def chaîne Séquence(même, cible: str) -> liste[str]:
res = []
cur = []

pour ch dans la cible:
# Clé 1
Annexe
Annexe('.join(cur))

# Clé 2
alors que cur[-1] < ch:
cur[-1] = chr(((ord(cur[-1])) - 97 + 1) % 26) + 97)
Annexe('.join(cur))

retour res
«» "

> **Pourquoi une liste de chars? * *
> Les listes sont mutables et `''.join` est linéaire; construire la chaîne une fois par presse maintient l'exécution basse.

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<string> stringSequence(string cible) {
vecteur <string> rés;
chaîne de caractères cur;

pour (char ch : cible) {
// Clé 1
cur.push_back('a');
res.push_back(cur);

// Clé 2
pendant que (cur.back() < ch) {
cur.back() = (cur.back() - 'a' + 1) % 26 + 'a';
res.push_back(cur);
}
}
retour rés;
}
};
«» "

> **Pourquoi `cur.back()`? * *
> Donne O(1) accès au dernier caractère, idéal pour l'étape de l'incrément dernier char.

---

Analyse de complexité

Métrique
- C'est quoi ?
**Heure**= O(n2) (= 400 * 25=10 000 opérations)= O(n2)= O(n2)=
**Espace**= O(n2) pour la liste de sortie== O(n2)= O(n2)=
**Pourquoi O(n2)?**= Chacun des caractères de la cible `n` peut déclencher jusqu'à 25 incréments de clé 2. Autres

Pour les contraintes (`n ≤ 400`), c'est trivial – les trois solutions fonctionnent en < 1 ms sur les juges modernes.

---

Pièges communs

Pourquoi ça casse
C'est quoi ?
**Si vous oubliez d'enregistrer la chaîne lorsque le dernier caractère correspond finalement à la cible, la réponse sera incomplète. Autres
**Utiliser `+=` sur les chaînes immuables (Java/Python)** Utilisez `StringBuilder` ou une liste. Autres
**Optimisation excessive à l'O(n)**=C'est impossible; vous devez enregistrer chaque chaîne intermédiaire, qui est intrinsèquement l'O(n2). Autres
Bien que la cible du problème soit constituée uniquement de lettres minuscules, la logique d'enroulement est essentielle pour une solution générique. Autres

---

À emporter pour votre entrevue

1. **Greedy est roi** – toujours chercher l'étape la plus petite possible qui vous maintient toujours sur la bonne voie.
2. **Expliquez votre raison** – J'appuie sur la touche 1 une fois par nouveau caractère parce que vous ne pouvez pas sauter ; J'appuie sur la touche 2 jusqu'à ce que le dernier caractère corresponde parce que c'est le nombre minimal d'accroissements. (en milliers de dollars)
3. **Show the code is clean** – use language‐idiomatic data structures (Java `StringBuilder`, liste Python, chaîne C++).
4. **Complexité des phrases** – les intervieweurs adorent vous voir penser à la performance.
5. **Test edge cases** – cible vide (invalide par contraintes mais toujours bonne à penser), caractère unique, ou cible contenant `'z'`.

La maîtrise de ce problème vous donnera une base solide pour d'autres questions de simulation et de construction incrémentale que vous pouvez rencontrer.

---

Article du blog : Le bon, le mauvais, et le mauvais de LeetCode 3324

> **Mots clés**: *LeetCode 3324, Trouver la séquence des chaînes Apparu sur l'écran, algorithme, solution Java, solution Python, solution C++, question d'entrevue, manipulation de chaînes, algorithme avide, conseils d'entretien d'emploi, entretien d'ingénieur logiciel*

---

Introduction

LeetCodeS *Trouver la séquence des cordes Apparu sur l'écran* (Problème 3324) est un problème trompeur simple qui se transforme en une grande vitrine de raisonnement avide et de manipulation efficace des cordes. Dans cet article, je vais marcher à travers le **bon**, **bad**, et **ugly** façons les gens le résoudre, puis révéler la solution propre, optimale qui impressionnera les recruteurs.

---

### La bonne – Une approche propre de l'avidité

> *Pourquoi est-ce bon? *
> 1. ** Presses à clés miniatures**: La solution suit une stratégie d'avidité éprouvée – appuyez sur « a » pour chaque nouveau caractère, puis incrémentez le dernier caractère jusqu'à ce qu'il corresponde à la cible.
> 2. ** Logique linéaire** : On passe sur la chaîne cible, travail constant par caractère (sauf les incréments inévitables).
> 3. **Code lisible**: Utilise des constructions de langage idiomatique (`StringBuilder`, `list`, `std::string`).

Les extraits Java, Python et C++ ci-dessus illustrent ce style.

---

### Les mauvais – Variantes trop compliquées ou inefficaces

Mauvaise approche
C'est quoi ?
**Brute-force BFS** Autres
**Récupérer les mêmes préfixes plusieurs fois; toujours O(n2) mais avec de lourds frais de récursion. Autres
**Utiliser `+` pour concaténer les chaînes**.Dans des langages comme Java/Python, crée un nouvel objet de chaîne sur chaque presse. Autres

Ces modèles existent parce que les gens obtiennent **traped dans ..find la séquence la plus courte** pensant qu'il faut une recherche. Une fois que vous réalisez que *doit* enregistrer chaque chaîne intermédiaire, vous pouvez abandonner la recherche entièrement.

---

### L'Ugly – Ignorer les cas de bord et les structures de données erronées

> *Qu'est-ce qui rend ça moche? *
> 1. **Exportation de chaîne immuable** – `current = courant + 'a' dans Java ou `current += 'a' dans Python.
> 2. ** Logique de recouvrement incorrecte** (`(char)(current.back() + 1)` sans module 26).
> 3. **Limites codées en dur** – En supposant 25 incréments toujours ; en négligeant le cas particulier où un caractère est « a » lui-même.

Le code Ugly entraîne souvent des limites de mémoire ou TLE même sur des cas de test trivial.

---

### L'indulgence – L'erreur d'un liner

> *Certains candidats essaient de presser toute la solution dans une seule ligne, en utilisant des compréhensions de liste fantaisie ou des fonctions lambda. *
> Cela semble intelligent mais cache en fait une boucle complexe, rendant le débogage presque impossible. Les recruteurs apprécient rarement le code qui semble bon mais ne peut pas être tracé.

---

### Votre trousse à outils – Pourquoi L'avidité suffit

- ** Expliquez le "Why"** – pas seulement le "how".
- **Discuse le temps et l'espace** – O(n2) est le meilleur que vous pouvez faire parce que la sortie elle-même a des éléments n2.
- **Afficher la couverture des tests** – Vérifier les cibles à caractère unique, toutes les cibles `'z'` et le comportement d'enroulement.

---

Conclusion

Le problème 3324 est une micro-salle de classe de la conception, de la maîtrise de la langue et de la communication par entrevue**. La solution *good* utilise une stratégie avide et un code propre. Les solutions *mauvais* perdent du temps et de la mémoire, et les solutions *mauvais* obstinent l'idée centrale.

En maîtrisant ce problème, vous démontrerez aux recruteurs que vous pouvez:

- Traduire une contrainte du monde réel (presses à clé minimales) en un algorithme optimal.
- Manipulation de cordes dans l'une des langues principales.
- Communiquez avec confiance la complexité et la gestion des cas.

**Prenez la prochaine fois que vous voyez une question de simulation de chaînes de caractères – rappelez-vous l'amertume d'ajouter 'a' puis incrémenter, et vous serez prêt à impressionner tout gestionnaire d'embauche. Bon codage ! **