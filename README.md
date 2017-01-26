<div id="D-Entire-document">
<h1>Minimob Offers API Guide</h1>
<div id="D-introduction">
<h3>Introduction</h3>
   <p>The purpose of the Minimob API for Monetization is to help you to implement automated offer importing to your system by using the ad serving technology platform of your choice. Note that this is NOT an ad serving API to be used for direct ad serving.</p>
<h5>Prerequisites</h5>
   <p>For having access to the API you must have a valid Minimob account. Each Minimob account is uniquely associated with a randomly generated API key. All requests require the parameter API key in order to identify and authorize your request.</p>
<h5>API Calls and Responses</h5>
   <p>The API is based on HTTP protocol and all data interchanged are in JSON format.</p>
   <p>The API calls have the following format:</p>
<ul>
    <li><em>API Endpoint</em>: the url that corresponds to the specific API call</li>
    <li><em>apikey</em>: your unique API key </li>
    <li><em>Call specific parameters</em>: depending on the API call, you may need to include additional parameters that are specific to the particular call</li>
</ul>
   <p>The response to an API call can be:</p>
<ul>
    <li>A <em>JSON object</em>, where its properties are contained in <strong>{</strong>curly brackets<strong>}</strong> </li>
    <li>A <em>JSON array of objects</em>, where the collection of the objects is contained in <strong>[</strong>square brackets<strong>]</strong> </li>
</ul>
<h5>Versions</h5>
   <p>There are two versions available: API 1.0 and API 1.1. Version 1.1 provides a single call for getting the details of all offers which have been approved for you.</p>
</div>
<div id="D-api10">
<h3>API 1.0</h3>
   <p>Version 1.0 of the API allows access to the following Minimob resources:</p>
<ul>
    <li><strong>available offers</strong>: all offers that are available to you and you can by requesting approval have access to use them</li>
    <li><strong>available offer details</strong>: detailed information for a particular offer</li>
    <li><strong>my offers</strong>: all offers that you have access to use </li>
    <li><strong>my offer details</strong>: detailed information for a particular offer that you are allowed to use</li>
    <li><strong>approval request</strong>: for gaining access you must send an approval request for a particular offer</li>
</ul>
<div id="D-all-offers-api10">
<h4>Available Offers</h4>
   <p>This API Call returns summarized information about all the offers that are available in Minimob.</p>
   <p><em>Url:</em> <a href="http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key" target="_blank">http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key</a></p>
   <p><em>HTTP method:</em> GET</p>
   <p><em>Returns:</em> json array of objects [{},{}….{}]</p>
   <p>Each JSON object contains the following properties:</p>
<ul>
    <li><strong>id</strong>: [<em>string</em>] the offer's id that is unique across the Minimob platform</li>
    <li><strong>name</strong>: [<em>string</em>] the name of the offer</li>
    <li><strong>targetedCountries</strong>: [<em>string</em>] the list of countries in which the offer can be served (country codes as per <a href="https://www.iso.org/obp/ui/#search" target="_blank">ISO 3166-1 alpha-2</a>)</li>
    <li><strong>payout</strong>: [<em>double</em>] the monetary compensation per each goal achieved as defined by the payout model</li>
    <li><strong>payoutCurrency</strong>: [<em>string</em>] the currency of the payout (currency codes as per <a href="http://www.iso.org/iso/currency_codes" target="_blank">ISO 4217</a>)</li>
    <li><strong>payoutModel</strong>: [<em>string</em>] the model on which the payout is based (currently CPI only is supported)</li>
    <li><strong>targetPlatform</strong>: [<em>string</em>] the mobile operating system that is targeted </li>
    <li><strong>overallConversionCap</strong>: [nullable <em>int</em>] the conversion cap for the entire lifetime of the offer</li>
    <li><strong>dailyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per day</li>
    <li><strong>weeklyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per week</li>
    <li><strong>monthlyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per month</li>
    <li><strong>status</strong>: [<em>enum</em>] indicates the status of the offer. It can have one of the following values:</li>
        <ul>
        <li>0: The offer is <em>Available</em> for you to request it</li>
        <li>1: Your request for this offer is <em>Pending</em> </li>
        </ul>
    <li><strong>incentivized</strong>: indicates whether the offer is allowed to run on incentivized traffic or not. It can have one of the following values:</li>
        <ul>
        <li>0: Both Incentivized traffic and Non-Incentivized traffic are allowed</li>
        <li>1: Incentivized traffic only</li>
        <li>2: Non-Incentivized traffic only</li>
        <li>3: Uncertain (the offer is allowed to run on both Incentivized traffic and Non-Incentivized traffic)</li>
        </ul>
    <li><strong>incentivizedDescription</strong>: [<em>string</em>] a textual description regarding whether the offer is <em>Incentivized</em> </li>
    <li><strong>storeId</strong>: [<em>string</em>] indicates the store through which the application is distributed. It can have one of the following values:</li>
        <ul>
        <li>1: corresponds to <em>Google Play</em> </li>
        <li>2: corresponds to <em>Apple iTunes</em> </li>
        <li>3: corresponds to <em>Minimob Store</em> </li>
        </ul>
    <li><strong>storeName</strong>: [<em>string</em>] the name of the store through which the application is distributed </li>
</ul>
<h6>Example</h6>
   <p>An example of the response is given below:</p>
