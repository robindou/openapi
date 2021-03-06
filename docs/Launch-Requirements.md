<a name="Launch-Requirements"></a>

Launch requirements help check whether you are ready to serve your clients and provide a satisfactory service. Our launch requirements set the standards you must meet before we finally authorize your web portals, applications or offline tools to go live and sell our inventories.

When you finish the integration, you must request a site review to our tech team. Our tech support team will contact you directly for site review and offer any necessary assistance. Note that you might be required go back and implement or optimize certain launch requirements when they don't meet our standards. To minimize even avoid this possibility, we strongly recommend you to follow each appropriate requirement during your integration.

### 1. General requirements

#### 1.1 Authentication stage
Make sure `Refresh Access Token` API has been properly used. Sometimes partners often skip this API for convenience purpose and directly use ‘Initialize Access Token’ API for generating and updating access tokens. This is not recommened at all since frequent expose of your API key will bring more potential of leakage of the key.

#### 1.2 Adopt https protocol
Make sure you have adopted https protocol when requesting our proxy service either for initializing access token, updaing access token or accessing other backend service APIs.

#### 1.3 Make sure you won't use the same UUID to request the same API
For each request hitting the same backend API, we need you pass to us a unique UUID. This UUID works as the logid which we use to trace your request log of the API at this time. So don't use the same UUID to request the same backend API at any time. However, you could use the same UUID to request a different backend API since we could still identify it with logid and API name. This rule must be strictly followed!  

**Code sample**
```json
// UUID used to request the same API couldn't be repeated. They must be different.

https://BaseURL?AID=1&SID=1&ICODE=12345&UUID=aadd-edfr-ctr3-45gh&Token=cd88ertfer674&mode=1&format=json

https://BaseURL?AID=1&SID=1&ICODE=12345&UUID=ccbb-nmhg-35rf-89jy&Token=cd88ertfer674&mode=1&format=json
```

#### 1.4 Make sure you have requested us with correct user basic info
In certain APIs, we will require you pass to us basic user info. These basic info are represented in object `IntlUserProperties` crossing different API requests. If you don't pass to us when we need them, we won't respond you geo rates and possible member rates.  

**Code sample**

```json

"IntlUserProperties": {
    "Locale": "en_US",
    "Platform": "online",
    "UserLevel": 0,
    "CrossUser": "true",
    "CountryCode": "UK"

}
```

### 2. Hotel page

#### 2.1 List policies on hotel page
Display hotel policies properly on hotel page. Policies such as check-in & check-out, children occupancy & extra bed, extra meal and pet policy must be displayed clearly. You could get these policies from `Get Hotel Static Info` API.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-hotelpolicy.png)

**Code Sample**
```json
// Check-in & check-out policy:
"ArrivalTimeLimitInfo":{"EarliestTime":"string","LatestTime":"string","IsMustBe":"T"},"DepartureTimeLimitInfo":{"EarliestTime":"string","LatestTime":"string"},

// Children & extra bed policy:
"ChildAndExtraBedPolicy":{"ExistingBed":{"LimitInfo":[{"Type":"Age","Min":"string","Max":"string"}],"Fees":[{"RangeLimit":[{"Type":"string","Start":"string","End":"string"}],"Amount":[{"Type":"string","Amount":0,"Currency":"string"}],"Percent":{"Percent":0},"MealInfo":{"BreakfastType":0},"Occupancy":0,"ChargeUnit":"PerPerson","ChargeFrequency":"Daily","IsFree":true}],"MaxOccupancy":0},"ExtraBed":{"Fees":[{"RangeLimit":[{"Type":"Age","Start":"string","End":"string"}],"Amount":[{"Type":"string","Amount":0,"Currency":"string"}],"Percent":{"Percent":0},"MealInfo":{"BreakfastType":0},"Category":2,"BedType":1,"ChargeUnit":"PerPerson","ChargeFrequency":"Daily","IsFree":true}],"MaxQuantity":0,"ExtraBedType":1,"ExtraBedType1":"string","MaxCribQuantity":0},"Descriptions":[{"Text":"string","Category":"SpecialTips"}],"AllowChildrenToStay":true,"AllowUseExistingBed":true,"AllowExtraBed":true,"AllowExtraCrib":true,"AllowUseExistingBedV2":"true","AllowExtraBedV2":"true","AllowExtraCribV2":"true"}

// Meal policy:
"MealsPolicyV2":{"MealPolicyV2":[{"Amount":[{"Type":"string","Amount":0,"Currency":"string"}],"MealType":[{"Code":"string","Name":"string","Extra":"string"}],"ServeType":[{"Code":"string","Name":"string","Extra":"string"}],"FoodMenu":[{"Code":"string","Name":"string","Extra":"string"}],"BusinessHourInfo":[{"StartTime":"string","EndTime":"string","WeeklyIndex":"string","IsOpen":0}],"IsProvide":"T"}],"Placeholder":"string"}

// Parking policy & charging points:
"ExternalFacilities":[{"FacilityItem":[{"Code":"string","Name":"string","Value":"string","Desc":"string"}],"Amount":[{"Type":"string","Amount":0,"Currency":"string"}],"CategoryName":"Parking"}],

// Pet policy
"Policies":[{"Text":"Pets are not allowed.","Code":"Pet"}]
```

