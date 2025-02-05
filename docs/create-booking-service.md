# Create Booking Service
[Swagger documentation](https://propertyhub.gaveia.com/partner-api/index.html#/default/post_booking_create)<br>
Create a new booking by posting booking data to “/booking/create” endpoint. The "bookingId" is returned.

## Description
How to fill the booking data depends on the selected payment method. The allowed payment methods are defined at the price list level and are retrieved from the response of the "/accommodation/availability" service. Below is a short description of each payment method.

### No Guarantee payment method ("no_guarantee")
The reservation will be created in the system, no deposit or credit card guarantee required.

### Bank Transfer payment method ("bank_transfer")
The reservation will be created in the system, and the guest is required to make the payment via bank transfer within the due defined in the booking conditions.

### Credit Card VPP payment method ("credit_card_vpp")
With this payment method, the payment is processed on our side. We use an external payment gateway to which the user needs to be redirected to complete the payment. Upon successful payment, the user will be redirected to the reservation confirmation page; otherwise, they will be redirected to an error page.

The /booking/create service response will return a "redirectUrl" string, which should be used to redirect the user for payment completion.

The required parameters for this payment method are the redirect URLs, which determine where the user will be redirected based on the payment outcome:
<br>
```    
"paymentMethod": "credit_card_vpp",
"redirectUrl": "https://example.com/booking-confirmation",
"cancelPaymentRedirectUrl": "https://example.com/booking-failed",
```  
**Note:** _This request should not include credit card details, nor should they be collected on the client side._

### Credit Card OTA payment method ("credit_card")
In this payment method, the data is collected on the client side, and valid data must be sent through the booking data in the request. Attention should be paid to the allowed card types.

The required fields are:
<br>
```  
"paymentMethod": "credit_card",
"creditCardFirstName": "John",
"creditCardLastName": "Doe",
"creditCardType": "VISA",
"creditCardNo": "4111111111111111",
"creditCardVerificationCode": "123",
"creditCardValidThroughMonth": "08",
"creditCardValidThroughYear": 2025,
```
**Note:** _Partners connecting to our API will not need to use this payment method because they can only access properties that are in the VPP type of partnership._

## Examples
**Note:** _For testing, set the parameter "test" to true._

### Credit Card OTA
Request:
<br>
```
{
  "accommodationReference": "61238f3b1b82b658ac5919f1",
  "priceListReference": "669710af5af7adef1b06b3dc",
  "language": "en",
  "arrival": "20250606",
  "departure": "20250613",
  "adults": 2,
  "children": 1,
  "childrenAges": [
    {
      "age": 2
    }
  ],
  "pets": 0,
  "clientFirstName": "John",
  "clientLastName": "Doe",
  "clientEmail": "john-doe@gmail.com",
  "clientPhone": "355152255",
  "clientCountry": "Croatia",
  "clientCountryCode": "HR",
  "paymentMethod": "credit_card",
  "vehicleType": "",
  "vehicleLength": "",
  "comment": "Test reservation",
  "guests": [],
  "services": [],
  "creditCardFirstName": "John",
  "creditCardLastName": "Doe",
  "creditCardType": "VISA",
  "creditCardNo": "4111111111111111",
  "creditCardVerificationCode": "123",
  "creditCardValidThroughMonth": "08",
  "creditCardValidThroughYear": 2027,
  "propertyDamageInsurance": false,
  "test": true
}
```
Response:
<br>
```
{
  "success": true,
  "bookingId": "67a210aff33f7280ba0fa0f3"
}
```
### Credit Card VPP
Request:
<br>
```
{
  "accommodationReference": "6123919c1b82b658ac67a317",
  "priceListReference": "66ed516f72169adcf503d85e",
  "language": "en",
  "arrival": "20250606",
  "departure": "20250613",
  "adults": 2,
  "children": 1,
  "childrenAges": [
    {
      "age": 2
    }
  ],
  "pets": 0,
  "clientFirstName": "John",
  "clientLastName": "Doe",
  "clientEmail": "john-doe@gmail.com",
  "clientPhone": "355152255",
  "clientCountry": "Croatia",
  "clientCountryCode": "HR",
  "paymentMethod": "credit_card_vpp",
  "vehicleType": "",
  "vehicleLength": "",
  "comment": "Test reservation",
  "guests": [],
  "services": [],
  "propertyDamageInsurance": false,
  "test": true,
"redirectUrl": "https://example.com/booking-confirmation",
"cancelPaymentRedirectUrl": "https://example.com/booking-failed"
}
```
Response:
<br>
```
{
  "success": true,
  "bookingId": "67a2130b2725ccf0d40e2ac3",
  "redirectUrl": "http://propertyhub.local/front/payment/?id=67a2130b2725ccf0d40e2ac3&apiSourceName=test1"
}
```
