# SPARQL Examples
### Prefixes

    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX gi2mo:<http://purl.org/gi2mo/ns#>    
    PREFIX inov:<http://purl.org/innovonto/types/#>
    PREFIX oid: <http://purl.org/innovonto/legacy/types#>

## Count Ideas per IdeaContest
    PREFIX gi2mo:<http://purl.org/gi2mo/ns#>
    
    SELECT ?project (COUNT(?idea) as ?ideaCount) WHERE {
      ?project a gi2mo:IdeaContest.
      OPTIONAL {
        ?idea a gi2mo:Idea;
              gi2mo:hasIdeaContest ?project
      }.
    }
    GROUP BY ?project

## Count Participants per IdeaContest

    PREFIX gi2mo:<http://purl.org/gi2mo/ns#>
    PREFIX inov:<http://purl.org/innovonto/types/#>
    
    SELECT ?project (COUNT(?user) as ?userCount) WHERE {
      ?project a gi2mo:IdeaContest.
      OPTIONAL {
        ?user a inov:Ideator;
                 inov:hasSubmittedIdeasForIdeaContest ?project}.
    }
    GROUP BY ?project
    
## Find People with more than one Brainstorming Session

    PREFIX gi2mo:<http://purl.org/gi2mo/ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX inov:<http://purl.org/innovonto/types/#>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    
    SELECT ?ideator (COUNT(?session) as ?sessionCount) WHERE {
      ?ideator a inov:Ideator;
               inov:hasBrainstormingSession ?session.
    }
    GROUP BY ?ideator
    ORDER BY DESC(?sessionCount)