---
titre: LeetCode 2167. Délai minimum pour retirer tous les wagons contenant des marchandises illégales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2167 – Délai minimum pour enlever tous les wagons contenant des marchandises illégales
*Temps dur O(n), espace O(1)

---

Récapitulation des problèmes

On vous donne une chaîne binaire `s` où
- `s[i] = '0'' – la voiture est *propre*
- `s[i] = '1'' – la voiture contient *biens illicites*

Vous pouvez effectuer l'une des opérations suivantes n'importe quel nombre de fois:

Opération
- C'est quoi ?
Autres Supprimer de **gauche** fin (`s[0]`) - Oui.
Autres Supprimer de **à droite** fin (`s[n-1]`) - Oui.
Supprimer ** n'importe où** dans la chaîne

Retournez le temps total *minimum* nécessaire pour supprimer **chaque** `1` de la chaîne.
(Une chaîne vide compte comme "aucune marchandise illégale".)

> **Exemples**
> `s = "1100101"` → réponse = `5`
> `s = "0010"` → réponse = `2`

---

### # Une perspective fondamentale

Au lieu de penser en termes de "where to remove first", pensez à **splitting the string** at a pivot `p`:

«» "
[ 0 ... p-1) p ... n-1 ]
«» "

* Pour la partie gauche `0 ... p-1` nous pouvons:
* soit supprimer tout de la fin gauche (`coût = p`)
* ou supprimer chaque `1` individuellement (`coût = 2 * (#ones dans cette partie)`)

* Pour la bonne partie `p ... n-1` nous pouvons faire l'opération symétrique.

Si nous connaissons le coût *meilleur* pour le côté gauche jusqu'à chaque indice `i`, nous pouvons scanner une fois et évaluer le meilleur coût total pour chaque pivot dans O(n).

---

### -Passe unique O(1)-Algorithme spatial

1. **Initialiser**
- `n = longueur s. "
- `leftCost = 0` – le meilleur coût pour effacer tout jusqu'à l'index actuel (en utilisant seulement les suppressions de gauche ou de milieu)
- `réponse = n` – pire cas: supprimer tout de la gauche

2. **Scan gauche → droite* *
Pour chaque indice «i» (0-basé):
- `leftCost = min(leftCost + (s[i] == '1' ? 2 : 0), i + 1)`
*`i+1`* est le coût si nous décidons de supprimer le préfixe entier `[0 ... i]` de la gauche.
- `réponse = min(réponse, gaucheCoût + (n - 1 - i))`
*`n-1-i`* est le coût de la suppression du suffixe `[i+1 ... n-1]` à droite.

3. **Retour** "réponse".

Pourquoi ça marche ?
- `leftCost` représente toujours le coût *optimal* pour supprimer tous les `1`s du préfixe `[0 ... i]` en utilisant les opérations autorisées (soit en coupant le préfixe entier ou en supprimant chaque `1` individuellement).
- Ajouter des comptes `n-1-i` pour la meilleure façon de supprimer le suffixe restant (le réduire de la droite).
- Oui. En mettant à jour la réponse à chaque étape, nous examinons chaque position de pivot possible.

---

Complexe

Valeur métrique
C'est pas vrai.
Heure **O(n)** Autres
Espace

`n` ≤ 200 000, donc cette solution linéaire passe facilement tous les essais.

---

Mise en œuvre du code

Voici trois solutions complètes et autonomes – une pour chaque langue demandée.
Tous utilisent le même algorithme, juste des différences de syntaxe.

---

Java

"Java
solution de classe {
Int minimum public Heure(s) {
int n = s.longueur();
Int gauche Coût = 0;
réponse int = n; // pire cas: supprimer tout de la gauche

pour (int i = 0; i < n; i++) {
// coût si nous continuons à supprimer le '1' actuel (ou rien si c'est '0')
int supprimer Milieu = gauche Coût + (s.charAt(i) == '1' ? 2 : 0);
// coût si nous coupons le préfixe entier [0..i] de la gauche
l'extrémité intLeft = i + 1;
gauche Coût = Math.min(deleteMiddle, trimLeft);

// meilleur coût pour le suffixe après i (à droite)
Int droite Trim = n - 1 - i;
réponse = Math.min(réponse, gauche) Coût + droitTrim);
}
réponse de retour;
}
}
«» "

---

Python

'`python
Solution de classe:
def minimum Temps (même, s: str) -> Int:
n = len(s)
gauche _coût = 0
réponse = n

pour i, ch dans le(s) énuméré(s):
delete_middle = left_cost + (2 si ch == '1' autre 0)
trim_left = i + 1
gauche_cost = min(delete_middle, trim_left)

droite = n - 1 - i
réponse = min(réponse, gauche_cost + droite_trim)

réponse de retour
«» "

---

C++

