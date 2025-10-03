---
titre: LeetCode 3136. Mot valide -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3136. Mot valide – Java / Python / C++ Solutions + Blog
*(Tout ce dont vous avez besoin pour as ce problème LeetCode et atterrir votre travail de rêve.) *

---

Récapitulation des problèmes (Code de débit 3136)

Exigence Ce que ça veut dire
C'est quoi ?
**Longueur**
**Caractéristiques**= Seulement les chiffres `0‐9' ou les lettres anglaises (en haut ou en bas)=
Au moins une voyelle (`a e i o u`, insensible à la casse) **et** au moins une consonne (toute autre lettre)

Retourner `true` si la chaîne satisfait aux règles *all*, sinon `false`.

---

Une idée de solution

1. ** Sortie précoce** – si longueur < 3 → `faux`.
2. Scanner la chaîne une fois :
* Si un personnage est une lettre → vérifier si il est une voyelle ou consonne.
* Si c'est un chiffre → ok.
* Tout autre symbole → `faux` immédiatement.
3. Après la boucle, assurez-vous de voir ** au moins une voyelle** et ** au moins une consonne**.
4. Complexité: **O(n)** temps, **O(1)** espace.

Il s'agit d'un algorithme monopass sans structures de données supplémentaires – parfait pour les paramètres d'entrevue.

---

- Oui. Code

#### 3.1 Java

"Java
// 3136. Mot valide
solution de classe publique {
Le booléen public est Valid (mot en boucle) {
si (mot.longueur) < 3) retourner faux;

booléen hasVowel = faux;
booléen aConsonant = faux;
pour (charc : mot.toCharArray()) {
si [Caracter.isLettre(c)] {
si ("aeiouAEIOU".indexOf(c) >= 0) {
hasVowel = true;
} autre {
hasConsonant = true;
}
} sinon si (!Caracter.isDigit(c)) {
retourner faux; // symbole illégal
}
}
retour hasVowel && hasConsonant;
}
}
«» "

3.2 Python

'`python
# 3136. Mot valide
Solution de classe:
def isValid(self, mot: str) -> C'est vrai.
si len(mot) < 3:
Retour Faux

voyelles = ensemble('aiouAEIOU')
has_vowel = has_consonant = Faux

pour ch en mot:
si ch.isalpha():
si ch en voyelles:
has_vowel = Vrai
Sinon:
has_consonant = Vrai
elif pas ch.isdigit():
Retour Faux

return has_vowel et has_consonant
«» "

### 3.3 C++

'`cpp
// 3136. Mot valide
solution de classe {
public:
bool isValid(string word) {
si (word.size() < 3) retourner faux;

bool hasVowel = false, hasConsonant = false;
const string voyelles = "aeiouAEIOU";

pour (charc : mot) {
si [isalpha(c)] {
if (vowels.find(c) != string::npos) hasVowel = true;
sinon aConsonant = true;
} sinon si (!isdigit(c)) {
retourner faux; // symbole illégal
}
}
retour hasVowel && hasConsonant;
}
};
«» "

> Les trois implémentations fonctionnent dans **O(n)** temps, **O(1)** espace.

---

- Oui. Billet de blog – Le bon, le mauvais, et le mauvais de LeetCode 3136: Mot valide

### 4.1 Titre (optimisé par le référencement)

> (LeetCode 3136) – Java, Python, C++ Solutions + Conseils d'entrevue pour votre prochain travail**

4.2 Introduction

Lorsque vous frappez le problème LeetCodes *=Valid Word=* (3136), vous entrez dans une question d'entrevue classique *string validation*. Il est facile à résoudre, mais il vous enseigne les fondamentaux de l'analyse, des contrôles des frontières et des sorties précoces – compétences dont chaque ingénieur logiciel a besoin.

Dans ce billet, nous passerons par:

1. **Le bon** – pourquoi ce problème est un *doit être résolu* pour les entrevues de codage.
2. **Les mauvais** – pièges communs et comment les éviter.
3. **La laide** – sur-ingénierie (p. ex., regex) et pourquoi c'est une mauvaise idée pour les entrevues.

