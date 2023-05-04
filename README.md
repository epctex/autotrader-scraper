# Actor - Autotrader Scraper

## Autotrader scraper

Since Autotrader doesn't provide a good and free API, this actor should help you to retrieve data from it.

The Autotrader data scraper supports the following features:

-   Search any search results - Get any search results. New or used cars with brand and model information.

-   Filter by anything without any limits - Filter your search results by brand, price and any other options that the website provides. No limits!

-   Scrape any listing details - Retrieve information about the cars. Brand, model, price, mileage, fuel type, transmission, interior colors, exterior colors and many other features.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/autotrader-scraper/issues).


## Input Parameters

The input of this scraper should be JSON containing the list of pages on Autotrader that should be visited. Possible fields are:

- `startUrls`: (Required) (Array) List of Autotrader URLs. It should be search, list, or listing detail URL.

- `includeReviews`: (Optional) (Boolean) This will add all the reviews that XXXXX provides into the detail objects. Please keep in mind that the time and resources the actor uses will increase proportionally by the number of reviews.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as argument and returns object with data.

- `customMapFunction`: (Optional) (String) Function that takes each objects handle as argument and returns object with executing the function.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

### Tip

When you want to have a scrape over a specific listing URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape many as listings as possible. Therefore, it forefronts all listing detail requests. If actor doesn't block very often it'll scrape 100 listings in 2 minutes with ~0.15-0.25 compute units.

### Autotrader Scraper Input example

```json
{
  "startUrls":[
    "https://www.autotrader.com/cars-for-sale/all-cars/harrisburg-pa-17101",
    "https://www.autotrader.com/cars-for-sale/vehicledetails.xhtml?0=vehicledetails.xhtml&listingId=675520329&allListingType=all-cars&city=Harrisburg&state=PA&zip=17101&searchRadius=50&=&isNewSearch=false&referrer=%2Fcars-for-sale%2Fall-cars%2Fharrisburg-pa-17101%3F0%3Dvehicledetails.xhtml%26listingId%3D651889249%26searchRadius%3D50%26&clickType=listing",
    "https://www.autotrader.com/cars-for-sale/vehicledetails.xhtml?0=vehicledetails.xhtml&listingId=675490538&allListingType=all-cars&city=Harrisburg&state=PA&zip=17101&searchRadius=50&=&isNewSearch=false&referrer=%2Fcars-for-sale%2Fall-cars%2Fharrisburg-pa-17101%3F0%3Dvehicledetails.xhtml%26listingId%3D651889249%26searchRadius%3D50%26&clickType=listing",
    "https://www.autotrader.com/cars-for-sale/vehicledetails.xhtml?0=vehicledetails.xhtml&listingId=675749094&allListingType=all-cars&city=Harrisburg&state=PA&zip=17101&searchRadius=50&=&isNewSearch=false&referrer=%2Fcars-for-sale%2Fall-cars%2Fharrisburg-pa-17101%3F0%3Dvehicledetails.xhtml%26listingId%3D651889249%26searchRadius%3D50%26&clickType=listing"
  ],
  "endPage": 3,
  "proxy":{
    "useApifyProxy":true,
    "countryCode":"US"
  }
}


```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## Autotrader Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Autotrader actor.

## Scraped Autotrader Output

The structure of each item in Autotrader looks like this:

