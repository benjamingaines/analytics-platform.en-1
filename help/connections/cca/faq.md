---
title: Cross-Channel Analytics FAQ
description: Frequently asked questions for Cross-Channel Analytics
exl-id: 2ad78c19-4b13-495b-a0aa-44e0a3c95b5e
solution: Customer Journey Analytics
feature: Cross-Channel Analytics
---
# Frequently asked questions

## How can I use CCA to see how people move from one channel to another?

You can use a Flow visualization with the Dataset ID dimension.

1. Log in to [analytics.adobe.com](https://analytics.adobe.com) and create a blank Workspace project.
2. Click the Visualizations tab on the left, and drag a Flow visualization to the canvas on the right.
3. Click the Components tab on the left, and drag the dimension 'Dataset ID' to the center location labled 'Dimension or Item'.
4. This flow report is interactive. Click any of the values to expand the flows to subsequent or previous pages. Use the right-click menu to expand or collapse columns. Different dimensions can also be used within the same flow report.

If you would like to rename dataset ID dimension items, you can use a lookup dataset.

## How far back does CCA rekey visitors?

The lookback window for rekeying depends on your desired frequency of data [replay](replay.md). For example, if you set up CCA to replay data once every week, the lookback window for rekeying is 7 days. If you set up CCA to replay data every day, the lookback window for rekeying is 1 day.

## How are shared devices handled?

In some situations it is possible that multiple people log in from the same device. Examples include a shared device at home, shared PCs in a library, or a kiosk in a retail outlet.

The transient ID overrides the persistent ID, so shared devices are considered separate people (even if they originate from the same device).

## How does CCA handle situations where a single person has a large number of persistent IDs?

In some situations, an individual user can associate with a large number of persistent IDs. Examples include an individual frequently clearing browser cookies, or using the browser's private/incognito mode.

The number of persistent IDs is irrelevant in favor of the transient ID. A single user can belong to any number of devices without impacting CCA's ability to stitch across devices.

## Once I contact my Account Manager with the desired information, how long does it take for the rekeyed dataset to become available?

Live stitching is available approximately 1 week after Adobe enables Cross-Channel Analytics. Backfill availability depends on the amount of existing data. Small datasets (less than 1 million events per day) typically take a couple days, while large data sets (1 billion events per day) can take a week or more.

## How does Cross-Channel Analytics handle GDPR and CCPA requests?

Adobe handles GDPR and CCPA requests in accordance to local and international laws. Adobe offers the [Adobe Experience Platform Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html) to submit data access and deletion requests. The requests apply to both the original and rekeyed datasets.

## What happens if the Persistent ID field in one or more events is blank?

If the `Persistent ID` field is blank on an event in a dataset being stitched with field-base stitching, CCA fills in the `Stitched ID` for that event in one of two ways: 
* If the `Transient ID` field is not blank, CCA uses the value in `Transient ID` as the `Stitched ID`.
* If the `Transient ID` field is blank, CCA also leaves the `Stitched ID` blank. In this case, `Persistent ID`, `Transient ID`, and `Stitched ID` will all be blank on the event. Events such as this are dropped from CJA in any CJA connection using the dataset being stitched where `Stitched ID` was chosen as the `Person ID`. 

## How do metrics in CJA stitched datasets compare with similar metrics in CJA unstitched datasets and with traditional Adobe Analytics?

Certain metrics in CJA are similar to metrics in traditional Analytics, but others are quite different, depending on what you are comparing. The table below compares several common metrics:

| **CJA stitched data** | **CJA unstitched data** | **Traditional Adobe Analytics** | **Analytics Ultimate with CDA** |
| ----- | ----- | ----- | ----- |
| **People** = Count of distinct `Person ID`s where `Stitched ID` is chosen as `Person ID`. **People** may be higher or lower than **Unique Visitors** in traditional Adobe Analytics, depending on the outcome of the stitching process. | **People** = Count of distinct `Person ID`s based on the column selected as `Person ID`. **People** in Adobe Analytics Connector (ADC) datasets is similar to **Unique Visitors** in traditional Adobe Analytics if `endUserIDs. _experience. aaid.id` is chosen as `Person ID` in CJA. | **Unique Visitors** = Count of distinct visitor IDs. Note that **Unique Visitors** may not be the same as the count of distinct **ECID**s.| See [People](https://experienceleague.adobe.com/docs/analytics/components/metrics/people.html?lang=en).  |
| **Sessions**: Is defined based on the sessionization settings specified in the CJA data view. The stitching process may combine individual sessions from multiple devices into a single session. | **Sessions**: Is defined based on the sessionization settings specified in the CJA data view.  | **Visits**: See [Visits](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html?lang=en). | **Visits**: Is defined based on the sessionization settings specified in the [CDA virtual report suite](https://experienceleague.adobe.com/docs/analytics/components/cda/setup.html?lang=en). |
| **Events** = count of rows in the stitched data in CJA. Generally this should be close to **Occurrences** in traditional Adobe Analytics. Note, however, the FAQ above regarding rows with a blank `Persistent ID`.| **Events** = count of rows in the unstitched data in CJA. Generally this should be close to **Occurrences** in traditional Adobe Analytics. Note, however, that if any events have a blank `Person ID` in the unstitched data in AEP data lake, these events will be dropped (not included) in CJA. | **Occurrences**: See [Occurrences](https://experienceleague.adobe.com/docs/analytics/components/metrics/occurrences.html?lang=en). | **Occurrences**: See [Occurrences](https://experienceleague.adobe.com/docs/analytics/components/metrics/occurrences.html?lang=en). |

Other metrics may be similar in CJA and traditional Adobe Analytics. For example, the total count for Adobe Analytics [custom events](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=en) (events 1-100) should generally be very close in traditional Adobe Analytics and CJA (whether stitched or unstitched). Note, however, this may not always be true due to [differences in capabilities](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-aa.html?lang=en)  such as event de-duplication between CJA vs. traditional Adobe Analytics.
