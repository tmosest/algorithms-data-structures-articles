---
titre: LeetCode 930. Subarrays binaires avec somme -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 930 – Subarrays binaires avec somme
### Comment faire face à cette question d'entrevue (Java-Python C++)

> **Objectif** – Avec un tableau binaire `nums` et un entier `objectif`, compter tous les sous-arrays non vides dont la somme équivaut à `objectif`.

---

Faits en bref

Mot-clé Pourquoi ça compte
C'est-à-dire
*LeetCode 930*
*Binary subarrays avec la somme*
*préfixe sum + hashmap*
*défaillance de la fenêtre
*O(n) temps, O(n) espace
*codage entretien* , recherche d'intention pour les demandeurs d'emploi

---

Récapitulation des problèmes

Texte
Entrée : nombres = [1,0,1,0,1], but = 2
Produit : 4
«» "

Les quatre sous-tribus sont :
«» "
[1,0,1], [1,0,1], [0,1,0,1], [1,0,1,1] (illustré en caractères gras/en ligne sur LeetCode)
«» "

---

Aperçu de la solution

La boucle double naïve `O(n2)` fonctionne mais est trop lente pour les éléments de 30 k.
Un *sliding window* ne fonctionne que pour les nombres **positifs**; les zéros le brisent.
La meilleure façon d'utiliser **préfixer les sommes + une carte de hachage**:

1. Calculer la somme du préfixe «currSum».
2. Pour chaque indice, le nombre de subdivisions se terminant à `i` avec la somme `objectif` est égal à
Compte [curreur Sum - objectif]» (Combien de fois la somme précédente nécessaire est apparue).
3. Mettre à jour `count[currSum]++` pour les indices futurs.

Cela fonctionne dans **O(n)** temps et **O(n)** espace auxiliaire.

---

Mise en œuvre du code

Ci-dessous sont propres, des extraits de production prêts dans **Java**, **Python** et **C++**.

C'est pas vrai. Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
***
* Compte le nombre de subarrays non vides d'un tableau binaire avec somme == but.
*
* @param nums Tableau binaire (éléments sont 0 ou 1)
* Objectif @param Montant cible
* @retour Nombre de sous-tribus admissibles
*/
public int numSubarraysWithSum(int[] nums, int but) {
// Préfixer la somme -> carte de fréquence
Carte<integer, integer> freq = nouveau HashMap<>();
freq.put(0, 1); // préfixe vide

Int currSum = 0;
résultat int = 0;

pour (int num : nombres) {
currSum += num;
// Subarrays s'achève ici avec une somme.
résultat += freq.getOrDefault(currSum - but, 0);
// Enregistrez la somme du préfixe actuel
freq.put(currSum, freq.getOrDefault(currSum, 0) + 1);
}
le résultat du retour;
}
}
«» "

# # # # # #

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def numSubarrays AvecSum(self, nombres: List[int], but: int) -> Int:
"""
Compte les sous-barrages d'un tableau binaire dont la somme égale le but.
"""
pref_count = defaultdict(int)
pref_count[0] = 1 # préfixe vide
_somme_curr = 0
Res = 0

pour n en nombres:
_somme_curr += n
res += pref_count[curr_sum - but] # subarrays se terminant ici
pref_count[curr_sum] += 1

retour res
«» "

C'est vrai. C++

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
utilisant l'espace de noms std;

solution de classe {
public:
int numSubarraysWithSum(vecteur<int>& nums, but int) {
unordered_map<int, long> freq; // utiliser longtemps pour les grands comptages
freq[0] = 1; // préfixe vide
long currSum = 0, ans = 0;

pour (int num : nombres) {
currSum += num;
auto it = freq.find(currSum - but);
si (it != freq.end()) ans += it->seconde;
freq[currSum]++; // enregistrement du préfixe courant
}
retourner static_cast<int>(ans);
}
};
«» "

> **Pourquoi "long" en C++? **
> `n` peut être de 30 k, de sorte que le nombre de subarrays peut atteindre ~450 M. Un int 32-bit déborderait.

---

Résultats

Langage de langue Complexité temporelle Complexité spatiale Remarques
-- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Java (n) O(n) O(n)
Python O(n) Autres
O(n)O(n)O(n)

Tous les trois passent la limite des éléments 3 × 104 en millisecondes.

---

La bonne, la mauvaise et la mauvaise

