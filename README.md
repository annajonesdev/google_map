<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="initial-scale=1.0, user-scalable=no">
    <meta charset="utf-8">
    <title>Travel modes in directions</title>
    <style>
      /* Always set the map height explicitly to define the size of the div
       * element that contains the map. */
      #map {
        height: 100%;
      }
      /* Optional: Makes the sample page fill the window. */
      html, body {
        height: 100%;
        margin: 0;
        padding: 0;
      }
      #floating-panel {
        position: absolute;
        top: 10px;
        left: 25%;
        z-index: 5;
        background-color: #fff;
        padding: 5px;
        border: 1px solid #999;
        text-align: center;
        font-family: 'Roboto','sans-serif';
        line-height: 30px;
        padding-left: 10px;
      }
    </style>
  </head>
  <body>
    <div id="floating-panel">
    <b>Mode of Travel: </b>
    <select id="mode">
      <option value="DRIVING">Driving</option>
      <option value="WALKING">Walking</option>
      <option value="BICYCLING">Bicycling</option>
      <option value="TRANSIT">Transit</option>
    </select>
    </div>
    <div id="map"></div>
    <script>
      function initMap() {
        var directionsDisplay = new google.maps.DirectionsRenderer;
        var directionsService = new google.maps.DirectionsService;
        var map = new google.maps.Map(document.getElementById('map'), {
          zoom: 14,
          center: {lat: 26.8653676, lng: 80.9440718}
        });
        directionsDisplay.setMap(map);

        calculateAndDisplayRoute(directionsService, directionsDisplay);
        document.getElementById('mode').addEventListener('change', function() {
          calculateAndDisplayRoute(directionsService, directionsDisplay);
        });
      }
    
var final_latitude=0;
var final_longitude=0;

     if (navigator.geolocation) {
                    navigator.geolocation.getCurrentPosition(showPosition, showError,{maximumAge:0});
                } else { 
                    x.innerHTML = "Geolocation is not supported by this browser.";
                }
                function showPosition(position) {
                    var lati=position.coords.latitude;
                    //alert(typeof lati);
                    final_latitude=lati;
                    var longi=position.coords.longitude;
                    //alert(typeof lati);
                    final_longitude=longi;
                    calculateAndDisplayRoute();
                }
                function showError(error) {
                    switch(error.code) {
                        case error.PERMISSION_DENIED:
                            x.innerHTML = "User denied the request for Geolocation."
                            break;
                        case error.POSITION_UNAVAILABLE:
                            x.innerHTML = "Location information is unavailable."
                            break;
                        case error.TIMEOUT:
                            x.innerHTML = "The request to get user location timed out."
                            break;
                        case error.UNKNOWN_ERROR:
                            x.innerHTML = "An unknown error occurred."
                            break;
                    }
                }
   
      function calculateAndDisplayRoute(directionsService, directionsDisplay) {

//alert(final_latitude);
//alert(typeof final_latitude);
//alert(final_longitude);


        var selectedMode = document.getElementById('mode').value;
        //var start = new google.maps.LatLng(26.856714, 80.9718676);
        //alert(typeof start);
        var start = {lat: final_latitude, lng: final_longitude};
       // alert(start);



        var end = new google.maps.LatLng(26.8466937, 80.946166);
        //alert(end);
        directionsService.route({
          //origin: {lat: 37.77, lng: -122.447},  // Haight.
          //destination: {lat: 37.768, lng: -122.511},  // Ocean Beach.


          origin: start,
          destination: end,



          // Note that Javascript allows us to access the constant
          // using square brackets and a string value as its
          // "property."
          travelMode: google.maps.TravelMode[selectedMode]
        }, function(response, status) {
          if (status == 'OK') {
            directionsDisplay.setDirections(response);
          } else {
            window.alert('Directions request failed due to ' + status);
          }
        });
      }
    </script>
    <script async defer
    src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDjiwZ1k6xJwDQqn1SFwaKr4N-yDnIyIUY&callback=initMap">
    </script>
  </body>
</html>
