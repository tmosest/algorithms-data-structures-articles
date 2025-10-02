---
titre: LeetCode 3527. Trouvez la réponse la plus courante -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3527. Trouver la réponse la plus courante
Récapitulation des problèmes

Compte tenu d'une liste 2-D de «réponses» où chaque sous-liste représente les réponses recueillies en une journée, nous devons déterminer la réponse **la plus courante** à tous les jours **après avoir retiré les réponses en double de chaque jour**.

Si deux ou plusieurs réponses partagent la même fréquence maximale, retournez le **lexicographiquement le plus petit**.

**Contrôles* *

Valeur
- Oui.
1=1 <= réponses.longueur <= 1000 '=
"1 <= réponses[i].longueur <= 1000"
"1 <= réponses[i][j].longueur <= 10"
Autres Chaque réponse ne contient que des lettres anglaises minuscules.

---

Idée de base

* **Dupliquer par jour** – Nous devons compter chaque réponse distincte une fois par jour.
* **Hash map** – Gardez un compteur de fréquence global (`Map<String, Integer>`).
* **Track meilleure réponse à la volée** – Lors de la mise à jour du compteur, nous pouvons vérifier si la nouvelle fréquence bat le meilleur ou s'il est lié à elle, mais est lexicographiquement plus petit.

La complexité temporelle globale est `O(total_answers)` et la complexité spatiale est `O(unique_answers)`.

---

Mise en œuvre des références

Voici des solutions propres et idiomatiques dans **Java, Python et C++**. Chacun suit la même logique : itérer sur des jours, utiliser un `HashSet`/`unordered_set` pour dédoubler dans ce jour-là, mettre à jour le compte global et garder une meilleure réponse.

> **Conseil** – Évitez les boucles imbriquées le même jour plus d'une fois.
> **Edge-case** – Lorsque la liste de réponses est vide, la fonction retourne une chaîne vide (vous pouvez modifier ce comportement si nécessaire).

####==# Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe publique {
chaîne publique trouverCommonRéponse(Liste<Liste<String>> réponses) {
Carte<String, entier> freq = nouveau HashMap<>();
La meilleure chaîne = ";
bestCount = 0;

pour (Liste <String> jour : réponses) {
Set<String> vu = nouveau HashSet<>();
pour (String ans : jour) {
si (see.add(ans)) { // seulement premier événement par jour
int cnt = freq.merge(ans, 1, entier::sum);
// Mettre à jour le mieux si nécessaire
si (cnt > bestCount) (cnt == bestCount && ans.compareTo( best) < 0)) {
bestCount = cnt;
best = ans;
}
}
}
}
le meilleur retour;
}
}
«» "

Python 3

'`python
de taper l'importation Liste
de collections importer par défautdict

Solution de classe:
def findCommonResponse(self, reponses: List[List[str]]) -> str:
freq = defaultdict(int)
meilleure = ""
best_cnt = 0

pour la journée en réponse:
vu = set()
pour les années du jour:
si le véhicule n'est pas vu:
voir.add(ans)
cnt = freq[ans] + 1
freq[ans] = cnt

si cnt > best_cnt ou (cnt == best_cnt et ans < best):
best_cnt = cnt
best = ans
le meilleur retour
«» "

C++ (C++17)

'`cpp
#incluez <vecteur>
#incluez <string>
#inclut <non-ordonné_map>
#inclut <unordered_set>
#incluez <algorithme>

solution de classe {
public:
std::string findCommonResponse(suite std::vector<std::vector<std::string>& réponses) {
std::unordered_map<std::string, int> freq;
md::string best = ";
int mieux Cnt = 0;

pour (const auto& jour : réponses) {
std::unordered_set<std::string> vu;
pour (const auto& ans : jour) {
si (see.insert(ans).second) { // seulement première occurrence par jour
int cnt = +freq[ans];
si (cnt > bestCnt=" (cnt == bestCnt && ans < best)) {
bestCnt = cnt;
best = ans;
}
}
}
}
le meilleur retour;
}
};
«» "

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Dédoublement par jour "O(unique_in_day)" (HashSet)
Mise à jour globale du dénombrement "O(unique_réponses)" (HashMap)
************************

Pour le cas le plus défavorable ('1000 jours × 1000 réponses/jour = 106 réponses'), l'algorithme s'adapte confortablement dans les délais des juges modernes.

---

Article du blog : Le bon, le mauvais, et le lamentable de trouver la réponse la plus commune

> **Cible auprès du public**: Les ingénieurs logiciels se préparent pour le LeetCode ou les entretiens de codage, en particulier ceux qui regardent les rôles à forte intensité de données (analyste de données, ingénieur de backend, etc.).
> **Mots-clés du référencement**: `leetcode 3527`, `la réponse la plus fréquente`, `hash map interview question`, `Java Python C++ solution`, `algorithme interview`, `fréquence compteur`, `élimination du duplicate`, `lexicographiquement plus petit`.

---

Introduction

Lorsque vous entrez dans une entrevue axée sur les données, vous êtes souvent demandé de traiter de grands volumes de chaînes ou de nombres. Une question faussement simple est de savoir quelle est la réponse la plus courante** – une variante du problème classique du compteur de fréquence. Bien qu'il semble trivial, des pièges subtils (duplications, rupture de cravate lexicographique) peuvent vous faire trébucher. Dans ce post, nous traversons le **bon** ( logique claire, optimale), le **mauvais** (erreurs courantes) et le **ugly** (des cauchemars de cas de référence). Nous terminons avec une solution polie, prête à l'entretien en Java, Python et C++.