Aspect du bien
- C'est quoi ?
**Idées algorithmiques**
**Edge Cases**=Poignées `but=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0=0= Autres
**Readability**= Effacer les noms de variables, les commentaires en ligne== Certaines solutions utilisent des boucles imbriquées → difficiles à suivre==Les solutions extrêmement ternes sans commentaires deviennent illisibles===
**Tester**= Vérifier avec `objectif = 0` et les tableaux aléatoires== Ne pas tester avec tous les zéros conduit à des bogues cachés== Ne pas utiliser `long long` pour les comptes → débordement silencieux===

- Oui. Quoi éviter

- **Naïve O(n2)**: passe encore de petits tests mais TLE sur l'entrée maximale.
- **Fenêtre coulissante**: Ne fonctionne que pour les nombres positifs; les zéros brisent l'invariant.
- **Over-optimization**: Enlever la carte de hachage pour la vitesse fait mal à la justesse.

- Oui. Que mettre en avant dans les entrevues

- Expliquez *pourquoi* préfixe des sommes aide: nous réduisons le problème de la somme subarray à une différence de deux préfixes.
- Montrer que les zéros sont manipulés de manière transparente – chaque zéro incréments la même somme de préfixe, de sorte que la carte de hachage compte correctement plusieurs sous-arraies se terminant à différents indices.
- Discutez du compromis : temps O(n) contre mémoire supplémentaire O(n).

---

## ♫ Interview-Ready à emporter

1. **Comprendre le problème** – Le tableau est binaire, donc les sommes de préfixe sont petites.
2. **Cochez l'algorithme droit** – Préfixe sum + hashmap = temps linéaire, espace linéaire.
3. **Write Clean Code** – Utiliser des noms descriptifs, commenter la logique et gérer les cas de bord.
4. **Tester abondamment** – `objectif = 0`, tous les zéros, tous les uns, tableaux d'éléments uniques.
5. ** Expliquer dans Words** – Articuler la solution pendant l'interview : -Nous conservons une somme courante ; chaque fois que nous revoyons la même somme, nous avons trouvé une subarraie qui se résume à zéro, etc. (en milliers de dollars)

---

Article du blog : Les sous-arrachages binaires avec somme – la solution d'entrevue-gagnant

> **Titre**
> *LeetCode 930: Subarrays binaires avec somme – solution O(n) (Java, Python, C++)*

> **Description détaillée**
> Maître LeetCode 930 en quelques minutes ! Apprenez la solution de carte de hachage optimale O(n)-sum en Java, Python et C++. Perfectionnez vos compétences d'entrevue avec un code clair, un traitement de cas de bord et un contenu optimisé par le référencement.

- Oui. 1. Présentation

> Dans les interviews de codage, LeetCode 930 est un problème de moyenne difficulté populaire. Il teste votre capacité à convertir une exigence de sommation en un balayage linéaire avec une carte de hachage. Cet article vous fait découvrir les parties du problème **good**, **bad** et **ugly**, fournit un code propre dans trois langues principales et offre des explications de style interview.

- Oui. 2. Exposé des problèmes et contraintes

> *Input*: `nums` – tableau binaire (`0` ou `1`), longueur jusqu'à 30 000.
> *Objectif* : Compter les sous-tarifs où la somme est égale à "objectif".
> *Objectif* va de «0» à «nums.longueur».
> *Output*: Nombre entier de sous-groupes admissibles.

- Oui. 3. Pièges communs

Pourquoi il échoue Exemple
- C'est quoi ?
Autres Utilisation d'une fenêtre coulissante.Les zéros brisent la propriété de la fenêtre qui augmente strictement.
O(n2) force brute

- Oui. 4. L'approche optimale: Préfixe Sum + Carte de la Hash

- **Idée** : Que le "préfixe" soit la somme des premiers éléments "i".
- **Observation**: Une sous-tribution `(l, r]` sommes à `objectif` iff `préfix[r] - préfix[l] = but`.
- **Mise en œuvre**: Pour chaque `préfixe[r]`, cherchez combien de fois `préfixe[r] - but` est apparu auparavant.

> **Heure**: O(n)
> **Espace**: O(n)

- Oui. 5. Passage du code (Java)

"Java
public int numSubarraysWithSum(int[] nums, int but) {
Carte<integer, integer> freq = nouveau HashMap<>();
freq.put(0, 1); // préfixe vide

somme int = 0, ans = 0;
pour (int n : nombres) {
somme += n;
ans += freq.get OrDefault(somme - but, 0);
freq.put(sum, freq.getOrDefault(sum, 0) + 1);
}
le retour des an;
}
«» "

* Points clés*:
- `freq[0] = 1` gère les sous-barrages qui commencent à l'index `0`.
- `sum - but` est le *cible préfixe* que nous devons avoir vu plus tôt.

- Oui. 6. Python & C++ Variantes

> (Montrer les extraits fournis précédemment.)

- Oui. 7. Liste de contrôle des cas de bord

Autres Tests attendus Pourquoi ça compte
- C'est quoi ?
"Objectif = 0", tous les zéros "n*(n+1)/2"
"Oeil = 0`, mixte" Compte des sous-arrachages de zéros seulement" Ne doit pas compter les sous-arrachages de ceux-ci
"Oeil = n", tous les "1"
Autres Élément unique = 1 si égal au but autre Valeur minimale d'entrée

- Oui. 8. Points d'entrevue

1. *Expliquer* l'intuition préfixe.
2. *Mention* la nécessité du "freq[0] = 1".
3. *Discussion* compromis temps/espace.
4. *Afficher* la solution dans votre langue préférée.

- Oui. 9. Conclusion

> LeetCode 930 est un exemple classique où une utilisation intelligente des structures de données transforme un problème autrement quadratique en un problème linéaire. La maîtrise de ce modèle vous donne non seulement un algorithme prêt à travailler, mais démontre également aux intervieweurs que vous pouvez penser critiquement sous des contraintes.

---

Liste de contrôle finale pour votre recherche d'emploi

- Ajouter le code dans votre portfolio (Java, Python, C++).
Écrire un court billet de blog (comme celui ci-dessus) et l'héberger sur Medium/Dev.to.
- Ajouter l'article à votre GitHub README avec les balises: `#leetcode #930 #binary-subarrays`.
- Pratique expliquant la solution à haute voix (interview de masse).
- Optimiser pour le référencement : ajouter des mots-clés, méta tags, backlinks.

Bonne chance – vos intervieweurs apprécieront la solution propre et efficace et les explications claires!