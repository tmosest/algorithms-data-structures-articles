---
titre: LeetCode 1386. Répartition des sièges du cinéma -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code – 3 langues

Voici les solutions **complètes, prêtes à copier** pour le problème LeetCode **1386 – Allocation des places du cinéma**.

Pourquoi ça marche
C'est pas vrai.
**Java**=Hash‐Map + cupidité par rang=' Garde seulement les lignes qui ont réellement des réserves. Pour chaque ligne, nous vérifions si l'allée gauche (`2–5`), le centre (`4–7`) ou l'allée droite (`6–9`) est bloquée. Autres
Chaque rangée est représentée par un entier de 10 bits (bits 1‐10). Les trois fenêtres possibles sont vérifiées avec des masques bit-wise. Autres
**C++**== `unordered_map` + bit‐mask=== Même idée que Python, mais en utilisant des entiers 64 bits pour la vitesse. Autres

> **Conseil** – Dans chaque langue, le nombre de lignes que *don=t* apparaissent dans `reservedSeats` peut être traité comme des lignes entièrement libres et donner des groupes `2` chacun, en nous sauvent de l'itération de plus de 10^9 lignes.

---

#### 1.1 Java – HashMap + Greedy

"Java
Importation de java.util.*;

solution de classe {
public int maxNumberOfFamilies(int n, int[][] réservéSeats) {
// ligne -> liste des sièges réservés
Carte<enteger, Liste<enteger>> carte = nouvelle HashMap<>();

pour (int[] siège : réservéSeats) {
map.computeIfAbsent(seat[0], k -> new ArrayList<>())add(seat[1]);
}

int ans = 2 * (n - map.size()); // lignes sans réservation

pour (Liste <entier> sièges : map.values()) {
booléen gauche = faux, droit = faux, milieu = faux;

pour (int s : sièges) {
si (s >= 2 && s <= 5) gauche = vrai;
si (s >= 6 && s <= 9) droit = vrai;
si (s >= 4 && s <= 7) milieu = vrai;

Si (gauche && droite && milieu) pause; // ne peut pas s'asseoir un groupe
}

// ajouter des groupes encore possibles
si (!gauche) ans++; // gauche allée
si (!right) ans++; // allée droite
if (gauche & & & & & & !mid) ans++; // fenêtre centrale seulement
}

le retour des an;
}
}
«» "

---

#### 1.2 Python – Dictionnaire + Bitmask

'`python
Solution de classe:
def maxNumberOfFamilies(self, n: int, réservé Sièges: Liste[Liste[int]]) -> Int:
# ligne -> Masque 10 bits des sièges occupés
lignes = {}
pour r, c dans réservé Sièges:
ligne.setdefault(r, 0)
rangées[r]= 1 << (c - 1) # bit 0 → siège 1

# nombre de base: lignes entièrement libres
ans = 2 * (n - len(rows))

# masques pour les trois fenêtres
MOTEUR = (1 << 5) - 1 # bits 1‐5 (positions 0‐4)
DROITE = (1 < < 9) - 1) ^ (1 < < 5) - 1) # bits 6 à 9 (positions 5 à 8)
MID = (1 << 8) - 1) ^ (1 << 3) - 1) # bits 4-7 (positions 3-6)

pour oct dans les valeurs de lignes():
gauche_libre = (occ et gauche) == 0
right_free = (occ & right) == 0
mi_libre = (occ & MID) == 0

if left_free: ans += 1
if right_free: ans += 1
if left_free et right_free et mi_free :
+= 1

retour et
«» "

---

### 1.3 C++ – `unordered_map` + Bitmask

'`cpp
solution de classe {
public:
int maxNumberOfFamilies(int n, vector<vector<int>>& reservedSeats) {
non ordonné_map<int, longues lignes>; // Masque 10 bits

pour (auto & siège : réservéSeats) {
int r = siège[0];
int c = siège[1] - 1; // à base de zéro
les lignes[r]= (1LL << c);
}

long ans = 2LL * (n - ranges.size()); // lignes libres

Const longue longue durée = (1LL << 5) - 1; // 0b11111
longue droite = ((1LL << 9) - 1) ^
DIM longue durée = ((1L << 8) - 1) ^ ((1L << 3) - 1); // 0b11111100

pour (auto &p : lignes) {
long oct = p.seconde;

bool left_free = (occ & LEFT) == 0;
bool right_free = (occ & right) == 0;
bool mi_free = (occ & MID) == 0;

si (sans_gauche) ans++;
si (droite_libre) ans++;
si (left_free && right_free && mi_free)
as++;
}
retour (int)ans;
}
};
«» "

