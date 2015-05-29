minimob offervault API Guide 
=============================

##### About This Guide

This is the offervault API Guide, version 1.0, of minimob.

Getting started with minimob offervault api
===========================================

Introduction
------------

The purpose of the minimob offervault api is to help you to implement
automated offer importing to your system by using the ad serving
technology platform of your choice. Note that minimob offervault api is
NOT an adserving api to be used for direct ad serving.

minimob offervault api allows access to the following resources and
actions of minimob offervault service:

-   **available offers**: all offers that are available to you and you
    can by requesting approval have access to use them

-   **available offer details**: detailed information for a particular
    offer

-   **my offers**: all offers that you have access to use

-   **my offer details**: detailed information for a particular offer
    that you are allowed to use

-   **approval request**: for gaining access you must send an approval
    request for a particular offer

The API is based on HTTP protocol and all data interchanged are in JSON
format.

Prerequisites
-------------

For having access to offervault api you must have a valid minimob
account. Each minimob account is uniquely associated with a randomly
generated api key. All requests require the parameter api key in order
to identify and authorize your request.

> **Note**: To see your API key, sign in to your account and navigate to
> the API page of the offervault. By default, your API key is included
> in the url that is displayed for each API call.

API Calls and Responses
-----------------------

The API calls have the following format:

-   *API Endpoint*: the url that corresponds to the specific API call

-   *apikey*: your unique api key

-   *Call specific parameters*: depending on the API call, you may need
    to include additional parameters that are specific to the particular
    call

The response to an API call can be:

-   A *JSON object*, where its properties are contained in **{**curly
    brackets**}**

<!-- -->

-   A *JSON array of objects*, where the collection of the objects is
    contained in **[**square brackets**]**

### Available Offers

This API Call returns summarized information about all the offers that
are available in minimob.

*Url:*
<http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key>

*HTTP method:* GET

*Returns:* json array of objects [{},{}….{}]

Each JSON object contains the following properties:

-   **id**: [*string*] the offer's id that is unique across the minimob
    platform

-   **name**: [*string*] the name of the offer

