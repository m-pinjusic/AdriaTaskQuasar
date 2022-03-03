<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated virtual-scroll>
      <q-toolbar>
        <q-btn
          size="lg"
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          <div class="q-pa-md">
            Kvaliteta zraka - Rijeka:
            <div>
              <div class="row items-center">
                <AQdetails
                  v-for="data in dataOpenAQ"
                  :key="data.title"
                  v-bind="data"
                >
                </AQdetails>
              </div>
            </div>
          </div>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list padding class="menu-list">
        <q-item clickable v-ripple to="/">
          <q-item-section>
            <q-item-label>Home</q-item-label>
          </q-item-section>
        </q-item>

        <q-separator></q-separator>

        <DrawerControllers
          v-for="controller in controllersData"
          :key="controller.id"
          v-bind="controller"
        />
        <q-item-section class="absolute-bottom q-ma-lg">
          <q-item-label>Današnji datum: {{ this.formattedDate }}</q-item-label>
          <q-item-label>Sljedeći blagdan: {{ this.nextHoliday }}</q-item-label>
        </q-item-section>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, onMounted, ref } from "vue";
import { api, axios } from "boot/axios";
import DrawerControllers from "src/components/DrawerControllers.vue";
import AQdetails from "components/AQdetails.vue";
import { date } from "quasar";

let timeStamp = new Date(Date.now());
//let timeStamp = new Date(2022, 4, 19);

let apiCalendarRequest = "";

export default defineComponent({
  name: "MainLayout",

  components: {
    DrawerControllers,
    AQdetails,
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      onClick() {
        // console.log('Clicked on a QChip')
      },
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
  data() {
    return {
      dataOpenAQ: [],
      controllersData: [],
      holidaysInCurrentMonth: [],
      nextHoliday: "",
      foundMonth: false,
      counter: 0,

      formattedDate: date.formatDate(timeStamp, "DD.MM.YYYY."),
    };
  },
  methods: {
    async getHolidayApi() {
      while (this.counter != 2) {
        this.counter = this.counter + 1;
        apiCalendarRequest =
          "https://calendarific.com/api/v2/holidays?&api_key=" +
          process.env.apiCalendar +
          "&country=HR&type=national&year=" +
          timeStamp.getFullYear() +
          "&month=" +
          //stavi na plus jedan
          (timeStamp.getMonth() + this.counter);
        await axios(apiCalendarRequest).then((response) => {
          if (response.data.response.holidays.length != 0) {
            this.foundMonth = true;
            this.nextHoliday = date.formatDate(
              new Date(
                response.data.response.holidays.find(
                  (element) =>
                    element.date.iso > date.formatDate(timeStamp, "YYYY-MM-DD")
                ).date.iso
              ),
              "DD.MM.YYYY."
            );
            console.log(
              "Svi blagdani u",
              timeStamp.getMonth() + this.counter,
              ". mjesecu",
              response.data.response.holidays
            );
            console.log("Sljedeci blagdan:", this.nextHoliday);
          } else {
            console.log(timeStamp.getMonth() + 1, "mjesec je prazan");
          }
        });
      }
    },
    async getOpenAQdata() {
      await axios(
        "https://docs.openaq.org/v2/locations/2982?limit=1&page=1&offset=0&sort=asc&radius=1000&order_by=lastUpdated&dumpRaw=false"
      ).then((response) => {
        response.data.results[0].parameters.map((x) => {
          this.dataOpenAQ.push({
            name: x.parameter,
            value: x.lastValue,
            title: x.displayName,
            averageValue: x.average,
            lastDate: x.lastUpdated,
            unit: x.unit,
          });
        });
        console.log(
          "Zadnji podaci o kvaliteti zraka u Rijeci:",
          JSON.parse(JSON.stringify(this.dataOpenAQ))
        );
        // console.log(this.dataOpenAQ);
      });
    },
    async getRoomStatusJSON() {
      axios("./room_status.json").then((response) => {
        this.controllersData = response.data.controllers;
        //console.log(this.controllersData[3]);
        this.$q.sessionStorage.set(
          "sessionControllerData",
          JSON.parse(JSON.stringify(response.data.controllers))
        );
      });
    },
  },

  mounted() {
    this.getOpenAQdata();
    this.getRoomStatusJSON();
    this.getHolidayApi();
  },
});
</script>