'`cpp
solution de classe {
public:
Int minimum Temps(chaîne s) {
int n = s.size();
Int gauche Coût = 0;
réponse int = n; // pire cas

pour (int i = 0; i < n; ++i) {
int supprimer Milieu = gauche Coût + (s[i] == '1' ? 2 : 0);
l'extrémité intLeft = i + 1;
gauche Coût = min(supprimer) Moyenne, trimLeft);

Int droite Trim = n - 1 - i;
réponse = min(réponse, gauche) Coût + droitTrim);
}
réponse de retour;
}
};
«» "

Les trois compilent sous les derniers paramètres du compilateur LeetCode (Java 17, Python 3.10, C++17).

---

Article du blog : Le bon, le mauvais et le mauvais de LeetCode 2167

> **Références géographiques:**
> *LeetCode 2167, délai minimum pour enlever toutes les voitures contenant des marchandises illégales, Solution Java, solution Python, solution C++, algorithme, temps O(n), espace O(1), interview de codage, programmation dynamique, prép d'entrevue*

---

C'est pas vrai. Le bien – ce qui fait Ce problème un Masterclass

- **Simplicité de la déclaration** :
Une chaîne binaire, trois opérations, trouvez le coût minimum. Les règles sont faciles à comprendre.

- ** Solution linéaire élégante** :
La stratégie optimale est une seule passe – pas de boucles imbriquées, pas de structures de données supplémentaires.
Le calcul est étonnamment soigné: `min(gauche Coût + droiteTrim, i+1, gaucheCoût+2)».

- **O(1) Espace**:
De nombreux problèmes de LeetCode exigent des tables DP. Tu n'as besoin que de deux entiers.

- **Analogie du monde réel**:
Imaginez nettoyer un train. Ce modèle reflète la prise de décision réelle : couper des extrémités ou saisir au milieu. Les intervieweurs aiment les problèmes avec ce récit intuitif.

---

C'est vrai. Les mauvaises – pièges communs et idées fausses

Pourquoi ça arrive ?
- Oui.
**En supposant que vous devez supprimer tous les zéros d'abord** Autres
Autres **L'utilisation d'un tableau DP naïf de taille n**. Autres
**Ne pas manipuler `n-1-i` correctement** Autres
Autres **Cadre d'Edge `n = 1'** Trim = n - 1 - i '. Fonctionne pour un seul personnage. Autres
**Utiliser `i` au lieu de `i+1` pour le coût de la trim gauche**. Autres

C'est vrai. Les cas lugubres – les cas de bord qui emportent même les codes intelligents

- **Tous les zéros** :
Votre algorithme fonctionne toujours, mais vous devez vous assurer de ne pas doubler le coût de l'intermédiaire (il doit rester `0`). Les opérations mineures s'en occupent avec grâce.

- **Tous les "1"**:
L'algorithme décidera entre couper la chaîne entière ou supprimer chaque `1` individuellement. Les deux donnent le même coût `n` ou `2n`.
La comparaison min nous permet de choisir le moins cher.

- **Longueur 200 000**:
L'utilisation d'un tableau de longueur `n` (comme beaucoup de solutions DP) consommerait de la mémoire et ralentirait en raison de caches manquants. La solution O(1) est la seule voie viable.

---

####3--- - Comment parler de ce problème dans une entrevue

> **Démarrer avec l'histoire de "Pivot"**: Choisissez un endroit pour diviser le train. (en milliers de dollars)
> **Afficher les maths rapidement**: Jusqu'à l'index `i`, le coût est `min(prefixTrim, middleDeletes)`. L'ajout du suffixe donne le total. (en milliers de dollars)
> **Complexité des peines**: Un passage, une mémoire constante – parfait pour une entrevue de codage. (en milliers de dollars)

Si vous pouvez expliquer ce qui précède en 2 à 3 minutes, l'intervieweur sera impressionné.

---

Comment utiliser cette solution dans votre préparation d'entrevue

1. ** Pratique sur LeetCode** – copiez le code dans l'éditeur, lancez des cas de test, modifiez l'entrée.
2. **Enseignez l'idée** – expliquer l'algorithme à un ami ou dans une interview simulée cimentera votre compréhension.
3. **Explorer les variations** – modifier le coût de l'opération moyenne (par exemple, 3 au lieu de 2) et voir comment la formule s'adapte.
4. **Ajouter des points de discussion** – dans une interview future, vous pouvez faire apparaître les points bons, mauvais, laids comme une démonstration de compréhension profonde des problèmes.

---

La pensée finale

LeetCode 2167 prouve que *hard* ne signifie pas toujours *complexe*.
Un énoncé de problème clair + une observation intelligente peut donner une solution rapide et efficace en mémoire qui se sent toujours comme un processus décisionnel réel. Maîtrisez-le, et vous aurez un exemple brillant à montrer lors de votre prochain entretien technique.

Bon codage ! C'est ce qu'il a dit.

---