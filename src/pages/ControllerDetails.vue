<template>
  <q-page class="q-pa-sm">
    <q-card>
      <q-card-section style="margin-left: 2%">
        <div class="text-h4 text-weight-bold text-primary">
          Zona: {{ this.basicControllersData.zone }}
        </div>
        <div class="text-h5 text-weight-bold">
          Naziv:
          {{ this.basicControllersData.name }}
        </div>
      </q-card-section>

      <q-separator></q-separator>
      <div class="flex" style="display: flex">
        <div class="q-mb-none" style="margin-left: 5%">
          <div class="q-mt-lg text-h5">Osnovni podaci:</div>

          <q-card-section class="q-mb-xl q-pl-none">
            <div class="q-pt-xs" style="max-width: 350px">
              <q-list bordered separator>
                <q-item>
                  <q-item-section>
                    <q-item-label overline>Adresa</q-item-label>
                    <q-item-label>{{
                      this.basicControllersData.address || "Empty"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item>
                  <q-item-section>
                    <q-item-label overline
                      >Lokalna naredba - grijanje/hlađenje</q-item-label
                    >
                    <q-item-label>{{
                      this.basicControllersData.LocalCommandHeatingCooling
                        ? "True"
                        : "False"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item>
                  <q-item-section>
                    <q-item-label overline
                      >Lokalna naredba - ploča blokirana</q-item-label
                    >
                    <q-item-label>{{
                      this.basicControllersData.LocalCommandPanelBlocked
                        ? "True"
                        : "False"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item>
                  <q-item-section>
                    <q-item-label overline>IP Adresa</q-item-label>
                    <q-item-label>{{
                      this.basicControllersData.ipAddress || "Empty"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item>
                  <q-item-section>
                    <q-item-label overline>IP Port</q-item-label>
                    <q-item-label>{{
                      this.basicControllersData.ipPort || "Empty"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item>
                  <q-item-section>
                    <q-item-label overline>Objekt</q-item-label>
                    <q-item-label>{{
                      this.basicControllersData.object || "Empty"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item>
                  <q-item-section>
                    <q-item-label overline>Sub-objekt</q-item-label>
                    <q-item-label>{{
                      this.basicControllersData.subObject || "Empty"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item>
                  <q-item-section>
                    <q-item-label overline>Sub-zona</q-item-label>
                    <q-item-label>{{
                      this.basicControllersData.subZone || "Empty"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>
              </q-list>
            </div>
          </q-card-section>
        </div>

        <div class="q-mb-none" style="margin-left: 5%">
          <div class="q-mt-lg text-h5">Svojstva:</div>

          <q-card-section class="q-mb-xl q-pl-none">
            <div class="q-pt-xs" style="max-width: 350px">
              <q-list bordered separator>
                <q-item>
                  <q-item-section>
                    <q-item-label overline>{{
                      this.propertiesControllerDataTempRoomSetName
                    }}</q-item-label>
                    <q-item-label>{{
                      this.propertiesControllerDataTempRoomSet.Value || "Empty"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label overline>{{
                      propertiesControllerDataTempRoomCurrentName
                    }}</q-item-label>
                    <q-item-label>{{
                      this.propertiesControllerDataTempRoomCurrent.Value ||
                      "Empty"
                    }}</q-item-label>
                  </q-item-section>
                </q-item>
                <q-item v-if="this.propertiesControllerDataDND.Value == 1">
                  <q-item-section>
                    <q-item-label>{{
                      this.propertiesControllerDataDND.Value == 1 ? "DND" : ""
                    }}</q-item-label>
                  </q-item-section>
                </q-item>
                <q-item
                  v-if="this.propertiesControllerDataDeopenedCard.Value == 1"
                >
                  <q-item-section>
                    <q-item-label>{{
                      this.propertiesControllerDataDeopenedCard.Value == 1
                        ? "Occupied"
                        : ""
                    }}</q-item-label>
                  </q-item-section>
                </q-item>
              </q-list>
            </div>
          </q-card-section>
        </div>
        <div style="margin-left: 5%" class="break q-mt-md q-mb-lg q-gutter-sm">
          <QRgenerator
            colorProp="primary"
            :flatProp="false"
            sizeProp="lg"
            :controllerName="this.basicControllersData.name + ''"
          />
          <q-btn
            size="lg"
            label="Postavke"
            color="primary"
            @click="seamless = true"
          />
        </div>
      </div>
    </q-card>

    <q-dialog v-model="seamless">
      <q-card style="width: 350px">
        <q-card-section class="row items-center no-wrap">
          <q-list>
            <q-item>
              <q-item-section>
                <q-item-label overline>{{
                  this.basicControllersData.settings[0].settingName
                }}</q-item-label>
                <q-item-label>{{
                  this.basicControllersData.settings[0].settingValue || "Empty"
                }}</q-item-label>
              </q-item-section>
            </q-item>

            <q-item>
              <q-item-section>
                <q-item-label overline>{{
                  this.basicControllersData.settings[1].settingName
                }}</q-item-label>
                <q-item-label>{{
                  this.basicControllersData.settings[1].settingValue || "Empty"
                }}</q-item-label>
              </q-item-section>
            </q-item>

            <q-item>
              <q-item-section>
                <q-item-label overline>{{
                  this.basicControllersData.settings[2].settingName
                }}</q-item-label>
                <q-item-label>{{
                  this.basicControllersData.settings[2].settingValue || "Empty"
                }}</q-item-label>
              </q-item-section>
            </q-item>

            <q-item>
              <q-item-section>
                <q-item-label overline>{{
                  this.basicControllersData.settings[3].settingName
                }}</q-item-label>
                <q-item-label>{{
                  this.basicControllersData.settings[3].settingValue || "Empty"
                }}</q-item-label>
              </q-item-section>
            </q-item>

            <q-item>
              <q-item-section>
                <q-item-label overline>{{
                  this.basicControllersData.settings[4].settingName
                }}</q-item-label>
                <q-item-label>{{
                  this.basicControllersData.settings[4].settingValue || "Empty"
                }}</q-item-label>
              </q-item-section>
            </q-item>

            <q-item>
              <q-item-section>
                <q-item-label overline>{{
                  this.basicControllersData.settings[5].settingName
                }}</q-item-label>
                <q-item-label>{{
                  this.basicControllersData.settings[5].settingValue || "Empty"
                }}</q-item-label>
              </q-item-section>
            </q-item>

            <q-item>
              <q-item-section>
                <q-item-label overline>{{
                  this.basicControllersData.settings[6].settingName
                }}</q-item-label>
                <q-item-label>{{
                  this.basicControllersData.settings[6].settingValue || "Empty"
                }}</q-item-label>
              </q-item-section>
            </q-item>

            <q-item>
              <q-item-section>
                <q-item-label overline>{{
                  this.basicControllersData.settings[7].settingName
                }}</q-item-label>
                <q-item-label>{{
                  this.basicControllersData.settings[7].settingValue || "Empty"
                }}</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
          <q-btn
            class="absolute-top-right q-ma-xs"
            flat
            round
            icon="close"
            v-close-popup
          />
        </q-card-section>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import routes from "src/router/routes";
import QRgenerator from "components/QRgenerator.vue";
import { ref } from "vue";

export default defineComponent({
  setup() {
    return {
      seamless: ref(false),
    };
  },
  name: "ControllerDetails",
  components: {
    QRgenerator,
  },
  data() {
    return {
      basicControllersData: [],
      propertiesControllerDataTempRoomSet: [],
      propertiesControllerDataTempRoomCurrent: [],
      propertiesControllerDataDND: [],
      propertiesControllerDataDeopenedCard: [],
      propertiesControllerDataTempRoomSetName: "",
      propertiesControllerDataTempRoomCurrentName: "",
    };
  },
  methods: {
    getData() {
      this.basicControllersData = this.$q.sessionStorage
        .getItem("sessionControllerData")
        .find((element) => element.id == this.$route.params.id);

      console.log("Detaljni podaci o controlleru:", this.basicControllersData);

      this.propertiesControllerDataTempRoomSet =
        this.basicControllersData.properties.find(
          (element) => element.id == 11
        );
      this.$q.localStorage.set(
        "localControllerDataTempRoomSetValue" + this.$route.params.id,
        this.propertiesControllerDataTempRoomSet.Value
      );
      this.propertiesControllerDataTempRoomCurrent =
        this.basicControllersData.properties.find(
          (element) => element.id == 12
        );
      this.propertiesControllerDataDND =
        this.basicControllersData.properties.find(
          (element) => element.id == 27
        );
      this.propertiesControllerDataDeopenedCard =
        this.basicControllersData.properties.find(
          (element) => element.id == 48
        );

      //for removing "in room" na desc
      this.propertiesControllerDataTempRoomSetName =
        this.propertiesControllerDataTempRoomSet.description.replace(
          " in room",
          ""
        );
      this.propertiesControllerDataTempRoomCurrentName =
        this.propertiesControllerDataTempRoomCurrent.description.replace(
          " in room",
          ""
        );

      console.log("DND podatak:", this.propertiesControllerDataDND.description);
      console.log("DND value:", this.propertiesControllerDataDND.Value);
      console.log(
        "Card podatak:",
        this.propertiesControllerDataDeopenedCard.description
      );
      console.log(
        "Card value:",
        this.propertiesControllerDataDeopenedCard.Value
      );
    },
    openSettings() {},
  },
  async mounted() {
    await this.getData();
    console.log(
      "GET -LOCAL TEMP ROOM SET:",
      this.$q.localStorage.getItem(
        "localControllerDataTempRoomSetValue" + this.$route.params.id
      )
    );
  },
  updated() {
    this.getData();
    console.log("updated");
  },
});
</script>
