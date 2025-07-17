# 1. 🧾 Handover Document – David Anderson
**Role:** Cross Product Platform Architect  
**Period:** [February 17 2020] – [July 18 2025]

[1. Executive Summary](#1-executive-summary)  
&nbsp;&nbsp;&nbsp;&nbsp;[2. Role Description](#2-role-description)  
&nbsp;&nbsp;&nbsp;&nbsp;[3. Key Feature Deliverables](#3-key-feature-deliverables)  
&nbsp;&nbsp;&nbsp;&nbsp;[4. Tools, Systems, & Processes](#4-tools-systems--processes)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4.1 Confluence](#41-confluence)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4.2 Plantuml Diagrams](#42-plantuml-diagrams)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4.3 Drawio Diagrams](#43-drawio-diagrams)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4.4 Cross Product ILDs](#44-cross-product-ilds)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4.5 Github](#45-github)  
[5. Challenges Encountered](#5-challenges-encountered)  
[6. Final Thoughts](#6-final-thoughts)  

---
## 1. Executive Summary

The primary objective was to provide architectural leadership to enable the Cross Product Value Stream to deliver a simple, compliant, and fit-for-purpose suite of products for ANZ. This included establishing the tools and processes required for effective and efficient product management.

> As Alexis de Tocqueville said, “The most difficult part of a revolution, like the most difficult part of a novel, is inventing the end.” 

Reflecting on the journey, the landscape has evolved significantly; new leadership, shifting priorities, and fresh perspectives are shaping the next chapter for ANZx.

I look forward to seeing how the next phase unfolds and hope to contribute again in the future if the opportunity arises.

---

## 2. Role Description

My role included:

- Defining the architecture to enable the build out of the required Product and Pricing capabilities.
- Supporting delivery teams in understanding the prescribed architecture and elaborating delivery views.
- Identifying and managing technical debt arising from sub-optimal delivery or design decisions.

---

## 3. Key Feature Deliverables 

<table>
    <thead>
        <tr>
            <th>Feature</th>
            <th>Description</th>
            <th>Your Role</th>
            <th style="width:50%; vertical-align:top;">Reflection</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td style="vertical-align:top;">ANZx Product Catalog</td>
            <td style="vertical-align:top;">Model/Configure the ANZX Product Catalog and expose via API</td>
            <td style="vertical-align:top;">
                Document <a href="https://confluence/display/ABT/Architecture+Summary+-+Zafin">Zafin Architecture</a> which includes data, integration and infrastructure views.
            </td>
            <td style="vertical-align:top;">
                The Zafin model is very verbose and complex which made adoption harder than it probably should.<br><br>
                The Model evolution was essentially driven by Zafin based on specific business requirements. While Zafin consultants could leverage use cases from other customers, the model updates appeared to be bespoke.<br><br>
                A Mulesoft Product Capability Service was deemed necessary to address the following issues:
                <ul>
                    <li>Orchestration of multiple Zafin APIs to simplify access to all/parts of the product catalog</li>
                    <li>Enabling eTag support</li>
                    <li>Error handling</li>
                </ul>
                In hindsight, Zafin should have supplied a <a href="https://bian.org/servicelandscape-12-0-0/views/view_53726.html">BIAN</a> aligned/compliant product model and restful services.
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Product Data Distribution</td>
            <td style="vertical-align:top;">Distribute Product Catalog to the ANZx constituents</td>
            <td style="vertical-align:top;">
                Document the <a href="https://confluence/display/ABT/001+Product+Distribution">Zafin Architecture Increment</a> which covers how Product Data is shared with <a href="https://what.apps.anz/cap">CAP</a>, Fabric and Stravinsky.<br><br>
                Document the<a href="https://confluence/display/ABT/006+Lightning+Product+Hub"> Lightning Product Hub Architecture Increment</a> which incldues the Lightning Data Model and associated source to target mappings.
                <br><br>
                Got agreement regarding the <a href="https://confluence/display/ABT/CPP-053+Product+Synchronisation+Roadmap+Planning">Product Distribution Roadmap</a> justifying the introduction of the Lightning Product Hub.
            </td>
            <td style="vertical-align:top;">
                The current solution to Product Distribution is transitional as per the Lightning Product Hub Roadmap.<br><br>
                The Product Model is being extended using BIAN/Open Banking as a reference model on a usecase by use case approach.<br><br>
                Remaining configuration items relate to Fee and Campaigns being passed to <a href="https://what.apps.anz/cap">CAP</a>.<br><br>
                Once these items have been incorporated into the Lightning's Product Hub, it is possible to decommission the Mulesoft CAP Experience API and associated Stargate workflows.<br><br>
                Fabric and Stravinsky are using the Mulesoft Product Capability Service, and ideally they should move to the Lightning Product Service or consume product update events published by the Product Hub.<br><br>
                Lex and Salesforce are sourcing product information via the Lightning's Product Service.<br><br>
                In hindsight, understanding non functional requirements in terms of volumes, means response times and availability is critical. Zafin service levels are mediocre at best and the Cross Product Platform needed to compensate to ensure Customer experience is not jeopordised.  
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Rest of Bank Publication</td>
            <td style="vertical-align:top;">
                Publish ANZx Product to Rest of Bank (RoB).<br><br>
                RoB includes Treasury, Finance, Risk etc.
            </td>
            <td style="vertical-align:top;">
                Provide Architecture to support distribution of Product Information from (Zafin SaaS) to ANZ On-Prem.<br><br>
                Support Design and Build of the Product File to be passed to ANZ RoB.<br><br>
                Assist RoB stakeholders in understanding what and how to access the product information provided.
            </td>
            <td  style="vertical-align:top;">
                On the surface this appears to be a comparatively simple ask which involved establishing a new integration pattern to support <a href="https://what.apps.anz/saas">SaaS</a> to ANZ On-Prem.<br><br>
                In reality it became a delivery nightmare hampered by evolving standards, technology and changes in organisational structures.<br><br>
                <a href="https://what.apps.anz/cpp">CPP</a> had autonomous delivery capability initially in the build out of Dataflows, however this responsibility moved to the Data Enablement delivery stream and inherited a number of technical debt items.<br><br>
                Some of these have been resolved with the introduction of Stargate, however we are still left with needing to deal with Zafin information being stored/accessed using <a href="https://what.apps.anz/dgcp">dGCP</a>.<br><br>
                The product information used by RoB is in a key-Value-Pair format, where the key is a specific name location in the <a href="https://what.apps.anz/json">JSON</a> response provided by Zafin/Mulesoft Experience API.<br><br>
                Given the Zafin message verbosity, this file is large and key values are long.<br><br>
                While this data format meets generic requirements, it requires intimate knowledge to be able to consume it and processes to be in place to deal with breaking schema changes introduced via Zafin API evolution.<br><br>
                The way forward is to move away from supporting the delivery of a KVP file to introducing consumption views from the Lightning Product & Pricing Data Product.<br><br>
                Data minded people, preferably with <a href="https://bian.org/servicelandscape-12-0-0/views/view_53726.html">BIAN</a> knoweldge, will be rquired to make this a reality. What data products are needed and who ultimately supports them needs to be planned, owned and resourced accordingly.
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Open Banking Products</td>
            <td style="vertical-align:top;">Provide Product Details to meet Open Banking Obligations</td>
            <td style="vertical-align:top;">
                Architecture, design and mapping support of Zafin Product Information to the Open Banking format.
            </td>
            <td style="vertical-align:top;">
            Once again what would/should have been a relatively simple ask, was made rather complicated due to the evolving Zafin model, product config was being updated regularly and the Zafin model did not natively support the Open Banking data requirements.<br><br>
            A Mulesoft Experience API was developed internally to manage these necessary transformations using logic and at times incurring technical debt to address Zafin model gaps.<br><br>
            Changes which should have been made via Zafin config required coding changes to implement.<br><br>
            Thankfully now, this has been resolved, to the point where all open banking product publications are managed via Zafin config and made available via API.<br><br>
            Zafin updates are only required when <a href="https://consumerdatastandardsaustralia.github.io/standards/#cdr-banking-api_get-product-detail">Consumer Data Standards updates the product details</a> data requirements.<br><br>
            The simplicity of the Open Banking standard allowed the <b>Get Help squad</b> to use this Open Banking endpoint to source rates to be displayed on <a href="https://www.anz.com.au/plus/interest-fees/">marketing websites</a> and for the terms of conditions within the mobile application.
            <br><br>
            <img src="img/rates.png" alt="Example of Zafin supplied rates" width="600"/>
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Product Manual Management</td>
            <td style="vertical-align:top;">Manage Product Terms and Conditions & collateral requried </td>
            <td style="vertical-align:top;">Journey Expert & Architecture</td>
            <td style="vertical-align:top;">
            In the past, ANZ has spent big money on needing to Find, Fix and Remediate banking issues and to subsequently compensate impacted customers.<br><br>In support of this process, there is a need to have an authoritative source of product information and detailed knowledge of the end to end processing.<br><br>At ANZx, the Product Manual was the document to be used to collate all the necessary information.<br><br> The creation of this document was commissioned to KPMG.<br><br>Emailing Microsoft word documents was not going to cut it.<br><br>My involvement was very broad with deliverables ranging from:
            <ul>
                <li>Documenting <a href="https://confluence/pages/viewpage.action?pageId=691649940">use case and non-functional requirements</a></li>
                <li>Building a <a href="https://confluence/pages/viewpage.action?pageId=780818484">prototype workflow using Box</a> </li>
                <li>Architectural assessment of ClauseMatch (halted due to partial Russian ownership)</li>
                <li>Transition responsibilities across to the <strong>document services</strong> team</li>
            </ul>
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Cross Product Architecture</td>
            <td style="vertical-align:top;">Mantain Cross Product Architectural Assets.</td>
            <td style="vertical-align:top;">Maintain the following Architectural documents
                <ul>
                <li><a href="https://confluence/display/ABT/Architecture+Summary+-+Zafin">Zafin Solution Architecture & Design</a> needs updating to reflect new controls framework</li>
                <li><a href="https://confluence/display/ABT/Architecture+Summary+-+Lightning">Lightning  Solution Architecture & Design</a> needs updating to reflect new controls framework</li>
                <li><a href="https://confluence/pages/viewpage.action?pageId=2455944403">CAP Architecture Summary</a> - hand balled to Rick Dowling</li>
                <li><a href="https://confluence/pages/viewpage.action?pageId=864870868">CTM Architecture Summary</a> hand balled to Rick Dowling</li>
                <li><a href="https://confluence/pages/viewpage.action?pageId=864870936">Cross Product Platform ETL Solution Arch & Design (decommissioned)</a> nothing to do here</li>
                <li><a href="https://confluence/pages/viewpage.action?pageId=1161045123">Cross Product Platform Position Paper</a> - Could do with a refresh</li>
                <li><a href="https://confluence/display/ABT/Cross+Product+Platform+-+Technical+Roadmap+-+ANZx+Overall+Architecture">Cross Product Platform Roadmap</a> - last updated Feb 2024, so is probably due for an update</li>
                <li><a href="https://confluence/display/ABT/Cross+Product+Layer+Capabilities">Cross Product Platform Architecure Decision Records</a></li>
                <li><a href="https://confluence/pages/viewpage.action?spaceKey=ABT&title=CPP+Decision+Register">Cross Product Platform Design Decisions</a></li>
                </ul>
            </td>
            <td style="vertical-align:top;">
            Not sure where we stand with PAC-001, but the <a href="https://confluence/display/ABT/Solution+Overview+-+Peer+review+and+approval">process to review, apply feedback and managing version of the Solution Arch and Design</a> is rather clunky.<br><br>
            It is also not clear just how important the Solution Architecture & Design document is. Over the 5 years I have been keeping these documents up to date, seldom has an initiaitve lead, product owner, security partner or engineering squad ever referenced them or provided direct feedback to them outside the PAC-001 cycle.<br><br>Ok, the security partner may use the <a href="https://what.apps.anz/ild">ILD</a> for preparing a <a href="https://what.apps.anz/sav">SAV</a>, but these ILDs are generally only useful at an increment level.<br><br>
            Personally, I believe everything we need to know about an asset should be in Service Now. All business, application, information and technology views should be version controled with automated policy checking in place to ensure document is fit-for-purpose, aligns with standards, uses approved patterns and most importantly is aligned from a wholistic system perspective.<br><br>
            Personally Business and Technolgy Roadmaps should be data driven and also navigatable from Service Now. In ANZx the Techncial Roadmaps were manufactured in a botton up approach and aligned during the review stage. Feedback received includes the roadmap is too detailed, presented as a laundry list of backlogged jira stories, didn't really paint a picture of where <a href="https://what.apps.anz/cpp">CPP</a> needs to be in 5 years time, what are the gaps, the dependancies with the other roadmaps. Still not sure we have nailed what this needs to look like.
            </p>
            My ADRs:<br>
            <img src="img/adr.png" alt="ADR Dashboard" width="600"/><br>
            My CPP Decisions:<br>
            <img src="img/cpp-decisions.png" alt="CPP Decision Dashboard" width="600"/><br>
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Cross Product Situational Controls</td>
            <td style="vertical-align:top;">Automate Controls to support consistency checking between Zafin and ANZ systems.</td>
            <td style="vertical-align:top;">Architect and Data Analyst</td>
            <td style="vertical-align:top;">Wow, this was an awesome piece of work if I do say myself.<br><br>When I started this gig, there was big talk about how we are delivering a platform which will scale, be reliable, cloud native etc. In the early days of thhe first produtct pilot, Cross Products had people logging into <a href="https://what.apps.anz/cap">CAP</a> and checking how many deposit accounts had been created and that they all looked ok. Every day, for 6 months, we had around 10 control checks being performed manually.<br><br>Check out this <a href="https://confluence/display/ABT/CPP+Showcase+Videos?preview=/733737189/802365038/CPP%20CONTROLS.mp4">show case video</a> that Mon put togther which describes the CPP control framework.<br><br>
            The automation of these validity and consistency checks started off with an <a href="https://confluence/display/ABT/CPP-028+Cross+Product+Data+Compliance+Detection">ADR</a> co-authored wth Surjit Rangi (Data Architect at the time) and then worked closely with <a href="https://what.apps.anz/xde">xDE</a> delivery team assigned (primarily as a Data Engineer) to build out the necessary views and rules to automate 6 key situational controls required by the Cross Product Value stream.<br><br>
            I have learned heaps, which included <a href="https://what.apps.anz/dbt">DBT</a>, BigQuery, Tableau and I wrote thousands of lines of code to build the sql views and associated data quality rules.json.
            <br><br>
            I enjoyed the challenge and opportunity to do this and happy to know that my work contributed to establishment of a solution which is being used across most of the other ANZx Value Streams.
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Pricing</td>
            <td style="vertical-align:top;">Rate and Fees associated with Products</td>
            <td style="vertical-align:top;">Architect</td>
            <td style="vertical-align:top;">A key capability to be delivered by Zafin was to provide Rates and Fees for all ANZx accounts, be it deposit or lending.
            <br><br>The orginal Architecture was to send Zafin lots of data, customer and account information, and Zafin will work out if any fees are to be charged and notify <a href="https://what.apps.anz/cap">CAP</a> of any Rate updates (the next day).<br><br>
            The original architecure proposed an <a href="https://what.apps.anz/etl">ETL</a> orientated solution where:
            <ul>
            <li>End of day account extracts were to be supplied by <a href="https://what.apps.anz/cap">CAP</a>, Customer relationships would come from <a href="https://what.apps.anz/ocv">OCV</a>.</li>
            <li> The Zafin result files needed to delivered to <a href="https://what.apps.anz/cap">CAP</a> before the start of <a href="https://what.apps.anz/cap">CAP</a>'s batch around 2am.</li>
            </ul>
            This gave an end to end processing window of 2 hours. Ample time when everything works as expected, however not much wiggle room if there were any problems encountered along the way.<br><br>
            Given the customer and account data that was required by Zafin was already being delivered to the google platform, a decision was approved to source the necessary data from <a href="https://what.apps.anz/dgcp">dGCP</a>.<br><br>On the surface this seemed reasonable, however it ended up being a bad decision as the service levels provided by <a href="https://what.apps.anz/dgcp">dGCP</a> were not at the level required.<br><br>
            A number of failures were experienced and ultimately the <a href="https://what.apps.anz/etl">ETL</a> jobs were put ice, and a tactial solution was quickly developed by the <a href="https://what.apps.anz/cap">CAP</a> Deposits team which worked for 12 months or more.<br><br> 
            We were in search of a strategic solution. A couple of ADRs, lots of workshops with Zafin architechts and product representatives and raft of <a href="https://confluence/pages/viewpage.action?spaceKey=ABT&title=CPP+Decision+Register">CPP Decisions</a> which was the genesis of the Pricing Service.<br><br>
            At the time, the Cross Product Platform Value Stream did not have ANZx type engineering capability. Stuff got done based on jira epics and managing many overloaded delivery partners. It always seemed a lot harder than it needed to be.<br><br>
            In response to this, the Lightning squad was formed things changed immediately. Personally I felt we are now building something, rather than raising/managing jira tickets. We transformed from being <a href="https://en.wikipedia.org/wiki/The_Chicken_and_the_Pig">chickens to pigs</a>. <br><br>
            Long story short, Lightning is real and helping deliver product and pricing services requried by the ANZx ecosystem, including the Pricing Service which syncronises Lending Accounts and Subscriptions (see below for more) wth Zafin.<br><br>
            I am immensely proud of my contribution to this point and helping shape <a href="https://confluence/display/ABT/11.4.1+Multi-Price+Products+to+enable+Personalised+Pricing">negotiated/personalised pricing</a> to meet future pricing capability<br><br>
            An awesome part of the discovery work for this service inclduded working with Khanin to model and execute the pricing service. The objective if this work was to help set SLO expectations, and influence the design of the pricing service.<br><br>
            See the following <a href="https://confluence/display/ABT/Discendi+Tempus+%28Learning+time%29+Talks#:~:text=David%20Anderson-,Process%20Mining%20and%20Predictive%20Simulation,-Process%20mining%20is">Discendi Tempus</a> presentation using Apromore. The huge learning here is that the Zafin contractual SLO of less than 1 second, 90% of the time over a 30 minute window introduces risk that a customer user expeience can be impacted due to high volumes with an unreliable network endpoint.  
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Offers & Rewards</td>
            <td style="vertical-align:top;">How to attract and engage customers</td>
            <td style="vertical-align:top;">Architect</td>
            <td style="vertical-align:top;">The <a href="https://confluence/display/ABT/002+Lightning+Offers+Service">Offer service</a> was an early service built and delivered by Lightning and involved socialising an architecture and the associated <a href="https://confluence/display/ABT/Welcome+Rate+Delivery+View">delivery view</a> with parties from Zafin, Lightning, Mulesoft, Stravinsky, <a href="https://what.apps.anz/cap">CAP</a>, APIMesh and Cosmos. I call out this diagram, as it was one of my first Gliffy diagrams using Layers. How to do layers was a gift from Bob, which has been passed on to others. So many thanks Bob.<br><br>
            The Offer Service and <a href="https://what.apps.anz/cap">CAP</a>'s Campaign capabilities became the enabler for the qualified saving product.<br><br>
            The Offer Service built does have a number of technical debts items associated with it. Things like it eligibility checks are coded in the service and not driven off Zafin config, does not yet support joint applications, and does not support multiple offers for a product. So it is likely uplift would be required to support credit card offers.<br><br>
            Refer-A-Friend was an interesting usecase which tested which Valaue Stream owns the offers and rewards capability. The build out of this capability was a set of fabric services which were controls via Zafin Offer configuration and the services were later transfered across to Lightning to manage support and future changes. This architecture was put in place largely by Matt Rankin which leveraged COSMOS provide capabilities to listen for speific events and track whether a customer has met the criteria, as per offer configuration from Zafin, for when a reward payment for the referal is be made.<br><br>
            The customer take up of this campaign was incredible and really boosted the number of ANZ Plus accounts. It was so popular that the camapign has to be cut short due to the reward payments budget was exhausted. My involvement in delivery was consulting only, however <a href="https://what.apps.anz/cpp">CPP</a> ended up either winning/losing the turf war and I was then tasked with uplifting the <a href="https://confluence/display/ABT/003+Lightning+Rewards+Service">Lightning Architecture</a>. 
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Subscriptions</td>
            <td style="vertical-align:top;">Provide a generic service to enable a feature</td>
            <td style="vertical-align:top;">Architect and pseudo Product Owner</td>
            <td style="vertical-align:top;">
            Off the back of some awesome architecture work for the Loan Offset feature from Chris Gavin, Steve Perry and Leng Poh, I was asked to provide architecture support to the Lightning sqaud to deliver the Subscription Service.<br><br>
            In large this was a good assignment and I enjoyed working with some very talented engineers both from Lighting and Lex.
            <br><br>
            Offset requirements were well understood, but there were some Zafin requirements around the calculation of the <b>Paid Up to Date</b> which were not identified in time resulting in some technical debt for this value to be calculated within the Subscrption service. <br><br>
            I believe this debt has been resolved from a Zafin perspective, however Lightning Subscription Service rework has not been prioritied.<br><br>
            Subscription Fee Amount displayed to the customer on the Offset Feature screen, I believe, is hard coded in Lex. Should be sourced from Pricing Service<br><br>
            Current solution does not support subscription fee discounting or waiving. Some consideration were included in the Personalised Pricing roadmap.<br><br>
            How to support pro-rata refunds has not been agreed to either.
            </td>
        </tr>
        <tr>
            <td style="vertical-align:top;">Store</td>
            <td style="vertical-align:top;">Provide a Marketable View of products ANZ want to sell to our Customers</td>
            <td style="vertical-align:top;">Architect</td>
            <td style="vertical-align:top;">
            Support Sandip and Matt Rankin in the build out of the <a href="https://confluence/display/ABT/008+Lightning+Product+Store">Lightning Store Service</a> and it's evolution as the Marketing Proposition concept is being introduced into Zafin.<br><br>
            This work is not without challenges as there are contributors across different delivery partners.<br><br>
            Not sure if there is any further architecture work here, but Kat needs support, Wayne may too, and sometimes Tim requires clarificartion or guidance around where certain things get done. I assume Ginni will be provide this support as required.
            <td>
        </tr>
    </tbody>
</table>

---

## 4. Tools, Systems, & Processes 

### 4.1 Confluence

All Cross Product Platform Architecture can be found in the following confluence locations.

#### 4.1.1 ANZX Architecture lives here

These are the prescribed views as per the prescribed ANZx templates and are subject to the ARCX process to review/approve process.

```
|   C. Team Spaces
|   ├── Architecture
│   |   ├── ANZx Overall Architecture
│   |   |       └── Roadmap - ANZx Overall Architecture
│   |   |           └── Technical - Roadmap - ANZx Overall Architecture
│   |   |               └── Cross Product Platform ...
│   |   ├── ADR Register
│   |   |       └── Cross Product Layer Capabilities
|   |   |       └── CPP-### Architectural Decision
│   |   ├── Solution Architecture & Design
│   │   ├── CAP for ANZx - Solution Arch & Design
│   │   ├── CTM for ANZx Solution Arch & Design
│   │   ├── Lightning - Solution Arch & Design
|   │   │   ├── Solution Architecture Overview - Lightning
|   │   │   ├── Architecture Increments - Lightning
|   │   │   └── Lightning - Solution Overview Approval
│   │   ├── Zafin - Solution Arch & Design
|   │   |   ├── Solution Architecture Overview - Zafin
|   │   |   ├── Architecture Increments - Zafin
|   │   |   └── ZAFIN - Solution Overview Approval
│   |   ├── Position Papers
|   |   |   └── Position Paper - Cross Product Platform....
│   |   ├── ARCX Tech Debt Inventory
|   |   |   └── DEBT-##### 

```

#### 4.1.2 CPP Architecture Content

```
|   C. Team Spaces
|   ├── Cross Product Platform (CPP)
│   |   ├── CPP Architecture
│   |   └── CPP Decision Register
|   |       └── Decsion with cpp-architecture label 
|   ├── Business Services
|       └──  Business Service Domains
|            └──  Product & Pricing Management - (Lightning Platform)
│               └──  Lightning Decision Register
|                    └── LTN_D_#### Decision  

```

Here you will find the key views important to <a href="https://confluence/display/ABT/CPP+Architecture">CPP Architecture</a>.

<img src="img/cpp-architecture.png" alt="Example of CPP Architecture Landing Page" width="600"/>

We are all very good at creating content, unfortunately it is a little harder to keep that content up to date. When I see a page that needs some work, I tag it with one of the following labels and use the <b>Out of Date</b> tab to review/update or archive accoringly.

<img src="img/spring-clean.png" alt="Confluence Page Labels" width="200"/>

#### 4.1.3 Confluence Labelling Conventions

Confluence Lables have been extensively used across CPP Architecture content. These lables are used to dynamically/automatically build the key views indluded in the Asset and Capability views.

| Label Type   | Description                                   | Example of Usage      |
|--------------|-----------------------------------------------|-----------------------|
| Asset        | All to one or more assets | lightning, zafin, cap |
| Component        | Identifies a component of an asset | lightning-product-hub |
| Capability   | Denotes the function/feature or capability | product-distribution, pricing      |
| View Type   | Cold be a C4 model layer, Architectural view description  | context-view, container-view, data-view, infrastructure-logical-diagram       |

#### 4.1.4 Table Transformers
Some of my confluence pages I have put together started simple, but overtime have got more sophisticated. One great way to to help the Don't Repeat Yourself (DRY) principle is by using table transformers.

##### 4.1.4.1 Volumertics

I personally this was an awesome result and it was fun to put together. However, not sure how useful it is.

The <a href="https://confluence/display/ABT/Lightning+-+Volumetrics"> Lightning Volumetrics</a> page aggregates the volumetrics from each Lighting Service.

<img src="img/lightning-volumetrics.png" alt="Lightning Volumetrics" width="600"/>

And subsquently the volume of calls to the dependant systems.

<img src="img/dependancies.png" alt="Lightning Dependancies Volumetrics" width="600"/>

Clicking thru to a service showss the use cases volumes and associated assumptions to are used to produce the volume numbers.

<img src="img/subscription-volumetrics.png" alt="Lightning Subscription Service Volumetrics" width="600"/>

##### 4.1.4.2 Assets of Interest to CPP

The context view found in <a href="https://confluence/display/ABT/009+Lightning+support+for+ANZx+Credit+Cards">009 Lightning support for ANZx Credit Cards</a> includes a table of systems where th description and link to the architecture (be it in confluence/backstage) are sourced from <a href="https://confluence/display/ABT/Assets+of+Interest+to+Cross+Product+Platform">Assets of Interest to Cross Product Platform</a>


##### 4.1.4.3 CPP Definitions

The <a href="https://confluence/display/ABT/Cross+Product+Conceptual+Data+Model">Cross Product Conceptual Data Model</a> sources defintion for concepts from <a href="https://confluence/display/ABT/CPP+Definitions">CPP Definitions</a> which ideally is managed by Matt's team.

### 4.2 Plantuml Diagrams
<p>
The majority of my diagrams have been modelled using Plantuml.<br>
All Plantuml script is written using Visual Studio Code with the jebbs PlantUML extension.<br>
SVGs are generated and saved to confluence along with the script.
<br><br>
<img src="img/c4-context.png" alt="Sample C4 Contrxt view with associated PlantUML Script" width="600"/>
</p>

### 4.3 Drawio Diagrams
For complex diagrams I generally use the Drawio Confleunce Macro.

### 4.4 Cross Product ILDs
I have been looking after the Infrastructure Logical Diagrams for Zafin and Lightning.

Given the compexity, there is generally an <a href="https://what.apps.anz/ild">ILD</a> for each capabilitiy. eg Lightning Product Hub which focusses on Product Distribution.

I have shared my knowlege of how to add/update an <a href="https://what.apps.anz/ild">ILD</a> with Rick and Ginni who have both completed one PR each approved. But the reality is that you need to do a few <a href="https://what.apps.anz/ild">ILD</a>s before you get the hang of them.

Cindy, our current security partner, often does do a deep review of the <a href="https://what.apps.anz/ild">ILD</a>. She assumes nothing and makes sure the <a href="https://what.apps.anz/ild">ILD</a> is <a href="https://what.apps.anz/csra">CSRA</a> compliant. Something that the <a href="https://backstage.service.anz/docs/default/component/sysl-plus/domains/architecture/infra-modelling/">ILD tooling</a> does not guarantee.  Cindy has raised a concern that the <a href="https://what.apps.anz/ild">ILD</a> needs to be reviewed by the PO/Engineering before she gets engaged. This is a process that she is used to from the Classic processes. So maybe this is a David Glagovs conversation that needs to be had.

<img src="img/ild.svg" alt="Revised ILD Approval Work Flow" height="600"/>

We inheritied the Zafin folder structure from Peter Dutch and would have liked to consolidate them to make it easier to find things. But never got around to it.

Some ILDs are sitting in cosmos, cpp, and stargate folders.

Some learnings:
- Keep diagrams small; it is easier to have them reviewed and approved.
- Use release views and make sure you update the disposition of the nodes (new, extended, reused) and flows.
- All lines must have a protocol.

### 4.5 Github

All my plantuml script and prototype pages can be found in the <a href="https://github.service.anz/andersd7/ANZx-CPP-Architecture">andersd7/ANZx-CPP-Architecture</a> repository.

Check ouy my <a href="https://pages.github.service.anz/andersd7/ANZx-CPP-Architecture/index.html">sandbox github page</a>.

>I am not sure what will happen to this repository once I have left.

#### 4.5.1 Product Config Viewer

The <a href="https://pages.github.service.anz/andersd7/ANZx-CPP-Architecture/product-config-view.html">Product Config Viewer</a> provides a static, interactive view of product configurations from multiple Zafin environments (e.g., Pre-Prod, SIT-K, SIT-L, ST). It is built using HTML, JavaScript, Handlebars, Bootstrap, and several supporting libraries.

The page has been very useful for the Lightning engineers and other users who do not have access to Zafin via the UI or able to view Zafin/Mulesoft api responses via postman. 

##### 4.5.1.1 Key Features

- Environment Comparison: View and compare product configurations across different environments.
- Product Categories: Products are grouped by categories (Deposits, Term Deposits, Credit Cards, Mortgages, RuleSets, Offers).
- Interactive UI: Click on a category to expand and see products per environment. Click on a product, ruleset, or offer to view detailed configuration.
- JSON View: Show/hide the raw <a href="https://what.apps.anz/json">JSON</a> for any product, ruleset, or offer.
- Comparison Tool: Compare a product’s configuration between environments and view a visual diff.
- Extensible Templates: Uses Handlebars partials for modular rendering of product details.

##### 4.5.1.2 Usage

<img src="img/product-config-viewer.png" alt="Zafin Product Config Viewer" width="600"/>

- Click a product category to expand and see available products in each environment.
- Click a product, ruleset, or offer to view its details.
- Use the "Show JSON" button to view the raw configuration.
- Use the "Show Compare" button to compare the product with another environment.

##### 4.5.1.3 Technical Notes

- Data is loaded from static <a href="https://what.apps.anz/json">JSON</a> files for each environment.

| Data Type   |  JSON File Name          |  Mulesoft API Endpoint       |
|-------------|--------------------------|------------------------------|
| Product     | ####-Product.json        | ```{{mulesoft_host}}/product-catalog/v2/products?include=feePlans&include=serviceDetails&include=ratePlans&include=packages&include=multiUseProducts``` |
| Offers     | ####-Product.json        | ```{{mulesoft_host}}/product-catalog/v2/offers``` |
| Rulesets     | ####-Rules.json        | ```{{mulesoft_host}}/product-catalog/v2/ruleDefinitionDetails``` |

```
Where ####:
 - st : dev/system test
 - sitl : integration
 - sitk : end to end testing
 - preprod : pre production
```

- Handlebars templates and partials are used for rendering.
- Bootstrap Table is used for tabular data display.
- <a href="https://what.apps.anz/json">JSON</a> diffing uses jsondiffpatch for visual comparison.

---

## 5. Challenges Encountered 

- Dealing with 3 different delivery models ie ANZx, Zafin and Core Systems/Rest of Bank can get complicated.
- Although we do have dedicated CORE resources in the <a href="https://what.apps.anz/cpp">CPP</a> squad, they are generally a protected species. 
- Core Design doco, is generally word documents managed in Teams. Design doco is very <a href="https://what.apps.anz/cap">CAP</a> centric and difficult to review/understand. Core designs are reviewed and approved by the Core Design Council with little input of review from <a href="https://what.apps.anz/cpp">CPP</a> Architects. 
- At one point, I did have access to the <a href="https://what.apps.anz/cap">CAP</a> code repository. Now I have over 20 years experience in building system in cobol, however I could never make sence of the Hogan code. It is a dialect of it's own. My knowledge of <a href="https://what.apps.anz/cap">CAP</a> systems has been handed down to me from the Core folks. Self learning/discovery of Core systems is very difficult.  
- I have already banged on about how complex/bespoke the Zafin Product Model is. This is some what compunded by Zafin System documentation which is volumous in nature and very generic. Zafin doco is composed of a series of PDFs all seemingly 800+ pages. They do not describe ANZx's implementation nor provide a data model. This often leads to an unsustainable dependancy on consulting provided by Zafin resources and the need for modelling decisions to be vetted by the Zafin Architecture team.
- Product features and offers can be modelled in Zafin in a number of ways. We have used Zafin services to model visa debit card and savings goals. But it looks like we are now defining features using a Zafin Multiuse Product. To be honest, I do not really understand the reasoning here, but it is very unintuitive to me. This has been resolved using the Lightning Product Data Model which takes shape from <a href="https://bian.org/servicelandscape-12-0-0/views/view_53726.html">BIAN</a>  and <a href="https://consumerdatastandardsaustralia.github.io/standards/#cdr-banking-api_get-products">Open Banking</a>.  
- Many of the architectural diagrams we produce eg C4, UML and ILDs are not universally accepted by the delivery community. We are either asked to produce delivery views, or to review diagrams produced by journey experts/delivery leads. Which is OK, but it does add another interpreted perspective and work products that will need to be updated for it to be kept current.  

---

## 6. Final Thoughts 

Firstly, I’d like to thank Dave Pilcher and Dave Abela for the opportunity to join the Cross Product Platform team, and Bob Raman for his ongoing support throughout my 5.5 years on the project. The experience, learnings, and opportunities have been invaluable.

Thanks also to Sandip and the CPP Architecture team. The collective blend of knowledge, skills, and perspectives has been instrumental in shaping the end-to-end architecture and contributing to ANZx’s progress.

The ANZx Architecture team has been a great source of support and collaboration, always open to ideas and feedback. It’s been a privilege to work alongside such an accomplished group.

Appreciation goes to Sunny, the Cross Product Value Stream, and all business and delivery partners for their passion and drive to deliver positive outcomes.

A special mention to Christian and the Lightning team for their dedication in delivering Product and Pricing services. The hard work and perseverance of the engineers, security partners, quality eningeers and everyone involved have been key to making it a success.

---
