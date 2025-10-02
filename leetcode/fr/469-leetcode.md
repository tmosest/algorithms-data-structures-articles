---
titre: LeetCode 469. Convex Polygone - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 469 – Polygone convexe
**Problème** – Vérifiez si un simple polygone (donné par une liste de ses sommets dans l'ordre) est convexe.
**Objectif** – Retour `true` si chaque angle intérieur est < 180° (les bords colinéaires sont autorisés), sinon `faux`.

---

Aperçu de l'algorithme

Étape Action Pourquoi ça marche
- C'est quoi ?
Autres 1= Calculer le produit **cross** pour chaque triple consécutif de points \((p_i, p_{i+1}, p_{i+2})\) (indices wrap around). Autres Le signe du produit croisé nous indique si le passage de \(p_i\to p_{i+1}\) à \(p_{i+1}\to p_{i+2}\) est **left** (`>0`) ou **right** (`<0`). Autres
Autres 2= Conservez le premier signe non zéro comme étant l'orientation *référence*. Un polygone convexe doit tourner dans la même direction à chaque sommet. Autres
Autres Pour chaque autre produit non-zéro, comparez son signe à la référence. S'ils diffèrent → **pas convexe**. Tout changement de direction signifie un angle intérieur > 180°.
Autres Si tous les tours partagent le même signe (ou sont zéro), le polygone est convexe. Les tours zéro représentent les bords colinéaires – toujours convexes. Autres

**Complexité** – \(O(n)\) temps, \(O(1)\) espace supplémentaire.
**Précision** – Utiliser `long` pour le produit croisé afin d'éviter le débordement (max. \(== x,=> ≤ 10^4\) → produit ≤ \(=4×10^8\), toujours en 32-bit, mais `long` est sûr).

---

C'est vrai. Mise en œuvre du code

Voici les solutions prêtes à fonctionner dans **Java**, **Python** et **C++**.

---

#### 3.1 Java

"Java
Importer java.util. Liste;

solution de classe publique {
le booléen public est Convexe (liste <liste<entier>> points) {
int n = points.size();
si (n < 3) retourner faux; // pas un polygone, mais des contraintes garantissent n >= 3

signe int = 0; // 0 = inconnu, 1 = positif, -1 = négatif
pour (int i = 0; i < n; i++) {
Liste <entier> p0 = points.get(i);
Liste <entier> p1 = points.get(i + 1) % n);
Liste <entier> p2 = points.get(i + 2) % n);

longue croix = croix produit(p0, p1, p2);
si (croisement) 0) continuer; // colinéaire, ignorer
si (signat) 0) signe = croix > 0 ? 1 : -1;
sinon si ((croisement > 0 ? 1 : -1) != signe) {
retour false; // changement de direction
}
}
retour vrai;
}

produit privé à long terme(Liste<entier> a, Liste<entier> b, Liste<entier> c) {
longue x1 = b.get(0) - a.get(0);
long y1 = b.get(1) - a.get(1);
long x2 = c.get(0) - a.get(0);
long y2 = c.get(1) - a.get(1);
retour x1 * y2 - y1 * x2;
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
def isConvex(self, points: list[list[int]]) -> C'est vrai.
n = len(points)
signe = 0 # 0 = inconnu, 1 = positif, -1 = négatif

pour i dans la plage(n):
p0 = points[i]
p1 = points[i + 1) % n]
p2 = points[(i + 2) % n]

(p1[0] - p0[0]) * (p2[1] - p0[1]) - \
(p1[1] - p0[1]) * (p2[0] - p0[0])

en cas de croisement 0:
poursuivre
si signe == 0:
signal = 1 si croisé > 0 autre -1
elif (1 si croix > 0 autre -1) != signe:
Retour Faux

retour Vrai
«» "

---

#### 3.3 C++

'`cpp
solution de classe {
public:
Bool isConvex(vector<vector<int>&points) {
int n = points.size();
signe int = 0; // 0 = inconnu, 1 = positif, -1 = négatif

pour (int i = 0; i < n; ++i) {
Const auto& p0 = points[i];
Const auto& p1 = points[(i + 1) % n];
Const auto& p2 = points[(i + 2) % n];

long long croisement = 1LL * (p1[0] - p0[0]) * (p2[1] - p0[1]) - Oui.
1LL * (p1[1] - p0[1]) * (p2[0] - p0[0]);

si (croisement) 0) poursuivre; //
si (signat) 0) signe = (croisement > 0) ? 1 : -1;
sinon si ((croisement > 0 ? 1 : -1) != signe) retourner faux;
}
retour vrai;
}
};
«» "

---

C'est pas vrai. Billet de blog: Covex Polygon – Le bon, le mauvais, et le rugly

> **Mots clés:** LeetCode 469, Convex Polygon, algorithme, solution Java, solution Python, solution C++, entretien d'ingénierie logicielle, structures de données, entretien d'emploi, entretien de codage, conception d'algorithme, vérification de polygone convexe, recherche d'emploi, optimisation de reprise, référencement

---

4.1 Introduction

Lorsque vous vous préparez à une interview d'ingénierie **logiciel**, vous rencontrerez des problèmes qui testent à la fois la connaissance de la structure des données* et l'intuition algorithmique*. Un défi classique est **LeetCode 469 – Convex Polygon**. Bien que la déclaration semble simple — juste vérifier si un polygone est convexe — il y a des pièges subtils qui peuvent vous faire monter.

Dans ce billet, nous passerons par:

1. Le *bon* – pourquoi une approche basée sur les produits croisés est élégante et rapide.
2. Le *mauvais* – erreurs courantes (dépassement, manipulation colinéaire, orientation).
3. Le *ugly* – maux de tête et comment les dompter.

