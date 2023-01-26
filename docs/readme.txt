# README
# Données Persée fournies dans le cadre du Master Humanite Numériques 2022-2023
# Comptes-rendus du Journal des Savants (ISSN 0021-8103)

## Conventions de nommage des fichiers

<date de création au format aaaammjj>_jds_<contenu du fichier>.extension

## Liste des fichiers et dictionnaire de données

- readme.txt
- 20221010_jds_CR.csv
	- fichier d'extraction brute des CR de la base de données (ne comprend pas les sections de CR correspondant plus à des articles ou des notes biblio)
	- date d'extraction 10/10/2022
	- Lors du traitement documentaire Persée, les éléments de la page sont analysés et circonscrits dans des zones. Le texte et le titre des comptes-rendus figurent dans de telles zones. Il est possible que le contenu d'un CR soit réparti dans plusieurs zones.
	- dans le fichier, chaque ligne correspond à une zone de compte-rendu

	- colonne issue_id: identifiant du numéro de fascicule de la zone de CR (contient notamment l'ISSN, l'année de parution)
	- colonne page_id: identifiant de la page dans laquelle figure la zone CR
	- colonne area_id: identifiant de la zone de CR (area=zone)
	- colonne area_previous: si le contenu d'un CR est réparti dans plusieurs zones, cette colonne indique l'identifiant area_id de la zone précédente. S'il n'y a pas de zone précédente (CR sur une seule zone), la valeur est NULL. Ex: le CR "Supplementary papers of the American school of classical studies in Rom" est réparti sur les zones jds_0021-8103_1909_num_7_1_T1_0047_0000_3 et jds_0021-8103_1909_num_7_1_T1_0047_0000_4
	- colonne area_title: titre du CR
	- colonne area_text: texte de la zone de CR. Il peut être nécessaire de concaténer plusieurs area_text pour reconstituer un CR complet
	
## Utilisation

Les données sont directement extraites de la base de données Persée pour le projet de Master HN 2022-2023.

L'exploitation des données de plein texte est rendue possible par l'Ordonnance n° 2021-1518 du 24 novembre 2021 https://www.legifrance.gouv.fr/jorf/id/JORFTEXT000044362034 qui autorise les opérations de fouille de texte et de données dans le marché numérique à des fins de recherche. Voir par exemple https://www.ouvrirlascience.fr/la-fouille-de-textes-et-de-donnees-a-des-fins-de-recherche-une-pratique-confirmee-et-desormais-operationnelle-en-droit-francais/

Les données ne peuvent être rediffusées en dehors du projet.

## Sources de données connexes

### SPARQL endpoint data.persee.fr (métadonnées)

Exemple de requêtes "liste des documents typés comptes-rendus" (comprend aussi les sections du genre "note critique", non extraites dans le fichier 

PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX n1: <http://data.persee.fr/ontology/persee-ontology/>
PREFIX n3: <http://purl.org/ontology/bibo/>
SELECT DISTINCT ?Document_40 ?Issue_73 ?Journal_108
WHERE { ?Document_40 a n3:Document .
        ?Document_40 rdf:type n1:Review .
        ?Issue_73 a n3:Issue .
        ?Document_40 dcterms:isPartOf ?Issue_73 .
        ?Journal_108 a n3:Journal .
        ?Issue_73 dcterms:isPartOf ?Journal_108 .
        ?Journal_108 dcterms:title "Journal des savants" . }
ORDER BY ?issue_73

## Références

https://www.aibl.fr/publications/periodiques/journal-des-savants
https://fr.wikipedia.org/wiki/Journal_des_savants
https://www.persee.fr/collection/jds


