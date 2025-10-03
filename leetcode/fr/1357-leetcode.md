---
Titre: LeetCode 1357. Appliquer Remise chaque n Commande -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1357 – *Demander une réduction chaque n commandes*
**Solution en Java, Python & C++ + une interview-blog

---

Récapitulation des problèmes

Un supermarché vend des «produits[i]» pour des «prix[i]».
Une facture client est deux tableaux parallèles `product` et `amount`.
Chaque client reçoit une remise %** sur le sous-total.

Vous devez mettre en œuvre :

Texte
Caisse(int n, rabais int, produits int[], prix int[]
double getBill(int[] produit, quantité int[])
«» "

`getBill` retourne le montant final qu'un client doit payer (réduction appliquée si elle
nième client). Les réponses dans la case `1e-5` sont acceptées.

> **Constraints**
> * `1 ≤ n ≤ 104`
> * `0 ≤ remise ≤ 100`
> * `1 ≤ produits longueur ≤ 200`
> * `1 ≤ produit. longueur ≤ produits. longueur "
> * `produit` Les ID sont uniques

---

Idée de base

* ** IDs de produit de carte → prix** (`HashMap / unordered_map / dict`).
* Conservez un compte **** (`client actuel`).
* Après chaque appel à `getBill`, incrémentez le compteur.
Si `currentCustomer % n == 0`, appliquez la réduction.
* Calculer le sous-total par itération à travers l'ordre et la somme
"montant[i] * prix[produit[i]]".

L'algorithme est **O(k)** par appel, où *k* est le nombre d'éléments dans ce
commande, et utilise **O(p)** espace supplémentaire pour la carte des prix.

---

Code

C'est pas vrai. Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

caisse publique {
Int final privé n; // chaque nième client obtient une remise
réduction privée finale int; // %
finale privée Carte <entier,entier> prixMap;
client privé Cnt = 0; // compte combien de clients jusqu'à présent

Caissier public(int n, rabais int, produits int[], prix int[]) {
n = n;
Ça. remise = remise;
prixMap = nouveau HashMap<>(produits.longueur);
pour (int i = 0; i < produits. longueur; i++) {
prixMap.put(products[i], prix[i]); // O(p)
}
}

public double getBill(int[] produit, quantité int[]) {
client Cnt++; // 1-base de comptage

le double sous-total = 0;
pour (int i = 0; i < longueur du produit; i++) {
sous-total += prixMap.get(product[i]) * (double) montant[i];
}

si (client Cnt % n == 0) {/ nième client
Sous-total *= (100 - réduction) / 100.0; // appliquer la réduction
}
le sous-total du retour;
}
}
«» "

# # # # # #

'`python
Caissier:
def __init_(self, n: int, discount: int, produits: list[int], prix: list[int]):
auto.n = n
Self.discount = remise
auto.price_map = {p: pr pour p, pr en zip(produits, prix)}
auto.client_cnt = 0

def getBill(self, produit: list[int], quantité: list[int]) -> flotteur:
auto.client_cnt += 1
Sous-total = somme(auto.price_map[prod] * amt pour prod, amt en zip(produit, montant))
if self.customer_cnt % self.n == 0: # chaque nième client
Sous-total *= (100 - autocompte) / 100,0
total partiel
«» "

C'est vrai. C++

'`cpp
#inclut <non-ordonné_map>
#incluez <vecteur>

Caissier {
int n; // fréquence de réduction
réduction int; // pour cent
std::unordered_map<int, int> prixMap; // produit → prix
client int Cnt = 0; // Compteur à 1

public:
Caissier(int n, Int discount, std::vector<int> produits, std::vector<int> prix)
: n(n), rabais {
pour (size_t i = 0; i < products.size(); ++i)
prixMap[produits[i]] = prix[i];
}

pour obtenir deux fois GetBill(const std::vector<int>&product, const std::vector<int>&quantity) {
++client Cnt;
double sous-total = 0,0;
pour (size_t i = 0; i < product.size(); ++i)
sous-total += prixMap[product[i]] * static_cast<double>(montant[i]);

si (client Cnt % n == 0)
Sous-total *= static_cast<double>(100 - rabais) / 100.0;
le sous-total du retour;
}
};
«» "

---

Analyse de complexité

Étape Temps Espace
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Carte des prix du bâtiment Autres
Appel `getBill` (par ordre)

Avec au plus 1000 appels et `p ≤ 200`, la solution s'intègre facilement dans le
limites.

---

Article du blog – Le bon, le mauvais, et le mauvais de *Appliquez des rabais sur toutes les commandes*

- Oui. 1. Titre et Méta-Description