Et nous saupoudrerons dans certains pointeurs SEO-friendly pour aider votre CV se démarquer lorsque les recruteurs cherchent des solutions d'entretien de type LeetCode convexe polygone ou -algorithme. (en milliers de dollars)

---

4.2 Le bon – produit croisé, temps linéaire, espace O(1)

Un polygone convexe est un polygone où tout tourne d'un bord à l'autre, allant de la même façon (à gauche ou à droite). Le produit croisé 2-D vous donne exactement cette information:

«» "
cross((p2-p1), (p3-p2)) = (x2-x1)*(y3-y2) - (y2-y1)*(x3-x2)
«» "

*Si le signe est positif → virage à gauche; négatif → virage à droite; zéro → colinéaire. *

Parce que nous avons seulement besoin de comparer le signe de chaque produit croisé, l'algorithme fonctionne dans **O(n)** temps avec **O(1)** mémoire supplémentaire – un ajustement parfait pour les paramètres d'entrevue où l'efficacité compte.

**Pourquoi croiser le produit? * *
- Oui. C'est une opération *temps constant* pour chaque triple.
- Oui. Pas besoin de tri ou de bibliothèques géométriques complexes.
- Gérez confortablement toute portée de coordonnées lorsque nous utilisons des entiers 64 bits.

---

#### 4.3 Les mauvais – pièges communs

Trappe Ce qui ne va pas
Il n'y a pas de lien entre les deux.
**Débordement entier**= L'utilisation de l'int' 32 bits peut déborder si les coordonnées sont proches de ±104 (produit jusqu'à 4×108). Utiliser `long`/`long`. Autres
**Ignorer les bords de la colinéaire**=Certains retournent *faux* quand un produit croisé est zéro. Zéro est autorisé pour la convexité (arêtes colinéaires). Traitez-le comme "pas de changement". Autres
En supposant que le polygone soit donné dans le sens des aiguilles d'une montre. Ne comptez pas sur l'ordre d'entrée; calculez le premier signe non zéro comme référence. Autres
**Les erreurs hors-par-un**Les indices d'erreur peuvent sauter un vertex ou un double-compte. Utiliser le modulo arithmétique (`(i+1)%n`, `(i+2)%n`). Autres

---

4.4 Les horribles cas de bord qui persistent

1. ** Tous les points sont colinéaires**
- Un dégénéré "polygon" avec tous les points sur une ligne est techniquement convexe, mais certaines solutions peuvent mal retourner *false*.
*Solution*: Si chaque produit croisé est zéro, considérez la forme convexe (ou la poignée comme un cas spécial si votre spécification de travail dit le contraire).

2. **Dupliquer les sommets**
- LeetCode garantit des points uniques, mais dans les données du monde réel vous pourriez rencontrer des duplicatas.
- *Solution* : supprimer les duplicatas ou le drapeau comme invalide tôt.

3. ** Grandes valeurs de coordonnées* *
- Même avec "long", des coordonnées extrêmement grandes (au-delà de 32 bits) pourraient encore déborder dans un produit croisé.
- *Solution* : utiliser l'arithmétique de précision arbitraire (`BigInteger` en Java) si nécessaire, ou normaliser les coordonnées.

4. ** Polygones non simples**
- Le problème garantit un polygone simple, mais les données réelles peuvent contenir des auto-intersections.
- *Solution* : Effectuez d'abord un test d'intersection segmentée (O(n2) ou une ligne de balayage) avant de vérifier la convexité.

---

#### 4.5 Conseils d'entrevue & SEO Boost

1. **Afficher les maths** – Lorsque vous expliquez votre solution, passez par la dérivation de produits croisés. Les recruteurs adorent vous voir connecter la géométrie au code.
2. **Parler d'Edge** – Mentionnez les cas de bord que vous avez considérés (colinéaire, duplicata). Il démontre la rigueur.
3. **Complexité du temps des peines** – Les intervieweurs veulent vous voir discuter \(O(n)\) vs \(O(n \log n)\).
4. **Fournir plusieurs implémentations** – Avoir des solutions Java, Python et C++ montre une polyvalence.
5. **SEO-friendly CV heading** – LeetCode 469 Convex Polygon – Java, Python, solutions C++, conception algorithmique, prêt à l'interview. (en milliers de dollars)
6. **Ajouter des balises** – Lors de l'affichage sur des plateformes comme GitHub ou LeetCode, saisissez vos solutions avec `#convex-polygon #geométrie #algorithm #leetcodelove`.

---

4.6 Conclusion

Le problème **Convex Polygon** est une grande vitrine de *perspective géométrique* et de * simplicité algorithmique*. En tirant parti des produits croisés, vous pouvez fournir une solution prête à l'entrevue qui est à la fois rapide et claire.

Rappelez-vous :

- **Bien** – temps O(n), espace constant, produit croisé intuitif.
- **Bad** – Méfiez-vous du débordement, de la manipulation colinéaire, de l'orientation.
- **Ugly** – Poignez les cas dégénérés et les entrées non simples.

Maintenant, vous êtes prêt à accepter le défi LeetCode, impressionner les recruteurs, et marquer ce rôle d'ingénierie logicielle de rêve! C'est ce qu'il a dit.

---

** Ressources**
- [LeetCode 469 – Convex Polygon] (https://leetcode.com/problèmes/convex-polygon/)
- Solution Java : *produit croisé par j9hv* (LeetCode)
- Équivalents Python & C++ inclus ci-dessus.

Bon codage !