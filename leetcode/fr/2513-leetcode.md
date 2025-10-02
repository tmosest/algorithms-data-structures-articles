---
titre: LeetCode 2513. Minimisez le maximum de deux tableaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – Minimisez le maximum de deux tableaux

On vous donne quatre entiers:

Sens de la variable
C'est pas vrai.
**diviseur1**
**diviseur2**
**uniqueCnt1** Autres
**uniqueCnt2** Autres

Les deux tableaux doivent être disjoints (aucun nombre ne peut apparaître dans les deux).
Votre tâche : **choisir les nombres entiers** pour les deux tableaux de manière à ce que l'entier *maximum* utilisé dans chaque tableau soit aussi petit que possible.
Retourner ce maximum minimum réalisable.

Les contraintes sont énormes («uniqueCnt1», «uniqueCnt2» jusqu'à 109) – une solution de force brute est impossible.

---

- Oui. 2. Intuition

Le problème est une recherche typique sur la réponse* question.

* Si vous fixez une borne supérieure `M`, vous pouvez décider s'il est **possible** de remplir les deux tableaux avec tous les nombres `=M`.
* Si c'est possible, vous pouvez essayer un plus petit `M`; si c'est impossible, vous devez essayer un plus grand.
* La recherche binaire sur `M` donne le maximum minimal possible dans les étapes `O(log range)`.

Le sous-problème clé est donc :

> **Avec une limite `M`, pouvons-nous sélectionner `uniqueCnt1` nombres non divisibles par `divisor1`,
> nombres `uniqueCnt2` non divisibles par `divisor2`, tous ≤ `M`, et tous distincts? * *

La réponse peut être dérivée du simple comptage :

* `cntBoth` – nombres ≤ `M` divisibles par **deux** diviseurs
* `cntOnly1` – divisible uniquement par `divisor1` (pas par `divisor2`)
* `cntOnly2` – divisible uniquement par `divisor2` (pas par `divisor1`)
* `cntAutre` – nombres divisibles par **ni l'un ni l'autre**

Seulement `cntOther` + `cntOnly2` sont des candidats pour `arr1`.
Seulement `cntOther` + `cntOnly1` sont des candidats pour `arr2`.

Si nous essayons de donner `arr1` tous les nombres qu'il peut utiliser, puis vérifier si
`arr2` a encore assez, la décision se réduit à une poignée d'arithmétiques
opérations – pas besoin d'une véritable construction gourmande.

---

- Oui. 3. Algorithme (Pseudo-code)

«» "
fonction possible(M):
l = lcm(diviseur1, diviseur2)
à la fois = M / l
Uniquement1 = M / diviseur1 - les deux
seulement2 = M/diviseur2 - les deux
Autre = M - (les deux +1 + seulement2)

# Nombres qui peuvent être utilisés par arr1:
1 = autre + seulement2
# Nombres qui peuvent être utilisés par arr2:
n°2 = autre + seulement1

si uniqueCnt1 > sec1 ou uniqueCnt2 > sec2:
retourner faux

# Après avoir donné arr1 et arr2 tous les candidats exclusifs,
Combien de "autres" nombres restent-ils ?
utiliséAutres = max(0, uniqueCnt1 - seulement2) + max(0, uniqueCnt2 - seulement1)
restant Autre = autre - utilisé Autres

retour restantAutres >= 0
«» "

Recherche binaire autour de `M`:

«» "
faible = 1
haute = 2 * (uniqueCnt1 + uniqueCnt2) * max(diviseur1, diviseur2) # limite supérieure sûre
alors que faible < élevé:
milieu = (faible + élevé) // 2
si possible (milieu):
haute = moyenne
Sinon:
faible = milieu + 1
retour faible
«» "

Tout l'arithmétique est fait avec 64 bits entiers (`long` en Java, `long` en C++,
`int`-type dans Python 3 parce qu'il encourage automatiquement).

---

- Oui. 4. Complexité

Étape Temps Mémoire
C'est pas vrai.
Recherche binaire ( < 50 itérations) Autres
"possible" "O(1)" Autres

Total: **'O(log range)' temps, `O(1)` mémoire** – assez rapide pour les limites.

---

- Oui. 5. Mise en œuvre

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.

---

#### 5.1 Java (Java 17)

"Java
importation java.io.*;
Importation de java.util.*;

solution de classe publique {
public int minimiseSet(int divisor1, int divisor2, int uniqueCnt1, int uniqueCnt2) {
long d1 = diviseur1, d2 = diviseur2;
long c1 = uniqueCnt1, c2 = unique Cnt2;

longue basse = 1;
longueur élevée = 2L * (c1 + c2) * Math.max(d1, d2); // limite supérieure sûre

pendant que (faible < haut) {
long milieu = faible + (élevé - faible) / 2;
si (possible(mid, d1, d2, c1, c2)) {
haute = moyenne;
} autre {
faible = milieu + 1;
}
}
retour (int) faible;
}

booléen privé possible(long m, long d1, long d2, long c1, long c2) {
longue l = lcm(d1, d2);

longue = m / l;
long1 = m / d1 - les deux;
longue seulement2 = m / d2 - les deux;
longue autre = m - (les deux + seulement1 + seulement2);

1 = autres + seulement2; // arr1 candidats
longue durée2 = autres + seulement1; // arr2 candidats

si (c1 > disc1 , c2 > disc2) retourner faux;

longue utilisationAutres = Math.max(0, c1 - seulement2) + Math.max(0, c2 - seulement1);
restant longtemps Autre = autre - utilisé Autres;

retourner le resteAutres >= 0;
}

privé long lcm(long a, long b) {
retourner a / gcd(a, b) * b; // a/gcd * b ne déborde jamais (64 bits)
}

privé long gcd(long a, long b) {
pendant que (b != 0) {
long t = a % b;
a = b;
b = t;
}
retour a;
}

// ----------------------------------------------
// Méthode principale pour lire les commentaires du juge en ligne.
// ----------------------------------------------
public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
StringTokenizer st = nouveau StringTokenizer(br.readLine());
int d1 = Integer.parseInt(st.nextToken());
int d2 = Integer.parseInt(st.nextToken());
int c1 = Integer.parseInt(st.nextToken());
int c2 = Integer.parseInt(st.nextToken());
Solution s = nouvelle solution();
Système.out.println(s.minimizeSet(d1, d2, c1, c2));
}
}
«» "