<pre class="prettyprint linenums">
<code>[
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
]</code>
</pre>
</div>
<div id="D-offer-details-api10">
<h4>Available Offer Details</h4>
   <p>This API Call returns the full details of an offer that is available for you to request it.</p>
   <p>In addition to the <strong>apikey</strong>, you need to include the <strong>id</strong> of the offer to the url.</p>
   <p><em>Url:</em> <a href="http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key&id=an_available_offer_id" target="_blank">http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key&amp;id=an_available_offer_id</a></p>
   <p><em>HTTP method:</em> GET</p>
   <p><em>Returns:</em> json object</p>
   <p>The JSON object contains the following properties:</p>
<ul>
    <li><strong>id</strong>: [<em>string</em>] the offer's id that is unique across the Minimob platform</li>
    <li><strong>name</strong>: [<em>string</em>] the name of the offer</li>
    <li><strong>targetedCountries</strong>: [<em>string</em>] the list of countries in which the offer can be served (country codes as per <a href="https://www.iso.org/obp/ui/#search" target="_blank">ISO 3166-1 alpha-2</a>)</li>
    <li><strong>payout</strong>: [<em>double</em>] the monetary compensation per each goal achieved as defined by the payout model</li>
    <li><strong>payoutCurrency</strong>: [<em>string</em>] the currency of the payout (currency codes as per <a href="http://www.iso.org/iso/currency_codes" target="_blank">ISO 4217</a>)</li>
    <li><strong>payoutModel</strong>: [<em>string</em>] the model on which the payout is based (currently CPI only is supported)</li>
    <li><strong>targetPlatform</strong>: [<em>string</em>] the mobile operating system that is targeted </li>
    <li><strong>description</strong>: [<em>string</em>] A detailed description of the offer </li>
    <li><strong>overallConversionCap</strong>: [nullable <em>int</em>] the conversion cap for the entire lifetime of the offer</li>
    <li><strong>dailyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per day</li>
    <li><strong>weeklyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per week</li>
    <li><strong>monthlyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per month</li>
    <li><strong>appIconLink</strong>: [<em>string</em>] a url which points to the icon of the application through which the offer is promoted</li>
    <li><strong>appTitle</strong>: [<em>string</em>] the title of the application </li>
    <li><strong>appId</strong>: [<em>string</em>] the application ID (as registered to the app store)</li>
    <li><strong>appDescription</strong>: [<em>string</em>] A detailed description of the application</li>
    <li><strong>appPreviewLink</strong>: [<em>string</em>] A link directing to the application page in the app store</li>
    <li><strong>expirationDate</strong>: [<em>string</em>] Specifies the date until which the offer can be promoted</li>
    <li><strong>incentivized</strong>: indicates whether the offer is allowed to run on incentivized traffic or not. It can have one of the following values:</li>
        <ul>
        <li>0: Both Incentivized traffic and Non-Incentivized traffic are allowed</li>
        <li>1: Incentivized traffic only</li>
        <li>2: Non-Incentivized traffic only</li>
        <li>3: Uncertain (the offer is allowed to run on both Incentivized traffic and Non-Incentivized traffic)</li>
        </ul>
    <li><strong>incentivizedDescription</strong>: [<em>string</em>] a textual description regarding whether the offer is <em>Incentivized</em> </li>
    <li><strong>storeId</strong>: [<em>string</em>] indicates the store through which the application is distributed. It can have one of the following values:</li>
        <ul>
        <li>1: corresponds to <em>Google Play</em> </li>
        <li>2: corresponds to <em>Apple iTunes</em> </li>
        <li>3: corresponds to <em>Minimob Store</em> </li>
        </ul>
    <li><strong>storeName</strong>: [<em>string</em>] the name of the store through which the application is distributed </li>
    <li><strong>creatives</strong>: Contains the creatives that are associated with the offer. For each creative, the following are returned: </li>
        <ul>
        <li><strong>Id</strong>: [<em>string</em>] the unique id of the creative</li>
        <li><strong>previewUrl</strong>: [<em>string</em>] the url where you can preview the creative</li>
        <li><strong>mimeType</strong>: [<em>string</em>] the mime type of the creative</li>
        <li><strong>dimensions</strong>: [<em>string</em>] the dimensions of the creative</li>
        <li><strong>locale</strong>: [<em>string</em>] the locales supported by the creative [Feature to be supported in a future release]</li>
        </ul>
</ul>
<h6>Example</h6>
   <p>An example of the response is given below:</p>
<pre class="prettyprint linenums">
<code>{
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
	"appPreviewLink": "https://play.google.com/store/apps/details?hl=en&amp;id=com.minimob.app",
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
}</code>
</pre>
</div>
<div id="D-my-offers-api10">
<h4>My Offers</h4>
   <p>This API Call returns summarized information about all the offers that you have been approved to promote.</p>
<blockquote><strong>Note</strong>: In order to better serve requests for <strong>My Offers</strong>, the same user is not allowed to make more than one such API Call per minute.</blockquote>
   <p><em>Url:</em> <a href="http://dashboard.minimob.com/api/myoffers/?apikey=your_api_key" target="_blank">http://dashboard.minimob.com/api/myoffers/?apikey=your_api_key</a></p>
   <p><em>HTTP method:</em> GET</p>
   <p><em>Returns:</em> json array of objects</p>
   <p>Each JSON object contains the following properties:</p>