> **Complexité** –
> "O(k)" heure, où "k = reservedSeats.length" (10 000).
> `O(k)` espace pour la table de hachage; au plus les lignes `k` sont stockées.

---

- Oui. 2. Article de blog – Le bon, le mauvais et le mauvais de LeetCode Cinema Seat Allocation

> **Titre prêt au référencement**: *Cinéma Allocation de siège (Code Leet 1386) – Java, Python & C++ Solutions + Guide d'entrevue**
> **Meta-description**: Master LeetCodeS Cinema Seat Allocation problème en Java, Python et C++. Apprenez les meilleures pratiques, les pièges et pourquoi cela compte pour votre prochaine entrevue.

---

2.1 Aperçu

1. **Introduction** – Pourquoi ce problème est une vitrine d'entrevue parfaite.
2. **Récap** – Le cinéma, les familles et les contraintes de réservation.
3. **Le bien – Ce qui rend ce problème grand* *
4. **L'écueil commun et comment les éviter* *
5. **Les cas d'Edge qui font monter les débutants* *
6. **Plongée profonde – Solution algorithmique* *
- Choix de la structure des données
- Logique d'avidité par rang
- Optimisation bit-masque
7. **Code Walk‐through** – Mettre en avant les extraits de clés en Java, Python, C++
8. **Complexité du temps et de l'espace** – Pourquoi `O(k)` bat la force brute.
9. **Testing & Edge Cases** – Comment valider votre code.
10. **A emporter et conseils d'entrevue** – Pourquoi tu devrais maîtriser ça.
11. **Appel à l'action** – Partagez, commentez et suivez pour plus d'entrevues.

---

2.2 L'article

> **[Cinéma attribution des sièges – LeetCode 1386 – Java, Python & C++ Solutions]**
> *Optimisé pour les recruteurs, les intervieweurs et les étudiants de bootcamp. *

---

Introduction

Chaque année, des milliers d'ingénieurs se préparent à des entrevues de codage.
LeetCodes **1386 – Cinema Seat Allocation** est l'une des questions les plus fréquemment posées sur les difficultés moyennes.
Il teste trois compétences de base :

1. ** Optimisation de la structure des données** – nous ne pouvons pas itérer plus de 10 lignes<sup>9</sup>.
2. **Choix de la fenêtre de mariage** – placement des familles dans un bloc de 4 places.
3. ** Manipulation par le bit** – représentation efficace de l'occupation des sièges.

Si vous cherchez à *show off* ce problème sur votre CV ou GitHub, les solutions ci-dessous vous aideront à le faire avec confiance.

---

Récapitulation du problème

Un cinéma a **n** rangées, chacune avec 10 sièges (numérotés 1‐10).
Les familles de quatre personnes veulent s'asseoir ensemble dans l'un des blocs suivants:

Les sièges qui doivent être libres
- C'est quoi ?
Gauche : 2 – 5
Moyenne 4 – 7
Droite: 6 – 9

Le tableau `reservedSeats` liste les sièges qui sont déjà réservés.
Retournez le nombre maximal de familles qui peuvent être assises.

---

C'est vrai. Le bien

Aspect Pourquoi c'est génial
-- -- -- -- -- --
**Linear dans les réservations** – L'algorithme fonctionne dans `O(k)` où `k` est le nombre de sièges réservés, *pas* dans le nombre total de lignes. Autres
**Efficacité spatiale** – Seules les lignes qui contiennent des réservations sont stockées. Autres
**Language-agnostique** – La logique est identique entre Java, Python et C++. Autres
**Readable** – Les drapeaux booléens ou bit-masks maintiennent l'arbre de décision par rang court et clair. Autres

> * Conseil pro :*
> Pour les intervieweurs, mentionnez l'astuce de pré-calculer les 2 familles pour une ligne totalement libre ; elle montre que vous comprenez les contraintes (n peut être 10^9).

---

C'est vrai. Le "Bad"

Problème Cause typique
- C'est quoi ?
**La force brute sur toutes les lignes** – serait time-out ou s'écraserait sur 10^9 lignes. Ignorant l'observation que seules les lignes qui *ont* réserves comptent. Utilisez une table de hachage ou un dictionnaire clé par numéro de ligne. Autres
**Éviter la fenêtre du milieu lorsque les deux allées sont bloquées** Ajoutez une troisième vérification pour la fenêtre du milieu seulement si les deux allées sont bloquées. Autres
**Les erreurs hors-par-un dans bit-mask**=Bit 1 est en fait le siège 0 dans l'indexation basée sur 0. Toujours soustraire 1 lors du déplacement (`1 << (c-1)`). Autres
Autres **Masque Wong pour les fenêtres**=En utilisant des positions de bits erronées ou en évitant les chevauchements.=Définir les masques une fois et les réutiliser. Autres

