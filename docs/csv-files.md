# Monento CSV files

*Version 1*

## File formats

### Accounts

Columns:

* name – **required**. Unique name of an account.
* type – **required**. Values: `asset`, `income` and `expense` (see below the description).
* parentName – **required**, can be empty. Name of a parent account. If the parent account is missed it will be created. The account will be added into a group of the parent account.
* iconName – **required**, can be empty. Name of app's icon.
* iconColor – **required**, can be empty. Name of app's color (see below).
* notes – **required**, can be empty.
* templateCode – optional. Used by the app to identify predefined standard accounts.
* isArchived – optional. Values: `true`, `false`. The account is in the archive in case the value is `true`.

Example: 

```
name,parentName,type,iconName,iconColor,templateCode,isArchived,notes
ATM fees,Bank services,expense,bank-atm-fees,green,atm_fees,false,
Accessories,Clothing,expense,clothing-accessories,light_blue,accessories,false,
Allowance,Kids,expense,kids-allowance2,teal,allowance,false,
Anniversary,Gifts,expense,gifts-anniversary,deep_orange,anniversary,false,
Attractions,Travels,expense,travel-attraction,deep_orange,attractions,false,
Auto parts,Car,expense,car-auto-parts,amber,auto_parts,false,
Baby supplies,Kids,expense,kids-baby-supplies,green,baby_supplies,false,
Babysitter & daycare,Kids,expense,kids-daycare,light_green,babysitter_and_daycare,false,
Bank accounts,,asset,bank,green,asset_bank_accounts,false,
Bank card costs,Bank services,expense,bank-credit-card-fees,light_green,credit_card_fees,false,
Bank charges,Bank services,expense,bank-service-fees,lime,bank_charges,false,
Bank services,,expense,bank,pink,bank_services,false,
Beauty salon,Personal care,expense,personal-care-beauty-salon,orange,beauty_salon,false,
Birthdays,Gifts,expense,gifts-birthday,red,birthdays,false,
Bonus,Earnings,income,money-bonus,pink,bonus,false,
Books,Entertainment & recreation,expense,entertainment-books,pink,books,false,
Car,,expense,car,purple,car,false,
Car insurance,Car,expense,car-insurance,orange,car_insurance,false,
```

### Transactions

Columns:

* id  – **required**, can be empty. Unique identifier (ID) of a transaction. In case it is empty a new transaction will be created on each importing of the file. Otherwise a transaction specified by ID will updated or created.
* date – **required**. A date of transaction, it must use one of supported date formats (see below)
* sourceAccountName – **required**. Name of a source account. The account is not present it will be created.
* sourceAccountType – **required**. Type of the source account (see below).
* sourceAmount – **required**. Amount to be subtracted from the source account (negative value).
* sourceCurrencyCode – **required**. See available codes below.
* destAccountName – **required**. Name of a destination account. The account is not present it will be created.
* destAccountType – **required**. Type of the destination account (see below).
* destAmount – **required**. Amount to be added to the destination account (positive value).
* destCurrencyCode – **required**. See available codes below.
* notes – **required**, can be empty.
* tags – optional. A comma-separated list of tag names. It should be in double quotes in case more than one tag is specified. Example: `"MyTag,SomeTag"`.

Example:

```
id,date,sourceAccountType,sourceAccountName,sourceAmount,sourceCurrencyCode,destAccountType,destAccountName,destAmount,destCurrencyCode,notes,tags
bA7DaqeD4hNs4jJNz,2018-12-14 04:04,asset,Wallet,-2.65,USD,expense,Coffee,2.65,USD,,MyTag
1ln47w14Xu2TbLnGy,2018-12-14 04:04,asset,Wallet,-9.35,USD,expense,Lunch,9.35,USD,,"MyTag,SomeTag"
7kQpy1Dp0fgfmwQL,2018-12-13 04:04,income,Salary & wages,-500,USD,asset,My card,500,USD,,
wENA6q4AvCWc9n2yK,2018-12-13 04:04,asset,Wallet,-32.15,USD,expense,Food & Groceries,32.15,USD,,
BAq2YQz2bh3HBl2eb,2018-12-12 04:04,asset,My card,-2,USD,expense,Bank charges,2,USD,,
NaXL6WnLYi5I3k9QD,2018-12-12 04:04,asset,Wallet,-16,USD,expense,Car wash,16,USD,,
XZ5K0WjKYuBCA9vzk,2018-12-12 04:04,asset,My card,-23.41,USD,expense,Gasoline,23.41,USD,,
oPw3bm23BuKt9EX,2018-12-12 04:04,asset,My card,-7,USD,expense,Clothing,7,USD,,
kGbrY7BrnCMi94oko,2018-12-12 04:04,asset,My card,-22,USD,expense,Textbooks,22,USD,,
M1K9JW0PGHYTwlDmk,,equity,Opening Balances,-100,USD,asset,Wallet,100,USD,,
2lMKD4p66s0Tdve11,,equity,Opening Balances,-100,USD,asset,Piggy Bank,100,USD,,
9g20aNB0pFATv0NJ,,equity,Opening Balances,-100,USD,asset,My card,100,USD,,
eAPgkbNgDI6TkQm6r,,equity,Opening Balances,-1000,USD,asset,Savings,1000,USD,,
```

