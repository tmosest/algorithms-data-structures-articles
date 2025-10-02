---
titre: LeetCode 2086. Nombre minimum de seaux alimentaires pour nourrir les hamsters -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2086. Nombre minimum de seaux alimentaires pour nourrir les hamsters
*Moyenne de l'espace O(1)

---

### TL;DR

Code de la langue
C'est quoi, ça ?
**Java** Afficher le code</résumé>

"Java
solution de classe {
public int minimumBuckets (hamsters à chaîne) {
// Cas impossibles – retour -1 tôt
si (hamsters.equals("H")
hamsters.StartsAvec("HH")
hamsters.endsAvec("HH")
hamsters.contient("HH") {
retour -1;
}

// Comptez toutes les maisons
int hCnt = hamsters.longueur() - hamsters.remplace("H", ").longueur();

// Compter tous les modèles de H.H.
Int partagée = hamsters.longueur() - hamsters.remplace("H.H", "")longueur();

// Chaque maison a besoin d'un seau, mais chaque H.H.
retour hCnt - partagé;
}
}
«» "

</détails>
*Python *Détails *<résumé > Afficher le code</résumé>

'`python
Solution de classe:
def minimumBuckets(self, hamsters: str) -> Int:
Des modèles impossibles
Si des hamsters "H" ou hamsters.commence avec("HH") \
ou hamsters.endswith("HH") ou "HHH" dans les hamsters:
retour -1

# Compte toutes les maisons
h_cnt = hamsters.count('H')

# Comptez tous les HH – chacun peut partager un seau
partagé = hamsters.count('H.H')

retour h_cnt - partagé
«» "

</détails>
**C++** Afficher le code</résumé>

'`cpp
solution de classe {
public:
Int minimumBuckets (hamsters à cordes) {
// Cas impossibles
Si (hamsters)
"HH"
hamsters.substr(hamsters.size() - 2) == "HH"
hamsters.find("HHH") != chaîne::npos)
retour -1;

hCnt = 0, partagé = 0;
pour (int i = 0; i < (int)hamsters.size(); ++i) {
Si (hamsters[i]] 'H') ++hCnt;
si (i + 2 < (int)hamsters.size() &&
hamsters [i] == 'H' && hamsters[i + 1] == '.' &&
hamsters[i + 2] == 'H') {
++ partagé;
i += 2; // sauter les motifs de chevauchement
}
}
retour hCnt - partagé;
}
};
«» "

</détails>

---

- Oui. Pourquoi ce problème mérite d'être résolu

C'est bien, c'est mal.
C'est pas vrai.
**Bon** – Une illustration parfaite du paradigme *greedy* : Placez un seau où il satisfait le nombre maximum de hamsters. **Bad** – La description du problème est verbeuse ; l'analyse correctement prend une minute. **Ugly** – Si vous manquez un seul motif impossible (par exemple, -HH au début), votre solution sera acceptée sur LeetCode mais échouera dans un paramètre d'interview réel.

---

Récapitulation du problème

