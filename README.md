# WMS MapType

JavaScript library for overlaying WMS content on Google Maps (v3).

Mimics a tiling web service by calculating the Web Spherical Mercator (`EPSG:3857`, `EPSG:900913`) bounding box of the visible tiles.

Uses include overlaying weather data (radar, warnings, storm forecasts), satellite imagery, landmarks, topographic features, and other WMS provided content.

## Usage

Create a new WMS MapType using the following constructor.

    WmsMapType(name, url, params[, options])

* __`name:string`__: (Required) Name of the MapType
* __`url:string`__: (Required) Base URL for the WMS
* __`params:object`__: (Required) Key/value pairs representing WMS params (e.g. `layers`)
 * `service`: The service type [default: `'WMS'`]
 * `version`: The service version [default: `'1.1.1'`]
 * `request`: The service request [default: `'GetMap'`]
 * `format`: The image format [default: `'image/png'`]
 * `transparent`: Transparent image [default: `true`]
 * `width`: The image width [default: `256`]
 * `height`: The image heigh [default: `256`]
 * `srs`: The projection [default: `'EPSG:3857'`]
 * `styles`: The WMS style(s) [default: `''`]
 * __`layers`__: (Required) The WMS layer(s) [default: `''`]
* `options:object`: Extra options for library (e.g. `opacity`)
 * `opacity`: The tile opacity [default: `0.5`]
 * `cache`: Cache WMS requests [default: `false`]

Add to a base map using the following method.

    addToMap(map[, index])

* __`map:google.maps.Map`__: (Required) Base map
* `index:int`: Optional layer index

Remove from a base map using the following method.

    removeFromMap(map)

* __`map:google.maps.Map`__: (Required) Base map

## Example

    var wxRadar = new WmsMapType(
            "NEXRAD Base Reflectivity",
            "http://mesonet.agron.iastate.edu/cgi-bin/wms/nexrad/n0q.cgi",
            {layers: "nexrad-n0q-900913"},
            {opacity: 0.7});

    var wxWarnings = new WmsMapType(
            "NWS Warnings",
            "http://mesonet.agron.iastate.edu/cgi-bin/wms/us/wwa.cgi",
            {layers: "warnings_p,warnings_c"});

    wxRadar.addToMap(map);
    wxWarnings.addToMap(map);

## Extension

Extended services, like those that accept `time` or `elevation`, can also be used with this library.

<pre>
var wxRadarHistory = new WmsMapType(
        "Historical NEXRAD Base Reflectivity",
        "http://mesonet.agron.iastate.edu/cgi-bin/wms/nexrad/n0q-t.cgi",
        {layers: "nexrad-n0q-wmst", <b>time: "2014-04-28T21:00:00Z"</b>},
        {cache: true});

wxRadarHistory.addToMap(map);
</pre>

## Notes

Currently optimized for WMS 1.1.1 and does not support WMS 1.3.0 params.

The WMS must support `EPSG:3857` or `EPSG:900913` SRS. 

## Acknowledgements

Credit goes to the following resources.

* https://msdn.microsoft.com/en-us/library/bb259689.aspx
* http://www.maptiler.org/google-maps-coordinates-tile-bounds-projection/
* https://github.com/timwaters/whoots/

## Etc

Beau Grantham <br />
https://www.nologs.org/6EA6595C.asc