À la fin, vous aurez une solution propre et prête à la production en Java, Python et C++, ainsi que des points de conversation de style interview pour impressionner les gestionnaires d'embauche.

### 4.3 Énoncé du problème (récapitulatif rapide)

- Longueur minimale 3
- Seulement chiffres ou lettres anglaises
- Doit contenir au moins une voyelle * et* une consonne

Retour `true` si toutes les conditions sont remplies.

4.4 Les bonnes – Pourquoi Ce problème est important

Pourquoi il est précieux
-- -- -- -- -- -- -- ------------------
**Scannage mono-pass**= Démontre l'efficacité algorithmique – temps O(n). Autres
**Classification des caractéristiques** Autres
**Début de la sortie** Autres
**Connaissance de l'Edge** Autres

4.5 Les mauvaises – erreurs courantes

Pourquoi ça fait mal
- C'est quoi ?
Autres Oubliant le contrôle de la longueur, valide incorrectement si (len < 3) retourner faux;
Utiliser un ensemble insensible à la casse ou « toLowerCase()» Autres
Autres Autoriser n'importe quel symbole Failes $3 $3 $ Rejeter explicitement tout ce qui n'est pas un chiffre ou une lettre
Dénommer les chiffres comme consonnes Déclassifie -123abc-

#### 4.6 L'Ugly – Sur-Ingénierie avec Regex

Une solution régex seule peut paraître compacte :

'`python
[bcdfghjklmnpqrstvwxyzBCDFGHJKLMNPQRSTVWXYZ])[0-9A-Za-z]{3,}', mot)
«» "

Mais dans une interview :

- **Readability souffre** – les recruteurs pourraient ne pas le comprendre rapidement.
- **Performance** – les moteurs régex peuvent être plus lents pour les longues cordes.
- **Le débogage est difficile** – si le modèle échoue, vous devrez le réécrire.

S'en tenir à l'approche simple et impérative ci-dessus, sauf si l'intervieweur demande explicitement un régex.

4.7 Complexité temporelle et spatiale

- **Heure:** O(n) – un passage sur la chaîne.
- **Espace:** O(1) – seulement quelques drapeaux booléens.

4.8 Cas d'essai (Mini-Test Suite)

Valeur prévue Raison
C'est quoi, ça ?
""234Adas""""true"" Valable – chiffres + voyelles + consonnes Autres
Trop court, pas de voyelle
"a3$e" "false"" Contient "$" (symbole illégal)
"AEIOU123" "False" "Pas de consonnes"
Pas de voyelles
« aB1c » « vrai » Mélange de cas, toutes les règles satisfaites

###4.9 Conseils d'entrevue

1. **Expliquez votre approche** – Mentionnez la sortie anticipée, le laissez-passer unique et pourquoi vous comptez les voyelles/consonnes séparément.
2. **Discus cas bord** – Mettre en évidence la longueur, la manipulation des symboles et le cas mixte.
3. **Complexité des peines** – Montre que tu tiens à l'efficacité.
4. **Demander des éclaircissements** – par exemple, considérons-nous une voyelle? (en milliers de dollars)
5. **Afficher votre code** – Partagez l'extrait Java/Python/C++ ; soyez prêt à refactorer sur place.

4.10 Conclusion

Le problème *Valid Word* est une base d'entrevue petite mais puissante. Ça vous oblige à penser à :

- **Validation d'entrée* *
- **Classification des caractères**
- **Conditions limites**

Avec les solutions ci-dessus et la stratégie d'entretien esquissée, vous êtes prêt à affronter 3136 avec confiance – et impressionner les recruteurs avec un code clair et efficace. Bonne chance pour ce travail de rêve !

---

**Vous avez d'autres défis à relever par LeetCode? * *
Laissez un commentaire ou envoyez-moi un e-mail – Je vais vous aider à résoudre le prochain problème!