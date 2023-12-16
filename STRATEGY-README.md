# Strategy
This file will describe a strategy to build this project in phases.  Each phase will be described in only a high-level of detail here. 
Details for phase should include updated system and application architecture, data model changes, technologies and tooling, and goals.

## (In Planning) Target State Architecture

I think this will be a 3-tier web-app architecture.  

Research/Get Help:  I am not sure yet how to describe the other applications that will be involved.  I believe they are either part of the Application tier or their own tier, depending on implementation (spark app, ml model).  

### Tier 1: Presentation 
#### Plan:
JS/HTML/CSS for browser/front-end web app/site.  Probably a site, due to limited time for learning UX.
Make it a RESTbased front-end, plan to create REST services in the application.
Implement FHIR format standards for data I/O from the application.

#### Goals:
Host a EMR-like web form that will mock a workflow for a FHIR encounter. Get patient data, add a diagnosis, get a recommendation, save encounter (if recommendation from model used by provider to recommend to patient, keep track)

#### Consider:
Having the data format between the Application and the front end not use FHIR standard over JSON.  Might be more realistic setting it up that way.

## Tier 2: Applications

### Back-end
#### Plan:
Spring or Flask or Django, something easy to setup and build REST services on, connect DBs too.
Make the API/services RESTbased for communication with front-end.  Use JSON format for feeding data to front-end.
Implement FHIR format standards for data I/O with the front-end.

#### Goals:
Support a EMR-like web form that will mock a workflow for a FHIR encounter. Get patient data, add a diagnosis, get a recommendation, save encounter (if recommendation from model used by provider to recommend to patient, keep track)
Simulate users accessing the workflow and using the web-form on the front-end, test concurrency, TPS and data pipeline capabilities.
Request a treatment recommendation from a ML model, serve that prediction back to the front end.
Store the encounter, predicted treatment (recommendation) info in a DB (and/or stream it to a kafka topic). 

#### Consider:
Having the data format between the Application and the front end not use FHIR standard over JSON.  Might be more realistic setting it up that way.

### ML Treatment Prediction Model
#### Plan:
Need to do research here.  I am hoping to find a model with APIs that is freely available to use (hopefully its mock or anonymized data)
If I can't, I'll need to have a way to get training data for the model, create and host a model, then train the model.  
The trained model version then needs to be hosted/available to the Backend, via API I am thinking, to request treatment predictions.
The output treatment recommendation needs to be stored or streamed somewhere to be used in analyzing the model and patient/encounter outcomes.

#### Goals:
Same as plan right now.

#### Consider:
Open source or freely available models with existing API, doesn't need to be FHIR standard data.  I could figure out some mapping or conversion if needed.

### Spark App / Jobs
#### Plan:
For training the model will need a way to get the data set wrangled and transformed into training data.
Could also use this to coordinate model training - create model, select type, transform data, split training/test sets, train model, get stats on model.  Idk if I can deploy/test with this yet.
Might have spark jobs to pull data out of DBs, transform/calcs on it to prepare for analytics and then dump/stream output to ... for analytic dashboard.

#### Goals:
Same as plan right now.

#### Consider:


## Tier 3: Data

### PostgreSQL or MySQL (Might be several of same or differing techs)
#### Plan:
Store raw data for training model, and transformed training data, which models and trainings its used in
Store mocked provider, encounter, and patient data needed for the web application - for loading it, actions taken, saving, ending, etc.
Store predictions model makes.

#### Goals:
Same as plan right now.

#### Consider:

### Kafka 
#### Plan:
Setup topics and schemas to support event streaming.
Configure (if needed) to allow the necessary producers / consumers to use Topics.
A Topic for predictions by the model to storing into a DB or pull for analytic dashboard. 
A Topic for model training (training sets used, model metrics, version, etc) to store into DB or pull for analytic dashboard.
A Topic for enounters? or "prediciton recommended"? 

#### Goals:
Same as plan right now.

#### Consider:


## Phase 1:  Get a web app running that simulates an EMR that loads/communicates data for an "Encounter".

Looking at PyHipster and JHipster to easily spin up a web app framework ->  web server backend, data model, services and front-end with main (a template) site
JHipster will be used to setup Sprint backend, React or Angular front end.  PyHistper would give us Flask or Django I believe, with React front end.

Im on a tight timeline to get phase 1 working and demonstratable.  I will use a simple 3-tier architecture for the web app.
Tier 1: Presentation - JS/HTML/CSS for browser/front-end, probably make use of templates to save time.
Tier 2: App - Spring or Flask or Django, something easy to setup and build REST services on, connect DBs too.
Tier 3: Data -  Whatever is needed for the web-form in PostgreSQL or MySQL (mocked patient and provider info, mocked predictions, saved encounters, etc.)

I need to select a particular web form or workflow and form to simulate with my web app.  
Now I'm also thinking I might want to simulate hundreds of web-apps at some point to test real-time data for a whole network of uses.

Learn the data and FHIR specification that should be used with that web form.  Work out a phase 1 data model from there.
I want to then spin use PyHipster or JHipster to create the web app.

