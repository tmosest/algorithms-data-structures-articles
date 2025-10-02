---
titre: LeetCode 2710. Supprimer les zéros de piste d'une chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Supprimer Trailing Zeros d'une chaîne – 2710 LeetCode
*Java-Python C++ – Interview-Ready Solution + SEO-Optimized Blog Post*

---

Pourquoi ce problème compte

- **Question d'entrevue commune** – -Supprimer les zéros en arrière d'un nombre représenté comme une chaîne. (en milliers de dollars)
- **Démonstrations**:
- Compréhension de la manipulation des cordes.
- Logique de boucle efficace (pas de regex, pas de conversion entière).
- Sensibilité des cas de bord (tous les zéros, pas de zéros, cordes courtes).
- **Balises du référencement**: *Code de débit 2710*, *Supprimer les Zeros Trailing*, *Solution de Java*, *Solution de Python*, *Solution de C++*, *Codage de l'entrevue d'embauche*, *Manipulation de bande*, *O(n) Temps*, *O(1) Espace*

---

Déclaration du problème

Compte tenu d'un entier `num` positif représenté comme une chaîne, retourner l'entier `num` ** sans suivre les zéros** comme une chaîne.

«» "
Entrée : num = "51230100"
Sortie : "512301"

Entrée : num = "123"
Sortie : "123"
«» "

**Contrôles* *

- "1 ≤ longueur nominale ≤ 1000"
- `num` se compose de chiffres seulement.
- `num` n'a pas de zéros.

---

Une solution propre, O(n)

Le moyen le plus rapide est de marcher la chaîne **en arrière** jusqu'à ce que nous atteignions un chiffre non zéro, puis de retourner la chaîne jusqu'à ce point.

### Java

"Java
solution de classe publique {
public Chaîne supprimerTrailingZeros(String num) {
i = longueur num.longueur() - 1; // commencer à la fin
alors que (i >= 0 && num.charAt(i) == '0') {
i--; // sauter les zéros
}
// sous-chaîne(0, i+1) -> la fin est exclusive
retour num.substring(0, i + 1);
}
}
«» "

Python

'`python
Solution de classe:
Def removeTrailingZeros(self, num: str) -> str:
i = len(num) - 1
alors que i >= 0 et num[i] == «0»:
I -= 1
retour num[:i+1]
«» "

C++

'`cpp
solution de classe {
public:
chaîne supprimerTrailingZeros(chaîne num) {
int i = static_cast<int>(num.size()) - 1;
pendant que (i >= 0 & & num[i] == '0')
--i;
retour num.substr(0, i + 1);
}
};
«» "

Complexité

- **Heure**: `O(n)` – passe unique de la fin.
- **Espace**: `O(1)` – nous utilisons seulement une variable d'index.

---

Les pièges communs

Pourquoi c'est mauvais Que faire pour éviter
- C'est quoi ?
**Regex `num.rstrip('0')'** Toujours linéaire, mais ajoute les frais généraux et la lisibilité souffre. Éviter quand les intervieweurs veulent une clarté algorithmique. Autres
**`Integer.parseInt(num)` puis `String.valueOf(... / 10^k)`**= Excédents pour les grandes cordes, et nécessite des calculs entiers coûteux. Jamais convertir des nombres énormes en primitifs. Autres
**Loop depuis le début**= Vous devez stocker tous les chiffres jusqu'à ce que vous frappez le premier non-zéro, ce qui est gaspillé. Toujours traiter à partir de la fin lors de la suppression des suffixes. Autres
Le dernier chiffre non-zéro sera supprimé. Rappelez-vous que la sous-chaîne est *exclusive* à la fin. Autres
**Ignorer la chaîne tout-zéro** Poignée : Autres

---

Les variantes trop compliquées

Parfois, les gens sur-moteur:

1. **Créer une liste de personnages** – mémoire inutile, ajoute de la complexité.
2. **Récursion** – la profondeur de la pile est égale à la longueur de la chaîne, risque de `StackOverflowError`.
3. ** Implémentation personnalisée de la pile** – ré-implémentations de la manipulation de chaîne intégrée.
4. **Multiples Passes** – premier compte zéros, deuxième coupe.

Ces approches sont amusantes sur le plan académique mais ** jamais** dans une entrevue de codage. Soyez simple.

---

Suite de test rapide

'`python
essais = [
(« 51230100 », « 512301 »),
("123", "123"),
("1000", "1"),
("10", "1"),
("5", "5"),
("0", "0") # défensive, mais pas dans les contraintes
- Oui.

pour inp, exp dans les essais:
res = Solution().removeTrailingZeros(inp)
affermissez res == exp, f"Echec {inp}: obtenu {res}"
print("Tous les tests sont passés!")
«» "

---

## -- Interviews à emporter

1. ** Expliquez la logique O(n)** – Je marche de la fin jusqu'à ce que je frappe un non-zéro.
2. **Cas de bord de Mention** – tous les zéros, un seul chiffre, pas de zéros.
3. **Afficher l'analyse temps/espace** – temps O(n), espace O(1). (en milliers de dollars)
4. **Pourquoi ne pas utiliser `int`** – risque de débordement, non autorisé par les contraintes.
5. **Pourquoi ne pas utiliser regex** – toujours linéaire, mais frais généraux supplémentaires; les intervieweurs préfèrent souvent des boucles explicites.

---

Titre du blog optimisé du SEO

LeetCode 2710 – Supprimer les zéros de piste d'une chaîne Java, Python, C++ Solutions (Interview-Ready) – Le bon, le mauvais, le mauvais* *

### Description de la méta suggérée

> Master LeetCode 2710 avec des solutions Java, Python et C++ propres. Comprenez l'algorithme, évitez les pièges courants et asez votre entrevue de codage. Découvrez les bonnes, mauvaises et laides façons de résoudre "Supprimer les zéros de piste d'une corde."

Mots clés suggérés

- LeetCode 2710
- Supprimer les zéros de fuite
- Solution Java
- Solution Python
- Solution C++
- Problème de codage des entretiens
- Manipulation de chaînes
- Algorithme O(n)
- Préparation d'un entretien d'embauche

---

## Description du blog (pour l'article)

1. **Introduction** – Pourquoi le problème est une question d'entrevue de base.
2. **Réévaluation des problèmes** – Aperçu rapide des contraintes et des exemples.
3. **Bonne solution** – Pas à pas avec des extraits de code.
4. **Bad Solutions** – Erreurs courantes à surveiller.
5. **Modèles** – Exemples exagérés (et pourquoi ils sont mauvais).
6. **Testing & Edge Cases** – Comment valider votre code.
7. ** Analyse de complexité** – Temps et espace.
8. **Conseils d'entrevue** – Comment parler de votre solution.
9. **Conclusion** – Récapitulation, réflexion finale, appel à l'action (partager vos résultats, commenter).

---

Mot final

Gardez votre solution **concise** et **explicable**. Les intervieweurs apprécient autant la clarté que l'exactitude. En maîtrisant ce simple problème, vous montrerez que vous pouvez:

- Manipulation efficace des cordes.
- Éviter les pièges courants (dépassement, régex, passes inutiles).
- Discutez avec confiance de la complexité.

Bonne chance pour votre prochaine entrevue de codage – vous venez d'ajouter une solution propre et prête à l'entrevue à votre trousse!