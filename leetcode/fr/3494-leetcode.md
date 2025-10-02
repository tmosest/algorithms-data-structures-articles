---
titre: LeetCode 3494. Trouvez le minimum de temps pour vendre des potions -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code de Leet de Mastering 3494: Trouver le minimum de temps pour fabriquer des potions
> Une plongée profonde dans le problème, trois solutions prêtes à la production (Java, Python, C++), et un blog prêt à l'interview qui explique le **bon**, **mauvais** et **ugly** de ce puzzle classique de programmation.

---

Aperçu du problème

Dans le monde brasseur-wizard, chaque potion doit traverser **n** les magiciens dans un ordre fixe.
L'assistant *i* prend

«» "
time_ij = compétence[i] * Mana[j]
«» "

pour finir la potion *j*.
L'objectif est de trouver le temps *minimum* nécessaire pour **m** potions à finir lorsque le processus est *asynchronisé le plus possible* (chaque assistant peut démarrer la prochaine potion dès que l'assistant précédent la remet).

> **Pourquoi cela compte dans les entrevues* *
> * Les problèmes de calendrier, de flux et d'avidy/DP sont fréquemment demandés sur LeetCode.
> * La même pensée est utilisée dans les interviews d'emploi du monde réel chez Google, Amazon, Stripe et Fintechs.
> * Résoudre ce problème montre que vous pouvez ** modéliser les contraintes**, ** utiliser des montants préfixes pour le travail O(nm)** et **écrire un code propre et convivial**.

---

Principales contraintes

Symbole Signification Exemple
- C'est quoi ?
Nombre de magiciens
Nombre de potions
"compétence [i]" *i*S facteur de compétence
"mana[j]" Potion *J*S mana factor `4, 5, 2, 7`
`time_ij = compétence[i] * mana[j]` *i* besoin de potion *j*

Le temps total **minimum** est le moment où l'assistant *dernier* termine la potion *dernier*.

---

Stratégies de solution

Stratégie Ce qu'il fait Quand l'utiliser
- C'est quoi ?
**Simulation et correction de la rupture**= Simuler l'ensemble du pipeline, mais garder la rupture* entre les potions consécutives minimale. Plus facile à comprendre, bon pour les petits `n,m`. Autres
**Prefix-Sum + Greedy**= Précalculer les compétences cumulatives, les utiliser pour calculer le temps d'attente supplémentaire pour chaque assistant en O(1). Solution optimale `O(nm)`, prête à la production. Autres
**Binary Search sur le temps total**.Devinez le temps total, vérifiez si toutes les potions peuvent finir, recherche binaire la réponse. Autres

La solution **prefix-sum** est la plus populaire car elle est concise, facile à prouver et fonctionne assez vite pour les limites (`n, m ≤ 1000`).

---

Mise en œuvre du code

Ci-dessous sont trois solutions prêtes à coller qui compilent sur la plateforme LeetCode. Tous les trois tournent en **«O(n·m)» temps** et utilisation **'O(n)' espace supplémentaire**.

> *Astuce*: Dans les interviews, commencez par une explication claire **préfixe** avant de plonger dans le code – qui démontre que vous comprenez les maths derrière le problème.

---

### Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe {
public long minTime(int[] compétence, int[] mana) {
n = habileté.longueur, m = mana.longueur;

// 1 préfixe des montants de compétences
long[] pref = nouveau long[n + 1];
pour (int i = 0; i < n; i++) pref[i + 1] = pref[i] + compétence[i];

long cur = 0; // heure à laquelle la potion précédente a fini
pour (int j = 1; j < m; j++) { // itérer sur tous sauf la première potion
long suivant = 0;
pour (int i = 0; i < n; i++) {
// Temps supplémentaire de l'assistant i doit attendre avant de commencer potion j
besoin long = cur + 1L * mana[j - 1] * pref[i + 1] - 1L * mana[j] * pref[i];
si (besoin > suivant) suivant = besoin;
}
cur = suivant; // cela devient l'heure de départ de la potion j
}

// temps total final = heure de début de la dernière potion + temps de brassage
retour cur + 1L * mana[m - 1] * pref[n];
}
}
«» "

---

### Python (style LeetCode)

'`python
à partir d'import d'itertools
de taper l'importation Liste

Solution de classe:
def minTime(self, compétence: List[int], mana: List[int]) -> Int:
n, m = len(skill), len(mana)

# préfixer les sommes (1 base)
pref = [0]
pour les compétences:
pref.append(pref[-1] + s)

pour = 0
pour j à portée (1, m):
nxt = 0
pour i dans la plage(n):
besoin = cur + mana[j - 1] * pref[i + 1] - mana[j] * pref[i]
si nécessaire > nxt:
nxt = besoin
cur = nxt

retour cur + mana[-1] * pref[-1]
«» "

---

C++ (style LeetCode)

