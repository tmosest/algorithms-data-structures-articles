---
titre: LeetCode 3571. Trouvez la plus courte Superstring II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3571 – Trouvez la plus courte superchaîne II
### Code Leet

> **Objectif** – Avec deux chaînes *s1* et *s2*, retourner la chaîne la plus courte qui contient les deux sous-chaînes contiguës.
> Si plusieurs superchaînes existent, une seule est acceptable.

---

Extraits de code rapide

Langue Solution Complexité
C'est pas vrai.
**O(n2)** temps, **O(1)** espace supplémentaire
**Python**
**C++**

> *Les trois implémentations suivent la même logique : 1) maîtrise de la poignée, 2) trouver le chevauchement maximum, 3) fusionner. *

---

Problème

1. **Contenu** – Si une chaîne est déjà une sous-chaîne de l'autre, la réponse est la chaîne plus longue.
2. **Overlap** – Trouvez le suffixe le plus long d'un qui correspond à un préfixe de l'autre *et vice versa*.
3. **Merge** – Ajouter la partie non recouverte de l'autre chaîne à la première.

Comme les chaînes d'entrée sont au plus 100 caractères, une simple double boucle pour tester tous les chevauchements (`O(n2)`) est plus que rapide.

---

Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Complexité du temps** Pour n plus grand, vous auriez besoin d'un algorithme de style suffixe ou KMP. Autres
Autres **Complexité de l'espace**= Espace supplémentaire constant.= Aucune.= La concaténation de la chaîne naïve dans de nombreuses langues peut causer des copies cachées. Autres
**Readability** L'utilisation de `String.contient()` sur de grandes chaînes peut être coûteuse en Java (O(n2) par appel). Autres
**Cas d'Edge** Des erreurs hors-par-un dans les indices de sous-chaîne. Autres
**Extensibilité**= Facile à adapter pour >2 chaînes.= Besoin de modifier la boucle. Pour les chaînes 3‐4 vous pourriez générer par inadvertance une solution de force brute O(2n). Autres

---

Répartition du code

### Java – Force brute simple (O(n2))

"Java
// 3571. Trouvez la plus courte Superstring II
solution de classe {
public Superchaîne(String s1, String) s2) {
int m = s1.longueur(), n = s2.longueur();

// 1. Si l'un contient l'autre, retourner plus
si (s1.contient(s2)) retour s1;
si (s2.contient(s1)) retour s2;

à l'intérieur maxOverlap = 0;
Chaîne best = s1 + s2; // repli si aucun chevauchement

// 2. Vérifier tous les chevauchements possibles
pour (int i = 1; i <= Math.min(m, n); i++) {
// s1 suffixe == préfixe s2
si (s1.substring(m - i).equals(s2.substring(0, i)) {
si (i > maxOverlap) {
maxOverlap = i;
best = s1 + s2.substring(i);
}
}
// s2 suffixe == s1 préfixe
si (s2.substring(n - i).equals(s1.substring(0, i)) {
si (i > maxOverlap) {
maxOverlap = i;
best = s2 + s1.substring(i);
}
}
}
le meilleur retour;
}
}
«» "

**Pourquoi ça marche* *
* `s1.contient(s2)` / `s2.contient(s1)` poignées de confinement.
* La double boucle `pour` tente chaque longueur de chevauchement possible (`1 ... min(m,n)`).
* Le premier match qui donne le plus grand chevauchement produit la superchaîne minimale.
* Parce que nous ne stockons que la meilleure corde jusqu'ici, aucun espace supplémentaire n'est utilisé.

---

### Python – Mise en œuvre directe

'`python
# 3571. Trouvez la plus courte Superstring II
Solution de classe:
def le plus court Superchaîne (self, s1: str, s2: str) -> str:
1. Containment
si s1 dans s2:
retour s2
si s2 dans s1:
retour s1

m, n = len(s1), len(s2)
best = s1 + s2
max_overlap = 0

2. Recherche de chevauchement
pour i dans la plage (1, min(m, n) + 1):
# s1 suffixe == préfixe s2
Si s1[-i:]== s2[:i]:
i > _surface maximale :
max_overlap = i
best = s1 + s2[i:]
# s2 suffixe == s1 préfixe
si s2[-i:] == s1[:i]:
i > _surface maximale :
max_overlap = i
best = s2 + s1[i:]

le meilleur retour
«» "

*Notes de python:*
* String slice `s1[-i:]` est O(i), mais pour n=100 il est trivial.
* La logique reflète la version Java, en gardant le code concis.

---

### C++ – Rapide et chaleureux

'`cpp
// 3571. Trouvez la plus courte Superstring II
solution de classe {
public:
chaîne la plus courte Superchaîne(chaîne s1, chaîne s2) {
// 1. Le confinement
si (s1.find(s2) != string::npos) retourne s1;
si (s2.find(s1) != string::npos) retourne s2;

int m = s1.size(), n = s2.size();
string best = s1 + s2; // repli
int max_overlap = 0;

// 2. Recherche de chevauchement
pour (int i = 1; i <= min(m, n); ++i) {
// s1 suffixe == préfixe s2
si (s1.comparer(m - i, i, s2, 0, i)) 0) {
si (i > max_overlap) {
max_overlap = i;
best = s1 + s2.substr(i);
}
}
// s2 suffixe == s1 préfixe
si (s2.comparer(n - i, i, s1, 0, i)) 0) {
si (i > max_overlap) {
max_overlap = i;
best = s2 + s1.substr(i);
}
}
}
le meilleur retour;
}
};
«» "

