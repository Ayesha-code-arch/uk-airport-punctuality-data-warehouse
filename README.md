# UK Airport Punctuality Data Warehouse

## Overview

This project builds a star‑schema data warehouse to analyse flight punctuality for UK airports using 24 monthly datasets from 2023–2024.  A fact table stores aggregated delay and cancellation metrics, while four dimension tables (Date, Airline, Airport and Destination) support multi‑dimensional slicing.

## Data Source

The raw data are monthly CSV files published by the UK Civil Aviation Authority (CAA).  They contain metrics such as average delays, number of flights cancelled, and percentages of flights in various delay categories for all commercial routes between UK airports and their destinations.

## Schema Design

The star schema consists of one fact table and four dimension tables:

- **Fact_Flight_Punctuality** – central fact table with key metrics including `Average_Delay_Mins`, `Number_Flights_Cancelled`, `Actual_Flights_Unmatched` and percentage delay categories (e.g., `Flights_0_To_15_Minutes_Late_Percent`).  Foreign keys link to the dimension tables to enable slicing by date, airline, airport and destination.

- **DIM_DATE** – calendar dimension with `Date_ID`, `Reporting_Period`, `Year` and other temporal attributes to support trends and seasonality analysis.

- **DIM_AIRLINE** – contains `Airline_ID` and `Airline_Name` for airline‑specific performance comparisons.

- **DIM_AIRPORT** – stores `Airport_ID`, `Airport_Name` and codes (IATA/ICAO) to analyse punctuality by departure airport.

- **DIM_DESTINATION** – includes `Destination_ID`, `Origin_Destination` and `Origin_Destination_Country` enabling route‑level insights.

This denormalised design improves query performance for dashboards in Tableau and can be extended with additional metrics in future (e.g., weather‑related delays).

## Data Preparation

- **Cleaning** – unified column names across 24 CSV files, corrected inconsistent casing (e.g., "UK" vs "United Kingdom"), added missing columns for 2023 and filled null values.

- **Normalisation** – standardised airline and airport names, appended IATA codes and normalised strings.

- **Integration** – loaded all files into a single dataset and populated the fact and dimension tables (\u224879 842 rows) with appropriate surrogate keys.

## Analysis & Visualisations

The warehouse enables exploratory analysis of flight punctuality.  Example insights include:

- **Top 10 airlines by average delay** – British Airways and Air India exhibited some of the longest average delays【981962952002436†screenshot】.
- **Flight cancellations by month** – cancellations peaked in August 2023 (\u22484 141 flights)【915748098102448†screenshot】, while 2024 showed lower peaks.
- **Punctuality by destination** – routes to Antalya and Dublin had higher proportions of severe delays【646688908409176†screenshot】.
- **Year‑over‑year comparisons** – average delays in 2023–2024 were lower than in 2022–2023【194940230824084†screenshot】.

A Tableau workbook accompanies this project (not included here) to reproduce these charts.

## Files

- **DataAnalysis2_53_75_single.docx** – detailed report describing the data warehouse design, data cleaning steps, and analysis.
- Additional scripts or notebooks can be added in `src/` or `notebooks/` when the code for building the warehouse is shared.

## Usage

To explore the data warehouse or reproduce the analysis:

1. Review the report in `DataAnalysis2_53_75_single.docx`.
2. Prepare the CSV files and follow the schema definitions in the report to load data into a relational database or Tableau.
3. Use the provided dimension and fact tables to create visualisations of delays, cancellations and other metrics.

## License

This project is licensed under the MIT License – see the LICENSE file for details.

## Acknowledgements

The flight punctuality data are provided by the UK Civil Aviation Authority.  Thanks to Kingston University for guidance on data warehousing and Tableau.
