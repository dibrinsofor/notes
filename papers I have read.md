# papers I have read

* #### [Thinking aloud about confusing code: a qualitative investigation of program comprehension and atoms of confusion](https://dl.acm.org/doi/10.1145/3368089.3409714) by **Dan Gopstein** et al, 2020.
  This paper probes prior research work on [Atoms of Confusion](https://atomsofconfusion.com/) -- tiny hand-picked code patterns whose outputs are validated and proven to be confusing to programmers -- exploring reasons why programmers may fail to properly evaluate these code samples and futhermore, the correctness of hand-evaluation (self evaluation by programmers) as a study tool. By leveraging a hybrid qualitative study approach (interviews and observations), Gopstein et al presents novel taxonomies to categorize the confusions found among subjects with the code snippets: unfamiliarity, misunderstanding, language transfer, and attention. This paper gives ample context to the results found [here](https://dl.acm.org/doi/10.1145/3106237.3106264). [Easy to follow] 
  
* #### [Tracking Ransomware End-to-End](https://ieeexplore.ieee.org/document/8418627) by **Danny Y. Huang** et al, 2018.
  Over the course of two years, Danny et al studied ransomware operators who adopted Bitcoin (from delivery of the ransomware to Liquidation of funds from victims) using data from "real" victims found on public forums and "synthetic" victims generated in a sandbox environment. To discover additional wallet addresses of ransomware operators, the authors devised a co-spending heuristic and supported that with micropayments to monitor cash-out. In addition to all of this, the paper also explores the impact of ther Cerber ransomware on victims by reverse engineering the malware's command and control to measure the number of infected systems per affiliate. To conclude, Danny et al present a conservative estimate of 19,750 victims affected by 10 different families of Ransomware. [Easy to follow]
  
* #### [Paging and the address-translation problem](https://dl.acm.org/doi/pdf/10.1145/3409964.3461814) by **Micheal A. Bender** et al, 2021.
  This paper breaks down the **Address Translation** problem in virtual memory access and formulates a solution (using [huge-pages](https://www.youtube.com/watch?v=zZbbD4Iu-8Y)) to reduce the translation cost without increasing the paging and reallocation costs. Programs who access pages through a virtual page address require for the virtual address to be translated to a physical address in RAM where the page is stored, this step is called **Address Translation (AT)** and is done using a Page Table stored in-RAM that holds virtual to physical address mappings. The cost of **AT** becomes a lot more significant when you consider that every memory reference MUST undergo **AT**, hence the reason modern CPUs have **TLBs** (Translation Lookaside Bufffers) -- kv stores that cache pointers to data in the page table. Using pointers instead of caching actual data vastly increases the amount of data a single address can point to. Traditional **TLBs** cannot store an array of huge-page addresses as a value because of bit size limitations, however, this paper suggests a *Low associative paging algorithm* (derived using a blackbox transformation) that returns relatively small addresses that can be packed together as one TLB entry. [See this](https://www.youtube.com/watch?v=AbvW8m7xMFI&t=743s). [Not as easy to follow]
  
  






