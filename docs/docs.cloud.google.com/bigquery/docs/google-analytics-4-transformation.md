# Google Analytics 4 report transformation

When your Google Analytics 4 reports are transferred to BigQuery, the reports are transformed into the following BigQuery tables and views.

<table>
<thead>
<tr class="header">
<th><strong>GA4 report name</strong></th>
<th><strong>BigQuery table</strong></th>
<th><strong>BigQuery view</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Audiences</td>
<td>p_ga4_Audiences</td>
<td>ga4_Audiences</td>
</tr>
<tr class="even">
<td>Demographic details</td>
<td>p_ga4_DemographicDetails</td>
<td>ga4_DemographicDetails</td>
</tr>
<tr class="odd">
<td>Ecommerce purchases</td>
<td>p_ga4_EcommercePurchases</td>
<td>ga4_EcommercePurchases</td>
</tr>
<tr class="even">
<td>Events</td>
<td>p_ga4_Events</td>
<td>ga4_Events</td>
</tr>
<tr class="odd">
<td>Landing page</td>
<td>p_ga4_LandingPage</td>
<td>ga4_LandingPage</td>
</tr>
<tr class="even">
<td>Pages and screens</td>
<td>p_ga4_PagesAndScreens</td>
<td>ga4_PagesAndScreens</td>
</tr>
<tr class="odd">
<td>Promotions</td>
<td>p_ga4_Promotions</td>
<td>ga4_Promotions</td>
</tr>
<tr class="even">
<td>Tech details</td>
<td>p_ga4_TechDetails</td>
<td>ga4_TechDetails</td>
</tr>
<tr class="odd">
<td>Traffic Acquisition</td>
<td>p_ga4_TrafficAcquisition</td>
<td>ga4_TrafficAcquisition</td>
</tr>
<tr class="even">
<td>User Acquisition</td>
<td>p_ga4_UserAcquisition</td>
<td>ga4_UserAcquisition</td>
</tr>
</tbody>
</table>

## Table schemas for Google Analytics reports

Table Name: Audiences

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>audienceName</td>
<td>The given name of an Audience. Users are reported in the audiences to which they belonged during the report's date range. Current user behavior does not affect historical audience membership in reports.</td>
</tr>
<tr class="even">
<td>averageSessionDuration</td>
<td>The average duration (in seconds) of users' sessions.</td>
</tr>
<tr class="odd">
<td>newUsers</td>
<td>The number of users who interacted with your site or launched your app for the first time (event triggered: first_open or first_visit).</td>
</tr>
<tr class="even">
<td>screenPageViewsPerSession</td>
<td>The number of app screens or web pages your users viewed per session. Repeated views of a single page or screen are counted. (screen_view + page_view events) / sessions.</td>
</tr>
<tr class="odd">
<td>sessions</td>
<td>The number of sessions that began on your site or app (event triggered: session_start).</td>
</tr>
<tr class="even">
<td>totalRevenue</td>
<td>The sum of revenue from purchases, subscriptions, and advertising (Purchase revenue plus Subscription revenue plus Ad revenue) minus refunded transaction revenue.</td>
</tr>
<tr class="odd">
<td>totalUsers</td>
<td>The number of distinct users who have logged at least one event, regardless of whether the site or app was in use when that event was logged.</td>
</tr>
</tbody>
</table>

Table Name: DemographicDetails

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>brandingInterest</td>
<td>Interests demonstrated by users who are higher in the shopping funnel. Users can be counted in multiple interest categories. For example, Shoppers, Lifestyles &amp; Hobbies/Pet Lovers, or Travel/Travel Buffs/Beachbound Travelers.</td>
</tr>
<tr class="even">
<td>city</td>
<td>The city from which the user activity originated.</td>
</tr>
<tr class="odd">
<td>country</td>
<td>The country from which the user activity originated.</td>
</tr>
<tr class="even">
<td>language</td>
<td>The language setting of the user's browser or device. For example, English.</td>
</tr>
<tr class="odd">
<td>region</td>
<td>The geographic region from which the user activity originated, derived from their IP address.</td>
</tr>
<tr class="even">
<td>userAgeBracket</td>
<td>User age brackets.</td>
</tr>
<tr class="odd">
<td>userGender</td>
<td>User gender.</td>
</tr>
<tr class="even">
<td>activeUsers</td>
<td>The number of distinct users who visited your website or application.</td>
</tr>
<tr class="odd">
<td>engagedSessions</td>
<td>The number of sessions that had an engaged event.</td>
</tr>
<tr class="even">
<td>engagementRate</td>
<td>The percentage of sessions that had an engaged event.</td>
</tr>
<tr class="odd">
<td>eventCount</td>
<td>The count of events.</td>
</tr>
<tr class="even">
<td>keyEvents</td>
<td>The number of key events that occurred.</td>
</tr>
<tr class="odd">
<td>newUsers</td>
<td>The number of users who interacted with your site or launched your app for the first time (event triggered: first_open or first_visit).</td>
</tr>
<tr class="even">
<td>totalRevenue</td>
<td>The sum of revenue from purchases, subscriptions, and advertising (Purchase revenue plus Subscription revenue plus Ad revenue) minus refunded transaction revenue.</td>
</tr>
<tr class="odd">
<td>totalUsers</td>
<td>The number of distinct users who have logged at least one event, regardless of whether the site or app was in use when that event was logged.</td>
</tr>
<tr class="even">
<td>userEngagementDuration</td>
<td>The total amount of time (in seconds) your website or app was in the foreground of users' devices.</td>
</tr>
<tr class="odd">
<td>userKeyEventRate</td>
<td>The percentage of users who triggered any key event.</td>
</tr>
</tbody>
</table>

