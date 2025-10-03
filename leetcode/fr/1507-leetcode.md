---
titre: LeetCode 1507. Date de la réforme
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Date de la réforme – Une entrevue complète Guide prêt
C++*

---

Table des matières

Secteur
- Oui.
Exposé du problème
Les cas d'idées et de bords de base
Approches de solution
Mise en œuvre Java Autres
Mise en œuvre de Python
Mise en œuvre C++ Autres
Temps et complexité spatiale
Les pièges communs et les odieux
Trucs d'entrevue et amélioration des compétences
Liste de contrôle du SEO et de l'emploi Autres

---

- Oui. 1. Déclaration de problème

> **LeetCode 1507 – Date de la réforme**
> **Difficulté:** Facile
> Vu une chaîne de dates dans la forme **`Jour Mois Année`** (par exemple, `"20th Oct 2052"`), convertir en **`AAAA-MM-JJ`**.
>
> - **Day** est une chaîne dans le set `{"1st", "2nd", ..., "31st"}`.
> - **Mois** est une abréviation: "{"Jan", "Feb", ..., "Dec"}".
> - **Année** est un entier dans `[1900, 2100]`.
>
> Les dates d'entrée sont toujours valides.

---

- Oui. 2. Idées de base et cas de bord

1. **Split** l'entrée sur les espaces → `[jour, mois, année]`.
2. **Strip** le suffixe ordinal (`st`, `nd`, `rd`, `th`) à partir du jour.
3. **Pad** une journée à un seul chiffre avec un zéro en tête.
4. **Abréviations de mois de carte** aux valeurs numériques (`Jan → 01`, ...).
5. **Concaténat** en "AAAA-MM-JJ".

*Les cas d'Edge sont minimes*:
- Jour 1st.
- Mois Jan → Jan.
- Des années restent intactes.
Le problème garantit la validité, donc nous n'avons pas besoin de traitement des erreurs.

---

- Oui. 3. Approches de solution

Pourquoi ça marche ?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Autres *Split + HashMap * * Carte directe, recherche O(1)
**Convertisseur / Enum**
**Regex**= Extrait de pièces dans un passage== O(n)==1=

Pour un *interview*, vous choisissez habituellement l'approche **Split + HashMap** – elle est concise et démontre clairement les compétences en manipulation de chaînes.

---

Mise en œuvre Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
public Chaîne reformatDate(Date de la chaîne) {
// 1. Diviser en [jour, mois, année]
Parties de chaînes = date.split(");

// 2. Cartographie mensuelle
Carte<String, String> moisMap = nouveau HashMap<>();
moisMap.put("Jan", "01");
moisMap.put("Feb", "02");
moisMap.put("Mar", "03");
moisMap.put("Apr", "04");
moisMap.put("mai", "05");
moisMap.put("Jun", "06");
moisMap.put("Jul", "07");
moisMap.put("Aug", "08");
moisMap.put("Sep", "09");
moisMap.put("Oct", "10");
moisMap.put("Nov", "11");
moisMap.put("Dec", "12");

// 3. Année d ' extraction
Année de chaîne = pièces[2];

// 4. Convertir mois
mois de chaîne = moisMap.get(parties[1]);

// 5. Jour propre (supprimer les 2 derniers caractères)
Jour de chaîne = parties[0].sous-chaîne(0, parties[0].longueur() - 2);
si (jour.longueur()] 1) jour = "0" + jour;

retour Chaîne.format("%s-%s-%s", année, mois, jour);
}
}
«» "

**Traitements clés pour les recruteurs:**
- Utilise **HashMap** pour les recherches O(1).
- Poignée à zéro.
- Pas de bibliothèque externe – pure Java SE.

---

- Oui. 5. Mise en œuvre de Python

'`python
Date(date: str) -> str:
# Split: [20ème, 'Oct', '2052']
jour_str, mois_str, année = date.split()

# Strip ordinal suffixe
jour = int(jour_str[:-2)] # p.ex. -> 20

