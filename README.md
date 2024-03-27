# Welcome to the Private Preview of experimentation in Azure App Configuration!

Split Experimentation for Azure App Configuration is a feature that allows developers to easily run A/B tests for their applications and expand the monitoring phase of the DevOps loop to act on user feedback seamlessly. This experience is powered by the combined use of Azure App Configuration, Application Insights and Split Experimentation Workspace, to help you leverage your existing resources. To get started on your first experiment on Azure, follow these steps:

## Overview
**Experimentation in Azure App Configuration:**
- What is experimentation?
- Setting up goals for your experiment
- Understanding your experiment results

**Get Started:**
- Steps to setup experimentation in Azure App Configuration - how-to-setup-experimentation.md
- Data Access Control - how-to-setup-data-access-experimentation.md
- QuickStart App Quote of the Day - QuoteOfTheDayQuickStart folder
- ARM Template Instructions
- Known Issues and Troubleshooting - known-issues-and-troubleshooting.md

## Experimentation in Azure App Configuration

### What is experimentation?
Microsoft has partnered with Split Software to deliver experimentation as a feature in Azure App Configuration. If this is your first time running an experiment, here are some terms to familiarize yourself with beforehand in the context of Feature Flags in App Configuration:<br/>
- **Feature Flags:** Allow teams to **toggle features on or off** dynamically during runtime. The feature flag also has an associated code block. The feature flag's state triggers whether the code block runs. Read more about [Feature Flags on Azure App Configuration](https://learn.microsoft.com/en-us/azure/azure-app-configuration/concept-feature-management#basic-concepts). <br/>
- **Variant Feature Flags:** Represent different versions or configurations of a feature. In an experiment, the variant feature flags are compared in relevance to the metrics you are interested in and the traffic you have allocated for the application audience. Read more about [Variant Feature Flags on Azure App Configuration](https://github.com/microsoft/FeatureManagement-Dotnet/tree/release/v4?tab=readme-ov-file#variants).<br/>
- **A/B Testing:** A/B testing, also known as split testing, is an industry-standard method for evaluating the impact of potential changes within a technology stack. Read more about [A/B Testing on Products](https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/a-b-testing-across-products/).

Consider the following example: you want to see if customers of your e-commerce website are more likely to click the checkout button on their shopping cart if it is yellow in color (variant A) or when the same checkout button is orange in color (variant B). To setup this comparison, you are likely to divide traffic by half to each variant of the feature flag and use number of clicks as a metric to measure which one is performing better (where better is defined by an increase in number of clicks on the checkout button). It is unlikely that all your features will be as simple to measure and immediately evaluate, and that is where experimentation comes in. Running an experiment involves setting up a timeline for this process of comparing the performance of each variant relevant to the metrics you are interested in. The terms ‘A/B testing’ and ‘experimentation’ are often used interchangeably, where experimentation is essentially an extended A/B test where you are systematically testing hypotheses. 

**Experimentation**: The process of systematically testing hypotheses or changes to improve user experience or software functionality. This definition also holds true for most scientific fields including technology, where all experiments have 4 common steps:<br/>

**1.	Developing a hypothesis** to document the purpose of this experiment,  <br/>
**2.	Outlining a method** of carrying out the experiment including setup, what will be measured and how,  <br/>
**3.	Observation** of the results measured by the metrics defined in the previous step,  <br/>
**4.	Drawing a conclusion** regarding whether the hypothesis was validated or invalidated. <br/>

All A/B tests are experiments, but not all experiments are A/B tests, essentially implying that in the digital world, an A/B test is the simplest form of an experiment. Experimentation encompasses various controlled tests, including A/B testing, and can include more types of tests such as multivariate tests that include in-depth statistical analysis and more complex combinations of variant feature flags. 

In this tutorial where you will be generating a quote of the day to different users and checking their likes, our hypothesis is that users are more likely to click on the heart/like icon if the quote of the day is accompanied by a special message (“*hope this makes your day*”). Therefore, our metric of measure would be number of clicks on the heart icon (or Likes) and comparing between the two variants: one where the user sees the special message, one where the user does not. In this scenario, the two variations of the feature are true and false. This makes our experiment an A/B test. However, if we were testing multiple combinations of multiple variants such as adding multiple like buttons or changing colors of the special message as well, then it would be a Multivariate test. It is important for you to identify what kind of experiment you want to run so that the results can help you improve your application be it for performance or business. 

### Setting goals for your experiment
Before starting, consider the following in your hypothesis discovery stage: 
What should you run an experiment on? Why? Where do you even start? What problem are you trying to solve by running an experiment? What are some strategies to follow according to your business needs? Will this experiment help you make immediate improvements to the performance of your application or to your business? 

Now that you have identified what you hope to achieve by running an experiment on your application, you have to document your methodology: how will you run this experiment? What are some metrics you are interested in? What events of user or system interaction will you use to capture data to fuel these metrics for measure? As your experiment plan starts getting implemented: this is where the tutorial below goes. Your goal at this **methodology definition stage** is to make sure you are setting up your application code and resources to capture the correct data you are interested in.

When your experiment duration is nearing completion, it’s time to seek results. Observe and analyze the data and outcome to subsequently determine successes and failures, insights into user behavior, and learnings. Your goal at this stage is to make sure the data captured in all the resources you’ve deployed on Azure are passing validations: that you are indeed receiving the data that you had set up your resources to. If there are discrepancies, this is where you can edit your variant feature flags and view a different version of the same on-going experiment. 

**Drawing a conclusion** (or multiple conclusions if needed) is the final stage of your experimentation cycle. Learnings and outcomes that you can immediately implement into production go here. However, experimentation is a continuous process. Begin new experiments to continuously improve your product. 

### Understanding your experiment results
Your experiment is only as good as the data your App Insights resource has collected. Once there is enough traffic to your application and subsequently more data from user interactions with events you have set up under the metrics mapping, you must determine which variant you intend to use as the control (baseline variant) and which one you intend to see changes in (comparison variant).  <br/>
- **Desired Outcome:** The desired outcome refers to the specific result or effect we hope to achieve through an experiment or intervention. It represents success according to our goals. <br/>
- **Undesired Outcome:** An undesired outcome is the opposite of what we want to achieve. It represents failure or an unexpected result. <br/>
- **Inconclusive:** An inconclusive result occurs when the data collected from an experiment does not provide clear evidence for either the desired or undesired outcome. It means that we can not confidently conclude whether the intervention had a significant impact. Inconclusive results might arise due to insufficient sample size, noisy data, or other factors. Remember that experimentation involves analyzing data objectively and drawing meaningful conclusions based on evidence. Desired outcomes drive our efforts, undesired outcomes guide improvements, and inconclusive results prompt further investigation.

---
Now that you know the basics of experimentation and how it can benefit your team, you can begin setting up your first experiment on Azure by [following the instructions document](/how-to-setup-experimentation.md) which will allow you to create an experiment, setup metrics for results, create a QuickStart application to run the experiment on, and setup data access policies.
