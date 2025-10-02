---
titre: LeetCode 3340. Vérifier la chaîne équilibrée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3340 – Chaîne de vérification équilibrée
> **Bon, mauvais et lugubre** – Un guide pratique sur les ongles Cette question d'entrevue (et poser votre travail de rêve)

---

TL; RD

- **Problème**: Pour une chaîne "num`, vérifiez si la somme des chiffres à des indices égaux à la somme des chiffres à des indices impairs.
- **Solution**: Un scan linéaire, en conservant deux totaux.
- **Heure**: "O(n)"
- **Espace**: "O(1)"
- **Langues**: Java, Python, C++
- **Pourquoi ça compte**: Simple mais parfait pour démontrer la pensée O(n), le code propre et les fondamentaux de l'entrevue.

---

- Oui. 1. Énoncé de problème (Code de bord)

> **Vérifier la chaîne équilibrée**
> * Difficulté: * Facile
> **Définition**
> Une chaîne de chiffres est *équilibrée* si la somme des chiffres à indice pair est égale à la somme des chiffres à indice impair.
> Retour `true` si `num` est équilibré, sinon `faux`.
> **Constraints**
> - `2 <= longueur num. <= 100`
> - `num` se compose seulement de chiffres.

*Exemples*

Entrée Sortie Explication
C'est pas vrai.
""1234""""false"" Même somme = 1+3=4, somme marginale = 2+4=6"
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

---

- Oui. 2. Le bien – Pourquoi Ce problème est idéal pour les entrevues

Pourquoi ça aide votre carrière
- C'est pas vrai.
**Clear, déterministe**= Pas de cas ambigus – parfait pour les écrans de première ronde. Autres
**L'algorithme d'un seul passage** Autres
**Complexité de l'affaire des bords miniatures**= Concentre votre attention sur la clarté algorithmique, et non sur le codage défensif. Autres
**Language-agnostique**= Vous pouvez le résoudre en Java, Python ou C++ – choisissez la langue la plus confortable pour vous. Autres
Autres **Possibilité d'une solution d'espace O(1) propre** Autres

---

- Oui. 3. Les pièges communs

Piège
- Oui.
**Utiliser `int` débordement sur de grandes cordes**.Pas un problème ici en raison de la longueur max 100, mais toujours être attentif aux limites entiers. Autres
**Les indices de création sont basés sur 1**. Autres
**Confuser des indices mêmes avec des chiffres mêmes**= Même des indices signifie la position (0, 2, 4, ...), pas la parité des chiffres. Autres
**Utiliser des structures de données lourdes** Autres
**Ignorer l'espace blanc/invalidité de l'entrée**=LeetCode garantit des chaînes de caractères numériques seulement; le code de production doit encore valider. Autres

---

- Oui. 4. L'Ugly – Variations et extensions avancées

Variation de la solution
- C'est quoi ?
Autres **Grande chaîne de caractères (106+)**. Toujours O(n) avec un espace constant, mais regardez pour `long` vs `int` si la somme peut dépasser `Integer. MAX_VALUE'. Autres
**Streaming input**=Trouver les caractères à leur arrivée; maintenir deux sommes sans stocker la chaîne entière. Autres
**Requêtes multiples**=Si vous êtes demandé pour de nombreuses chaînes, précalculez les montants de préfixe pour répondre à chaque requête dans O(1). Autres
**Généralisation à des positions arbitraires** Autres

---

- Oui. 5. Marche de l'algorithme

1. **Initialiser deux compteurs**: `evenSum = 0`, `odd Somme = 0 %.
2. **Itérer sur la chaîne** caractère par caractère.
3. **Convertissez chaque caractère** à sa valeur numérique (`ch - '0'` dans C++/Java, `int(ch)` dans Python).
4. **Ajouter** à `evenSum` si l'indice est uniforme, sinon à `oddSum`.
5. Après la boucle, **return** `evenSum == impairSum`.

Aucune structure de données auxiliaire n'est nécessaire — une seule boucle et deux variables entières.

---

- Oui. 6. Solutions de code

Autres Les trois solutions fonctionnent dans **O(n)** temps et **O(1)** espace.

#### 6.1 Java

"Java
solution de classe {
booléen public estBalanced(String num) {
Int evenSum = 0, impair Somme = 0;
pour (int i = 0; i < longueur num(); i++) {
num.charAt(i) - '0';
Si (i et 1)] 0) mêmeSum += chiffre;
Autre étrange Montant += chiffre;
}
rendre evenSum == impairSum;
}
}
«» "

6.2 Python

'`python
Solution de classe:
def isBalanced(self, num: str) -> C'est vrai.
even_sum, impair_sum = 0, 0
pour idx, ch dans l'énumération(num):
chiffre = int(ch)
si idx % 2 == 0 & #160;:
even_sum += chiffre
Sinon:
impair_sum += chiffre
retourner even_sum == impair_sum
«» "

*### 6.3 C++

'`cpp
solution de classe {
public:
bool isBalanced(string num) {
Int evenSum = 0, impair Somme = 0;
pour (int i = 0; i < num.size(); ++i) {
le chiffre int = num[i] - '0';
Si (i % 2 == 0) mêmeSum += chiffre;
Autre étrange Montant += chiffre;
}
rendre evenSum == impairSum;
}
};
«» "

---

- Oui. 7. Autre approche – utiliser `map` / `reduce` (Python seulement)

'`python
def is_balanced(num: str) -> C'est vrai.
même = somme(int(num[i]) pour i dans l'intervalle(0, len(num), 2))
impair = somme(int(num[i]) pour i dans la fourchette(1, len(num), 2))
retour même == étrange
«» "

*Pro*: Très concis.
*Cons*: Frais généraux constants légèrement plus élevés; pas idéal pour les entrevues critiques.

---

- Oui. 8. Conseils d'entrevue

Pourquoi ça aide ?
C'est quoi ?
**Déclarez votre approche**="Je vais utiliser un seul passage O(n) scan" – montre une pensée algorithmique claire. Autres
Autres **Parler du temps et de l'espace** Autres
**Demander des éclaircissements** Autres
**Boîtes de bord de Mention**= Bien que minimal ici, vous pouvez discuter de ce qui se passe si la longueur de la chaîne est impair/même. Autres
**Essai d'analyse**= Exécutez votre code sur les exemples fournis, et aussi sur les cas bord comme `"00"` et `"9999"`. Autres
**Afficher le code propre**= Préférez la lisibilité par rapport aux micro-optimisations dans les entrevues. Autres

---

- Oui. 9. Conclusion optimale en matière de référencement

> Vous cherchez à décrocher un rôle de promoteur d'avant-garde, d'arrière-garde ou d'arrière-garde? Maîtrise **LeetCode 3340 – Check Balanced String** prouve que vous pouvez penser à *O(n*), écrire du code Java/Python/C++ propre, et éviter les pièges d'interview communs. Partagez cette solution sur votre GitHub, votre blog ou votre portfolio et les recruteurs observent votre netteté algorithmique.

**Mots-clés**: LeetCode, Check Balanced String, Balanced String, Java interview, Python interview, C++ interview, codage interview prep, algorithme, O(n), O(1), entretien d'emploi, ingénieur logiciel, recruteur technique.

---

**Codage heureux, et bonne chance pour votre prochaine interview! * *