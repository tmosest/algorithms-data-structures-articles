---
titre: LeetCode 2029. Jeu de pierre IX -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Jeu de pierre IX – La solution «Math‐Only»
* (Java) Python ++ – O(n) temps, O(1) espace*

---

Récapitulation du problème (Code de débit 2029)

> **Stone Jeu IX**
> Il y a une rangée de pierres `n`, chacune ayant une valeur positive `pierres[i]`.
> Alice et Bob prennent à tour de rôle enlever **une** pierre.
> Si la somme ** de toutes les pierres enlevées** est divisible par 3, le joueur qui vient de retirer une pierre **perde**.
> Si la pile est vide après un mouvement, Bob gagne automatiquement.
> Les deux jouent de façon optimale. Alice gagne ?

Un échantillon de pierres Alice ? Autres
C'est quoi, ça ?
[2,1]
[2]
[5,1,2,4,3]

> **Constraints**
> `1 ≤ pierres longueur ≤ 105 "
> `1 ≤ pierres[i] ≤ 104 "

---

- Oui. L'Intuition – Bonne, mauvaise, mauvaise

Autres Phase Ce que vous devriez faire Ce que vous **devriez faire** Pourquoi
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bonne**Trouvez les pierres par la valeur restante « % 3 ». Une explosion exponentielle – impossible pour `n=105`. Autres
Utiliser la parité des pierres divisibles par 3 ('cnt[0] % 2'). Répondez au nombre absolu de « cnt[0] » (impair/même seulement). Un compte étrange peut faire basculer le résultat; compter trop est inutile. Autres
**Souvenez-vous qu'il n'y a pas de 1 ou 2 pierres de rechange → Bob gagne**. Cette petite affaire est la seule façon pour Alice de perdre sans bouger. Autres

La vraie sauce secrète est que **seulement la parité de `cnt[0]` et les nombres *relatifs* de "1" et "2" de pierres de rechange**.
Toutes les autres informations peuvent être rejetées dans l'espace O(1).

---

## La solution O(n) expliquée

Texte
cnt[0] = nombre de pierres avec la valeur % 3 == 0
cnt[1] = nombre de pierres avec la valeur % 3 == 1
cnt[2] = nombre de pierres ayant une valeur de % 3 == 2

Si cnt[1]==0 && cnt[2] ==0 -> Bob gagne (faux)

Laisser plus petite = min(cnt[1], cnt[2])
plus grande = max(cnt[1], cnt[2])

Si cnt[0] est égal: // parité même
Alice gagne iff plus petit > 0

Autrement (cnt[0] est impair): // parité impair
Alice gagne iff plus grand > plus petit + 2
«» "

Pourquoi ça marche ?

1. **Paires de 1 et 2**
Un `1` + `2` = `3` → supprimer les deux en même temps perdrait instantanément.
Alice va donc essayer de ** forcer Bob** à prendre une paire qui lui laisse un résidu gagnant.

2. **Trois du même reste (1 ou 2*) *
«1+1+1 = 3» (ou «2+2+2 = 6»).
Enlever n'importe lequel laisse une pierre de ce reste qui peut être pris sans causer de perte.

3. **Parité des pierres de 0-récidive* *
Chaque fois qu'une pierre de type `0` est enlevée, la somme change de `0` modulo 3.
Ainsi, la *parité* (impair/même) de ces pierres détermine si l'état global de la divisibilité-par-trois retourne après le premier déplacement d'Alice.

4. **Lorsque la parité est égale**
Alice peut miroiter les mouvements de Bob sur les pierres de "0".
Elle gagne si au moins une pierre non ' 0 ' existe (`plus petite > 0').
Si toutes les pierres sont « 0 », Bob gagnera parce que la somme finale ne peut jamais être divisible par 3.

5. **Quand la parité est étrange**
Alice peut forcer une victoire si le **gap** entre les nombres de `1` et `2` pierres est **≥ 3** (`plus grand > plus petit + 2`).
Sinon Bob peut refléter Alice et gagner.

---

Mise en œuvre

### Java

"Java
Importation de java.util.*;

solution de classe {
pierre de booléen publiqueGameIX(int[] pierres) {
int[] cnt = nouvelle int[3];
pour (int s : pierres) cnt[s % 3]++;

Si (cnt[1] == 0 && cnt[2] == 0) retourner faux;

int plus petit = Math.min(cnt[1], cnt[2]);
int plus grand = Math.max(cnt[1], cnt[2]);

si (cnt[0] % 2] 0) { // même nombre de pierres de 0-récipient
retour plus petit != 0;
} autres { // nombre impair de pierres de marque 0
retour plus grand > plus petit + 2;
}
}
}
«» "

---

Python

'`python
Solution de classe:
def pierre GameIX(self, pierres: List[int]) -> bool:
cnt = [0, 0, 0]
pour les pierres:
cnt[s % 3] += 1

si cnt[1] == 0 et cnt[2] == 0:
Retour Faux

plus petite = min(cnt[1], cnt[2])
plus grande = max(cnt[1], cnt[2])

si cnt[0] % 2 == 0: # même les pierres de 0-remainder
retour plus petit != 0
Autre: # impair 0-remainder pierres
retour plus grand > plus petit + 2
«» "

---

C++

'`cpp
solution de classe {
public:
pierre de boolGameIX(vecteur<int>& pierres) {
int cnt[3] = {0, 0, 0};
pour (int s : pierres) cnt[s % 3]++;

Si (cnt[1] == 0 && cnt[2] == 0) retourner faux;

int plus petit = min(cnt[1], cnt[2]);
int plus grand = max(cnt[1], cnt[2]);

si (cnt[0] % 2] 0) { // même nombre de pierres de 0-récipient
retour plus petit != 0;
} autres { // nombre impair de pierres de marque 0
retour plus grand > plus petit + 2;
}
}
};
«» "

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
Java / Python / C++. **O(n)** (passe unique au compte)

