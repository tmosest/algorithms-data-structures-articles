---
titre: LeetCode 3285. Trouvez les indices des montagnes stables -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Recherche de montagnes stables – LeetCode 3285
**Problème**

> Une montagne est appelée stable si la montagne juste avant elle (si elle existe) a une hauteur strictement supérieure à un seuil donné. *
> Retournez les indices de toutes les montagnes stables.

---

Répartition des problèmes

Point de détail
- C'est quoi ?
**Input**. `int[] height` – hauteurs de montagnes consécutives (‘2 ≤ n ≤ 100') Autres
Valeur de seuil («1 ≤ seuil ≤ 100») Autres
(Java), "List[int]" (Python), `vector<int>` (C++) contenant les indices de toutes les montagnes stables. L'ordre n'a aucune importance. Autres
**Règle spéciale**La montagne `0` est *jamais* stable (pas de montagne précédente). Autres

La tâche est essentiellement une analyse en un seul passage du tableau, en vérifiant l'élément précédent par rapport au « seuil ».

---

- Oui. Principales observations

1. **Scan linéaire est suffisant** – nous n'avons besoin que de l'élément précédent, pas de structure de données supplémentaires.
2. **Arithmétique de l'indice** – lorsque nous sommes à l'indice « i » (i ≥ 1 »), la montagne stable candidate est « i ».
3. **Comparaison strictement supérieure** – seuil de «hauteur[i-1] >».

Ces observations nous donnent un temps O(n) propre, O(1) espace auxiliaire (à part la liste des résultats).

---

- Oui. Algorithme (Pseudocode)

«» "
stableIndices = liste vide
pour i de 1 à n-1:
si hauteur[i-1] > seuil:
ajouter i à stableIndices
retour stableIndices
«» "

C'est ça.

---

Analyse de complexité

Calcul métrique
C'est pas vrai.
**Heure**="O(n)" – un passage sur le tableau. Autres
**L'espace**=O(k)– où `k` est le nombre de montagnes stables (sorties). Autres

(L'espace extra n'est que la liste des résultats; aucun autre conteneur auxiliaire.)

---

## 5.

Cas de bord Quoi faire ?
C'est ce que j'ai dit.
**Longueur minimale du tableau** (`n = 2`) Autres
**Toutes les hauteurs ≤ seuil**Le résultat doit être une liste vide. Autres
**Toutes les hauteurs > seuil**Le résultat est "[1, 2, ..., n-1]". Autres
**Le seuil est égal à une hauteur**. Autres
** Hauteurs négatives** (non autorisées par les contraintes) Si vous élargissez les contraintes, assurez-vous que la comparaison fonctionne. Autres

Erreurs courantes

- Erreurs hors-par-un : ajouter `i` au lieu de `i+1` (lorsqu'on utilise `pairwise` ou Python=s `enumerate`).
- Ignorer cette montagne n'est jamais stable.
- Utiliser `>=` au lieu de `>` pour la comparaison.

---

## 6.

- **Readability** – noms de variables clairs (`idx`, `prevHeight`, `result`).
- **L'élégance d'un liner** – possible en Python avec "pairwise" de "itertools".
- **Pas de mémoire supplémentaire** – une simple boucle ou compréhension.
- **Type sécurité** – types génériques explicites en Java (`Liste<Intégrer>`).
- **Commentaires** – brèves et explicatives qui ajoutent de la valeur.

---

## 7.

- Utiliser `ArrayList` en Java mais pas la capacité de pré-allouer.
- Utiliser `stream().filter()` en Java 8, ce qui ajoute des frais généraux.
- Ecrire une boucle imbriquée ou des appels inutiles.
- Oublier de gérer une entrée vide (bien que les contraintes l'interdisent).

---

Mise en œuvre en 3 langues

Java (OOP + collections)

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
***
* trouve les indices des montagnes stables.
*
* @param hauteur gamme de hauteurs de montagne
* Valeur seuil @param
* @retour liste des indices des montagnes stables
*/
liste publique<entier> stableMountains(int[] hauteur, seuil int) {
Liste <Integer> res = nouvelle liste de distribution<>();
pour (int i = 1; i < hauteur.longueur; i++) { // commencer à 1 parce que 0 ne peut pas être stable
si (hauteur[i - 1] > seuil) {
res.add(i); // l'indice actuel est stable
}
}
retour rés;
}
}
«» "

Python (4 lignes de version concise)

'`python
de itertools importer pairwise
de taper l'importation Liste

Solution de classe:
Def stable Montagnes(self, height: List[int], seuil: int) -> Liste[int]:
# couple donne (prev, curr) pour chaque paire adjacente
retour [i + 1 pour i, (prev, _) dans l'énumération (pairwise(hauteur)) si prev > seuil]
«» "

*Si vous préférez une boucle plus explicite (par exemple, pour les anciennes versions de Python): *

'`python
Solution de classe:
Def stable Montagnes(self, height: List[int], seuil: int) -> Liste[int]:
res = []
pour i dans la plage (1, len(hauteur)):
si hauteur[i - 1] > seuil:
res.append(i)
retour res
«» "

### C++ (bibliothèque standard)

'`cpp
#incluez <vecteur>

solution de classe {
public:
std::vector<int> stableMountains(suite std::vector<int>& hauteur, seuil int) {
std::vector<int> res;
pour (size_t i = 1; i < height.size(); ++i) { // commencer à 1
si (hauteur[i - 1] > seuil) {
le nom de l'entité ou de l'entité concernée;
}
}
retour rés;
}
};
«» "

---

Essais (utilisation simple)

"Java
// Java
Solution s = nouvelle solution();
System.out.println(s.stableMountains(nouvelle int[]{1,2,3,4.5}, 2)); // [3,4]
«» "

'`python
# Python
sol = Solution()
print(sol.stableMountains([10,1,10,1,10], 3)) # [1, 3]
«» "

'`cpp
// C++
Solution s;
auto ans = s.stableMountains({10,1,10,1,10}, 3);
pour (int idx : ans) md::tout << idx << '; // 1 3
«» "

---

Article sur le blog optimisé du SEO

---

Titre
**LeetCode 3285: Trouver des indices des montagnes stables – Java, Python, C++ Solutions & Conseils d'entrevue *

Description de la méta
Résolvez le LeetCode 3285 avec le code Java, Python et C++. Comprendre le problème des montagnes stables, analyser la complexité du temps et de l'espace, apprendre les meilleures pratiques et se préparer aux entrevues.

Mots clés
LeetCode 3285, trouver des indices de montagnes stables, interview de codage, algorithme, structures de données, solution Java, solution Python, solution C++, question de codage d'entrevue, complexité du temps, complexité de l'espace, préparation d'entrevue d'emploi.

---

Introduction

Lors d'un entretien technique, résoudre *LeetCode 3285 – Trouver des indices de montagnes stables* met en évidence votre capacité à traduire un problème réel en code propre et efficace. Ce post vous emmène à travers le problème, plonge dans le bon, le mauvais, et le laid de solutions typiques, et présente Java, Python, et C++ de travail implémentations que vous pouvez copier-coller dans votre harnais de test.

> **Pourquoi ce problème est important:**
> - Il teste **array traversal** et **index arithmétique** – fondamentaux de toute entrevue de codage.
> - La solution est **O(n)** le temps, **O(1)** l'espace auxiliaire, parfait pour une question haut de gamme.
> - Vous allez apprendre à éviter les pièges communs et écrire un code que les recruteurs aiment.

---

Récapitulation des problèmes

Compte tenu d'un tableau entier `hauteur` (taille `n`) et d'un entier `seuil`, une montagne à l'index `i` (où `i > 0') est **stable** si `hauteur[i-1] > seuil. Montagne `0` n'est jamais stable. Retourner tous les indices de montagne stables.

---

#### Le bon – Pour quoi viser

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Scan linéaire**= Un passage – temps minimum. Autres
**Simple Condition** , pas de logique complexe. Autres
**Indexage explicite** Exclure les bogues hors-par-un en commençant par la boucle `1`. Autres
**Aucun Conteneur supplémentaire** Exclusivement liste de résultats/vecteur – efficace en mémoire. Autres
**Clean Code**. Autres

---

Les erreurs communes

1. **Off‐by‐One** – ajouter `i` au lieu de `i+1` lors de l'utilisation de la boucle `énumérer` ou Java= pour`.
2. **Comparaison des erreurs** – en utilisant `>=` au lieu de ">".
3. **Ignorer la montagne 0** – oublier que l'indice 0 n'est jamais stable.
4. **Complexité inutile** – utilisation de flux ou d'appels récursifs où une simple boucle suffit.

---

#### - Les choses à éviter

- **Sur-ingénierie** : p.ex. construire une liste complète d'adjacence lorsque seul l'élément précédent compte.
- **Grande empreinte mémoire** : pré-allouer d'énormes tableaux ou listes lorsque ce n'est pas nécessaire.
- **Hacks spécifiques à la plate-forme**: utilisation de «pairwise» dans Python uniquement lorsque l'interprète le supporte (Python 3.10+).

---

Code Passage

(Voir les sections ci-dessus pour les extraits complets de Java, Python et C++.)

- **Java** : utilise `ArrayList<integer>` pour le calibrage dynamique.
- **Python**: La solution 4 lignes met à profit "itertools.pairwise" pour l'élégance.
- **C++**: Une boucle `pour` simple avec des indices `size_t`.

---

Répartition de la complexité

- **Heure**: "O(n)" – une traversée.
- **Espace**: `O(k)` – liste de sortie/vecteur; l'espace auxiliaire est constant.

---

Conseils d'entrevue

- ** Expliquer la logique d'abord**: Nous regardons la montagne précédente... si elle dépasse le seuil, la montagne actuelle est stable. (en milliers de dollars)
- **Boîtes de bord de la Mention**: Quand `n = 2` ou lorsque toutes les hauteurs sont inférieures au seuil. (en milliers de dollars)
- **Afficher un harnais d'essai**: Utilisez les exemples fournis et quelques cas de bord.
- **Afficher l'efficacité**: Temps linéaire, espace auxiliaire constant – optimal pour cette taille de problème. (en milliers de dollars)

---

Autres lectures

- Problème de LeetCode 3285: https://leetcode.com/problèmes/indices-de-stable-montagnes/
- Plans de traversée des rayons: https://leetcode.com/articles/array-traversal/
- Documentation Python `itertools` : https://docs.python.org/3/library/itertools.html

---

Conclusion

LeetCode 3285 est un exemple de manuel de transformation d'une simple observation en une solution propre et optimale. La maîtrise démontre la maîtrise de la manipulation du réseau, les conditions de limites et le codage concis – tous les recruteurs de compétences cherchent. Déposez l'échantillon dans votre IDE, faites quelques tests, et vous serez prêt à répondre à cette question dans n'importe quelle interview.

Joyeux codage, et que les montagnes stables vous favorisent!

---

** (Fin de l ' article)**

---

À emporter

Vous avez maintenant :

1. Une compréhension profonde du problème et de ses contraintes.
2. Voyez ce qui fait une solution --good-- versus --bad-- ou--ugly. (en milliers de dollars)
3. Prêt à utiliser le code Java, Python et C++ qui fonctionne efficacement.
4. Un article de blog entièrement optimisé pour vous aider à pratiquer ou à partager avec vos pairs.

Utilisez ces connaissances pour impressionner les recruteurs, résoudre le problème sur LeetCode et passer à votre prochain entretien technique. C'est ce qu'il a dit.

---