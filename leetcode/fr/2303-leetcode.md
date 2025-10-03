---
titre: LeetCode 2303. Calculer le montant payé en impôts -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2303 – Calculer le montant payé en impôts
** Solutions linguistiques-agnostiques (Java / Python / C++)**
**Article de blog** – Le bon, le mauvais, et la laid de s'attaquer à ce problème dans une interview, ainsi qu'un guide rapide de référencement pour obtenir ce travail de codage.

---

### TL;DR

- **Objectif** : Compte tenu des tranches d'imposition progressives et d'un revenu, calculez le montant exact de l'impôt que vous devez.
- **Heure**: O(n) – on passe par les crochets.
- **Espace**: O(1) – mémoire supplémentaire constante.
- **Réponse acceptée**: "double", précision jusqu'à "1e-5".

---

- Oui. 1. Récapitulation des problèmes

> **Input**
> - `brackets`: tableau 2-D, `brackets[i] = [upper_i, percent_i] "
> - «revenu»: montant entier gagné
>
> ** Sortie**
> - Impôt total dû en tant que «double»

Les crochets sont ** triés par limite supérieure** et la dernière limite supérieure est toujours `≥ revenu`.
Chaque tranche représente une tranche d'imposition * progressive* :
- Le premier dollar supérieur est taxé à "pourcentage".
- Le prochain `upper1 – upper0` dollars à `pour cent1%`, etc.

---

- Oui. 2. Intuition Brute-Force

Passez par les crochets, déterminer combien de dollars tombent dans la bande actuelle, calculer la taxe, et l'accumuler.

Texte
pour chaque tranche (en haut, en pourcentage):
imposable = min(revenu, supérieur - précédent)
taxe += imposable * pour cent / 100
revenu -= imposable
précédent Supérieur = supérieur
«» "

Une fois que le revenu est zéro, nous pouvons arrêter tôt.

---

- Oui. 3. Mise en œuvre du code

#### 3.1 Java

"Java
solution de classe publique {
double calcul public Impôt(int[][] entre parenthèses, revenu int) {
double imposition = 0,0;
int moins = 0; // limite inférieure du support courant

pour (int[] : crochets) {
int supérieur = support[0];
pourcentage int = tranche[1];

// Combien de revenus entre dans cette tranche
double imposition = Math.min (revenu, supérieur - inférieur);
taxe += imposable * pour cent / 100,0; // appliquer le taux
revenu -= imposable; // supprimer le montant traité

si (revenu <= 0) pause; // tous les revenus imposés
inférieur = supérieur; // passer à la prochaine tranche
}
l'impôt de retour;
}
}
«» "

> **Pourquoi `double`?**
> Le problème exige un résultat en point flottant; l'utilisation de «double» donne la précision nécessaire («10−5»).
> **Complexité** – temps « O(n) », espace « O(1) ».

---

3.2 Python 3

'`python
Solution de classe:
def calcul Impôt(supplémentaire, entre parenthèses: Liste[Liste[int]], revenu: int) -> flotteur:
taxe = 0,0
inférieur = 0

pour le haut, pour cent entre parenthèses:
imposable = min(revenu, supérieur - inférieur)
taxe += imposable * pour cent / 100,0
revenu -= imposable
si le revenu est <= 0:
pause
inférieur = supérieur

impôt de retour
«» "

> **Conseils pour le python**
> - `min()` garde le code concis.
> - La "Liste [Liste]" type conseil est facultatif mais recommandé pour la lisibilité.

---

### 3.3 C++

'`cpp
solution de classe {
public:
double calculTaxe(vecteur<vecteur<int>>&entre parenthèses, revenu int) {
double imposition = 0,0;
int inférieur = 0;

pour (const auto & entre crochets : crochets) {
int supérieur = support[0];
pourcentage int = tranche[1];

int imposable = min(revenu, supérieur - inférieur);
taxe += imposable * pour cent / 100,0;
revenu -= imposable;

si (revenu <= 0) rupture;
inférieure = supérieure;
}
l'impôt de retour;
}
};
«» "

> **Pourquoi `std::min`?**
> La fonction STL maintient la logique identique à Java/Python.

---

- Oui. 4. Pourquoi le Code fonctionne

Étape Ce qu'il fait Pourquoi il importe
-- -- -- -- -- -- -- -- -- -- -- --
= min(revenu, supérieur - inférieur) Détermine combien de dollars sont imposés au taux actuel.
"Taxe += taxable * pour cent / 100,0`=" Accumule l'impôt dans une valeur en points flottants
"revenu -= imposable"
"si (revenu <= 0) break" "Départ anticipé" Évite les itérations inutiles (optimalité)