`n` est jusqu'à 100 000, donc cette solution linéaire répond facilement aux contraintes.

---

## Article de blog – Comment faire pour clouer la pierre jeu IX dans votre mémoire

Titre
**************************************************************************************************************************************************************************************************************************************************************** *

Description de la méta
Apprenez la solution O(n) élégante à LeetCode 2029 – Pierre Jeu IX. Obtenez des implémentations Java, Python et C++, une explication claire et du contenu optimisé SEO qui stimule votre marque personnelle pour les rôles d'ingénierie logicielle.

---

- Oui. 1. Crochet – Pourquoi Ce qui compte

- **Les problèmes de LeetCode sont d'entretien.
- Le jeu de pierre IX présente *le raisonnement mathématique* + *la netteté algorithmique*.
- La rédaction d'un article concis avec un code démontre **les connaissances du domaine** et **les compétences en communication**— exactement ce que les gestionnaires d'embauche recherchent.

---

- Oui. 2. Déclaration de problème en anglais clair

[Récapitulez le problème]

---

- Oui. 3. La feuille de route "Bonne, mauvaise, mauvaise"

[Insérer le tableau d'avant]

---

- Oui. 4. Démarche de la stratégie optimale

Expliquez avec un exemple en 5 étapes :
1. Compter les résidus.
2. Poignez l'étui d'angle de l'angle de 1 1/2.
3. Compte de partage.
4. Vérifiez la parité des pierres de 0-remainder.
5. Décidez gagnant/perte.

Ajouter un diagramme ou une table de 2 colonnes pour plus de clarté.

---

- Oui. 5. Extraits de code

- Bloc Java
- Bloc Python
- Bloc C++

Ajouter **syntax surlignage** et ** courtes lignes de commentaires** pour la lisibilité.

---

- Oui. 6. Pourquoi c'est "Job-Ready"

- ** Temps linéaire, espace constant** → répond aux contraintes de production.
- **Aucune bibliothèque supplémentaire** → portable dans tous les environnements d'entrevue.
- **Clear, maintenable commentaires** → montre que vous pouvez écrire propre, code de niveau de production.
- **Analyse des problèmes** → démontre *la pensée algorithmique* – la marque d'un ingénieur logiciel senior.

---

- Oui. 7. Liste de contrôle pour le démarrage rapide

Objet
- Oui.
Ajouter le lien **LeetCode** et **tags** (`#programmation dynamique`, `#math`) Autres
Inclure un tableau **complexité temporelle**
Fournir des exemples de cas de test** (tableau ci-dessus)
Ajouter un appel à l'action**: Veuillez me laisser un message sur LinkedIn – laissez-nous discuter de la façon dont je peux apporter ce niveau d'optimisation à votre équipe. Autres

---

- Oui. 7. Pensée finale – -Math est puissant

[Le court paragraphe encourage les lecteurs à pratiquer des tours de compte par rappel sur d'autres jeux combinatoires.]

---

- Oui. 8. Clôture et appel à l ' action

- Inviter les participants à faire des commentaires et à discuter.
- Mentionnez votre URL personnelle LinkedIn/GitHub.
- Offre d'examiner d'autres solutions.

---

Liste de contrôle du référencement

Mise en œuvre
-- -- -- -- -- --
**Mot-clé principal** ─Stone Game IX solution (utilisé 3–5× dans le corps)
Mots-clés secondaires
**Structure de la tête**
**Alt text** pour les diagrammes
Lien vers vos autres messages LeetCode
**Liens sortants** Autres
Ajouter des images à sitemap.xml pour l'indexation de Google
Utiliser JSON‐LD pour l'exemple de code

---

- Oui. 9. A emporter

> *Vous venez de résoudre un jeu de 100 à 000 pierres en 50 lignes de code et avez écrit un blog qui montre que vous pouvez transformer cette solution en un atout professionnel. Bonne chance pour votre prochain entretien ! *

---

Conclusion

Stone Game IX peut ressembler à un jeu de hasard, mais le vrai tour est **parité + nombres relatifs**.
Le code Java/Python/C++ fourni est la solution O(n) la plus courte possible que vous pouvez taper dans une interview de codage.

---

> **Vous voulez plus de maîtrise de LeetCode? * *
> Abonnez-vous à mon bulletin d'information et recevez des articles hebdomadaires, des solutions annotées et des vidéos de préparation d'entrevue directement dans votre boîte de réception.
> [S'abonner maintenant](https://votrenewsletter.com)

---