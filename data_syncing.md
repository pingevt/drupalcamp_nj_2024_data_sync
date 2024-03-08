autoscale: false
build-lists: false
slidenumbers: true
slide-transition: push(horizontal, 0.25)
footer: **Pete Inge** | Bluecadet | __Synchronizing Art with Technology__

# Synchronizing Art with Technology
## Data Integration at the Amon Carter Museum of American Art

^
* Be the Storyteller
* Breath....

---

# Who am I?

## Pete Inge
### Senior Systems Architect, Bluecadet

**pinge@bluecadet.com**
**github.com/pingevt**
**peteinge.com**

![right 78%](media/bc/Bluecadet_Monogram-White.png)

^ Experience: ~10yrs freelance in web dev
Worked in D5-D10
Current: @ BC for >8 years
I'm a problem solver
Contact for more info

___

[.background-color: #FFFFFF]
[.slide-transition: push(horizontal, 0.3)]

![fit](media/bc/Bluecadet_Lockup-Primary.png)

---

[.slide-transition: push(horizontal, 0.3)]

# What is Amon Carter

**Located in the heart of Fort Worth’s Cultural District, the Amon Carter Museum of American Art (the Carter) is a dynamic cultural resource that provides unique access and insight into the history and future of American creativity through its expansive exhibitions and programming. Admission is always free. To learn more about the Carter, visit cartermuseum.org.**

![](media/20200730_0606.jpg)

![inline right](media/ACMoAA_Logo_RGB.png)

---

[.build-lists: true]
# Quick Poll

* Interest in Art and Technology Integration
* Developer/PM (with current challenges in mind)
* Developer/PM (with a future project in mind)
* Developer/PM (Other)
* Art Museum Directors looking to hire me/Bluecadet

^ 2 mins
Audience? Why did they attend the talk?

---

# What is **Data Syncing**?

![right](media/vert.jpg)

^
What is Data syncing? (2 mins)

---

# What is **Data Syncing**?

## Bringing external data into your site for a specific purpose

![right](media/vert.jpg)

^
What is Data syncing? (2 mins) [AI imagery]
Bringing external data into your site for a specific purpose
Maintains current Source of truth
Maintaining 2 independent sources

---

# What is **Data Syncing**?

## Bringing external data into your site for a specific purpose

### It is **NOT** migration

![right](media/vert.jpg)

^
What is Data syncing? (2 mins) [AI imagery]
Bringing external data into your site for a specific purpose
Maintains current Source of truth
Maintaining 2 independent sources

^
- It is NOT migration (explain the difference)
Migration is changing the source of truth
Moving old source to new source

^
- Picky distinction, but I think important **detail** to keep in mind

---

[.build-lists: true]

# Why are we talking about this today?

* We're developers.. duh
* Current state of technology
* Accross the board, we've seen a surge in organisations wanting to digitize
* In the museum space, a typical museum has about 95% of their collection in storage

^
Why are we talking about this? (2 mins) [diagrams]
  Microservices and data everywhere
  Modernizing collections (data)
  Typical museum has about 95% of their collection in storage
  W/ the pandemic, surge in orgs wanting to digitize
  Drupal is a great platform for larger enterprise level syncs
  Getting the public to see your content, not just researchers
~~What was the purpose for the Carter?
  AC purpose was~~

^
-->However many more reasons for Syncing Data.

---

^Lets dive in!

---

[.text: alignment(center)]
[.footer-style: alignment(left)]
[.slidenumber-style: alignment(right)]

# <br>
# <br>
# <br>
# First, _define_ the **state**
# and the **constraints**

---

[.text: alignment(center)]
[.footer-style: alignment(left)]
[.slidenumber-style: alignment(right)]

# <br>
# <br>
# <br>
# Second, _decide_ on an
# execution **strategy**

---

[.text: alignment(center)]
[.footer-style: alignment(left)]
[.slidenumber-style: alignment(right)]

# <br>
# <br>
# <br>
# Third, _decide_ on
# the right **tools**

---

# Say it again

1. First, _define_ the **state** and the **constraints**
1. Second, _decide_ on an execution **strategy**
1. Third, _decide_ on the right **tools**

^ Lets look at how we did walked through these steps for Amon Carter.

---

# First, _define_ the **state** and the **constraints**
## Why were we doing this for the Carter?

> Create an easy-to-use and accessible collections explorer. The collections explorer will highlight the Carter’s dynamic collection and act as a digital extension of the in-gallery experience.

<!-- Create a best-in-class Collections Explorer for both researchers and the general public that integrates Amon Carter’s Art and Archive collections -->

^ less technical client so we had braod strokes vs hard rukes

---

[.build-lists: true]

# First, _define_ the **state** and the **constraints**
## Starting Development

* AC's IT team had set up a pipeline of their Collection Data and Raw media to their DAMs
* Custom Data Structures (but in JSON)
* Did not need immediate updates
* Low volume of updates
* Wanted all the imagery **in** the CMS

^ We are lucky with most museums that we don't need instantanious/real-time updates.
We were told low volume of updates
I forget why, but all imagery in the CMS

^ We created more constraints as we worked through the process.

---

---

# Second, _decide_ on an execution **strategy**
## Syncing Strategies

1. Use live external endpoints

^ I would say not recommended, but there are some use cases.
THF is a good example of the use case. [todo pics!]
Connection to Github (to display open tickets) [todo pics!]
NOT an option for AC

---

# Second, _decide_ on an execution **strategy**
## Syncing Strategies

1. Use live external endpoints

![right fit](media/thf_sync.mp4)
# todo get vid of Ryan's work

^ I would say not recommended, but there are some use cases.
THF is a good example of the use case. [todo pics!]
Connection to Github (to display open tickets) [todo pics!]
NOT an option for AC

---

# Second, _decide_ on an execution **strategy**
## Syncing Strategies

1. Use live external endpoints
1. Save raw data, process on the fly

^
Where do you want the lift to be?
**Will the end user be affected by this?**
Ex: Wikidata bio fields
“Fallback content” - could process on the fly
 * Process thousands of pieces of data with an unknown amount actually needed.
 * Assuming “Important” content will not need fallbacks

---

# Second, _decide_ on an execution **strategy**
## Syncing Strategies[^*]

1. Use live external endpoints
1. Save raw data, process on the fly
1. Bring all data into Drupal Entities, _nodes and taxonomies etc._

[^*]: A few more we’ll talk about later, but these were the options I had in my mind at the time for AC.

^ Most robust
How much do we need to “Drupalize” all the data? I may need taxonomies for other parts of the site to build views or determine “related” content.

---

# Second, _decide_ on an execution **strategy**
## Syncing Strategies - Solution

[.text-strong: #ff0000]
1. Use live external endpoints
1. Save raw data, process on the fly
1. **Bring all data into Drupal Entities, _nodes and taxonomies etc._**

 <!-- todo - video building a field... -->

^ Unfortunately I don't rememebr the exact why's on these decisions.

^ We had a lot of timing issues to work with checking for updates. So queueing up needed to be custom and partially just continued.

^ I had used search_api in the past, but ...I was a configurer but didn't understand the nuts and bolts.

---

# Second, _decide_ on an execution **strategy**
## Syncing Strategies - Solution

### We wanted to “Drupalize” all the data
  1. Needed related data, data was not in a silo

^
We're relating artworks and artists in content throughout the site.

---

# Second, _decide_ on an execution **strategy**
## Syncing Strategies - Solution

### We wanted to “Drupalize” all the data
  1. Needed related data, data was not in a silo
  1. Content was going to be enhanced (added fields and content and display options) in the CMS

^
Needed a ref for content authors.

---

# Second, _decide_ on an execution **strategy**
## Syncing Strategies - Solution

### We wanted to “Drupalize” all the data
  1. Needed related data, data was not in a silo
  1. Content was going to be enhanced (added fields and content and display options) in the CMS
  1. Search API indexing [^**]

[^**]: honestly not needed, but I didn’t fully understand that at the time

^
At this point, I had used search_api in the past, but ...I was a "configurer" but didn't understand the nuts and bolts.

---

^
-->

---

# Third, _decide_ on the right **tools**
## What tools exist?

* Migrate Module

^ Migrate module
History of migrate: D->D

---

# Third, _decide_ on the right **tools**
## What tools exist?

* Migrate Module
* Feeds Module

^ Feeds __module__
History of feeds: Ingesting RSS, XML feeds

---

# Third, _decide_ on the right **tools**
## What tools exist?

* Migrate Module
* Feeds Module
* Custom Code

^
Custom Code
* Extra effort
* Technical debt

---

# Third, _decide_ on the right **tools**
## What tools exist?

* Migrate Module
* Feeds Module
* Custom Code
* External to CMS

^ Not sure what conditions I would suggest this.
You really have to know what you're doing
Let Drupal, **Drupal**
(especially writing directly to the DB, or at least to drupal’s tables)

---

# Third, _decide_ on the right **tools**
## What tools exist?

* Migrate Module
* Feeds Module
* **Custom Code**
* External to CMS

---

^
I like to reinvent the wheel, b/c i obvisouly can do it better...

^
--> So lets look at some more technical reasons.

---

# Third, _decide_ on the right **tools**
## What tools exist?

### Timing and queueing the updates required a custom code solution

<br>

---

[.build-lists: true]

# Third, _decide_ on the right **tools**
## What tools exist?

### Timing and queueing the updates required a custom code solution

1. Grab Data
2. Add item to a Queue Worker(s)
3. Process Item in the queue at a later time

![inline](media/horizontal-flow.jpg)

---

# Third, _decide_ on the right **tools**
## What tools exist?

### Custom Code

Actual ingestion of data could have been Feeds or Migration, but would have required some custom tampering, or migration processes[^***]

[^***]: I always go back and forth, b/c I want to do it the “Drupal way” but reality is you will still need custom code.

---

---

# Things we learned

* Dealing with Image files
  * Text is fast, images (files) are not
  * How to detect new images
* Custom Code
  * Error catching and handeling
  * Proper reporting for what fails
* Reliability of your external data sources
* Dates
* Pre-caching

^
What worked and what did not.  (5 mins)
Dealing with images - should spend a lot more time thinking about this.
Slow external API.
B/c of custom code, we needed to add in more error checking and handling after the fact. We weren’t handling failure well or able to debug why failures were happening.
Date strings to date objects.
During maintenance, second queue to pre-cache teaser views of artwork content

---

# Future Thougths and Strategies

* “Synced data Entities” connected to “Enhanced Data” nodes
* Bringing in majority of data to custom database tables
* Re: Search API, writing custom index plugins is really easy (Once you figure it out)

^
Future Strategies  (5 mins)
“Synced data Entities” connected to “Enhanced Data” nodes.
Current project, bringing in majority of data to custom DB tables
Speeds up syncing (less entities for complicated data)
Speeds up development time
If I need to “Drupalize” specific data, I can in the future.
Code is a bit more in-line with “Drupal code”
I could be wrong about this, but I'd like to think it's true.
Re Search API, writing custom index plugins is really easy (Once you figure it out)

---

# Thank you!

### Questions?
### Comments?
### Discussion?
### Feedback?

^
QA (rest)

---


---


---


---


---


---


---


---


---


---


---


---


---


---

[.header: #FF0000, alignment(center), line-height(20), text-scale(2.0)]
<br>
# OLD Structure

---

# Why are we talking about this today?

## What was the purpose for the Carter?

> Create an easy-to-use and accessible collections explorer for the Amon Carter Museum of American Art. The collections explorer will highlight the Carter’s dynamic collection and act as a digital extension of the in-gallery experience.

Create a best-in-class Collections Explorer for both researchers and the general public that integrates Amon Carter’s Art and Archive collections

![right fit autoplay mute](media/ce_walkthrough.mp4)

^ How do we think about doing this?

---

[.text: alignment(center)]
# <br>
# <br>
# <br>
# First, _define_ the **state**
# and the **constraints**


^
First, define the state and constraints. (8 mins) [???]
AC’s IT team had set up a pipeline of Collection Data, Raw imagery => DAMs.
Custom Data Structures (but in JSON)
(Timing) Didn’t need immediate updates.
Low volume of updates (proved to be inaccurate)
Wanted all the imagery IN the CMS.

---

# First, _define_ the **state** and the **constraints**

* AC's IT team had set up a pipeline of their Collection Data and Raw media to their DAMs
* Custom Data Structures (but in JSON)
* Didn’t need immediate updates
* Low volume of updates
* Wanted all the imagery **in** the CMS

^
First, define the state and constraints. (8 mins) [???]

^ - AC’s IT team had set up a pipeline of Collection Data, Raw imagery => DAMs.

^ - Custom Data Structures (but in JSON) **MEANING NO CONTRIB TO HELP OUT**

^ - (Timing) Didn’t need immediate updates.

^ - Low volume of updates (proved to be inaccurate)

^ - Wanted all the imagery IN the CMS.

---

[.text: alignment(center)]
# <br>
# <br>
# <br>
# Second, Decide on an
# Execution **Strategy**

^
Second, Decide on an Execution Strategy (10 mins) [???]

---

# Second, Decide on an Execution **Strategy**

1. Syncing Strategy
1. Syncing Tools

---

# Second, Decide on an Execution **Strategy**
## Syncing Strategies[^1]

1. Use live external endpoints
1. Save raw data, process on the fly
1. Bring all data into Drupal Entities, _nodes and taxonomies etc._

[^1]: A few more we’ll talk about later, but these were the options I had in my mind at the time for AC.


^
Syncing Strategies
Use live external 3rd party Endpoints
Not recommended
THF is a good example of the use case.
Connection to Github (to display open tickets)
NOT an option for AC
Save raw data, process on the fly
Where do you want the lift to be?
Will the end user be affected by this?
Ex: Wikidata bio fields
“Fallback content”
Process thousands of pieces of data with an unknown amount actually needed.
Assuming “Important” content will not need fallbacks
Bring all data into Drupal Entities, nodes/taxonomy etc.
How much do we need to “Drupalize” all the data? I may need taxonomies for other parts of the site to build views or determine “related” content.
A few more we’ll talk about later, but these were the options I had in my mind at the time for AC.


^ todo: build these out with comments on each slide.

---

# Second, Decide on an Execution **Strategy**
## Syncing Tools

* Migrate Module
* Feeds Module
* Custom Code
* External to CMS

![right fit 12%](media/IMG_1888.JPG)

^
Strategies for ingesting
Migrate module
History of migrate: D->D
Feeds module
History of feeds: Ingesting RSS, XML feeds
Custom Code
Technical debt
External to CMS
Not sure what conditions I would suggest this. (especially writing directly to the DB, or at least to drupal’s tables)

^ todo: build these out with comments on each slide.

---

# Amon Carter Solutions

## We wanted to “Drupalize” all the data
  1. Needed related data, data was not in a silo
  1. Content was going to be enhanced (added fields and content and display options) in the CMS
  1. Search API indexing [^2]

[^2]: honestly not needed, but I didn’t fully understand that at the time

---

# Amon Carter Solutions

## Timing and queueing the updates required a custom code solution

1. Grab Data
1. Add item to a Queue Worker(s)
1. Process Item in the queue at a later time


---

# Amon Carter Solutions

## Custom Code

Actual ingestion of data could have been Feeds or Migration, but would have required some custom tampering, or migration processes[^3]

[^3]: I always go back and forth, b/c I want to do it the “Drupal way” but reality is you will still need custom code.

---

^
AC Solution [diagrams from past presentations]
AC - decided we wanted to “Drupalize” all the data.
Needed related data, data was not in a silo.
Content was going to be enhanced (added fields and content and display options) in the CMS.
Search API indexing (honestly not needed, but I didn’t fully understand that at the time)
Timing and queueing the updates required a custom code solution. Which (of course) led to the entire thing being custom code.
Typical solution I use for a lot of things
Grab Data
Add item to a Queue Worker(s)
Process Item in the queue at a later time
Actual ingestion of data could have been Feeds or Migration, but would have required some custom tampering, or migration processes.
I always go back and forth, b/c I want to do it the “Drupal way” but reality is you will still need custom code.

---

# Things we learned

* Dealing with Image files
  * Text is fast, images (files) are not
  * How to detect new images

* Reliability of your external data sources
* Custom Code
  * Error catching and handeling
  * Proper reporting for what fails
* Dates
* Pre-caching


^
What worked and what did not.  (5 mins)
Dealing with images - should spend a lot more time thinking about this.
Slow external API.
B/c of custom code, we needed to add in more error checking and handling after the fact. We weren’t handling failure well or able to debug why failures were happening.
Date strings to date objects.
During maintenance, second queue to pre-cache teaser views of artwork content


---

# Future Thougths and Strategies

* “Synced data Entities” connected to “Enhanced Data” nodes
* Bringing in majority of data to custom database tables
* Re: Search API, writing custom index plugins is really easy (Once you figure it out)

^
Future Strategies  (5 mins)
“Synced data Entities” connected to “Enhanced Data” nodes.
Current project, bringing in majority of data to custom DB tables
Speeds up syncing (less entities for complicated data)
Speeds up development time
If I need to “Drupalize” specific data, I can in the future.
Code is a bit more in-line with “Drupal code”
I could be wrong about this, but I'd like to think it's true.
Re Search API, writing custom index plugins is really easy (Once you figure it out)

---

# Thank you!

### Questions?
### Comments?
### Discussion?

^
QA (rest)

---


---