<ul>
    <li><strong>id</strong>: [<em>string</em>] the offer's id that is unique across the Minimob platform</li>
    <li><strong>name</strong>: [<em>string</em>] the name of the offer</li>
    <li><strong>targetedCountries</strong>: [<em>string</em>] the list of countries in which the offer can be served (country codes as per <a href="https://www.iso.org/obp/ui/#search" target="_blank">ISO 3166-1 alpha-2</a>)</li>
    <li><strong>incentivized</strong>: [<em>string</em>] a textual description regarding whether the offer is <em>Incentivized</em> </li>
    <li><strong>storeName</strong>: [<em>string</em>] the name of the store through which the application is distributed </li>
    <li><strong>qualityScore</strong>: [nullable <em>double</em>] An index indicative of the reliability of the offer (the higher the better), which is calculated based on a proprietary ranking algorithm developed by the Minimob development team </li>
    <li><strong>payout</strong>: [<em>double</em>] the monetary compensation per each goal achieved as defined by the payout model</li>
    <li><strong>payoutCurrency</strong>: [<em>string</em>] the currency of the payout (currency codes as per <a href="http://www.iso.org/iso/currency_codes" target="_blank">ISO 4217</a>)</li>
    <li><strong>payoutModel</strong>: [<em>string</em>] the model on which the payout is based (currently CPI only is supported)</li>
    <li><strong>targetPlatform</strong>: [<em>string</em>] the mobile operating system that is targeted </li>
    <li><strong>overallConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the expiration of the offer </li>
    <li><strong>dailyConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the end of the current day </li>
    <li><strong>weeklyConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the end of the current week </li>
    <li><strong>monthlyConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the end of the current month </li>
</ul>
<h6>Example</h6>
   <p>An example of the response is given below:</p>
<pre class="prettyprint linenums">
<code>[
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
]</code>
</pre>
</div>
<div id="D-myoffer-details-api10">
<h4>My Offer Details</h4>
   <p>This API Call returns the details of an offer that you have been approved to promote.</p>
   <p>In addition to the <strong>apikey</strong>, you need to include the <strong>id</strong> of the offer to the url.</p>
   <p><em>Url:</em> <a href="http://dashboard.minimob.com/api/myoffers/?apikey=your_api_key&id=my_offer_id" target="_blank">http://dashboard.minimob.com/api/myoffers/?apikey=your_api_key&amp;id=my_offer_id</a></p>
   <p><em>HTTP method:</em> GET</p>
   <p><em>Returns:</em> json object</p>
   <p>The JSON object contains the following properties:</p>
<ul>
    <li><strong>id</strong>: [<em>string</em>] the offer's id that is unique across the Minimob platform</li>
    <li><strong>name</strong>: [<em>string</em>] the name of the offer</li>
    <li><strong>targetedCountries</strong>: [<em>string</em>] the list of countries in which the offer can be served (country codes as per <a href="https://www.iso.org/obp/ui/#search" target="_blank">ISO 3166-1 alpha-2</a>)</li>
    <li><strong>payout</strong>: [<em>double</em>] the monetary compensation per each goal achieved as defined by the payout model</li>
    <li><strong>payoutCurrency</strong>: [<em>string</em>] the currency of the payout (currency codes as per <a href="http://www.iso.org/iso/currency_codes" target="_blank">ISO 4217</a>)</li>
    <li><strong>payoutModel</strong>: [<em>string</em>] the model on which the payout is based (currently CPI only is supported)</li>
    <li><strong>targetPlatform</strong>: [<em>string</em>] the mobile operating system that is targeted </li>
    <li><strong>description</strong>: [<em>string</em>] A detailed description of the offer </li>
    <li><strong>overallConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the expiration of the offer </li>
    <li><strong>dailyConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the end of the current day </li>
    <li><strong>weeklyConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the end of the current week </li>
    <li><strong>monthlyConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the end of the current month </li>
    <li><strong>appIconLink</strong>: [<em>string</em>] a url which points to the icon of the application through which the offer is promoted</li>
    <li><strong>appTitle</strong>: [<em>string</em>] the title of the application </li>
    <li><strong>appId</strong>: [<em>string</em>] the application ID (as registered to the app store)</li>
    <li><strong>appDescription</strong>: [<em>string</em>] A detailed description of the application</li>
    <li><strong>appPreviewLink</strong>: [<em>string</em>] A link directing to the application page in the app store</li>
    <li><strong>expirationDate</strong>: [<em>string</em>] Specifies the date until which the offer can be promoted</li>
    <li><strong>incentivized</strong>: [<em>string</em>] a textual description regarding whether the offer is <em>Incentivized</em> </li>
    <li><strong>storeName</strong>: [<em>string</em>] the name of the store through which the application is distributed </li>
    <li><strong>objectiveUrl</strong>: [<em>string</em>] the link for redirecting the end user to the app store for downloading the app, as well as for notifying Minimob when a user clicks on the offer. The format of the url can be customized through the UI of the Minimob application, but, in general, it consists of the following:</li>
        <ul>
        <li><strong>clicks.minimob.com/tracking/click?</strong> : the tracking url</li>
        <li><strong>clickid</strong>: a parameter for holding the click id that corresponds to a user (its value can be customized)</li>
        <li><strong>trafficsource</strong>: the unique id which has been assigned by the system to your traffic source</li>
        <li><strong>offerid</strong>: a unique id that identifies the particular campaign through which the offer is being promoted</li>
        <li>custom parameters: any additional parameters that you may have defined when configuring (though the UI) the format of the click url</li>
        </ul>
    <li><strong>creatives</strong>: Contains the creatives that are associated with the offer. For each creative, the following are returned: </li>
        <ul>
        <li><strong>Id</strong>: [<em>string</em>] the unique id of the creative</li>
        <li><strong>previewUrl</strong>: [<em>string</em>] the url where you can preview the creative</li>
        <li><strong>mimeType</strong>: [<em>string</em>] the mime type of the creative</li>
        <li><strong>dimensions</strong>: [<em>string</em>] the dimensions of the creative</li>
        <li><strong>locale</strong>: [<em>string</em>] the locales supported by the creative </li>
        </ul>
    <li><strong>acquisitionModel</strong>: [<em>string</em>] the name of the acquisition model</li>
    <li><strong>acquisitionModelDescription</strong>: [<em>string</em>] the description of the acquisition model </li>
    <li><strong>qualityScore</strong>: [nullable <em>double</em>] An index indicative of the reliability of the offer (the higher the better), which is calculated based on a proprietary ranking algorithm developed by the Minimob development team </li>
    <li><strong>qualityScorePerCountry</strong>: Contains the quality score per country. For each country of the offer, the following are returned: </li>
        <ul>
        <li><strong>countryCode</strong>: [<em>string</em>] the country code</li>
        <li><strong>qualityScore</strong>: [nullable <em>double</em>] <strong>calculated as the overall qualityscore index, but on a country-level</strong> </li>
        </ul>
