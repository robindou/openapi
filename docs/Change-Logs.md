> **2020-07-24**
> Modified description of room nationality restrictions for *Get Room Static Info* API.

> **2020-07-23**
> Optimized doc structure to cover more solutions!

> **2020-06-25**
> Added param `IsAllowRepricing` in response of *Get Hotel Detail Price* and *Provision Check* API.

> **2020-06-25**
> Added total cost  in *Reservation Saving* API, free partners from calculating total cost.

> **2020-06-25**
> Added param `FilterByLanguage` in *Get Hotel List* API.

> **2020-05-20**
> Added new api *Get Payment Elements* in chapter *Extended API Service*.

> **2020-05-10**
> Deprecated existing api *Report Guest Actual Stay Info*. Night audit result depends on Trip.com night check result with hotel.

> **2020-05-10**
> Modified the description of param `Start` and `End` of cancellation policy in *Reservation Details*, *Reservation Saving*, *Provision Check* and *Get Hotel Detail Price* APIs.

> **2020-04-25**
> Added new object `IntlUserProperties` in *Reservation Saving* and *Provision Check* APIs. This aims to allign membership layers with Trip.com.

> **2020-04-11**
> Added array `Taxes` and `Fees` in *Reservation Details*, *Reservation Saving* and *Provision Check* APIs.

> **2020-04-11**
> Added object `IDCard` and modified description of param `InvoiceType` in request of *Reservation Saving* API.

> **2020-04-02**
> Added overall meal plan and daily meal plans in response of *Provision Check* API.

> **2020-03-28**
> Added param `ID` for taxes and fees in response of *Get Hotel Detail Price* API.

> **2020-03-28**
> Added object `ParentCity`, `Province` and `Country` in *Get Hotel Static Info* API.

> **2020-03-08**
> Modified description of payment ways in *Reservation Submitting* API.

> **2020-02-25**
> Added more possible values of param `IsAllowSmoking` in *Get Room Static Info* API.

> **2020-02-19**
> Modified description of param `DisplayCurrency` in *Reservation Saving* API.

> **2020-02-19**
> Modified description of array `DepositPayments` in *Provision Check* and *Reservation Saving* APIs.

> **2020-02-19**
> Modified description of array `UserProperties` in *Get Hotel Detail Price*, *Provision Check* and *Reservation Saving* APIs.

> **2020-02-10**
> Modified descrition of param `GuaranteeCode` in *Provision Check* API.

> **2020-01-22**
> Modified descrition of array `MaskCampaignInfos` in *Get Room Static Info* API. The restriction applies to Trip.com China affiliate partners only.

> **2020-01-02**
> Deprecated `BookingRules.MemberLimitInfo` in response of *Get Room Static Info* API.

> **2020-01-02**
> Assigning proxy icodes into each sepated api insteading of grouping them into one single chapter. This helps to understand their usage scenarios.

> **2019-12-24**
> Added extra params to turn on membership rates for *Get Hotel Detail Price* API.

> **2019-12-24**
> Added extra params that must be verified when doing provision check for a membership rate.

> **2019-12-10**
> Replace original *Detect Static Info Change* API with a complete new one. New API supports much more features.

> **2019-11-03**
> Added new entities such as `HotelTags`, `BossInfo`, `SellerShowInfos`, `VideoItems`, `SepecialServiceForChinese`, `HotelFeatures`, `HotelUsedNames`, `ApplicabilityInfo` in *Get Hotel Static Info* API.

> **2019-09-24**
> Deprecated *Get Hotel List By City* API. Replaced it with *Get Hotel List* API.

> **2019-09-24**
> Deprecated original *Get City List* API. Replaced it with a new one supporting much more new features.

> **2019-09-24**
> Modified children occupancy limits in object `ChildAndExtraBedPolicy` of *Get Hotel Static Info* API.

> **2019-06-18**
> Modified descrition of param `LateArrivalTime` and `HoldTime` in *Provion Check* API.

> **2019-03-06**
> Deprecated original textual meal policy. Added structured meal policy `MealsPolicyV2` in *Get Hotel Static Info* API.

> **2019-01-01**
> Added customized search tag `MinPriceRoomID` for *Get Hotel Detail Price* API. It helps to improve rate consistency between city page and hotel page.

> **2018-10-21**
> Added a new order status `NoRoom` for `Reservation Details`. Affiliate partners should set different order processing mechanisms when they meet the order status.

> **2018-09-15**
> Deprecated original textual child and adult occupancy policy. Replaced it with structured children occupancy and adult occupancy policy in *Get Hotel Static Info* API.

> **2018-08-02**
> Make *Payment Confirmation* API more compatible supporting both `Get` and `Post` methods.

> **2018-05-02**
> Added adult and children occupancy filters in *Get Hotel Lowest Price* and *Get Hotel Detail Price* APIs.

> **2018-03-15**
> Modified `OnlineIntlGTASearch` to `OnLineIntlGTASearch` for param `SearchType` in request of `Get Hotel Lowest Price` API.

> **2018-03-10**
> More revision records are ommitted here.
