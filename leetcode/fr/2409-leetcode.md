---
titre: LeetCode 2409. Nombre de jours passés ensemble - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Comment résoudre le LeetCode 2409 – Compter les jours passés ensemble
C++ – Un guide complet + SEO-Optimized Blog Post**

---

Table des matières

Description de la section
C'est pas vrai.
Aperçu du problème Ce que le problème demande et pourquoi il importe pour l'interview prep
Une solution O(1) concise
Mise en œuvre Java Code complet, prêt à coller
Mise en œuvre de Python
C++ Mise en œuvre Code complet, prêt à coller
Bien, mal et mal Ce que vous devriez aimer, ce qu'il faut faire attention, et les parties sales
Trucs de référencement Comment cet article peut stimuler votre Linked Dans / GitHub trafic
Pourquoi ce problème est un must-solve pour les interviews technologiques

---

Aperçu du problème

> **LeetCode 2409 – Nombre de jours passés ensemble**
> *Difficulté: Facile*

Alice et Bob voyagent à Rome. Chacun a une date **start** et **end** (`"MM-JJ"`). Nous devons retourner le nombre de jours **les deux** sont à Rome ** simultanément**.

Principales contraintes :
- Toutes les dates sont dans une année **non-leap**.
- Les chaînes sont toujours valides "MM-JJ".
- Oui. La portée inclusive `[arrivée, congé]` est garantie.

> **Pourquoi ça compte**
> - Il teste **date arithmétique** sans compter sur des bibliothèques externes.
> - Cela vous oblige à penser en **espace entier** – convertir des mois/jours en une seule valeur de jour de l'année.
> - Il s'agit d'un problème classique d'intersection d'intervalle qui apparaît souvent dans les interviews.

---

# # # #=2 Aperçu algorithmique

1. **Comptes mensuels précalculés** – un tableau "moisJours = [0,31,59,90,...]" donne les jours cumulatifs *avant* chaque mois.
2. **Convertir une chaîne `"MM-DD"` à un jour de l'année**:
Texte
jourOfAnnée = moisJour[mois] + jour
«» "
3. **Trouver l'intersection des deux intervalles**:
Texte
début = max(startA, startB)
fin = min(endA, finB)
«» "
4. Si `end < start` → aucun chevauchement → réponse `0`.
Autre réponse `end - start + 1`.

Toutes les opérations sont **temps constant** – O(1) temps et O(1) espace.

---

- Oui. Mise en œuvre Java

"Java
***
* LeetCode 2409 – Nombre de jours passés ensemble
* Auteur: ChatGPT
* Date: 2025‐09‐24
*/
solution de classe publique {
// Excédents de jour avant chaque mois d'une année hors congé
finale statique privée JOURS_BEFORE_MONTH = {
0, // mannequin pour l'indexation à base de 1
0,/ Janv.
31 février
59, // mars
90, // avr
120, // mai
151, // juin
181, // Juil
212, // Août
243, // Sep
273, // Oct
304,/ nov.
334 // Déc
};

Nombre d'entrées publiques Ensemble des jours(Arrivée en chaîneAlice, Départ en chaîneAlice,
String arriveBob, String leaveBob) {
Int aStart = toDayOfYear(arrivéeAlice);
int aFin = àJour de l'année (leaveAlice);
int bStart = àJour de l'année(arrivezBob);
int bEnd = jusqu'au jour de l'année (leaveBob);

début int = Math.max(aStart, bStart);
int end = Math.min(aEnd, bEnd);

retour Math.max(0, fin - début + 1);
}

/** Convertir "MM-JJ" → jour de l'année (1‐basé). */
Int privé jusqu'au jour de l'année (date de publication) {
mois int = Integer.parseInt(date.substring(0, 2));
int day = Integer.parseInt(date.substring(3, 5));
retour JOURS_BEFORE_MONTH[mois] + jour;
}

// --- Harnais d'essai (facultatif) ---
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.countDaysTogether("08-15", "08-18", "08-16", "08-19"); // 3
Système.out.println(s.countDaysTogether("10-01", "10-31", "11-01", "12-31"); // 0
}
}
«» "

> **Pourquoi ce code Java est propre**
> - Pas de bibliothèques externes (`java.time`) pour le garder.
> - le tableau `privé statique final` garantit la compilation de l'espace constant temps.
> - `Math.max/min` poignées élégantement intersection vide.

---

Mise en œuvre de Python

'`python
# LeetCode 2409 – Nombre de jours passés ensemble
♪ Auteur: ChatGPT
Date: 2025-09-24

Solution de classe:
# jours cumulatifs avant chaque mois (1 base)
JOURS_BEFORE_MONTH = [0, 0, 31, 59, 90, 120, 151,
181, 212, 243, 273, 304, 334]

Dénombrement JoursEnsemble(s, arrivezAlice: str, leaveAlice: str,
arriveBob: str, leaveBob: str) -> Int:
a_start = self.to_day_of_year(arrivéeAlice)
a_end = self.to_day_of_year(leaveAlice)
b_start = self.to_day_of_year(arrivéeBob)
b_end = self.to_day_of_year(leaveBob)

début = max(a_start, b_start)
fin = min(a_end, b_end)

retour max(0, fin - début + 1)

@staticmethod
def to_day_of_year(date: str) -> Int:
mois, jour = carte(int, date.split('-'))
Return Solution.DAYS_BEFORE_MONTH[mois] + jour


