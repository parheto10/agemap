<template>
  <div>
    <l-map :center="center" :zoom="zoom" class="map" @update:center="centerUpdated" @update:zoom="zoomUpdated">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
      <l-marker v-for="chambre in chambres" :key="chambre.id" :lat-lng="[chambre.latitude, chambre.longitude]">
        <l-popup>
          <table class="table table-striped table-bordered">
            <thead style="align-items: center">
            <tr>
              <th scope="col" class="center">ID</th>
              <th scope="col" class="center">INFORMATIONS</th>
            </tr>
            </thead>
            <tbody style="align-items: center">
            <tr>
              <th scope="col"><b>VILLE :</b></th>
              <td class="text-uppercase"><strong>{{ chambre.ville }}</strong></td>
            </tr>
            <tr>
              <th scope="col"><b>COMMUNE :</b></th>
              <td class="text-uppercase"><strong>{{ chambre.commune }}</strong></td>
            </tr>
            <tr>
              <th scope="col"><b>CHAMBRE :</b></th>
              <td class="text-uppercase"><strong>{{chambre.libelle}}</strong></td>
            </tr>
            <tr>
              <th scope="col"><b>CONCESSONNAIRE :</b></th>
                <td class="text-uppercase"><strong>{{chambre.concessionnaire}}</strong></td>
            </tr>
            <tr>
              <th scope="col"><b>TYPE EQUIPEMENT :</b></th>
              <td class="text-uppercase">{{chambre.type_equipement}}</td>
            </tr>
            <tr>
              <th scope="col"><b>PROFONDEUR CABLE : </b></th>
              <td class="text-uppercase">{{chambre.profondeur_cable}} (M)</td>
            </tr>
            <tr>
              <th scope="col"><b>COORDONNEES :</b></th>
              <td class="text-uppercase">({{chambre.latitude}}; {{chambre.longitude}})</td>
            </tr>
            <tr>
              <th scope="col"><b>CHAMBRE PROCHE :</b></th>
              <td class="text-uppercase"><strong>{{ chambre.chbre_proche.libelle}}</strong></td>
            </tr>
            <tr>
              <th scope="col"><b>DSTCE CHAMBRE PROCHE</b></th>
              <td class="text-uppercase">{{chambre.dtce_chambre_proche}} (M)</td>
            </tr>
            </tbody>
          </table>
        </l-popup>
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import axios from "axios";
import L from 'leaflet';
import { LMap, LTileLayer, LMarker, LPopup } from 'vue2-leaflet';
import "leaflet/dist/leaflet.css";
import { Icon } from 'leaflet';

delete Icon.Default.prototype._getIconUrl;
Icon.Default.mergeOptions({
  iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),
  iconUrl: require('leaflet/dist/images/marker-icon.png'),
  shadowUrl: require('leaflet/dist/images/marker-shadow.png'),
});

