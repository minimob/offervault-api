# Getting started with minimob offervault api

## Prerequisites 
For having access to offervault api you must have a valid minimob account. Each minimob account is uniquely associated with a randomly generated api key. All request require the paramter api key in order to identify and authorize your request.

## Introduction
minimob offervault api allows access to the following resources and actions of minimob offervault service
* available offers: all offers that are available to you and you can by requesting approval have access to use them
* available offer details: detailed information for a perticular offer
* my offers: all offers that you have access to use 
* my offer details: detailed information for a particular offer that you allowed to use
* approval request: for gaining access you must send an aproval request for a particular offer

>minimob offervault api is NOT an adserving api. It's one and only purpose is to help you to implement automated offer importing in your system and not for direct ad serving, by using the technology platform you might suite best for your case.

Tha API is based on HTTP protocol and all data interchanged are in JSON format.

## API documentation
### My Offers
>This API Call returns all your offers in a condensed format

*Url:* <http://dashboard.minimob.com/api/myoffers/?apikey=your_api_key>  
*HTTP method:* GET  
*Returns:* json array of objects  
