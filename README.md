# <p style="text-align: center; font-size: 30px; ">Enhancing User Experience on IBM SkillsBuild with NLP</p>  
## <p style="text-align: center; font-size: 24px; ">Navigating the Learning Landscape with a Simple Search Engine</p>
### <p style="text-align: center;">UCL MSc Business Analytics <br>MSIN0114 Consulting Project Masters Dissertation </p>
#### <p style="text-align: center;">Candidate Number: BSVN6 </p>
---

## Table of Contents
- [Abstract](#abstract)
- [Usage](#usage)
1. [Introduction](#1-introduction)
2. [Methodology](#2-methodology)
3. [Analyses](#3-analyses)
4. [Search Engine](#4-search-engine)
5. [Conclusion](#5-conclusion)

### Abstract
This dissertation explores the challenge of navigating complex online educational platforms, specifically one of two IBM SkillsBuild platforms[^1][^2]. Despite its extensive resources, SkillsBuild’s structure can be challenging for users try- ing to locate specific information. This study presents an innovative solution to this challenge, aimed at improving user navigation and enhancing the overall experience.

The primary focus is the development of a search engine, designed to guide users to relevant courses based on their input queries. It leverages natural language processing (NLP) and employs various word embedding models, such as GloVe, BERT, and RoBERTa, to interpret user input and provide pertinent responses.

Findings indicate that BERT, when paired with Euclidean distance mea- surements, performs the best, i.e. most accurately matches user input with existing IBM SkillsBuild courses. It proves more efficient at providing precise and contextually relevant results. However, these results are limited to the specific IBM platform studied, as the project scope dictated exclusive focus on the IBM SkillsBuild Software Download platform[^3].

This dissertation demonstrates the potential of using NLP and machine learning to enhance the user experience on educational platforms. It also suggests future areas for research, including the expansion of the tool’s utility to other IBM platforms and its optimisation for mobile devices. Although the implemented tool is not fully integrated into the IBM SkillsBuild platform and currently exists independently on Google Cloud, and it is not fully deployable, it showcases a practical solution that could be adapted for commercial use.

This significant contribution to academic discourse provides practical insights on the application of NLP in a business context.

***Keywords***: NLP; IBM SkillsBuild; search engine; word embeddings; BERT

[^1]: Used: https://www.ibm/academic/home
[^2]: Unused: https://skillsbuild.org
[^3]: https://www.ibm.com/academic/home

--- 
### Usage
In this GitHub Repository, you will find the following files: 
- `MSIN0114 Dissertation - BSVN6 (Supplementary Notebook).ipynb`
- `MSIN0114 Dissertation - BSVN6 (Supplementary Notebook).pdf`
- `dropdown.html`
- `sunburst.html`

The supplementary notebooks encompass the entirety of the code utilised for the dissertation. Additionally, they encapsulate all the textual content present in the primary dissertation that was submitted to Turnitin. Given GitHub's file size constraints of 25MB, the original Dissertation in PDF format in the Turnitin submission has been omitted from this repository. Nevertheless, the `dropdown.html` and `sunburst.html` files grant access to the charts in their pristine, interactive configurations. For reference, all these files are also contained within the ZIP file submitted to Turnitin.

Please be informed that this README serves as a condensed representation of the full dissertation in the PDF format. 

---
### 1. Introduction
This dissertation project is an NLP-focused project in collaboration with IBM, and in specific, a platform called IBM SkillsBuild, which aims to help individuals acquire professional and technical skills. The section of IBM SkillsBuild that I was tasked with in this project was IBM SkillsBuild Software Downloads, which will hereafter be referred to as 'IBM SkillsBuild SD'.

IBM SkillsBuild SD does not have a very user-friendly, intuitive layout and design - it has numerous linked websites and intricate sections, therefore understanding and locating precise resources can be an arduous task, especially for new users. The search function on IBM SkillsBuild SD is also set up in a way that searches all of IBM, meaning all the results shown will be where the input phrase occured throughout the entirety of IBM, instead of showing results from the IBM SkillsBuild SD platform only. 

Thus, this project aims to create a simple search engine tailored for IBM SkillsBuild SD and not show results that are all-encompassing.

---
### 2. Methodology
**Data Collection** <br>
Data for this project was not provided by IBM. Instead, students were tasked to collect the data ourselves. And as IBM had explicitly specified, data collected was ONLY from IBM SkillsBuild SD, and NOT from the IBM SkillsBuild platform as a whole. This was done by collecting the topic, link of topic, names of skills taught, descriptions of the skill, the type of the skill and the specific URL of the skill. Each column of the dataset is described in the table below. 
|**Column Name**   |**Description**|
|:---|:---|
|**Topic** |  11 topics available on IBM SkillsBuild SD: AI, Data Science, IBM Z, IBM Cloud, IBM Engineering, IBM Security, IBM Automation, Capstone, IBM Quantum, Red Hat Academy, Power Systems. |
|**Link** | The link for each main topic. |
|**Type**  | The 3 different types of skills available: courseware, software, or resource. |
|**Skill Name**  | Skills under each topic. |
|**Specific Link**| The specific URL for each of the skills.  |
|**Description**  | Description accompanying each skill. |
|**Comments**  | Any additional comments |
|**Course Appears If**  | 3 categories: “not signed in”, “am signed in”, “both” to denote which circumstance the skill is available. |
|**Course Appears If (Numerical)**  | Numerical representation: “not signed in” = 0, “am signed in” = 1, “both” = 2 |


<br>

**Visualisations** <br>

Some visualisations were created to aid in understanding the data better. <br>

<img src="https://github.com/blueykale/ucl-ibm-search-engine/assets/128978402/229cdf15-46cc-4f63-9af6-4814ff4ca147" alt="1_piechart" width="500"/>
<br> This is the distribution of the 11 topics available on IBM SkillsBuild SD - with AI being the majority, followed by Data Science. It offers a quick overview of the diversity of topics that IBM SkillsBuild SD offer. <br> <br>

<img src="https://github.com/blueykale/ucl-ibm-search-engine/assets/128978402/e2815d4c-0c74-4e27-bb1d-50a2b4c0dee1" alt="2_piechart" width="500"/>
<br> This depicts the breakdown of three types of content present on IBM SkillsBuild SD - Software, Courseware and Resources. To view what the breakdown is of the type for every topic, please download the `dropdown.html` file. <br> <br>

<img width="530" alt="dataviz_sunburst_static" src="https://github.com/blueykale/ucl-ibm-search-engine/assets/128978402/99d10ef4-49d3-464f-9319-ddba2adf1d2f">
<br> This shows an even more in-depth breakdown of the above piechart. To view it in its interactive form, please download the `sunburst.html` file. 

<br> 
<br>
<br>

**Functions**<br> 
Before creating the search engine, helper functions were needed.  <br>
<img width="500" alt="function_flowchart" src="https://github.com/blueykale/ucl-ibm-search-engine/assets/128978402/034869b8-d8d6-42ea-ad51-c6ae14745c10">
<br> The function would need to take a string as an input, process it, then output the relevant skills from IBM SkillsBuils SD. 

To do that, 2 similarity measures and 3 word embedding models were used: Cosine similarity and Euclidean distance measures, and GloVe, BERT and RoBERTa models. 

<br>

![flowchart](https://github.com/blueykale/ucl-ibm-search-engine/assets/128978402/aa0bfe10-dc8c-42ad-a01d-4fa7e488932f)
<br> In order to transform the text dataset into something that the models can understand, it needs to be pre-processed, meaning that the dataset is converted into lowercase, and all punctuation, numbers and white spaces are removed. And then the text is tokenised to split the text into discrete, meaningful units. In the case of GloVe, the text also removed any stopwords, which are words that are typically insignificant, such as "to" or "the" or "is", words that don't carry inherent meaning. By doing that, another text dataset made specifically for the GloVe model is created. And by feeding this dataset through the GloVe model, an embedded dataset is created. Then using this dataset, I created 2 functions - `glove_cosine` and `glove_euclidean`. The function will accept a user query as its input, process the user query, and output the results based on cosine similarity or euclidean distance. The entire process was repeated for BERT and RoBERTa to obtain 6 functions. 

<br>
<br>

### 3. Analyses
All 6 functions were tested using many different input test phrases, such as "quantum", and the number of accurate results each function gave was tabulated below. 

<img width="550" alt="analyses" src="https://github.com/blueykale/ucl-ibm-search-engine/assets/128978402/fbb809a3-72a9-4482-a84a-e3b0d8a3973f">



<img width="900" alt="function_results" src="https://github.com/blueykale/ucl-ibm-search-engine/assets/128978402/ae76ffb6-5593-4d98-b429-24cce74cd2a0">
<br> <br>


| **Function**      | **Count of 'best'** | **Count of '2nd best'** | **Total** |
|-------------------|---------------------|------------------------|-----------|
| glove_cosine      | 1                   | 0                      | 1         |
| glove_euclidean   | 2                   | 2                      | 4         |
| bert_cosine       | 8                   | 7                      | 15        |
| bert_euclidean    | 12                  | 3                      | 15        |
| roberta_cosine    | 5                   | 4                      | 9         |
| roberta_euclidean | 10                  | 3                      | 13        |

Number of ‘best’ and ‘2nd best’ for each function

<br>

| **Model** | **Best** | **2nd Best** | **Total** |
|-----------|----------|--------------|-----------|
| GloVe     | 3        | 2            | 5         |
| BERT      | 20       | 10           | 30        |
| RoBERTa   | 15       | 7            | 22        |

Number of ‘best’ and ‘2nd best’ for each word embedding model

<br>

| **Measure** | **Best** | **2nd Best** | **Total** |
|-------------|----------|--------------|-----------|
| Cosine      | 14       | 11           | 25        |
| Euclidean   | 24       | 8            | 32        |

Number of ‘best’ and ‘2nd best’ for each similarity measure
<br>
<br> 

From the tests, the best performing function was actually `bert_euclidean`. 

<br>

### 4. Search Engine
The search engine therefore incorporates the `bert_euclidean` function. 
<img width="700" alt="function_results" src="https://github.com/blueykale/ucl-ibm-search-engine/assets/128978402/2302fea2-a817-4047-9012-c160a3076dc9">
<br> When users submit a query, the system undergoes an intricate preprocessing phase akin to the procedure employed for GloVe. During this phase, additional stopwords such as "where" and "learn" are excluded, considering their anticipated frequent usage in typical search queries of this domain.

Subsequently, the system evaluates if the user's query incorporates expressions of gratitude, such as "thanks", "cheers", or "appreciate it". If identified, the system refrains from processing further and reciprocates with a courteous acknowledgment, such as "you're welcome".

In the absence of gratitude phrases, the query undergoes an assessment for direct phrase matches within the dataset. To elucidate, a query such as "where to learn process mining" would, post-processing, be distilled to "process mining". If the dataset encapsulates an exact match for "process mining", only corresponding results are presented.

However, if no direct matches are discerned, the system invokes the `bert_euclidean` function. This function meticulously scans for relevance and subsequently displays the top ten pertinent results.

The search engine can be found <a href="http://35.223.46.163" target="_blank">here</a>.

<br>


### 5. Conclusion
Throughout this project, I've utilised models like GloVe, BERT, and RoBERTa, along with distance measures such as Cosine similarity and Euclidean distance. However, the vast landscape of NLP and AI offers various other models and measures that are yet to be explored. Diving into these could potentially enhance the results beyond what BERT and Euclidean distance measures have provided.

The tool has room for enhancements. By considering user details like age, education, or career goals, we can better tailor search results. Adding filters for skill level, course duration, or skill type can offer more personalized outcomes. Features like autocomplete, spelling checks, multi-language support, user reviews, and visual aids can further boost user experience. Incorporating job market insights would also be a valuable addition. Overall, there's ample opportunity to elevate this tool.

In wrapping up, this endeavour overcame numerous challenges to create a game-changing, AI-powered search solution tailored for educational content. While we achieved our foundational goals, the journey also unveiled future opportunities ripe for investigation. As a final note, this GitHub repository presents a succinct rendition of the comprehensive dissertation. Thank you for your time and interest. 
