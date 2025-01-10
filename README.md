# Data-Engineering Marketing Project

[English version](#Overview)

# Überblick

Dieses Projekt zeigt anhand einer fiktiven Firma, welche Erkenntnisse man aus
Marketing Daten gewinnen kann. Hierzu werden die Daten von einer API abgefragt,
transformiert und dann in übersichtlichen Dashboards mit Power BI dargestellt.

## Szenario

Fantasy AG ist eine Firma die Hundespielzeuge verkauft und dafür viel online
Werbung, vor allem über Facebook macht. Nachdem nun eine Woche lang mehrere
Werbekampagnen geschaltet wurden, ist es an der Zeit diese auszuwerten. Die
Firma hat hierbei drei Kampagnen mit mehreren verschiedenen Werbungen erstellt.
Die gewünschte Zielgruppe sind 40-45 jährige Frauen, die sich für Hunde,
Haustiere und Spielzeuge (Hunde/Haustierspielzeuge) interessieren.

Die Geschäftsführung möchte nun wissen:

-   Überblick über geschaltete Anzeigen, Kosten, Klicks, Conversion Rate
-   Meist erreichteste Zielgruppe
-   Conversion Rate und Approved conversion Rate (Prozentzahl wieviele Nutzer
    nach dem Ansehen der Werbung gekauft haben)
-   Meistgeklickste Kampagne und Gewinn daraus
-   Prognose für Clickzahlen, wenn man die Kampagnenkosten erhöht

## Vorüberlegungen

Das Hauptziel des Projektes ist es, die vorhandenen Unternehmensdaten zu
zentralisieren und dann für datengetriebene Analysen zu nutzen.

Hierbei soll der Prozess des manuellen Übertragens von Daten (was oft sehr
fehleranfällig ist) gelöst werden und somit neueste Daten und Analysen auf
Tagesbasis bereit stehen, ohne zusätzlichen Aufwand zu verursachen.

Die gegebenen Marketing Daten sollen dann analysiert werden und Erkenntnisse
darüber gewonnen werden, welche Marketing Kampagne besonders lukrativ ist und
sich ein weiteres Investment lohnt.

Interessant ist hier dann die Prognose, die mittels Machine Learning erstellt
wird. Mithilfe dieser Prognose kann man dann die Clickzahlen, je nachdem welche
Kampagne man bewirbt und wieviel Geld man investiert, erwarten kann.

Die hier benutzten Daten kommen von:

### Facebook Marketing Daten:

-   https://www.kaggle.com/datasets/loveall/clicks-conversion-tracking
-   https://www.kaggle.com/datasets/madislemsalu/facebook-ad-campaign?resource=download

Diese beiden Datasets wurden zusammengelegt und außerdem wurden diese Daten
hinzugefügt, um ein anschaulicheres Ergebnis, statt nur Zahlen zu haben:

-   campaign_data.csv: Eine Tabelle die den Kampagnen ein Spielzeug und dessen
    Preis zuordnet
-   interest_data.csv: Eine zufällig erstelle Liste an Interessen der Nutzer, so
    abgestimmt dass die Hauptinteressen zur Werbung für Hunde passt

# Benutzte Technologien

Python Notebooks in Google Workflow werden benutzt um die Daten von der Kaggle
API zu laden und zunächst in einem DataLake (Google S3 Bucket) zu speichern.
Dann werden diese Daten transformiert und anschließend in einem DataWarehouse
gespeichert (Google BigQuery). Anschließend werden die Daten übersichtlich mit
Power BI dargestellt.

Alle benutzten Skripte hierfür, finden sich im Ordner "scripts".

![Pipeline Bild](assets/pipeline.png)

# Batch Data Ingestion

Die Daten werden im Notebook per API von Kaggle geladen, dann partioniert und im
.parquet Format abgespeichert. Dies geschieht als DataLake in einem Google S3
Bucket.

# Data Warehouse

Weiter per Google Workflow werden diese Daten dann transformiert und in das
gewünschte Format gebracht. Sobald dies geschehen ist, werden sie über eine
Pipeline in Google Bigquery gespeichert als Grundlage für die spätere Analyse.

Daten Vorhersage: Mit Hilfe eines Random Forest werden die Prognosen erstellt
und gespeichert. Die Genauigkeit mit 80% Trainingsdaten und 20% Testdaten
beträgt hier 90%.

# Dashboard

Das Dashboard ist mit Power BI erstellt und visualisert die oben genannten
Probleme in verschiedenen Ansichten.

![Dashboard Bild](assets/power_bi_analysis.pdf)

Power BI Datei:

In dieser sieht man das erstellte Dashboard aus den oben generierten Daten.
Zudem ist die Prognose Seite interaktiv, sodass man selbst die Clickzahlen
abschätzen kann.

# Kosten

Nach einer aktuellen Analyse würde dieses Projekt monatlich ca. 80€ Kosten. Die
Kosten bestehen aus:

-   Hosting von Google Workflow und ML Analyse auf Google Compute (80€)
-   Daten speichern (Free tier)
-   Daten abfragen (Free tier)
-   Daten visualisieren (Free tier)

Die Entwicklungszeit betrug: 30h

# Data Engineering Marketing Project

[German version](#Überblick)

# Overview

This project demonstrates how insights can be gained from marketing data using a
fictional company. Data is retrieved from an API, transformed, and then
visualized in clear dashboards with Power BI.

## Scenario

Fantasy AG is a company that sells dog toys and heavily invests in online
advertising, primarily through Facebook. After running several advertising
campaigns for a week, it is time to evaluate their performance. The company has
created three campaigns with multiple different ads. The target audience is
women aged 40-45 who are interested in dogs, pets, and pet toys.

The management wants to know:

-   Overview of the ads run, costs, clicks, and conversion rates
-   The most reached target group
-   Conversion rate and approved conversion rate (percentage of users who
    purchased after seeing the ad)
-   The most clicked campaign and its profit
-   Forecast for click numbers if campaign costs are increased

## Preliminary Considerations

The main goal of the project is to centralize the company's existing data and
use it for data-driven analysis.

This aims to eliminate the error-prone manual data transfer process, providing
up-to-date data and analyses on a daily basis without additional effort.

The given marketing data will be analyzed to gain insights into which marketing
campaign is particularly lucrative and worth further investment.

Of particular interest is the forecast generated through machine learning. This
forecast allows predictions of click numbers depending on which campaign is
promoted and how much money is invested.

The data used in this project comes from:

### Facebook Marketing Data:

-   https://www.kaggle.com/datasets/loveall/clicks-conversion-tracking
-   https://www.kaggle.com/datasets/madislemsalu/facebook-ad-campaign?resource=download

These two datasets were merged, and additional data was added to provide a more
illustrative result beyond just numbers:

-   `campaign_data.csv`: A table that assigns a toy and its price to the
    campaigns
-   `interest_data.csv`: A randomly generated list of user interests, tailored
    to match the main interests related to dog advertising

# Technologies Used

Python notebooks in Google Workflow are used to load data from the Kaggle API
and initially store it in a DataLake (Google S3 Bucket). The data is then
transformed and stored in a DataWarehouse (Google BigQuery). Finally, the data
is clearly visualized with Power BI.

All scripts used for this can be found in the "scripts" folder.

![Pipeline Image](assets/pipeline.png)

# Batch Data Ingestion

Data is loaded via the Kaggle API in the notebook, partitioned, and stored in
`.parquet` format. This is done as a DataLake in a Google S3 Bucket.

# Data Warehouse

Using Google Workflow, the data is then transformed and formatted. Once this is
complete, it is stored in Google BigQuery via a pipeline as a basis for later
analysis.

Data Prediction: Forecasts are created and stored using a Random Forest model.
The accuracy with 80% training data and 20% test data is 90%.

# Dashboard

The dashboard is created with Power BI and visualizes the issues mentioned above
in various views.

![Dashboard Image](assets/power_bi_analysis.pdf)

Power BI File:

This file displays the created dashboard from the generated data. Additionally,
the forecast page is interactive, allowing users to estimate click numbers
themselves.

# Costs

According to a recent analysis, this project would cost approximately €80 per
month. The costs consist of:

-   Hosting Google Workflow and ML analysis on Google Compute (€80)
-   Data storage (Free tier)
-   Data querying (Free tier)
-   Data visualization (Free tier)

The development time was: 30 hours