Comme les crochets sont triés, chaque dollar de revenu est traité **exactement une fois** – garantissant un temps linéaire.

---

- Oui. 5. Les bonnes, les mauvaises et l'atroce problème d'entrevue

Les bons
1. **Énoncé de problème clair** – L'impôt progressif est un scénario d'entrevue courant.
2. **Simple boucle** – Facile à raisonner, aucune récursion ou DP nécessaire.
3. **Scales bien** – Jusqu'à 100 crochets, coût de calcul insignifiant.
4. **Connectivité réelle** – La logique du calcul fiscal apparaît dans les concours de finances, de systèmes de paye et de codage.

- Oui. Les mauvais
1. **Pièges de précision** – Utiliser `float` au lieu de `double` peut conduire à des erreurs `1e‐5`.
2. ** Erreurs hors-par-un** – Oubliant de mettre à jour « plus bas » après chaque itération ou mal calculer la largeur du support.
3. **Chiffres d'épargne** – Le revenu correspond exactement à une tranche supérieure; zéro revenu; zéro pour cent d'impôt.
4. **Parsage d'entrée de LeetCode** – Parfois, `brackets` peut venir comme des tableaux imbriqués de longueur inconnue, nécessitant une analyse robuste.

- Oui. L'Ugly
1. ** stress d'entrevue** – Les candidats pourraient surestimer le problème en ajoutant des structures de données inutiles.
2. **La confusion dans le fuseau horaire** – Certains peuvent mal interpréter l'ordre des crochets; rappelez-vous toujours que le tableau est trié.
3. **Quirks de langue** – En Java, la division entière tronque silencieusement, de sorte que le casting vers "double" est essentiel.
4. ** Contraintes lourdes** – Le problème garantit que la dernière tranche limite supérieure ≥ revenu; oubliant cela peut rendre la solution incomplète.

---

- Oui. 6. En-tête du blog optimisé SEO

> **LeetCode 2303 – Calculer le montant payé en impôts : Java, Python, C++ Solutions + Stratégie d'entrevue**

### Description de la méta (155 caractères)

> Maître LeetCode 2303 en quelques minutes. Obtenez le code Java, Python et C++ propre, apprenez l'algorithme linéaire, et voyez comment aser le problème de calcul de la taxe dans une interview d'emploi.

### Mots-clés pour éparpiller

- LeetCode 2303
- Calculer le montant payé en impôts
- Algorithme des tranches d'imposition
- Entretien de codage Java
- Solutions Python LeetCode
- Entretien de codage C++
- Calcul progressif de l'impôt
- Solution de problème d'entretien
- Entretien des structures de données
- Entretien de l'ingénieur logiciel

---

- Oui. 7. Comment utiliser ce blog pour trouver un emploi

1. **Afficher le code** – Publier les trois extraits de code dans une repo GitHub. Étiquettez vos commits avec le code Leet 2303 – Calcul fiscal.
2. **Exposer le processus de pensée** – Dans le README, marchez à travers l'analyse "bonne, mauvaise, laid". Les recruteurs aiment voir la profondeur de résolution des problèmes.
3. **Ajouter une démonstration en direct** – Créer une petite page Web (HTML + JS) où les utilisateurs peuvent saisir des crochets et des revenus et voir l'impôt instantanément.
4. **Lien vers un blog** – Poster l'article sur Medium, Dev.to, ou un site personnel. Utilisez les mots-clés de référencement afin que les recruteurs le trouvent lors de la recherche de calcul d'impôt de LeetCode.
5. ** Variantes de pratique** – Rédigez un article de suivi sur -Bracket fiscal Variations: Bound supérieur > Revenu par rapport à < Revenu. Elle démontre sa capacité d'adaptation.

---

- Oui. 8. Pensées finales

- **Gardez-le simple** – Une boucle linéaire est tout ce dont vous avez besoin.
- **Précision** – Utilisez toujours `double` (Java/C++) ou `float` avec soin (Python `float`).
- **Test Edge Cases** – Aucun revenu, zéro pour cent, revenu égal limite supérieure.
- **Documentez votre processus de pensée** – Les intervieweurs apprécient la clarté; expliquez pourquoi vous avez choisi l'algorithme et comment vous avez géré les pièges.

Joyeux codage, et que votre prochaine interview soit sur la solution *bonne* et *propre* que vous venez de construire! C'est ce qu'il a dit