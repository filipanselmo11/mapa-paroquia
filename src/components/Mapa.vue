
<script lang="ts">
import L from 'leaflet';
import 'leaflet/dist/leaflet.css';
import { defineComponent } from 'vue';
export default defineComponent({
    name: 'Mapa',
    data() {
        return {
            map: null,
            tileLayer: null,
            marker: null,
            locations: [
                ["location_1", -0.13058287994446194, -67.08370578614496, "Paróquia São Gabriel Arcanjo"],
                ["location_2", -0.13544650623680196, -67.07956956457983, "Paróquia São Gabriel Arcanjo"],
                ["location_3", -0.13062188176745562, -67.08706235018404, "Paróquia São Gabriel Arcanjo"],
                ["location_4", -0.13147398172201985, -67.08094205420043, "Paróquia São Gabriel Arcanjo"],
                ["location_5", -0.1356705274939071, -67.07584574747234, "Paróquia São Gabriel Arcanjo"],
                ["location_6", -0.15779952127405997, -66.93068504333498, "Paróquia São Gabriel Arcanjo"],
                ["location_7", -0.13883100275962731, -66.91682338714601, "Paróquia São Gabriel Arcanjo"],
                ["location_8", -0.18110245112288664, -66.850004196167, "Paróquia São Gabriel Arcanjo"],
                ["location_9", -0.2094264135464264, -66.79224014282228, "Paróquia São Gabriel Arcanjo"],
                ["location_10", -0.21586367084460562, -66.84442520141603, "Paróquia São Gabriel Arcanjo"],
                ["location_11", -0.245045868554101, -67.01668739318849, "Paróquia São Gabriel Arcanjo"],
                ["location_12", -0.3464963773330212, -66.54599189758302, "Paróquia São Gabriel Arcanjo"],
                ["location_13", -0.4212532238045312, -66.409649848938, "Paróquia São Gabriel Arcanjo"],
                ["location_14", -0.37344718942813093, -66.28798830928369, "Paróquia São Gabriel Arcanjo"],
                ["location_15", -0.3779956100442933, -66.27279281616212, "Paróquia São Gabriel Arcanjo"],
                ["location_16", -0.26236204012862363, -66.69782638549806, "Paróquia São Gabriel Arcanjo"],
            ],
        }
    },

    mounted() {
        this.initMap();
    },

    methods: {
        initMap() {
            this.map = L.map("map").setView([-0.1306783854436242, -67.08850595028112], 16);
            this.tileLayer = L.tileLayer(
                "https://cartodb-basemaps-{s}.global.ssl.fastly.net/rastertiles/voyager/{z}/{x}/{y}.png",
                {
                    maxZoom: 18,
                    atribution:
                        '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, &copy; <a href="https://carto.com/attribution">CARTO</a>',
                }
            );
            this.tileLayer.addTo(this.map);
            for (var i = 0; i < this.locations.length; i++) {
                this.marker = new L.marker([this.locations[i][1], this.locations[i][2]])
                    .bindPopup(this.locations[i][3])
                    .on('mouseover', function(e:any) {
                        e.target.openPopup();
                        // this.marker.openPopup();
                    })
                    .on('mouseout', function(e:any) {
                        e.target.closePopup();
                    })
                    .addTo(this.map);
            }

            this.map.on('click', function(e:any){ console.log(e.latlng)});
            // this.marker = L.marker([-0.12900469134855577, -67.08378526242971]).addTo(this.map);
        }

    },
});
</script>


<template>
    <div id="map"></div>
</template>

<style scoped>
#map {
    height: 900px;
}
</style>