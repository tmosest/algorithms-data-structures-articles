---
titre: LeetCode 295. Trouver médian à partir du flux de données -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. Trouver médiane à partir du flux de données
### Solution complète (Java-Python C++) + SEO-Optimized Blog Post

---

### TL;DR
- **Problème** – Construire une classe `MedienFinder` qui supporte:
- `vit addNum(int num)` – insérer un nombre à partir d'un flux de données
- `double findMedian()` – retourner la médiane actuelle
- **Complexité** – `addNum` : **O(log n)**, `findMedien` : **O(1)**
- **Approche** – Deux tas (un lourd max pour la moitié inférieure, un lourd min pour la moitié supérieure)
- **Pourquoi ça compte** – C'est un problème d'entrevue classique qui montre que vous connaissez *les files d'attente prioritaires*, *les arbres équilibrés* et *l'analyse amortie*.

---

- Oui. 1. Code – Une mise en œuvre par langue

> La même logique est appliquée dans les trois langues:
> *Maintenir deux tas: `faible` (pap maximum) et `haut` (pap minimum). *
> *Conservez la différence de taille ≤ 1 et `low.peek() ≤ high.peek()'.
> Médiane est soit l'élément supérieur unique (taille od) ou la moyenne des deux sommets (taille égale). *

#### 1.1 Java (style LeetCode)

"Java
Importer java.util. Priorité Demande;
Importer java.util. Comparateur;

classe publique MedianFinder {
// Max-heap pour la moitié inférieure
priorité privée Queue<integer> low = new PriorityQueue<>(Comparator.reverseOrder());
// Min–heap pour la moitié supérieure
finale privée PriorityQueue<Integer> high = nouveau PriorityQueue<>();

public MedianFinder() {}

public vide addNum(int num) {
// / / / / / / /
i (faible.isEmpty()== num <= low.peek()) {
low.offre(num);
} autre {
offre élevée(num);
}

Rééquilibrer de telle sorte que la taille (faible) – la taille (élevée) ≤ 1
si (bas.size() > high.size() + 1) {
offre élevée(faible.poll());
} sinon si (high.size() > low.size() + 1) {
faible.offre(haut.poll());
}
}

public double rechercheMedien() {
Calculer la médiane en O(1)
int total = low.size() + high.size();
si (total % 2] 1) {
// Nombre étrange d'éléments – un tas plus grand tient la médiane
retour low.size() > high.size() ? low.peek() : high.peek();
} autre {
// Même – moyenne des deux sommets
retour (low.peek() + high.peek()) / 2.0;
}
}
}
«» "

#### 1.2 Python

'`python
importation heapq

classe MedianFinder:
def _init_(self):
# max-heap (panneau inversé) et min-heap
Self.low = [] #pap max pour la moitié inférieure
self.high = [] # Mini-pap pour la moitié supérieure

def addNum(self, num: int) -> Aucun:
N° 1 Poussez dans le bon tas
si ce n'est pas soi. faible ou num <= -self.low[0]:
heapq.heappush(self.low, -num) # signe inverse → max‐heap
Sinon:
heapq.heappush (soi-même.haut, num)

N° 2 Rééquilibre
si len(self.low) > len(self.high) + 1:
heapq.heappush (soi-même haut, -heapq.heappop (soi-même bas))
elif len(supérieur) > len(supérieur) + 1:
heapq.heappush(self.low, -heapq.heappop(self.high))

def findMedien(self) -> flotteur:
O(1) médiane
Si len (self.low) == len (self.high):
retour (-self.low[0] + self.high[0]) / 2.0
retour float(-self.low[0]) si len(self.low) > len(self.high) autre float(self.high[0])
«» "

*## 1.3 C++

'`cpp
#incluez <queue>
#incluez <vecteur>

classe MedianFinder {
particulier:
// max-heap (moitié inférieure)
std:priority_queue<int> faible;
// min-pap (la moitié supérieure)
std::priority_queue<int, std::vector<int>, std::gros<int>> haut;

public:
MedianFinder() = par défaut;

vide addNum(int num) {
// / / / / / / / / /
si (faible.vide()== num <= low.top()) low.push(num);
autres haute.push(num);

Rééquilibrer pour garder le niveau le plus bas () - haut () = 1
si (bas.size() > high.size() + 1) {
le haut.push(low.top()); le bas.pop();
} sinon si (high.size() > low.size() + 1) {
low.push(haut.top()); high.pop();
}
}

double rechercheMedien() {
Calcul médian O(1)
si (bas.size() == haut.size())
retour (bas.top() + haut.top()) / 2.0;
retour low.size() > high.size() ? low.top() : high.top();
}
};
«» "

