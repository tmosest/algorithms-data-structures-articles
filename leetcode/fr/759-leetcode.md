---
titre: LeetCode 759. Temps libre des employés -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. Solutions de code

Voici trois implémentations indépendantes et entièrement commentées qui résolvent **LeetCode 759 – Temps libre des employés**.
Chaque mise en œuvre suit la même stratégie *merge-intervalles*:

1. Aplatir tous les horaires des employés en une seule liste d'intervalles.
2. Trier la liste par heure de début.
3. Fusionner les intervalles de chevauchement en enregistrant les écarts entre eux.

Le résultat est la liste des intervalles libres finis communs à **tous** employés.

> **Astuce** – Dans une entrevue, mentionner que l'approche fonctionne dans le temps `O(N log N)` (dominé par le tri) et `O(1)` espace supplémentaire au-delà de la liste des résultats.

---

- Oui. Java – Propre et intuitif

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Recouvrements;
Importer java.util. Comparateur;
Importer java.util. Liste;

***
* Définition pour un intervalle.
* Vous pouvez également utiliser la classe Interval fournie à partir de LeetCode.
*/
Intervalle de classe {
int début, fin;
Interval() { this.start = 0; this.end = 0; }
Interval(int s, int e) { this.start = s; this.end = e; }
@Override
public Chaîne toString() { retour "[" + début + "," + fin + "]; }
}

solution de classe publique {
liste publique<Interval> employé temps libre(liste<Liste<Interval>> calendrier) {
Liste<Interval> tous = nouvelle liste de distribution<>();
Liste <Interval> libre = nouvelle liste de distribution<>();

si (horaire) null.isEmpty() retourne gratuitement;

Aplatir tous les intervalles
pour (Liste <Interval> emp : horaire) {
tous.addAll(emp);
}

Tri par heure de début
Collections.sort(toutes, Comparator.comparingInt(a -> a.start));

// 3
Intervalle prev = all.get(0);
pour (int i = 1; i < all.size(); i++) {
Cur interval = all.get(i);
si (cur.start > prev.end) { // trou trouvé
free.add(nouveau Interval(prev.end, cur.start));
prév = cur;
} autres {/
prev.end = Math.max(prev.end, cur.end);
}
}
retour gratuit;
}
}
«» "

---

## Python – Concise et lisible

'`python
de taper l'importation Liste

Intervalle de classe:
def __init__(self, début: int, fin: int):
self.start = début
auto.end = fin
def _repr_(self):
retourner f"[{self.start},{self.end}]"

Solution de classe:
def employé Temps libre(soi-même, calendrier: Liste[Liste[Interval]]) -> Liste[Intervalle]:
N° 1 : Aplati
intervalles = [il pour emp dans le calendrier pour lui en emp]
N° 2 Tri
intervalles.sort(key=lambda x: x.start)

libre = []
prev = intervalles[0]
pour cur en intervalles[1:]:
si cur.start > prev.end: # écart
gratuit.append(Interval(prev.end, cur.start))
prev = cur
Autre: # chevauchement
prev.end = max(prev.end, cur.end)

retour gratuit
«» "

---

## C++ – Moteur STL

'`cpp
#incluez <vecteur>
#incluez <algorithme>

struct Intervalle {
début int;
à l'extrémité interne;
Interval() : début(0), fin(0) {}
Intervalle(int s, int e) : début(s), fin(e) {}
};

solution de classe {
public:
std::vector<Interval> employeeFreeTime(std::vector<std::vector<Interval>& calendrier) {
md::vecteur <Interval> tous libres;
si (schedule.vide()) retourne libre;

Aplatissement
pour (auto & emp : horaire)
tous.insert(all.end(), emp.begin(), emp.end());

//
à l'ordre du jour
[](const Interval&a, const Interval&b){ retourner a.start < b.start; });

// Fusionner et collecter les lacunes
Intervalle prev = tout[0];
pour (size_t i = 1; i < all.size(); ++i) {
Cur interval = tout[i];
si (cur.start > prev.end) { // intervalle libre
free.emplace_back(prev.end, cur.start);
prév = cur;
} autres {/
prev.end = std:max(prev.end, cur.end);
}
}
retour gratuit;
}
};
«» "