</ul>
<h6>Example</h6>
   <p>An example of the response is given below:</p>
<pre class="prettyprint linenums">
<code>{
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
	"appPreviewLink": "https://play.google.com/store/apps/details?hl=en&amp;id=com.minimob.app",
	"expirationDate": "12/31/2018 10:00:00 PM",
	"incentivized": "NonIncentivized",
	"storeName": "Google Play",
	"objectiveUrl": "http://clicks.minimob.com/tracking/click?clickid=[[clickid]]&amp;trafficsource=1373664459&amp;cid=[[cid]]&amp;offerid=151494",
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
}</code>
</pre>
</div>
<div id="D-approval-request-api10">
<h4>Approval Request</h4>
   <p>In order to gain access to a Minimob offer a user has to make an approval request which needs to be accepted by a Minimob account manager.</p>
   <p><em>Url:</em> <a href="http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key" target="_blank">http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key</a></p>
   <p><em>HTTP method:</em> POST</p>
   <p><em>Request Header:</em> Content-Type:application/json</p>
   <p><em>Request Body:</em> json array of strings where each string is an available offer id. Example: ["00000000000000","00000000000001"]</p>
   <p><em>Returns:</em> json array of objects</p>
<h6>Example</h6>
   <p>Assuming that you have you have made the following request for the specific offer ids:</p>
<pre class="prettyprint linenums">
<code>["00000000000000","00000000000001"]</code>
</pre>
   <p>You would get the following response:</p>
<pre class="prettyprint linenums">
<code>[
	"00000000000000",
	"00000000000001"
]</code>
</pre>
</div></div>
<div id="D-api11">
<h3>API 1.1</h3>
   <p>Version 1.1 of the API allows access to the following Minimob resources:</p>
<ul>
    <li><strong>available offers</strong>: all offers that are available to you and you can by requesting approval have access to use them</li>
    <li><strong>available offer details</strong>: detailed information for a particular offer</li>
    <li><strong>my offers</strong>: detailed information for each and every offer that you have been given approval to promote</li>
    <li><strong>approval request</strong>: for gaining access you must send an approval request for a particular offer</li>
</ul>
<div id="D-all-offers-api11">
<h4>Available Offers</h4>
   <p>This API Call returns summarized information about all the offers that are available in Minimob.</p>
   <p><em>Url:</em> <a href="http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key" target="_blank">http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key</a></p>
   <p><em>HTTP method:</em> GET</p>
   <p><em>Returns:</em> json array of objects [{},{}….{}]</p>
   <p>Each JSON object contains the following properties:</p>
<ul>
    <li><strong>id</strong>: [<em>string</em>] the offer's id that is unique across the Minimob platform</li>
    <li><strong>name</strong>: [<em>string</em>] the name of the offer</li>
    <li><strong>targetedCountries</strong>: [<em>string</em>] the list of countries in which the offer can be served (country codes as per <a href="https://www.iso.org/obp/ui/#search" target="_blank">ISO 3166-1 alpha-2</a>)</li>
    <li><strong>payout</strong>: [<em>double</em>] the monetary compensation per each goal achieved as defined by the payout model</li>
    <li><strong>payoutCurrency</strong>: [<em>string</em>] the currency of the payout (currency codes as per <a href="http://www.iso.org/iso/currency_codes" target="_blank">ISO 4217</a>)</li>
    <li><strong>payoutModel</strong>: [<em>string</em>] the model on which the payout is based (currently CPI only is supported)</li>
    <li><strong>targetPlatform</strong>: [<em>string</em>] the mobile operating system that is targeted </li>
    <li><strong>overallConversionCap</strong>: [nullable <em>int</em>] the conversion cap for the entire lifetime of the offer</li>
    <li><strong>dailyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per day</li>
    <li><strong>weeklyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per week</li>
    <li><strong>monthlyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per month</li>
    <li><strong>status</strong>: [<em>enum</em>] indicates the status of the offer. It can have one of the following values:</li>
        <ul>
        <li>0: The offer is <em>Available</em> for you to request it</li>
        <li>1: Your request for this offer is <em>Pending</em> </li>
        </ul>
    <li><strong>incentivized</strong>: indicates whether the offer is allowed to run on incentivized traffic or not. It can have one of the following values:</li>
        <ul>
        <li>0: Both Incentivized traffic and Non-Incentivized traffic are allowed</li>
        <li>1: Incentivized traffic only</li>
        <li>2: Non-Incentivized traffic only</li>
        <li>3: Uncertain (the offer is allowed to run on both Incentivized traffic and Non-Incentivized traffic)</li>
        </ul>
    <li><strong>incentivizedDescription</strong>: [<em>string</em>] a textual description regarding whether the offer is <em>Incentivized</em> </li>
    <li><strong>storeId</strong>: [<em>string</em>] indicates the store through which the application is distributed. It can have one of the following values:</li>
        <ul>
        <li>1: corresponds to <em>Google Play</em> </li>
        <li>2: corresponds to <em>Apple iTunes</em> </li>
        <li>3: corresponds to <em>Minimob Store</em> </li>
        </ul>
    <li><strong>storeName</strong>: [<em>string</em>] the name of the store through which the application is distributed </li>