Table Name: EcommercePurchases

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>itemBrand</td>
<td>Brand name of the item.</td>
</tr>
<tr class="even">
<td>itemCategory</td>
<td>The hierarchical category in which the item is classified. For example, in Apparel/Mens/Summer/Shirts/T-shirts, Apparel is the item category.</td>
</tr>
<tr class="odd">
<td>itemCategory2</td>
<td>The hierarchical category in which the item is classified. For example, in Apparel/Mens/Summer/Shirts/T-shirts, Mens is the item category 2.</td>
</tr>
<tr class="even">
<td>itemCategory3</td>
<td>The hierarchical category in which the item is classified. For example, in Apparel/Mens/Summer/Shirts/T-shirts, Summer is the item category 3.</td>
</tr>
<tr class="odd">
<td>itemCategory4</td>
<td>The hierarchical category in which the item is classified. For example, in Apparel/Mens/Summer/Shirts/T-shirts, Shirts is the item category 4.</td>
</tr>
<tr class="even">
<td>itemCategory5</td>
<td>The hierarchical category in which the item is classified. For example, in Apparel/Mens/Summer/Shirts/T-shirts, T-shirts is the item category 5.</td>
</tr>
<tr class="odd">
<td>itemId</td>
<td>The ID of the item.</td>
</tr>
<tr class="even">
<td>itemListPosition</td>
<td>The position of an item in a list. For example, a product you sell in a list. This dimension is populated in tagging by the index parameter in the items array.</td>
</tr>
<tr class="odd">
<td>itemName</td>
<td>The name of the item.</td>
</tr>
<tr class="even">
<td>itemVariant</td>
<td>The specific variation of a product. For example, XS, S, M, or L for size; or Red, Blue, Green, or Black for color. Populated by the item_variant parameter.</td>
</tr>
<tr class="odd">
<td>itemAddedToCart</td>
<td>The number of units added to cart for a single item. This metric counts the quantity of items in add_to_cart events.</td>
</tr>
<tr class="even">
<td>itemRevenue</td>
<td>The total revenue from purchases minus refunded transaction revenue from items only. Item revenue is the product of its price and quantity. Item revenue excludes tax and shipping values; tax &amp; shipping values are specified at the event and not item level.</td>
</tr>
<tr class="odd">
<td>itemsPurchased</td>
<td>The number of units for a single item included in purchase events. This metric counts the quantity of items in purchase events.</td>
</tr>
<tr class="even">
<td>itemsViewed</td>
<td>The number of units viewed for a single item. This metric counts the quantity of items in view_item events.</td>
</tr>
</tbody>
</table>

Table Name: Events

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>eventName</td>
<td>The name of the event.</td>
</tr>
<tr class="even">
<td>eventCount</td>
<td>The count of events.</td>
</tr>
<tr class="odd">
<td>eventCountPerUser</td>
<td>The average number of events per user (Event count divided by Active users).</td>
</tr>
<tr class="even">
<td>totalRevenue</td>
<td>The sum of revenue from purchases, subscriptions, and advertising (Purchase revenue plus Subscription revenue plus Ad revenue) minus refunded transaction revenue.</td>
</tr>
<tr class="odd">
<td>totalUsers</td>
<td>The number of distinct users who have logged at least one event, regardless of whether the site or app was in use when that event was logged.</td>
</tr>
</tbody>
</table>