---

#### 5.2 Python 3 (3.10+)

'`python
importations
importer des maths

def minimiseSet(divisor1: int, divisor2: int,
uniqueCnt1: int, uniqueCnt2: int) -> Int:
d1, d2 = diviseur1, diviseur2
c1, c2 = uniqueCnt1, uniqueCnt2

faible, élevée = 1, 2 * (c1 + c2) * max(d1, d2)

alors que faible < élevé:
milieu = (faible + élevé) // 2
si possible(mid, d1, d2, c1, c2):
haute = moyenne
Sinon:
faible = milieu + 1
retour faible


def possible(m: int, d1: int, d2: int, c1: int, c2: int) -> C'est vrai.
l = lcm(d1, d2)
les deux = m // l
Uniquement1 = m // d1 - les deux
seulement2 = m // d2 - les deux
autres = m - (les deux + seulement1 + seulement2)

1 = autre + seulement2
n°2 = autre + seulement1
si c1 > disc1 ou c2 > disc2:
Retour Faux

_autre = max(0, c1 - seulement2) + max(0, c2 - seulement1)
retourner autre - used_other >= 0


def lcm(a: int, b: int) -> Int:
retourner a // maths.gcd(a, b) * b


♪ ----------------------------------------------------------------------------------
# Point d'entrée standard du juge en ligne
♪ ----------------------------------------------------------------------------------
si __nom__ == "__main__" :
données = list(map(int, sys.stdin.read().strip().split())
d1, d2, c1, c2 = données
print(minimizeSet(d1, d2, c1, c2))
«» "

---

### 5.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minimiseSet(int divisor1, int divisor2, int uniqueCnt1, int uniqueCnt2) {
long d1 = diviseur1, d2 = diviseur2;
long long c1 = uniqueCnt1, c2 = unique Cnt2;

longue longue basse = 1;
long long haut = 2LL * (c1 + c2) * max(d1, d2); // limite supérieure sûre

pendant que (faible < haut) {
long moyen = faible + (élevé - faible) / 2;
si (possible(mid, d1, d2, c1, c2)) {
haute = moyenne;
} autre {
faible = milieu + 1;
}
}
retourner static_cast<int>(faible);
}

particulier:
long (long long a, long b) {
retourner a / md::gcd(a, b) * b; // aucun dépassement: 64-bit
}

