---
Titre: LeetCode 487. Max Consécutive Ones II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 487. Max Consécutive Ones II – Le guide complet (Java-Python C++)

> **Mots clés** – Max Consécutif Ones II, LeetCode 487, fenêtre coulissante, solution O(n), codage d'entretien, ingénieur logiciel, entretien d'emploi, algorithme, programmation dynamique, flux infini, blog de recherche d'emploi

---

Présentation

Si vous vous préparez à une entrevue d'ingénierie logicielle, vous aurez rencontré au moins une fois LeetCode. Il s'agit d'un défi classique de fenêtre coulissante qui teste votre capacité à penser en temps linéaire tout en manipulant un *simple* a permis de faire un "flip" de 0 à 1.

Ci-dessous vous trouverez:

Langue Nom du fichier Complexité
- C'est quoi ?
**Java**
**Python**
**C++**="solution.cpp"=" **O(n)** temps, **O(1)** espace

Et puis un blog de plongée profonde qui couvre *le bon, le mauvais, et le laid* de ce problème – tout en saupoudrant de contenu SEO-friendly pour vous aider à atterrir cette interview.

---

1. Solutions de code

#### 1.1 Java

"Java
// Solution.java
solution de classe publique {
public int findMaxConsecutiveOnes(int[] nums) {
int maxLen = 0; // séquence la plus longue trouvée jusqu'à présent
int gauche = 0; // lié à gauche de la fenêtre coulissante
int zéros = 0; // nombre de zéros dans la fenêtre actuelle

pour (int droite = 0; droite < nums.longueur; droite++) {
// Étendre la fenêtre en ajoutant l'élément le plus droit
si (en chiffres) 0) zéros++;

// Si nous avons plus d'un zéro, rétrécissez à gauche
pendant que (zéro > 1) {
si (nums[gauche]] 0) zéros--;
gauche++;
}

// Mettre à jour la meilleure réponse
maxLen = Math.max(maxLen, droite - gauche + 1);
}
retour maxLen;
}
}
«» "

#### 1.2 Python 3

'`python
# solution. py
Solution de classe:
def findMaxConsecutiveOnes(self, nombres: List[int]) -> Int:
max_len = 0
gauche = 0
zéros = 0

pour droite, val in énumérate(nums):
si val == 0:
zéros += 1

alors que zéro > 1 :
si nombres[à gauche] 0:
zéros -= 1
gauche += 1

max_len = max(max_len, droite - gauche + 1)

_retourner maxlen
«» "

*## 1.3 C++

'`cpp
// solution.cpp
solution de classe {
public:
dans findMaxConsecutiveOnes(vecteur<int>& nums) {
int maxLen = 0, gauche = 0, zéros = 0;
pour (int right = 0; right < nums.size(); ++right) {
si (en chiffres) 0) + zéros;

pendant que (zéro > 1) {
si (nums[gauche]] 0) --zéros;
+ + gauche;
}
maxLen = maxLen, droite - gauche + 1;
}
retour maxLen;
}
};
«» "

---

2. L'article du blog – Le bon, le mauvais et le mauvais

> *Pourquoi cet article? *
> Si vous cherchez à **booster votre CV** et impressionner les gestionnaires d'embauche, écrire un billet comme celui-ci démontre la profondeur, les compétences en communication et la résolution de problèmes dans le monde réel – tous les traits que les recruteurs aiment.

> *Comment le référencement aide-t-il? *
> En utilisant des mots-clés tels que *=LeetCode 487, *=Max Consécutive Ones II, *=Codage de l'entrevue* et *=Algorithme de la fenêtre coulissante**, l'article est plus susceptible de faire surface dans les recherches par les gestionnaires d'embauche, les recruteurs ou les autres candidats se préparant aux entrevues.

---

### 2.1 Déclaration de problème (Code de bord 487)

