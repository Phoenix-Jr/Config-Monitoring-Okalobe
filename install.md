Voici un runbook détaillé pour permettre à n'importe qui de prendre en main et de lancer ce projet de surveillance avec Prometheus, Grafana, Alertmanager et Blackbox Exporter.

### Pré-requis

1. **Docker et Docker Compose** doivent être installés sur la machine.
   - Pour installer Docker, suivez les instructions sur [Docker's official website](https://docs.docker.com/get-docker/).
   - Pour installer Docker Compose, suivez les instructions sur [Docker Compose's official website](https://docs.docker.com/compose/install/).

### Structure du Projet

Assurez-vous que la structure de votre projet ressemble à ceci :

```
project-directory/
├── docker-compose.yml
├── containers/
│   ├── prometheus/
│   ├── prometheus_config/
│   │   ├── prometheus.yml
│   │   ├── myrules.yml
│   ├── grafana/
│   ├── alertmanager_data/
│   ├── alertmanager_config/
│   │   └── alertmanager.yml
│   └── blackbox/
│       └── blackbox.yml
```

### Etapes pour Lancer le Projet

1. **Cloner le Répertoire du Projet**:
   Si vous n'avez pas encore le projet sur votre machine, clonez-le à partir de son dépôt source.

   ```bash
   git clone https://github.com/Phoenix-Jr/Config-Monitoring-Okalobe.git
   cd project-directory
   ```

2. **Vérifier la Configuration des Fichiers**:

   - Ouvrez et vérifiez les fichiers de configuration pour vous assurer qu'ils contiennent les bonnes configurations :
     - `prometheus.yml`
     - `myrules.yml`
     - `alertmanager.yml`
     - `blackbox.yml`

3. **Lancer les Conteneurs**:
   Utilisez Docker Compose pour lancer les conteneurs.

   ```bash
   docker-compose up -d
   ```

4. **Vérifier le Statut des Conteneurs**:
   Assurez-vous que tous les conteneurs sont correctement lancés.

   ```bash
   docker ps
   ```

   Vous devriez voir les conteneurs `prometheus`, `grafana`, `alertmanager` et `blackbox-exporter` en cours d'exécution.

5. **Accéder aux Interfaces Web**:
   - **Prometheus**: [http://localhost:9090](http://localhost:9090)
   - **Grafana**: [http://localhost:3000](http://localhost:3000)
   - **Alertmanager**: [http://localhost:9093](http://localhost:9093)
   - **Blackbox Exporter**: [http://localhost:9115](http://localhost:9115)

### Configuration et Utilisation

1. **Prometheus**:

   - Ouvrez Prometheus à [http://localhost:9090](http://localhost:9090).
   - Vérifiez que les cibles (targets) sont correctement configurées en naviguant vers `Status > Targets`.

2. **Grafana**:

   - Ouvrez Grafana à [http://localhost:3000](http://localhost:3000).
   - Connectez-vous avec les identifiants par défaut (utilisateur : `admin`, mot de passe : `admin`).
   - Ajoutez Prometheus comme source de données :
     - Naviguez vers `Configuration > Data Sources`.
     - Cliquez sur `Add data source` et sélectionnez `Prometheus`.
     - Configurez l'URL comme (ex:`http://prometheus:9090`) et enregistrez.

3. **Alertmanager**:

   - Ouvrez Alertmanager à [http://localhost:9093](http://localhost:9093).
   - Vérifiez que les alertes configurées sont présentes.

4. **Blackbox Exporter**:

   - Ouvrez Blackbox Exporter à [http://localhost:9115](http://localhost:9115).
   - Assurez-vous que le fichier de configuration `blackbox.yml` est correctement chargé.
   - Puis il faudra rajouter un dashboard

5. **Creer un nouveau dashboard**:
   - Choisir le template approprié importer sur graphana

### Arrêt du Projet

Pour arrêter les conteneurs :

```bash
docker-compose down
```

### Dépannage

- **Conteneur ne démarre pas**:

  - Vérifiez les logs du conteneur avec `docker logs <container_name>`.
  - Assurez-vous que les chemins des volumes et les fichiers de configuration sont corrects.

- **Problèmes de Connexion**:

  - Vérifiez les paramètres réseau.
  - Assurez-vous que les ports utilisés par les services ne sont pas occupés par d'autres applications.

- **Accès à Grafana**:
  - Si les identifiants par défaut ne fonctionnent pas, réinitialisez le mot de passe ou recréez le conteneur Grafana après suppression des volumes.

En suivant ce runbook, vous devriez être en mesure de lancer et gérer efficacement le projet de surveillance avec Prometheus, Grafana, Alertmanager et Blackbox Exporter.
