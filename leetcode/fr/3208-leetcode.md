---
titre: LeetCode 3208. Groupes alternatifs II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3208. Alterner les groupes II – Les bons, les mauvais et les méchants
*LeetCode – Medium – Fenêtre coulissante sur un tableau circulaire*

> **Objectif:** Compter combien de groupes contigus de longueur **k** dans un tableau circulaire de 0-1 couleurs alternent (pas deux couleurs adjacentes sont les mêmes).
> **Input:** `int[] colors`, `int k`
> ** Sortie:** `int` – nombre de groupes alternés valides

Ci-dessous vous trouverez une solution claire et prête à la production dans **Java**, **Python** et **C++** (tout le temps O(n), O(1) espace supplémentaire).
Après le code, un billet de blog SEO optimisé explique l'algorithme, les pièges et les conseils d'entrevue.

---

Code de démarrage rapide

"Java
// Java (Signature de code leet)
solution de classe {
Nombre d'entrées publiquesOfAlternatingGroups(int[] couleurs, int k) {
int n = couleur.longueur;
si (k > n) retourner 0; // impossible

int ans = 0; // nombre de groupes alternés trouvés
int len = 1; // longueur du courant de course alternée

// Marcher le tableau circulaire exactement une fois (n + k - 1 pas)
pour (int i = 1; i < n + k - 1; i++) {
int cur = couleurs[i % n];
int prev = couleurs[(i - 1 + n) % n];

// Démarrer une nouvelle course si les couleurs adjacentes sont les mêmes
si (cur== prev) len = 1;
autres len++;

// Chaque fois que le parcours atteint la longueur k, il contient
// un groupe alternatif valide se terminant en position i
si (len >= k) ans++;
}
le retour des an;
}
}
«» "

'`python
# Python 3
Solution de classe:
def numberOfAlternatingGroups(self, colors: List[int], k: int) -> Int:
n = len(couleurs)
si k > n:
retour 0

ans, exécution = 0, 1
# Marcher le tableau circulaire n + k - 1 étapes
pour i dans la plage (1, n + k - 1):
cur, prev = couleurs[i % n], couleurs[i - 1) % n]
run = 1 si cur == prev sinon run + 1
si exécuté >= k:
+= 1
retour et
«» "

'`cpp
// C++17
solution de classe {
public:
Numéro int De groupes alternatifs(vecteur<int>& couleurs, int k) {
int n = colors.size();
si (k > n) retourne 0;
int ans = 0, run = 1;
pour (int i = 1; i < n + k - 1; ++i) {
int cur = couleurs[i % n];
int prev = couleurs[(i - 1 + n) % n];
run = (cur == prev) ? 1 : run + 1;
si (course >= k) ++ans;
}
le retour des an;
}
};
«» "

> **Pourquoi `n + k - 1` itérations? **
> Les premiers éléments `k-1` du tableau circulaire sont enroulés de la fin.
> En itérant `n + k - 1` fois nous voyons chaque fenêtre possible exactement une fois.

---

## Blog Post – Les bons, les mauvais et les méchants

- Oui. H1 – Alternating Groups II on LeetCode: Une plongée profonde pour la préparation de l'entrevue

> **Mots clés**: Groupes alternants II, LeetCode 3208, fenêtre coulissante, tableau circulaire, question d'entrevue, Java, Python, C++, algorithme, complexité temporelle, complexité spatiale.

---

- Oui. H2 – Aperçu du problème

On vous donne un tableau **circulaire** `couleurs` de 0s et 1s.
Un **groupe alternatif** de longueur `k` est un segment contigu où chaque paire de carreaux adjacents a des couleurs différentes.
Parce que le tableau est circulaire, les premiers et derniers éléments sont adjacents.

**Tâche**: Comptez le nombre de ces groupes.

---

- Oui. H2 – Intuition et le bon

1. **Fenêtre coulissante**
- Dans un tableau linéaire, nous allons glisser une fenêtre de taille `k` et vérifier si toutes les paires adjacentes diffèrent.
- Naïf, ce serait "O(nk)".

2. **One-pass, mémoire O(1)**
- Conservez une variable `run` qui enregistre la longueur du courant alternatif.
- Chaque fois que nous voyons deux couleurs adjacentes égales, `run` réinitialise à 1.
- Lorsque `run >= k`, la fenêtre se terminant à la position actuelle est un groupe alternatif valide.

