---
titre: LeetCode 1226. Les Philosophes de la Table -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# Philosophes de la salle à manger – Un LeetCode Classic (1226)
> **Problème**: Cinq philosophes s'assoient autour d'une table circulaire, chacun avec un bol de spaghetti.
> Entre chaque paire de philosophes se trouve une fourchette.
> Un philosophe ne peut manger que lorsqu'il tient ** à la fois** sa fourchette gauche et droite.
> Implémenter `wantsToEat()` de sorte qu'aucun philosophe ne meurt de faim, même lorsque la méthode est appelée à plusieurs reprises et à partir de plusieurs fils.

> **Pourquoi ça compte**
> Le problème des Philosophes de la salle à manger est l'exemple canonique d'un algorithme concomitant à l'arrêt.
> Les intervieweurs adorent parce qu'il teste votre compréhension de **mutexes**, **semaphores**, **resource order** et **fairness** dans un contexte réel.

> **Langues**: Java, Python, C++

---

- Oui. 1. Le piège classique – toutes les fourches d'abord

Une solution naïve ressemble à ceci :

Texte
Serrure gauche
Serre la fourche droite
manger
déverrouiller la fourche droite
débloquer la fourche gauche
«» "

Quand chaque philosophe saisit d'abord la fourche gauche, une attente circulaire surgit:

«» "
P0 -> gauche0
P1 -> gauche1
P2 -> gauche2
P3 -> gauche3
P4 -> gauche4
«» "

Tous les philosophes bloquent alors sur la bonne fourchette, ne progressant jamais → **deadlock**.

---

- Oui. 2. Le bien – Acquérir la fourche inférieure

La façon la plus simple d'éviter l'impasse est d'imposer une commande globale sur l'acquisition de la fourche.

* **Règle**: Toujours verrouiller l'index ** plus petit** d'abord, puis le plus grand.
* Pour le philosophe ` Les "
* Indice de la fourche gauche = ` Les "
* indice de fourche droite = `(i+1) % 5`

Si un philosophe trouve l'index de gauche < l'index de droite, choisissez la première à gauche; sinon choisissez la première à droite.

**Pourquoi ça marche* *
L'ordre rompt l'attente circulaire : chaque fourchette ne peut être demandée que dans une direction unique.

**Équité** – Il est encore possible pour un philosophe de mourir de faim si le programmeur est biaisé, mais LeetCode , les tests montrent rarement ce comportement extrême.

**Complexité** – O(1) par appel, pas d'attente occupée, pas de type de verrouillage spécial.

---

- Oui. 3. Le "Bad" – Tournage occupé et inutile

Une erreur courante est de continuer à essayer d'acquérir une fourchette dans une boucle serrée ('tryLock()' à plusieurs reprises).
Cela gaspille les cycles du CPU, dégrade le débit et peut encore entraîner la famine.

---

- Oui. 4. Le "Ugly" – Utilisation "synchronisée" sans équité

«» "
synchrone (fork[i]) {
synchronisé (fourche[(i+1)%5]) { ... }
}
«» "

Java.lang. Les serrures de l'objet sont *non-fair*. Si vous avez beaucoup de tentatives simultanées, certains fils peuvent être affamés pendant de longues périodes.

---

- Oui. 5. La solution finale – Code pour Java, Python, C++

Vous trouverez ci-dessous une mise en œuvre propre et prête à la production pour chaque langue, conformément à la règle **inférieure‐ID‐first**.

#### 5.1 Java

"Java
importer java.util.concurrent.locks.Lock;
importer java.util.concurrent.locks.ReentrantLock;

cours public Salle à mangerPhilosophers {

// 5 serrures de fourche
Serrure finale privée[] fourches = nouveau ReentrantLock[5];

Restaurant publicPhilosophers() {
pour (int i = 0; i < 5; i++) {
forks[i] = nouveau ReentrantLock(); // serrure non-fair est bien ici
}
}

// run() exécutera l'exécutable fourni
public vide veutToEat(int philosophe,
Prunable pickLeftFork,
Prunable pickRightFork,
Mangez,
PutLeft runnable Fourche,
Courable putRightFork) lance InterruptedException {

int left = philosophe; // index de la fourche gauche
int droite = (philosophe + 1) % 5; // indice de la fourchette droite

// choisir l'index inférieur d'abord pour éviter l'attente circulaire
int first = Math.min (gauche, droite);
int second = Math.max (gauche, droite);

// acquérir des serrures
forks[first].lock(); // bloquera jusqu'à ce que le verrou soit disponible
essayer {
fourches[seconde].lock();
essayer {
// ramasser les fourchettes
si (premier == gauche) pickLeftFork.run(); sinon, pickRightFork.run();
if (second == droite) pickRightFork.run(); sinon pickLeftFork.run();

// Manger
Mang.run();

// déposer les fourchettes
si (premier == gauche) putLeftFork.run(); sinon putRightFork.run();
if (second == droite) putRightFork.run(); sinon putLeftFork.run();
} enfin {
fourks[second].unlock(); // relâche la deuxième fourche
}
} enfin {
forks[first].unlock(); // relâcher la première fourche
}
}
}
«» "

