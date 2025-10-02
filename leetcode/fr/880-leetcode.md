---
titre: LeetCode 880. Chaîne décodée à index -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Résumé du problème – Chaîne décodée à index (LeetCode 880)

> **Objectif** – Avec une chaîne encodée `s` et un entier `k`, retournez le
> `k`‐th caractère de la chaîne *décodée*.
> `s` est composé de lettres minuscules et de chiffres `2–9`.
> Les chiffres indiquent que la bande décodée *current* doit être répétée
> « chiffres » fois au total (c'est-à-dire « d – 1 » exemplaires supplémentaires).
> La chaîne décodée peut être astronomiquement longue (jusqu'à 232 ‐ 1),
> mais `k` est toujours dans ses limites.

L'approche naïve classique serait en fait construire la chaîne décodée, qui
rapidement devient impossible. Le défi est d'obtenir le caractère "k"
sans matérialiser la corde.



-----------------------------------------------------------------------------------

- Oui. 2. Idée de solution de haut niveau

1. **Passer vers l'avant – Longueurs de calcul**
Scanner `s` de gauche à droite, en conservant une variable courante `len` qui
représente la longueur de la chaîne décodée *jusqu'à* le courant
position.
* Si le caractère actuel est une lettre → `len += 1`.
* Si c'est un chiffre `d` → `len *= d`.
Comme la longueur de chaîne décodée est garantie < 232, nous pouvons
conserver en toute sécurité dans un entier 64 bits (`long` in Java / C++ / `int` in
Python 3).

2. **Pass en arrière – Réduire `k`**
Iterate sur `s` **backwards** et ajuster `k` comme nous
expansions:
* Quand nous avons frappé un chiffre `d`, nous savons la bande avant le chiffre était
"len / d". Donc nous définissons `k %= len / d`.
(Si `k == 0`, cela signifie que nous voulons vraiment le dernier caractère de
la bande prénumérique, donc nous définissons `k = len / d`)
Puis mettre à jour `len = len / d` (désactiver la multiplication).
* Lorsque nous avons frappé une lettre, nous vérifions simplement si `k == 1`.
Si c'est le cas, cette lettre est la réponse – retournez-la.
Dans le cas contraire, `len -= 1` (sauf l'ajout de caractère unique) et
Continuez.

3. **Retourner le résultat** – La boucle frappera inévitablement une lettre où
1. Cette lettre est la réponse.

L'algorithme fonctionne dans **O(n)** temps (une fois en avant, une fois en arrière) et
utilise **O(1)** espace supplémentaire – parfait pour des solutions adaptées aux entrevues.



-----------------------------------------------------------------------------------

- Oui. 3. Code

Ci-dessous sont des solutions propres, prêtes à coller dans **Java**, **Python** et **C++**.

> **Astuce:** Dans chaque langue, nous gardons les noms de variables clairs (`len` est
> la longueur actuelle décodée, `k` l'index cible).
> Les commentaires expliquent chaque étape.

---

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
chaîne publique décodeAtIndex(chaîne s, int k) {
longue len = 0; // longueur décodée jusqu'à présent
int n = s.longueur();

/* ---- Passage vers l ' avant: calcul de la longueur totale ---- */
pour (int i = 0; i < n; i++) {
c = s.charAt(i);
si [Caracter.isLettre(c)] {
len++; // ajouter une lettre
} autre { // chiffre
int d = c - '0';
len *= d; // répéter la bande d
}
}

/* ---- Pass en arrière: trouver le caractère k-th ---- */
pour (int i = n - 1; i >= 0; i--) {
c = s.charAt(i);
si [Caracter.isLettre(c)] {
// Si k indique cette lettre
si (k == 1) retourner String.valueOf(c);
// annuler l'ajout de la lettre
} autre { // chiffre
int d = c - '0';
/= d; // annuler la multiplication

// k était à l'intérieur du bloc élargi
k %= len; // réduire k à la position du bloc prénumérique
i (k == 0) k = len; // si nous avons atterri sur le dernier char du bloc
}
}
retour "; // Impossible car le problème garantit une solution
}

/* ---- harnais d ' essai simple
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.decodeAtIndex("leet2code3", 10)); // o
Système.out.println(sol.decodeAtIndex("ha22", 5)); // h
Système.out.println(sol.decodeAtIndex("a2345678999999999999", 1)); // a
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
def décodeAtIndex(self, s: str, k: int) -> str:
longueur = 0 # longueur décodée jusqu'à présent

# Pass avant – calcul de la longueur finale
pour ch en s:
si ch.isalpha():
longueur += 1
Autre: # chiffre
longueur *= int(ch)

# Pass arrière – trouver le caractère k-th
pour ch en sens inverse(s):
si ch.isalpha():
Si k == 1:
retour ch
longueur -= 1
Autre: # chiffre
d = int(ch)
longueur //= d
k %= longueur
si k == 0:
k = longueur

# Le problème garantit que nous serons revenus.
retour ""

# ----- Démo ----
si __nom__ == "__main__" :
sol = Solution()
print(sol.decodeAtIndex("leet2code3", 10) # o
print(sol.decodeAtIndex("ha22", 5) # h
print(sol.decodeAtIndex("a2345678999999999999", 1)) #a
«» "

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
code de caractèresAtIndex(chaîne s, int k) {
longue len longue = 0; // longueur décodée jusqu'à présent
pour (charc : s) {
si [isalpha(c)]
len += 1;
Autre // chiffre
len *= (c - '0');
}

// Passage en arrière
pour (int i = (int)s.size() - 1; i >= 0; --i) {
c = s[i];
si [isalpha(c)] {
si (k) 1) retour c;
- = 1;
} autre {
int d = c - '0';
len /= d;
k %= (int)len;
si (k == 0) k = (int)len;
}
}
retour ' '; // inaccessible
}
};

/* ---- Démo ---- */
Int main() {
Solution sol;
Cout << sol.decodeAtIndex("leet2code3", 10) << endl; // o
Cout << sol.decodeAtIndex("ha22", 5) << endl; // h
<< sol.decodeAtIndex("a2345678999999999999999", 1) << endl; // a
retour 0;
}
«» "

-----------------------------------------------------------------------------------

- Oui. 4. Billet de blog – Le bon, le mauvais, et le lamentable des cordes de déco

> **Mots clés:** `chaîne décodée à index`, `leetcode 880`, `algorithme interview`,
> `O(n) solution`, `string decoding`, `coding interview prep`, `software engineer job interview`, `problem resolution "

---

4.1 Pourquoi ce problème est-il une médaille d'or pour les entrevues

LeetCode="S'il y a une chaîne décodée à Index=" est un exemple de manuel d'une interview
question qui teste plusieurs compétences de base:

Pourquoi ça compte ?
- Oui.
**Décomposition du problème**
**Mathématical Insight**
Autres **Optimisation de l'espace**
Autres **Edge-Case Awareness** Autres

Obtenir cette question de bons signaux que vous pouvez penser *hors de la boîte*,
identifier l'astuce cachée de la traversée inverse et coder proprement.

---

4.2 Les bonnes – Ce que nous aimons à propos de cette approche

1. **Complexité temporelle O(n)** – Nous lisons la chaîne deux fois (une fois en avant,
une fois en arrière). Même pour le maximum "s.longueur = 100", c'est le flambage
Vite.
2. **Complexité spatiale O(1)** – Pas de piles, pas de tableaux, juste quelques entiers
variables. Dans les entrevues, les intervieweurs aiment l'utilisation concise de l'espace.
3. **Aucun risque de dépassement** – En utilisant "long`/`long` (ou Python)
Nous entreposons en toute sécurité jusqu'à 232 ‐ 1.
4. **Maths intuitifs** – L'astuce modulo à l'arrière est naturelle une fois
Tu le vois pour la première fois. C'est une illustration parfaite de
Penser à l'envers dans la conception de l'algorithme.
5. **Évaluable à d'autres problèmes** – Le même modèle fonctionne pour
Chaîne décodée aux variantes de l'index et similaire *dilatation de la chaîne*
problèmes.

---

4.3 Les mauvaises – Pièges communs qui rompent votre code

Pourquoi ça arrive ?
- Oui.
Autres **Naïve String Building**
l'explosion. Utilisez plutôt le suivi de la longueur. Autres
La longueur décodée peut dépasser 231 – 1 ; les débordements de `int`. Autres
Après `k %= len`, oubliant que `k` pourrait être `0` causes
Erreurs hors-par-un. Autres
**L'ordre d'avancement du passage vers l'arrière**Le traitement vers l'avant dans la deuxième boucle s'applique mal
inverse la logique. "Renversés" (ou indice `i = n-1 ... 0`). Autres
**En supposant que tous les chiffres sont simples Le problème garantit 2-9, mais la généralisation sans
vérifier peut rompre avec `10` ou plus. Ne traitez que les caractères à un seul chiffre. Autres

---

4.4 Les horreurs – Ce qui peut mal tourner si vous êtes négligent

1. ** Dépassement dans les calculs intermédiaires* *
Si vous multipliez d'abord avant de diviser, un `long` peut encore déborder
pendant le passage avant (p. ex., 9 × 9 × ... Toujours jeter à "long"
avant la multiplication.

2. **Loop infini avec une logique Modulo incorrecte* *
Oublier `k %= len` après chaque chiffre mène à la boucle jamais
atteindre la réponse.

3. **Type de faute pour `k` en Python* *
Utiliser `int` (Python 2) ou `np.int32` va tronquer; utiliser toujours
Python 3=s intégré `int`.

4. **Ne pas manipuler les chaînes vides (Edge-Case)* *
LeetCode garantit `s` commence par une lettre, mais un codeur défensif
devrait toujours vérifier "len". 0' avant de revenir.

---

4.5 Résumé rapide de l'algorithme

«» "
1. len = 0
2. Pour chaque omble en s:
IF c est la lettre: len += 1
ELSE: len *= (c - '0')
3. Pour chaque char c en s (ordre inverse):
FI c est la lettre:
IF k == 1 : retour
-= 1
- Oui.
d = c - '0'
len /= d
k %= len
IF k == 0: k = len
«» "

*Temps: * O(=)
*Espace:* O(1)

---

### 4.6 Comment cela vous prépare pour une entrevue d'ingénieur logiciel

* **Code d'exposition propre** – Les extraits de Java, Python et C++ fournis
sont prêts à passer; les intervieweurs aiment quand vous pouvez livrer un poli
solution sans plaque de chaudière.

* ** Expliquer les échanges** – Mention que nous évitons O(n log n) ou
Des solutions de mémoire exponentielles, des intervieweurs de points demandent souvent.

* **Parler des cas d'Edge** – Discutez pourquoi nous traitons `k == 0`, pourquoi
"long" est utilisé, et pourquoi nous itérer à l'envers. Ceci démontre
profondeur de compréhension.

* **Lien vers d'autres études** – Dans votre CV ou portfolio,
à un blog (celui-ci) où vous analysez le problème à partir de multiples
angles — un excellent démarreur de conversation.

---

4.7 Pensée finale

Le problème de chaîne décodée à index de la chaîne peut ressembler à une simple chaîne
trick, mais il cache une leçon puissante: **quand un problème semble
besoin de construire toute la réponse, chercher un moyen de calculer seulement le
les métadonnées nécessaires et les calques. **

Maîtriser cette technique non seulement vous fait un chèque vert sur LeetCode
mais vous équipe également d'un état d'esprit que chaque entreprise de haute technologie
désirs – des solutions efficaces, élégantes et mathématiquement saines.

---

Codage heureux !

-----------------------------------------------------------------------------------

* Fin du blog *
---


---

N'hésitez pas à copier le code ou le billet de blog dans votre portfolio ou
GitHub README pour présenter vos côtelettes de résolution de problèmes et attirer
les gestionnaires d'embauche à la recherche de l'assistant (O(n)) dans votre prochain logiciel
l'équipe d'ingénierie.