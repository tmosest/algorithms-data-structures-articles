---
titre: LeetCode 1111. Profondeur maximale de deux cordes de parenthèses valides -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation du problème – 1111. Profondeur maximale de nidification de deux cordes de parenthèses valides

Autres Quoi ?
- Oui.
**Input** Longueur ≤ 10 000. Autres
* Objectif * Répartir `seq` en deux sous-séquences disjointes `A` et `B` qui sont également VPS. Le **maximum** de `profondeur(A)` et `profondeur(B)` doit être **minimum**. Autres
**Extrait**= Un tableau entier `réponse` de longueur `=seq=` où `answer[i] = 0` si `seq[i]` appartient à `A`, sinon `answer[i] = 1`.

> **Pourquoi ce problème est-il important? * *
> Il vous apprend à utiliser un *simple compteur* (ou pile) pour distribuer les parenthèses entre deux cordes d'une manière qui équilibre leurs profondeurs. Il s'agit d'un LeetCode classique qui apparaît fréquemment dans les entrevues parce qu'il teste à la fois la compréhension de la profondeur de la pile et la pensée gourmande.

---

- Oui. 2. The Greedy Insight (la partie "Good")

Si nous traversons la chaîne de gauche à droite, nous pouvons garder un seul compteur `profondeur` qui représente le niveau de nidification actuel de la chaîne d'origine.

- Lorsque nous voyons `'('`, nous * devons* ouvrir un support dans `A` ou `B`.
Nous l'affectons à ** l'un des deux groupes** et ensuite **incrément** "profondeur".
L'astuce est d'alterner l'affectation du groupe entre `'('` consécutif au même niveau de nidification.
Pour ce faire, il faut prendre "en profondeur % 2".

- Lorsque nous voyons `')'`, la correspondance `'('` a déjà été attribuée à un groupe.
Pour maintenir l'équilibre entre les parenthèses, il faut mettre ce `''' dans le groupe **same** comme support d'ouverture.
Par conséquent, nous décrémentons `profondeur` *premier* (puisque la profondeur de la paire correspondante est terminée) puis utilisons `profondeur % 2` pour décider du groupe.

> **Pourquoi ça marche ? **
> La parité de la profondeur actuelle nous indique si la paire actuelle de parenthèses est à un niveau pair ou étrange de nidification. En renversant la parité chaque fois que nous ouvrons un support, nous répartissons la nidification uniformément entre les deux groupes, en veillant à ce que la profondeur maximale de chaque groupe soit "ceil(originalDepth/2)"** – le minimum théorique.

---

- Oui. 3. Le "Bad" – Cas et pièges

Piège
- Oui.
Autres **Utiliser la profondeur après incrémentation pour `'(''**) Incrément *après* décider le groupe, sinon vous utiliseriez le niveau de profondeur *next*. Autres
Autres **Utiliser la profondeur avant de décrémenter pour `')''**=Décret *avant* décider du groupe, parce que la parenthèse de clôture appartient à la même paire qui s'est terminée à cette profondeur. Autres
** Supposons qu'une pile soit nécessaire**. Utiliser une pile ajoute de l'espace et du temps inutiles. Autres
**Confuser la séquence suivante avec la sous-chaîne** Le tableau d'affectation ne réordonne pas les caractères ; il se contente de signaler l'appartenance. Aucun réarrangement n'est effectué. Autres

---

- Oui. 4. La performance et la lisibilité

- **Complexité temporelle**: `O(n)` – une passe sur la chaîne.
- **Complexité spatiale**: `O(n)` pour le tableau de réponses (obligatoire par le problème).
- **Readability**: La solution contre-basée est courte et claire, mais l'astuce `% 2` peut être déroutant à première vue. Ajouter des commentaires ou une petite fonction d'aide (`group = profondeur & 1`) aide.

---

- Oui. 5. Mise en oeuvre des références

Vous trouverez ci-dessous une solution **propre, prête à la production** dans **Java**, **Python** et **C++**. Tous les trois utilisent la même logique contre-basée.

---

#### 5.1 Java

"Java
***
* 1111. Profondeur maximale de nidification de deux parenthèses valides
* Solution de Greedy O(n) qui utilise un compteur de profondeur unique.
*/
solution de classe publique {
public int[] maxDepthAfterSplit(String sq) {
int n = longueur suivante();
réponse int[] = nouvelle réponse int[n];
profondeur int = 0; // profondeur de nidification actuelle

pour (int i = 0; i < n; i++) {
c = suiv.charAt(i);
si c == '(') {
// Assigner en fonction de la profondeur du courant, puis incrémenter
réponse[i] = profondeur % 2;
profondeur++;
} autres { // c == ') '
// Décret d'abord, puis attribuer
profondeur...
réponse[i] = profondeur % 2;
}
}
réponse de retour;
}
}
«» "

