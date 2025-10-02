---
titre: LeetCode 2053. Kth Distinct Chaîne dans un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2053 – Kth Chaîne distincte dans un tableau
C++ – 3 solutions propres et prêtes à l'entretien* *

> **Pourquoi ce problème est important* *
> *LeetCode 2053* est une question d'entrevue qui teste trois compétences de base :
> 1. **Hash-map / dictionnaire** utilisation pour le comptage des fréquences.
> 2. **Logique à deux passages** – premier décompte, puis trouver la cible.
> 3. **Ordonnance** – préserver l'ordre de première apparition.
> La maîtrise montre que vous pouvez résoudre des problèmes réels en temps O(n) et en espace O(n), un must-have pour toute entrevue d'ingénierie logicielle.

---

- Oui. 1. Déclaration de problème (Code de bord 2053)

Avec un tableau de chaînes minuscules `arr` et un entier `k`, retournez la chaîne distincte *k*-th dans le tableau.
Une chaîne *distinct* apparaît **exactement une fois** dans `arr`.
Si moins de `k` chaînes distinctes existent, retourner la chaîne vide `""`.

**Contrôles* *

Valeur
-- -- -- -- -- --
1 ≤ k ≤ longueur ≤ 1000
1 ≤ arr[i].longueur ≤ 5
Les lettres anglaises minuscules

---

- Oui. 2. Intuition

1. **Count occurrences** – Une carte de hachage (`string → int`) nous indique si une chaîne est unique.
2. **Itérer de nouveau** – Scanner le tableau original dans l'ordre, garder un compteur de chaînes distinctes trouvées.
3. Quand le compteur est égal à `k`, nous avons trouvé la réponse.
4. Si la boucle se termine avant d'atteindre `k`, retourner `""`.

---

- Oui. 3. Aperçu de la solution

«» "
1. Construire une carte de fréquence : pour chaque s dans arr → freq[s]++.
2. Traverse arr à nouveau:
si freq[s] == 1 :
distinct Consulté++
si elle est distincte Voir == k: retour s
3. retour ""
«» "

**Complexités* *

Temps Espace
C'est le cas.
(pour la carte de fréquence)

*`n` = longueur approximative. *

---

- Oui. 4. Code (3 langues)

> Toutes les solutions sont des classes/fonctions de type LeetCode `Solution`.
> Ils compilent avec Java 17, Python 3.10+ et C++17.

#### 4.1 Java

"Java
Importer java.util. HashMap;

solution de classe {
chaîne publique kthDistinct(String[] arr, int k) {
// 1-
HashMap<String, entier> freq = nouveau HashMap<>();
pour (String s : arr) freq.put(s, freq.getOrDefault(s), 0) + 1);

// 2--Scanner de nouveau pour le k-th distinct
Int distinct Voir = 0;
pour (String s : arr) {
si (freq.get(s)) == 1) {
distinct vu++;
si (distinctSeen == k) retourne s;
}
}
retour ";
}
}
«» "

4.2 Python 3

'`python
de taper l'importation Liste
Importations provenant des collections Compteur

Solution de classe:
def kthDistinct(self, arr: List[str], k: int) -> str:
N° 1 Fréquences de comptage
freq = contre(arr)

N° 2 Trouver le k‐th distinct dans l'ordre
pour s in arr:
si freq[s] == 1 :
k -= 1
si k == 0:
retour s
retour ""
«» "

### 4.3 C++

'`cpp
#incluez <vecteur>
#incluez <string>
#inclut <non-ordonné_map>

solution de classe {
public:
std::string kthDistinct(std::vector<std::string>& arr, int k) {
std::unordered_map<std::string, int> freq;
pour (const auto& s : arr) ++freq[s];

pour (const auto & s : arr) {
si (freq[s]) 1) {
si (--k) 0) retour s;
}
}
retour ";
}
};
«» "

---

- Oui. 5. Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
**Clarté**= Fréquence de passage unique + deuxième passage → facile à lire== Certains peuvent sauter le second passage et essayer de stocker toutes les chaînes distinctes dans un vecteur (inférieur)=== Défaut d'utiliser `HashMap<String, Boolean>` (true/false) au lieu d'un nombre entier peut conduire à des bogues lorsqu'une chaîne apparaît plus de deux fois. Autres
En utilisant une carte ou une liste triée pour maintenir l'ordre ajoute des frais généraux inutiles. Autres
**Ordonnance**= Ordre naturel conservé parce que nous re-scans `arr`=Relying on `HashMap` itération order (unordered) va briser l'exigence==Le mélange de l'ordre et des vérifications d'unicité dans un seul passage peut se tromper. Autres
Autres **Edge Cases**=Poigne un tableau de chaînes vide, `k` plus grand que le compte distinct=== Aucune=Le retour `""` pour aucun résultat peut être mal interprété comme une chaîne valide dans certains contextes. Autres

