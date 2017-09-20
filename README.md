# odokus 3rd Party API (Android)

Simple class to use odokus 3rd party API calls in your project. Using the geo api - you gain a very easy and fast way to store and fetch geo tagged events from and to your odokus account.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to install the software and how to install them

* Android Studio
* Your project setup to start with
* The following libraries ([Get libs](http://software.dzhuvinov.com/json-rpc-2.0-client.html))
	* json-smart-1.2.jar
	* jsonrpc2-base-1.38.jar
	* jsonrpc2-client-1.16.4jar 
* copy json* libs to libs folder in your project root
* Add json* libs to project / build.gradle 
* Clone this repo into your projects source code folder
* Your user credentials for odokus 


### Using the API

Using the API to fetch GeoEvents from odokus is very simple. In your project, i.e. in your activities onCreate() method, instantiate the api object and start fetching or writing events. The api contains a listener interface so you can add multiple listeners that will receive api answers.

#### API instantiation

Import the needed files by adding `import de.whilecoffee.geoapi.*;` to your activity class file.

Add an api object variable and instantiate it by:

```
... 
public class MyAwesomeActivity extends AppCompatActivity implements Odokus3rdPartyGeoAPI.OdokusGeoApiListener {

    Odokus3rdPartyGeoAPI geoApi;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        geoApi = new Odokus3rdPartyGeoAPI(this, "YOUR_USER", "YOUR_PASSWORD");
        geoApi.setOdokusGeoApiListener(this);

```
After setting yourself as listener, you can ask the geoApi for Events by calling

```
		// Create start and end dates
		Calendar cal = Calendar.getInstance();
        cal.add(Calendar.DATE, -3);
        Date start = cal.getTime();
        Date end = new Date();
        
        // make request with geoApi
        geoApi.getGeoEvents(start, end);
```
You will receive the response through your listener methods:

```
public void receivedGeoEvents(List<GeoEvent>events)
{
    // Handle GeoEvents
    for (GeoEvent e : events)
    {
        // i.e. add overlay to a map or add to observable list,
        //...
    }
    // update UI
    //...
}
```


## Authors

* **Johannes Dürr** - *Initial work* - [whileCoffee](https://whilecoffee.de)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details