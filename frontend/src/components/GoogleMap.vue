<script setup>
import { onMounted, ref } from 'vue';
import { Loader } from '@googlemaps/js-api-loader';
import config from '../config.json'

// mapElementをrefで作成する
const mapElement = ref(null);
const apiKey = config.apiKey;
onMounted(() => {
  const loader = new Loader({
    apiKey: apiKey,
    version: 'weekly',
  });

  loader.load().then(() => {
    const mapOptions = {
      center: { lat: 35.658581, lng: 139.745433 },
      zoom: 18,
    };
    // mapElement.valueを使用して要素にアクセスする
    new google.maps.Map(mapElement.value, mapOptions);
  }).catch(e => {
    console.error('Error loading Google Maps API', e);
  });
});
</script>

<template>
  <!-- mapElementを使用する -->
  <div ref="mapElement" style="width: 100%; height: 100vh;"></div>
</template>