export default {
  name: "Map",
  components : {
    LMap,
    LTileLayer,
    LMarker,
    // LIcon,
    LPopup
  },
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      center: [5.344686014173548, -3.9484254556761504],
      zoom: 15,
      attribution: '&copy; <a target="_blank" href="https://agromap10.pythonanywhere.com/">AGEROUTE-MAP (c) 2021</a>',
      chambres: [
        {
          "id": 6,
          "ville": "ABIDJAN",
          "commune": "COCODY",
          "libelle": "AMBASSADE DE CHINE",
          "type_equipement": "FO/PAIRES DE CUIVRE",
          "profondeur_cable": "1.20",
          "latitude": "5.3313167",
          "longitude": "-3.9403867",
          "concessionnaire": "ORANGE CI",
          "chbre_proche": {
            "ville": "",
            "commune": "",
            "libelle": "",
            "type_equipement": "",
            "profondeur_cable": null,
            "latitude": "",
            "longitude": "",
            "concessionnaire": "",
            "chbre_proche": null,
            "dtce_chambre_proche": null
          },
          "dtce_chambre_proche": null
        },
        {
          "id": 4,
          "ville": "ABIDJAN",
          "commune": "COCODY",
          "libelle": "AXE AMBASSADE CHINE1",
          "type_equipement": "FO/PAIRES DE CUIVRE",
          "profondeur_cable": "1.00",
          "latitude": "5.3438454",
          "longitude": "-3.9453229",
          "concessionnaire": "ORANGE CI",
          "chbre_proche": {
            "id": 5,
            "ville": "ABIDJAN",
            "commune": "COCODY",
            "libelle": "AXE AMBASSADE CHINE2",
            "type_equipement": "FO",
            "profondeur_cable": "2.00",
            "latitude": "5.3412008",
            "longitude": "-3.9451241",
            "concessionnaire": "ORANGE CI",
            "chbre_proche": {
              "id": 6,
              "ville": "ABIDJAN",
              "commune": "COCODY",
              "libelle": "AMBASSADE DE CHINE",
              "type_equipement": "FO/PAIRES DE CUIVRE",
              "profondeur_cable": "1.20",
              "latitude": "5.3313167",
              "longitude": "-3.9403867",
              "concessionnaire": "ORANGE CI",
              "chbre_proche": {
                "ville": "",
                "commune": "",
                "libelle": "",
                "type_equipement": "",
                "profondeur_cable": null,
                "latitude": "",
                "longitude": "",
                "concessionnaire": "",
                "chbre_proche": null,
                "dtce_chambre_proche": null
              },
              "dtce_chambre_proche": null
            },
            "dtce_chambre_proche": "1.20"
          },
          "dtce_chambre_proche": "379.00"
        },
        {
          "id": 5,
          "ville": "ABIDJAN",
          "commune": "COCODY",
          "libelle": "AXE AMBASSADE CHINE2",
          "type_equipement": "FO",
          "profondeur_cable": "2.00",
          "latitude": "5.3412008",
          "longitude": "-3.9451241",
          "concessionnaire": "ORANGE CI",
          "chbre_proche": {
            "id": 6,
            "ville": "ABIDJAN",
            "commune": "COCODY",
            "libelle": "AMBASSADE DE CHINE",
            "type_equipement": "FO/PAIRES DE CUIVRE",
            "profondeur_cable": "1.20",
            "latitude": "5.3313167",
            "longitude": "-3.9403867",
            "concessionnaire": "ORANGE CI",
            "chbre_proche": {
              "ville": "",
              "commune": "",
              "libelle": "",
              "type_equipement": "",
              "profondeur_cable": null,
              "latitude": "",
              "longitude": "",
              "concessionnaire": "",
              "chbre_proche": null,
              "dtce_chambre_proche": null
            },
            "dtce_chambre_proche": null
          },
          "dtce_chambre_proche": "1.20"
        },
        {
          "id": 3,
          "ville": "ABIDJAN",
          "commune": "COCODY",
          "libelle": "EN FACE DE LA PHARMACIE",
          "type_equipement": "FO/PAIRES DE CUIVRE",
          "profondeur_cable": "1.20",
          "latitude": "5.3461898",
          "longitude": "-3.9454624",
          "concessionnaire": "ORANGE CI",
          "chbre_proche": {
            "id": 4,
            "ville": "ABIDJAN",
            "commune": "COCODY",
            "libelle": "AXE AMBASSADE CHINE1",
            "type_equipement": "FO/PAIRES DE CUIVRE",
            "profondeur_cable": "1.00",
            "latitude": "5.3438454",
            "longitude": "-3.9453229",
            "concessionnaire": "ORANGE CI",
            "chbre_proche": {
              "id": 5,
              "ville": "ABIDJAN",
              "commune": "COCODY",
              "libelle": "AXE AMBASSADE CHINE2",
              "type_equipement": "FO",
              "profondeur_cable": "2.00",
              "latitude": "5.3412008",
              "longitude": "-3.9451241",
              "concessionnaire": "ORANGE CI",
              "chbre_proche": {
                "id": 6,
                "ville": "ABIDJAN",
                "commune": "COCODY",
                "libelle": "AMBASSADE DE CHINE",
                "type_equipement": "FO/PAIRES DE CUIVRE",
                "profondeur_cable": "1.20",
                "latitude": "5.3313167",
                "longitude": "-3.9403867",
                "concessionnaire": "ORANGE CI",
                "chbre_proche": {
                  "ville": "",
                  "commune": "",
                  "libelle": "",
                  "type_equipement": "",
                  "profondeur_cable": null,
                  "latitude": "",
                  "longitude": "",
                  "concessionnaire": "",
                  "chbre_proche": null,
                  "dtce_chambre_proche": null
                },
                "dtce_chambre_proche": null
              },
              "dtce_chambre_proche": "1.20"
            },
            "dtce_chambre_proche": "379.00"
          },
          "dtce_chambre_proche": "281.00"
        },
        {
          "id": 2,
          "ville": "ABIDJAN",
          "commune": "COCODY",
          "libelle": "PHARMACIE SYNACASSI",
          "type_equipement": "FO",
          "profondeur_cable": "1.20",
          "latitude": "5.3464695",
          "longitude": "-3.9454936",
          "concessionnaire": "ORANGE CI",
          "chbre_proche": {
            "id": 3,
            "ville": "ABIDJAN",
            "commune": "COCODY",
            "libelle": "EN FACE DE LA PHARMACIE",
            "type_equipement": "FO/PAIRES DE CUIVRE",
            "profondeur_cable": "1.20",
            "latitude": "5.3461898",
            "longitude": "-3.9454624",
            "concessionnaire": "ORANGE CI",
            "chbre_proche": {
              "id": 4,
              "ville": "ABIDJAN",
              "commune": "COCODY",
              "libelle": "AXE AMBASSADE CHINE1",
              "type_equipement": "FO/PAIRES DE CUIVRE",
              "profondeur_cable": "1.00",
              "latitude": "5.3438454",
              "longitude": "-3.9453229",
              "concessionnaire": "ORANGE CI",
              "chbre_proche": {
                "id": 5,
                "ville": "ABIDJAN",
                "commune": "COCODY",
                "libelle": "AXE AMBASSADE CHINE2",
                "type_equipement": "FO",
                "profondeur_cable": "2.00",
                "latitude": "5.3412008",
                "longitude": "-3.9451241",
                "concessionnaire": "ORANGE CI",
                "chbre_proche": {
                  "id": 6,
                  "ville": "ABIDJAN",
                  "commune": "COCODY",
                  "libelle": "AMBASSADE DE CHINE",
                  "type_equipement": "FO/PAIRES DE CUIVRE",
                  "profondeur_cable": "1.20",
                  "latitude": "5.3313167",
                  "longitude": "-3.9403867",
                  "concessionnaire": "ORANGE CI",
                  "chbre_proche": {
                    "ville": "",
                    "commune": "",
                    "libelle": "",
                    "type_equipement": "",
                    "profondeur_cable": null,
                    "latitude": "",
                    "longitude": "",
                    "concessionnaire": "",
                    "chbre_proche": null,
                    "dtce_chambre_proche": null
                  },
                  "dtce_chambre_proche": null
                },
                "dtce_chambre_proche": "1.20"
              },
              "dtce_chambre_proche": "379.00"
            },
            "dtce_chambre_proche": "281.00"
          },
          "dtce_chambre_proche": "2.00"
        },
        {
          "id": 1,
          "ville": "ABIDJAN",
          "commune": "COCODY",
          "libelle": "ROND POINT JACQUES PREVERT",
          "type_equipement": "FO/PAIRES DE CUIVRE",
          "profondeur_cable": "2.00",
          "latitude": "5.3456370",
          "longitude": "-3.9493724",
          "concessionnaire": "ORANGE CI",
          "chbre_proche": {
            "id": 2,
            "ville": "ABIDJAN",
            "commune": "COCODY",
            "libelle": "PHARMACIE SYNACASSI",
            "type_equipement": "FO",
            "profondeur_cable": "1.20",
            "latitude": "5.3464695",
            "longitude": "-3.9454936",
            "concessionnaire": "ORANGE CI",
            "chbre_proche": {
              "id": 3,
              "ville": "ABIDJAN",
              "commune": "COCODY",
              "libelle": "EN FACE DE LA PHARMACIE",
              "type_equipement": "FO/PAIRES DE CUIVRE",
              "profondeur_cable": "1.20",
              "latitude": "5.3461898",
              "longitude": "-3.9454624",
              "concessionnaire": "ORANGE CI",
              "chbre_proche": {
                "id": 4,
                "ville": "ABIDJAN",
                "commune": "COCODY",
                "libelle": "AXE AMBASSADE CHINE1",
                "type_equipement": "FO/PAIRES DE CUIVRE",
                "profondeur_cable": "1.00",
                "latitude": "5.3438454",
                "longitude": "-3.9453229",
                "concessionnaire": "ORANGE CI",
                "chbre_proche": {
                  "id": 5,
                  "ville": "ABIDJAN",
                  "commune": "COCODY",
                  "libelle": "AXE AMBASSADE CHINE2",
                  "type_equipement": "FO",
                  "profondeur_cable": "2.00",
                  "latitude": "5.3412008",
                  "longitude": "-3.9451241",
                  "concessionnaire": "ORANGE CI",
                  "chbre_proche": {
                    "id": 6,
                    "ville": "ABIDJAN",
                    "commune": "COCODY",
                    "libelle": "AMBASSADE DE CHINE",
                    "type_equipement": "FO/PAIRES DE CUIVRE",
                    "profondeur_cable": "1.20",
                    "latitude": "5.3313167",
                    "longitude": "-3.9403867",
                    "concessionnaire": "ORANGE CI",
                    "chbre_proche": {
                      "ville": "",
                      "commune": "",
                      "libelle": "",
                      "type_equipement": "",
                      "profondeur_cable": null,
                      "latitude": "",
                      "longitude": "",
                      "concessionnaire": "",
                      "chbre_proche": null,
                      "dtce_chambre_proche": null
                    },
                    "dtce_chambre_proche": null
                  },
                  "dtce_chambre_proche": "1.20"
                },
                "dtce_chambre_proche": "379.00"
              },
              "dtce_chambre_proche": "281.00"
            },
            "dtce_chambre_proche": "2.00"
          },
          "dtce_chambre_proche": "400.00"
        }
      ]
    }
  },
  methods : {
    centerUpdated(center) {
      this.center = center;
      console.log('CENTER')
      console.log(this.center)
    },
    zoomUpdated(zoom) {
      this.zoom = zoom;
      console.log('zoom')
      console.log(this.zoom)
    }
  },
}
</script>

<style scoped>
.map {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.tree-icon {
  width: 32px;
}
</style>