1. Which is cheaper the Azure cloud models or the openai api? - Reason being n8n will be deployed in the azure so those APIs can be used
2. Is it possible to use the openrouter APIs to use the small language models in the MACbook?
3. Is it possible to host the n8n pipeline in macbook and run it everyday at a particular instant and use the loaclly avaible models?

----

THis is a simple n8n agent which is used to extract the JObs from the linkedin, glassdoor and the indeed platform which are sent as a email.

This is a simple script that is exectuted manually everyday to topup the Notion JOb directory and classify based on the categorey and assign a three day timer assuming perday three applications are applied.

----

The structure of this n8n agent is as follows
1. Extract the followup section of the gmail
2. Using an AI agent read the subject of the email to extract the company, JOb title from the subject
3. Select the JObs which follow in the list from the enum which are the type of profile the user is intrested in
4. Based on 90% closeness with the JOb titile in the enum select those jObs. [Filter 1]
5. Extract the JOb description of those roles and and do a analysis if the JObs based on the 4 CVs present for each of the each category are relevant for the application there should be atleast 95% relevance with the JOb description and the CVs of those type of roles [Segreation 1] [Filter 2]
6. Finally add those JObs in the Notions and the company names in the company directory with the expiry date and the assuming three applications per day. [Segregation 2]

----
How to use this applicaiton:

1. Steps to add the filter in gmails

2. Setup the agent in the PC

3. Setup the notion

4. Happy applying.