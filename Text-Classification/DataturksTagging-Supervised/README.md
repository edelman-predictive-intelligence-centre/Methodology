# DataturksTagging-Supervised

## How to

### Phase 1 - Labelling Taxonomy Preparation & System Configuration

#### Phase 1.1 - Labelling Taxonomy Preparation 
1. Collaborate with domain experts to brainstorm and decide overall structure and definition of labelling Taxonomy

#### Phase 1.2 - Dataturks container set-up
1. Set up an Compute Engine/virtual machine instance on GCP
2. Install Docker on Compute Engine (CE) instance
3. Load and start Dataturks docker image
4. Access Dataturks app through External IP address

#### Phase 1.3 - Automation scripts on Compute Engine instance
1. Generate API key and project name from Dataturks
2. Call Dataturks internal API to retrieve labelled data every 15mins
3. Save labelled data into local on CE
4. Set up Google Cloud Storage (data lake) buckets and BigQuery schema 
5. Transfer labelled data from local to Google Cloud Storage bucket in ndjson format
6. Transfer ndjson from Cloud Storage into BigQuery schema
7. Set up bash scripts and crontab jobs for running scripts from background


### Phase 2 - Experimental labelling & Taxonomy refinement
1. Prepare a testing dataset for experimental labelling (Max 100 MB for free plans)
   -  A text file with each line in file having sentence to be classified. OR
   -  A zip file of all the text documents to be classified. 
2. Create a new Text Classification project, with all tags required, on Dataturks
3. Label testing dataset (Two taggers will label one article)
5. Export labeled data via UI
6. Conduct Intercoder Reliability Check (IRC) on labelled data (See table below)
   - If the discrepancy of labelling is less than 10% (At least 90% articles are labelled as the same tag), IRC is passed
   - Otherwise
     - Manually evaluate articles with differernt tags from 2 taggers
     - Refine Taxonomy definitions internally for better clarity
     - Repeat step 2-5

| Intercoder Reliability Check  | labeler2 - category1 | labeler2 - category2 | labeler2 - category3 |
| --- | --- | --- | --- |
| labeler1 - category1 | 30 |3 |2 |
| labeler1 - category2 | 2 |30 |1 |
| labeler1 - category3 | 3 |5 |20 |

### Phase 3 - Official Labelling & Further refinement
1. Prepare dataset for labelling (Max 100 MB for free plans)
   -  A text file with each line in file having sentence to be classified. OR
   -  A zip file of all the text documents to be classified. 
2. Create a new Text Classification project, with all tags required, on Dataturks
3. Label dataset (Two taggers will label one article)
4. Export labeled data via UI
5. Conduct Intercoder Reliability Check (IRC) on labelled data
   - If the discrepancy of labelling is less than 10% (At least 90% articles are labelled as the same tag), IRC is passed
   - Otherwise
     - Manually evaluate articles with differernt tags from 2 taggers
     - Refine Taxonomy definitions internally for better clarity
     - Repeat step 2-5
6. Configure API key and project name for Automation scripts and start crontab jobs
7. Scripts will run every 15mins to transfer labelled data into Cloud Storage and BigQuery

### Phase 4 - Modelling
1. Train Model
2. Save Model 
3. Make Prediction

## Case Studies

### Dow Jones Human Trafficking Categorization 

### Risk Sensing Risk Categorization 