</ul>
<h6>Example</h6>
   <p>An example of the response is given below:</p>
<pre class="prettyprint linenums">
<code>[
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
]</code>
</pre>
</div>
<div id="D-offer-details-api11">
<h4>Available Offer Details</h4>
   <p>This API Call returns the full details of an offer that is available for you to request it.</p>
   <p>In addition to the <strong>apikey</strong>, you need to include the <strong>id</strong> of the offer to the url.</p>
   <p><em>Url:</em> <a href="http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key&id=an_available_offer_id" target="_blank">http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key&amp;id=an_available_offer_id</a></p>
   <p><em>HTTP method:</em> GET</p>
   <p><em>Returns:</em> json object</p>
   <p>The JSON object contains the following properties:</p>
<ul>
    <li><strong>id</strong>: [<em>string</em>] the offer's id that is unique across the Minimob platform</li>
    <li><strong>name</strong>: [<em>string</em>] the name of the offer</li>
    <li><strong>targetedCountries</strong>: [<em>string</em>] the list of countries in which the offer can be served (country codes as per <a href="https://www.iso.org/obp/ui/#search" target="_blank">ISO 3166-1 alpha-2</a>)</li>
    <li><strong>payout</strong>: [<em>double</em>] the monetary compensation per each goal achieved as defined by the payout model</li>
    <li><strong>payoutCurrency</strong>: [<em>string</em>] the currency of the payout (currency codes as per <a href="http://www.iso.org/iso/currency_codes" target="_blank">ISO 4217</a>)</li>
    <li><strong>payoutModel</strong>: [<em>string</em>] the model on which the payout is based (currently CPI only is supported)</li>
    <li><strong>targetPlatform</strong>: [<em>string</em>] the mobile operating system that is targeted </li>
    <li><strong>description</strong>: [<em>string</em>] A detailed description of the offer </li>
    <li><strong>overallConversionCap</strong>: [nullable <em>int</em>] the conversion cap for the entire lifetime of the offer</li>
    <li><strong>dailyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per day</li>
    <li><strong>weeklyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per week</li>
    <li><strong>monthlyConversionCap</strong>: [nullable <em>int</em>] the conversion cap per month</li>
    <li><strong>appIconLink</strong>: [<em>string</em>] a url which points to the icon of the application through which the offer is promoted</li>
    <li><strong>appTitle</strong>: [<em>string</em>] the title of the application </li>
    <li><strong>appId</strong>: [<em>string</em>] the application ID (as registered to the app store)</li>
    <li><strong>appDescription</strong>: [<em>string</em>] A detailed description of the application</li>
    <li><strong>appPreviewLink</strong>: [<em>string</em>] A link directing to the application page in the app store</li>
    <li><strong>expirationDate</strong>: [<em>string</em>] Specifies the date until which the offer can be promoted</li>
    <li><strong>incentivized</strong>: indicates whether the offer is allowed to run on incentivized traffic or not. It can have one of the following values:</li>
        <ul>
        <li>0: Both Incentivized traffic and Non-Incentivized traffic are allowed</li>
        <li>1: Incentivized traffic only</li>
        <li>2: Non-Incentivized traffic only</li>
        <li>3: Uncertain (the offer is allowed to run on both Incentivized traffic and Non-Incentivized traffic)</li>
        </ul>
    <li><strong>incentivizedDescription</strong>: [<em>string</em>] a textual description regarding whether the offer is <em>Incentivized</em> </li>
    <li><strong>storeId</strong>: [<em>string</em>] indicates the store through which the application is distributed. It can have one of the following values:</li>
        <ul>
        <li>1: corresponds to <em>Google Play</em> </li>
        <li>2: corresponds to <em>Apple iTunes</em> </li>
        <li>3: corresponds to <em>Minimob Store</em> </li>
        </ul>
    <li><strong>storeName</strong>: [<em>string</em>] the name of the store through which the application is distributed </li>
    <li><strong>creatives</strong>: Contains the creatives that are associated with the offer. For each creative, the following are returned: </li>
        <ul>
        <li><strong>Id</strong>: [<em>string</em>] the unique id of the creative</li>
        <li><strong>previewUrl</strong>: [<em>string</em>] the url where you can preview the creative</li>
        <li><strong>mimeType</strong>: [<em>string</em>] the mime type of the creative</li>
        <li><strong>dimensions</strong>: [<em>string</em>] the dimensions of the creative</li>
        <li><strong>locale</strong>: [<em>string</em>] the locales supported by the creative [Feature to be supported in a future release]</li>
        </ul>
</ul>
<h6>Example</h6>
   <p>An example of the response is given below:</p>
