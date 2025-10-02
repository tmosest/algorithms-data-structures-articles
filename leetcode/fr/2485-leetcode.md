---
titre: LeetCode 2485. Trouvez l'entier pivot -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Trouvez l'entier pivot (Code de bord 2485) – Un guide d'entrevue complet

> **Référencement optimal :**
> LeetCode 2485 – Trouvez le Pivot entier – Java / Python / C++ Solutions + Conseils d'entrevue

> **Meta Description:**
> Master LeetCode 2485 avec des explications claires, des solutions de maths O(1), la manipulation des cas de bord et le code en Java, Python et C++. Apprenez le bon, le mauvais, et le laid de ce problème pour as votre prochaine entrevue de codage.

---

- Oui. 1. Aperçu du problème

> **Trouver l'entier pivot**
> *Difficulté: * Facile (Code Leet 2485)
> **Objectif**:
> Pour un `n` donné (1 ≤ n ≤ 1000), trouver un entier `x` tel que

«» "
somme(1 ... x) == somme(x ... n)
«» "

Si aucun entier n'existe, retourner `-1`.
Il est garanti qu'il y aura **au plus un** entier pivot pour toute entrée.

> **Exemple**
> `n = 8 → x = 6`
> `1 + 2 + 3 + 4 + 5 + 6 = 6 + 7 + 8 = 21`

---

- Oui. 2. Intuition et mathématiques

La somme des premiers nombres `k` naturels est `k(k+1)/2`.
Laissez :

«» "
S_total = n(n+1)/2 // somme(1 ... n)
S_left = x(x+1)/2 // somme(1 ... x)
S_right = S_total - somme(1 ... (x-1))
«» "

La condition de pivot est:

«» "
_à gauche = _à droite
«» "

Utilisation de la formule pour les sommes:

«» "
x(x+1)/2 = n(n+1)/2 - (x-1)x/2
«» "

Simplifier → `x2 = n(n+1)/2`.
Ainsi, l'entier pivot est la racine carrée **integer** de `n(n+1)/2`.
Si cette racine carrée est un entier, c'est la réponse; sinon, aucun pivot n'existe.

---

- Oui. 3. Algorithme (O(1) Temps, O(1) Espace)

1. Calculer `total = n*(n+1)/2`.
2. Calculer `root = sqrt(total)` (double).
3. Si `root` est un entier (`root= sol(root)`), retourner `(int)root`.
4. Sinon, retourner `-1`.

Parce que `n ≤ 1000`, `total` convient confortablement aux entiers signés 32 bits, et la racine carrée est exacte pour tous les pivots valides.

---

- Oui. 4. Traitement des cas de bord

Motif Résultat
C'est pas vrai.
= 1'', sqrt = 1' Pivot = 1'
# # # # # # # # # # # # # # # # # # # # # # # "-1"
Total = 36 ' , pivot = 6
Grand `n` (p. ex. 1000)

---

- Oui. 5. Bon, mauvais, et humble

Aspect du bien
- C'est quoi ?
**Élégance mathématique**= Une ligne de maths → temps constant== Nécessite une familiarité avec les séries arithmétiques=Le relying sur point flottant peut introduire des erreurs de précision si elles ne sont pas manipulées avec soin==
**Mise en oeuvre**= Très court, code propre== Aucune= Besoin de se protéger contre le débordement d'entiers pour de plus grandes contraintes (pas de problème ici)==
**Scalabilité**= Fonctionne pour n'importe quel `n` qui convient à 64-bit=1=1 Si les contraintes ont changé (p. ex. `n > 109`), la formule est toujours maintenue, mais vous devez utiliser des ints 64-bit et une double précision sqrt=1
Certains préfèrent une boucle explicite. Autres

---

- Oui. 6. Autres approches

Méthode Complexité
- C'est quoi ?
**Recherche itérative** (pour la boucle 1...n) Autres
**Binary Search on `x`**= O(log n)=" Généralisable à d'autres contraintes=" Overkill pour un problème facile="
**Math + Contrôle entier** (préféré)

---

- Oui. 7. Mise en œuvre du code

