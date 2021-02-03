## Usage Guide

As a research oriented project, we do not have an specific user guide, however we can still help you navigate through how to go setting up the research tools we used, as well as other tools used.

To get started, you will want to download the Stanford Core NLP software package off their website [link](https://stanfordnlp.github.io/CoreNLP/download.html). You will require Java to be installed on your device.

Stanford CoreNLP v.3.5+ requires Java 8, but works with Java 9/10/11 as well. If using Java 9/10/11, you need to add this Java flag to avoid errors (a CoreNLP library dependency uses the JAXB module that was deleted from the default libraries for Java 9+):

From the command line Java interface, you will enter the following to get the program available to run.

### How do I update ...

Use:

```sh
$ --add-modules java.se.ee
$ java -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLP -file input.txt
```

Or, a user interface is available from the zipped folder found from the download.


Another, and much different, tool we used in the project was Fleiss' Kappa.

This value is used to determine the level of agreement within multiple raters in a scenario. Temporal logic was a key aspect in our research, ergo, we had to develop a way to determine the team's level of agreement on whether or not a phrase contains temporal logic. This was key in generating training data for a potential Machine Learning algorithm.

[Image of Fleiss] (https://github.com/NLP-with-GKS/Senior-Design/blob/master/f.PNG)

## FAQ

### I made a change to the ---, how to I run the changes?

Use:

```sh
$ docker-compose up --build
# open http://localhost/ to see changes
```

### How do I run ...
Ensure the following ports are exposed for incoming traffic to ... :

```
80, 4000, 5000, 8080, and 8888
```
