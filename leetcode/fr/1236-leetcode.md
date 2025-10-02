---
titre: LeetCode 1236. Web Crawler - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La maîtrise du Leetcode 1236 – **Crawler Web* *
**Bon / Mauvais / Ugly *

> *=Si vous voulez décrocher un emploi d'ingénierie logicielle, vous devez répondre aux problèmes d'entrevue classiques. Leetcode 1236 (Web Crawler) est une mine d'or qui teste la traversée du graphe, l'analyse des cordes et la manipulation soigneuse des caisses.

---

Récapitulation des problèmes

> **Objectif** – À partir du début Url`, ramper chaque URL qui se trouve sous le *même nom d`hôte* (par exemple `http://exemple.org`) en utilisant le `HtmlParser` fourni.
> **Constraints**
> * Pas de doublon (chaque URL visitée une seule fois).
> * Ignorez les URLs qui pointent vers un autre nom d'hôte.
> * Traiter les URLs avec/sans barre oblique comme distinctes.
> * Toutes les URL utilisent le protocole `http` et aucun port personnalisé.

> **Output** – Liste de toutes les URL accessibles (tout ordre).

> **Heure** – O(V + E)
> **Espace** – O(V)

---

Aperçu de la solution

Le graphique est implicite : chaque URL est un nœud, et les bords sont les hyperliens retournés par `htmlParser.getUrls(url)`.
Un classique **Breadth‐First Search (BFS)** (ou Profondeur‐First Search) est tout ce dont nous avons besoin.

1. **Extrait le nom d'hôte** de `startUrl`.
«nom d'hôte = url[7: url.find('/', 7)]» (la partie après "http://" et avant le premier "/" après elle).
2. **Queue** – pour BFS; **Stack** – pour DFS.
3. ** Set visible** – pour éviter de revoir les URL.
4. Alors que la queue/la pile n'est pas vide :
* Pop une URL.
* Demandez `htmlParser.getUrls(url)` pour les voisins.
* Pour chaque voisin qui partage le nom d'hôte ** et** n'a pas été visité, l'ajouter à l'ensemble visité et le pousser sur la file d'attente / pile.
5. Retournez l'ensemble visité comme une liste.

---

Code – Java

"Java
Importation de java.util.*;

solution de classe {
*** Interface donnée par la plate-forme (ne pas implémenter) */
interface HtmlParser {
Liste <String> getUrls(String url);
}

liste publique <String> ramper(démarrage de la chaîne htmlParser) {
Chaîne host = getHostname(startUrl);

Queue<String> q = nouveau ArrayDeque<>();
Set<String> visité = nouveau HashSet<>();

q.offre(startUrl);
visité.add(startUrl);

alors que (!q.isEmpty()) {
la chaîne url = q.poll();
pour (String nxt : htmlParser.getUrls(url)) {
si (nxt.startsWith(hôte) && visited.add(nxt)) {
q.offre(nxt);
}
}
}
retourner la nouvelle liste d'array<>(visité);
}

chaîne privée getHostname(String url) {
int idx = url.indexOf('/', 7); // skip "http://"
retour idx == -1 ? url : url.substring(0, idx);
}
}
«» "

---

Code – Python

'`python
à partir de collections import deque
de taper l'importation Liste

♪ La plateforme fournit cette interface – ne l'implémentez pas
Classe HtmlParser:
def getUrls(self, url: str) -> Liste[str]:
...

Solution de classe:
def crawl(self, startUrl: str, htmlParser: HtmlParser) -> Liste[str]:
host = self._hostname(startUrl)

