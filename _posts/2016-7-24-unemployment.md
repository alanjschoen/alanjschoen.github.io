---
layout: post
title: US unemployment at different geographic scales
published: True
---

I've spent a few weeks using Pandas and I'm starting to appreciate just how powerful it is.  I recently used it with geographic data for the first time, and that's the topic of this post.

I'm working on a larger project, where I want to see the imapact of different measures of unemployment on Americans' political views.  This was inspired by my AT through hike.  I walked through a lot of Appalachian communities, where I talked to locals and heard stories about economic decline.  Having witnessed this firsthand, I don't believe that the nationwide 6% unemployment rate captures the reality in many small towns in America.

My goal is to get a clearer picture my looking at metrics other than the unemployment rate, and to see if I can find a connection to voting behavior.  My analysis will have to happen at different geographic scales.  Presidential primary results are counted by county, so I need county data to analyze primary votes.  Senate and House races are done by state and congressional district, so I need to be able to work at that scale as well.

My first step was to gather [unemployment data](http://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml "American Fact Finder") and [cartographic files](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html) from the US Census Bureau.  Fortunately, it's quite easy to get these data files.  

I processed the data using [Pandas](http://pandas.pydata.org/) and plotted it with [Vincent](https://vincent.readthedocs.io/en/latest/). Processing them was a little harder, so I wrote a little library to import census data and link it to shape files.  I put my code on [Github](https://github.com/alanjschoen/magamap) to help out my classmates who are also working with political and economic data.

{% include image.html url="/assets/unemployment/congress.png" description="2015 unemployment rate by congressional district" %}
I looked at the data first by congressional district.  Here we see values ranging from 3% to about 20%.  Unemployment looks very low in the Dakotas and Minnesota, and it is highest in parts of the Deep South and California.  Southern Maine has a pocket of extreme unemployment.  This map has a couple of odd features: my home state of Maryland is bloated, and lake Michigan is missing.  I think this is because bodies of water like the Chesapeake Bay and Lake Michigan are included in congressional districts, so this map does not adhere strictly to land boundaries.

{% include image.html url="/assets/unemployment/state.png" description="2015 unemployment rate by state" %}
At the state level, unemployment looks lower across the board.  I preserved the same coloring scale so it would be easy to compare the maps.  State-by-state, the highest rate of unemployment is only 7%.  Right away, this shows a big hazard of looking at the nation-wide unemployment rate.  The average does not show that some areas have it much worse than others.  Furthermore, the national average is weighted per-capita, meaning that it puts more weight on cities.  If you drive (or walk) across the country, on the other hand, you will spend most of your time in less dense areas.  So the spatial average of unemployment is considerably different from the per-capita average.

{% include image.html url="/assets/unemployment/county.png" description="2011 unemployment rate by county" %}

I used 2011 data in this case because I found it from another source in a convenient format.  I will switch to 2015 data as soon as I am able to.

I preserved the 0-20 range but there are actually a few counties that exceed 20% unemployment. Looking at the numbers, I see that most are in Puerto Rico, but there are about 5 on this map. Imperial County in CA has nearly 30% unemployment, and Yuma County in Arizona is not far off.

Generally, the unemployment rate looks much worse on this map.  This is related to the "spatial average" problem that I talked about before.  But it also shows that the economy isn't great for everyone.  Some people live in communities with unemployment rates as high as 30%, even as the economy at large is doing much better.  Perhaps the disconnect between what these people experience and what they hear on the news causes them to seek out radical political remedies.

I have a big caveat about comparing this to the other maps: these numbers are from 2011, and unemployment rates were higher across the board at that time.  I will update this post as soon as I have 2015 unemployment numbers.