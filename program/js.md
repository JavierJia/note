# Random Number
Math.random generate float from (0,1)

    Math.floor(Math.random()*1000)+1000

# A real sleep

    function pausecomp(millis)
    {
      var date = new Date();
      var curDate = null;
      do { curDate = new Date(); }
      while(curDate-date < millis);
    }

Otherwise using asynchronized 

    setTimeout( function(){}, 300)

# About 'this'
We need to transfer correct "this" object to other function to prevent point to hosts own 'this'

    FooClass{
        var _this = this;         
        $(window).on('beforeunload', function() { _this.close() });    
        this.connection.onmessage = function(evt) { _this.receive(evt) }
        this.connection.onopen = function() {
            _this.send({ action: 'join', user: username });
        }
    }

# Get geolocation by Google Map API

    function codeAddress(address) {
        geocoder.geocode( { 'address': address+ ',University California,Irvine','region': 'us'}, function(results, status) {
            if (status == google.maps.GeocoderStatus.OK) {
                console.log('address:'+address + results[0].geometry.location);
            } else {
                console.warn('warn:Geocode was not successful for the following reason: ' + status);
                return true;
            }
        });
    }

# Font color:
http://www.computerhope.com/htmcolor.htm