q = deque([startUrl])
visité = {départ - Oui.

alors que q:
url = q.popleft()
pour nxt dans htmlParser.getUrls(url):
si nxt. commence avec(hôte) et nxt non visité:
visité.add(nxt)
q.annexe(nxt)

liste de retour(visité)

@staticmethod
def _hostname(url: str) -> str:
idx = url.find('/', 7) # sauter "http://"
retourner l'url si idx == -1 autre url[:idx]
«» "

---

Code – C++

'`cpp
#incluez <string>
#incluez <vecteur>
#incluez <queue>
#inclut <unordered_set>
utilisant l'espace de noms std;

// La plateforme fournit cette interface – ne pas implémenter
classe HtmlParser {
public:
vecteur virtuel<string> getUrls(const string& url) = 0;
};

solution de classe {
public:
vectorielle<string> ramper(chaîne commencer Parseur et htmlParser) {
chaîne host = getHostname(startUrl);

file d'attente <string> q;
non ordonné_set<string> visité;

q.push(startUrl);
visited.insert(startUrl);

pendant que (!q.vide()) {
chaîne url = q.front(); q.pop();
vector<string> neigh = htmlParser.getUrls(url);
pour (cont string & nxt : proche) {
si (nxt.compare(0, host.size(), host) == 0 &&
visited.insert(nxt).second) { // inséré avec succès
q.push(nxt);
}
}
}
vecteur de retour<string>(visited.begin(), visited.end());
}

particulier:
chaîne statique getHostname(const string& url) {
taille_t pos = url.find('/', 7); // sauter "http://"
Return pos == chaîne::npos ? url : url.substr(0, pos);
}
};
«» "

---

Les bons, les mauvais et les mauvais – Interview Insight

Aspect du bien
- C'est quoi ?
**BFS garantit une profondeur minimale; DFS est plus simple à écrire récursivement.
**Extraction d'un nom d'hôte** Exclure simplement `startswith` permet d'économiser du temps , difficile d'obtenir à droite sur le premier essai (off‐by‐one, protocole manquant) , oubliant de gérer les URL sans barre oblique (par exemple `http://a.com` vs `http://a.com/`) conduit à de mauvaises réponses ,
**Manipulation visitée de l'ensemble**
**L'utilisation de `contains(host)` peut faussement correspondre à `http://evil.com` dans une URL différente. Ne pas échapper à des caractères spéciaux ou manipuler `https://` conduit à de faux positifs.
**Profondeur de la récursion** 104 → crash d'exécution
**Complexité**= O(V + E) – optimum pour l'interview== Aucune= Oublier le filtre hostname →= O(V + E + X) où X est le nombre de liens cross-host==
**Cas d'escroquerie**=Slash de trailing traité comme distinct (vérification explicite)=Les URLs peuvent contenir des paramètres de requête; toujours le même nom d'hôte – fine=_htmlParser.get Urls` retournant la même URL à plusieurs reprises – toujours en sécurité à cause de l`ensemble visité

À emporter

* Expliquez toujours vos choix de conception. *
Dites à l'intervieweur pourquoi vous utilisez BFS, comment vous êtes garantir aucun duplicata, et comment vous êtes extraire le nom d'hôte en toute sécurité.
Si vous pouvez également signaler les pièges (par exemple, la partie "gugly" de l'analyse des cordes) vous démontrerez la maturité.

---

Comment utiliser ceci dans une entrevue d'emploi

1. **Afficher le squelette** – Commencez par l'interface de la plate-forme et la classe `Solution`.
2. **Parlez de l'extraction du nom d'hôte** – expliquez pourquoi l'index commence à 7 ("http://").
3. **Discuser les structures de données** – pourquoi une « file » sur une pile (si vous choisissez BFS).
4. **Complexité de l'état** – mettre l'accent sur le comportement O(V + E).
5. **Pièges de Mention** – Slashes de fuite, URLs dupliquées, limites de récursion.

> **Astuce**: Si l'intervieweur demande une version DFS, échangez la file d'attente contre une pile ou un assistant récursif. La logique fondamentale reste la même.

---

Article de blog optimisé par le SEO

> **Titre**:
> * Maîtriser le Leetcode 1236: Web Crawler – le bon, le mauvais, et le mauvais *

> **Mots clés:
> `Leetcode 1236 Web Crawler`, `Java BFS Web Crawler`, `Python DFS Crawler Web, `C++ Solutions Leetcode`, `entretien d'ingénierie logiciel`, `conseils d'entretien de codage`, `problèmes de codage d'entretien d'emploi "

Article

> **Introduction**
> Le problème de Web Crawler est un bijou caché dans le seau Leetcode.
> Il vous force à jongler graph traversal avec la manipulation de cordes – un combo d'interview classique.

> **Ce qui le rend génial pour votre consommation* *
> * Démontre la maîtrise du BFS/DFS.
> * Fait ressortir l'attention portée aux détails (extraction du nom d'hôte, traitement du duplicata).
> * Affiche la possibilité d'écrire un code propre et réutilisable en plusieurs langues.

> **Les extraits de code**
> • Java (BFS) – voir section ci-dessus
> • Python (BFS) – voir section ci-dessus
> • C++ (BFS) – voir section ci-dessus

> ** Analyse de complexité**
> * **Heure** : Chaque URL est traitée une fois ; chaque bord (hyperlien) examiné une fois → O(V + E).
> * **Space**: La file d'attente/stack tient au plus toutes les URL accessibles → O(V).

> **Pièges communs d'entrevue* *
> 1. **Parsage d'hôte** – les débutants oublient souvent le décalage de 7 pour "http://" ou mal gérer les URL sans suivre `/`.
> 2. **Set visible** – en utilisant `visited. contient alors `add` peut doubler le processus d'un noeud si ce n'est prudent.
> 3. **Profondeur de récursion** – une récursion DFS naïve peut atteindre la limite de la pile sur une chaîne de liaison très profonde.

> **Pro‐Tip**
> Écrivez d'abord un helper `getHostname()`. Testez-le sur les cas de bord:
> * `http://a.com` (pas de barre oblique)
> * `http://a.com/` (root)
> * `http://a.com/path`

> **Enveloppe**
> La maîtrise de Web Crawler vous équipe avec un modèle robuste pour *toute* problème d'entrevue graphe-traversale. Pratiquez le modèle BFS/DFS, modifiez la logique d'appariement des chaînes pour différents domaines, et vous serez prêt à accepter le prochain cycle de codage.

> **Appel à l'action**
> Vous voulez en voir plus Leetcode gold-mines? Suivez-moi sur GitHub, LinkedIn et Medium pour des solutions d'entrevues de taille mordue qui atterrissent!

---

Prêt à décrocher votre prochain emploi ?

Donnez-moi une ligne sur Linked Si vous voulez une plongée plus profonde, une interview simulée ou un plan d'étude personnalisé.
*Les Leetcode 1236 deviennent votre histoire de réussite d'entrevue! *

---