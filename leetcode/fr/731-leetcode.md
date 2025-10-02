---
titre: LeetCode 731. Mon calendrier II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 731 – Mon calendrier II
**Solutions en Java, Python & C++ + une interview-blog conviviale au référencement* *

---

## Description du problème (LeetCode 731)

> *Vous devez implémenter un calendrier qui peut réserver des événements aussi longtemps qu'aucun **trois** événements se chevauchent en même temps.
> Les événements sont des intervalles demi-ouverts \([start, fin)\). Retourner `true` si l'événement peut être ajouté, sinon `faux`. *

> **Constraints**
> * `0 ≤ début < fin ≤ 10^9`
> * ≤ 1000 `livre()` appels

---

Idée clé

Maintenir **deux collections**:

1. **Tous les événements réservés** – pour détecter tout chevauchement *nouveau*.
2. ** Intervalles à double réservation** – intervalles déjà couverts par deux événements.
Si un nouvel événement chevauche l'un de ces événements, une réservation **triple** se produira → rejeter.

La solution classique "Two-list" fonctionne dans **O(N)** par `book()` (N = nombre d'événements existants).
Une approche plus efficace utilise une *sweep‐line* (`TreeMap` / `std::map`) et fonctionne en **O(log N)** par appel.

Voici trois implémentations idiomatiques (Java, Python, C++) qui utilisent la stratégie *deux-liste* pour la clarté.

---

Mise en œuvre Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

événement de classe {
int début, fin;
Événement(int s, int e) { début = s; fin = e; }
}

cours MyCalendar Deux {

liste finale privée<événement> réservations = nouvelle liste d'array<>();
liste finale privée<événement> chevauchements = nouvelle liste de distribution<>();

public MyCalendar Deux() {}

livre public booléen(int start, int end) {
// 1) Vérifier la triple réservation
pour (Evénement : chevauchements) {
si (estOverlap(e, début, fin)) retourner faux;
}

// 2) Enregistrer de nouvelles doubles réservations
pour (événement e : réservations) {
si (estOverlap(e, début, fin)) {
chevauchements.add(nouveau événement(
Math.max(e.démarrer, commencer),
Math.min(e.end, fin)
));
}
}

// 3) Persistez le nouvel événement
réservation.add(nouveau événement(début, fin));
retour vrai;
}

booléen privé estOverlap (événement e, int s, int t) {
retourner Math.max(e.start, s) < Math.min(e.end, t);
}
}
«» "

> **Complexités**
> • **Heure:** `O(n)` par `book()` (scan linéaire des pires cas).
> **Espace:** `O(n)` pour les deux listes.

---

Mise en œuvre de Python

'`python
événement:
__slots__ = ("s", "e")
def __init_(self, s, e):
Self.s, self.e = s, e

cours MyCalendar Deux :
def _init_(self):
auto-réservation = [] # Tous les événements
self.overlaps = [] # intervalles de double réservation

def book(self, start: int, fin: int) -> C'est vrai.
# 1) Garde à trois réservations
pour moi. chevauchements:
si max(e, début) < min(e, fin):
Retour Faux

2) Construire de nouveaux chevauchements
pour moi. réservations:
si max(e, début) < min(e, fin):
auto.overlaps.append(événement(
max(e.s, début),
min(e, fin)
))

3) Persistez le nouvel événement
auto.bookings.append(Event(start, fin))
retour Vrai
«» "

> **Complexités**
> **Heure:** `O(n)` par appel.
> **Espace:** "O(n)".

---

C++ Mise en œuvre

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

struct Event {
e);
Événement(int ss, int ee) : s(ss), e(ee) {}
};