```json
{
	"id": 674376797,
	"url": "https://www.autotrader.com/cars-for-sale/vehicledetails.xhtml?listingId=674376797&allListingType=all-cars&city=Harrisburg&state=PA&zip=17101&searchRadius=50&marketExtension=include&isNewSearch=false&showAccelerateBanner=false&sortBy=relevance&numRecords=25&referrer=%2Fcars-for-sale%2Fall-cars%2Fharrisburg-pa-17101%3FsearchRadius%3D50%26marketExtension%3Dinclude%26isNewSearch%3Dfalse%26showAccelerateBanner%3Dfalse%26sortBy%3Drelevance%26numRecords%3D25&clickType=listing",
	"title": "Used 2021 Toyota Tacoma TRD Off-Road",
	"brand": "Toyota",
	"model": "Tacoma",
	"stockNumber": "MM403382",
	"vin": "3TMCZ5AN8MM403382",
	"year": 2021,
	"price": 42242,
	"features": {
		"Exterior": [
			"Aluminum Wheels",
			"Automatic Headlights",
			"Automatic Highbeams",
			"Fog Lamps",
			"Heated Mirrors",
			"Integrated Turn Signal Mirrors",
			"Power Mirror(s)",
			"Tires - Front All-Season",
			"Tires - Rear All-Season",
			"Tow Hitch"
		],
		"Interior": [
			"A/C",
			"Adjustable Steering Wheel",
			"Auto-Dimming Rearview Mirror",
			"Bucket Seats",
			"Cloth Seats",
			"Driver Adjustable Lumbar",
			"Intermittent Wipers",
			"Leather Steering Wheel",
			"Pass-Through Rear Seat",
			"Power Door Locks",
			"Power Driver Seat",
			"Power Windows",
			"Privacy Glass",
			"Rear Bench Seat",
			"Steering Wheel Audio Controls",
			"Trip Computer",
			"Variable Speed Intermittent Wipers"
		],
		"Safety": [
			"ABS",
			"Brake Assist",
			"Child Safety Locks",
			"Conventional Spare Tire",
			"Daytime Running Lights",
			"Driver Air Bag",
			"Front Head Air Bag",
			"Front Side Air Bag",
			"Knee Air Bag",
			"Lane Departure Warning",
			"Passenger Air Bag",
			"Passenger Air Bag Sensor",
			"Rear Head Air Bag",
			"Security System",
			"Stability Control",
			"Tire Pressure Monitor",
			"Traction Control"
		],
		"Mechanical": [
			"Four Wheel Drive",
			"Front Disc/Rear Drum Brakes",
			"Power Steering"
		],
		"Technology": [
			"AM/FM Stereo",
			"Adaptive Cruise Control",
			"Auxiliary Audio Input",
			"Back-Up Camera",
			"Bluetooth Connection",
			"Cruise Control",
			"Immobilizer",
			"Keyless Entry",
			"Keyless Start",
			"MP3 Player",
			"Satellite Radio",
			"Telematics",
			"WiFi Hotspot"
		],
		"Other": [
			"Driver Monitoring",
			"Front Collision Mitigation",
			"Locking/Limited Slip Differential",
			"Requires Subscription",
			"Smart Device Integration",
			"Tow Hooks"
		]
	},
	"daysOnSite": 3,
	"engine": "6-Cylinder",
	"fuelType": "Gasoline",
	"description": "Priced below KBB Fair Purchase Price!<br>Non-Smoker, 120V/400W Deck Mounted AC Power, 6 Speakers, ABS brakes, Air Conditioning, Alloy wheels, Anti-whiplash front head restraints, Apple CarPlay/Android Auto, Auto High-beam Headlights, Black Overfenders, Brake assist, Dual front impact airbags, Dual front side impact airbags, Electronic Stability Control, Engine Immobilizer, Fabric Seat Trim (FD), Front Center Armrest, Front fog lights, Heated door mirrors, Illuminated entry, Low tire pressure warning, Panic alarm, Passenger door bin, Power door mirrors, Power driver seat, Power Sliding Rear Window w/Privacy Glass, Radio: AM/FM Radio, Rear step bumper, Remote keyless entry, Speed control, Split folding rear seat, Steering wheel mounted audio controls, Tachometer, Tilt steering wheel, Traction control, TRD Off Road Package. CARFAX One-Owner. Certified.<br>Cement 2021 Toyota Tacoma TRD Off-Road V6 4WD 6-Speed 3.5L V6 PDI DOHC 24V LEV3-ULEV70 278hp<br><br>Recent Arrival! Odometer is 8707 miles below market average!<br><br>Toyota Certified Used Vehicles Details:<br><br>* Roadside Assistance<br>* Limited Warranty: 12 Month/12,000 Mile (whichever comes first) from TCUV purchase date<br>* Limited Comprehensive Warranty: 12 Month/12,000 Mile (whichever comes first) from certified purchase date. Roadside Assistance for 7 Year / 100,000 Mile<br>* 160 Point Inspection<br>* Vehicle History<br>* Warranty Deductible: $0<br>* Transferable Warranty<br>* Powertrain Limited Warranty: 84 Month/100,000 Mile (whichever comes first) from TCUV purchase dateTacoma 4WD Four Wheel Drive, Locking/Limited Slip Differential, Tow Hitch, Power Steering, ABS, Front Disc/Rear Drum Brakes, Brake Assist, Locking/Limited Slip Differential, Aluminum Wheels, Tires - Front All-Season, Tires - Rear All-Season, Conventional Spare Tire, Tow Hooks, Heated Mirrors, Power Mirror(s), Integrated Turn Signal Mirrors, Intermittent Wipers, Variable Speed Intermittent Wipers, Privacy Glass, Power Door Locks, Daytime Running Lights, Automatic Headlights, Automatic Highbeams, Fog Lamps, AM/FM Stereo, Satellite Radio, MP3 Player, Bluetooth Connection, Auxiliary Audio Input, Smart Device Integration, Requires Subscription, Steering Wheel Audio Controls, Power Driver Seat, Bucket Seats, Driver Adjustable Lumbar, Pass-Through Rear Seat, Rear Bench Seat, Adjustable Steering Wheel, Trip Computer, Power Windows, WiFi Hotspot, Leather Steering Wheel, Keyless Entry, Power Door Locks, Keyless Entry, Power Door Locks, Keyless Start, Cruise Control, Adaptive Cruise Control, A/C, Cloth Seats, Auto-Dimming Rearview Mirror, Power Windows, Power Door Locks, Trip Computer, Security System, Immobilizer, Traction Control, Stability Control, Traction Control, Front Side Air Bag, Telematics, Requires Subscription, Lane Departure Warning, Front Collision Mitigation, Driver Monitoring, Tire Pressure Monitor, Front Head Air Bag, Rear Head Air Bag, Passenger Air Bag Sensor, Knee Air Bag, Driver Air Bag, Passenger Air Bag, Child Safety Locks, Back-Up Camera",
	"images": [
		"https://images.autotrader.com/hn/c/2b8d9b3ced6649a4bfb0d9f5c1c604ec.jpg",
		"https://images.autotrader.com/hn/c/b09db1d7d92a4e15a001d59b582cd084.jpg",
		"https://images.autotrader.com/hn/c/9df669fc7b064a26b2814c6694c87004.jpg",
		"https://images.autotrader.com/hn/c/5ff9c77054074b2580cd13422bee7032.jpg",
		"https://images.autotrader.com/hn/c/51adf23e01f04373aa86386a3abbf379.jpg",
		"https://images.autotrader.com/hn/c/367d292505c04ccc8846bdab5ca134f3.jpg",
		"https://images.autotrader.com/hn/c/2139773562874e39b7856b06e8be4186.jpg",
		"https://images.autotrader.com/hn/c/3cc10090552f406ca42911298f4c93b2.jpg",
		"https://images.autotrader.com/hn/c/8f74cbd9ab814a3b8e93cfbb84c7d774.jpg",
		"https://images.autotrader.com/hn/c/9275f2e471b74d75bf963222349cab87.jpg"
	],
	"ownerTitle": "Faulkner Toyota - Harrisburg",
	"ownerRating": 5,
	"ownerRatingCount": 1589,
	"ownerPhone": "7177988257"
}
```

## Contact
Please visit us through [epctex.com](https://epctex.com) to see all the products that is available for you. If you are looking for any custom integration or so, please reach out to us through the chat box in [epctex.com](https://epctex.com). In need of support? [devops@epctex.com](mailto:devops@epctex.com) is at your service.