#### 2.2 List important notices on hotel page
For certain time periods, there might be some important notices either from hotel or the municipal governnent. It's necessary to notify guests of these notices ahead of time so as to reduce complaints. You could get important notices from `Get Hotel Static Info` API. Make sure you have displayed important notices clearly on hotel page.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-hotelnotice.png)

**Code Sample**
```json
"ImportantNotices": [
    {
        "Text": "Disposable toiletries such as toothbrushes, combs, bath sponges, razors, nail files etc. are not provided by the hotel any more from Jul 1, 2019. Please contact the front desk for details.",
        "Category": "City"
    },
    {
        "Text": "In compliance with the Shanghai Regulations on Smoking Control in Public Places, effective Mar 1st 2017, this property will NOT offer smoking rooms. Smoking is prohibited anywhere inside the property.",
        "Category": "City"
    },
    {
        "Text": "Japanese guests must provide names in Roman letters.",
        "Category": "Hotel",
        "Start": "2017-06-21",
        "End": "2021-12-31",
        "Channel": "A"
    }
]
```

#### 2.3 Make sure each sellable room is exposed to the fitting guests.
Mind that some sellable rooms have certain sale restrictions on guests' nationalities and guests' identity proof for checkin. Make sure you have built corresponding mechanism to make sure each sellable room with these sale restrictions is exposed to guests of thaose restrictioned nationalities. Object `AreaApplicabilityInfo` and array `ApplicabilityIDs` in response of `Get Room Static Info` API have included the restrictions.

On our own platform, we combine user language (we have different sub-sites, such as US site, UK site, Japanese Site), user currency (rate display currency which guests choose), user profile, user ip address to help identify guests' real nationality. Then further decide which sellable room should be displayed to which guest.

 **Example**
 ![Picture is missing.](../assets/pictures/launch-requirements-nationalityrestriction.png)

 **Code Sample**
```json
// Nationality restriction:
"AreaApplicabilityInfo": {
    "Details": [
        {
            "ContinentID": "string",
            "ContinentName": "string",
            "CountryID": "string",
            "CountryName": "string",
            "RegionID": 1,
            "RegionName": "string",
            "IsApplicative": 0
        }
    ],
    "Description": "string"
}

// Identify proof needed when checking in:
"ApplicabilityIDs": 1,
```