> **Titre**: *Appliquez une remise sur toutes les commandes – Solutions Java, Python & C++ (Code Leet 1357)*
> **Méta-Description**: Résoudre le LeetCode 1357 Application de réduction Chaque commande n avec le code Java, Python et C++ propre. Apprenez les compromis, les cas de bord et les conseils d'entrevue pour répondre à la question.

- Oui. 2. Aperçu général

1. **Introduction** – Pourquoi ce problème est un élément essentiel des entretiens techniques
2. **Énoncé du problème** – Rétablir les contraintes, les objectifs et les résultats attendus
3. **Notes clés** – ID de produit unique, fréquence de réduction fixe
4. **Stratégie** – Carte de recherche + compteur
5. **Mise en œuvre** – Extraits de code pour Java, Python, C++
6. **Cas de complexité et de bord** – Débordement, précision des points flottants
7. **Le Bon** – Simplicité, lisibilité, espace O(1) par appel
8. **Le mauvais** – Pièges alternatifs (recherche, récursion)
9. **L'Ugly** – Pièges du monde réel (débordement entier, remise manquante)
9. **Point de vue** – Ce que les intervieweurs recherchent vraiment
10. **Tests** – Comment écrire des tests unitaires
11. **FAQ** – Points de confusion communs
12. **Conclusion et appel à l'action** – Encourager la pratique et la préparation à l'emploi

- Oui. 3. Texte du blog complet

```markdown
# Appliquer une réduction sur tous les ordres – Solutions Java, Python & C++ (LeetCode 1357)

> **LeetCode 1357** est une question d'entrevue classique qui teste
> *choix de la structure des données*, *contre logique* et *gestion des points flottants*.
> Voici un guide étape par étape avec code propre en trois langues principales,
> plus une plongée profonde dans les compromis que chaque candidat devrait connaître.

Présentation

Les intervieweurs aiment les problèmes qui mélangent un système *stateful* (un caissier)
règle arithmétique simple (chaque client reçoit une remise).
Il vérifie :
- votre compréhension des cartes **hash** pour la recherche O(1)
- **Modulo arithmétique** pour les événements périodiques
- manipulation **déplacement-point maths** sans perte de précision

Si vous avez cloué cette question, vous vous sentirez confiant s'attaquer au même
des problèmes d'état dans tout cycle d'embauche technique.

---

Déclaration du problème

> Un magasin vend *produits* pour *prix*.
> Une commande client est deux tableaux: `product[]` et `amount[]`.
> Chaque client `n`‐th obtient un `décompte` % sur le sous-total.
> Mettre en œuvre `Cashier` avec `getBill()` qui retourne le montant final.

Contraintes:
- `1 ≤ n ≤ 104`
- "0 ≤ remise ≤ 100"
- "produits, longueur ≤ 200"
- "produit" Les ID sont **unique** et **positif**.

---

Remarques clés

Observation Pourquoi ça compte
C'est-à-dire
**Identifications uniques**= Permet la recherche directe de la carte de hachage. Autres
**Compte simple avec modulo. Autres
**"déduction"** ≤ 100" Cas de bord 0 % (pas de réduction) et 100 % (gratuit). Autres
Autres **Aucun changement d'ordre** ► Carte de prix construite une fois dans le constructeur. Autres

---

Stratégie

1. **Carte des prix** – `product → prix "
*O(p)* à construire, *O(1)* par recherche.
2. **Compte client** – `currentCustomer++`.
Appliquer la réduction lorsque `currentCustomer % n == 0`.
3. **Calcul partiel** – itérer sur commandes.

Le design est *O(k)* par appel, *O(p)* espace.
Les trois langues (Java, Python, C++) utilisent la même logique – juste différente
syntaxe.

---

Faits saillants de la mise en oeuvre