<pre class="prettyprint linenums">
<code>{
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
	"appPreviewLink": "https://play.google.com/store/apps/details?hl=en&amp;id=com.minimob.app",
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
}</code>
</pre>
</div>
<div id="D-my-offers-api11">
<h4>My Offers</h4>
   <p>This API Call returns the details of each and every offer that you have been approved to promote.</p>
   <p>The results are returned in one or more pages, each one carrying a maximum of 200 offers. Each page returned contains a URL pointing to the next set of offers, assuming that there are more offers remaining to be fetched. Note that the actual number of offers that are eventually included in a page may be less than the maximum, because changes to the status of some offers may occur from the time that the API call was made until the relevant page is fetched.</p>
   <p>For example, if you have been given approval for 430 offers, the results returned for this API call would be organized in three pages; the first and the second would each contain a maximum of 200 offers while the third page would contain 30 offers. Upon making the request, you will get the first page with information about the first 200 offers, together with the URL where you can fetch the second page. Assuming that until you fetch the second page one the offers of the second page has been paused, the second page will eventually return information for 199 offers. The third page will return information for the last 30 offers (assuming that none of them has been paused in the meantime) and a null-valued URL for the next page to fetch, which is the signal that the request returned the final and last page of the results.</p>
<blockquote><strong>Note</strong>: In order to better serve requests for this API call, the same user is not allowed to make more than one request per second (otherwise Error 409 is returned).</blockquote>
   <p><em>URL:</em> <a href="http://dashboard.minimob.com/api/v1.1/myoffers/?apikey=your_api_key" target="_blank">http://dashboard.minimob.com/api/v1.1/myoffers/?apikey=your_api_key</a></p>
   <p><em>HTTP method:</em> GET</p>
   <p><em>Returns:</em> JSON object</p>
   <p>The JSON object contains the following properties:</p>
<ul>
    <li><b>pageCount</b>: [<i>long</i>] the total number of pages that comprise the response to the call</li>
    <li><b>pageSize</b>: [<i>long</i>] the maximum number of offers that can be included at the specific page </li>
    <li><b>nextpageUrl</b>: [<i>string</i>] the URL of the page that contains the next set of offers, if more results exist; otherwise it is null.</li>
    <li><b>Offers</b> </li>
</ul>
   <p>Within the <b>Offers</b> part of the response, the following are included:</p>
<ul>
    <li><strong>id</strong>: [<em>string</em>] the offer's id that is unique across the Minimob platform</li>
    <li><strong>name</strong>: [<em>string</em>] the name of the offer</li>
    <li><strong>payoutModel</strong>: [<em>string</em>] the model on which the payout is based (currently CPI only is supported)</li>
    <li><strong>payout</strong>: [<em>double</em>] the monetary compensation per each goal achieved as defined by the payout model</li>
    <li><strong>payoutCurrency</strong>: [<em>string</em>] the currency of the payout (currency codes as per <a href="http://www.iso.org/iso/currency_codes" target="_blank">ISO 4217</a>)</li>
    <li><strong>targetedCountries</strong>: Contains the countries in which the offer can be served </li>
        <ul>
        <li><strong>countryCode</strong>: [<em>string</em>] the 2-letter country code (as per <a href="https://www.iso.org/obp/ui/#search" target="_blank">ISO 3166-1 alpha-2</a>)</li>
        <li><strong>runningStatus</strong>: [<em>string</em>] the status of the offer for the specific country, either <i>Running</i> or <i>Paused</i> </li>
        <li><strong>reactivationEstimatedTime</strong>: [<i>DateTime</i>] <i>null</i>, if <b>runningStatus</b> is <i>Running</i>; otherwise, it holds the date and time (UTC) when the status of the offer for the specific country is expected to switch back to <i>Running</i> </li>
        </ul>
    <li><strong>targetPlatform</strong>: [<em>string</em>] the mobile operating system that is targeted, currently one of: <em>Android</em>, <em>iOS</em> </li>
    <li><strong>description</strong>: [<em>string</em>] A detailed description of the offer </li>
    <li><strong>overallConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the expiration of the offer </li>
    <li><strong>dailyConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the end of the current day </li>
    <li><strong>weeklyConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the end of the current week </li>
    <li><strong>monthlyConversionCap</strong>: [nullable <em>int</em>] the remaining conversion cap until the end of the current month </li>
    <li><strong>appIconLink</strong>: [<em>string</em>] a URL which points to the icon of the application through which the offer is promoted</li>
    <li><strong>appTitle</strong>: [<em>string</em>] the title of the application </li>
    <li><strong>appId</strong>: [<em>string</em>] the application ID (as registered to the app store)</li>
    <li><strong>appDescription</strong>: [<em>string</em>] A detailed description of the application</li>
    <li><strong>appPreviewLink</strong>: [<em>string</em>] A link directing to the application page in the app store</li>
    <li><strong>expirationDate</strong>: [<em>string</em>] Specifies the date until which the offer can be promoted</li>
    <li><strong>incentivized</strong>: [<em>string</em>] a textual description regarding whether the offer is <em>Incentivized</em>, its value can be one of: <em>BothIncentivizedAndNot</em>, <em>Incentivized</em>, <em>NonIncentivized</em>, <em>Uncertain</em> </li>
    <li><strong>storeName</strong>: [<em>string</em>] the name of the store through which the application is distributed </li>
    <li><strong>runningStatus</strong>: [<em>string</em>] the status of the offer, either <i>Running</i> or <i>Paused</i> (this status refers to the overall status of the offer, i.e. applying to all of the countries of the offer)</li>
    <li><strong>reactivationEstimatedTime</strong>: [<i>DateTime</i>] it is <i>null</i> unless the offer is temporarily paused, in which case it holds the date and time (UTC) when the status of the offer is expected to switch back to <i>Running</i> </li>
    <li><strong>objectiveUrl</strong>: [<em>string</em>] the link for redirecting the end user to the app store for downloading the app, as well as for notifying Minimob when a user clicks on the offer. The format of the URL can be customized through the UI of the Minimob application, but, in general, it consists of the following:</li>
        <ul>
        <li><strong>clicks.minimob.com/tracking/click?</strong> : the tracking URL</li>
        <li><strong>clickid</strong>: a parameter for holding the click id that corresponds to a user (its value can be customized)</li>
        <li><strong>trafficsource</strong>: the unique id which has been assigned by the system to your traffic source</li>
        <li><strong>offerid</strong>: a unique id that identifies the particular campaign through which the offer is being promoted</li>
        <li>custom parameters: any additional parameters that you may have defined when configuring (though the UI) the format of the click URL</li>
        </ul>
    <li><strong>creatives</strong>: Contains the creatives that are associated with the offer. For each creative, the following are returned: </li>
        <ul>
        <li><strong>Id</strong>: [<em>string</em>] the unique id of the creative</li>
        <li><strong>previewUrl</strong>: [<em>string</em>] the URL where you can preview the creative</li>
        <li><strong>mimeType</strong>: [<em>string</em>] the mime type of the creative</li>
        <li><strong>dimensions</strong>: [<em>string</em>] the dimensions of the creative</li>
        <li><strong>locale</strong>: [<em>string</em>] the locales supported by the creative </li>
        </ul>
    <li><strong>acquisitionModel</strong>: [<em>string</em>] the name of the acquisition model</li>
    <li><strong>acquisitionModelDescription</strong>: [<em>string</em>] the description of the acquisition model </li>
    <li><strong>qualityScore</strong>: [nullable <em>double</em>] An index indicative of the reliability of the offer (the higher the better), which is calculated based on a proprietary ranking algorithm developed by the Minimob development team. This property is an indicative estimation and should not be taken as a recommendation.</li>
    <li><strong>qualityScorePerCountry</strong>: Contains the quality score per country. For each country of the offer, the following are returned: </li>
        <ul>
        <li><strong>countryCode</strong>: [<em>string</em>] the 2-letter country code</li>
        <li><strong>qualityScore</strong>: [nullable <em>double</em>] <strong>calculated as the overall qualityscore index, but on a country-level</strong></li>
        </ul>