**À emporter :** Suivez l'approche à deux passages avec une carte de fréquence. C'est rapide, simple et pare-balles.

---

- Oui. 6. Essais et validation

'`python
# Harnais d'essai Python
def test():
sol = Solution()
Dire sol.kthDistinct(["d","b","c","b","c","a"], 2) == "a"
Dire sol.kthDistinct(["aaa","aa","a"], 1) == "aaa"
Dire sol.kthDistinct(["a","b","a"], 3) == ""
affirmant sol.kthDistinct(["x","x","y","z"], 2) == "z"
print("Tous les tests ont réussi.")
essai()
«» "

Exécuter des essais unitaires similaires en Java (JUnit) et en C++ (GoogleTest ou simple «assert»).

---

- Oui. 7. Variations et extensions

Comment s'adapter
C'est quoi ?
*Trouver le i-th non-duplicate*. Autres
*Normez toutes les chaînes en minuscule/en haut avant de compter. Autres
*Strings avec des chiffres ou des caractères spéciaux*= Pas de changement – les touches de carte fonctionnent pour n'importe quelle chaîne. Autres
*Plus grande entrée (n > 106)* .Utilisez le streaming : comptez d'abord, puis le deuxième passage en streaming ; la mémoire reste O(n) mais peut nécessiter un stockage externe. Autres

---

- Oui. 8. Conseils d'entrevue

1. ** Expliquez votre algorithme avant de coder** – l'intervieweur aime un plan clair.
2. **Cas de bord des peines** : Et si `k` est plus grand que le nombre de chaînes distinctes ? (en milliers de dollars)
3. **Demander des éclaircissements** : faut-il préserver l'ordre original ? (en milliers de dollars)
4. **Choisir la bonne structure de données**: `unordered_map`/`HashMap` est la moyenne O(1).
5. ** Optimisation de l'espace**: Dans C++, utilisez `unordered_map<string, int>`. En Java, utilisez `HashMap`.
6. **Complexité du temps**: soulignez-vous en faisant deux scans linéaires – O(n).
7. **Pratique**: Écrivez la solution sur un tableau blanc; gardez-la propre.

---

- Oui. 9. Conclusion – Pourquoi maîtriser ce problème vous aide à trouver un emploi

LeetCode 2053 est le problème d'entrevue quintessence.
En le résolvant dans **Java, Python et C++**, vous montrez :

* Vous pouvez utiliser **hash-maps** pour le comptage des fréquences – une compétence de base en structure de données.
* Vous comprenez **stable order** et comment le préserver.
* Vous pouvez raisonner sur **temps/espace compromis** et les articuler clairement.

Ce sont exactement les types de conversations que les gestionnaires recrutent recherchent lors d'une entrevue de codage.

> **Prochaine étape** – jumeler le code avec un billet de blog bien écrit (celui ci-dessous). Partagez-le sur LinkedIn, Medium ou sur un site de portfolio personnel. Utilisez les mêmes mots-clés dans votre curriculum vitae : *=Solved LeetCode 2053 en Java/Python/C++ (O(n)) – solution de compte de fréquence prête à l'entrevue.

---

Billet de blog: Chaîne distincte de Kth dans un tableau – 3 Interview-Ready Solutions

> **Cible Public** – Aspirant ingénieurs logiciels, recruteurs, et tous ceux qui veulent un blog de technologie favorable au référencement.
> ** Mots-clés du référencement**: LeetCode 2053, Kth Distinct Chaîne, question d'entretien, interview de codage, solution Java, solution Python, solution C++, conseils d'entretien d'emploi, structures de données, conception d'algorithmes.

---

Titre
**LeetCode 2053 – Kth Distinct Chaîne: Java, Python et C++ Solutions + Conseils d'entrevue**

Description de la méta
> Apprenez à cracher le LeetCode 2053 – Kth Distinct String in an Array. Parfait pour coder la préparation d'entrevue.

---

- Oui. 1. Présentation

Quand les recruteurs scourd Linked Dans ou GitHub pour la preuve des côtelettes algorithmiques, un problème apparaît souvent: Montrez-moi comment résoudre LeetCode 2053.
Cette question teste votre compréhension des cartes de hachage, des scans linéaires et de la préservation de l'ordre – compétences qui se traduisent directement en code de production.

Ci-dessous vous trouverez:

* L'énoncé complet du problème
* Une stratégie algorithmique claire
* Trois implémentations de production (Java, Python, C++)
* Une analyse de bonne qualité qui met en évidence les pièges que vous devriez éviter
* Tester les scripts et les points d'entrevue prêts à parler

Laisse plonger.

---

- Oui. 2. Énoncé de problème (réimprimé pour référencement)