Pourquoi ça a l'air bien
-- -- -- -- -- -- -- -- -- -- -- -- --
**Java**="priceMap.put(products[i], prix[i]);` + `sous-total *= (100-discount)/100.0;`= Strong typing + explicite `double` cast.
**Python**= {p: pr for p, pr in zip(products, prices)}=` + `sous-total *= (100-discount)/100.0`= Compréhension concise, support automatique grand-int. Autres
**C++**= `unordered_map<int,int> priceMap;` + `sous-total *= (100-discount)/100.0`= Recherche rapide de compilation-temps, casting explicite au double. Autres

Les blocs de code de la section **Solution** sont intégrés pour copier rapidement.

---

Cas de complexité et de bord

* **Heure** – `O(k)` par ordre, linéaire en nombre d'articles.
* **Espace** – «O(p)» pour la carte; par appel «O(1)».
* **Overflow** – "Montant[i] * prix" correspond à l'int signé 32 bits ("" 200 × 104"),
mais nous jetons à "double" avant de se multiplier pour éviter un débordement accidentel.
* **Précision** – Utilisez `double` et un multiplicateur comme `(100-discount)/100.0`.
LeetCode accepte `1e-5`, de sorte que la norme IEEE-754 est sûre.

---

Les bonnes

Explication
C'est pas vrai.
Une carte, un compteur – pas de tours cachés. Autres
**Performance**= Recherche de cartes à temps constant; linéaire dans l'ordre seulement. Autres
**Maintenabilité**=Constructeur et méthode séparés; facile à tester. Autres
Même algorithme, adaptation minimale pour Java/Python/C++. Autres

---

Les mauvais

Pourquoi ça fait mal ?
C'est pas vrai.
**Array-Search Alternative**.L'utilisation d'une recherche linéaire dans le tableau produit donne du temps `O(p*k)` – inutile si `p` est 200. Autres
**Contrôle récursif**. Récursion serait empiler-overflow si `n` est grand. Autres
**Manquement de réinitialisation** Autres

---

Les affreux

Problème
C'est ce qu'on dit.
**Débordement entier**** Le «montant[i] * prix» pourrait dépasser le «231‐1» si vous restez dans «int». Promouvoir le "long" ou le "double" avant la multiplication. Autres
**Dérivation en points flottants**. Les remises répétées peuvent accumuler des erreurs d'arrondi. Retourner `double` et compter sur la tolérance `1e‐5`; utiliser `Décimal` en Python si l'exactitude est nécessaire. Autres
**Zero-division guard** Cnt % 1 == 0' toujours vrai. Fonctionne bien; il suffit de garantir la réduction s'applique à chaque client – un cas de coin que vous devriez tester. Autres

---

Conseils d'entrevue

1. **Demander des éclaircissements** – L'escompte est-il appliqué au sous-total ou au total final? (en milliers de dollars)
2. **Expliquez la logique du compteur** – incrémentez d'abord le compteur, puis vérifiez `cnt % n == 0`. (en milliers de dollars)
3. **Voir la carte construction** – Nous allons construire la carte une fois dans le constructeur pour l'espace O(p). (en milliers de dollars)
4. **Point flottant de Mention** – Nous utilisons le double pour préserver les cents. (en milliers de dollars)
5. **Discuss test cases** – Donner des exemples, en particulier pour les cas border Cases: `discount = 0`, `discount = 100`, `n = 1`, commandes importantes.

---

Liste de contrôle des essais

Autres Essai Que vérifier
-- -- -- -- -- --
Un exemple de base (du problème) Un rabais correct sur les 3ème et 6ème clients. Autres
"Réduction = 0" Aucun changement au sous-total. Autres
"Réduction = 100"" Zéro facture finale. Autres
Chaque client obtient une remise. Autres
Grande commande (200 articles) Autres
Autres Appels répétés > Le contre-modulo fonctionne toujours. Autres

---

Conclusion

LeetCode 1357 est une question *state-ful* qui combine l'utilisation de la structure de données avec
arithmétique modulaire.
Une approche simple de hachage + compteur donne un code propre et efficace dans **Java,
Python et C++**.
Comprendre les pièges (débordement, point flottant) et discuter de la conception
compromis dans les entrevues – vous démontrerez à la fois les compétences techniques et
résoudre les problèmes avec attention.

---

FAQ

C'est ce qu'il a dit.
-- -- -- -- -- --
**Puis-je utiliser un tableau au lieu d'une carte?**= Oui, mais vous avez besoin d'une recherche linéaire `O(p)` pour chaque ordre – O(k × p) temps. Autres
Autres **Que faire si les ID de produit ne sont pas uniques?**=Le problème garantit l'unicité; sinon vous auriez besoin d'une liste de prix par ID. Autres
**Utiliser `long` ou lancer `double` avant la multiplication. Autres
**Le code Leet accepte l'erreur 1e‐5; le double 53‐bit mantissa est plus que suffisant. Autres

---

# # # Obtenez l'embauche

La maîtrise de ce problème montre que vous pouvez :

* Carter les données d'une valeur efficacement (`HashMap` / `dict`).
* Manipulation des changements d'état périodique (opérateur « % »).
* Écrire un code propre, multiplateforme.

Ajoutez les solutions ci-dessus à votre portfolio, incluez l'explication prête à l'entrevue, et vous aurez un point de discussion fort pour toute interview **logiciel-ingénierie**.

Bon codage & bonne chance sur votre prochaine interview!