---

Le "Ugly"

Parfois, les solutions les plus simples semblent désordonnées. Voici quelques pièges dans lesquels les novices tombent souvent :

1. **Tarifs de sièges codés sur la piste** – L'écriture de conditions explicites pour chaque siège (`2–5`, `4–7`, `6–9`) peut conduire à des bugs subtils si une réservation se trouve sur le siège 3, par exemple.
2. **Des calculs de masque répétés dans les boucles** – L'informatique `1 << c` à plusieurs reprises pour chaque siège peut nuire aux performances.
3. ** Copie de données inutiles** – La création d'une copie de `reservedSeats` pour chaque langue ajoute des frais généraux.
4. **Grandes boucles sans ligne** – Certaines personnes essaient de boucler de 1 à n et sautent les lignes réservées ; c'est *impossible* pour les contraintes données.

Éviter ces risques en :
- Utiliser `computerIfAbsent` (Java) ou `rows.setdefault(r,0)` (Python).
- Prédéfinir les masques.
- Travailler directement avec le tableau d'entrée sans copies supplémentaires.

---

Algorithme détaillé (même pour toutes les langues)

1. **Réservations de groupe par rangée. **
`Map<row, mask>` ou `unordered_map<int, long> rows`.
2. **Couvercle de lignes entièrement libres. **
`ans = 2 * (n - ranges.size())`.
3. **Définir des masques pour les trois fenêtres.
- "LEFT = 0b11111" (bits 0‐4).
- "RIGHT = 0b1111100000" (bits 5-8).
- `MID = 0b11111100` (bits 3-6).
4. **Pour chaque ligne occupée** vérifier quelles fenêtres sont encore libres.
Texte
gauche_libre = (occ et gauche) == 0
right_free = (occ & right) == 0
mi_libre = (occ & MID) == 0
«» "
5. **Réponse actualisée**:
- Ajouter 1 pour une allée libre gauche.
- Ajouter 1 pour une allée libre.
- Si les deux allées sont libres * et * le milieu est libre, ajoutez un troisième groupe.

6. **Retour** "ans".

---

#### Testez votre mise en œuvre