---

### Le Bon: Simplicité et efficacité

* **Dédoublement par jour** – Un seul `HashSet`/`unordered_set` par jour élimine les duplications dans *O(day_longueur*).
* ** Comptabilité de laissez-passer unique** – Mise à jour d'une carte de hachage globale pendant que l'itération est O(1) amortie par élément.
* **Le meilleur suivi en vol** – Pas besoin de passer séparément pour trouver le maximum.
* **Clean tie-breaking** – `String.compareTo` (ou `<` dans Python) gère l'ordre lexicographique avec grâce.

> *Résultat*: Temps linéaire, frais généraux auxiliaires constants par jour – parfait pour les contraintes d'entrevue.

---

### Les mauvaises: Pièges communs

1. **Ignorer les duplicata intra-journaliers**
*Exemple*: `["bon","bon"]` compté deux fois → mauvaise fréquence.
*Fix*: Utilisez un jeu par jour avant de compter.

2. **Multi-passes**
*Première passe* pour dédoubler → *Deuxième passe* pour compter → *Troisième passe* pour trouver max.
*Coût*: Frais généraux supplémentaires O(n) et complexité du code.

3. **Incidences lexicographiques**
*Utiliser `>` ou `>=` au lieu de `<` pour la rupture de l'attache* → retourne une chaîne plus grande lexicographiquement.

4. Les chaînes de caractères en Java
L'utilisation de `StringBuilder` ou `StringBuffer` pour les clés peut entraîner des collisions involontaires.

5. **En supposant une entrée non vide**
Retourner `""` quand toutes les listes sont vides peut ne pas correspondre aux attentes du problème; envisager de lancer une exception ou de retourner `null`.

---

- Oui. L'Ugly: les cas de bord et le dépassement

Pourquoi ça compte ?
- Oui.
Autres **Plus grand nombre de chaînes uniques** (=106)= La carte Hash pourrait atteindre les limites de mémoire. Utiliser le hachage personnalisé (par exemple `String.intern()') ou une solution de stockage externe pour la production. Autres
Autres **Terrasse longue corde**="compareTo" devient cher. Raccourcis par contraintes. Autres
Autres **L'entrée négative ou non-ASCII**La déclaration de problème garantit les lettres minuscules. Toujours garder contre les caractères inattendus si réutilisé ailleurs. Autres
**Le fait de retourner """" peut être trompeur. Décider d'une valeur sentinelle ou lancer une exception. Autres

---

### Une solution propre et prête à l'entrevue

Ci-dessous se trouve l'implémentation Java qui incarne toutes les pratiques de « good » tout en contournant les pièges. Il peut être collé directement dans votre éditeur LeetCode.

"Java
Importation de java.util.*;

solution de classe {
chaîne publique trouverCommonRéponse(Liste<Liste<String>> réponses) {
Carte<String, entier> freq = nouveau HashMap<>();
La meilleure chaîne = ";
bestCount = 0;

pour (Liste <String> jour : réponses) {
Set<String> vu = nouveau HashSet<>();
pour (String ans : jour) {
si (see.add(ans)) { // dupliquer par jour
int cnt = freq.merge(ans, 1, entier::sum);
si (cnt > bestCount) (cnt == bestCount && ans.compareTo( best) < 0)) {
bestCount = cnt;
best = ans;
}
}
}
}
le meilleur retour;
}
}
«» "

*Heure*: 'O(total_réponses) "
*Espace*: "O(unique_réponses) "

La même logique dans Python et C++ n'est que quelques lignes plus courtes – voir les implémentations de référence ci-dessus.

---

### Comment cela aide votre travail de chasse

* **Maîtrise de la structure des données** – Les cartes et ensembles Hash sont des agrafes d'entrevue.
* **Clarté de résolution des problèmes** – Démontre que vous pouvez repérer des contraintes cachées (enlèvement du double, rupture des liens).
* ** Polyvalence des langues** – Résolue dans trois langues populaires; montre la capacité d'adaptation.
* **Code optimisé** – Temps linéaire et mémoire supplémentaire minimale – les recruteurs aiment l'efficacité.

Dans un entretien technique, vous pouvez dire en toute confiance, "I"ll duplicata par jour, mettre à jour un compteur global, et garder la meilleure réponse en un seul passage. C'est un récit propre, prêt à l'entrevue.

---

Conclusion

Trouver la réponse la plus courante peut sembler trivial, mais il teste votre attention au détail, la capacité de gérer les cas de bord, et la compréhension du comptage basé sur le hachage. En suivant l'approche **good**, en évitant les écueils **bad** et en se préparant pour les boîtiers **ugly**, vous atterrissez une solution propre et prête à la production en Java, Python ou C++. Bonne chance pour votre prochaine interview – et le codage heureux! C'est ce qu'il a dit.

---

- Oui. Bonus: SEO–Friendly Meta‐Description

> Master LeetCode 3527 Trouvez la réponse la plus courante avec nos solutions Java, Python et C++. Apprenez l'approche de la carte de hachage optimale, évitez les pièges communs et passez votre entrevue sur la structure des données. - Oui.

---