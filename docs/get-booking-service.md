# Get Booking Service
[Swagger documentation](https://propertyhub.gaveia.com/partner-api/index.html#/default/get_booking_get__bookingReference_)<br>
Retrieve the status of an existing booking by making a GET request to the `/booking/get` endpoint, using the "bookingId" returned from the `/booking/create` endpoint.

## Description
This service allows you to retrieve the current status of a booking. The booking information will be returned along with details like the payment method, booking dates, client information, and more.

To query the booking details, provide the `bookingId` that was generated during the booking creation process.

### Notes
- **Booking Status**: The status of the booking can be "RESERVATION", "ON HOLD", "Waiting/Failed payment", "FAILED" or "CANCELLED".