-   **targetedCountries**: [*string*] the list of countries in which the
    offer can be served (country codes as per [ISO 3166-1
    alpha-2](https://www.iso.org/obp/ui/#search))

-   **payout**: [*double*] the monetary compensation per each goal
    achieved as defined by the payout model

-   **payoutCurrency**: [*string*] the currency of the payout (**search
    for currency ISO** codes)

-   **payoutModel**: [*string*] the model on which the payout is based
    (currently CPI only is supported)

-   **targetPlatform**: [*string*] the mobile operating system that is
    targeted

-   **overallConversionCap**: [nullable *int*] the conversion cap for
    the entire lifetime of the offer

-   **dailyConversionCap**: [nullable *int*] the conversion cap per day

-   **weeklyConversionCap**: [nullable *int*] the conversion cap per
    week

-   **monthlyConversionCap**: [nullable *int*] the conversion cap per
    month

-   **status**: [*enum*] indicates the status of the offer. It can have
    one of the following values:

    -   0: The offer is *Available* for you to request it

    -   1: Your request for this offer is *Pending*

-   **incentivized**: indicates whether the offer is allowed to run on
    incentivized traffic or not. It can have one of the following
    values:

    -   0: Both Incentivized traffic and Non-Incentivized traffic are
        allowed

    -   1: Incentivized traffic only

    -   2: Non-Incentivized traffic only

    -   3: Uncertain (the offer is allowed to run on both Incentivized
        traffic and Non-Incentivized traffic)

-   **incentivizedDescription**: [*string*] a textual description
    regarding whether the offer is *Incentivized*

-   **storeId**: [*string*] indicates the store through which the
    application is distributed. It can have one of the following values:

    -   1: corresponds to *Google Play*

    -   2: corresponds to *Apple iTunes*

    -   3: corresponds to *Minimob Store*

-   **storeName**: [*string*] the name of the store through which the
    application is distributed

###### **Example**

An example of the response is given below:

    [
    	{
    		"id": " FFFFFFFFFFFFFFF",
    		"name": "Hello minimob app offer (incent)",
    		"targetedCountries": [
    			"NZ",
    			"GB",
    			"GR"
    		],
    		"payout": 0.42,
    		"payoutCurrency": "USD",
    		"payoutModel": "CPI",
    		"targetPlatform": "iOS",
    		"overallConversionCap": 10000,
    		"dailyConversionCap": 500,
    		"weeklyConversionCap": 2000,
    		"monthlyConversionCap": 5000,
    		"status": 0,
    		"incentivized": 1,
    		"incentivizedDescription": "Incentivized",
    		"storeId": "2",
    		"storeName": " Apple iTunes "
    	},
    	{
    		"id": " FFFFFFFFFFFFFFFE",
    		"name": "Hello world app offer",
    		"targetedCountries": [
    			"CR"
    		],
    		"payout": 1.7,
    		"payoutCurrency": "USD",
    		"payoutModel": "CPI",
    		"targetPlatform": "Android",
    		"overallConversionCap": 40000,
    		"dailyConversionCap": 300,
    		"weeklyConversionCap": 3000,
    		"monthlyConversionCap": 10000,
    		"status": 0,
    		"incentivized": 0,
    		"incentivizedDescription": "BothIncentivizedAndNot",
    		"storeId": "1",
    		"storeName": "Google Play"
    	}
    ]

### Available Offer Details

This API Call returns the full details of an offer that is available for
you to request it.

In addition to the **apikey**, you need to include the **id** of the
offer to the url.

*Url:*
<http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key&id=an_available_offer_id>

*HTTP method:* GET

*Returns:* json object

The JSON object contains the following properties:

-   **id**: *as per description in* **Available Offers**

-   **name**: *as per description in* **Available Offers**

-   **targetedCountries**: *as per description in* **Available Offers**

-   **payout**: *as per description in* **Available Offers**

-   **payoutCurrency**: *as per description in* **Available Offers**

-   **payoutModel**: *as per description in* **Available Offers**

-   **targetPlatform**: *as per description in* **Available Offers**

-   **description**: [*string*] A detailed description of the offer

-   **overallConversionCap**: *as per description in* **Available
    Offers**

-   **dailyConversionCap**: *as per description in* **Available Offers**

-   **weeklyConversionCap**: *as per description in* **Available
    Offers**

-   **monthlyConversionCap**: *as per description in* **Available
    Offers**

-   **appIconLink**: [*string*] a url which points to the icon of the
    application through which the offer is promoted

-   **appTitle**: [*string*] the title of the application

-   **appId**: [*string*] the application ID (as registered to the app
    store)

-   **appDescription**: [*string*] A detailed description of the
    application

-   **appPreviewLink**: [*string*] A link directing to the application
    page in the app store

-   **expirationDate**: [*string*] Specifies the date until which the
    offer can be promoted

-   **incentivized**: *as per description in* **Available Offers**

-   **incentivizedDescription**: *as per description in* **Available
    Offers**

-   **storeId**: *as per description in* **Available Offers**

-   **storeName**: *as per description in* **Available Offers**

<!-- -->

-   **creatives**: Contains the creatives that are associated with the
    offer. For each creative, the following are returned:

    -   **Id**: [*string*] the unique id of the creative

    -   **previewUrl**: [*string*] the url where you can preview the
        creative

    -   **mimeType**: [*string*] the mime type of the creative

    -   **dimensions**: [*string*] the dimensions of the creative

    -   **locale**: [*string*] the locales supported by the creative
        [Feature to be supported in a future release]

###### Example

An example of the response is given below:

    {
    	"id": "FAFAFAFAFAFAFA",
    	"name": "minimob app offer",
    	"payoutModel": "CPI",
    	"payout": 0.13,
    	"payoutCurrency": "USD",
    	"targetedCountries": [
    		"BR"
    	],
    	"targetPlatform": "Android",
    	"description": "this is a sample app offer description",
    	"overallConversionCap": 0,
    	"dailyConversionCap": 100,
    	"weeklyConversionCap": 0,
    	"monthlyConversionCap": 0,
    	"appIconLink": " https://lh5.ggpht.com/F_A_K_E_2NnqKdVDrfCkDQeUPTi8Rptn3hgqQQzbO-rNJhBJsMVn39TENB=b200",
    	"appTitle": "minimob app",
    	"appId": "com.minimob.app",
    	"appDescription": "Minimob app makes you happy.",
    	"appPreviewLink": "https://play.google.com/store/apps/details?hl=en&id=com.minimob.app",
    	"expirationDate": "12/31/2018 10:00:00 PM",
    	"incentivized": 2,
    	"incentivizedDescription": "NonIncentivized",
    	"storeId": "1",
    	"storeName": "Google Play",
    	"creatives": [
    		{
    			"Id": "5498257d2e9be1171c07ae53",
    			"previewUrl": "http://cdn.minimob.com/creative/2000FCF4-3169-4FCD-8E0C-41FB0C8DA377.jpg",
    			"mimeType": "image/jpeg",
    			"dimensions": "120x20",
    			"locale": ""
    		},
    		{
    			"Id": "5498257e2e9be1171c07ae55",
    			"previewUrl": "http://cdn.minimob.com/creative/2000FCF4-3169-4FCD-8E0C-41FB0C8DA377.jpg",
    			"mimeType": "image/jpeg",
    			"dimensions": "168x28",
    			"locale": ""
    		},
    		{
    			"Id": "5498257f2e9be1171c07ae57",
    			"previewUrl": "http://cdn.minimob.com/creative/2000FCF4-3169-4FCD-8E0C-41FB0C8DA377.jpg",
    			"mimeType": "image/jpeg",
    			"dimensions": "168x42",
    			"locale": ""
    		}
    	]
    }

### My Offers

This API Call returns summarized information about all the offers that
you have been approved to promote.

> **Note**: In order to better serve requests for **My Offers**, the
> same user is not allowed to make more than one such API Call per
> minute.

*Url:* <http://dashboard.minimob.com/api/myoffers/?apikey=your_api_key>

*HTTP method:* GET

*Returns:* json array of objects

Each JSON object contains the following properties:

-   **id**: *as per description in* **Available Offers**

-   **name**: *as per description in* **Available Offers**

-   **targetedCountries**: *as per description in* **Available Offers**

-   **incentivized**: [*string*] a textual description regarding whether
    the offer is *Incentivized*

-   **storeName**: *as per description in* **Available Offers**

-   **qualityScore**: [nullable *double*] An index indicative of the
    reliability of the offer (the higher the better), which is
    calculated based on a proprietary ranking algorithm developed by the
    minimob development team

-   **payout**: *as per description in* **Available Offers**

-   **payoutCurrency**: *as per description in* **Available Offers**

-   **payoutModel**: *as per description in* **Available Offers**

-   **targetPlatform**: *as per description in* **Available Offers**

-   **overallConversionCap**: [nullable *int*] the remaining conversion
    cap until the expiration of the offer

-   **dailyConversionCap**: [nullable *int*] the remaining conversion
    cap until the end of the current day

-   **weeklyConversionCap**: [nullable *int*] the remaining conversion
    cap until the end of the current week

-   **monthlyConversionCap**: [nullable *int*] the remaining conversion
    cap until the end of the current month

###### Example

An example of the response is given below:

    [
    	{
    		"id": "ffffe",
    		"name": "minimob app offer",
    		"targetedCountries": [
    			"IN"
    		],
    		"incentivized": "NonIncentivized",
    		"storeName": "Google Play",
    		"qualityScore": 159.98785667625523,
    		"payout": 0.39,
    		"payoutCurrency": "USD",
    		"payoutModel": "CPI",
    		"targetPlatform": "Android",
    		"overallConversionCap": null,
    		"dailyConversionCap": 2843,
    		"weeklyConversionCap": null,
    		"monthlyConversionCap": null
    	},
    	{
    		"id": "ffffd",
    		"name": "minimob app next offer",
    		"targetedCountries": [
    			"FR"
    		],
    		"incentivized": "Incentivized",
    		"storeName": "Google Play",
    		"qualityScore": 166.99970029044277,
    		"payout": 0.48,
    		"payoutCurrency": "USD",
    		"payoutModel": "CPI",
    		"targetPlatform": "Android",
    		"overallConversionCap": null,
    		"dailyConversionCap": 1716,
    		"weeklyConversionCap": null,
    		"monthlyConversionCap": null
    	}
    ]

### My Offers Details

This API Call returns the details of an offer that you have been
approved to promote.

In addition to the **apikey**, you need to include the **id** of the
offer to the url.

*Url:*
<http://dashboard.minimob.com/api/myoffers/?apikey=your_api_key&id=my_offer_id>

*HTTP method:* GET

*Returns:* json object

The JSON object contains the following properties:

-   **id**: *as per description in* **Available Offers**

-   **name**: *as per description in* **Available Offers**

-   **payout**: *as per description in* **Available Offers**

-   **payoutCurrency**: *as per description in* **Available Offers**

-   **payoutModel**: *as per description in* **Available Offers**

<!-- -->

-   **targetedCountries**: *as per description in* **Available Offers**

<!-- -->

-   **targetPlatform**: *as per description in* **Available Offers**

-   **description**: *as per description in* **Available Offers
    Details**

-   **overallConversionCap**: *as per description in* **My Offers**

-   **dailyConversionCap**: *as per description in* **My Offers**

-   **weeklyConversionCap**: *as per description in* **My Offers**

-   **monthlyConversionCap**: *as per description in* **My Offers**

-   **appIconLink**: *as per description in* **Available Offers Details
    **

-   **appTitle**: *as per description in* **Available Offers Details **

-   **appId**: *as per description in* **Available Offers Details **

-   **appDescription**: *as per description in* **Available Offers
    Details **

-   **appPreviewLink**: *as per description in* **Available Offers
    Details **

-   **expirationDate**: *as per description in* **Available Offers
    Details **

-   **incentivized**: *as per description in* **My Offers**

-   **storeName**: *as per description in* **Available Offers**

-   **objectiveUrl**: [*string*] the link for redirecting the end user
    to the app store for downloading the app, as well as for notifying
    minimob when a user clicks on the offer. The format of the url can
    be customized through the UI of the minimob application, but, in
    general, it consists of the following:

    -   **clicks.minimob.com/tracking/click?** : the tracking url

    -   **clickid**: a parameter for holding the click id that
        corresponds to a user (its value can be customized)

    -   **trafficsource**: the unique id which has been assigned by the
        system to your traffic source

    <!-- -->

    -   **offerid**: a unique id that identifies the particular campaign
        through which the offer is being promoted

    <!-- -->

    -   custom parameters: any additional parameters that you may have
        defined when configuring (though the UI) the format of the click
        url

-   **creatives**: *as per description in* **Available Offers Details **

<!-- -->

-   **acquisitionModel**: [*string*] the name of the acquisition model

-   **acquisitionModelDescription**: [*string*] the description of the
    acquisition model

-   **qualityScore**: *as per description in* **My Offers**

<!-- -->

-   **qualityScorePerCountry**: Contains the quality score per country.
    For each country of the offer, the following are returned:

    -   **countryCode**: [*string*] the country code

    -   **qualityScore**: *as per description in* **My Offers**

###### Example

An example of the response is given below:

    {
    	"id": "ffffe",
    	"name": "minimob app offer",
    	"payoutModel": "CPI",
    	"payout": 0.52,
    	"payoutCurrency": "USD",
    	"targetedCountries": [
    		"ID"
    	],
    	"targetPlatform": "Android",
    	"description": "this is a sample app offer description",
    	"overallConversionCap": 0,
    	"dailyConversionCap": 2000,
    	"weeklyConversionCap": 0,
    	"monthlyConversionCap": 0,
    	"appIconLink": "https://lh6.ggpht.com/F_A_K_E_2NnqKdVDrfCkDQeUPTi8Rptn3hgqQQzbO-rNJhBJsMVn39TENB=b200",
    	"appTitle": "minimob app",
    	"appId": "com.minimob.app",
    	"appDescription": "Minimob app makes you happy.",
    	"appPreviewLink": "https://play.google.com/store/apps/details?hl=en&id=com.minimob.app",
    	"expirationDate": "12/31/2018 10:00:00 PM",
    	"incentivized": "NonIncentivized",
    	"storeName": "Google Play",
    	"objectiveUrl": "http://clicks.minimob.com/tracking/click?clickid=[[clickid]]&trafficsource=1373664459&cid=[[cid]]&offerid=151494",
    	"creatives": [
    		{
    			"Id": "5498257d2e9be1171c07ae53",
    			"previewUrl": "http://cdn.minimob.com/creative/2000FCF4-3169-4FCD-8E0C-41FB0C8DA377.jpg",
    			"mimeType": "image/jpeg",
    			"dimensions": "120x20",
    			"locale": ""
    		},
    		{
    			"Id": "5498257e2e9be1171c07ae55",
    			"previewUrl": "http://cdn.minimob.com/creative/2000FCF4-3169-4FCD-8E0C-41FB0C8DA377.jpg",
    			"mimeType": "image/jpeg",
    			"dimensions": "168x28",
    			"locale": ""
    		},
    		{
    			"Id": "5498257f2e9be1171c07ae57",
    			"previewUrl": "http://cdn.minimob.com/creative/2000FCF4-3169-4FCD-8E0C-41FB0C8DA377.jpg",
    			"mimeType": "image/jpeg",
    			"dimensions": "168x42",
    			"locale": ""
    		}
    	],
    	"acquisitionModel": "CPI",
    	"acquisitionModelDescription": "USER FLOW:\n\n1) User clicks on creative and is forwarded to Apple / Google Play Store\n2) User downloads the App on the phone\n3) User opens the App after download",
    	"qualityScore": 25.858030913895444,
    	"qualityScorePerCountry": [
    		{
    			"countryCode": "US",
    			"qualityScore": 0
    		},
    		{
    			"countryCode": "ID",
    			"qualityScore": 25.858030913895444
    		}
    	]
    }

### Approval Request

In order to gain access to a minimob offer a user has to make an
approval request which needs to be accepted by a minimob account
manager.

*Url:*
<http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key>

*HTTP method:* POST

*Request Header:* Content-Type:application/json

*Request Body:* json array of strings where each string is an available
offer id. Example: ["00000000000000","00000000000001"]

*Returns:* json array of objects

###### **Example**

Assuming that you have you have made the following request for the
specific offer ids:

    ["00000000000000","00000000000001"]

You would get the following response:

    [
    	"00000000000000",
    	"00000000000001"
    ]