</ul>
<h6>Notes about Pausing of Offers</h6>
   <p>There are certain circumstances and conditions where an offer may be paused. Pausing of an offer can apply:</p>
<ul>
    <li>Generally to all the countries of the offer </li>
    <li>To specific countries of the offer</li>
</ul>
   <p>For describing the status of the offer, the <strong>runningStatus</strong> and <b>reactivationEstimatedTime</b> parameters are used, both at the offer level (i.e. across all countries) and at the country level (i.e. for each country individually). In order for an offer to run in a country, <strong>runningStatus</strong> needs to have the value <i>Running</i> both at the offer level and at the country level (for the specific country).</p>
   <p>General pausing of an offer occurs when either one of the daily, weekly, monthly or total cap of the offer has been reached. In this case, the offer’s overall <b>runningStatus</b> (i.e. applying to all the countries of the offer) is set to <i>Paused</i>. If the total cap has been reached, then the offer is permanently paused. If either one of the daily, weekly or monthly cap has been reached, the offer is temporarily paused and the parameter <b>reactivationEstimatedTime</b> holds the date and time (UTC) when the status of the offer is expected to switch back to <i>Running</i>. If the:</p>
<ul>
    <li>Daily cap has been reached, <b>reactivationEstimatedTime</b> returns the date and time (UTC) of the start of the next day.</li>
    <li>Weekly cap has been reached, <b>reactivationEstimatedTime</b> returns the date and time (UTC) of the start of the next Monday.</li>
    <li>Monthly cap has been reached, <b>reactivationEstimatedTime</b> returns the date and time (UTC) of the start of next month.</li>
    <li>Overall cap has been reached, <b>reactivationEstimatedTime</b> returns null.</li>
</ul>
   <p>Pausing of an offer for a specific country is directly related to the quality level of the offer for that country. Minimob periodically checks the quality of the offer for each country that the offer is allowed to run. If the quality for a country does not meet the desired standards, the offer is temporarily paused for that country. In this case, the offer’s <b>runningStatus</b> for that particular country is automatically set to <i>Paused</i> while the parameter (at country level) <b>reactivationEstimatedTime</b> holds the date and time (UTC) when the status of the offer is expected to switch back to <i>Running</i>. The quality detection and control mechanism is entirely programmatic and automated so the estimated date and time is only indicative and it may be changing frequently, while the status of the offer may change to <i>Running</i> before the estimated date and time.</p>
   <p>As a publisher, you are strongly advised to respect a campaign which is paused for one or more specific targeted countries, and temporarily suspend it accordingly from your network of traffic sources. In this way you can optimize the performance of your traffic.</p>
<h6>Example</h6>
   <p>An example of the response is given below:</p>