---

5.2 Python

'`python
Solution de classe:
def maxDepthAfterSplit(self, sq: str) -> Liste[int]:
profondeur = 0
réponse = []

pour ch en suivant:
Si ch == '(':
réponse.annexe(profondeur % 2)
profondeur += 1
Sinon: # ch == ') '
profondeur -= 1
réponse.annexe(profondeur % 2)

réponse de retour
«» "

---

C++

'`cpp
solution de classe {
public:
vector<int> maxDepthAfterSplit(string sq) {
vecteur<int> réponse;
réponse.reserve(seq.size());
profondeur int = 0; // profondeur de nidification actuelle

au lieu de (charte c : suiv) {
si c == '(') {
reponse.push_back(profondeur & 1); // même profondeur % 2
+ profondeur;
} autres { // c == ') '
--profondeur;
reponse.push_back(profondeur & 1);
}
}
réponse de retour;
}
};
«» "

> **Pourquoi `profondeur & 1` au lieu de `% 2`? **
> Bit-wise ET est une petite victoire de performance (et démontre également le tour de parité). Il est entièrement équivalent pour les entiers non négatifs.

---

- Oui. 6. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 1111

> **Titre**: *Mastering LeetCode 1111: Une plongée profonde dans la profondeur maximale de nidification
> **Meta Description** : Apprenez la solution O(n) optimale pour LeetCode 1111 en Java, Python et C++. Comprendre la stratégie gourmande, les pièges et les idées prêtes à l'entrevue.

---

6.1 Introduction

Si vous chassez un rôle d'ingénierie logicielle, vous avez probablement fait face à une question d'entrevue à chaîne qui semble simple à première vue, mais cache une astuce intelligente. Code du leet 1111 – *Profondeur maximale de deux parenthèses valides* – est une de ces pierres précieuses. Il teste non seulement vos côtelettes de codage, mais aussi votre capacité à penser à *équilibre* et *distribution* en un seul passage.

Dans cet article nous allons décomposer:

1. L'idée **core** (le bien).
2. Fréquent **mauvais pas** (le mauvais).
3. Poireaux de performance et conseils de lisibilité (laid).
4. Mises en œuvre intégrales et translingues.

Prêt ? Laisse plonger.

---

6.2 Réévaluation des problèmes

Vous recevez une chaîne `seq` qui est une chaîne de parenthèses valide (VPS). Vous devez le diviser en deux sous-séquences disjointes `A` et `B` de sorte que les deux sont VPS. Votre objectif: **minimiser** `max(profondeur(A), profondeur(B)`. Retourner un tableau qui indique à quel groupe chaque caractère va (`0` pour `A`, `1` pour `B`).

---

6.3 Le point de vue sur l'avidité – le bon

Pensez à la chaîne comme une série de *niveaux de profondeur*:

«» "
0 1 2 3 2 1 0
(()()) → la profondeur augmente et diminue
«» "

Si on divise toujours les crochets à **alterner les profondeurs**, la paire la plus profonde sera partagée aussi uniformément que possible. Officiellement :

