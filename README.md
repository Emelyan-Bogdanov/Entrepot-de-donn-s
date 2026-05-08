📋 RAPPORT 2 : TAJMOUATI Moad - BI4people (2021-2022)
Vue d'ensemble
AspectDétailsÉtudiantTAJMOUATI MoadMasterInformatique Décisionnelle Et Vision IntelligenteUniversitéSidi Mohamed Ben Abdellah (Fès, Maroc) + Lumière Lyon 2 (France)Période23 mars - 29 juillet 2022 (18 semaines)LaboratoireERIC (Université Lyon 2 & Lyon 1)ProjetANR BI4people - "Le décisionnel pour tous"
Objectif Principal
Rendre l'analyse interactive OLAP accessible à tous en automatisant complètement le processus d'entreposage de données (ETL), intégration multi-source, et visualisation intelligible.

🏗️ Architecture Technique (BI4people)
Stack Technologique
┌─────────────────────────────────────────────┐
│         BI4people Platform                   │
├─────────────────────────────────────────────┤
│                                              │
│  Frontend:                                   │
│  ├─ React.js                                │
│  ├─ React-i18next (multilingue)             │
│  ├─ jQuery, Bootstrap                       │
│  └─ CubeJS (OLAP client)                   │
│                                              │
│  Orchestration:                              │
│  └─ Node.js (scripts d'interopérabilité)   │
│                                              │
│  Backend/Analyse:                            │
│  ├─ CubeJS (OLAP engine)                   │
│  ├─ Python (données scientifiques)          │
│  ├─ C++ (autres modules)                    │
│  └─ Java (modules additionnels)             │
│                                              │
│  Base de Données:                            │
│  └─ MariaDB (datawarehouse_BI4people)       │
│                                              │
│  Concepts clés:                              │
│  ├─ ETL (Extract-Transform-Load)           │
│  ├─ OLAP vs OLTP                            │
│  ├─ Snowflake Schema                        │
│  └─ Data Mart                               │
│                                              │
└─────────────────────────────────────────────┘
Partenaires du Projet
Académiques:

ERIC (Lyon) - OLAP, Personnalisation BI, Cryptographie
IRIT (Toulouse) - Modèles entrepôts, ETL
LIFAT (Tours) - Visualisations données
ELICO (Lyon) - Études d'usage

Industriels:

TRIMANE - Big Data R&D

Associés:

TUBA (Lyon), FING - Protection données personnelles


🎯 Mission de Stage Réalisée
Trois composantes principales:
1. ETL - Étude de Cas "Scolarisation en France"
Source: Base INSEE (Recensement population 2007, 2012, 2017)

Fichier: base-cc-diplomes-formation-2017-2012-2007.xlsx

Modèle Données (Snowflake Schema):
sql-- Tables de Dimensions
dim_annee, dim_catDiplome, dim_sexe, dim_scolarisation
dim_trancheage, dim_commune, dim_departement, dim_region

-- Table de Faits
fact_population (FK_IDscolarisation, FK_IDcommune, FK_IDannee, FK_IDsexe, 
                 FK_IDcategorieDiplome, FK_IDtrancheage, nombrePersonnes)
Processus ETL:
pythonExtraction:
├─ 3 sheets Excel (COM_2007, COM_2012, COM_2017)
├─ Filtrer colonnes INTEGRER*
└─ Charger via Pandas

Transformation:
├─ Remplacer valeurs NULL par 0
├─ Diviser colonnes par racines
│  (P07_HSCOL0205 → CODGEO, REG, DEP, LIBGEO, SEXE, SCOLARITE, AGE, ANNEE, DIPLOME, NOMBREPERSONNES)
├─ Créer tables staging (stagingarea2007, 2012, 2017)
└─ Normaliser selon modèle cible

Chargement:
├─ Remplir dimensions avec jointures
└─ Insérer dans fact_population via merges pandas
Technologies Utilisées:

Python (Pandas, MySQL Connector)
MariaDB
UML Diagramming


2. Visualisations OLAP avec CubeJS + React
CubeJS Architecture:
CubeJS Backend (Node.js)
├─ Gère connexion MariaDB
├─ Queue de requêtes
├─ Mise en cache
├─ Pré-agrégations
└─ ORM (Object-Relational Mapping)

         ↓ API REST

CubeJS Frontend (React)
├─ @cubejs-client/core
├─ @cubejs-client/react
└─ Composants de visualisation
   ├─ Tables
   ├─ Bar Charts
   ├─ Pie Charts
   └─ Lignes, Aires, Zones
Schéma CubeJS (Measures & Dimensions):
javascript// Mesures (données quantitatives)
measures: [
  count: COUNT(*)
]

// Dimensions (données catégorielles)
dimensions: [
  annee: STRING,
  sexe: STRING,
  scolarisation: STRING,
  trancheage: STRING,
  diplome: STRING
]
Commandes de Démarrage:
bashnpx cubejs-cli create ProjectBI -d MySQL
npm i --save @cubejs-client/core
npm i --save @cubejs-client/react

# Serveur backend: http://localhost:4000
# Dashboard React: http://localhost:3000

3. Internationalisation (i18n) - Dashboard Bilingue (FR/EN)
Framework: react-i18next
bashnpm install react-i18next i18next --save
npm install i18next-browser-languagedetector --save
Dictionnaire JSON (FR → EN):
json{
  "translation": {
    "Explore": "Explorez",
    "Measure": "Mesure",
    "Dashboard": "Tableau de bord",
    "Dimension": "Une dimension",
    "Chart": "Graphique",
    "Bar": "Barre",
    "Pie": "Tarte",
    "settings": "Configurations"
  }
}
Configuration (src/i18n.js):
javascriptimport LanguageDetector from "i18next-browser-languagedetector";

i18n
  .use(LanguageDetector)
  .use(initReactI18next)
  .init({
    resources: { /* FR & EN translations */ },
    interpolation: { escapeValue: false },
    react: { useSuspense: false }
  });
Changement de Langue (Header.js):
javascriptconst Header2 = () => {
  const [t, i18n] = useTranslation();
  return (
    <button onClick={() => i18n.changeLanguage('fr')}>
      {t('explore')}
    </button>
  );
};

📊 Concepts BI Collaboratifs
Collaborative Business Intelligence (CBI)
Définition: Extension à dessein du processus d'analyse BI en ajoutant partenaires internes/externes et ouvrant accès aux données.
Formes de CBI:

Discussion générale
Discussion centrée sur rapport
Ajout d'annotations
Partage d'information
Orientation d'analyse
Visualisation du comportement
Coordination des tâches

Phases Processus Décision Collaborative:
Phase 1: Pré-Décision
├─ Partage compréhension commune du problème
├─ Liste objectifs
├─ Représentation commune
└─ Définir limites & frontières

Phase 2: Décision
├─ Générer & comparer idées (tous participants)
├─ Organiser idées (augmenter visibilité)
├─ Comparer solutions (points de vue différents)
└─ Identifier & publier accords, sélectionner solution

Phase 3: Post-Décision
├─ Suivi décision
├─ Plan d'action
└─ Mise en œuvre

🔍 Différences OLTP vs OLAP
CaractéristiqueOLTPOLAPUtilisationSGBD productionEntrepôt donnéesOpérationMise à jourAnalyseType d'accèsLecture/ÉcritureLectureTaille BDFaible (< 1 GB)Importante (> TB)RequêtesSimples, régulièresComplexes, irrégulièresQuantité infosFaibleImportantOrientationLigneMulti-dimensionStructureBeaucoup tablesPeu tables largesAncienneté donnéesRécenteHistorique

📈 Résultats Obtenus
Dashboard Finalisé:
✅ Visualisations créées:

Table de données (population par commune)
Bar Charts (population par région, années)
Pie Charts (répartition sexe, scolarisation)
Multi-dimension (population × tranches âge × diplômes)

✅ Enregistrement visualisations pour réutilisation
✅ Édition/Suppression post-création des graphiques
✅ Interface bilingue (FR/EN) détectée automatiquement

💡 Comparaison des Deux Rapports
AspectRapport 1 (WANG)Rapport 2 (TAJMOUATI)Année2017-20182021-2022ProjetGDE (Moteur indexation)BI4people (Collaborative BI)FocusSearch + IndexingETL + OLAP + i18nStackJava EE, Lucene, TikaNode.js, React, CubeJSBase donnéesRelationnel (SGBD)MariaDBDonnéesScientifiques/Études EDFINSEE (Scolarisation France)InternationalizationNonOUI (React-i18next)Architecture3-tier (C++/Python/Web)Modulaire microservices

🎓 Conclusion
Ce rapport représente une évolution significative de l'informatique décisionnelle :
✨ Avancées:

Automatisation complète ETL
Collaborative Business Intelligence
Support multilingue natif
OLAP accessible "self-service"
Architecture serverless/modulaire

📌 Challenges:

Arrivée tardive en France (contraintes administratives)
Intégration dans grand projet distribué
Communication équipe virtuelle multi-établissements