cours MyCalendar Deux {
les réservations vectorielles<événement>;
le vecteur<événement> se chevauche;

bool isOverlap(const Event &e, int s, int t) const {
retour max(e, s) < min(e, t);
}
public:
Mon calendrier Deux() = par défaut;

bool book(int start, int end) {
// 1) Garde à trois réservations
pour (const auto& e : chevauchements)
si (estOverlap(e, début, fin)) retourner faux;

// 2) Enregistrer les nouveaux chevauchements
pour (const auto& e : réservations)
si (estOverlap(e, début, fin))
chevauchements.emplace_back(
max(e.s, début),
min(e, fin)
);

// 3) Persistez le nouvel événement
reservations.emplace_back(départ, fin);
retour vrai;
}
};
«» "

> **Complexités**
> **Heure:** `O(n)` par `book()`.
> **Espace:** "O(n)".

---

Article de blog – Le bon, le mauvais, et le mauvais de mon calendrier II

> **Titre:** *LeetCode 731 – Mon calendrier II: Une plongée profonde dans le calendrier interval, la triple-réservation et votre prochaine entrevue de codage*

> **Meta Description:** Master LeetCode 731 avec des solutions Java, Python et C++. Découvrez les compromis entre deux listes et la ligne de balayage, optimisez votre algorithme et agréez votre entrevue d'ingénierie logicielle.

---

C'est pas vrai. Pourquoi ce problème fait-il des ravages?

- **Fonctionnalité réelle:** Calendrier, systèmes de réservation et allocation des ressources.
- **Profondeur algorithmique:** Détection du chevauchement intervalle, comptage des événements, choix de la structure des données.
- **Tarif de popularité :** Foire aux questions sur les interviews d'entreprises technologiques (Google, Amazon, Microsoft).

---

- Oui. Le Bon – Ce qui fonctionne

Aspect Explication
C'est pas vrai.
**Simplicité**La solution à deux listes est intuitive : une liste pour toutes les réservations, une autre pour les chevauchements. Aucune bibliothèque externe n'est requise. Autres
**Complexité déterministe** Avec des réservations ≤ 1000, un 'O(n)' scanner par appel est assez rapide. Autres
Autres Les intervalles demi-ouverts évitent les écueils comme «[10,20]» et «[20,30]» considérés comme se chevauchant. Autres

---

C'est vrai. Le mauvais – où il peut glisser

Numéro Description
C'est quoi ?
**Scan linéaire**= À mesure que les réservations augmentent, chaque `book()` devient plus lent (`O(n)`). Pour d'énormes ensembles de données (millions d'événements), c'est inacceptable. Autres
**Duplicate Overlaps**La démarche naïve peut stocker plusieurs fois le même segment à double réservation (p. ex. si trois paires distinctes partagent le même chevauchement). C'est toujours correct, mais gaspillé. Autres
**La difficulté à la raison à propos**=Le débogage des boucles imbriquées peut être source de confusion pour les candidats à l'entrevue sous pression temporelle. Autres

---

C'est pas vrai. Les odieux – Gotchas et idées fausses

1. **Triple-Reservation de mauvaise identification**
*De nombreux candidats ne vérifient à tort que les "réservations" pour les chevauchements, en supposant que deux événements ne se chevauchent jamais. Ceci manque la liste de chevauchement *double* et accepte une triple réservation. *

2. **L'utilisation des ensembles d'intervalles**
*Un motif commun mais buggy: stocker les intervalles dans un `HashSet` et tester le chevauchement par itération. Il ignore l'état déjà double-réservé. *

3. ** Erreurs de mise en œuvre de la ligne de balayage**
*La solution `TreeMap`/`std::map` nécessite une logique d'accroissement/de déclin soignée. Les erreurs hors-par-une sur la limite demi-ouverte sont fréquentes. Un seul `+1` manquant peut faire de votre algorithme une erreur. *

---

####4-Sweep-Line (TreeMap / md::map) – L'alternative élégante

