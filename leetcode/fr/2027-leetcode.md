---
titre: LeetCode 2027. Déplacements minimum pour convertir les chaînes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# Déplacement minimum pour convertir la chaîne – Guide d'entrevue complet
**LeetCode 2027.

---

- Oui. 1. Récapitulation des problèmes

> **Input** – une chaîne `s` de longueur `n (3 ≤ n ≤ 1000)` composé uniquement des caractères `'X'` et `'O'`.
> **Déplacer** – choisir les *trois caractères consécutifs* de `s` et les changer tous en `'O'`.
> **Objectif** – retourner le nombre *minimum* de mouvements requis pour que chaque caractère de `s` devienne `'O'`.

> **Exemples**
> * `"XXX"` → `1` mouvement
> * `"XXOX"` → `2` mouvements
> * `"OO"` → `0` mouvements

---

- Oui. 2. Pourquoi est-ce un problème ?

- Un mouvement couvre toujours ** exactement trois positions consécutives**.
- Oui. Si le premier caractère d'un triplet est `'X'`, nous *doit* le convertir – sinon il restera `'X'` pour toujours.
- La conversion de `'X'` transforme également les deux caractères suivants en `'O'`, quel que soit leur état d'origine.
- Oui. Par conséquent, lorsque nous voyons un `'X'`, la stratégie *optimale* est d'utiliser un mouvement qui commence à cet indice - nous ne pouvons jamais faire mieux.

Cette intuition se transforme en un algorithme cupide linéaire.

---

- Oui. 3. L'algorithme de l'avidité (temps O(n), espace O(1))

1. Scanner la chaîne de gauche à droite.
2. Chaque fois que nous rencontrons un `'X'` à l'index `i`:
* Incrémenter le compteur de réponses.
* Passez les deux indices suivants (`i += 3`) parce que le triplet entier est maintenant `'O'`.
3. Sinon (le caractère est déjà `'O'`), il suffit de faire un pas en avant.
4. Retourne le comptoir.

---

- Oui. 4. Mise en œuvre du code

Ci-dessous sont propres, implémentations idiomatiques dans **Java, Python, et C++**. Tous courent dans **O(n)** temps et utiliser **O(1)** espace supplémentaire.

---

#### 4.1 Java

"Java
solution de classe {
Int minimum public Déplacement(String s) {
mouvement int = 0;
pour (int i = 0; i < s.longueur(); ) {
si (s.charAt(i) == 'X') { // nous devons agir
mouvements++;
i += 3; // le triplet entier devient 'O '
} autre {
i++; // sauter un 'O '
}
}
les mouvements de retour;
}
}
«» "

---

4.2 Python

'`python
Solution de classe:
def minimum Déplacement(self, s: str) -> Int:
mouvements, i = 0, 0
n = len(s)
alors que i < n:
si s[i] == "X":
mouvements += 1
i += 3 # les trois deviennent 'O '
Sinon:
i += 1 # unique 'O '
retour
«» "

---

### 4.3 C++

'`cpp
solution de classe {
public:
Int minimum Déplace(chaîne s) {
mouvement int = 0;
pour (int i = 0; i < (int)s.s.ize(); ) {
si (s[i] == 'X') {
+ mouvements;
i += 3; // triplet devient 'O '
} autre {
++i; // sauter le 'O '
}
}
les mouvements de retour;
}
};
«» "

---

- Oui. 5. Analyse de la complexité

Métrique
- C'est quoi ?
Temps **O(n)**
Espace

`n` est la longueur de la chaîne d'entrée.

---

- Oui. 6. Cas de bord et pièges communs

Numéro
C'est quoi ?
Autres Oublier de sauter les deux indices suivants après un mouvement 3` (pas `i++`) Autres
Utiliser `i < n-2` comme condition de boucle Fonctionne mais force un contrôle supplémentaire; un simple `i < n` avec `continue` à l`intérieur est plus propre.
Autres Traiter l'opération comme réversible.L'opération est **non** réversible; une fois qu'un `'X'` est converti en `'O'` il le reste. Autres
Autres Penser que nous devrions *toujours* déplacer le pointeur par 3 même lorsque les deux suivants sont déjà `'O''' C'est très bien ; il donne toujours le compte optimal parce que le triplet deviendra `'O'` indépendamment. Autres

---

- Oui. 7. Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
L'observation gourmande est *extrêmement* simple une fois que vous voyez la logique triplet. Certains pourraient trop réfléchir et essayer DP ou BFS, trop compliquer le problème. Une solution naïve qui scanne chaque triplet sur chaque étape conduit à O(n2) le temps – un manuel. Autres
**Mise en œuvre**=O(n) boucle avec un seul compteur – pas de structures de données supplémentaires nécessaires. Utiliser une récursion ou une copie excessive de la chaîne est inutile. Oublier que l'opération couvre *trois* caractères peut produire des réponses erronées (par exemple, `s[i] = 'X' → `i += 1'). Autres
**Testation**= Inclure les chaînes avec des motifs en alternance `XO`, tous `'O'`, tous `'X'` et des mélanges aléatoires. Encadré de longueur 3 ou 4 – assurer une manipulation correcte des limites. Très longues chaînes (n = 1000) pour valider la linéarité. Autres
**Interview Perception** Un manque d'explication sur la raison pour laquelle l'algorithme est optimal peut soulever des drapeaux rouges. Le fait de ne pas discuter de complexité temporelle ou spatiale ou de cas de limites peut nuire à votre score. Autres

---

- Oui. 8. Takeaway optimisé SEO

Si vous préparez des interviews de codage ou appliquez à des entreprises de technologie, **

- **Algorithmes de grêle** – une base de résolution de problèmes d'entrevue.
- **O(n) temps, O(1) espace** solutions – précieux pour les discussions de performance.
- **Java, Python, C++** implémentations – prêtes à coller dans votre GitHub ou portfolio.

**Mots clés**: LeetCode 2027, Déplacement minimum vers la conversion Chaîne, Algorithme de Greedy, entretien de codage, solution Java, solution Python, solution C++, prép d'entrevue, pensée algorithmique, questions d'entrevue.

---

- Oui. 9. Mot final

- S'en tenir à la perspicacité avide : *=Quand vous voyez un X, agissez maintenant.
- Gardez votre boucle simple, il suffit de scanner une fois et sauter trois quand vous agissez.
- Souvenez-vous des pièges et testez votre solution contre les cas de bord.
- Expliquez l'intuition lors d'une entrevue – les intervieweurs aiment voir *pourquoi* vous avez choisi une solution, pas seulement *comment* vous l'avez mise en œuvre.

Bonne chance, et que vos interviews de codage convertissent plus que des chaînes!