### Tags

Columns:

* `name`  – **required**. Unique name of a tag.
* `iconName` – **required**, can be empty. Name of app's icon.
* `color` – **required**, can be empty. Name of app's color (see below).
* `isArchived` – optional. Values: `true`, `false`. The tag is in the archive in case the value is `true`.
* `isPinned` – optional. Values: `true`, `false`. The tag is pinned to the app menu in case the value is  `true`.

Example:

```
name,iconName,color,isArchived,isPinned
MyTag,,,false,false
SomeTag,,,false,false
```

## Data types and values

### Account types

* `asset` – asset account, e.g. wallet, cards and bank accounts.
* `income` – income category.
* `expense` – expense category.
* `equity` – used by the app internally for opening balances.
* `liability` – reserved type for the app.

### Date formats

* `YYYY-MM-DD` – a date
* `YYYY-MM-DD HH:mm` – a date with time
* `YYYY-MM-DD HH:mm ZZ` – a date with time and timezone

Timezone can be specified in the following formats:
* `+9999`, `-9999` – Time offset
* `UT` – equals to `+0000`
* `GMT` – equals to `+0000`

### Currency codes

ISO currencies:

`AED`, `AFN`, `ALL`, `AMD`, `ANG`, `AOA`, `ARS`, `AUD`, `AWG`, `AZN`, `BAM`, `BBD`, `BDT`, `BGN`, `BHD`, `BIF`, `BMD`, `BND`, `BOB`, `BRL`, `BSD`, `BTN`, `BWP`, `BYN`, `BZD`, `CAD`, `CDF`, `CHF`, `CLP`, `CNY`, `COP`, `CRC`, `CUC`, `CUP`, `CVE`, `CZK`, `DJF`, `DKK`, `DOP`, `DZD`, `EGP`, `ERN`, `ETB`, `EUR`, `FJD`, `FKP`, `GBP`, `GEL`, `GHS`, `GIP`, `GMD`, `GNF`, `GTQ`, `GYD`, `HKD`, `HNL`, `HRK`, `HTG`, `HUF`, `IDR`, `ILS`, `INR`, `IQD`, `IRR`, `ISK`, `JMD`, `JOD`, `JPY`, `KES`, `KGS`, `KHR`, `KMF`, `KPW`, `KRW`, `KWD`, `KYD`, `KZT`, `LAK`, `LBP`, `LKR`, `LRD`, `LSL`, `LYD`, `MAD`, `MDL`, `MGA`, `MKD`, `MMK`, `MNT`, `MOP`, `MRO`, `MUR`, `MVR`, `MWK`, `MXN`, `MYR`, `MZN`, `NAD`, `NGN`, `NIO`, `NOK`, `NPR`, `NZD`, `OMR`, `PAB`, `PEN`, `PGK`, `PHP`, `PKR`, `PLN`, `PYG`, `QAR`, `RON`, `RSD`, `RUB`, `RWF`, `SAR`, `SBD`, `SCR`, `SDG`, `SEK`, `SGD`, `SHP`, `SLL`, `SOS`, `SRD`, `SSP`, `STD`, `SVC`, `SYP`, `SZL`, `THB`, `TJS`, `TMT`, `TND`, `TOP`, `TRY`, `TTD`, `TWD`, `TZS`, `UAH`, `UGX`, `USD`, `UYU`, `UZS`, `VEF`, `VND`, `VUV`, `WST`, `XAF`, `XCD`, `XOF`, `XPF`, `YER`, `ZAR`, `ZWL` 

Crypto currencies:

`BTC`, `BCH`, `BTG`, `ETC`, `ETH`, `LTC`, `XMR`, `XRP`, `ZEC`

### Colors

* Name of the app colors:

  `red`, `pink`, `purple`, `deep_purple`, `indigo`, `blue`, `light_blue`, `cyan`, `teal`, `green`, `light_green`, `lime`, `yellow`, `amber`, `orange`, `deep_orange`, `brown`, `grey`, `blue_grey`, `black`, `white`
* Value of HTML color in hexadecimal format: `#FF00AA`. 