> **Grâce à un tableau binaire `nums`, retournez le nombre maximum de `1`s consécutifs dans le tableau si vous pouvez retourner au plus un `0`.
> **Exemple**
> ```texte
> Entrée : [1,0,1,0]
> Produit : 4
> Explication : Dépliez le premier 0 → [1,1,1,1,0]
> `` "
> **Constraints**
> 1 ≤ longueur nominale ≤ 105
> * nombres[i] = 0 ou 1

---

2.2 Pourquoi cela compte dans les entrevues

* **La pensée algorithmique** – Reconnaît le modèle classique *la fenêtre coulissante*.
* ** Optimisation de l'espace** – Faits saillants comment atteindre la mémoire O(1).
* **Manipulation de la valise** – Manipulation de tableaux pleins de `1`s, tous `0`s ou un seul élément.

Les gestionnaires d'embauche apprécient les candidats qui peuvent traduire une description de problème en une solution efficace et propre.

---

2.3 La bonne – Fenêtre coulissante, O(n) Heure

- **Intuition** – Gardez une fenêtre `[gauche, droite]` qui contient au plus un `0`.
- Pourquoi O(n) ? * *
*Chaque index est visité au plus deux fois:* une fois lorsque `droit` s'étend, une fois lorsque `gauche` contrats.
- **Espace O(1)** – Seulement les compteurs et les pointeurs.

> *Conseil:* Dans l'entrevue, expliquer les invariants:
> La fenêtre tient toujours ≤1 zéro. Si l'ajout d'un nouvel élément créerait un second zéro, nous glisserons à gauche jusqu'à ce que le nombre zéro retombe à 1. (en milliers de dollars)

---

2.4 Les mauvaises – Pièges communs

Piège Explication
- C'est quoi ?
En utilisant `droite - gauche` au lieu de `droite Ajouter +1
Autres Oublier de rétrécir sur le *first* 0% Lorsque le premier zéro apparaît, nous l'autorisons encore, mais ajouter un second zéro brise la règle.
Utiliser `pour (int left = 0; left < n; ++ left)`'Wrong: nous avons besoin de contracter *intérieur* la boucle, pas une boucle extérieure séparée.

Ces erreurs entraînent souvent un dépassement du délai (TLE) ou une mauvaise réponse (WA) dans les plateformes de codage.

---

2.5 L'Ugly – Variante de flux infini

**Question de suivi**: *=Et si les nombres venaient comme un flux infini? Vous ne pouvez pas stocker tous les éléments.

**Solution** – Maintenir :

1. `lastZeroIdx` – indice du zéro le plus récent.
2. `countOnes` – nombre de suites vues jusqu'à présent.
3. "maxLen" – meilleure réponse.

Quand un nouveau `1` arrive, incrémenter `countOnes`.
Quand un `0` arrive, mettez à jour `maxLen` en utilisant la distance entre `lastZeroIdx` et l`index courant, puis définissez `lastZeroIdx` à l`index courant et réinitialisez `count Les uns.

**Code Pseudo**:

Texte
maxLen = 0
lastZeroIdx = -1
courantLen = 0

pour chaque bit b entrant à la position i:
Si b) 1 :
actuel Len += 1
Autrement: // b == 0
maxLen = maxLen, i - lastZeroIdx) // retourner ce zéro
lastZeroIdx = i
courantLen = 0

// Après la fin du flux (si c'est le cas)
maxLen = maxLen, courantLen
«» "

Cela fonctionne dans **O(1)** espace et traite chaque élément dans **O(1)** temps – parfait pour la diffusion de données.

---

2.6 Résumé de la complexité

L'approche Temps Espace
- C'est quoi ?
Fenêtre coulissante (Array)
PDD/préfixe-sum
Volet infini O(1) par élément **O(1)**

---

2.7 Conseils d'entrevue

Motif Autres
- Oui.
**Expliquez l'invariant** Autres
Autres **Parler des cas de bord** ► Les recruteurs testent les candidats sur 0 longueur, tous les sujets, tous les zéros. Autres
**Mention temps/espace compromis** Autres
**Écrire un code propre, commenté** Autres
Autres **Afficher l'idée d'un flux infini**= Même si l'interview ne demande que le cas du réseau, présenter la variante en streaming met en valeur la créativité. Autres

---

2.8 Pourquoi ce blog aide-t-il votre recherche d'emploi

1. ** Démontrer l'expertise** – Un article clair et bien structuré montre que vous pouvez expliquer les algorithmes aux intervenants non techniques.
2. **SEO visibilité** – Les gens qui cherchent la solution Consecutive Ones II de Max vous trouveront. Les recruteurs cherchent parfois des blogs de candidats.
3. ** Portefeuille de contenu** – Ajoutez cet article à votre blog GitHub README, LinkedIn ou à votre blog personnel pour mettre en valeur les compétences en résolution de problèmes et en communication.
4. **Interview prep** – Relire ce post renforce les concepts, vous rendant plus confiant lors des entrevues de codage en direct.

---

3. Résumé

- **Problème**: Trouvez le maximum consécutif 1 après avoir retourné au plus 0.
- ** Solution optimale**: Fenêtre coulissante avec ≤1 zéro, **O(n)** temps, **O(1)** espace.
- **Infini-stream**: Maintenir le dernier indice zéro et compter le courant pour un algorithme en ligne O(1).
- **Stratégie d'entrevue**: Discutez des invariants, des cas de bord et des pièges potentiels.

** Préparez-vous à avoir cette interview** en pratiquant la fenêtre coulissante, en écrivant du code propre en Java, Python et C++, et en partageant vos idées à travers un billet de blog poli. Bonne chance ! C'est ce qu'il a dit.

---