Table Name: LandingPage

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>landingPage</td>
<td>The page path associated with the first pageview in a session.</td>
</tr>
<tr class="even">
<td>activeUsers</td>
<td>The number of distinct users who visited your website or application.</td>
</tr>
<tr class="odd">
<td>keyEvents</td>
<td>The number of key events that occurred.</td>
</tr>
<tr class="even">
<td>newUsers</td>
<td>The number of users who interacted with your site or launched your app for the first time (event triggered: first_open or first_visit).</td>
</tr>
<tr class="odd">
<td>sessionKeyEventRate</td>
<td>The percentage of sessions in which any key event was triggered.</td>
</tr>
<tr class="even">
<td>sessions</td>
<td>The number of sessions that began on your site or app (event triggered: session_start).</td>
</tr>
<tr class="odd">
<td>totalRevenue</td>
<td>The sum of revenue from purchases, subscriptions, and advertising (Purchase revenue plus Subscription revenue plus Ad revenue) minus refunded transaction revenue.</td>
</tr>
<tr class="even">
<td>userEngagementDurationPerSession</td>
<td>Average engagement time per session</td>
</tr>
</tbody>
</table>

Table Name: PagesAndScreens

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>contentGroup</td>
<td>A category that applies to items of published content. Populated by the event parameter content_group.</td>
</tr>
<tr class="even">
<td>unifiedPagePathScreen</td>
<td>The page path (web) or screen class (app) on which the event was logged.</td>
</tr>
<tr class="odd">
<td>unifiedScreenClass</td>
<td>The page title (web) or screen class (app) on which the event was logged.</td>
</tr>
<tr class="even">
<td>unifiedScreenName</td>
<td>The page title (web) or screen name (app) on which the event was logged.</td>
</tr>
<tr class="odd">
<td>activeUsers</td>
<td>The number of distinct users who visited your website or application.</td>
</tr>
<tr class="even">
<td>eventCount</td>
<td>The count of events.</td>
</tr>
<tr class="odd">
<td>keyEvents</td>
<td>The number of key events that occurred.</td>
</tr>
<tr class="even">
<td>screenPageViews</td>
<td>The number of app screens or web pages your users viewed. Repeated views of a single page or screen are counted. (screen_view + page_view events).</td>
</tr>
<tr class="odd">
<td>screenPageViewsPerUser</td>
<td>The number of app screens or web pages your users viewed per active user. Repeated views of a single page or screen are counted. (screen_view + page_view events) / active users.</td>
</tr>
<tr class="even">
<td>totalRevenue</td>
<td>The sum of revenue from purchases, subscriptions, and advertising (Purchase revenue plus Subscription revenue plus Ad revenue) minus refunded transaction revenue.</td>
</tr>
<tr class="odd">
<td>userEngagementDuration</td>
<td>The total amount of time (in seconds) your website or app was in the foreground of users' devices.</td>
</tr>
</tbody>
</table>

Table Name: Promotions

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>itemPromotionCreativeName</td>
<td>The name of the item-promotion creative.</td>
</tr>
<tr class="even">
<td>itemPromotionId</td>
<td>The ID of the promotion.</td>
</tr>
<tr class="odd">
<td>itemPromotionName</td>
<td>The name of the promotion for the item.</td>
</tr>
<tr class="even">
<td>itemListPosition</td>
<td>The position of an item in a list. For example, a product you sell in a list. This dimension is populated in tagging by the index parameter in the items array.</td>
</tr>
<tr class="odd">
<td>itemAddedToCart</td>
<td>The number of units added to cart for a single item. This metric counts the quantity of items in add_to_cart events.</td>
</tr>
<tr class="even">
<td>itemCheckedOut</td>
<td>The number of units checked out for a single item. This metric counts the quantity of items in begin_checkout events.</td>
</tr>
<tr class="odd">
<td>itemPromotionClickThroughRate</td>
<td>The number of users who selected a promotion(s) divided by the number of users who viewed the same promotion(s). This metric is returned as a fraction; for example, 0.1382 means 13.82% of users who viewed a promotion also selected the promotion.</td>
</tr>
<tr class="even">
<td>itemRevenue</td>
<td>The total revenue from purchases minus refunded transaction revenue from items only. Item revenue is the product of its price and quantity. Item revenue excludes tax and shipping values; tax &amp; shipping values are specified at the event and not item level.</td>
</tr>
<tr class="odd">
<td>itemsClickedInPromotion</td>
<td>The number of units clicked in promotion for a single item. This metric counts the quantity of items in select_promotion events.</td>
</tr>
<tr class="even">
<td>itemsPurchased</td>
<td>The number of units for a single item included in purchase events. This metric counts the quantity of items in purchase events.</td>
</tr>
<tr class="odd">
<td>itemsViewedInPromotion</td>
<td>The number of units viewed in promotion for a single item. This metric counts the quantity of items in view_promotion events.</td>
</tr>
</tbody>
</table>

