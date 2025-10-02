---
titre: LeetCode 2224. Nombre minimum d'opérations pour convertir le temps -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions de code

Voici des implémentations propres et prêtes à la production de **LeetCode 2224 – Nombre minimum d'opérations pour convertir le temps** en **Java, Python et C++**.
Chaque solution suit la même stratégie gourmande : convertir les deux chaînes en minutes et soustraire à plusieurs reprises le plus grand incrément possible (60 → 15 → 5 → 1) jusqu'à ce que le temps `current` corresponde `correcte`.
La complexité temporelle est **O(1)** (la boucle tourne au plus quelques dizaines d'itérations) et la complexité de l'espace est **O(1)**.

---

### 1.1 Java – `Solution.java "

"Java
// 2025‐09‐23 – Code Leet 2224
// O(1) temps et espace – cupidité gourmande
solution de classe publique {
public int converti Heure(String current, String correct) {
int cur = toMinutes(current);
cible int = toMinutes(correcte);
Int ops = 0;
int[] inc = {60, 15, 5, 1};

pour (int d : inc) {
ops += (cible - cur) / d;
cur += ((cible - cur) / d) * d;
}
les opérations de retour;
}

Int privé à Minutes(String t) {
Parties de chaînes = t.split(":");
retour Integer.parseInt(parties[0]) * 60 + Integer.parseInt(parties[1]);
}
}
«» "

---

### 1.2 Python – `solution.py "

'`python
No 2025‐09‐23 – Code Leet 2224
# O(1) solution avec soustraction gourmande

def convert_time(current: str, correct: str) -> Int:
cur = _to_minutes(current)
cible = _à_minutes(correct)

ops = 0
pour inc in (60, 15, 5, 1):
delta = cible - cur
ops += delta // inc
* inc
retour ops

def _to_minutes(t: str) -> Int:
h, m = carte(int, t.split(":"))
retour h * 60 + m
«» "

---

### 1.3 C++ – `solution.cpp "

'`cpp
// 2025‐09‐23 – Code Leet 2224
// Greedy, O(1) temps, O(1) espace

#incluez <string>
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
convertisseur int Time(string current, chaîne correcte) {
int cur = toMinutes(current);
cible int = toMinutes(correcte);
Int ops = 0;
vecteur<int> inc = {60, 15, 5, 1};

pour (int d : inc) {
int delta = cible - cur;
ops += delta / d;
cr += (delta / d) * d;
}
les opérations de retour;
}

particulier:
int toMinutes(const string &t) {
int h = stoi(t.substr(0, 2));
int m = stoi(t.substr(3, 2));
retour h * 60 + m;
}
};
«» "

---

- Oui. 2. Article de blog – Le Bon, le Mauvais, et l'Ugly de LeetCode 2224

> **Titre**: *Le bon, le mauvais, et le mauvais de LeetCode 2224 – Conversion du temps en minutes (prép. d'entrevue d'embauche)*

> **Meta Description**: Master LeetCode 2224 - Nombre minimum d'opérations pour convertir le temps avec des tours avides, des pièges et un guide étape par étape. Boostez votre score d'entrevue de codage et atterrissez ce travail de rêve.

> **Mots clés**: LeetCode 2224, Nombre minimum d'opérations pour convertir le temps, entretien de codage, algorithme avide, problème de conversion du temps, code d'entretien d'emploi, solutions Python Java C++, préparation d'entrevue, pensée algorithmique.

---

2.1 Introduction

Dans le monde du codage des interviews, le problème **LeetCode 2224** – *Nombre minimal d'opérations pour convertir le temps* – est un exemple classique de la façon dont une question apparemment simple peut tester votre compréhension des algorithmes **Greedy**, de l'analyse du temps-complexité** et de la prise de conscience des cas**.