**Conseils C++**
* `string::compare` est O(i) mais efficace.
* `substr` crée une copie seulement lorsque nécessaire, en maintenant faible utilisation de la mémoire.

---

Les leçons à suivre

La leçon Comment ça aide
C'est pas vrai.
**Vérifier d'abord le confinement** Autres
**Toujours tester les deux directions de chevauchement**.Les cordes peuvent se chevaucher de deux façons; l'absence d'une seule donne une réponse sous-optimale. Autres
Autres **Gardez un candidat « best »**= Un seul laissez-passer suffit; pas besoin de construire toutes les possibilités. Autres
Pour les cordes de 100 caractères, la force brute est parfaitement acceptable; pour les ensembles de données plus importants, il faudrait une approche suffixe ou KMP. Autres
**L'unité-test en profondeur**Les cas de bordure : chaînes identiques, l'une à l'intérieur de l'autre, aucun chevauchement, chevauchement complet. Autres

---

## ♫ SEO-Optimized Blog Post (Job-Interview Focus)

Titre
*Cracking LeetCode 3571: Superstring II le plus court – Java, Python, C++ Solutions + Conseils d'entrevue**

Description de la méta
> Apprenez à résoudre le LeetCode 3571 -Découvrez la plus courte superchaîne II en Java, Python et C++. Ce post explique l'algorithme, la complexité et les meilleures pratiques de codage pour impressionner les recruteurs.

Mots clés
- LeetCode 3571
- Superstring le plus court
- Manipulation à cordes
- Problème d'entrevue Java
- Défi de codage Python
- C++ Algorithme
- Conseils d'entretien d'emploi
- Complexité de l'algorithme
- Couverture à deux rangs
- Codage de la préparation de l'entrevue

Aperçu

1. **Aperçu du problème** – Énoncé rapide, contraintes, exemples.
2. **Pourquoi ça compte** – Pertinence d'interviewer des questions sur la manipulation de chaînes et la conception d'algorithmes.
3. **Solution Strategy** – Containment → Overlap → Fusionner.
4. **Code détaillé Walk‐through** – Java, Python, C++.
5. ** Analyse de complexité** – temps « O(n2) », espace « O(1) ».
6. **Cas et pièges d'Edge** – Contrôles de chevauchement hors-par-le-champ.
7. **Au-delà de deux cordes** – Conseil à la programmation dynamique pour les chaînes *k*.
8. **Conseils d'entrevue** – Comment formuler l'approche, les compromis et discuter des optimisations.
9. **Conclusion** – Résumer et encourager la pratique de problèmes similaires.

### Crochet et appel à l'action
♪Got coincé sur les problèmes de cordes? Maîtrisez la technique de superchaîne la plus courte et observez les recruteurs remarquer votre code clair et efficace. Essayez les solutions ci-dessous et ajoutez-les à votre portfolio!

---

Les pensées finales

- **La simplicité gagne** – Une solution propre, O(n2) pour ce problème n'est pas seulement acceptable; c'est idéal pour un réglage d'entrevue.
- **Consistance entre les langues** – Démontrer la même logique en Java, Python et C++ montre une compréhension et une polyvalence profondes.
- **Soyez prêt à discuter des compromis** – Si l'intervieweur pousse pour un algorithme plus rapide, soyez prêt à mentionner des tableaux suffixes ou KMP pour des entrées plus importantes.

Utilisez cet article comme un point de contrôle d'apprentissage, ajoutez les extraits de code à votre GitHub, et pratiquez expliquer chaque étape à haute voix. Bonne chance pour cet entretien !