Table Name: TechDetails

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>appVersion</td>
<td>The app's versionName (Android) or short bundle version (iOS).</td>
</tr>
<tr class="even">
<td>browser</td>
<td>The browsers used to view your website.</td>
</tr>
<tr class="odd">
<td>deviceCategory</td>
<td>The type of device: Desktop, Tablet, or Mobile.</td>
</tr>
<tr class="even">
<td>operatingSystem</td>
<td>The operating systems used by visitors to your app or website. Includes desktop and mobile operating systems such as Windows and Android.</td>
</tr>
<tr class="odd">
<td>operatingSystemVersion</td>
<td>The operating system versions used by visitors to your website or app. For example, Android 10's version is 10, and iOS 13.5.1's version is 13.5.1.</td>
</tr>
<tr class="even">
<td>operatingSystemWithVersion</td>
<td>The operating system and version. For example, Android 10 or Windows 7.</td>
</tr>
<tr class="odd">
<td>platform</td>
<td>The platform on which your app or website ran; for example, web, iOS, or Android. To determine a stream's type in a report, use both platform and streamId.</td>
</tr>
<tr class="even">
<td>platformDeviceCategory</td>
<td>The platform and type of device on which your website or mobile app ran. (example: Android / mobile)</td>
</tr>
<tr class="odd">
<td>screenResolution</td>
<td>The screen resolution of the user's monitor. For example, 1920x1080.</td>
</tr>
<tr class="even">
<td>activeUsers</td>
<td>The number of distinct users who visited your website or application.</td>
</tr>
<tr class="odd">
<td>engagedSessions</td>
<td>The number of sessions that lasted longer than 10 seconds, or had a key event, or had 2 or more screen views.</td>
</tr>
<tr class="even">
<td>engagementRate</td>
<td>The percentage of engaged sessions (Engaged sessions divided by Sessions). This metric is returned as a fraction; for example, 0.7239 means 72.39% of sessions were engaged sessions.</td>
</tr>
<tr class="odd">
<td>eventCount</td>
<td>The count of events.</td>
</tr>
<tr class="even">
<td>keyEvents</td>
<td>The number of key events that occurred.</td>
</tr>
<tr class="odd">
<td>newUsers</td>
<td>The number of users who interacted with your site or launched your app for the first time (event triggered: first_open or first_visit).</td>
</tr>
<tr class="even">
<td>totalRevenue</td>
<td>The sum of revenue from purchases, subscriptions, and advertising (Purchase revenue plus Subscription revenue plus Ad revenue) minus refunded transaction revenue.</td>
</tr>
<tr class="odd">
<td>userEngagementDuration</td>
<td>The total amount of time (in seconds) your website or app was in the foreground of users' devices.</td>
</tr>
</tbody>
</table>

Table Name: TrafficAcquisition

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>sessionCampaignName</td>
<td>The marketing campaign name for a session. Includes Google Ads Campaigns, Manual Campaigns, &amp; other Campaigns.</td>
</tr>
<tr class="even">
<td>sessionDefaultChannelGroup</td>
<td>The session's default channel group is based primarily on source and medium. An enumeration which includes Direct, Organic Search, Paid Social, Organic Social, Email, Affiliates, Referral, Paid Search, Video, and Display.</td>
</tr>
<tr class="odd">
<td>sessionMedium</td>
<td>The medium that initiated a session on your website or app.</td>
</tr>
<tr class="even">
<td>sessionPrimaryChannelGroup</td>
<td>The primary channel group that led to the session. Primary channel groups are the channel groups used in standard reports in Google Analytics and serve as an active record of your property's data in alignment with channel grouping over time.</td>
</tr>
<tr class="odd">
<td>sessionSource</td>
<td>The source that initiated a session on your website or app.</td>
</tr>
<tr class="even">
<td>sessionSourceMedium</td>
<td>The combined values of the dimensions sessionSource and sessionMedium.</td>
</tr>
<tr class="odd">
<td>sessionSourcePlatform</td>
<td>The source platform of the session's campaign. Don't depend on this field returning Manual for traffic that uses UTMs; this field will update from returning Manual to returning (not set) for an upcoming feature launch.</td>
</tr>
<tr class="even">
<td>eventCount</td>
<td>The count of events.</td>
</tr>
<tr class="odd">
<td>eventsPerSession</td>
<td>The average number of events per session (Event count divided by Sessions).</td>
</tr>
<tr class="even">
<td>engagementRate</td>
<td>The percentage of engaged sessions (Engaged sessions divided by Sessions). This metric is returned as a fraction; for example, 0.7239 means 72.39% of sessions were engaged sessions.</td>
</tr>
<tr class="odd">
<td>engagedSessions</td>
<td>The number of sessions that lasted longer than 10 seconds, or had a key event, or had 2 or more screen views.</td>
</tr>
<tr class="even">
<td>keyEvents</td>
<td>The number of key events that occurred.</td>
</tr>
<tr class="odd">
<td>sessions</td>
<td>The number of sessions that began on your site or app (event triggered: session_start).</td>
</tr>
<tr class="even">
<td>sessionKeyEventRate</td>
<td>The percentage of sessions in which any key event was triggered.</td>
</tr>
<tr class="odd">
<td>sessionsPerUser</td>
<td>The average number of sessions per user (Sessions divided by Active Users).</td>
</tr>
<tr class="even">
<td>totalRevenue</td>
<td>The sum of revenue from purchases, subscriptions, and advertising (Purchase revenue plus Subscription revenue plus Ad revenue) minus refunded transaction revenue.</td>
</tr>
<tr class="odd">
<td>userEngagementDurationPerSession</td>
<td>Average engagement time per session</td>
</tr>
</tbody>
</table>