Les trois extraits sont prêts à être collés pour une soumission **LeetCode 295** ou pour une entrevue technique.
N'hésitez pas à ajouter des tests unitaires ou à les intégrer à votre propre échafaudage.

---

- Oui. 2. Pourquoi ce blogue est-il Job‐Interview‐ Prêt

L'objectif n'est pas seulement de résoudre LeetCode 295; il est de démontrer *design* et *optimization* compétences que les gestionnaires d'embauche désirent.
Ci-dessous, nous cassons la solution en trois sections – **Les bons**, **Le mauvais**, **Le mauvais** – afin que vous puissiez articuler les compromis lorsque vous expliquez le code dans une entrevue.

---

2.1 Les bonnes – Pourquoi Cette solution Rocks

Pourquoi il est grand
- Oui.
**O(log n) insertion**Utiliser un tas binaire → *logarithmique* coût, même pour 5 × 104 opérations. Autres
**O(1) la question médiane**=Il suffit de regarder au sommet des deux tas – pas de traversée, pas de copie. Autres
**Space-optimal**= Entrepose chaque élément une fois: **O(n)** total. Autres
**Simplicité & Clarté**=La logique de rééquilibrage est facile à coder, tester et expliquer. Autres
**Scalable**= Fonctionne pour *any* integer range – aucune hypothèse sur la distribution des données. Autres
**Préparé à l'entrevue**=Il montre la maîtrise des files d'attente prioritaires** et **une analyse amortie**– un must-know pour les rôles de structure de données seniors. Autres

---

## 2.2 Les mauvaises – Pièges et causes de bord communes

Pièges Correction / Insight
C'est quoi ?
**Choisir le mauvais type de tas**= En Java: utilisez `Comparator.reverseOrder()` pour le tas max; en Python: signe inverse; en C++: `std::greater<int>` pour le tas min. Autres
**Off‐by‐one sur la différence de taille**= Toujours vérifier `=low.size() – high.size()= ≤ 1'. Oublier cela rompt la logique médiane pour les comptes pair/odd. Autres
**Éviter d'équilibrer après l'insertion**. Un seul `heap.pop()` / `push()` déplace l'élément offensif. Autres
**Débordement entier sur calcul médian**= En Java, lancer à `long` avant d'ajouter: `((long)low.peek() + high.peek()) / 2.0`.
Autres **L'utilisation d'un seul tas (fermeture, scrutin)**=Le clonage d'un tas pour chaque `findMedien()` conduit à **O(n)** temps – *jamais* faire cela dans une interview. Autres

---

## 2.3 L'horrible – Quand les choses tournent mal

Pourquoi ça arrive ?
- Oui.
**Il y a des tas déséquilibrés sur Insert**.Si vous poussez naïvement chaque nombre dans un tas, l'autre reste vide → médiane mal. Autres
**Neglecting Order Contrastint**"low.peek()" doit être ≤ `high.peek()"; sinon la médiane sera de la mauvaise moitié. Autres
**Wrong Median Calcul on Even Size**.Returning `low.peek()` or `high.peek()` seul pour un nombre pair d'éléments est incorrect. Autres
**L'utilisation de la récursion ou de la fusion Tri**= Certaines solutions (par exemple, fusion-tri après chaque insertion) sont *O(n log n)* ou *O(n)* pour la requête médiane – inacceptable pour les grands flux. Autres
**En supposant l'entrée triée**= Si le flux de données est déjà trié, un seul tableau peut donner la médiane en O(1), mais vous *doit* gérer le cas général. Autres

---

- Oui. 3. Bonus: optimisation minuscule pour les petites gammes entières

Si vous savez que les valeurs du flux sont garanties dans `[0, 100]`, vous pouvez abandonner complètement les files d'attente prioritaires:

