# Known Issues and Troubleshooting

This document includes known issues you may face when creating an experiment on Azure App Configuration that are currently being resolved (once these issues are resolved, this document will be updated to reflect the changes).

## Overview
- Known Issues
- Troubleshooting

## Known Issues

### Links to Documentation

The "learn more" links in Azure Portal are pointing to an AppConfig overview page instead of specific documents relevant to the context. This is because we don't have public documentation published yet as this feature is still in Private Preview.

### Sampling in Application Insights

Application Insights samples telemetry events by default, so you may not see all the expected events in Application Insights or Split Experimentation Workspace. Results can be skewed because of the partial event data. You should choose appropriate sampling according to your needs. For the QuickStart (Quote of the Day) application linked in this repository for Private Preview tutorial, you are instructed to disable sampling on Application Insights. 

### Failed to assign Tags notification

The Tags edit operation in Split Overview blade succeeds, but shows a notification with ‘Failed to assign tags’ title. You can ignore this notification.

### Unicode Resource Name - Do Not Use

A Split Experimentation Workspace can be created with unicode resource name, but the data-plane operations will fail. Please do not using unicode resource name for now.

### Refresh to view recalculated results with updated data

If the data is more than 10 minutes old, requesting results will cause a recalculation on the experimentation results page that takes ~15 seconds to complete. You need to refresh after the recalculation is completed in order to see the updated data.

### Reusing a deleted Experimentation Workspace name results in error

Please do not recreate a Split Experimentation Workspace with the same name even after you have already deleted the original resource as it will result in failure.

## Troubleshooting

### Quickstart application (Quote of the Day) not showing data in experimentation results page

Solution(s):
1. Go to **App Configuration > Feature Manager**. In the 3 dot dropdown **"..."** for your variant feature flag: <br/>
a. Select History. Take note of the timestamp and etag of the newest version. <br/>
b. Select Experiment. The "Version" timestamp should match the timestamp seen in step 1.a. <br/>

2. Go to **App Insights > Logs**. Run the query "customEvents" and sort by timestamp. <br/>
a. You should see Events with name: FeatureEvaluation <br/>
      &nbsp;&nbsp;&nbsp;&nbsp; i. Ensure the customDimension.eTag matches the eTag in step 1. <br/>
      &nbsp;&nbsp;&nbsp;&nbsp; ii. Ensure the customDimension.TargetingId has a value. <br/>
b. You should see Events with different name. These are the events you can build metrics from. Take note of the "Name".*(This string was defined by your code in the "TrackEvent" call to App Insights)* <br/>

3. Go to **Split Experimentation Workspace > Experimentation Workspace** and click **Edit** on your Metric <br/>
a. Ensure the Application Insights Event Name exactly matches the "Name" seen in App Insights in step 2.b. <br/>

4. Watch the network traffic of the Experiment results page and check the response of the metric-results call. You should see SampleSizeReceived. <br/>
a. If SampleSizeReceived is more than 0, your Split Experimentation Workspace is receiving events but the mapping of the resources on Azure to create your experiment may not have been correctly setup. <br/>
b. If SampleSizeReceived equal to 0, your Split Experimentation Workspace is not seeing any of the data. This can be due missing data in your Storage Account implying an incorrect export rule, or incorrect permissions setup between your Split Experimentation Workspace and your Storage Account.
Navigate to your Split Experimentation Workspace resource to review details of the linked Storage Account under "Data Source".
