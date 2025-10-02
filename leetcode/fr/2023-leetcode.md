---
titre: LeetCode 2023. Nombre de paires de cordes avec concaténation égale à la cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2023 – Nombre de paires de cordes avec concaténation égale à la cible

Langue Solution Complexité
C'est pas vrai.
*Java** * 1-pass hash map * O(n · L) time, O(n) space *
**Python**============================================================================================================================================================================================================================
*C++ *C(n)

> Si vous voulez décrocher un emploi technologique, vous devez maîtriser les problèmes qui mettent en évidence votre capacité à penser en algorithme et à écrire du code propre. ** Vos futurs intervieweurs* *

Ci-dessous vous trouverez le code complet et prêt à la production pour chaque langue, suivi d'un blog détaillé qui explique le **bon, le mauvais et le laid** de résoudre ce problème. L'article est optimisé pour vous aider à vous classer plus haut sur les moteurs de recherche et être remarqué par les recruteurs.

---

Le problème (Code Leet 2023)

> **Donné** d'un tableau de chaînes de chiffres `nums` et d'une chaîne de chiffres `target`, **retour** du nombre de paires d'indices `(i, j)` (où `i != j`) de telle sorte que `nums[i] + nums[j]]. la cible.

**Contrôles* *

Description
C'est quoi, ça ?
1=2 <= nums.longueur <= 100== Petite taille de tableau
Les chaînes individuelles peuvent être longues.
La chaîne cible peut être longue.
Autres Toutes les chaînes sont composées de chiffres et **pas de zéros de tête**

---

Aperçu rapide

1. ** Approche naïve** – boucles imbriquées O(n2). Fonctionne pour les contraintes données mais n'est pas élégant ou évolutive.
2. **Hash-Map (Optimal)** – O(n) temps, O(n) espace. Comptez les occurrences de chaque chaîne et cherchez ensuite la partie complémentaire de la cible.
3. **Pourquoi Hash-Map?** – Il élimine les comparaisons redondantes, donne une recherche à temps constant et garde le code succinct.

---

Solutions de code

> Toutes les solutions partagent la même idée de base : pour chaque chaîne `s` dans `nums`, si `target` commence par `s`, le suffixe `t` restant doit exister dans `nums` (sauf quand `s=t`, nous devons éviter de compter le même index deux fois).

C'est pas vrai. Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
***
* Compte le nombre de paires ordonnées (i, j) telles que nums[i] + nums[j] == cible.
* Heure: O(n * L)
* Espace: O(n)
*/
public int numOfPairs(String[] nums, String cible) {
Carte<String, entier> freq = nouveau HashMap<>();
pour (String s : nombres) {
freq.put(s), freq.getOrDefault(s), 0) + 1);
}

nombre int = 0;
pour (String s : nombres) {
si (cible.startsAvec(s)) {
String suffix = cible.substring(s.length());
int add = freq.get OuDéfaut(suffix, 0);
si (suffix.egals(s)) add--; // exclusion i == j
nombre += ajouter;
}
}
le nombre de retours;
}
}
«» "

# # # # # #

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

def num_of_pairs(nums: List[str], cible: str) -> Int:
"""
Renvoie le nombre de paires ordonnées (i, j) où nums[i] + nums[j] == cible.
Heure: O(n * L)
Espace: O(n)
"""
freq = compteur(s)
nombre = 0

pour s en nombres:
si cible.commence avec(s) :
suffixe = cible[len(s):]
nombre += freq.get(suffix, 0)
si suffixe == s:
Nombre -= 1 # éviter i == j

Nombre de retours
«» "

C'est vrai. C++

'`cpp
#incluez <vecteur>
#incluez <string>
#inclut <non-ordonné_map>

int numOfPairs(suite::vector<std::string>& Nums, const st::string & cible) {
std::unordered_map<std::string, int> freq;
pour (const auto & s : nombres) {
++fréq[s];
}

nombre int = 0;
pour (const auto & s : nombres) {
si (cible.rfind(s, 0)) 0) { // cible.startsAvec(s)
std::string suffix = cible.substr(s.size());
auto it = freq.find(suffix);
si (it != freq.end()) {
nombre += it->seconde;
i (suffixe) nombre--; // éviter i) j
}
}
}
le nombre de retours;
}
«» "

> Les trois snippets compilent les derniers compilateurs JDK 17 / Python 3.10+ / C++17 et s'exécutent en temps linéaire.

---

Article du blog – Le bon, le mauvais et l'acharnement de la concaténation des paires