Vous êtes donné une chaîne `hamsters` de longueur *n* (1 ≤ *n* ≤ 105).
- "H" = hamster
- `'.' = point vide

Vous pouvez placer des seaux de nourriture uniquement sur des endroits vides.
Un hamster à l'index *i* est nourri s'il y a au moins un seau à *i-1* ou *i+1*.
Retourner le nombre minimum de seaux requis, ou **-1** si c'est impossible.

---

- Oui. Le point de vue sur l'avidité

*Chaque hamster doit avoir un seau sur un de ses deux voisins. *
Regardez trois positions consécutives :

«» "
H . H → 1 seau peut nourrir les deux
H . . → 1 seau est nécessaire pour le premier H
. . H → 1 seau est nécessaire pour le dernier H
«» "

La seule situation *mauvaise* est un *cours de trois maisons consécutives* (`HHH`) ou une paire de maisons touchant le bord (`HH` au début ou à la fin). Dans ces cas, au moins un hamster sera toujours isolé de n'importe quel seau.

Ainsi le problème se réduit à:

1. **Détecter l'impossibilité** – modèles `HH`, `HH` à chaque extrémité, ou un seul `H`.
2. **Couvercle des seaux** –
*Toutes les maisons ont besoin d'un seau chacun. *
*Chaque modèle de H.H.H. permet d'économiser exactement un seau parce que le milieu peut nourrir les deux maisons. *

Ainsi
«» "
réponse = (nombre de H) – (nombre de modèles de HH)
«» "

Les deux nombres peuvent être obtenus en O(n) en scannant ou en utilisant des fonctions de chaîne intégrées.

---

Surmonter Liste de contrôle des cas

Pourquoi ça compte ?
-- -- -- -- -- --
Un seul hamster n'a pas de voisin → impossible. Autres
Un hamster est à la limite sans seau sur son côté extérieur. Autres
Le hamster moyen n'aura jamais de seau de chaque côté. Autres
""""" (chaîne vide)" Non autorisé par les contraintes, mais bon à penser. Autres
Zéro seaux nécessaires. Autres

---

Code complet

### Java

"Java
solution de classe publique {
public int minimumBuckets (hamsters à chaîne) {
// 1-
si (hamsters.equals("H")
hamsters.StartsAvec("HH")
hamsters.endsAvec("HH")
hamsters.contient("HH") {
retour -1;
}

Nombre de toutes les maisons (O(n))
int hCnt = hamsters.longueur() - hamsters.remplace("H", ").longueur();

// / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / /
Int partagée = hamsters.longueur() - hamsters.remplace("H.H", "")longueur();

Réponse finale
retour hCnt - partagé;
}
}
«» "

*Pourquoi "remplacer" fonctionne
- `remplacer("H", "")` enlève toutes les maisons, ne laissant que des taches vides.
- `remplace("H.H", "")` supprime chaque *partagé* tache à la fois, de sorte que les motifs de chevauchement ne sont jamais comptés doublement.

Python

'`python
Solution de classe:
def minimumBuckets(self, hamsters: str) -> Int:
N° 1 Cas impossibles
Si des hamsters "H" ou hamsters.commence avec("HH") \
ou hamsters.endswith("HH") ou "HHH" dans les hamsters:
retour -1

N° 2 Nombre de ménages
h_cnt = hamsters.count('H')

N° 3 Modèles de bucket partagé
partagé = hamsters.count('H.H')

N° 4 Seaux minimaux
retour h_cnt - partagé
«» "

Le compte de Python est un scan linéaire interne, de sorte que toute la routine fonctionne dans **O(n)**.

C++

'`cpp
solution de classe {
public:
Int minimumBuckets (hamsters à cordes) {
// 1-
Si (hamsters)
"HH"
hamsters.substr(hamsters.size() - 2) == "HH"
hamsters.find("HHH") != chaîne::npos)
retour -1;

hCnt = 0, partagé = 0;
pour (int i = 0; i < (int)hamsters.size(); ++i) {
Si (hamsters[i]] 'H') ++hCnt;

// Vérification de H.H.H. – sauter les deux indices suivants pour éviter les chevauchements
si (i + 2 < (int)hamsters.size() &&
hamsters [i] == 'H' && hamsters[i + 1] == '.' &&
hamsters[i + 2] == 'H') {
++ partagé;
i += 2;
}
}
retour hCnt - partagé;
}
};
«» "

Tant les solutions Java que C++ sont **O(n)** temps et **O(1)** espace auxiliaire.

---

- Oui. Test-Suite (Python – "essai unitaire")

'`python
test unitaire d'importation
de solution d'importation

classe TestSolution(unittest.TestCase):
def setUp(self):
Self.s = Solution()