Que vous soyez un développeur junior ou un ingénieur chevronné, cracher ce problème démontre non seulement la fluidité algorithmique, mais montre également votre capacité à écrire du code propre et de qualité de production en plusieurs langues. Ci-dessous nous allons marcher à travers le **bon** (pourquoi il est un exercice d'entrevue précieux), le **mauvais** (pièges communs et pourquoi les solutions naïves échouent), et le **ugly** (les pièges subtils qui voyagent même les candidats expérimentés).

---

2.2 Les bonnes – Pourquoi Ce problème est important

Pourquoi ça aide dans les entrevues
- C'est quoi ?
**Greedy Insight**Le problème vous oblige à penser en termes de . C'est une caractéristique de nombreuses questions d'entrevue. Autres
**Constant-Time Raisonnement**Vous devez prouver que la solution fonctionne dans *O(1)*, pas *O(n)*. Comprendre pourquoi un nombre constant d'itérations suffit est crucial pour la rigueur algorithmique. Autres
**Multilinguisme de la mise en œuvre**** Démontrer la même logique dans **Java, Python et C++** montre la polyvalence – quelque chose que les recruteurs aiment. Autres
Autres **Connaissance des cas**= Les temps à la limite (p. ex. 23:59 à 23:59) ou les incréments minimaux (1 minute) testent votre capacité à gérer correctement les cas de bord. Autres
Autres **Clear Code Style**La solution est brièveté (souvent de moins de 10 lignes) met en évidence des pratiques de code propres et réduit les bugs. Autres

---

2.3 Les mauvaises – erreurs courantes

Pourquoi il fait défaut
C'est quoi ?
**Simuler toutes les minutes**=La boucle minute par minute conduit à *O(Δt)* temps, ce qui est inutile et lent pour les grandes différences de temps. Autres
**Utiliser des astuces de point flottant ou de modulo** Autres
**Codage dur incréments dans l'ordre inverse**. Certains candidats commencent par 1 min et ajoutent, ce qui fonctionne mais est moins efficace et plus difficile à justifier. Autres
**Ignorer le courant <= correct**En supposant que le courant peut être plus grand que correct peut conduire à des boucles infinies ou de mauvaises réponses. Autres

---

2.4 Les cas d'indulgence – bord épineux

1. **Différence de zéro* *
*Input*: `current = "12:00"`, `correct = "12:00"` → Réponse: `0`
Oublier de gérer ce cas peut causer la division par zéro ou itérations supplémentaires.

2. ** Grandes différences Heures de passage* *
*Input*: `current = "00:00"`, `corrige = "23:59"` → Doit utiliser 23 incréments complets de 60 minutes, puis les minutes restantes.

3. **Trainer des zéros dans les cordes* *
`current = "04:05"` → Assurez-vous que la logique `split` ou substring gère correctement les zéros.

4. **Modèles de temps locaux-dépendants* *
Certaines langues (p. ex. Javas `DateTimeFormatter`) peuvent parse `"HH:mm"` différemment si le local est défini à autre chose. Toujours utiliser l'analyse explicite.

---

### 2.5 Solution étape par étape

1. **Parcourir les deux temps dans les minutes* *
minutes = heures * 60 + minutes "

2. ** Calculer la différence**
`delta = correctMinutes - courants "

3. **Réduction du nombre de naissances**
Pour chaque incrément `d` dans `[60, 15, 5, 1]`:
- `ops += delta / d "
- `delta -= (delta / d) * d "

4. **Retour `ops`**

> **Pourquoi ça marche**
> Parce que chaque opération peut ajouter *exactement* 60, 15, 5 ou 1 minute, le choix gourmand de la plus grande étape possible donne toujours une solution optimale. C'est un problème classique de changement de monnaie avec les dénominations de pièces canoniques.

---

2.6 Échantillons de code – propres et réutilisables

(Voir Section 1 pour le code complet en Java, Python et C++.)
**Astuce**: Enveloppez la logique d'analyse dans une méthode d'aide pour éviter les répétitions dans les langues.

---

2.7 Réflexions finales : Transformer le problème en une compétence gagnante

- ** Variantes de pratique** : Essayez de changer les incréments autorisés en `{10, 20, 30}` et réécrivez l'algorithme avide.
- **Tests de l'unité**: Écrire des cas d'essai pour tous les cas de bord; cela démontre l'attention portée aux détails.
- ** Expliquez votre raison** : Dans une interview, racontez pourquoi l'algorithme avide est optimal (système de pièces canoniques).
- **Afficher la complexité du temps**: soulignez que la boucle tourne au plus 4 itérations – une quantité constante – donc la solution est *O(1)*.

En maîtrisant LeetCode 2224, vous ne résolvez pas seulement un puzzle de conversion du temps soigné, mais vous équipez également d'une stratégie d'entrevue portable : Quand vous pouvez prendre la plus grande étape qui ne dépasse pas, faites-le.

Bonne chance pour vos interviews de codage – et peut-être que la différence de minute ne vous gêne jamais!

---

#### 2.8 SEO— Fermeture prête

Si vous préparez des interviews de codage, concentrez-vous sur la maîtrise des algorithmes gourmands comme celui de **LeetCode 2224**. Nos solutions propres Java, Python et C++ vous donnent le code exact que les recruteurs d'extraits de code aiment. Utilisez le blog pour stimuler votre marque personnelle – partagez-le sur LinkedIn, GitHub et Medium.
Rappelez-vous: chaque minute que vous investissez dans la pratique est un pas plus près de ce travail de rêve. Bon codage !