# Carte mensuelle (index de liste 0 -> Janv.
mois_map = ["Jan", "Feb", "Mar", "Apr", "May", "Jun",
"Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
mois = mois_map.index(mois_str) + 1 # 1

# Format avec rembourrage zéro
retour f"{année}-{mois:02d}-{jour:02d}"
«» "

**Pourquoi Python fonctionne bien:**
- `int(day_str[:-2))` supprime automatiquement le suffixe.
- La liste `index()` indique le numéro du mois en O(12).
- `:02d` garde le code propre.

---

- Oui. 6. Mise en œuvre C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
reformater la chaîne Date(date de la chaîne) {
// Séparer manuellement la chaîne pour éviter le régex
ss(date);
jour de corde Str, moisStr, année;
ss >> jourStr >> moisStr >> année;

// Supprimer les deux derniers caractères (suffix ordinaire)
string day = dayStr.substr(0, dayStr.size() - 2);

// Cartographie mensuelle via tableau
vecteur<chaîne> mois = {
"Jan", "Feb", "Mar", "Apr", "May", "Jun",
"Jul", "Aug", "Sep", "Oct", "Nov", "Dec"
};
mois à chaîne;
pour (int i = 0; i < 12; ++i) {
si (mois [i] == moisStr) {
mois = (i < 9 ? "0" : "") + to_string(i + 1);
pause;
}
}

// S'assurer que le jour est deux chiffres
si (day.size()) == 1) jour = "0" + jour;

année de retour + "-" + mois + "-" + jour;
}
};
«» "

**Points saillants pour les recruteurs C++:**
- Utilise `stringstream` pour une séparation robuste.
- `vector<string>` pour la carte du mois – recherche O(1) par simple boucle.
- "à_chaîner" La concaténation des chaînes de caractères maintient le code lisible.

---

La complexité temporelle et spatiale

Langue Heure Espace
- C'est quoi ?
Java **O(1)** (ops de taille fixe, recherche de carte)
Python **O(1)**
* * * * * * * *

Toutes les solutions fonctionnent en temps constant parce que la longueur d'entrée est limitée (20 caractères).

---

- Oui. 8. Pièges communs et l'Ugly

Pourquoi c'est mauvais
- C'est quoi ?
**Déplacement de zéros en tête**="3e janv. 1999"=" → `"1999-01-3"=" (format défectueux)="Jour et mois avec `:02d` (Python) ou `String.format("%02d")=" (Java)
En supposant que tous les jours se terminent avec 2 chars; 11e versus 1st. Autres
**Case-sensitive mois map**.
**Utiliser le regex avec le rétrotraçage**
**Ignorer la plage d'année**= Pas besoin – entrée garantie valide==Toujours, des contrôles de santé peuvent être ajoutés pour le codage défensif==

- Oui. L'Ugly: Suringénierie

> Puis-je utiliser une bibliothèque d'analyse de date complète? (en milliers de dollars)
>
> **Réponse:** Pour ce problème LeetCode, un analyseur personnalisé **tiny** est préférable. L'utilisation de bibliothèques lourdes (par exemple, `java.time`, `datetime` avec `%b`) peut confondre les intervieweurs et encombrer votre solution. Gardez le **lean**.

---

- Oui. 9. Conseils d'entrevue et amélioration des compétences

1. **Clarifier le problème**: Confirmez le format d'entrée, demandez au sujet des cas bord.
2. ** Expliquez votre plan** : Description split → carte → format.
3. **Montrer les compromis**: Pourquoi vous avez choisi un hashmap vs enum vs regex.
4. **Écrire un code propre**: Utilisez des noms de variables significatifs (`dayStr`, `moisAbbrev`).
5. **Testez rapidement**: Exécutez quelques exemples sur un REPL pour valider.
6. **Parler du temps/de l'espace**: Toujours parler O(1) pour les intervieweurs.
7. **Extensibilité des peines**: Si vous deviez supporter des dates ISO complètes, comment modifieriez-vous?

---

# 10.

Pourquoi ça compte ?
C'est-à-dire
**Titre riche en mots clés** 1507 – Reformatat Date (en anglais seulement) attire les recruteurs qui cherchent le problème exact. Autres
**Description de la Meta**=Solve LeetCode Reformat Date en Java, Python et C++. Apprenez le code propre, l'analyse de complexité et les conseils d'entrevue. Autres
**En-têtes avec mots-clés** Autres
**Les blocs de code**=Les extraits de code en évidence rendent le poste écrémable pour les gestionnaires d'embauche. Autres
**Lien vers LeetCode** – montre l'authenticité. Autres
**Call-to-action**=Vous souhaitez maîtriser les défis algorithmiques? Suivez pour plus de solutions. Autres
**Partager sur LinkedIn / Twitter ** Les recruteurs parcourent souvent les blogs technologiques. Autres

---

### TL;DR

- **Problème**: Convertir `"Jour Mois Année"` → `"AAAA-MM-JJ"`.
- **Solution**: Split → suffixe de bande → carte mois → pad → rejoindre.
- **Langues**: Java, Python, C++.
- **Complexité**: temps O(1), espace O(1).
- **Interview**: Gardez-le propre, expliquez les compromis, testez rapidement.

Bon codage et bonne chance pour ce rôle d'ingénierie logicielle! C'est ce qu'il a dit