---
titre: LeetCode 2806. Solde du compte après l'achat arrondi -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2806. Solde de compte après l'achat arrondi – Problème de LeetCode facile
**Langues**: Java-Python-C++
**Objectif**: Ecrivez une solution propre et unique, expliquez la logique, et transformez-la en un billet de blog qui est convivial pour le référencement et prêt à travailler.

---

Aperçu du problème

- **Balance initiale**: 100 dollars.
- **Input**: "achatMontant" (0 ≤ achatMontant ≤ 100).
- **Processus**:
1. Tourner l'achat au multiple le plus proche de 10.
* Si le dernier chiffre est 5 ou plus → round **up**.
* Sinon → round **down**.
2. Soustraire le montant arrondi du solde.
- **Retour** le solde final.

---

Exemple

Montant arrondi Solde final
C'est pas vrai.
10,50 $ 90,50 $
15,0 20,0 80,0
100 000 $

---

- Oui. Contraintes

- 0 ≤ achat
- complexité du temps : **O(1)**
- La complexité spatiale : **O(1)**

---

Logique monoligne

Le montant arrondi peut être calculé directement:

Texte
arrondi = achatMontant + (10 - achatMontant % 10) % 10
«» "

- "Acheter % 10" donne le dernier chiffre.
- Oui. Si elle est 0‐4, `(10 - chiffre) % 10` → 0 → arrondir.
- Oui. Si c'est 5-9, l'expression → 10 chiffres → arrondir.

Solde final : 100 - arrondi.

---

Mise en œuvre du code

Java

"Java
solution de classe {
compte public intBalanceAfterPurchase(achat intMontant) {
int arrondi = achatMontant + (10 - achatMontant % 10) % 10;
retour 100 - arrondi;
}
}
«» "

Python

'`python
Solution de classe:
def accountBalanceAfterPurchase(self, buyMontant: int) -> Int:
arrondi = achatMontant + (10 - achatMontant % 10) % 10
retour 100 - arrondi
«» "

C++

'`cpp
solution de classe {
public:
compte intBalanceAfterPurchase(int buyMontant) {
int arrondi = achatMontant + (10 - achatMontant % 10) % 10;
retour 100 - arrondi;
}
};
«» "

Les trois snippets courent dans **O(1)** temps et **O(1)** espace.

---

C'est pas vrai. Essais de cas

Montant prévu
- Oui.
100 % 100 %
C'est le cas.
- Oui.
C'est une bonne idée.
100 % 0 % 0 %

La formule fonctionne pour chaque condition de limite parce que l'opération modulo et l'ajout de `10` produisent toujours un multiple valide de 10.

---

Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
Solution O(1); pas de boucles ou d'espace supplémentaire; logique intuitive d'arrondi
Certains candidats sur-ingénieur avec des déclarations conditionnelles; toujours O(1) mais plus longtemps.
Utiliser `Math.round` ou `DecimalFormat` en Java → frais généraux inutiles.

** À emporter**: Gardez-le simple, lisible et mathématiquement sain. Les solutions à un liner sont idéales pour coder les entrevues, mais ne sacrifient jamais la clarté.

---

Article de blog optimisé par le SEO

Titre
> **= Solde comptable après l'achat arrondi – solution Java, Python et C++ pour un liner (Code Leet 2806)* *

Description de la méta
> Découvrez comment résoudre LeetCode 2806 – Solde de compte après l'achat arrondi – en Java, Python et C++ avec un monoligne O(1) propre. Parfait pour coder la préparation d'entrevue, les entretiens d'emploi d'ingénieur de logiciel, et stimuler votre portefeuille de codage.

### Rubriques & Contenu

```markdown
# Solde de compte après l'achat arrondi – LeetCode 2806

## Résumé du problème
- Solde initial : 100 dollars
- Achat rond au multiple le plus proche de 10
- Soustraire l'équilibre
- Contraintes: Montant ≤ 100

- Oui. Pourquoi ce problème est important
- Démontre **arithmétique modulaire** – un élément de base dans les entrevues de codage.
- Testez votre capacité à écrire des solutions **O(1)**.
- Bon pour montrer que vous pouvez ** optimiser** et garder le code concis.

## La magie d'un liner en trois langues
### Java
"Java
int arrondi = achatMontant + (10 - achatMontant % 10) % 10;
retour 100 - arrondi;
«» "
Python
'`python
arrondi = achatMontant + (10 - achatMontant % 10) % 10
retour 100 - arrondi
«» "
C++
'`cpp
int arrondi = achatMontant + (10 - achatMontant % 10) % 10;
retour 100 - arrondi;
«» "

## Cas de bord & Validation
- 0 → 100
- 5 → 90
- 45 → 60
- 100 → 0

## Bonne, mauvaise, mauvaise – Une lentille d'entrevue de codage
- **Bien**: O(1) temps, pas de boucles, expression unique.
- **Bad**: Logique conditionnelle trop compliquée.
- **Ugly**: Modifier l'entrée, en utilisant des bibliothèques inutiles.

Comment cela stimule votre chasse à l'emploi
- Montre la maîtrise de **arithmétique de base** et **optimisation du code**.
- Démontre la compétence translingue** (Java, Python, C++).
- souligne votre capacité à produire **propre, code prêt à la production**.

Résumé
LeetCode 2806 est un échauffement parfait pour toute entrevue avec un ingénieur logiciel. Une solution monoligne reflète une pensée propre et une forte compréhension des fondamentaux – caractérise chaque gestionnaire d'embauche.

---

Mots clés pour référencement
- LeetCode 2806
- Solde du compte après l'achat arrondi
- Solution Java Python C++
- Problème de LeetCode
- Codage de la préparation de l'entrevue
- Solution O(1)
- Entretien arithmétique modulaire
- Conseils d'entretien de l'ingénieur logiciel
«» "

Pourquoi cet article vous aide à être embauché

1. **Showcases compétences de résolution de problèmes** – Le post passe par le raisonnement derrière le monoligneur.
2. **Démonstration du code propre** – Vous gagnerez des points de brownie pour la brièveté et la lisibilité.
3. **Cross‐Language Proficiency** – Les intervieweurs aiment les candidats qui peuvent coder en plusieurs langues.
4. **Mots-clefs de référence** – Lorsque les recruteurs recherchent le code de crédit 2806, ou l'achat arrondi de votre article.
5. ** Valeur du portefeuille** – Ajouter l'article à votre GitHub README ou blog personnel; il devient un point de conversation dans les interviews.

---

La dernière pensée

Une solution concise et mathématiquement élégante est la marque d'un développeur expérimenté. En maîtrisant des problèmes comme **Compte Balance After Rounded Purchase** et en articulant la logique dans un billet de blog, vous allez non seulement ace LeetCode mais aussi atterrir ce rôle convoité d'ingénierie logicielle. Bon codage !