#### 2.4 Make it obvious to identify whether guests must pay in advance or pay at hotel
Reservations made on sellable rooms must be [paid in advance](#pay-type) or [paid at hotel](#pay-type) depending on parameter `PayType` in response of `Get Hotel Detail Price` API. Be sure you have exposed clearly to guests.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-paytype.png)

#### 2.5 Mark clearly whether each sellable room needs to be guaranteed with credit card
For [pay-at-hotel rooms](#pay-type), they might need to be guaranteed by credit cards. Mark clearly whether guests will be required to provide credit card info at booking stage.You could rely on a combination of parameter `PayType`, `IsGuarantee` and `HoldTime` in response of `Get Hotel Detail Price` API to help identify it.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-guaranteetag.png)

#### 2.6 Label fast-confirmed rooms and non-fast confirmed rooms differently
In general, reservations made on rooms tagged [fast confirmation](#confirm-type) could get a final confirmation result very soon (often within 1 mins), while confirmation waiting time for reservations made on rooms tagged [non-fast confirmation](#confirm-type) is very uncertain (often within 24 hours). So it's very necessary to give guests different expectations. Parameter `IsFastConfirm` in response of `Get Hotel Detail Price` helps you identify whether a room could be confirmed fast or uncertain.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-confirmtime.png)

#### 2.7 Display physical room name, sellable room bed info and meal plan clearly
Make sure you have clearly displayed physical room name clearly. Take physical room name from parameter `RoomTypeName` in response of `Get Room Static Info` API. Also be sure that bed info of each sellable room could be easily found on your hotel page. Take bed info from array `RoomInfos.RoomBedInfos` in response of `Get Room Static Info` API.

Each sellable room has its own free meal plan which might differ a lot with others. Non-display or wrong display of meal plan could easily bring customer complaints. Make sure you have displayed clearly on each sellable room. `Get Hotel Detail Price` API will respond you meal plans.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-roomname-mealplan-occupancy-bedinfo.png)

#### 2.8 Cancellation policy of each sellable room is clearly visible
Cancellation policy is indicated by a combination of array `CancelPolicyInfos` and object `FreeCancelPolicyInfo` in response of `Get Hotel Detail Price` API. Clearly label whether a sellalbe room could be cancelled and display details of the cancellation policy.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-cancelpolicy.png)

**Code Sample**
```json
// Cancellation policy:
"CancelPolicyInfos":[{"PenaltyAmount":[{"Type":"DisplayCurrency","Amount":0,"Currency":"string"}],"PenaltyPercent":{"Percent":0},"Start":"2020-01-13T07:20:04Z","End":"2020-01-13T07:20:04Z"}]

// 30-minute Unconditional Cancellation Activity:
"FreeCancelPolicyInfo":{"Scene":-1},
```

#### 2.9 Taxes and fees are clearly stated as a separate line item
When price breakdown is provided for a sellable room, you must display tax items, fee items and their values clearly. When you are selling at our [retail price](#price-type), you could directly take tax amounts and fee amounts from array `Taxes` and `Fees` in response of `Get Hotel Detail Price` API. If you are selling at our [settlement price](#price-type), then you should calculate tax amounts and fee amount based on tax rules and fee rules which we provide in response `Get Room Static Info` API.

Above works for **international hotels only** (hotels in Hong Kong, Macao and Taiwan; hotels outside of China). For hotels within in China Mainland, we won't offer your price breakdown. This means you should separate taxes on your own. In practice, our partners often use this basic formula: 1. Total tax-exclusive price = Total tax-inclusive price / 115%.  2. Total tax = Total tax-inclusive price - total tax-exclusive price.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-taxfee.png)

### 3. Booking page

#### 3.1 Display extra important notices properly
Make sure you have also displayed extra important notices at booking page. Mind that extra important notices here differ from hotel-level important notices and city-level important notices. They are often more important and much easier to receive complaints. For example, guests must pay for gala dinner for New Year Festival. For extra important notices, you could access array `VendorMessages` in response of `Provision Check` API and must display these extra notices on your booking page.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-hotelextranotice.png)

**Code Sample**
```json
"VendorMessages":[{"SubSection":[{"Paragraph":["string"],"SubTitle":"City"}],"Title":"HotelNotice","Language":"zh","InfoType":"string"}]
```

#### 3.2 Display physical room name, sellable room bed info properly
Make sure that physical room name and sellable room bed info could be easily found on booking page. As per our experience, incorrect room name mapping and wrong display of bed info will cause more complaints. You could take these information from parameter `RoomTypeName` and array `RoomInfos.RoomBedInfos` in response of `Get Room Static Info` API.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-bookingpage-roomname-bedinfo.png)

