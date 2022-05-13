---
layout: page
title: Projects
permalink: /students
---

## Bluetooth dosimeter - COVID 19 topical!

Contact tracing is a contentious issue and fraught with technical problems. However, a simple "bluetooth dosimeter" which records unique bluetooth devices you have seen and when (after discarding your own, housemates and neighbours!) is an index of how much social contact you may have had. If we presented this to people and showed them the times of day etc they were in busy places, perhaps even augmented with their location data, this might form the basis for behaviour change to reduce exposure, e.g. avoiding busy shopping or travel times. As with the COVID tracing on iPhone and Android, if attempting to do this bluetooth tracking in an app on a phone it would need to run all the time, or be builtin by Apple and/or Google. Instead we could use a simple arduino or raspberry pi (like) device which could be always on in your pocket and simply download the data once a day (when plugged in to recharge) to a platform for visualization. We can supply the hardware if anyone is interested in building the system and visualization, possibly linking to location data and perhaps even as a stretch goal running a few trials with users. This project can be in any language supported on your choosen HW platform.

### Online corpus linguistics

Corpus Linguistics is the study of language as expressed in corpora (i.e. samples) or real-world text. As an example, we may wish to discover how often (more precisely how frequently) the name of a product, TV show or politician appears in sentences with words that are complementary or negative. We would like to study the words people are exposed to as they use a web-browser, but we need to do this in a privacy preserving way. We have developed the Pripa tool which integrates a browser plugin with Teams as a platform for doing this work (you can install it from the Chrome web store). However, the Teams integration requires complex authorization mechanics and so the tool is too complex for many to deploy. Starting with the prototype Pripa browser plugin, we want to implement a different and simpler method for the data collection, e.g. using Dropbox or somethign similar. This project requires knowlege of Javascript, HTML and CSS.

### Factchecker plugin

Develop a Chrome plugin that grabs the content of a webpage visited, pulls out keywords and searches amongst fact checking websites for relevant fact checked stories. The Google FactCheck Explorer tool <https://toolbox.google.com/factcheck/explorer> provides a tool to perform such searches across fact checking sites, and indeed they also offer an API <https://toolbox.google.com/factcheck/api> that the project could use. As a starting point we already have the "Pripa" prototype browser plugin that provides a framework for processing the text in a page that can be extended... (see project above). This project requires knowlege of Javascript, HTML and CSS.

### Other plugins

Given a plugin framework - make up your own plugin based on text being read on web page: readability? harmful language? angry conten? etc 

### Smarter charging

The Carbon Intensity service (https://www.carbonintensity.org.uk) offers an API to obtain predictions of electricity grid carbon intensity. Considering specifically at home electric vehicle charging as a use case, the project is to write an optimization system that given a predicted demand (a schedule of upcoming electric car journeys), uses the carbon intensity API to generate the best times during which to charge the vehicle to minimise the carbon footprint and continuously update it based on unanticpated usage (e.g. unscheduled quick trip to shops). The demands will be based on a series of personas (9-5 office worker car communter, nurse car commuter on shift pattern, community worker, car only evenings and weekend, etc), to exercise the optimization.


