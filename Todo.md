# TODO.md — Thread-Safe Task Scheduler

## Objectif du projet

Créer un scheduler C++ capable de lancer des tâches différées et récurrentes dans un environnement multithread, en garantissant la sécurité thread-safe.

---

## 1. Setup du projet

* [x] Créer l’arborescence de dossiers (`src/`, `include/`, `tests/`, `build/`)
* [x] Initialiser un repo Git (`git init`)
* [x] Ajouter un `.gitignore` pour C++ (`build/`, fichiers objets, etc.)
* [x] Configurer un `CMakeLists.txt` minimal pour compiler et linker (C++17 minimum)
* [x] Créer un `main.cpp` minimal pour tester la compilation

---

## 2. Conception et structure

* [ ] Définir une classe `TaskScheduler`
* [ ] Prévoir une structure pour représenter une tâche :

  * Identifiant unique (ex: int ou UUID)
  * Fonction à exécuter (`std::function<void()>`)
  * Temps d’exécution prévu (timestamp)
  * Intervalle pour tâches récurrentes (optionnel)
* [ ] Utiliser un `std::priority_queue` ou `std::multiset` pour stocker les tâches triées par temps d’exécution

---

## 3. Gestion des threads

* [ ] Ajouter un pool de threads (ex: vecteur de `std::thread`)
* [ ] Implémenter une boucle de travail dans chaque thread qui :

  * Attend la prochaine tâche à exécuter (condition\_variable)
  * Exécute la tâche quand son temps est arrivé
* [ ] Gérer l’arrêt propre du scheduler (flag atomic, wake-up threads)

---

## 4. Synchronisation et sécurité

* [ ] Utiliser `std::mutex` pour protéger la queue de tâches et les structures partagées
* [ ] Utiliser `std::condition_variable` pour notifier les threads de l’ajout de nouvelles tâches ou de l’arrêt
* [ ] Garantir que l’accès concurrent aux tâches soit thread-safe

---

## 5. Fonctionnalités principales

* [ ] Méthode `schedule(task, delay_ms)` : planifier une tâche unique différée
* [ ] Méthode `scheduleAtFixedRate(task, delay_ms, interval_ms)` : planifier tâche récurrente
* [ ] Méthode `cancel(taskId)` : annuler une tâche planifiée
* [ ] Méthode `shutdown()` : arrêter tous les threads proprement

---

## 6. Tests unitaires & validation

* [ ] Écrire des tests basiques de planification simple (avec `assert` ou framework minimal)
* [ ] Tester les tâches récurrentes
* [ ] Tester l’annulation de tâche
* [ ] Tester la fermeture propre du scheduler avec `shutdown()`

---

## 7. Optimisations & extensions (optionnel)

* [ ] Gérer la répartition intelligente des tâches dans le pool de threads
* [ ] Ajouter des logs simples pour déboguer (timestamps, thread ids)
* [ ] Ajouter une gestion des exceptions dans les tâches
* [ ] Implémenter une interface pour récupérer la liste des tâches planifiées

---

## Notes & références utiles

* Utiliser `std::chrono` pour les mesures de temps
* `std::function` pour stocker les callbacks
* Mutex + condition\_variable pour synchronisation (thread-safe)
* Thread pool simple avec `std::thread`
* Exemple d’algorithme priority queue : [https://en.cppreference.com/w/cpp/container/priority\_queue](https://en.cppreference.com/w/cpp/container/priority_queue)

---