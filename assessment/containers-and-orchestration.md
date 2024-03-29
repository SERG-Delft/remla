---
layout: page
title: Containers & Orchestration
parent: Assessment
---

# {{page.title}}

The following rubric items will be assessed on a scale from *Insufficient* to *Excellent*.

### Model Service

Sufficient
: Flask server is used to serve the model. The server is distributed through an image that is build with a workflow.

Good
: The model that is served can be updated without creating a new image, i.e., it is either downloaded on-start or mounted.

Very good
: The server pre-processes queries the same was as the training data.

Excellent
: All server endpoints have a well-defined API definition that follows the [Open API Specification](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/2.0.md#operation-object).
Swagger is used to generate an API documentation.



### App

Sufficient
: The application\* uses the microservice that serves the model through REST. The microservice uses the version-aware `lib` through a package manager. The application has a basic frontend that allows to query the model ("a textbox with a button") and shows the result.

Good
: The app has an actual "use case" that offers interactions that go beyond the basic query/response. For example, the app could be the central system for a restaurant: users can see reviews and leave their own, the restaurant can access all reviews and sees statistics on how users like their services.

Very Good
: Better than "good", but not all criteria of "excellent" are fulfilled.
For example, the monitoring extension is trivial or the interactions cannot be easily used for an experiment.
If you select this point please elaborate your reason briefly.

Excellent
: The application contains interactions that could be monitored and leveraged for continuous experimentation. For example, the restaurant could see the predicted sentiment for reviews, but is allowed to flag/change incorrect labels. Another option is to make the sentiment label a part of the user input and use the information to validate whether the prediction is correct.

{:.footnote}
(\*) The intention is to build a basic microservice architecture on the server.
If your app is built with a rich-client framework like Angular or React, do not connect to the model service directly, but introduce an *API gateway* in between.


### Operation

Sufficient
: The operation repository contains a Docker compose file\* that allows to start up the application and use it. The app is the only service that is accessible from the outside.

Good
: The Docker compose file contains examples of how to use a volume mapping, a port mapping, and an environment variable.

Very Good
: Better than "good", but not all criteria of "excellent" are fulfilled.

Excellent
: The repository contains a `README.md` file that elaborates on required parameters and provides starting points for outsiders that want to investigate the code base.

{:.footnote}
The Docker compose file does not need to grow with the later complexity of the Kubernetes deployment.
The intention is to keep it as a *simple-to-start* illustration of the deployed app.


The peer review will also contain a free text form.
Please use this form to summarize your assessment of all rubric criteria in this category, especially if you rated something as insufficient.
In addition, explain what you think would be the next important step that needs to be realized.