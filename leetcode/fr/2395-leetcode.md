---
titre: LeetCode 2395. Trouver des sous-tribus avec une somme égale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code Leet 2395 – Trouver des sous-barrages avec une somme égale
**Un parcours convivial pour les débutants (Java, Python & C++ + SEO-optimized blog)* *

---

Table des matières

1. [Énoncé du problème] (#Énoncé du problème)
2. [Jurisprudences d'intuition et de bord] (#Cours d'intuition et de bord)
3. [Algorithme] (#algorithme)
4. [Analyse de la complexité] (#analyse de la complexité)
5. [Mise en œuvre](#Mise en œuvre)
* Java
* Python
* C++
6. [Bonne, mauvaise et mauvaise] (#Bonne et mauvaise)
7. [Pourquoi cette solution rock pour les interviews] (#Why-this-solution-rocks)
8. [Mots-clés et étiquettes](#seo-keywords-&-tags)

---

## Énoncé du problème <un nom="état du problème"></a>

> **2395. Trouver des sous-barrages avec une somme égale**
> Compte tenu d'un nombre entier indexé à 0, déterminer s'il existe deux sous-barrages de **longueur 2** avec une somme égale.
> Les deux sous-tribus doivent commencer à des indices différents.
> Return `true` si de tels subarrays existent, sinon retourner `faux`.

**Contrôles* *

- "2 ≤ longueur nominale ≤ 1000"
- `-10^9 ≤ nums[i] ≤ 10^9`

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
"[4, 2, 4]" "vrai" "[4,2]" et "[2,4]" les deux montants à 6
Aucune paire adjacente ne partage une somme
Deux paires de `[0,0]` (indices 0‐1 & 1‐2)

---

## Intuition & Edge Cases <un nom</a>

Nous n'avons qu'à examiner les paires *adjacents* parce qu'un subarray de longueur 2 n'est que deux nombres consécutifs.
Si une somme apparaît deux fois, les deux sous-barrages sont garantis pour commencer à des indices différents (parce que nous traversons de gauche à droite).

**Juge**

- Arrays avec **exactement 2** éléments → une seule paire → réponse est toujours `false`.
- Nombres négatifs → aucune manipulation particulière nécessaire; les sommes peuvent également être négatives.
- Grandes valeurs → utiliser 64-bit (`long`) pour éviter le débordement en Java et C++.

---

## Algorithme <un nom="algorithme"></a>

1. ** Sortie précoce** – si `nums.longueur < 3`, retourner `faux`.
2. Créez un hachage vide (ou une carte de hachage) pour suivre les sommes que nous avons vues.
3. Itérer `i` de `0` à `nums.longueur - 2`:
- Calculer `s = nombres[i] + nombres[i+1]`.
- Si `s` est déjà dans le jeu → retourner `true`.
- Sinon insérer `s` dans l'ensemble.
4. Après boucle, retourner `faux`.

Il s'agit essentiellement du premier élément répété sur une fenêtre coulissante de taille 2.

---

## Analyse de complexité <un nom="analyse de complexité"></a>

Métrique Temps Espace
- Oui.
Autres Algorithme entier **O(n)**

`n` est la longueur des `nums`. Le hash‐set donne un temps d'insertion/de recherche constant moyen.

---

## Mise en oeuvre <un nom></a>

Voici des implémentations idiomatiques propres dans **Java**, **Python** et **C++**.

### Java

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe {
public booléen trouverSubarrays(int[] nums) {
si (nums.longueur < 3) retourner faux; // une seule paire existe

Set<Long> vu = nouveau HashSet<>(); // utiliser longtemps pour éviter le débordement
pour (int i = 0; i < nombres.longueur - 1; i++) {
somme longue = (long) nombres[i] + (long) nombres[i + 1];
si (!seen.add(sum)) retourne true; // ajouter retourne false si déjà présent
}
retourner faux;
}
}
«» "

Python

'`python
Solution de classe:
def findSubarrays(self, nombres: list[int]) -> bool:
si len(nums) < 3:
Retour Faux

vu = set()
pour i dans la plage (len(nums) - 1):
s = nombres[i] + nombres[i + 1]
si s en vue:
retour Vrai
voir.add(s)
Retour Faux
«» "

C++

'`cpp
#incluez <vecteur>
#inclut <unordered_set>

solution de classe {
public:
Bool findSubarrays(const std::vector<int>& nums) {
si (nums.size() < 3) retourner faux;

std::unordered_set<long> vu; // sommes de 64 bits
pour (size_t i = 0; i + 1 < nums.size(); ++i) {
longue somme longue = statique_cast<long long>(nums[i]) +
statique_cast<long long>(nums[i + 1]);
si (!seen.insert(sum).second) retourne vrai;
}
retourner faux;
}
};
«» "

Les trois solutions fonctionnent dans le temps linéaire et utilisent un jeu de hachage pour l'espace auxiliaire O(n).

---

## Bon, mauvais et humble <un nom</a>

Qu'est-ce qui est bien Ce qui pourrait être mieux
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Clarté**=Loop + set – facile à lire. Aucun. Autres
**Performance** Pourrait réduire l'espace à O(1) si nous avons seulement besoin de détecter *toute* duplicata, mais nous avons déjà linéaire-temps & espace – optimal pour ce problème. L'utilisation de boucles imbriquées (force brute) conduit à O(n2) – inacceptable pour n=1000. Autres
**Sécurité de l'écurie**=Poigne les nombres négatifs, les grandes valeurs avec des sommes de 64 bits.== Aucune.= Oublier de lancer `long` en Java ou `long` en C++ peut déborder. Autres
**Maintenabilité**= Petite méthode autonome.= Aucune.= Mélange de types de données (`int` vs `long`) dans la même expression (buggy). Autres
**Le style de l'interview**=Show hash-set connaissances & fenêtre coulissante. Aucune explication n'est possible. Autres

---

- Oui. Pourquoi cette solution rock pour des interviews <a name="Why-this-solution-rocks"></a>

1. **Sécurité du temps** – LeetCode=1 ms, 100 %=1 est obtenu par un seul laissez-passer, qui est la norme d'or pour les problèmes d'entrevue.
2. **Space‐efficiency** – O(n) set est le plus nécessaire; nous n'avons pas besoin d'une carte à moins de vouloir des indices.
3. **Narration claire de l'entrevue** – Nous faisons glisser une fenêtre de taille 2, calculons les sommes, et cherchons des duplicatas à l'aide d'un jeu de hachage. (en milliers de dollars)
4. **Couverture de cas** – Nombres négatifs, duplicata, taille minimale du tableau – tous traités en un seul balayage.
5. **Portabilité en langue brute** – La même logique fonctionne en Java, Python, C++ – un bon point de conversation si vous êtes interviewer pour un rôle nécessitant plusieurs langues.

---

## SEO Mots-clés et mots-clés <un nom="seo-keywords-&-tags"></a>

- **LeetCode 2395**
- Trouver des sous-tribus avec une somme égale
- Solution Java
- Solution Python
- Solution C++
- Entretien de la carte de hachage
- fenêtre coulissante
- Codage de la préparation de l'entrevue
- entretien avec un ingénieur logiciel
- analyse par algorithme
- complexité du temps
- complexité spatiale
- problèmes LeetCode pour débutants

---

La pensée finale

En maîtrisant ce sum de paire adjacente, vous serez prêt à affronter une large gamme de questions de sum duplicate ou de subarray sur le plancher de l'entretien d'emploi. Continuez à pratiquer des modèles semblables (deux-pointeurs, fenêtre coulissante, hachage) et vous allez construire une trousse robuste qui brille dans toute entrevue technique. Bon codage ! C'est ce qu'il a dit