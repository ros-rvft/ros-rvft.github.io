---
title: "Evaluation"
layout: single
permalink: /evaluation
---

This section presents the outcomes of our validation with industry and academia experts, conducted through questionnaires available in the replication package section of the website. Our aim is to assess whether the guidelines synthesized from literature and insights from open-source ROS repositories are perceived as useful, clear, and applicable by developers and QA teams testing and verifying ROS code. We formulate three hypotheses per guideline:

- H1. Overall, the guideline is useful. (Usefulness)
- H2. The formulation of the guideline is clear. (Clarity)
- H3. The guideline is applicable to ROS-based systems. (Applicability)

Unlike usefulness, applicability refers to the extent to which respondents consider that the guideline could be directly applied to ROS-based systems they have worked with. Conversely, usefulness pertains to ROS-based systems in general.

## Summary of Respondent Profiles

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

## Likert Plot for Questionnaire Answers

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

## Statistical Significance

![Wilcoxon one-sample test](/img/statistical_sig.png)
{: style="text-align: center;"}

*Figure 3: Wilcoxon one-sample test for statistical significance (hypothesis: μ ≥ 0)*
{: style="text-align: center;"}

We tested the hypotheses for statistical significance using the one-sample Wilcoxon test. The tests confirm the statistical significance of the correlation between guidelines and attributes of applicability, clarity, and usefulness, except for guidelines CI2, MTA2, and PE2.

## Practical Significance

![Effect size for one sample Wilcoxon test](/img/practical_sig.png)
{: style="text-align: center;"}

*Figure 4: Effect size for one sample Wilcoxon test for practical significance*
{: style="text-align: center;"}

Practical significance was assessed using the effect size calculated from the one-sample Wilcoxon signed-rank test. Guidelines with small effect sizes (CI2, MTA2, and PE2) required further data to strengthen conclusions, while guidelines with moderate and large effect sizes justify their practical significance.

Ultimately, we conducted a follow-up discussion with respondents who disagreed with the usefulness/applicability of CI2, MTA2, and PE2, and modified the guidelines.
