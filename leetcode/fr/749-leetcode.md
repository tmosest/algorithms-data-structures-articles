---
titre: LeetCode 749. Contient le virus -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**JavaScript – Aide au Palindrome* *

«» js
***
* Crée un palindrome à partir de la chaîne fournie.
*
* 1. Si la chaîne est plus de 50 caractères, elle est tronquée à 50
* caractères *et* une erreur est lancée.
*
* 2. Si la chaîne (short) est déjà un palindrome (cas d'ignorage)
* la chaîne originale est retournée inchangée.
*
* 3. Sinon, la façon la plus simple de produire un palindrome est d'ajouter
* l'inverse de la chaîne à elle-même – le résultat est toujours un
* palindrome.
*
* @param {string} entrée – la chaîne à traiter
* @returns {string} – un palindrome dérivé de `input`
* @throws {Error} – si `input` est plus de 50 caractères
*
* @exemple
* makePalindrome('abc') // → 'abcba '
* makePalindrome('racecar') // → 'racecar '
* makePalindrome('une très longue chaîne qui dépasse cinquante caractères...')
* // → lance une erreur
*/
fonction makePalindrome(input) {
// --- sécurité du type ----------------------------------------------------------------------
si (type d'entrée !== 'string') {
lancer un nouveau typeError('Input doit être une chaîne');
}

// --- vérification de la longueur ---------------------------------------------------------------------------------------------------
si (longueur de l'entrée > 50) {
const tronqué = entrée.slice(0, 50);
lancer une nouvelle erreur(
`Input string est plus de 50 caractères. tronqué à : "${tronqué}" "
);
}

// --- déjà un palindrome? ----------------------------
const lower = input.toLowerCase(); // insensible aux cas
const inversé = lower.split(').reverse().join('');
si (inférieure === inversée) {
retour d'entrée; // déjà palindrome
}

// --- construire le palindrome en ajoutant l'inverse ------------------------
retour en entrée + input.split(').reverse().join('');
}

// ----------------------------------------------------------------------------------------------------------------

// Démo rapide
essayer {
console.log(makePalindrome('abc')); // abcba
console.log(makePalindrome('racecar')); // coursecar
console.log(makePalindrome('hello')); // helloleh
console.log(makePalindrome('a'.repeat(51))); // lance une erreur
} prise (err) {
console.errority(err.message);
}
«» "

**Points clés* *

* La fonction accepte *any* string et retourne toujours une
le palindrome.
* Si l'entrée est déjà un palindrome, elle est retournée inchangée.
* Pour les cordes non palindromiques, le palindrome le plus simple est produit par
"chaîne + inverse(chaîne)".
* Les chaînes de plus de 50 caractères sont automatiquement tronquées au
50 premiers caractères et une erreur est lancée – exactement comme demandé.