"Java
// Esquisse Java (O(log n) par appel)
cours MyCalendar Deux {
carte finale privée TreeMap<entier, Integer> carte = nouveau TreeMap<>();
livre public booléen(int start, int end) {
map.put(début, map.getOrDefault(début, 0) + 1);
map.put(end, map.getOrDefault(end, 0) - 1);

Int concurrent = 0;
pour (int v : map.values()) {
simultanément += v;
si (concurrent > 2) { // triple réservation détectée
// Retour en arrière
map.put(départ, map.get(départ) - 1);
si (map.get(start)) == 0) map.supprimer(démarrer);
la carte.put(fin, map.get(fin) + 1);
si (map.get(end)) == 0) map.supprimer(enfin);
retourner faux;
}
}
retour vrai;
}
}
«» "

*Avantages:* `O(log n)` par appel, aucun double chevauchement, parfait pour les intervieweurs qui se soucient de l'optimalité asymptotique.

---

#### 5=" Échanges sur le temps et l'espace

Démarche Temps par `book()` Espacement Quand utiliser
- C'est quoi ?
"O(n)"
"O(log n)" Les gros ensembles de données, les intervieweurs favorisent les limites asymptotiques

---

- Oui. Essai Cheat cas Feuille

Autres Résultats attendus
-- -- -- -- -- --
`book(10,20)` → `true`
`book(50,60)` → `true`
`book(10,40)` → `true`
`book(5,15)` → `false`=Créer une triple réservation avec `[10,20]` & `[10,40]`=
`book(25,55)` → `true`

> *Astuce:* Inclure toujours les cas de bord où les intervalles se touchent mais ne se chevauchent pas (`[20,30]` après `[10,20]`).

---

Liste de contrôle de l'entrevue

1. ** Expliquez votre algorithme** – deux listes ou ligne de balayage, selon votre code.
2. ** État du temps et de l'espace** – les intervieweurs adorent voir la complexité à l'avance.
3. **Boîtes de bord** – intervalles demi-ouverts, événements consécutifs.
4. **Afficher une piste sèche** – marcher à travers un petit exemple sur le tableau blanc.
5. **Soyez prêt pour les variations** – et si la limite était de 10^5 réservations? Utilisez la ligne de balayage.

---

- Oui. Pensée finale – *Job-Interview Takeaway*

Une solution propre et bien commentée qui couvre les cas de bord, explique la complexité, et peut être facilement porté entre Java, Python, et C++ démontre une pensée algorithmique candidate et la discipline de codage – exactement ce que les recruteurs recherchent.

> Si vous pouvez surmonter ce problème, expliquer pourquoi vous avez choisi une structure de données particulière, et discuter des compromis, vous impressionnerez les intervieweurs dans n'importe quelle grande entreprise technologique.

---

Bonus : Visite vidéo

*(Dans le blog réel vous avez intégré un lien YouTube ou GIF courte)*

> Regardez-moi résoudre LeetCode 731 en 5 minutes. Je vais montrer l'approche à deux listes, une variante de ligne de balayage, et mettre en évidence les pièges communs. Consultez la vidéo complète ici: <https://youtu.be/YourVideoID>.

---

Liste de contrôle du référencement

- **Mots-clés principaux:** *LeetCode 731*, *Mon calendrier II*, *Mon calendrier Deux*, *horaire d'intervalle*, * réservation triple*
- **Mots-clés secondaires:** * Solution Java*, * Solution Python*, * Solution C++*, *Algorithme d'entrevue*, *Entretien de l'ingénieur logiciel*, *Questions d'entrevue de codage*, *Préparation de l'entrevue d'embauche*
- **Traitements (H1, H2, H3)** avec aspersion de mots clés.
- **Alt-text pour les extraits de code**: *Java MyCalendar Mise en œuvre
- **Liens internes:** Lire notre solution de balayage → lien vers l'article suivant.
- **Meta tags**: Titre, description, liste de mots clés.

---

Enveloppe

- **Trois solutions propres** dans les langues d'entretien les plus populaires.
- **Un article complet, optimisé par le SEO** qui couvre la pertinence du problème, les choix de conception et les conseils d'entrevue.
- **Tous prêts à coller** dans un CV, un message LinkedIn ou un kit de préparation d'entrevue.

Bonne chance pour décrocher ce poste, votre maîtrise de *Mon calendrier II* vous séparera!