---

♪ 2. Article du blog – Le temps libre de l'employé : le bon, le mauvais et le mauvais

> **Titre:** *Salarié temps libre – Le bon, le mauvais et le mauvais: un emploi-intervieweur Guide amical*
> **Mots clés cibles:** `temps libre des employés`, `leetcode 759`, `interval merge`, `job interview coding`, `algorithm interview`, `Python solution`, `Java solution`, `C++ solution "

---

Présentation

Chaque ingénieur logiciel a un problème d'entrevue qui ressemble à un *lot* plus qu'il ne l'est.
LeetCode 759 – *Salarié Temps libre* est l'un de ces problèmes de «look‐simple‐but‐has‐gotchas».

Dans ce billet, nous passerons par:

1. **Le Bon** – pourquoi le problème est une grande question d'entrevue.
2. **Les mauvais** – les pièges communs qui font monter les candidats.
3. **L'Ugly** – cas de bord et bugs subtils qui peuvent dérailler une solution par ailleurs parfaite.

En chemin, nous présenterons des solutions propres et idiomatiques dans **Java, Python et C++** – les trois langues que les intervieweurs aiment voir.

> **Pourquoi est-ce important? * *
> Une bonne compréhension des problèmes d'intervalle démontre votre capacité à penser à *overlap*, *conditions limites* et *stratégies d'équilibre* – compétences qui sont inestimables dans le code de production.

---

- Oui. Le Bon : pourquoi 759 est un Gold-Mine pour les entrevues

Raison de ce qu'il montre
C'est quoi, ça ?
**Simplicité**La déclaration est courte, la structure des données (intervalles) est intuitive. Autres
**Approches multiples** Les candidats peuvent choisir celui qui convient à leur confort. Autres
**Analogie du monde réel** Autres
**Edge-case Rich**. Autres
**Échelle**La solution s'étend naturellement aux listes de «k» (fusion de k-way). Autres

### À emporter avec l'intervieweur

> *Vous êtes à l'aise avec un motif algorithmique classique, et vous êtes capable de l'adapter aux contraintes du problème.

---

- Oui. Les mauvais : des erreurs communes

Pourquoi ça arrive ?
- Oui.
** Supposons que l'entrée est triée en totalité**. Aplatir et trier *avant la fusion. Autres
**Ignorer les intervalles de longueur zéro** Passer les intervalles où `start == fin` ou vérifier la longueur de l'écart. Autres
Autres L'utilisation de `>=` au lieu de `>` conduit à des lacunes manquantes. Autres
**Non Manipulation Horaires vides**= L'entrée nulle ou vide peut lancer `IndexOutOfBounds`.= Retourner la liste vide tôt. Autres
**Objets d'intervalle immuables par rapport à des objets immuables**. Créer un nouvel intervalle pour les intervalles fusionnés. Autres

> Le diable est dans l'étape de tri. Beaucoup de candidats sautent parce qu'ils voient l'horaire de chaque employé est trié. (en milliers de dollars)

---

- Oui. L'horrible : les cas de bord qui énervent même les plus intelligents

Qu'est-ce qui arrive ? Comment manipuler ?
Il n'y a pas de problème.
**Très grands nombres**= valeurs `end` jusqu'à `10^8` – pas de débordement en int. Utilisez `long` dans les langues qui l'exposent (Java) si vous voulez une sécurité supplémentaire. Autres
**Tous les employés occupés tout le temps** Après fusion, si la liste est vide, retournez-la. Autres
**Single Employee** Toujours fonctionne – l'algorithme réduit à une seule fusion de liste. Autres
**Intervalles Touchant exactement**= `[1,3]` et `[3,5]` – pas de temps libre. Utiliser la comparaison `>` et non `>=`. Autres
**Intervalles hors de l'ordre au sein d'un employé** Une solution robuste pourrait d'abord réorganiser chaque liste d'employés. Autres

---

Récapitulation de l'algorithme – Fusion-Intervalles

1. **Flatten** tous les intervalles dans un seul tableau.
2. **Trier** par "départ".
3. **Itérer** une fois, fusionner les chevauchements et enregistrer les lacunes.
4. Rends les vides.

Complexité

Heure Espace
- C'est quoi ?
`O(N log N)` – `N` = intervalles totaux, en raison du tri `O(1)` extra (résultat d'écart)

> **Pourquoi cela importe :**
> L'intervieweur s'intéresse souvent plus à votre *processus de réflexion* qu'aux micro-optimisations, mais savoir la complexité vous donne un avantage.

---

## Code Afficher-et- Dites

Histoire Autres
C'est pas vrai.
**Java** Int`; mute `prev` pour la brièveté. Autres
**Python**= Compréhension de la liste pour aplatir; lambda trier la clé. Autres
**C++**= STL `sort` avec lambda; `emplace_back` pour l'efficacité. Autres

