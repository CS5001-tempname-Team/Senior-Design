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

![Image of Fleiss] (https://github.com/NLP-with-GKS/Senior-Design/blob/master/2021%20User%20Guide/f.PNG)

## FAQ


### What is our project focusing on?

We are looking to see if there is an efficient method of taking natural language requirements and finding a way to take these requirements and have a more formal method of analzying their properties. This project has the ambition of being an automated process.

### Could I use an API for the Stanford Core NLP?

Below is a quick snippet of code that demonstrates running a full pipeline on some sample text. It requires the english and english-kbp models jars which contain essential resources.

It uses new wrapper classes that have been developed for Stanford CoreNLP 3.9.0 to make it easier to work with annotations.

Please note that this new API has not been tested as much as the classic API. Below this section is the documentation for the classic pipeline API.

```sh
import edu.stanford.nlp.coref.data.CorefChain;
import edu.stanford.nlp.ling.*;
import edu.stanford.nlp.ie.util.*;
import edu.stanford.nlp.pipeline.*;
import edu.stanford.nlp.semgraph.*;
import edu.stanford.nlp.trees.*;
import java.util.*;


public class BasicPipelineExample {

  public static String text = "Joe Smith was born in California. " +
      "In 2017, he went to Paris, France in the summer. " +
      "His flight left at 3:00pm on July 10th, 2017. " +
      "After eating some escargot for the first time, Joe said, \"That was delicious!\" " +
      "He sent a postcard to his sister Jane Smith. " +
      "After hearing about Joe's trip, Jane decided she might go to France one day.";

  public static void main(String[] args) {
    // set up pipeline properties
    Properties props = new Properties();
    // set the list of annotators to run
    props.setProperty("annotators", "tokenize,ssplit,pos,lemma,ner,parse,depparse,coref,kbp,quote");
    // set a property for an annotator, in this case the coref annotator is being set to use the neural algorithm
    props.setProperty("coref.algorithm", "neural");
    // build pipeline
    StanfordCoreNLP pipeline = new StanfordCoreNLP(props);
    // create a document object
    CoreDocument document = new CoreDocument(text);
    // annnotate the document
    pipeline.annotate(document);
    // examples

    // 10th token of the document
    CoreLabel token = document.tokens().get(10);
    System.out.println("Example: token");
    System.out.println(token);
    System.out.println();

    // text of the first sentence
    String sentenceText = document.sentences().get(0).text();
    System.out.println("Example: sentence");
    System.out.println(sentenceText);
    System.out.println();

    // second sentence
    CoreSentence sentence = document.sentences().get(1);

    // list of the part-of-speech tags for the second sentence
    List<String> posTags = sentence.posTags();
    System.out.println("Example: pos tags");
    System.out.println(posTags);
    System.out.println();

    // list of the ner tags for the second sentence
    List<String> nerTags = sentence.nerTags();
    System.out.println("Example: ner tags");
    System.out.println(nerTags);
    System.out.println();

    // constituency parse for the second sentence
    Tree constituencyParse = sentence.constituencyParse();
    System.out.println("Example: constituency parse");
    System.out.println(constituencyParse);
    System.out.println();

    // dependency parse for the second sentence
    SemanticGraph dependencyParse = sentence.dependencyParse();
    System.out.println("Example: dependency parse");
    System.out.println(dependencyParse);
    System.out.println();

    // kbp relations found in fifth sentence
    List<RelationTriple> relations =
        document.sentences().get(4).relations();
    System.out.println("Example: relation");
    System.out.println(relations.get(0));
    System.out.println();

    // entity mentions in the second sentence
    List<CoreEntityMention> entityMentions = sentence.entityMentions();
    System.out.println("Example: entity mentions");
    System.out.println(entityMentions);
    System.out.println();

    // coreference between entity mentions
    CoreEntityMention originalEntityMention = document.sentences().get(3).entityMentions().get(1);
    System.out.println("Example: original entity mention");
    System.out.println(originalEntityMention);
    System.out.println("Example: canonical entity mention");
    System.out.println(originalEntityMention.canonicalEntityMention().get());
    System.out.println();

    // get document wide coref info
    Map<Integer, CorefChain> corefChains = document.corefChains();
    System.out.println("Example: coref chains for document");
    System.out.println(corefChains);
    System.out.println();

    // get quotes in document
    List<CoreQuote> quotes = document.quotes();
    CoreQuote quote = quotes.get(0);
    System.out.println("Example: quote");
    System.out.println(quote);
    System.out.println();

    // original speaker of quote
    // note that quote.speaker() returns an Optional
    System.out.println("Example: original speaker of quote");
    System.out.println(quote.speaker().get());
    System.out.println();

    // canonical speaker of quote
    System.out.println("Example: canonical speaker of quote");
    System.out.println(quote.canonicalSpeaker().get());
    System.out.println();

  }

}

```

### Any ports I should keep open?
For the sake of the Stanford Core NLP keep port 80 open, as well as 8080:

```
IP address: 80
IP address: 8080
```