<pre class="prettyprint linenums">
<code>{
"pageCount":5,
"pageSize":200,
"nextPageUrl":"http://dashboard.minimob.com/api/v1.1/myoffers?apikey= F_A_K_E_-fe05-11e4-adc5-2cc58487f907&amp;page=1",
"offers":[&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{"id":"12345678901234",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name":"minimob app offer ONE",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"payoutModel":"CPI",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"payout":0.114,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"payoutCurrency":"USD",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"targetedCountries":[
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"countryCode":"CY","runningStatus":"Running","reactivationEstimatedTime":null},
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"countryCode":"GR","runningStatus":"Running","reactivationEstimatedTime":null}
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;],
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"targetPlatform":"Android",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"description":"A description of the offer ONE",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"overallConversionCap":null,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"dailyConversionCap":75,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"weeklyConversionCap":null,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"monthlyConversionCap":null,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appIconLink":"https://lh3.googleusercontent.com/F_A_K_E-ISG9UVy0EKYq9Ikon2dKS-0uXwtdldpe8LR39J7QVbRtVry5-KCQ7M4Ao1FP=w300",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appTitle":"app ALPHA",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appId":"com.myapp.alpha",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appDescription":null,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appPreviewLink":"https://play.google.com/store/apps/details?hl=en&amp;id=com.myapp.alpha",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"expirationDate":"",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"incentivized":"NonIncentivized",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"storeName":"Google Play",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"runningStatus":"Running",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"reactivationEstimatedTime":null,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"objectiveUrl":"http://clicks.minimob.com/tracking/click?clickid=[[clickid]]&amp;trafficsource=1373664459&amp;cid=[[cid]]&amp;offerid=151494",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"creatives":[
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"Id":"561ce92dc7820c12e4654503","previewUrl":"http://cdn.minimob.com/creative/F_A_K_E_-c48c-4758-805a-ab9b2c690199.png","mimeType":"image/png","dimensions":"300x300","locale":""}
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;],
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"acquisitionModel":"CPI",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"acquisitionModelDescription":"USER FLOW:\n1) User clicks on creative and is forwarded to Apple / Google Play Store\n2) User downloads the App on the phone\n3) User opens the App after download",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"qualityScore":10.874485393191936,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"qualityScorePerCountry":[
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"countryCode":"CY","qualityScore":5.4986516592362022},
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"countryCode":"GR","qualityScore":5.3820509956498066},
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"countryCode":"US","qualityScore":0.0}
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]
&nbsp;&nbsp;&nbsp;&nbsp;},
&nbsp;&nbsp;&nbsp;&nbsp;{"id":"12345678901235",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name":"minimob app offer TWO",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"payoutModel":"CPI",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"payout":0.73,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"payoutCurrency":"USD",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"targetedCountries":[
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"countryCode":"BR","runningStatus":"Running","reactivationEstimatedTime":null}
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;],
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"targetPlatform":"iOS",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"description":"A description of the offer TWO",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"overallConversionCap":null,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"dailyConversionCap":0,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"weeklyConversionCap":null,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"monthlyConversionCap":null,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appIconLink":"http://a5.mzstatic.com/us/r30/Purple6/v4/19/ec/33/F_A_K_E_-4ae8-3445-c9f1-e1104c2c1965/icon350x350.jpeg",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appTitle":"app BETA",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appId":"id123456789",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appDescription":null,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appPreviewLink":"https://itunes.apple.com/gb/app/id123456789",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"expirationDate":"",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"incentivized":"NonIncentivized",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"storeName":"Apple iTunes",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"runningStatus":"Paused",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"reactivationEstimatedTime":"2015-10-28T00:00:00Z",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"objectiveUrl":"http://clicks.minimob.com/tracking/click?clickid=[[clickid]]&amp;trafficsource=1373664459&amp;cid=[[cid]]&amp;offerid=151495",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"creatives":[
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"Id":"556ebebf38866608b8789a11","previewUrl":"http://cdn.minimob.com/creative/F_A_K_E_-1e11-42ce-b0a5-de238321faf7.png","mimeType":"image/png","dimensions":"300x300","locale":""},
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"Id":"55d0e5f9c7820c2ab4b6e6df","previewUrl":"http://cdn.minimob.com/creative/F_A_K_E_-edda-4c06-8829-1d24f0b3e9ba.png","mimeType":"image/png","dimensions":"960x640","locale":""}
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;],
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"acquisitionModel":"CPI",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"acquisitionModelDescription":"USER FLOW:\n\n1) User clicks on creative and is forwarded to Apple / Google Play Store\n2) User downloads the App on the phone\n3) User opens the App after download",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"qualityScore":22.112443333692923,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"qualityScorePerCountry":[
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{"countryCode":"BR","qualityScore":22.112443333692923}
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]
&nbsp;&nbsp;&nbsp;&nbsp;}
]}</code>
</pre>
</div>
<div id="D-approval-request-api11">
<h4>Approval Request</h4>
   <p>In order to gain access to a Minimob offer a user has to make an approval request which needs to be accepted by a Minimob account manager.</p>
   <p><em>Url:</em> <a href="http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key" target="_blank">http://dashboard.minimob.com/api/availableoffers/?apikey=your_api_key</a></p>
   <p><em>HTTP method:</em> POST</p>
   <p><em>Request Header:</em> Content-Type:application/json</p>
   <p><em>Request Body:</em> json array of strings where each string is an available offer id. Example: ["00000000000000","00000000000001"]</p>
   <p><em>Returns:</em> json array of objects</p>
<h6>Example</h6>
   <p>Assuming that you have you have made the following request for the specific offer ids:</p>
<pre class="prettyprint linenums">
<code>["00000000000000","00000000000001"]</code>
</pre>
   <p>You would get the following response:</p>
<pre class="prettyprint linenums">
<code>[
	"00000000000000",
	"00000000000001"
]</code>
</pre>
</div></div>
</div>