(Voir les blocs de code ci-dessus.)

---

- Oui. Comment faire l'entretien

1. **Demander des précisions**
* Les intervalles sont-ils inclusifs ou exclusifs?
* Devrions-nous ignorer les intervalles de longueur zéro? (Clarifie toujours.)

2. **Parlez de votre processus de pensée**
* Les listes sont aplaties d'abord parce que chaque employé est trié individuellement. (en milliers de dollars)
* Ensuite, je vais fusionner tout en recueillant des lacunes. (en milliers de dollars)
Enfin, je vais rendre les vides. (en milliers de dollars)

3. **Écrire un code propre**
* Évitez les bugs cachés comme `>=` vs `>`.
* Utiliser des noms de variables descriptives (`prev`, `cur`).

4. **Cas de bord d'essai**
* Un seul employé.
* Des horaires qui se chevauchent complètement.
* Intervalles adjacents.
* Entrée vide.

5. **Exposer la complexité**
* Le tri domine l'exécution à `O(N log N)`.
* La fusion est linéaire.

6. **Prolongations des peines**
* Si nous devions supporter des limites infinies, nous pourrions les traiter comme `INT_MAX` et `INT_MIN` et les ignorer. (en milliers de dollars)

---

## Dernier départ

LeetCode 759 est *pas* une question astucieuse; c'est un problème d'entrevue *bien équilibré* qui teste les bases de la conception de l'algorithme, la manipulation soigneuse des limites et la robustesse du code.

En maîtrisant le **Good**, en évitant le **Bad**, et en confrontant le **Ugly**, vous partirez avec une solution *confidente, bien structurée*, qui montre exactement pourquoi vous êtes le bon candidat pour un rôle de production.

Bonne chance, et rappelez-vous : *les intervalles ne sont que des timbres-temps qui attendent votre intuition gourmande. *

---

> **Vous voulez vous entraîner? **
> Essayez d'écrire la solution dans votre langue préférée, puis exécutez-la contre le harnais de test suivant (disponible sur GitHub).

---

** Bon codage !**
---

> **Auteur:**
> **Contact:** `alex.johnson@example.com "
> **S'abonner** pour plus de tutoriels prêts à l'entrevue.
> ** Suivez :** @AlgoMentor sur Twitter.

---

> **Disclaimer:** *Les extraits de code ci-dessus sont à des fins éducatives. Toujours les adapter à votre propre style de codage. *

---

* Fin du poste. *

---

**Note moyenne (pour les recruteurs et les gestionnaires d'embauche): * *
Lorsque les candidats peuvent articuler l'histoire de *Bonne, mauvaise, mauvaise* et fournir des solutions propres dans les principales langues, ils démontrent le mélange de * résolution de problèmes, communication et préparation à la production* dont chaque équipe moderne a besoin. Cet article est un ajout idéal à votre trousse de préparation d'entrevue.