---
title: "About the Paper"
layout: single
permalink: /paper
redirect_from:
  - /authors
  - /research
  - /evaluation
  - /replication
sidebar:
  nav: "guidelines"
toc: true
toc_label: "On this page"
toc_sticky: true
---

## Citation
{: #citation}

R. Caldas, J. A. Pinera Garcia, M. Schiopu, P. Pelliccione, G. Rodrigues, and T. Berger, "Runtime Verification and Field-based Testing for ROS-based Robotic Systems," *IEEE Transactions on Software Engineering*, vol. 50, no. 10, pp. 2544–2567, 2024. DOI: [10.1109/TSE.2024.3444697](https://doi.org/10.1109/TSE.2024.3444697)

[![DOI](https://zenodo.org/badge/DOI/10.1109/TSE.2024.3444697.svg)](https://doi.org/10.1109/TSE.2024.3444697)

### BibTeX

```bibtex
@ARTICLE{caldas2024guidelines,
  author={Caldas, Ricardo and Pi{\~n}era Garc{\'i}a, Juan Antonio and Schiopu, Matei and Pelliccione, Patrizio and Rodrigues, Gena{\'i}na and Berger, Thorsten},
  journal={IEEE Transactions on Software Engineering},
  title={Runtime Verification and Field-based Testing for ROS-based Robotic Systems},
  year={2024},
  volume={50},
  number={10},
  pages={2544--2567},
  keywords={Robots;Testing;Runtime;Guidelines;Software;Quality assurance;Robot kinematics;Field-based Testing;Runtime Verification;Robotic Systems;Robot Operating System (ROS);Uncertainty;Guidelines},
  doi={10.1109/TSE.2024.3444697}
}
```

## Authors
{: #authors}

<p><img src="/img/ricardo.jpg" style="float:right; overflow: auto; width:200px; margin-left: 1em;"></p>

### Ricardo Caldas (primary contact)

PhD. Candidate, Chalmers University of Technology, Interaction Design and Software Engineering, Computer Science and Engineering

[Contact Information](https://ricardocaldas.me/)

Email: [ricardo.caldas@gssi.it](mailto:ricardo.caldas@gssi.it)

<p style="clear:both;"><br></p>

<p><img src="/img/tony.png" style="float:right; overflow: auto; width:200px; margin-left: 1em;"></p>

### Juan Antonio Pinera Garcia

PhD Candidate, Gran Sasso Science Institute

[Contact Information](https://www.gssi.it/people/students/students-computer-science/item/15647-pinera-garcia-juan-antonio)

<p style="clear:both;"><br></p>

<p><img src="/img/matei.jpg" style="float:right; overflow: auto; width:200px; margin-left: 1em;"></p>

### Matei Schiopu

Assistant Researcher, Chalmers University of Technology

[Contact Information](https://www.linkedin.com/in/matei-schiopu-37aa071a1/)

<p style="clear:both;"><br></p>

<p><img src="/img/patrizio.jpg" style="float:right; overflow: auto; width:200px; margin-left: 1em;"></p>

### Patrizio Pelliccione

Director of the Computer Science area and Professor in Computer Science and Software Engineering at GSSI (Gran Sasso Science Institute), Italy.

[Contact Information](http://www.patriziopelliccione.com/)

<p style="clear:both;"><br></p>

<p><img src="/img/geanina.jpg" style="float:right; overflow: auto; width:200px; margin-left: 1em;"></p>

### Genaína Nunes Rodrigues

Associate Professor of Computer Science, University of Brasilia

[Contact Information](https://genaina.github.io/)

<p style="clear:both;"><br></p>

<p><img src="/img/thorsten.jpg" style="float:right; overflow: auto; width:200px; margin-left: 1em;"></p>

### Thorsten Berger

Chair of Software Engineering / Professor Ruhr University Bochum, Germany

[Contact Information](https://se.ruhr-uni-bochum.de/thorsten-berger/)

<p style="clear:both;"><br></p>

## Evaluation
{: #evaluation}

This section presents the outcomes of our validation with industry and academia experts, conducted through questionnaires available in the replication package section of the website. Our aim is to assess whether the guidelines synthesized from literature and insights from open-source ROS repositories are perceived as useful, clear, and applicable by developers and QA teams testing and verifying ROS code. We formulate three hypotheses per guideline:

- H1. Overall, the guideline is useful. (Usefulness)
- H2. The formulation of the guideline is clear. (Clarity)
- H3. The guideline is applicable to ROS-based systems. (Applicability)

Unlike usefulness, applicability refers to the extent to which respondents consider that the guideline could be directly applied to ROS-based systems they have worked with. Conversely, usefulness pertains to ROS-based systems in general.

### Summary of Respondent Profiles

<table>
  <tr>
    <td><b>ID</b></td>
    <td><b>Time</b></td>
    <td><b>Experience</b></td>
    <td><b>Organization</b></td>
    <td><b>Domain</b></td>
    <td><b>Role</b></td>
    <td><b>Individuals</b></td>
  </tr>
  <tr>
    <td>P1</td>
    <td>&gt;10y</td>
    <td>Contributed to ROS packages</td>
    <td>Academia and Industry</td>
    <td>Service Robotics</td>
    <td>Developer</td>
    <td>18</td>
  </tr>
  <tr>
    <td>P2</td>
    <td>3-5y</td>
    <td>Worked on applications using ROS</td>
    <td>Industry</td>
    <td>Industrial automation</td>
    <td>Developer</td>
    <td>17</td>
  </tr>
  <tr>
    <td>P3</td>
    <td>1-3y</td>
    <td>Contributed to ROS packages</td>
    <td>Academia</td>
    <td>General-purpose</td>
    <td>Developer</td>
    <td>6</td>
  </tr>
  <tr>
    <td>P4</td>
    <td>1-3y</td>
    <td>Worked on applications using ROS</td>
    <td>Academia and Industry</td>
    <td>General-purpose</td>
    <td>QA</td>
    <td>3</td>
  </tr>
  <tr>
    <td>P5</td>
    <td>3-5y</td>
    <td>Worked on applications using ROS</td>
    <td>Academia and Independent Groups</td>
    <td>Marine Robotics</td>
    <td>QA</td>
    <td>11</td>
  </tr>
</table>

We received 55 questionnaire responses, with 33 from developers and 22 from QA teams. These responses were obtained through targeted emails and posts in the ROS discourse forum. The questionnaire was tailored to test the three hypotheses, and respondents were also asked about their experience in robotics, ROS experience, organizational background, and robotics domains they've worked on.

### Likert Plot for Questionnaire Answers

![Likert plot for the questionnaire answers](/img/linkert2.png)
{: style="text-align: center;"}

*Figure 1: Likert plot for the questionnaire answers*
{: style="text-align: center;"}

The Likert plot provides an overview of the questionnaire responses. While most votes lean towards 'Agree,' some guidelines received 'Strongly Disagree' votes. We focus on analyzing disagreements, as they may indicate areas for further research.

![Boxplots for the results bird's eye view](/img/boxplots.png)
{: style="text-align: center;"}

*Figure 2: Boxplots for the results bird's eye view*
{: style="text-align: center;"}

In addition to the Likert plot, we conducted statistical analysis using boxplots to visualize whether the hypotheses hold for each guideline. Overall, developers and QA teams agree that the synthesized guidelines are applicable, useful, and clear.

### Statistical Significance

![Wilcoxon one-sample test](/img/statistical_sig.png)
{: style="text-align: center;"}

*Figure 3: Wilcoxon one-sample test for statistical significance (hypothesis: μ ≥ 0)*
{: style="text-align: center;"}

We tested the hypotheses for statistical significance using the one-sample Wilcoxon test. The tests confirm the statistical significance of the correlation between guidelines and attributes of applicability, clarity, and usefulness, except for guidelines CI2, MTA2, and PE2.

### Practical Significance

![Effect size for one sample Wilcoxon test](/img/practical_sig.png)
{: style="text-align: center;"}

*Figure 4: Effect size for one sample Wilcoxon test for practical significance*
{: style="text-align: center;"}

Practical significance was assessed using the effect size calculated from the one-sample Wilcoxon signed-rank test. Guidelines with small effect sizes (CI2, MTA2, and PE2) required further data to strengthen conclusions, while guidelines with moderate and large effect sizes justify their practical significance.

Ultimately, we conducted a follow-up discussion with respondents who disagreed with the usefulness/applicability of CI2, MTA2, and PE2, and modified the guidelines.

## Replication Package
{: #replication-package}

*Would you like to replicate our study?* This page will take you through the steps to replicate our study. We use the methodology to guide you through the replication process. We understand that some steps are hard or even impossible to replicate, thus we provide artifacts (protocols, scripts, spreadsheets with results) generated during our study to help you follow along. Please, contact us in case you have any doubts.

Before you start, [click here](/replication_package_extras/replication_package.zip) to download the replication package as a .zip.

We followed design science to synthesize the guidelines. We guide you through each cycle of the design science process from Fig 5.

<img style="width: 75%;" class="center" src="/img/cycles.png">
<p class="center" style="text-align: center;"><b>Figure 5:</b> Activities to synthesizing guidelines according to design science</p>

### First Cycle: Survey Elicitation and Terminology

The first cycle is devoted to establishing awareness of the state-of-the-art and building the terminology used in the study.

We elicit important surveys in runtime verification and field-based testing:

<ul style="list-style-type: none;">
  <li>1. Afzal, Afsoon, et al. "A study on challenges of testing robotic systems." 2020 IEEE 13th International Conference on Software Testing, Validation and Verification (ICST). IEEE, 2020.</li>
  <li>2. Albonico, Michel, et al. "Software engineering research on the Robot Operating System: A systematic mapping study." Journal of Systems and Software 197 (2023): 111574.</li>
  <li>3. Bertolino, Antonia, et al. "A survey of field-based testing techniques." ACM Computing Surveys (CSUR) 54.5 (2021): 1-39.</li>
  <li>4. Falcone, Yliès, et al. "A taxonomy for classifying runtime verification tools." International Journal on Software Tools for Technology Transfer 23.2 (2021): 255-284.</li>
  <li>5. Garousi, Vahid, Michael Felderer, and Feyza Nur Kılıçaslan. "A survey on software testability." Information and Software Technology 108 (2019): 35-64.</li>
  <li>6. Luckcuck, Matt, et al. "Formal specification and verification of autonomous robotic systems: A survey." ACM Computing Surveys (CSUR) 52.5 (2019): 1-41.</li>
  <li>7. Malavolta, Ivano, et al. "Mining guidelines for architecting robotics software." Journal of Systems and Software 178 (2021): 110969.</li>
</ul>

From the surveys, we extracted the following terminology. We present it in the format of a search string since the terminology intended to be used in a systematic literature review (in Cycle 2):

```
IEEE Xplore Search String = ("ros" OR "robotic operating system" OR "robot operating system") AND ("runtime verification" OR "run−time verification" OR "runtime assurance" OR "run−time assurance" OR "online verification" OR "on−line verification" OR "runtime monitoring" OR "run−time monitoring" OR "runtime testing" OR "run−time testing" OR "online testing" OR "on−line testing" OR "field−based testing" OR "field testing" OR "in−vivo testing")
```

```
Scopus Search String =TITLE−ABS−KEY ( ( ros OR "robotic operating system" OR "robot operating system" ) AND ( "runtime verification" OR "run−time verification" OR "runtime assurance" OR "run−time assurance" OR "online verification" OR "on−line verification" OR "runtime monitoring" OR "run−time monitoring" OR "runtime testing" OR "run−time testing" OR "online testing" OR "on−line testing" OR "field−based testing" OR "field testing" OR "in−vivo testing"))
```

```
ACM DL Search String = Fulltext:(("ros" OR "robotic operating system" OR "robot operating system") AND ("runtime verification" OR "run−time verification" OR "runtime assurance" OR "run−time assurance" OR "online verification" OR "on−line verification" OR "runtime monitoring" OR "run−time monitoring" OR "runtime testing" OR "run−time testing" OR "online testing" OR "on−line testing" OR "field−based testing" OR "field testing" OR "in−vivo testing"))
```

The terminology was validated internally, through peer reviews and discussions with co-authors to consolidate the scope of our study.

### Second Cycle: Literature Review, Guideline Templates, External Validation

The Second Cycle focused on performing a literature review, synthesizing the guideline templates, and performing an external validation of the template.

#### Systematic Literature Review

We used the search string to perform a systematic literature review to understand the studies discussing runtime verification and field-based testing for ROS applications. The SLR followed the activities in Fig. 6.

<img style="width: 75%;" class="center" src="/img/systematic_literature_review.png">
<p class="center" style="text-align: center;"><b>Figure 6:</b> Activities to conducting the systematic literature review</p>

We present precise descriptions for each activity in a [protocol](/replication_package_extras/slr_protocol.pdf).

In short, we searched for the string in IEEEXplore, ACM Digital Library, and Scopus.

Then, we used the inclusion and exclusion criteria from Tab. 1 to filter out relevant studies.

<table>
  <tr>
    <td>ID</td>
    <td>Description</td>
    <td>Reasoning</td>
  </tr>
  <tr>
    <td>IC_1</td>
    <td>ROS-based application. Including ROS1 and ROS2.</td>
    <td>Robotic Operating System (ROS) is a must</td>
  </tr>
  <tr>
    <td>IC_2</td>
    <td>Explicit description (or reference to peer-reviewed venue) of the verification, validation, or testing technique.</td>
    <td>Papers that do not explicitly describe the employed technique may lead to ambiguous interpretation</td>
  </tr>
  <tr>
    <td>EC_1</td>
    <td>Tutorial, artifact, short paper (less than 5pgs), keynote, secondary studies, roadmaps, duplicated study</td>
    <td>Such papers do not provide enough contextual information.</td>
  </tr>
  <tr>
    <td>EC_2</td>
    <td>Verification, validation, or testing techniques that do not make use of the ROS Ecosystem</td>
    <td>Papers targeting V&amp;V of non-ROS applications should be excluded.</td>
  </tr>
  <tr>
    <td>EC_3</td>
    <td>Verification, validation, or testing techniques that do not address solely hardware properties</td>
    <td>Papers targeting V&amp;V of hardware should be excluded</td>
  </tr>
  <tr>
    <td>EC_4</td>
    <td>Papers that are not in Computer Science or Engineering fields</td>
    <td>Papers from other fields should be excluded since they do not discuss means to engineering robotics systems.</td>
  </tr>
</table>

<p class="center" style="text-align: center;"><b>Table 1:</b> Inclusion Criterion (IC) and Exclusion Criterion (EC)</p>

Finally, we selected the runtime verification and field-based testing approaches according to a classification scheme. [spreadsheet](/replication_package_extras/literature_review.xlsx)

#### Guidelines Template

Then, we understood what was necessary for a guideline and designed a template, see Tab. 2. We used the template to synthesize our initial set of guideline sketches.

<table>
  <tr>
    <td><b>Element</b></td>
    <td><b>Description</b></td>
  </tr>
  <tr>
    <td><b>ID</b></td>
    <td>Identifier used to facilitate tracing guidelines between groups</td>
  </tr>
  <tr>
    <td><b>Title</b></td>
    <td>Title summarizes an action that practitioners should follow to mitigate or avoid a recurring problem.</td>
  </tr>
  <tr>
    <td><b>Context (WHEN)</b></td>
    <td>The Context is a paragraph placing the guideline among a known set of conditions. This paragraph should delimit the scope in which the guideline is applicable. It should also introduce the conceptual terminology used in the guideline, which is defined by the conditions under which the guideline is valid.</td>
  </tr>
  <tr>
    <td><b>Reason (WHY)</b></td>
    <td>Reason introduces the recurring problem faced by practitioners. It intends to leverage the relevance of the guideline to practitioners</td>
  </tr>
  <tr>
    <td><b>Suggestion (WHAT)</b></td>
    <td>Suggestion is a sentence or two introducing WHAT should the practitioners do to mitigate the recurring problem</td>
  </tr>
  <tr>
    <td><b>Process (HOW)</b></td>
    <td>Process is a paragraph that carefully guides the practitioners through HOW they can practice the guideline. In this paragraph, there should be references to tools that may help, concrete examples, or references to precise explanations of researchers or practitioners who have done something similar.</td>
  </tr>
  <tr>
    <td><b>Exemplars</b></td>
    <td>Exemplars are concrete descriptions of papers/artifacts that follow the guidelines. An exemplar can be generic such as an artifact or rather specific such as a model problem in testing ROS-based systems in the field.</td>
  </tr>
  <tr>
    <td><b>Strengths</b></td>
    <td>Strengths is a list of benefits that the practitioners should consider when applying the guideline</td>
  </tr>
  <tr>
    <td><b>Weaknesses</b></td>
    <td>Weaknesses is a list of technological/theoretical barriers that may slow the actual implementation of the guideline, either by undesired side-effects or scenarios in which applying the guideline might not lead to the desired effect.</td>
  </tr>
</table>

<p class="center" style="text-align: center;"><b>Table 2:</b> Template for Guideline Specification</p>

#### External validation

Finally, we shared, through a [questionnaire](/replication_package_extras/pre-external_questionnaire.pdf), the sketches with members of the Robotics Software Engineering Workshop. Three experts sent us their [feedback](/replication_package_extras/pre-external_answers.xlsx).

### Third Cycle: Repos Mining, Guidelines with Exemplars, Online Survey

The third cycle was devoted to consolidating the guidelines with concrete examples, clustering, organizing the guidelines, and validating with researchers and practitioners.

#### Consolidating the Guidelines

To consolidate the guidelines we further looked for specific papers on the topic of the guideline and performed a data mining. For the specific search, we used Google Scholar with terms extracted from the guideline sketches. The repositories mining followed the procedure described in Fig. 7.

<img class="center" style="width: 75%;" src="/replication_package_extras/methodology.png">
<p class="center" style="text-align: center;"><b>Figure 7:</b> Data mining activities</p>

For more details, check the [GitHub repository](https://github.com/SchiopuMatei/Chalmers-ROS-RM-FT-Datamining) with scripts and the [protocol](/replication_package_extras/Datamining_Paper.pdf) with details explaining the steps in Fig. 7.

This step resulted in the guidelines catalog. Each guideline follows a template and they are all documented in a separate [guidelines.pdf file](/replication_package_extras/clustered_guidelines_3rd cycle.pdf).

#### Online Survey

Finally, we validated the final set of guidelines with practitioners and researchers. To this end, we designed and distributed an online questionnaire.

The questionnaire was split in two targeting developers or quality assurance teams.

- **Developers**
  - [Developer's Questionnaire Form](/replication_package_extras/DevelopersSurvey.pdf)
  - [Developer's Answers](/replication_package_extras/DevelopersSurvey.csv)
- **Quality Assurance Teams**
  - [QA Team's Questionnaire Form](/replication_package_extras/QATeamSurvey.pdf)
  - [QA Team's Answers](/replication_package_extras/QATeamSurvey.csv)

The results from the third cycle confirmed the guidelines' relevance and helped us fine-tune them. The analysis that followed up the questionnaires is available in the [Evaluation](#evaluation) section above.