bool statique possible(long long m,
long long d1, long long d2,
long long c1, long long c2) {
long l = lcm(d1, d2);
longueur longue = m / l;
longueur longue seulement1 = m / d1 - les deux;
longueur longue seulement2 = m / d2 - les deux;
longue longue autre = m - (les deux + seulement1 + seulement2);

longue durée1 = autre + seulement2;
longue durée2 = autre + seulement1;
si (c1 > disc1 , c2 > disc2) retourner faux;

longue utilisation Autres = max(0LL, c1 - seulement2) + max(0LL, c2 - seulement1);
longue durée restant Autre = autre - utilisé Autres;
retourner le resteAutres >= 0;
}
};
«» "

---

- Oui. 6. Bon, mauvais, mauvais – quoi surveiller

Qu'est-ce que *pas* à faire
- C'est pas vrai.
**Bonne**) Utilisez l'arithmétique 64 bits partout – la réponse peut être ~1014. Se tenir à 32-bit `int` – vous obtiendrez de mauvaises réponses pour les grandes entrées. Autres
**Binary search the *upper lied* prudemment ("high = 2*(c1+c2)*max(d1,d2)"); vous ne frapperez jamais l'affaire "High = 2*(c1+c2)*max(d1,d2)". Autres Choisissez un `haut` trop petit (par exemple `c1+c2`) – la recherche binaire va boucler pour toujours ou retourner un résultat incorrect. Autres
**Bien**. Testez d'abord l'aide avec un petit script d'aide (`M=10,20,30` etc.). Supposons que la vérification «disponible seulement‐exclusive» soit suffisante – vous devez toujours comptabiliser le pool «autre» partagé. Autres
Oubliez que "cntOther" compte *ni l'un ni l'autre* diviseur. Pensez que `cntOther` compte -- alors vous pourrez remplir `arr1` mais pas `arr2`. Autres
**Ugly**= Une implémentation =Pick= qui construit en fait deux tableaux va rapidement exploser sur les contraintes `109` et est inutile. Implémenter une cupidité naïve ou une cupidité à deux points – cela va prendre du temps. Autres

---

- Oui. 7. Pourquoi ce problème se pose pour une entrevue de codage

1. **Afficher votre maîtrise de la recherche binaire sur la réponse** – un modèle d'entrevue récurrent.
2. **Teste votre capacité à faire un comptage prudent** au lieu de construire des solutions explicites.
3. ** Nécessite une bonne compréhension de la théorie des nombres** (`lcm`, `gcd`) dans un contexte de programmation.
4. ** Démontrer votre compétence avec l'arithmétique 64 bits** – la plupart des intervieweurs vous demanderont d'expliquer pourquoi 32 bits sont dangereux.
5. **Fait ressortir comment concevoir une limite supérieure sûre** pour la gamme de recherche binaire – un petit détail qui peut voyager beaucoup de candidats.

> *Si vous pouvez expliquer l'algorithme ci-dessus en moins de 5 minutes, vous impressionnerez presque chaque gestionnaire d'embauche. *

---

- Oui. 8. Principaux choix pour votre prochaine entrevue

Pourquoi ça compte ?
-- -- -- -- -- -- -- --
**Expliquez la vérification possible(M) de mots** (pas seulement le code). Montre une compréhension profonde, pas seulement la mémorisation. Autres
Autres **Afficher l'intuition liée supérieure** (pourquoi `2*(c1+c2)*max(d1,d2)` travaille). Évite une question d'entrevue à propos de Pourquoi la recherche binaire se termine-t-elle? Autres
**Discussion de la complexité temporelle** – échelle de log même pour `1014`. Démontre que vous pouvez raisonner sur l'asymptotique sous des contraintes serrées. Autres
**Pièges potentiels de concentration**: débordement, indexation 1-basée, manipulation des numéros `autres` correctement. Beaucoup de candidats abandonnent le pool de l'autre; vous aurez plein de points. Autres

---

- Oui. 9. Conclusion

*Le problème est trompeurment simple une fois que vous réalisez que c'est un problème de comptage caché derrière un choix de la plus petite question maximum. *
La recherche binaire sur le maximum couplée à un test de faisabilité `O(1)` donne une solution propre, rapide et mathématiquement rigoureuse qui échelle aux plus grandes entrées le problème permet.

Bon codage – et bonne chance pour l'entretien!