---
titre: LeetCode 2137. Verser de l'eau entre les seaux pour faire des niveaux d'eau égaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Leetcode 2137 – Verser de l'eau entre les seaux pour faire des niveaux d'eau égaux
**Solution** – Recherche binaire (Java / Python / C++)
**Blog** – Le Bon, le Mauvais et l'Ugly – guide d'entrevue optimisé SEO

---

- Oui. 1. Récapitulation des problèmes

Vous avez des seaux `n` avec des quantités entières d'eau (`buckets[i]`).
Lorsque vous versez `k` gallons d'un seau à l'autre, vous perdez `perdu%` de cette goutte.

«» "
k → k * (perte/100) est renversé
k' = k * (1 - perte/100) atteint effectivement le seau cible
«» "

Vous pouvez verser *any* montant (pas nécessairement un entier) entre deux seaux.
Objectif : **Faire en sorte que tous les seaux contiennent la même quantité d'eau et retourner la quantité maximale possible. **

- `1 ≤ n ≤ 10^5`
- `0 ≤ seaux[i] ≤ 10^5`
- «0 ≤ perte ≤ 99»

Les réponses à l'intérieur de `1e‐5` de la valeur réelle sont acceptées.



---

- Oui. 2. Intuition Brute-Force (Pourquoi c'est trop lent)

Une façon naïve est d'essayer tous les niveaux finals possibles (par exemple en énumérant toutes les quantités de seau distinctes) et de simuler les vers.
Avec `n = 10^5` qui est impossible (`O(n^2)` dans le pire des cas).

Au lieu de cela, nous pouvons nous demander : **Puissons-nous atteindre un niveau cible "L" ? **
Cela transforme le problème en un problème de décision qui peut être résolu dans "O(n)".

Ensuite, nous pouvons faire une recherche binaire sur `L` pour trouver le niveau maximum possible.
Ceci donne un algorithme global `O(n log V)`, où `V = 10^5` (le volume maximum du seau).

---

- Oui. 3. Fonction de décision

Pour un niveau candidat «L»:

«» "
besoin = 0 // eau totale qui doit encore être ajoutée à un seau
donner = 0 // eau totale qui doit être retirée de certains seau

pour chaque quantité de seau x:
Si x < L: // le godet a besoin d'eau
// pour amener x jusqu'à L nous devons verser (L - x) / (1 - perteFraction)
besoin += (L - x) / (1 - perte)
sinon si x > L: // seau a un excès d'eau
donner += (x - L) // cette eau sera déversée
«» "

Si `besoin <= donner` (c'est-à-dire que nous avons assez d'excédent pour couvrir les dépenses requises après la comptabilisation de la perte), le niveau `L` est réalisable.
Nous voulons le *maximum* `L` qui satisfait cette condition.

---

- Oui. 4. Recherche binaire

«» "
faible = 0
haute = max(buckets) // limite supérieure; ne peut pas dépasser le maximum initial
eps = 1e-6 // prescription de précision

alors que haut - bas > eps:
milieu = (faible + élevé) / 2
si possible (au milieu):
faible = milieu // nous pouvons aller plus haut
Sinon:
haute = moyenne // trop élevée, rétrécir
retour faible
«» "

L'essai de faisabilité utilise la fonction de décision ci-dessus.

---

- Oui. 5. Code – Java

"Java
Importation de java.util.*;

solution de classe publique {
public double égaliserEau(int[] seaux, perte int) {
double perteFraction = perte / 100,0; // p.ex. 80% → 0,80
double eps = 1e-6;

double faible = 0,0;
double hauteur = Arrays.stream(buckets).max().getAsInt(); // lien supérieur

alors que (élevé - faible > eps) {
double milieu = (faible + élevé) / 2,0;
si (peutreach(buckets, milieu, perteFraction)) {
faible = milieu; // milieu est possible, essayer plus haut
} autre {
haute = moyenne; // moyenne trop élevée
}
}
retour faible;
}

booléen privé canReach(int[] seaux, double niveau, double perteFraction) {
double besoin = 0,0; // eau qui doit être versée dans
double donner = 0,0; // eau qui sera déversée

pour (int x : seaux) {
si (x < niveau) {
besoin += (niveau - x) / (1,0 - perteFraction);
} sinon si (x > niveau) {
donner += (x - niveau);
}
}
// Nous avons besoin d'une quantité suffisante pour couvrir les besoins après la perte
besoin de retour <= donner + 1e-12; // petit epsilon pour la sécurité numérique
}

public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
System.out.println(sol.equalizeWater(new int[]{1, 2, 7}, 80)); // 2.0
System.out.println(sol.equalizeEau(nouvelle int[[]{2, 4, 6}, 50)); // 3.5
Système.out.println(sol.equalizeEau(nouvelle int[[]{3, 3, 3}, 40)); // 3.0
}
}
«» "

---

- Oui. 6. Code – Python

'`python
def égalizeWater(buckets: list[int], perte: int) -> flotteur:
perte_frac = perte / 100,0
eps = 1e-6
faible, élevée = 0,0, max (poulets)

(niveau: flotteur) -> C'est vrai.
besoin = 0,0
donner = 0,0
pour x dans les seaux:
si x < niveau:
besoin += (niveau - x) / (1.0 - perte_frac)
elif x > niveau:
donner += (x - niveau)
besoin de retour <= donner + 1e-12

alors que haut - bas > eps:
milieu = (faible + élevé) / 2,0
si possible (au milieu):
faible = moyenne
Sinon:
haute = moyenne
retour faible


si __nom__ == "__main__" :
imprimer(égaliserEau([1, 2, 7], 80)) # 2.0
imprimer(égaliserEau([2, 4, 6], 50)) # 3.5
imprimer(égaliserEau([3, 3, 3, 3], 40)) # 3.0
«» "

---

- Oui. 7. Code – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
double égaliserEau(vecteur<int>& seaux, perte int) {
perte doubleFrac = perte / 100,0;
double eps = 1e-6;
double faible = 0,0;
double hauteur = *max_element(buckets.begin(), seaux.end());

auto faisable = [&](double niveau) -> Bool {
double besoin = 0,0, donner = 0,0;
pour (int x : seaux) {
si (x < niveau)
besoin += (niveau - x) / (1,0 - perteFrac);
sinon si (x > niveau)
donner += (x - niveau);
}
besoin de retour <= donner + 1e-12;
};

alors que (élevé - faible > eps) {
double milieu = (faible + élevé) / 2,0;
si (facile(milieu))
faible = milieu;
Autre
haute = moyenne;
}
retour faible;
}
};

Int main() {
Solution sol;
Cout << fixe << setprecision(5);
Cout << sol.égaliserEau({12,7}, 80) << endl; // 2.00000
<< sol.égaliserEau({2,4,6}, 50) << endl; // 3,50000
Cout << sol.égaliserEau({3,3,3,3}, 40) << endl; // 3.00000
}
«» "

---

- Oui. 8. Article du blog – Le bon, le mauvais et le mauvais

> **Titre**
> **Leetcode 2137 – Verser de l'eau entre les seaux pour faire des niveaux d'eau égaux**
> *Une plongée profonde dans la recherche binaire, la maîtrise des cas et le succès de l'entrevue*

---

8.1 Pourquoi ce problème se pose-t-il pour les entrevues

Aspect Pourquoi ça compte
-- -- -- -- -- --
**Le raisonnement qualitatif**=Vous êtes demandé à raisonner sur la perte et le transfert, un puzzle mathématique subtil. Autres
**La recherche binaire**=Une technique algorithmique de base; les employeurs veulent vous voir l'utiliser dans des espaces continus. Autres
**La précision du point de flot**Le codage du monde réel nécessite une manipulation attentive du «double»/«float». Autres
**La chasse aux cadavres**Les contraintes (perdues de 0 à 99, gros tableaux) testent la robustesse. Autres
**Optimisation**= O(n log V) est le bon endroit pour 10^5 points de données. Autres

> **Mots-clés de référence**: Leetcode 2137, problème de seau d'eau, entretien de recherche binaire, solutions d'entretien Java, Codage d'entretien Python, algorithme d'entretien C++, prép d'entretien d'ingénieur logiciel, résolution de problèmes algorithmique, transfert de pourcentage de perte, codage d'entretien d'emploi, questions d'entretien d'algorithme.

---

### 8.2 Ventilation des problèmes

1. **Comprendre la règle pour**
Lorsque vous versez `k` gallons, seulement `(1 - perte%) * k` arrive.
*Perdre 80% → vous obtenez efficacement 20% du volume versé. *

2. **Objectif**
Trouvez le niveau d'eau commun ** maximum** accessible par des vers répétés.

3. **Observations**
- Le niveau final ne peut jamais dépasser le seau initial maximum.
- Pour n'importe quel niveau candidat `L`, le total de la nécessité de remplir des seaux courts peut être calculé.
- Le montant total de la somme de la somme des "(x - L)" pour "x > L".
- Après la perte, la quantité *efficace* versée des seaux de débordement doit couvrir les besoins.

---

### 8.3 La fonction de décision – Le bien

**Pourquoi ça marche* *
- Oui. Il réduit un problème continu à un simple contrôle linéaire.
- O(n) temps par contrôle, pas de structures de données supplémentaires.
- Poigne un point flottant avec un minuscule épsilon pour éviter les erreurs d'arrondi.

** Faits saillants de la mise en œuvre* *
- "besoin" utilise la division par "(1 - LossFraction)" parce que c'est l'inverse de l'efficacité du transfert.
- "donner" est une soustraction simple.
- Oui. L'essai de faisabilité `besoin <= donne` permet de saisir directement l'état de faisabilité.

---

### 8.4 Recherche binaire – La mauvaise

Piège potentiel
Il s'agit d'un projet pilote.
**Perte de précision**= Utiliser un très petit 'eps' (1e-6 ou 1e-7) et `double`/`long double`. Autres
**Dépassement de la somme**= Toutes les sommes s'inscrivent dans le "double" parce que la somme maximale est 10^5 * 10^5 = 10^10, en toute sécurité à l'intérieur du double 53-bit mantissa. Autres
**Loop de l'infini**

**Pourquoi c'est
La recherche binaire sur les nombres flottants peut être déroutant mentalement. Dans les interviews, vous devez justifier clairement les limites et le critère d'arrêt; sinon l'intervieweur pourrait suspecter un bug subtil.

---

8.5 Les cas de stabilité numérique et de bord

1. ** Perte zéro (perte = 0)* *
La quantité effective versée équivaut à la quantité versée.
La fonction de décision fonctionne toujours : `1 - perteFraction = 1,0`.

2. **Perte = 99%**
Efficacité est `0.01`, donc diviser par `(1 - 0.99)` → `100`.
La précision est toujours sûre, mais méfiez-vous que `1 - LossFraction` soit extrêmement petite. Une vérification de la "perte == 100" provoquerait la division de zéro, mais les contraintes s'arrêtent à 99 %.

3. **Tous les seaux sont égaux**
La faisabilité tient toujours; la recherche binaire convergera rapidement.

4. **Grands tableaux**
L'algorithme reste rapide; aucune boucle nichée.

---

8.6 Comment le faire dans une interview en direct

1. **Lisez attentivement la question** – confirmez que vous comprenez que X% arrive.
2. **Exposer l'algorithme** avant le codage.
3. **Afficher la fonction de décision** – passer en revue un petit exemple manuellement.
4. **Précision des phrases** – expliquez pourquoi vous utilisez les "eps".
5. **Coder avec clarté** – éviter la surcomplication; écrire des boucles lisibles.
6. **Champs d'essai**:
- `[0,000]`, perte=0 → finale=100000.
- `[1, 2, 3]`, perte=99 → finale=0.01 * quelque chose? (montrer le résultat).
- Large tableau aléatoire avec perte = 50.

---

8.7 À emporter pour votre voyage de codage

- **La recherche binaire n'est pas seulement pour les tableaux** – elle fonctionne aussi pour les plages continues.
- **Les fonctions de décision sont de l'or** – ils vous permettent de convertir le meilleur d'entre eux est-ce possible ?
- **Soins flottants** – Prévoyez toujours les arrondis.
- **Toujours expliquer** – Un passage verbal clair impressionne les gestionnaires d'embauche bien plus qu'un extrait parfait mais illisible.

---

8.8 Verdict final

- **Bonne**: Le contrôle de faisabilité linéaire – simple, rapide, mathématiquement élégant.
- **Bad**: La boucle de recherche binaire – haute précision, mais gérable.
- **Ugly**: Gestion des points flottants et garantie de terminaison – l'habituel «gotcha» dans le codage des entrevues.

> **Résultat**
> La maîtrise de ce problème démontre une pensée algorithmique forte, une intuition pour la précision numérique et la confiance pour relever les défis de l'espace continu – toutes les compétences que les entreprises de pointe recherchent activement.

Bon codage et bonne chance pour la prochaine interview!

---

- Oui. 9. Remarques finales

Ce problème est un **tour de force** : mélange de mathématiques inspirées par la physique, de recherches binaires continues et d'une gestion prudente des points flottants.
Les solutions fournies Java, Python et C++ fonctionnent confortablement sous la limite de 105 données tout en répondant aux exigences de précision 1 e‐6.

Pour la prochaine entrevue, pratique expliquant la fonction **decision** étape par étape, montrez la logique de recherche binaire sur papier et soyez prêt à discuter de la manipulation des cas de bord.
Votre capacité à transformer une règle du monde réel apparemment désordonnée en un algorithme élégant est exactement ce que les recruteurs recherchent.

Bonne chance pour décrocher ce rôle d'ingénieur logiciel ! C'est ce qu'il a dit.

---