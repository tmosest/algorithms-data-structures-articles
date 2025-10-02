---
titre: LeetCode 517. Super machines à laver -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Super machines à laver – LeetCode 517
**Une plongée en profondeur dans un problème d'interview de --Hard-- Java, Python, et C++ solutions, pièges, et SEO-friendly blog contenu* *

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Insights clés et cas de bord] (#insights clés -- cas de bord)
3. [Algorithme dans une coquille de noix] (#algorithme dans une coquille de noix)
4. [Analyse de la complexité] (#analyse de la complexité)
5. [Détails de mise en œuvre] (#détails de mise en œuvre)
- Java
- Python
- C++
6. [erreur commune et „Pièges"](#erreur commune--pièges)
7. [Approches et variations alternatives] (# approches-variations alternatives)
8. [Pourquoi ce problème se trouve-t-il dans les entrevues] (#pourquoi ce problème se trouve-t-il dans les entrevues)
9. [Traitement et retrait] (#Traitement et retrait)

---

## Aperçu du problème <a name="problem-overview"></a>

> **LeetCode 517 – Super laveuses* *
> Vous avez `n` super machines à laver sur une ligne.
> Chaque machine contient un certain nombre de robes («machines[i]».
> **Règle du mouvement**: Dans un mouvement, vous pouvez choisir n'importe quelle machine `m` (1 ≤ m ≤ n) et chaque machine sélectionnée passe *une* robe à l'une de ses machines adjacentes simultanément.
>
> **Objectif**: Faire chaque machine contient le même nombre de robes en utilisant le nombre minimum de mouvements.
> Si cela est impossible, retourner `-1`.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
Après 3 mouvements, chaque machine a 2 robes. Autres
Après 2 mouvements, chaque machine a 1 robe. Autres
Impossible – robes totales (2) n'est pas divisible par 3. Autres

**Contrôles* *

- `1 <= n <= 104`
- `0 <= machines[i] <= 105`

---

## Points de vue clés et causes de bord <un nom="key-inights--edge-cases"></a>

1. ** Vérification de faisabilité* *
- Si le nombre total de robes n'est pas divisible par `n`, une distribution égale est impossible → retourner `-1`.

2. **Convertissez-vous aux différences* *
- Calculer les robes cibles par machine: `avg = total / n`.
Remplacer chaque `machines[i]` par `diff = machines[i] - Oui.
- Un "diff" positif signifie que la machine a *extra* robes à envoyer.
- Un "diff" négatif signifie qu'il a besoin de robes du côté gauche.

3. ** Flux cumulé**
- Alors que nous balayons de gauche à droite, gardez une somme "cur".
- `cur` représente le nombre net de robes qui doivent circuler **à travers** la frontière actuelle (entre la machine `i` et `i+1`).
- Les mouvements minimums nécessaires jusqu'à l'indice "i" sont "max(="cur, diff)".

4. **Réponse finale**
- La réponse est le maximum de toutes les valeurs `max(="cur, diff)` vues pendant le balayage.

5. **Délibérations**
- "n" 1` → réponse est toujours `0`.
- Toutes les machines sont déjà égales → répondre `0`.
- Les grands nombres → utilisent des entiers 64 bits pour éviter les débordements en Java/C++.

---

## Algorithme dans une coquille de noix <un nom</a>

Texte
1. total = somme (machines)
2. si total % n != 0: retour -1
3. avg = total / n
4. cur = 0 // différence cumulative
5. ans = 0 // déplacements maximum vus
6. pour chaque machine m en machines:
diff = m - avg
pour diff
ans = max(ans, abs(cur), diff)
7. retour
«» "

*Pourquoi `abs(cur)`? *
`cur` est le nombre de robes qui doivent franchir la frontière *à droite* (si positif) ou *à gauche* (si négatif).
La valeur absolue est le nombre total de robes qui doivent franchir cette limite, c'est-à-dire le minimum de déplacements requis.

*Pourquoi "diff"? *
Si une machine a un grand "diff" positif, il doit envoyer que beaucoup de robes immédiatement, même si la somme cumulée est petite.

---

## Analyse de complexité <un nom="analyse de complexité"></a>

Opération Temps Espace
- C'est quoi ?
Autres Somme et balayage Autres
Généralités Autres

L'algorithme est linéaire et utilise une mémoire auxiliaire constante, satisfaisant les contraintes même pour `n = 104`.

---

## Détails de la mise en oeuvre <un nom</a>

### Java

"Java
solution de classe {
public int findMinMoves(int[] machines) {
int n = machines, longueur;
long total = 0;
pour (int m : machines) total += m;

si (total % n != 0) retour -1;

Int avg = (int) (total / n);
long cur = 0; // différence cumulative
Int ans = 0;

pour (int m : machines) {
int diff = m - avg;
pour diff;
int need = Math.max(int) Math.abs(cur), diff;
ans = Math.max(ans, besoin);
}
le retour des an;
}
}
«» "

> **Pourquoi "long"?**
> `total` peut être jusqu'à `109`, donc l'utilisation de `long` empêche le débordement lors de la sommation.

---

Python

'`python
Solution de classe:
def trouver MinMoves(self, machines: List[int]) -> Int:
n = len(machines)
total = somme (machines)

si total % n != 0:
retour -1

avg = total // n
pour = 0
ans = 0

pour m dans les machines:
diff = m - avg
pour diff
besoin = max(abs(cur), diff)
ans = max(ans, besoin)

retour et
«» "

---

C++

'`cpp
solution de classe {
public:
int findMinMoves(vecteur<int>& machines) {
int n = machines.size();
long total = 0;
pour (int m : machines) total += m;

si (total % n != 0) retour -1;

int avg = static_cast<int>(total / n);
longue courbure = 0; // différence cumulative
Int ans = 0;

pour (int m : machines) {
int diff = m - avg;
pour diff;
int need = std::max(static_cast<int>(std::abs(cur)), diff);
ans = md:max(ans, besoin);
}
le retour des an;
}
};
«» "

---

## Erreurs courantes & ----------</a>

Pourquoi il échoue
- C'est quoi ?
**Ignorer la vérification de faisabilité**=Retourner un nombre arbitraire lorsque total % n != Ajouter le "si" garde précoce. Autres
**Utiliser `int` pour la somme totale**. Autres
**Tirer `max(cur, diff)` sans abs**= Négatif `cur` non considéré → sous-estime les déplacements== Utiliser `abs(cur)` dans le max. Autres
**En supposant des mouvements = `max(cur)` Uniquement**.Cas manquants où une machine a un surplus important qui doit être expédié immédiatement. Autres
Autres **Réutiliser le tableau `machines` d'origine pour stocker les différences**= Confuse les futures itérations et rend le débogage dur==Créer une variable séparée ou recalculer à la volée. Autres

---

## Autres approches et variantes <un nom="autres approches-variations"></a>

1. ** Approche de la somme de préfixe**
- Calculer les montants des différences.
- La réponse est "max(maxPrefix, abs(minPrefix)").
- Équivalent à la méthode de balayage, mais exprimé différemment.

2. **Simulation (inefficacité)* *
- Simuler chaque mouvement étape par étape.
- Ne fonctionne que pour les très petits `n` (p. ex., la pratique des entretiens) mais a `O(n * déménagements)` runtime → **non recommandé** pour la production.

3. **Two-Pointer / Demande**
- Gardez une file d'indices qui ont besoin de robes.
- Poussez à droite.
- Encore une fois linéaire, mais plus lourde de code.

4. ** Programmation dynamique sur les limites* *
- Traitez chaque limite comme un état DP : combien de robes la traversent.
- Transition DP identique à la logique de flux cumulatif.

---

## Pourquoi ce problème se trouve-t-il dans les entrevues <un nom></a>

- **Shows mathématiques pensée** – la conversion aux différences est un classique *balance* truc.
- ** Temps linéaire et espace constant** – idéal pour les contraintes d'entrevue.
- **Edge-case heavy** – force les candidats à penser à la faisabilité, au débordement et aux valeurs négatives.
- **Traitement d'entrevue extrêmement courant** – souvent demandé dans les rondes sur site de l'entreprise technique (Google, Facebook, Amazon, Microsoft).

> *Question de style d'entrevue*:
> Vous êtes donné `machines` et une règle de déplacement. Comment calculer le nombre minimum de mouvements sans simuler chaque étape? (en milliers de dollars)
> L'intervieweur s'attend à ce que le raisonnement du flux cumulatif *.

---

## Wrap-Up & Take-away <a name="wrap-up-take-away"></a>

- Le problème des machines à laver Super se résume à un flux cumulatif de différences**.
- Oui. Le nombre minimal de mouvements correspond au maximum de deux quantités à chaque limite :
1. La différence absolue cumulative qui doit franchir la frontière.
2. L'excédent/déficit net de la machine actuelle elle-même.
- Un seul balayage linéaire donne la réponse dans le temps `O(n)` et `O(1)` espace supplémentaire.
- Éviter les pièges courants (contrôle de faisabilité, sommes de 64 bits, "abs(cur)".

**Pour les recruteurs :**
Montrez au candidat comment l'algorithme fonctionne sur les exemples fournis, mettez en évidence le garde de faisabilité, et demandez-leur de raisonner sur les cas de bord.

**Pour les personnes interrogées :**
Pratiquez le balayage sur le papier; une fois que vous êtes à l'aise avec l'astuce diff / cur, vous allez as ce problème dans n'importe quelle langue.

---

### SEO-Friendly Meta Description
> Code maître de leet 517 – Super machines à laver. Apprenez les solutions Java, Python et C++, les idées d'algorithmes, la gestion des cas de bord et les pièges communs dans ce guide complet.

---

Bon codage – et bonne chance pour votre prochaine entrevue de codage!