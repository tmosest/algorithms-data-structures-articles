---
titre: LeetCode 1758. Minimum de modifications pour faire alterner la chaîne binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**JavaScript (Node.js) – Changements mineurs pour faire alterner la chaîne binaire *
*Heure O(n) Espace O(1)*

«» js
/* Modifications minimales pour faire alterner la chaîne binaire
--------------------------------------------------
Lit une chaîne binaire depuis la ligne de commande (par exemple :
solution de nœud.js 10010100
et imprime le nombre minimum de retournements de caractères nécessaires
pour le transformer en une corde parfaitement alternée
("1010..." ou "0101...").

L'algorithme compte des erreurs lorsque nous essayons de forcer le
modèle qui commence par '1' (c.-à-d. 1,0,1,...).
Pour toute position i, le chiffre attendu est:
i%2 ===0 → '1' (parce que le motif commence par '1')
i%2 ===1 → '0'
Si le chiffre actuel correspond au chiffre prévu, nous devons le retourner,
Donc nous incrémentons le compteur. Le nombre de flips nécessaires pour
le motif opposé ("0101...") est simplement
longueur - flowersForPatternStarting With1
La réponse est le minimum des deux.

Le script ne contient aucune fonction ou classe – juste de haut niveau
code qui fonctionne dans un seul fichier.
*/

const s = process.argv[2]; // lire la chaîne binaire des args

let flipsStartingWith1 = 0;

// Compter les erreurs pour le motif 1,0,1,0,...
pour (let i = 0; i < s.longueur; i++) {
si (parseInt(s[i], 10) === i % 2) {
flipsStartingWith1++;
}
}

// Retours minimums entre les deux modèles alternés possibles
const result = Math.min(flipsStartingWith1, s.longueur - flipsStartingWith1);

console.log(résultat);
«» "

**Comment courir**

"""
# Exemple
solution de nœud.js 10010100
# Sortie: 3
«» "

Le script utilise uniquement des fonctionnalités JavaScript intégrées, fonctionne dans le temps linéaire et utilise un espace supplémentaire constant.