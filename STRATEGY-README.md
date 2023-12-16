# Strategy
This file will describe a strategy to build this project in phases.  Each phase will be described in only a high-level of detail here. 
Details should include addtions and changes to architecture for the applications being built
Details should also include the overall system architecture, data model changes, technologies and tooling, and goals.

## Phase 1:  Get a web app running that simulates an EMR that loads/communicates data in FHIR formats.

Looking at PyHipster and JHipster to easily spin up a web app framework ->  web server backend, data model, services and front-end with main (a template) site
JHipster will be used to setup Sprint backend, React or Angular front end.  PyHistper would give us Flask or Django I believe, with React front end.

Im on a tight timeline to get phase 1 working and demonstratable.  I will use a simple 3-tier architecture for the web app.
Tier 1: Presentation - JS/HTML/CSS for browser/front-end to render site, REST Based
Tier 2: App - Spring or Flask or Django, something easy to setup and build REST services on, connect DBs too.
Tier 2: ML Model? -  This will need to go somewhere, need to learn how its done.  Want to ask model for predictions and serve them back to web-app.
Tier 2: Spark App? - Jobs to process large data sets and get training data for ML model, also train it maybe.
Tier 3: Data -  Thinking this will get more complicated than just a DB for the App.  Also want to store training data in here.


I need to select a particular web form or workflow and form to simulate with my web app.  
Now I'm also thinking I might want to simulate hundreds of web-apps at some point to test real-time data for a whole network of uses.

Learn the data and FHIR specification that should be used with that web form.  Work out a phase 1 data model from there.
I'm on a timeline, so i don't have the luxury of planning out the entire end state architecture, which requires research from me.

I want to then spin use PyHipster or JHipster to create the web app 