#### 3.3 Real-time cancellation policy must be stated clearly
Since there's time gap between guest viewing of hotel page and booking page, cancellation policy might have changed when guest view booking page. Make sure you are displaying the real-time cancellation policy to guests at this stage. When guests open booking page from hotel page, you must request `Provision Check` API once. Object `NewCancelPenalties` in its response includes the real-time cancellation policy.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-bookingpage-cancelpolicy.png)

**Code Sample**
```json
"NewCancelPenalties": {
	"CancelPenalty": [
		{
			"AmountPercent": {
				"DisplayCurrency": [
					{
						"ExclusiveAmount": 0,
						"InclusiveAmount": 0,
						"CurrencyCode": "string"
					}
				],
				"Amount": 0,
				"CurrencyCode": "string",
				"Percent": "string"
			},
			"Start": "string",
			"End": "string"
		}
	],
	"FreeCancelPolicyScene": "string",
	"CancelPenaltyType": "string"
}
```

#### 3.4 Real-time meal plans must be stated clearly
Since there's time gap between guest viewing of hotel page and booking page, meal plans might have changed when guests view booking page. Make sure you are displaying the real-time meal plans at this stage. When guests open booking page from hotel page, you must request `Provision Check` API once. Object `MealsIncluded` in its response includes the real-time meal plans.

Also mind that meal plan is based on each day within the reservation. This means it might happen that certain days within the reservation don't include free meal plans. Take care!

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-bookingpage-mealplan.png)

**Code Sample**
```json
"MealsIncluded": {
    "NumberOfBreakfast": 0,
    "NumberOfLunch": 0,
    "NumberOfDinner": 0

}
```

#### 3.5 Real-time total price must be used to make reservations
Since there's time gap between guest viewing of hotel page and booking page, room prices might have changed when guests view booking page. Make sure you are suing real-time price (either [retail price](#price-type) or [settlement price](#price-type)) to make a reservation. When guests open booking page from hotel page, you must request `Provision Check` API to request real-time price.

**Code Sample**
```json
// Total price based on retail price:
"Total": {
    "TPA_Extensions": [
        {
            "ExclusiveAmount": 0,
            "InclusiveAmount": 0,
            "CurrencyCode": "string"
        }
    ],
    "ExclusiveAmount": 0,
    "InclusiveAmount": 0,
    "CurrencyCode": "string"
}

// Total price based on settlement price:
"TotalCost": {
    "TPA_Extensions": [
        {
            "ExclusiveAmount": 0,
            "InclusiveAmount": 0,
            "CurrencyCode": "string"
        }
    ],
    "ExclusiveAmount": 0,
    "InclusiveAmount": 0,
    "CurrencyCode": "string"
}
```

#### 3.6 Taxes and fees are clearly stated as a separate line item
When price breakdown is provided for a sellable room, you must display tax items, fee items and their values clearly. When you are selling at our [retail price](#price-type), you could directly take tax amounts and fee amounts from array Taxes and Fees in response of `Provision Check` API. If you are selling at our [settlement price](#price-type), then you should calculate tax amounts and fee amount based on tax rules and fee rules which we provide in response `Get Room Static Info` API.

Above works for **international hotels only** (hotels in Hong Kong, Macao and Taiwan; hotels outside of China). For hotels within in China Mainland, we won't offer your price breakdown. This means you should separate taxes on your own. In practice, our partners often use this basic formula: 1. Total tax-exclusive price = Total tax-inclusive price / 115%. 2. Total tax = Total tax-inclusive price - total tax-exclusive price.

**Example**
![Picture is missing.](../assets/pictures/launch-requirements-bookingpage-taxfee.png)

#### 3.7 Credit cards must be encrypted for security purpose
You must also follow PCI (Payment Card Industry) regulations when requesting, handling and storing customer credit card data. When you pass a credit card to us to guarantee for a reservation made on a [pay-at-hotel room](#pay-type), credit card must be encrypted following our [encryption algorithm](#encryption-algorithm).