** Harnais d'essai (minimum)* *

"Java
public statique vide principal(String[] args) lance interrompuException {
DiningPhilosophers dp = nouveau DiningPhilosophers();
Prunable pickL = () -> System.out.println(Thread.currentThread().getName()+" picks left");
PickR exécutable = () -> System.out.println(Thread.currentThread().getName()+" choisit à droite");
Mangage runnable = () -> System.out.println(Thread.currentThread().getName()+" mange");
PutL exécutable = () -> System.out.println(Thread.currentThread().getName()+" met la gauche");
PutR exécutable = () -> System.out.println(Thread.currentThread().getName()+" met à droite");

int n = 3; // combien de fois chaque philosophe va essayer de manger

pour (int i = 0; i < 5; i++) {
int p = i;
nouveau fil() -> {
essayer { pour (int j = 0; j < n; j++) dp.wantsToEat(p, pickL, pickR, manger, putL, putR); }
capture (InterruptedException e) { e.printStackTrace(); }
}, "Philosopher-"+i).start();
}
}
«» "

---

5.2 Python

'`python
les fils d'importation
de taper l'importation Appelable

Salle à mangerPhilosophes:
def _init_(self):
auto.fourches = [threading.Lock() pour _ dans la plage(5)]

def wantsToEat(self,
philosophe: int,
pickLeftFork: Appelable[[], Aucun],
pickRightFork: Appelable[[], Aucun],
Manger: Appelable[], Aucun],
putLeftFork: Appelable[[], Aucun],
putRightFork: Appelable[[], Aucun]) -> Aucun:

gauche = philosophe
droite = (philosophe + 1) % 5

# serrures de commande par id
première = min (à gauche, à droite)
seconde = max (gauche, droite)

avec self.forks[premier]:
avec soi-même. Fourche[seconde]:
# Choisir des fourchettes
si la première est à gauche:
pickLeftFork()
Sinon:
choisirRightFork()

Si deuxième == droite:
choisirRightFork()
Sinon:
pickLeftFork()

# Mangez
manger()

# poser des fourchettes
si la première est à gauche:
putLeftFork()
Sinon:
PutRightFork()

Si deuxième == droite:
PutRightFork()
Sinon:
putLeftFork()
«» "

**Essais simple (utiliser 5 fils)* *

'`python
temps d'importation

def main():
dp = Salle à mangerPhilosophers()

def pickL(): print(f"{threading.current_thread().name} picks left")
def pickingR(): print(f"{threading.current_thread().name} pickings right")
def eat(): print(f"{threading.current_thread().name} eats")
def putL(): print(f"{threading.current_thread().name} met la gauche")
def putR(): print(f"{threading.current_thread().name} met right")

def philosophe(id):
pour _ dans l'intervalle(3):
dp.wantsToEat(id, picL, picR, manger, putL, putR)
time.sleep(0.01) # donner une chance à d'autres fils

fils = [filage. Thread(cible=philosophe, args=(i,), name=f"P{i}") pour i dans l'intervalle(5)]
pour t dans les fils: t.start()
pour t en fils: t.join()

si __nom__ == "__main__" :
principal()
«» "

> **Note** : Le GIL Python® protège toujours les serrures, mais l'algorithme est le même qu'en Java.

---

C++

'`cpp
#incluez <iostream>
#incluez <fil>
#incluez <vecteur>
#incluez <mutex>

cours de salle à mangerPhilosophers {
public:
RestaurationPhilosophers() {
pour (int i = 0; i < 5; ++i) {
forks[i] = std::make_unique<std::mutex>();
}
}

vide veutToEat(int philosophe,
const std::fonction<evit()>& Choisir Fourche gauche,
const std::fonction<evit()>& choisir à droite Fourche,
const std::fonction<evit()>& manger,
const std::fonction<evit()>& PutLeftFork,
const std::fonction<evit()>& la Fourche de droite) {

int gauche = philosophe;
int droite = (philosophe + 1) % 5;

int first = md::min(gauche, droite);
int second = md:max (gauche, droite);

// Verrouillage dans l ' ordre mondial
md::unique_lock<std::mutex> lk1(*forks[first]);
std::unique_lock<std::mutex> lk2(*forks[second]);

// Récupération
si (premier == gauche) pickLeftFork();
sinon, choisissezRightFork();
si (deuxième == droite)pickRightFork();
autres pickleftFork();

// Manger
manger();

// poser
si (première à gauche) putLeftFork();
sinon mettreRightFork();
si (deuxième) droite)putRightFork();
autres, putLeftFork();
}

particulier:
std::vector<std::unique_ptr<std::mutex>> les fourchettes {5};
};
«» "

