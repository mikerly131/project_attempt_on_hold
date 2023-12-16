# Passion Project: serveUpRecos

### serveUpRecos is a web application that mocks a workflow for a provider and patient in a Health Care System, called an encounter, and serves up a treatment recommendation as predicted by an AI model for a specific diagnosis.  

The web application will gather patient and provider information to populate a mocked web form a provider would use during the encounter.  A user or simulated user has the role of provider and will select diagnosis for the patient.  The diagnosis will be sent to a ML model trained to serve treatment recommendations for a prediction of the best treatment to apply for the given diagnosis and patient.  The provider then has the ability to take and use the recommendation or ignore it.  The encounter is then ended and data from it is staged for analytical dashboards.

Providers who want to start incorporating AI/ML predictions for treatments into the overall course of care for patients will now have this ability.  The idea is this system architecture is reproducible and extensible for many encounters, workflows, purposes and models.  For example, assisting with the diagnosis and/or framing of symptomps presented during an encounter. The data coming into and out of the encounters and forms will be FHIR standard, so it should be useable and shareable for the providers EMR systems, and network of partners and 3rd parties.

I will be working on this project in phases.  It may take more than one phase to produce a valuable web application.  Phase 1 is going to be creating the web application that mocks the EMR form/workflow used for a provider-patient encounter.  I'll do this using <Spring, Flask or Django back end>, < MySQL or PostgreSQL DB >, and < React or Angular with HTML/CSS for the front end >.  I also will be researching EMRs for style and experience as well as standards like FHIR to implement.  

See the [STRATEGY_README.md](https://github.com/mikerly131/serveUpRecos/blob/main/STRATEGY-README.md) for more detailed information on architecture and phased development plan.

Extensions or future phases of this project might add functionality like a second web form to capture success or failure of treatment, with subsequent build out spark jobs to processes that data with recommendation data and then feed output to the analytical dashboard.  Another job could then find and use the best recommendations and outcomes to prepare data for retraining the model and yet another job could train it.