> **Titre**: *LeetCode 2023 – Maîtrise du nombre de paires de cordes avec concaténation (Java, Python, C++)*

- Oui. 1. Présentation

Le nombre de paires de cordes avec la concaténation égale au problème de la cible semble faussement simple. Mais il enseigne une leçon qui apparaît dans les interviews de codage du monde réel : ** optimiser les structures de données et éviter le travail inutile** peut transformer une solution O(n2) naïve en une solution O(n) élégante.

Ci-dessous, nous traversons le problème, nous discutons de l'approche naïve, nous expliquons la solution de hash-map optimale et nous réfléchissons sur les aspects *bons, mauvais et laids* de chacun.

> ** Pourquoi lire ça ? * *
> *Si vous vous préparez pour des entretiens techniques, la maîtrise de ce problème va non seulement stimuler votre score LeetCode mais aussi vous donner un point de conversation que les recruteurs aiment. *

---

- Oui. 2. Récapitulation des problèmes

- **Input**: `nums` – tableau de chaînes à chiffres, `target` – chaîne à chiffres.
- **Output**: Nombre de paires ordonnées `(i, j)` (`i, J`) de telle sorte que `nums[i] + nums[j]== la cible.

*Exemples*
1. `nums = ["777,"7,"77","77"], cible = "7777"` → 4 paires
2. `nums = ["123","4","12","34"], cible = "1234"` → 2 paires
3. `nums = ["1","1","1"], cible = "11"` → 6 paires

La nuance clé : **Les indices doivent différer** – la même valeur de chaîne peut apparaître plusieurs fois, et chaque événement compte comme un indice distinct.

---

- Oui. 3. L ' approche naïve

'`python
nombre = 0
pour i dans la plage(n):
pour j dans la plage(n):
i != j et nombres[i] + nombres[j]] cible:
nombre += 1
«» "

**Pour**
*Simple pour écrire et comprendre. *
- Fonctionne sous le problème de petites contraintes (n ≤ 100).

**Cons**
- **O(n2)** complexité temporelle.
- Concaténations redondantes de cordes pour chaque paire.
- Faible évolutivité – serait temps sur des intrants plus importants.

En termes d'entrevue, c'est * assez bon pour une démo rapide*, mais les recruteurs cherchent des solutions *efficaces*. La méthode naïve cache également un bug subtil : si `nums[i]=cible`, vous devez toujours vous assurer que le suffixe existe dans le tableau. La solution hash‐map s'en occupe proprement.

---

- Oui. 4. L'approche optimale (bonne) – Carte d'accès unique

**Idée**
Pour chaque chaîne `s` dans `nums`, si `target` commence par `s`, le suffixe `t` restant doit apparaître quelque part dans `nums`. Compter les occurrences de chaque chaîne nous permet de trouver `t` dans **O(1)**.

**Étapes d'algorithme**

1. **Cartographie de fréquence construite**
`freq[s] = nombre de fois s apparaît en nombres`.

2. **Itérer sur chaque chaîne s**
- Si `cible` commence par `s`, let `t = cible.substring(len(s))`.
- Ajouter `freq[t]` à la réponse.
- Si `t= s`, soustrayez 1 pour éviter d'associer une chaîne à elle-même (les indices devant différer).

**Pourquoi ça marche* *
- Oui. On ne compare jamais chaque paire.
- Recherche constante de la partie complémentaire.
- Linéaire en `n` (plus la longueur de chaîne `L` qui est inévitable parce que nous devons inspecter `cible`).

**Complexités* *
- *Time*: `O(n · L)` – itérations de boucle `n`, chacune faisant une vérification de préfixe et une recherche de carte.
* Espace*: `O(n)` – pour la carte de fréquence.

**Proof d'exactitude* *
Chaque paire commandée qui satisfait à la condition sera comptée exactement une fois:

