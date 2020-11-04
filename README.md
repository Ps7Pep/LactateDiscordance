# LactateDiscordance

## LactateDiscordanceETL contains the ETL functions to obtain the cohort dataset

Note that this project uses data from 3 different sources, but only two of them are open access (MIMIC and eICU). This script contains the code to extract, transform and load all the data from all 3 sources, so people interested can check it. However, only the ETL parts related with MIMIC and eICU could be reproduced in case people interested have access to those databases.

This repo contains the file alldbs.csv, which is the output of the ETL script. People interested may reproduce the analysis using this file as input in the rest of notebooks.

## The rest of notebooks contain the different analyses applied to the data obtained by the ETL
