---
title: "On SPARQL and Wikidata"
date: 2024-12-12
draft: false
summary: "Some interesting exercises from my master's courses"
tags: ["study"]
---

One of the modules in my first semester of the master's program I'm in is Knowledge Models, for which I'm taking the subject "Knowledge Graphs". At the beginning it seemed like an intimidating subject, but now it's both still intimidating and really interesting as well (I prefer not to underestimate subjects until I've passed them XD). 

As I'm working with knowledge graphs and RDFs, I've learned to use SPARQL for writing queries (i.e. writing commands to retrieve information from the graphs you have). On top of that, the people teaching this subject have worked on Wikidata, so many of the assignments of this subject include using the <a href="https://query.wikidata.org/">Wikidata query service</a>, which can be so much fun once you get the grasp of it (this is for all of you out there who love reading Wikipedia articles and find fun facts or correlations).

Let's take a look at some examples of how you can use this query service (you can find more information in the documentation <a href="https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service">here</a>):

1. The first query gives us a list of famous dogs that have a Wikipedia article. You can go to the <a href="https://query.wikidata.org/">Wikidata query service</a> and paste the code below, then run it by pressing the "Play" button.
<pre>
  <code>
    SELECT ?item ?itemLabel
    WHERE {
	  ?item wdt:P31 wd:Q144 .
	  SERVICE wikibase:label { bd:serviceParam wikibase:language "en" }
    }
  </code>
</pre>

2. This example is a query that gives us a map with the location of all cities in the world that are named "Bergen".
<pre>
  <code>
    #defaultView:Map
    SELECT DISTINCT ?item ?label ?article ?coordinates
    WHERE {
      ?item rdfs:label "Bergen"@en.
      ?article schema:about ?item;
               schema:isPartOf [ wikibase:wikiGroup "wikipedia" ].
      OPTIONAL { 
      ?item wdt:P625 ?coordinates.
      }
    }
    ORDER BY ?item
  </code>
</pre>

The result of the query looks like this:
<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23defaultView%3AMap%0ASELECT%20DISTINCT%20%3Fitem%20%3Flabel%20%3Farticle%20%3Fcoordinates%0AWHERE%20%7B%0A%20%20%3Fitem%20rdfs%3Alabel%20%22Bergen%22%40en.%0A%20%20%20%20%3Farticle%20schema%3Aabout%20%3Fitem%3B%0A%20%20%20%20%20%20%20%20%20%20%20schema%3AisPartOf%20%5B%20wikibase%3AwikiGroup%20%22wikipedia%22%20%5D.%0A%20%20%20%20OPTIONAL%20%7B%20%0A%20%20%20%20%3Fitem%20wdt%3AP625%20%3Fcoordinates.%0A%20%20%7D%0A%7D%0AORDER%20BY%20%3Fitem" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

3. A last example for today is another map, but this time it has a pin on any city that is the location of formation of a boy band.
<pre>
  <code>
    #defaultView:Map
    SELECT DISTINCT ?boyband ?boybandLabel ?location ?locationLabel ?coord
    WHERE {
    ?boyband wdt:P31 wd:Q5741069;  
             wdt:P740 ?location.   
    ?location wdt:P625 ?coord.    
  
    SERVICE wikibase:label {bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en".}
    }
  </code>
</pre>

Check out the result here:
<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org./embed.html#%23defaultView%3AMap%0ASELECT%20DISTINCT%20%3Fboyband%20%3FboybandLabel%20%3Flocation%20%3FlocationLabel%20%3Fcoord%0AWHERE%20%7B%0A%20%20%3Fboyband%20wdt%3AP31%20wd%3AQ5741069%3B%20%20%23%20Instance%20of%20boyband%0A%20%20%20%20%20%20%20%20%20%20%20wdt%3AP740%20%3Flocation.%20%20%20%23%20Location%20of%20formation%0A%20%20%0A%20%20%3Flocation%20wdt%3AP625%20%3Fcoord.%20%20%20%20%23%20Coordinates%20of%20the%20location%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20%20%20%20%20%20%23%20Get%20labels%20for%20items%20in%20the%20user%27s%20language%0A%20%20%20%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%0A%20%20%7D%0A%7D%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

Hope this article gave you a bit of an insight of how using the WIkidata query service can be amazing to pull out random facts, let this be your next tool to explore the internet!