Concept Complexité
- C'est quoi ?
Java, `int[] freq = nouveau int[101];` "addNum" : **O(1)**, "findMedien" : **O(100)** (constante)
Collections Python. Counter` + prefix sum
* C++ *std::array<int,101> * Voir Java.

Cette variante est *agréable pour la micro-optimisation*, mais la plupart des intervieweurs s'attendent toujours à la solution à deux fois. Ne le mentionnez que si l'entrevue demande explicitement une solution à portée restreinte.

---

- Oui. 4. SEO-Optimized Blog Post: -Le bon, le mauvais, et le mauvais de LeetCode 295 – MedianFinder

> **Mots-clés cibles :** *LeetCode 295*, *MedienFinder*, *trouver la médiane du flux de données*, *deux tas*, *Entretien de Java*, *Entretien de Python*, *Entretien de C++*, *O(log n) file d'attente prioritaire*, *Entretien de structures de données*, *Questions d'entrevue technique*.

---

Titre
**Master LeetCode 295: MedianFinder – Une plongée profonde dans la solution à deux niveaux (Java / Python / C++)**

---

Description de la méta
Apprenez comment implémenter `MedienFinder` pour LeetCode 295 – Trouver Médian à partir de Data Stream – en Java, Python et C++.
Explorez le bon, le mauvais, et la laid des approches communes, et préparez-vous à l'entrevue avec l'insertion O(log n) et la requête O(1).

---

Corps

C'est vrai. 1. Présentation
Le problème** de recherche de la source de données (LeetCode 295) est un élément essentiel des entrevues sur la structure des données.
Il vous force à concevoir une structure de données *dynamique* qui permet de suivre l'élément médian d'un ensemble en croissance constante.
Dans cet article, nous allons parcourir l'algorithme optimal **deux fois**, illustrer comment le coder en **Java, Python et C++**, et mettre en évidence les compromis que vous pouvez discuter lors des entrevues.

C'est vrai. 2. Pourquoi le médiateur compte
- **Fonctionnalité réelle:** L'analyse en streaming, les moteurs de recommandation en ligne et les tableaux de bord des prix des actions doivent tous calculer la médiane à la volée.
- **Signal d'interview:** Démontre le contrôle des files d'attente **prioritaires**, de l'équilibre ** et de l'analyse amortie**.

C'est vrai. 3. Le Bien – Un O(log n) prouvé Stratégie
- **Binary heaps** fournissent l'insertion *logarithmique*, essentielle pour les flux de 105 + nombres.
- **Le rééquilibrage** maintient les tailles de tas proches, assurant ainsi une logique médiane pour les nombres impairs et même.
- **O(1) question médiane** – il suffit de regarder au sommet du tas.

C'est vrai. 4. Les mauvaises – erreurs communes à éviter
- L'utilisation d'un seul tas ou d'un seul tri naïf conduit à des temps de requête O(n).
- Oublier de maintenir la contrainte d'ordre ('low.peek() ≤ high.peek()').
- Débordement entier en Java en ajoutant deux hauts.

C'est vrai. 5. L'Ugly – Ce que les intervieweurs Je ne veux pas
- Le clonage ou le scrutateur se trouve à l'intérieur de «findMedien()».
- Des tas déséquilibrés qui brisent la médiane pour des longueurs impaires ou égales.
- Remise en œuvre de fusion-sort sur chaque insert – un désastre *O(n log n*).

C'est vrai. 6. Détails de la mise en œuvre
- Java: `PriorityQueue<Integer>` avec `Comparator.reverseOrder()` pour le talon max.
- Python: `heapq` avec inversion de signe pour simuler un max-heap.
- C++: `std::priority_queue` pour max-heap et min-heap avec `std::greater<int>`.

Chaque extrait est accompagné de commentaires clairs afin que vous puissiez copier-coller dans LeetCode ou votre IDE.

C'est vrai. 7. Bonus: Lorsque l'entrée est limitée à 0–100
Si le problème garantit de petites gammes entières, un tableau de fréquences donne *O(1) insert* et *O(1)* médiane en pratique.
Mais les intervieweurs s'attendent généralement à la solution générale à deux fois – mentionner l'optimisation seulement si demandé.

C'est vrai. 8. À emporter – Pourquoi devriez-vous faire face à cette question
- ** Compétence en conception :** Montrez que vous pouvez construire une structure de données *dynamique*.
- **Profondeur algorithmique:** requête – une référence d'efficacité classique.
- **Codage confiance:** Code prêt à fonctionner en Java, Python et C++ – parfait pour les tests de codage à distance.

---

Appel à l'action
> Vous voulez casser plus de problèmes LeetCode ? Abonnez-vous pour des plongées plus profondes dans des solutions de structure de données de style interview.

---

Remarque

Mastering LeetCode 295 vous équipe d'un modèle mental puissant : *deux tas + rééquilibrage*.
Vous pouvez discuter des compromis** (bon/mauvais/mauvais) dans n'importe quelle entrevue de structure de données, impressionner les gestionnaires d'embauche avec votre pensée de conception, et partir avec une solution **robuste, prêt à la production** dans trois langues principales.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---

- Oui. 5. Pensées finales

Que vous soyez en préparation pour une interview **Google**, **Amazon** ou **Microsoft**, ce blog et code snipets vous donnent:

1. Une solution *prête à fonctionner* dans la langue de votre choix.
2. Un cadre clair pour expliquer *pourquoi* l'algorithme fonctionne (Bon).
3. Une liste des erreurs courantes à éviter (Bad).
4. Un coup d'œil rapide aux pièges de lisière (Ugly).

Utilisez la narration « Good-Bad-Ugly » pour guider votre histoire d'entrevue, et vous laisserez les recruteurs convaincus que vous êtes un véritable **ingénieur de la structure des données**.

Joyeux entretien !

---