- Pour une ouverture `'('` à la profondeur `d`, mettez-la dans le groupe `d % 2`.
- Pour la fermeture correspondante `')'`, après avoir diminué la profondeur, mettez-la dans le groupe `d % 2` aussi.

La beauté ? Un compteur entier («profondeur») suffit; aucune pile ou carte de hachage n'est nécessaire. La profondeur maximale de l'un ou l'autre groupe devient "ceil(originalDepth / 2)", ce qui est le minimum théorique.

---

6.4 Les pièges – Les mauvais

Erreurs dans les résultats
- C'est quoi ?
Augmentation `profondeur` *avant* assigner `'(''''Utilise la mauvaise parité pour l'ouverture actuelle.
Décret `profonde` *after* attribuant `''''''''Décret de fermeture obtient un mauvais groupe
En supposant qu'une pile soit nécessaire.
Mauvaise lecture de la suite de la séquence de la sous-chaîne de la sous-chaîne de la sous-chaîne de la sous-chaîne de la sous-chaîne de la sous-direction de la réponse de la mauvaise réponse si vous réorganisez la commande de conserver l'ordre original; seulement l'adhésion au drapeau

---

#### 6.5 Performance et lisibilité – L'Ugly

- **Heure**: O(n) – un passage linéaire.
- **Espace**: O(n) – tableau de réponses (à retourner).
- **Readability**: «% 2` ou `& 1` peut être source de confusion. L'ajout d'un assistant ('int group = profondeur & 1;') ou de commentaires clarifie l'intention.

---

6.6 Échantillons de codes complets

> Les trois implémentations suivent le même algorithme.
> Choisissez la langue qui correspond à votre pile d'entrevue d'emploi.

C'est vrai. Java

"Java
solution de classe publique {
public int[] maxDepthAfterSplit(String sq) {
int n = longueur suivante();
réponse int[] = nouvelle réponse int[n];
profondeur int = 0;

pour (int i = 0; i < n; i++) {
c = suiv.charAt(i);
si c == '(') {
réponse[i] = profondeur % 2;
profondeur++;
} autre {
profondeur...
réponse[i] = profondeur % 2;
}
}
réponse de retour;
}
}
«» "

Python

'`python
Solution de classe:
def maxDepthAfterSplit(self, sq: str) -> Liste[int]:
profondeur = 0
ans = []

pour ch en suivant:
Si ch == '(':
(profondeur % 2)
profondeur += 1
Autre: # ') '
profondeur -= 1
(profondeur % 2)
retour et
«» "

C++

'`cpp
solution de classe {
public:
vector<int> maxDepthAfterSplit(string sq) {
vecteur <int> ans;
as.reserve(seq.size());
profondeur int = 0;

au lieu de (charte c : suiv) {
si c == '(') {
ans.push_back(profondeur & 1);
+ profondeur;
} autres { // ' ) '
--profondeur;
ans.push_back(profondeur & 1);
}
}
le retour des an;
}
};
«» "

---

### 6.7 Prise- Pour l'intervieweur

- **Pourquoi cette entrevue est prête**: La solution démontre le temps O(n), l'espace auxiliaire O(1), et une approche avide propre.
- **Pourquoi ça compte pour l'embauche**: Vous pourrez expliquer *pourquoi* la parité des travaux de profondeur, anticiper les pièges et écrire un code concis.
- **Quoi pratiquer ensuite**: Essayez le problème «Split Array with Maximum Sum» ; il utilise également la partition avide.

---

6.8 Réflexions finales

LeetCode 1111 peut sembler intimidant en raison de son exigence de deux chaînes, mais la logique sous-jacente est un exemple de manuel de *alterner la parité* pour équilibrer les structures imbriquées. En maîtrisant ce problème, vous gagnerez en confiance dans:

- Traduire les contraintes de problème en compteurs simples.
- Reconnaître quand une pile est exagérée.
- Ecrire du code idiomatique en Java, Python et C++.

Bonne chance, et que vos parenthèses restent toujours équilibrées!