> **Kth Chaîne distincte dans un tableau** (Code Leet 2053)
> *Input*: `string[] arr`, `int k`
> *Output*: `string` – la `k`-th chaîne distincte ou `""` si aucune
> * Distinct* : apparaît **une fois** dans "arr" "
> *Ordonnance*: l'ordre de première apparition est important

---

- Oui. 3. Intuition algorithmique

1. **Monter les fréquences** avec une carte de hachage.
2. **Scannez le tableau dans l'ordre original** et comptez les chaînes distinctes.
3. Retourne la chaîne lorsque le nombre est égal à `k`.

Deux passages linéaires, "O(n)" temps, "O(n)" espace.

---

- Oui. 4. Trois mises en œuvre propres

"Java
Java (style LeetCode) */
solution de classe {
chaîne publique kthDistinct(String[] arr, int k) {
Carte<String, entier> freq = nouveau HashMap<>();
pour (String s : arr) freq.put(s, freq.getOrDefault(s), 0) + 1);

Int vu = 0;
pour (String s : arr) {
si (freq.get(s)) == 1) {
si (++seen == k) retourne s;
}
}
retour ";
}
}
«» "

'`python
# Python 3.10
Importations provenant des collections Compteur
Solution de classe:
def kthDistinct(self, arr: List[str], k: int) -> str:
freq = contre(arr)
pour s in arr:
si freq[s] == 1 :
Si k == 1 : retour
k -= 1
retour ""
«» "

'`cpp
// C++17 (style LeetCode)
#inclut <non-ordonné_map>
#incluez <vecteur>
#incluez <string>

solution de classe {
public:
std::string kthDistinct(std::vector<std::string>& arr, int k) {
std::unordered_map<std::string, int> freq;
pour (const auto& s : arr) ++freq[s];
pour (const auto & s : arr) {
Si (freq[s] == 1 && --k == 0) retour s;
}
retour ";
}
};
«» "

---

- Oui. 5. Liste de contrôle des cas de bord

Pourquoi ça compte ?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
`k` > count distinct. Autres
Dupliquer les chaînes > 2 occurrences.La carte de fréquence gère n'importe quel nombre. Autres
Empty `arr`= Ne doit pas planter. Autres

---

- Oui. 6. Essai

'`python
def run_tests():
sol = Solution()
essais = [
[« d », « b », « c », « b », « c », « a », 2, « a »),
(["aa", "aa", "a"], 1, "aaa"),
(["a","b","a"], 3, "),
(["x", "x", "y", "z"], 2, "z"),
- Oui.
pour arr, k, attendu dans les essais:
affirmer sol.kth Dénomination(arr, k) == prévu
print(""Tous les tests ont réussi.")
run_tests()
«» "

Exécuter l'équivalent Java/JUnit et C++/Google Testez les suites pour valider.

---

- Oui. 7. Variations à discuter

1. **Case-insensible distinct** – `freq[s.lower()]` dans Python, `std::transform` dans C++.
2. ** Chaîne la plus longue** – Remplacer le compteur `k` par une comparaison de longueur.
3. **Streaming input** – Traiter des morceaux et écrire des comptes intermédiaires sur le disque si la mémoire `n` > .

---

- Oui. 8. Points d'entrevue prêts à parler

* ** Expliquer l'algorithme à deux passages** – Souligner le temps O(n) et préserver l'ordre.
* **Pourquoi une carte de fréquence?** – Parce que nous avons besoin de recherche O(1) pour chaque chaîne.
* **Manipulation des caisses** – Retour `""` en l'absence de résultat.
* **Possibles pièges** – Carte booléenne vs le nombre, itération non ordonnée, oubliant le décrément `k`.

---

- Oui. 9. Comment cela sème votre recherche d'emploi

1. **Showcasing Data‐Structure Mastery** – Les recruteurs aiment les solutions claires et évolutives.
2. **Heure d'entrevue rapide** – Le modèle à deux passages est rapide à coder sous une contrainte d'une minute.
3. ** Valeur du portefeuille** – Ajoutez l'extrait de code à votre repo GitHub; marquez-le `#LeetCode2053`.
4. **Resume Bullet** – solution O(n) appliquée pour LeetCode 2053 – Kth Distinct String in an Array, utilisant des cartes de fréquence et des scans commandés. (en milliers de dollars)

---

## 10. Dernier départ

- **Keep it simple** – Carte de fréquence + deuxième passe.
- **Éviter la suringénierie** – Pas besoin de cartes triées ou de vecteurs supplémentaires.
- **Test complet** – Les cas de bord sont les vrais examinateurs d'entrevue.

Avec ces trois implémentations et un récit d'entretien poli, vous êtes prêt à ace LeetCode 2053 et impressionner les gestionnaires d'embauche dans la prochaine ronde. Bon codage !

---