3. ** Manipulation circulaire**
- Traitez le tableau comme s'il était étendu par des éléments `k‐1` à la fin (`colors[0...k-2]`).
- Pas d'espace supplémentaire: il suffit d'utiliser le modulo arithmétique ( 'i % n').

Cela donne un algorithme propre, **O(n)** avec **O(1)** espace supplémentaire – la réponse d'entrevue parfaite.

---

- Oui. H2 – Détails de mise en œuvre

Langue
- C'est quoi ?
Pour (int i = 1; i < n + k - 1; i++) Autres
**Python**"pour i dans la plage(1, n + k - 1):""couleurs[i % n]" Autres
**C++**="pour (int i = 1; i < n + k - 1; ++i)="couleurs[i % n]" Autres

**Étapes clés**
1. `run = (cur == prev) ? 1 : run + 1;`
2. Si (course >= k) et

**Décisions de la Cour* *
- `k > n` → impossible, retour 0.
- `k == n` → tout le tableau doit alterner.
- Tous les éléments les mêmes → 0 groupes.
- Tous les groupes alternant → `n` (car chaque rotation forme un groupe).

---

### H2 – Les mauvaises (pièges communs)

1. **Ignorer la Circulaire* *
- Utiliser un simple `pour i dans la plage(k, n):` manquera les fenêtres qui enveloppent.
*Fix* : étendre logiquement par des étapes "k-1".

2. ** Erreurs hors pair**
- Décomptage de la première fenêtre ou mauvaise gestion de l'état de réinitialisation (`run = 1` vs `run = 0`).
- Vérifier avec de petits tests (`[0,1,0], k=3` → 1 groupe).

3. **Wrong Reset Logic**
- Réinitialiser `run` à `0` au lieu de `1` brise le compte d'alternance.
- La première tuile d'un nouveau tour fait toujours partie d'une séquence valide de longueur 1.

---

### H2 – L'horrible (Pourquoi un "One-Pass" est surprenant)

Une approche à deux passages naïve pourrait être :

'`python
pour i dans la plage(n):
si toutes les couleurs[(i + j) % n] != couleurs[(i + j + 1) % n] pour j dans l'intervalle(k - 1)):
+= 1
«» "

C'est **O(nk)** et il est facile de sortir pour `n = 10^5`.
L'astuce de la fenêtre coulissante est élégante parce que nous n'avons pas besoin de revérifier toute la fenêtre; nous étendons juste par un élément et décidons si la fenêtre est toujours alternée.

---

- Oui. H2 – Résumé de la complexité

Démarche Temps Espace supplémentaire
- C'est quoi ?
Naïf (cochez chaque fenêtre)
Fenêtre coulissante (cette solution)

Avec `n` jusqu`à `10^5`, l`algorithme O(n) est obligatoire pour LeetCode.

---

#### H2 – Cas d'essai à essayer

Autres Test d'entrée Résultats attendus
- C'est quoi ?
"[0,1,0,0]", "k=3"
"[0,1,0,1,0,1]", "k=6"
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
(invalide par contrainte)
[0,1,0,1] ", "k=4 "
"[0,00,0]", "k=3"
"[0,1,0,1]" et "k=3"

---

- Oui. H2 – Conseils d'entrevue

- ** Clarifier la circularité** : demander à l'intervieweur de confirmer si le tableau est enroulé.
- **Expliquer la variable « run »** : montrer comment elle maintient la longueur du segment alternatif du courant.
- **Edge cas**: discuter `k == n` et `k > n` devant.
- **Complexité** : soulignez que l'algorithme est linéaire et utilise une mémoire constante.

---

- Oui. H2 – Conclusion

Le problème Alternating Groups II est un exemple classique où une fenêtre ** glisse** sur un tableau **circulaire** tourne un "O(nk)" apparemment dur. tâche dans une solution "O(n)" propre.
La mettre en œuvre en Java, en Python ou en C++ est simple une fois que vous comprenez l'idée de "Run" et comment gérer l'enroulement avec modulo arithmétique.

**À emporter :** Gardez un œil sur la circulaire cachée et pensez en termes de *runs* ou de *segments alternatifs* ; vous remarquerez souvent une solution à un passage.

---

### Méta-Description (SEO)

Découvrez comment résoudre LeetCode 3208 – Groupes alternants II – avec un algorithme de fenêtre coulissante en Java, Python et C++. Comprendre l'astuce, les cas de bord et la mise en œuvre prête à l'entrevue. Parfait pour coder des entrevues et améliorer vos compétences algorithmiques.

---