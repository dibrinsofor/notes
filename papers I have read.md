# papers I have read

* #### [Thinking aloud about confusing code: a qualitative investigation of program comprehension and atoms of confusion](https://dl.acm.org/doi/10.1145/3368089.3409714) by **Dan Gopstein** et al, 2020.
  This paper probes prior research work on [Atoms of Confusion](https://atomsofconfusion.com/) -- tiny hand-picked code patterns whose outputs are validated and proven to be confusing to programmers -- exploring reasons why programmers may fail to properly evaluate these code samples and futhermore, the correctness of hand-evaluation (self evaluation by programmers) as a study tool. By leveraging a hybrid qualitative study approach (interviews and observations), Gopstein et al presents novel taxonomies to categorize the confusions found among subjects with the code snippets: unfamiliarity, misunderstanding, language transfer, and attention. This paper gives ample context to the results found [here](https://dl.acm.org/doi/10.1145/3106237.3106264). [Easy to follow] 
  
* #### [Tracking Ransomware End-to-End](https://ieeexplore.ieee.org/document/8418627) by **Danny Y. Huang** et al, 2018.
  Over the course of two years, Danny et al studied ransomware operators who adopted Bitcoin (from delivery of the ransomware to Liquidation of funds from victims) using data from "real" victims found on public forums and "synthetic" victims generated in a sandbox environment. To discover additional wallet addresses of ransomware operators, the authors devised a co-spending heuristic and supported that with micropayments to monitor cash-out. In addition to all of this, the paper also explores the impact of ther Cerber ransomware on victims by reverse engineering the malware's command and control to measure the number of infected systems per affiliate. To conclude, Danny et al present a conservative estimate of 19,750 victims affected by 10 different families of Ransomware. [Easy to follow]
  
* #### [Paging and the address-translation problem](https://dl.acm.org/doi/pdf/10.1145/3409964.3461814) by **Micheal A. Bender** et al, 2021.
  This paper breaks down the **Address Translation** problem in virtual memory access and formulates a solution (using [huge-pages](https://lwn.net/Articles/374424/)) to reduce the translation cost without increasing the paging and reallocation costs. By using pointers instead of caching actual data you can vastly increases the amount of data a single address can point to. Traditional **TLBs** cannot store an array of huge-page addresses as a value because of bit size limitations, however, this paper suggests a *Low associative paging algorithm* (derived using a blackbox transformation) that returns relatively small addresses that can be packed together as one TLB entry. [See this](https://www.youtube.com/watch?v=AbvW8m7xMFI&t=743s). [Not as easy to follow]
  
  <!-- Programs who access pages through a virtual page address require for the virtual address to be translated to a physical address in RAM where the page is stored, this step is called **Address Translation (AT)** and is done using a Page Table stored in-RAM that holds virtual to physical address mappings. The cost of **AT** becomes a lot more significant when you consider that every memory reference MUST undergo **AT**, hence the reason modern CPUs have **TLBs** (Translation Lookaside Bufffers) -- kv stores that cache pointers to data in the page table.  -->
  

  <!--- reduce to 6 lines -->

* #### [What goes around comes around](https://blog.vaticle.com/what-goes-around-comes-around-52d38ee1ea9e) by  **Joseph Hellerstein** and **Michael Stonebraker**, 2005.
  This paper breaks down over 3 decades worth of database proposals (or research) in hopes that young researchers do not *re-make* old mistakes. It starts off with IMS (a hierarchical data model) that introduced *record types* arranged in trees but was plagued by data dependence limitations and it's restrictive nature. Then CODASYL (a network data model) that traded ease of representing non-tree data (a problem with IMS) for additional complexity -- appaz it's easier to traverse a tree than it is to navigate multi-dimensional space. Subsequently the Relational model sought to improve data independence and proposed a Relational Schema that could represent almost anything. At around the same time, the Entity Relationship model was proposed but did not catch on (cause Relational DBs were all the hype) but was instead adopted as a database design tool. Then came the R++ and the Semantic Data Model eras that did not provide enough performance advantages to gain widespread adoption. The Object Oriented Model followed after and aimed to solve impedance mismatch (it didn't), it was also a niche product and could not go mainstream. Then came the INGRES team looking to solve GIS issues and offered code in DB and user defined access methods in the Object Relational Model (Postgres). And finally, the Semi-Structured Data model with X and all her friends. [Here's what happened to XML Schemas](https://doveltech.com/innovation/whatever-happened-to-xml-schemas/). [Easy to follow]

  <!--- reduce to 6 lines -->

* #### [My SIM is Leaking My Data: Exposing Self-Login Privacy Breaches in Smartphones](https://www.researchgate.net/publication/340033130_My_SIM_is_Leaking_My_Data_Exposing_Self-Login_Privacy_Breaches_in_Smartphones) by **Andrea Coletta** et al, 2020.
  This paper highlights privacy concerns for smartphone users, in Italy, whose carriers adopt a *[frictionless]()* self login feature. It also explores quite a number of countermeasures that can be taken to improve privacy, all with tradeoffs. Coletta et al present two heuristics to categorize said concerns: active (user's info can be read and modified) and passive attacks (user's info can only be read). The paper ends on a high note, suggesting the adoption of Captcha, a counter measure that is fairly unobtrusive. [Paper by Non Native English Speakers]

  Thoughts: How big is this Issue? it seems like it could be global issue. Also, is Captcha really that secure? can it curb this?
<!-- * #### [Securing computer hardware using 3D integrated circuit (IC) technology and split manufacturing for obfuscation]() by **Siddharth Garg** et al, 2013. -->
 
* #### [Securing the Internet of Things in the Age of Machine Learning and Software-Defined Networking](https://ieeexplore.ieee.org/document/8377989) by **Francesco Restuccia** et al, 2018.
  As we continue to rely more and more on IoT devices, the topic of Security and Privacy will continue to pop-up and unlike with consumer software we cannot just push out security patches ad hoc. This paper proffers a taxonomy to categorize IoT threats outside of the inherited Internet threats and highlights unique research challenges in IoT secruity that need to be overcome to make future devices more secure.
  