### Java (LeetCode Style)

"Java
solution de classe {
public int pivot Total(int n) {
= n * (n + 1) / 2;
double racine = Math.sqrt(total);
Si (racine) {
retour (int) racine;
}
retour -1;
}
}
«» "

Python 3

'`python
Solution de classe:
def pivot Integer(self, n: int) -> Int:
total = n * (n + 1) // 2
racine = int(total ** 0,5)
retourner racine si racine * racine == total autre -1
«» "

### C++ (C++17)

'`cpp
solution de classe {
public:
pivot int Total(int n) {
long total = 1LL * n * (n + 1) / 2;
longue racine longue = sqrt((long double)total);
retour (racine * racine == total) ? racine : -1;
}
};
«» "

> **Astuce:** En C++, moulé sur `long double` avant d'appeler `sqrt` pour préserver la précision pour les grandes valeurs.

---

- Oui. 8. Fermeture amicale du SEO

**Traitements clés pour les intervieweurs et les recruteurs**

- Oui. La solution démontre **math fluency** et **O(1) thought** – très apprécié dans les entrevues techniques.
- Un code propre et concis en plusieurs langues montre ** polyglotte**.
- L'examen des cas de bord et des pièges potentiels (précision du point de flottement) reflète **la robustesse**.

---

- Oui. 9. Billet de blog (Markdown)

```markdown
# LeetCode 2485 – Trouvez l'entier pivot (Java / Python / C++)

* Difficulté: * Facile
*Complexité temporelle:* **O(1)**
*Complexité spatiale:* **O(1)**

Récapitulation du problème

Étant donné un entier positif `n`, trouver un entier `x` tel que

«» "
1 + 2 + ... + x = x + (x+1) + ... + n
«» "

Retourner le pivot `x`; si aucun n'existe, retourner `-1`.
`1 <= n <= 1000`.

---

Intuition

Utilisation de la formule pour la somme des premiers nombres "k" naturels:

«» "
somme(1 ... k) = k(k+1)/2
«» "

L'état du pivot se transforme en:

«» "
x2 = n(n+1)/2
«» "

Le pivot est donc la racine carrée entière de `n(n+1)/2`.

---

Algorithme (O(1))

1. `total = n*(n+1)/2`
2. `root = carré(total) "
3. Si `root` est un entier → retourner `(int)root`
4. Sinon → retour `-1`

---

Cas de bord

- `n = 1` → pivot `1`
- `n = 4` → `total = 10`, sqrt 3.16 → `- 1'

---

- Oui. Tant mieux. Méchant

C'est bien, c'est mal.
C'est pas vrai.
Un liner maths Aucun point flottant peut être difficile
Temps constant doit protéger contre le débordement pour plus grand `n` Autres
Autres Effacer le code "ceil(a)" par rapport à "floor(a)" peut confondre

---

Code (Java / Python / C++)

**Java**

"Java
solution de classe {
public int pivot Total(int n) {
= n * (n + 1) / 2;
double racine = Math.sqrt(total);
si (root) Math.floor(root) retourne (int) root;
retour -1;
}
}
«» "

**Python**

'`python
Solution de classe:
def pivot Integer(self, n: int) -> Int:
total = n * (n + 1) // 2
racine = int(total ** 0,5)
retourner racine si racine * racine == total autre -1
«» "

**C++**

'`cpp
solution de classe {
public:
pivot int Total(int n) {
long total = 1LL * n * (n + 1) / 2;
longue racine longue = sqrt((long double)total);
retour (racine * racine == total) ? racine : -1;
}
};
«» "

---

Les pensées finales

- Oui. Ce problème est un **grand extrait d'entrevue**: il vérifie vos connaissances en mathématiques, code la brièveté, et l'attention aux cas de bord.
- Mettez en avant le point de vue O(1) dans votre interview pour impressionner les recruteurs.
- Pratiquer le même modèle sur d'autres problèmes de "sum-equal" pour renforcer la technique.

Bonne chance pour casser le LeetCode 2485 – et atterrir ce travail de technologie! C'est ce qu'il a dit.
«» "

---

**Fin de l'article**