- Supposons que `(i, j)` soit une paire valide. Let `s = nums[i]`.
- Dans la boucle pour `s`, nous voyons que `cible` commence par `s`, calculer `t = nums[j]`.
- Nous ajoutons `freq[t]`, qui compte *all* indices `k` de sorte que `nums[k] == t`.
- Si `k == j`, l`addition est correcte; si `k=i`, nous soustravons 1 quand `s=t`.

Toutes les paires sont capturées, et aucune paire étrangère n'est comptée.

**Cas d'urgence traités**

- Plusieurs chaînes identiques (`["1","1","1"]`).
- Le suffixe vide (seulement quand `s` est égal `cible`, mais le problème garantit `cible.longueur >= 2)).
- Très longues cordes (la concaténation serait coûteuse, mais l'extraction sous-chaîne est bon marché).

---

- Oui. 5. Extraits de mise en oeuvre (carte de vol à un pass)

(Voir la section du code ci-dessus.)

Les trois langues partagent la même structure :

- Construire un `Counter`/`HashMap`/`unordered_map`.
- Utilisez `startsWith`/`target.rfind`/`target.rfind(s, 0)`.
- `suffix = cible[len(s):]` (ou `substr`).
- Ajouter la fréquence, ajuster pour l'auto-pairing.

---

- Oui. 5. Les pièges potentiels et les erreurs courantes

Pourquoi ça arrive ?
- Oui.
**Collision de valeur de l'Index** – en utilisant une carte clé par *value* mais en oubliant que des valeurs identiques peuvent apparaître à différents indices. En supposant que chaque valeur est unique. Autres
**Off‐by‐one dans le sous-chaîne** – oubliant d'utiliser «len(s)» au lieu de «s.size()». Testez avec un test unitaire qui couvre les chaînes à caractères simples. Autres
**Solf-pairing** – compter `(i, i)` quand `s == t`. Autres
**Grand L** – la concaténation des cordes à l'intérieur des boucles imbriquées peut devenir coûteuse. Autres Même si `n` est petit, concaténer 100 chaînes de caractères 10 000 fois est un gaspillage. Éviter la concaténation en utilisant `startsWith`/`substring`. Autres
** Sensibilité au cas** – traiter «1» et «01» différemment. Le problème ne garantit pas de zéros de tête, mais certaines solutions gâchent les suffixes vides. Assurez-vous que `cible` longueur ≥ 2 et vérifiez `cible.startsWith(s)` d'abord. Autres

---

- Oui. 6. Pourquoi les recruteurs aiment la solution Hash‐Map

- **Échelle** : Le code reste rapide même si `n` augmente à 105 (la complexité du temps ne change pas).
- **Readability**: Une boucle, une carte, une branche minimale.
- **Utilisation idiomatique des caractéristiques linguistiques**: Java="Map.getOrDefault`, Python="s `Counter`, C++="s `unordered_map`.
- **Test-ability** : Test facile à unit-test de chaque composant (carte de fréquence, extraction suffixe, réglage automatique de la paire).

---

- Oui. 7. A emporter pour votre prochaine entrevue

Astuce Comment ça aide
C'est quoi ?
**Démarrer avec une carte de fréquence propre** Autres
**Éviter le double comptage**= Rappelez-vous que le problème demande des paires *ordonnées*, de sorte que `(i, j)` et `(j, i)` sont distinctes. Autres
**Edge-case first**. Écrire des tests pour `"1" * 3` & `"11"`, `"777" * 2` & `"7777"`, etc. Autres
**La complexité du temps est importante**. Même si les contraintes sont petites, elles visent toujours des solutions linéaires ou log-linéaires. Autres
**Leverage intégré dans les aides** Autres

---

- Oui. 8. SEO Boost – Mots clés et métadonnées

- ** Mots-clefs principaux**: LeetCode 2023, nombre de paires concaténation, problème de concaténation de chaîne, solution optimale, question d'entrevue de carte de hachage.
- ** Mots-clés secondaires**: solution Java LeetCode, solution Python LeetCode, solution C++ LeetCode, problèmes de codage d'entretien, algorithme efficace.

> *Ajouter cet article à votre site de portfolio ou LinkedIn blog et regarder recruteurs atteindre! *

---

- Oui. 9. Réflexions finales

- La solution **naïve** est facile mais échoue sur le critère *optimisation*.
- Oui. La solution **hash-map** est concise, évolutive et démontre une compréhension profonde de la structure du problème.
- **Interrogateurs** sonder souvent *pourquoi* vous avez choisi une structure de données particulière – soyez prêt à expliquer l'avantage de recherche `O(1)`.

Pratiquez les trois implémentations, exécutez vos propres harnais de test et essayez d'étendre le problème (p. ex., laissez des chaînes non numériques ou des tableaux plus grands). L'apprentissage que vous gagnez sera inestimable pour votre prochaine entrevue de codage.

---

Bonus : Harnais de test rapide (Python)

'`python
def test():
d'affirmer num_of_pairs(["777,"7","77","77"], "7777") == 4
affirmons num_of_pairs(["123","4","12","34", "1234") == 2
d'affirmer num_of_pairs(["1","1","1"], "11") == 6
print("Tous les tests sont passés!")

essai()
«» "

---

Bon codage, et que votre esprit algorithmique soit aussi vif que votre CV! C'est ce qu'il a dit