yii2-geoip
=========

Yii2 Module to allow for easy usage of the MaxMind Free dbs. (Develop by http://qtmax.com)

Installation of the component:
------------------------
* Extract the release file under `components`
* Change web.php configuration file

```php
        'components' => array(
            ...
           'geoip' => [
			'class' => 'app\components\CGeoIP',
			'filename' => dirname(__DIR__) . '/components/GeoIP/GeoIP.dat', // specify filename location for the corresponding database
			'mode' => 'STANDARD',  // Choose MEMORY_CACHE or STANDARD mode
	      ],
            ...
        ),
```

Usage instructions:
------------------------

All methods accept an IP address as an argument.
If no argument is supplied Yii::$app->getRequest()->getUserIP() is used.
```php
    $location = Yii::$app->geoip->lookupLocation();
    $countryCode = Yii::$app->geoip->lookupCountryCode();
    $countryName = Yii::$app->geoip->lookupCountryName();
    $org = Yii::$app->geoip->lookupOrg();
    $regionCode = Yii::$app->geoip->lookupRegion();
```
Location attributes:
```php
    $location->countryCode
    $location->countryCode3
    $location->countryName
    $location->region
    $location->regionName
    $location->city
    $location->postalCode
    $location->latitude
    $location->longitude
    $location->areaCode
    $location->dmaCode
```


How to update Maxmind Free DBs example:
------------------------
`updateGeoIP.sh`
this script will only download if there is a new version of the database
```bash
    cd /usr/local/share/GeoIP (change to your folder)
    wget -N -q http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz
    wget -N -q http://geolite.maxmind.com/download/geoip/database/GeoLiteCountry/GeoIP.dat.gz
    wget -N -q http://geolite.maxmind.com/download/geoip/database/GeoIPv6.dat.gz
    
    gunzip -c GeoLiteCity.dat.gz > GeoLiteCity.dat
    gunzip -c GeoIP.dat.gz > GeoIP.dat
    gunzip -c GeoIPv6.dat.gz > GeoIPv6.dat
```

* Setup a cron job to run this script monthly.