♪ --- Exemple d'utilisation (ne faisant pas partie du LeetCode) ---
si __nom__ == "__main__" :
sol = Solution()
imprimer(sol.countDaysTogether("08-15", "08-18", "08-16, "08-19") # 3
print(sol.countDaysTogether("10-01", "10-31", "11-01", "12-31") # 0
«» "

> ** Faits saillants du python* *
> - `split('-')` est concis et lisible.
> - `@staticmethod` garde l'aide logique autonome.
> - Pas besoin de `datetime` – garde l'exécution minimale.

---

C++ Mise en œuvre

'`cpp
// LeetCode 2409 – Nombre de jours passés ensemble
// Auteur: ChatGPT
Date: 2025-09-24

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
particulier:
jours statiques de constexpr AvantMois[13] = {
0, // mannequin (1-base d'indice)
0,/ Janv.
31 février
59, // mars
90, // avr
120, // mai
151, // juin
181, // Juil
212, // Août
243, // Sep
273, // Oct
304,/ nov.
334 // Déc
};

int toDayOfYear(chaîne de caractères et date de const) {
mois int = stoi(date.substr(0, 2));
int jour = stoi(date.substr(3, 2));
jours de retourAvant le mois + jour;
}

public:
nombre d'int Jours ensemble(la chaîne arrive) Alice, laisse la corde. Alice,
chaîne arrive Bob, la corde quitte Bob) {
Int aStart = toDayOfYear(arrivéeAlice);
int aFin = àJour de l'année (leaveAlice);
int bStart = àJour de l'année(arrivezBob);
int bEnd = jusqu'au jour de l'année (leaveBob);

démarrage int = max(aStart, bStart);
Int end = min(aEnd, bEnd);

retour max(0, fin - début + 1);
}
};

// --- Harnais d'essai facultatif ---
Int main() {
Solution s;
Cout << s.countDaysTogether("08-15", "08-18", "08-16", "08-19") << endl; // 3
<< s.countDaysTogether("10-01", "10-31", "11-01", "12-31") << endl; // 0
}
«» "

> **C++ Notes**
> - Utilise `constexpr` pour compiler les constantes de temps.
> - `substr` est sûr car le format d'entrée est corrigé.
> - Pas de conteneurs STL au-delà de `<string>` et `<bits/stdc++.h>` pour la brièveté.

---

# # # 6

Catégorie de ce qu'il y a de grand
-- -- -- -- -- -- -- -- -- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Bonne** Pas de bibliothèques lourdes<br>• Fonctionne avec toutes les dates valides. Fonctionne même si les plages se touchent aux paramètres
• Aucun pour un problème simple • Si vous utilisez accidentellement un décalage de l'année bissextile, vous obtiendrez de mauvaises réponses<br>• Oublier les «+1» inclus donne des erreurs hors-par-un
**Les décalages mensuels du codage dur peuvent être sensibles aux erreurs (valeurs mal typées)<br>• Remise en œuvre de l'analyse de la date au lieu d'utiliser `datetime` dans Python peut se sentir redondante<br>• Dans C++, vous pouvez oublier `constexpr` et finir avec les requêtes de tableau d'exécution.

**Ligne de bottom:** Le problème est intentionnellement trivial mais vérifie votre capacité à gérer les intervalles proprement. Gardez la logique de conversion de date compacte, évitez les bibliothèques lourdes et testez les cas de bord (même jour, aucun chevauchement, chevauchement complet).

---

## 7-SEO Conseils – Comment ce blog peut stimuler votre recherche d'emploi

Mise en œuvre de la stratégie
- C'est quoi ?
**Titre riche en mots-clés** (Java, Python, C++)
**En-têtes avec des mots-clés**=H2:=Java Solution pour LeetCode 2409=H2:=Python Implementation==H2:=C++ Code==
**Description de la meta**=Découvrez comment résoudre LeetCode 2409 – Compter les jours passés ensemble en Java, Python et C++. Solution O(1) rapide et code prêt à l'entrevue. Autres
**Liens internes**= Lien vers votre repo GitHub, votre profil LeetCode ou d'autres messages d'algorithmes. Autres
**Utiliser les étiquettes d'entretien**= Mettre l'accent sur la question d'entrevue facile, l'intersection interval, la manipulation de date. Autres
**Contient des extraits de code**= Utilisez des blocs de code Markdown pour améliorer la lisibilité tant pour les humains que pour les moteurs de recherche. Autres
**Engagement** Vous avez déjà résolu ça ? Partagez vos astuces dans les commentaires. Autres

> **Résultat:** L'article sera classé pour les requêtes comme *=LeetCode 2409 solution Java=* ou *== nombre de jours passés ensemble code===*, conduisant le trafic à votre profil et faisant des recruteurs repérer vos compétences de résolution de problèmes.

---

- Oui. A emporter

- **L'essence du problème**: Trouver l'intersection de deux séries de dates dans une année sans congé.
- **Approche optimale**: Convertir `"MM-JJ"` en un seul entier de jour de l'année → O(1).
- ** Mise en oeuvre en plusieurs langues** : Java, Python, C++ partagent tous la même logique ; il suffit d'adapter la syntaxe.
- **Valeur d'entrevue**: Montre la maîtrise de l'arithmétique des intervalles, des solutions à temps constant et des pratiques de codage propres.

> Soyez prêt à expliquer votre logique en moins de 5 minutes – c'est comment les intervieweurs testent vos compétences en communication.

Joyeux codage, et que ces portes d'entrevue s'ouvrent pour vous! C'est ce qu'il a dit