'`cpp
solution de classe {
public:
Long temps(vecteur<int>&compétence, vecteur<int>&mana) {
int n = compétence.size(), m = mana.size();
vecteur <long> pref(n + 1, 0);
pour (int i = 0; i < n; ++i) pref[i + 1] = pref[i] + compétence[i];

longue courbure = 0;
pour (int j = 1; j < m; ++j) {
longueur longue nxt = 0;
pour (int i = 0; i < n; ++i) {
long besoin = cur + 1LL * mana[j - 1] * pref[i + 1]
- 1LL * mana[j] * pref[i];
nxt = max (nxt, besoin);
}
cur = nxt;
}

retour cur + 1LL * mana[m - 1] * pref[n];
}
};
«» "

> Les trois extraits sont **O(n·m)**, utilisez des entiers 64 bits (`long` / `long`) pour éviter le débordement, et suivez le format de signature de fonction de LeetCode.

---

Analyse de complexité

Étape de travail Total
C'est pas vrai.
"O(n)" espace
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
Calcul final

Avec les limites de problèmes (`n, m ≤ 1000`), c'est confortablement en dessous de la limite de LeetCode de 1 seconde.

---

Le bon, le mauvais, le mauvais de ce problème

Qu'est-ce qui est grand Qu'est-ce qu'il faut faire attention
- C'est quoi ?
** Bon** • Modélisation directe d'un flow-shop. <br>• Peut être résolu avec **simulation** ou un truc bien **préfixe-sum**. <br>• Démontre le pouvoir du raisonnement *cumulatif*.
La simulation naïve (déploiement du temps) peut être O(n·m·maxMana) qui est trop lente. <br>• Utiliser `int` partout risque de déborder. N'oubliez pas le temps entre les potions. <br>• Méfiez-vous de l'attente supplémentaire qui peut être nulle ou négative. Autres
**Ugly**) • Certains candidats essaient d'utiliser ** recherche binaire** sur le temps total, mais le test de faisabilité de l'essai est lourd et difficile à déboguer. <br>• Le mélange de *sommes partielles* et de *simulations* peut conduire à des bogues hors-par-un. <br>• Oubliant que la première potion n'a pas besoin d'une étape de "max-wait". Autres

Pièges communs

Une erreur Pourquoi il casse
- C'est quoi ?
Utiliser `int` pour la réponse finale peut être jusqu'à `10^9` → produit jusqu'à `10^18`. Passez à `long`/`long`. Autres
Autres Off‐by‐one dans le tableau de préfixes devrait être la somme des premières compétences « i » (1 base). Initialiser `pref[0] = 0` et utiliser `pref[i + 1] = pref[i] + compétence[i]`. Autres
Sauter l'étape "max" pour `j > 0'- La première potion peut finir plus tôt, mais les potions plus tard peuvent devoir attendre tous les magiciens. Bouclez sur tous les assistants et gardez la valeur maximum d'attente supplémentaire. Autres
Autres L'ajout d'une recherche binaire sur le temps total rend le code plus long que nécessaire. Préférez la solution linéaire "O(n·m)"; elle est propre et assez rapide. Autres

---

## C'est l'entrevue-Conseils prêts

1. **Démarrer en expliquant les contraintes** – chaque assistant doit commencer dès que le précédent se retire.
2. **Afficher l'aperçu du «préfixe»** – il réduit la formule du temps d'attente à une seule ligne.
3. **Débordement de concentration tôt** – soulignez pourquoi vous utilisez `long`.
4. **Si le temps le permet**, dessinez une simulation simple et justifiez ensuite pourquoi vous passez à la formule gourmande.
5. **Demander des éclaircissements** si vous n'êtes pas sûr des indices (0-basé versus 1-basé) – les intervieweurs apprécient cela.
6. **Écrire un code propre** – utiliser des noms de variables descriptives (`pref`, `cur`, `nextWait`) et ajouter des commentaires en ligne.

> *Résultat*: Vous semblerez avoir une compréhension profonde des motifs algorithmiques, plutôt que de simplement copier le pseudocode.

---

Les pensées finales

- Oui. Ce problème est une grande vitrine** de *l'horaire d'une boutique de débit*, *le raisonnement d'accord* et *les montants préfixés*.
- Oui. Les extraits de code ci-dessus sont **minimaux, corrects et prêts à être soumis**.
- Comprendre les aspects *bons, mauvais, laids* vous permettra d'expliquer votre solution avec confiance dans n'importe quel entretien technique.

---

Prêt à casser plus de problèmes de style flow-shop ?
Découvrez le LeetCodeShop et pratiquez l'astuce *prefix-sum* – vous verrez le modèle apparaître dans beaucoup d'autres questions d'entrevue. Bon codage !

---

*Sentez-vous libre de commenter ci-dessous si vous voulez une plongée plus profonde dans la vérification de faisabilité de l'approche de recherche binaire, ou si vous avez besoin d'aide avec une variante de flow-shop différente. *