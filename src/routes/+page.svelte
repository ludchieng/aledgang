<script lang="ts">
  import L from 'leaflet';
  let map: L.Map | null = null;

  function leaflet(container: HTMLDivElement) {
    map = L.map(container, {
      preferCanvas: true,
      attributionControl: false,
      zoomControl: false,
    }).setView([48.862, 2.343], 13);

    L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}{r}.png', {
      maxZoom: 21,
      maxNativeZoom: 19,
    }).addTo(map);

    return {
      destroy: () => {
        map && map.remove();
        map = null;
      },
    };
  }
</script>

<svelte:window on:resize={() => map && map.invalidateSize()} />

<div class="map" use:leaflet />

<style>
  @import 'leaflet/dist/leaflet.css';

  .map {
    height: 100%;
    width: 100%;
  }
</style>