Table Name: UserAcquisition

<table>
<thead>
<tr class="header">
<th>Field Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>firstUserCampaignName</td>
<td>Name of the marketing campaign that first acquired the user. Includes Google Ads Campaigns, Manual Campaigns, &amp; other Campaigns.</td>
</tr>
<tr class="even">
<td>firstUserDefaultChannelGroup</td>
<td>The default channel group that first acquired the user. Default channel group is based primarily on source and medium. An enumeration which includes Direct, Organic Search, Paid Social, Organic Social, Email, Affiliates, Referral, Paid Search, Video, and Display.</td>
</tr>
<tr class="odd">
<td>firstUserMedium</td>
<td>The medium that first acquired the user to your website or app.</td>
</tr>
<tr class="even">
<td>firstUserPrimaryChannelGroup</td>
<td>The primary channel group that originally acquired a user. Primary channel groups are the channel groups used in standard reports in Google Analytics and serve as an active record of your property's data in alignment with channel grouping over time.</td>
</tr>
<tr class="odd">
<td>firstUserSource</td>
<td>The source that first acquired the user to your website or app.</td>
</tr>
<tr class="even">
<td>firstUserSourceMedium</td>
<td>The combined values of the dimensions firstUserSource and firstUserMedium.</td>
</tr>
<tr class="odd">
<td>firstUserSourcePlatform</td>
<td>The source platform that first acquired the user. Don't depend on this field returning Manual for traffic that uses UTMs; this field will update from returning Manual to returning (not set) for an upcoming feature launch.</td>
</tr>
<tr class="even">
<td>activeUsers</td>
<td>The number of distinct users who visited your website or application.</td>
</tr>
<tr class="odd">
<td>engagedSessions</td>
<td>The number of sessions that lasted longer than 10 seconds, or had a key event, or had 2 or more screen views.</td>
</tr>
<tr class="even">
<td>engagementRate</td>
<td>The percentage of engaged sessions (Engaged sessions divided by Sessions). This metric is returned as a fraction; for example, 0.7239 means 72.39% of sessions were engaged sessions.</td>
</tr>
<tr class="odd">
<td>eventCount</td>
<td>The count of events.</td>
</tr>
<tr class="even">
<td>keyEvents</td>
<td>The number of key events that occurred.</td>
</tr>
<tr class="odd">
<td>newUsers</td>
<td>The number of users who interacted with your site or launched your app for the first time (event triggered: first_open or first_visit).</td>
</tr>
<tr class="even">
<td>totalRevenue</td>
<td>The sum of revenue from purchases, subscriptions, and advertising (Purchase revenue plus Subscription revenue plus Ad revenue) minus refunded transaction revenue.</td>
</tr>
<tr class="odd">
<td>totalUsers</td>
<td>The number of distinct users who have logged at least one event, regardless of whether the site or app was in use when that event was logged.</td>
</tr>
<tr class="even">
<td>userEngagementDuration</td>
<td>The total amount of time (in seconds) your website or app was in the foreground of users' devices.</td>
</tr>
<tr class="odd">
<td>userKeyEventRate</td>
<td>The percentage of users who triggered any key event.</td>
</tr>
</tbody>
</table>