'`python
♪ - Oui. Python ------------------
s = Solution()
print(s.maxNumberOfFamilies(4, [[2, 1], [1, 8], [2, 6]]) # → 4
print(s.maxNumberOfFamilies(1, [[1, 2], [1, 3], [1, 4], [1, 5], [1, 6], [1, 7], [1, 8], [1, 9]]) # → 0
«» "

"Java
// - Oui. Java ------------------
int[[]] réservé = {{2, 1}, {1, 8}, {2, 6}};
Solution sol = nouvelle solution();
System.out.println(sol.maxNombreDeFamilles(4, réservé)); // 4
«» "

'`cpp
// - Oui. C++ ------------------
vecteur<vecteur<int>> réservé = {{2,1},{1,8},{2,6}};
Solution sol;
Cout << sol.maxNombreDeFamilles(4, réservé) << endl; // 4
«» "

Les trois solutions produisent le même résultat correct en temps **O(k)** et en mémoire **O(k)**.

---

#### À emporter pour l'intervieweur

* ** Expliquez l'optimisation de la base. **
Mentionnez que vous n'avez pas besoin de stocker 10^9 lignes ; vous ne gardez que les lignes affectées.
* **Afficher la technique bit-mask** (surtout en C++).
C'est un truc soigné qui démontre une compréhension de bas niveau.
* **La complexité** – linéaire dans le nombre de réservations.
* **Cas de bord de mention** – tous les sièges réservés, réservation unique au siège 5, etc.

Ces points de discussion vous aideront à démontrer *clarité* et *profondeur* dans votre solution.

---

- Oui. 3. SEO-Optimized Blog Post

> **Mots-clés cibles**:
> *LeetCode 1386, Cinema Seat Allocation, solution Java, solution Python, solution C++, entretien de codage, conception d'algorithmes, complexité temporelle, complexité spatiale, algorithme gourmand, opérations bitwise, préparation d'entretien, entretien d'emploi, reprise technique. *

---

Titre
**Cinéma répartition des sièges (LeetCode 1386) – Java, Python & C++ Solutions avec plongée profonde**

---

Description de la méta
Résolvez le problème Cinema Seat Allocation avec le code Java, Python et C++ propre. Apprenez l'algorithme avide, l'optimisation bit-mask et la manipulation de cas de bord conviviale d'entrevue dans ce guide convivial SEO.

---

#### En-tête 1 – Introduction
**Master LeetCode 1386: Attribution des sièges du cinéma – Un défi d'entrevue classique* *

---

#### En-tête 2 – Récapitulation des problèmes
Un cinéma, des familles et le puzzle de réservation. Comprendre pourquoi les familles de quatre personnes ont besoin d'un bloc de 4 places et pourquoi les contraintes rendent ce problème simple * et * difficile.

---

#### En-tête 2 – Le bon, le mauvais et le mauvais

- **Le Bon** – Temps linéaire, espace-efficace, langue-agnostique.
- **Les mauvais** – Pièges communs (off‐by‐one, mauvais masques, force brute).
- **L'Ugly** – Plages codées en dur, calculs répétés, grandes boucles sur n.

---

En-tête 2 – Solution algorithmique

1. Reservations de groupe par ligne en utilisant une table de hachage.
2. Compter les lignes libres en O(1).
3. Utilisez une sélection de fenêtres gourmande.
4. Appliquer l'optimisation bit-mask pour le temps O(k).

---

#### En-tête 2 – Passage de code

"Java
Carte <entier, entier> lignes = nouvelle HashMap<>();
rows.computeIfAbsent(row, k -> 0).ouElse(0);
«» "

'`python
rows.setdefault(row, 0)
«» "

'`cpp
rangées[ligne] = rangées[ligne]=1 (1LL << (siège - 1));
«» "

Expliquez en détail les masques et la logique booléenne, avec des commentaires en ligne.

---

#### En-tête 2 – Analyse de complexité

- **Time**: O(k) – linéaire dans le nombre de réservations.
- **Espace**: O(k) – seulement les lignes affectées stockées.

Ces chiffres sont essentiels pour les entretiens.

---

En-tête 2 – Edge- Essais de cas

1. Tous les sièges bloqués → 0 familles.
2. Réservation unique au siège 5 → 1 bloc gratuit dans cette rangée.
3. Les réservations s'étendent sur plusieurs lignes.

Montrez comment utiliser les tests unitaires pour valider ces scénarios.

---

#### En-tête 2 – Conseils d'entrevue

- *= Expliquer l'optimisation de la ligne uniquement* – montre la conscience des contraintes.
*Démontrer l'astuce bit-mask* – impressionne les recruteurs.
- **Discuss cas de bord – dépeint la rigueur.

Ajoutez une courte anecdote sur un candidat qui a réussi à résoudre ce problème et qui a obtenu un emploi dans une entreprise de haute technologie.

---

En-tête 2 – Appel à l'action

> **Avez-vous abordé la répartition des sièges du cinéma? * *
> Laissez un commentaire ci-dessous avec vos propres rebondissements, ou partagez ce post sur LinkedIn.
> Suivez notre chaîne pour plus de guides et d'extraits de code prêts à l'entrevue.

---

Notes

> Code de let 1386 – Cinema Seat Allocation est plus qu'un simple puzzle ; c'est une pièce de portefeuille qui montre que vous pouvez optimiser pour de grandes contraintes et utiliser des astuces de bas niveau.
> Maîtrisez-le, montrez-le sur GitHub, et augmentez votre confiance dans l'entrevue de codage. *

---

> **Publier** sur Medium, dev.to, ou votre blog personnel.
> Étiquette avec les mots-clés de la cible, ajoutez les balises pertinentes et partagez le lien de repo GitHub contenant les trois solutions.

---

- Oui. 4. Enveloppage

Vous avez maintenant :

- ** Trois extraits de code prêts à recharger** (Java, Python, C++) qui s'exécutent dans le temps `O(k)`.
- **Une discussion complète** sur les structures de données, la logique gourmande et l'optimisation bit-wise.
- **Un billet de blog SEO optimisé** qui aidera les recruteurs à vous trouver lorsqu'ils recherchent le code Leet 1386.

Que vous soyez en train de vous préparer à un rôle d'ingénieur logiciel senior, à une startup, ou à un bootcamp de codage, la maîtrise de ce problème vous mettra à part. Bon codage !

---

*Sentez libre de modifier le code ou l'article pour s'adapter à votre style personnel ou au contexte d'entrevue spécifique. *