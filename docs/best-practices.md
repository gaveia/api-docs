# Best Practices for Integration
To optimize traffic and performance, we recommend the following practices when working with accommodation data and images:

- Store accommodation data locally (except for availability and pricing data) to reduce server traffic.
- Download images locally to minimize unnecessary requests to our server.

## API Usage Overview
### Retrieve a List of Accommodation Units
[Swagger documentation](https://propertyhub.gaveia.com/partner-api/index.html#/default/get_accommodations_list)<br>
To get a list of campsites and accommodation units, use the accommodations/list endpoint.

### Retrieve Specific Camp Data
For details for a specific campsite, use the /camp/data endpoint. In the URL, provide the language and ID parameters. Supported languages are: _"en", "de", "it", "nl", "hr"_.

### Retrieve Data for Individual Accommodation Units
The data for individual accommodation units varies by unit type.<br>
For mobile home use: [Mobile homes endpoint](https://propertyhub.gaveia.com/partner-api/index.html#/default/post_accommodation_mobile_home)<br>
For pitch use: [Pitch endpoint](https://propertyhub.gaveia.com/partner-api/index.html#/default/post_accommodation_pitch)<br>
For glamping use: [Glampings endpoint](https://propertyhub.gaveia.com/partner-api/index.html#/default/post_accommodation_glamping)<br>
For apartment use: [Apartments endpoint](https://propertyhub.gaveia.com/partner-api/index.html#/default/post_accommodation_apartment)<br>


### Availability Search
We have two main endpoints for checking availability:

#### General Availability Search
[Swagger documentation](https://propertyhub.gaveia.com/partner-api/index.html#/default/post_accommodations_search)<br>
This endpoint is used when you need to check the availability for multiple accommodation units at once. It is allowed to call it for each unique availability search.

#### Single Accommodation Availability
[Swagger documentation](https://propertyhub.gaveia.com/partner-api/index.html#/default/post_accommodation_availability)<br>
To get the most up-to-date availability and pricing for a single accommodation unit, use this endpoint. It's essential for when entering the booking process, as it provides real-time data.

#### Accommodation Unit Calendar
[Swagger documentation](https://propertyhub.gaveia.com/partner-api/index.html#/default/post_accommodation_get_calendar)<br>
The calendar request can be used to retrieve the daily prices for a specific accommodation unit. The response will only include the available days. This data can also be downloaded locally, and the total price calculation can be performed on your side.<br>
**Notes:** _The obtained price is in some cases the base price, without including additional charges, and the total prices may not match the prices obtained through the real-time availability check request, on which the reservation must be based._<br>
**Note:** _If you choose to collect and display prices in this way, you must somehow present to guests that this is the base price, as we are unable to provide the additional charges that are added._

### Booking
You will receive more details on how to make a reservation in the sections below of the documentation.