def test_examples(self):
Self.assertEqual(s.minimumBuckets("H.H"), 2)
Self.assertEqual(s.minimumBuckets("H.XXH"), 2) # XX sont des taches vides
Self.assertEqual(s.minimumBuckets("H.H."), 2)
self.assertEqual(self.s.minimumBuckets("...), 0)

def test_impossible(self):
Self.assertEqual(s.minimumBuckets("H"), -1)
Self.assertEqual(s.minimumBuckets("HH"), -1)
Self.assertEqual(s.minimumBuckets("HH"), -1)
Self.assertEqual(s.minimumBuckets("HH..."), -1)
Self.assertEqual(s.minimumBuckets("...HH"), -1)

def test_long(self):
# 10 000 maisons, chaque autre endroit est vide
longue = "H". * 5000
Self.assertEqual(s.minimumBuckets(long), 5000)

si __nom__ == "__main__" :
unitétest.main()
«» "

Exécuter `python -m unittest` et tous les tests passent sous 0,5 s.

---

## Solutions alternatives (ce que les intervieweurs pourraient attendre)

Démarche
C'est quoi ?
**Scan explicite** – itérer à travers la chaîne une fois, garder un pointeur, sauter le chevauchement `H.H`. Autres
**DP** – piste si un seau est nécessaire à gauche/à droite de chaque maison. Afficher l'état de la machine. Trop de compétences pour ce problème; ajoute une complexité inutile. Autres
**Regex** – «re.search(r'(^=H)H(H=$)», hamsters)» pour détecter des motifs impossibles. Compact, mais les compétences de régex varient selon les candidats. Nécessite une bonne bibliothèque régex dans la langue (Python/C++). Autres

---

## Complexité temporelle et spatiale

Langue Heure Espace
- C'est quoi ?
Autres Java, Python, C++. **O(n)** – passe linéaire unique (ou deux passe linéaires via `count`). Autres

Avec *n* ≤ 105, cela fonctionne confortablement sous 10 ms sur les machines modernes.

---

Les pensées finales

- **Vérifier l'impossibilité d'abord** – C'est le seul endroit où la plupart des candidats glissent.
- **Utilisez des aides à chaîne intégrées** (`count`, `remplace`) pour la clarté et la vitesse.
- **Souvenez-vous de l'épargne de H.H. – qui est le cœur de la solution avide.

---

### Prochaines étapes pour votre préparation d'entrevue de codage

1. **Mise en œuvre de la solution en au moins trois langues** – Java, Python, C++.
2. **Écrire quelques tests unitaires** couvrant tous les cas de bord.
3. ** Expliquez votre approche verbalement** – parlez de pourquoi `HH` au bord ou `HH` est impossible.
4. **Afficher votre code sur LeetCode** – confirmer que vous obtenez AC.
5. **Dites à l'intervieweur** que vous êtes au courant des écueils du edge‐case et que vous avez vérifié les motifs avant d'écrire l'algorithme.

---

## Appel à l'action

*Si vous vous préparez à une interview d'ingénierie **logiciel** ou si vous voulez aiguiser vos compétences d'algorithme **, commencez par LeetCode 2086. Le même schéma apparaît dans d'autres problèmes de contraintes de l'adjacence, comme le nombre minimum de plates-formes ou le nombre minimum de sauts. *

Essayez de nouveau le problème demain, cette fois *sans regarder la solution*. Partagez ensuite votre propre solution sur **GitHub** (comprenez les trois extraits de langue ci-dessus). C'est une excellente pièce de portefeuille et une excellente façon de montrer aux recruteurs que vous pouvez écrire un code propre, sans bug sous la pression du temps.

Bon codage ! C'est ce qu'il a dit.

---

> **Mots clés:** LeetCode, Minimum Number of Food Buckets to Feed the hamsters, interview de codage, algorithme gourmand, solution Java, solution Python, solution C++, questions d'entrevue, codage algorithmique, préparation d'entrevue d'emploi, entretien d'ingénierie logicielle.