
<<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div id="map"></div>
  </div>
</template>

<style>
  /* Always set the map height explicitly to define the size of the div
   * element that contains the map. */
  #map {
    height: 500px;
  }
</style>

<script>
/* global google */
export default {
  data: function() {
    return {
      places: [
        { 
          lat: 37.773972, 
          lng: -122.431297, 
          description: "This is lower haight" 
        },
        { 
          lat: -25.363, 
          lng: 131.044, 
          description: "This is somewhere in Australia!" 
        },
        { 
          lat: -33.8675, 
          lng: 151.207, 
          description: "This is Sydney!" 
        },
        { 
          lat: 20, 
          lng: -105, 
          description: "This is Cacaluta!" 
        }
      ]
    };
  },
  methods: {},
  mounted: function() {
    var sanFran = { lat: 37.773972, lng: -122.431297, description: "This is a marker!" };
    var map = new google.maps.Map(document.getElementById('map'), {
      center: sanFran,
      zoom: 4
    });
    this.places.forEach(function(place){
      var infowindow = new google.maps.InfoWindow({
        content: place.description
      });
      var marker = new google.maps.Marker({
        position: place,
        map: map
      });
      marker.addListener('click', function() {
        infowindow.open(map, marker);
      });
    });
  },
  computed: {}
};