**Test rapide**

'`cpp
Int main() {
Salle à mangerPhilosophers dp;
auto pickL = [](){ std::cout << std::this_thread::get_id() << " pics left\n"; };
auto pickingR = [](){ std::cout << std::this_thread::get_id() << " picks right\n"; };
manger automatiquement = [](){ md::tout << md::cet_fil::get_id() << " mange\n"; };
auto putL = [](){ std::cout << std::this_thread::get_id() << " met left\n"; };
auto putr = [](){ std::cout << std::this_thread::get_id() << " met right\n"; };

md::vecteur<std::fil> c'est
pour (int i = 0; i < 5; ++i) {
[&dp,i,pickL,pickR,eat,putL,putR] {
pour (int j=0;j<3;++j)
dp.wantsToEat(i,pickL,pickR,eat,putL,putR);
});
}
pour (auto& t: ths) t.join();
}
«» "

---

- Oui. 6. Comment la solution répond aux exigences de LeetCode

* Le **API** est exactement la seule fourniture LeetCode – aucune fonction principale nécessaire pour le juge.
* Chaque méthode acquiert ** exactement deux** serrures et les libère immédiatement après avoir mangé.
* Pas d'attente, pas de famine de fil (aux fins des essais).
* Fonctionne sous une charge de travail très concurrente – chaque bloc d'appels seulement sur les deux fourchettes nécessaires.

---

- Oui. 7. Ce que les recruteurs veulent voir

1. **Clarifier le raisonnement de l'impasse** – Tous les philosophes accaparant la gauche d'abord → attente circulaire
2. **Création des ressources** – Acquérir la fourchette inférieure. (en milliers de dollars)
3. **Codage sûr** – Utiliser `Lock`/`Mutex`/`Semaphore` correctement.
4. **L'état d'esprit des essais** – Présentez un harnais d'essai minuscule ou des essais unitaires.
5. **Explication** – Pourquoi l'algorithme fonctionne, pas seulement le code.

---

- Oui. 8. SEO‐Amis Résumé (pour le développeur de recherche d'emploi)

- **Titre**: *Mastering LeetCode 1226 – Le problème des philosophes de la restauration en Java, Python & C++ *
- **Description détaillée**: Découvrez comment résoudre le problème de LeetCodeS Dining Philosophers (1226) avec un code propre et sans blocage en Java, Python et C++. Boostez votre préparation d'entrevue et atterrissez votre prochain emploi. (en milliers de dollars)
- **Mots-clés cibles**:
- Les philosophes du dîner "
- `Code de débit 1226`
- 'question d'entretien de devises "
- "Évitement de la mort" "
- `Java filetage "
- `Python multiprocessus "
- 'C++ mutex "
- "l'accord d'entretien d'emploi "

---

- Oui. 9. Dernier départ

Aspect du bien
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Algorithme**= Ordre des ressources (en premier lieu avec l'ID inférieur)=Horloge de boucle "tryLock" de type "synchronisé"
**Utilisation de l'unité de commande**
**Favorité**
**Readability** blocs

---

- Oui. Tu veux avoir ton prochain entretien ?

- **Expliquez le blocage**: Afficher le diagramme d'attente circulaire.
- **Afficher la correction**: Commande de ressources ou un seul sémaphore pour toutes les fourchettes.
- **Équité des peines** : "Utiliser un sémaphore " fair " si vous voulez un comportement round-robin strict. (en milliers de dollars)
- **Parler de l'évolutivité**: L'algorithme fonctionne en temps constant, indépendamment du nombre de philosophes.

Laissez cet article dans votre blog personnel ou LinkedIn, et regardez les recruteurs remarquer que vous pouvez **penser critiquement à la concurrence**, **écrire du code propre** en plusieurs langues, et ** résoudre les puzzles d'entrevue classiques**. Bonne chance !