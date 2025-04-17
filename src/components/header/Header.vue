<script setup>
import { ref } from "vue";

const originList = ref([
  {
    city: "New York",
    airport: "John F. Kennedy International Airport",
    code: "JFK",
    value: "JFK",
  },
  {
    city: "London",
    airport: "Heathrow Airport",
    code: "LHR",
    value: "LHR",
  },
  {
    city: "Tokyo",
    airport: "Haneda Airport",
    code: "HND",
    value: "HND",
  },
  {
    city: "Dubai",
    airport: "Dubai International Airport",
    code: "DXB",
    value: "DXB",
  },
  {
    city: "Paris",
    airport: "Charles de Gaulle Airport",
    code: "CDG",
    value: "CDG",
  },
  {
    city: "Singapore",
    airport: "Changi Airport",
    code: "SIN",
    value: "SIN",
  },
]);

const originPlaceholder = ref({
  city: "Origin",
  airport: "",
  code: "",
  value: "",
});

const destinationList = ref([
  {
    city: "Tokyo",
    airport: "Haneda Airport",
    code: "HND",
    value: "HND",
  },
  {
    city: "Dubai",
    airport: "Dubai International Airport",
    code: "DXB",
    value: "DXB",
  },
  {
    city: "Paris",
    airport: "Charles de Gaulle Airport",
    code: "CDG",
    value: "CDG",
  },
]);

const destinationPlaceholder = ref({
  city: "Destination",
  airport: "",
  code: "",
  value: "",
});

// Guest Menu visibility
const menu = ref(false)

// Guest data
const addGuest = ref([
  {
    title: 'Adults',
    description: 'Age 13 or above',
    value: 1,
  },
  {
    title: 'Children',
    description: 'Ages 2–12',
    value: 0,
  },
  {
    title: 'Infants',
    description: 'Under 2',
    value: 0,
  },
])

// Total guest count
const totalGuests = computed(() => {
  return addGuest.value.reduce((sum, item) => sum + item.value, 0)
})
</script>

<template>
  <div class="header">
    <div class="logo">
      <v-img
        src="/public/images/logo/logo.png"
        max-height="20"
        contain
        class="logo-img"
      ></v-img>
    </div>

    <!-- Origin -->
    <div class="transport-wrapper">
      <div class="transport-wrap">
        <v-select
          v-model="originPlaceholder"
          item-value="value"
          item-title="city"
          :items="originList"
          variant="plain"
          return-object
          density="compact"
        >
          <template #item="data">
            <v-list-item v-bind="data.props" class="custom-select-item">
              <template #title>
                <div class="select-item">
                  <h6>{{ data.item.raw.city }}</h6>
                  <div class="d-flex align-center justify-space-between">
                    <div class="select-item-content d-flex align-center mt-1">
                      <span class="mdi mdi-airplane air-icon"></span>
                      <span
                        class="select-text ml-2 text-truncate"
                        style="max-width: 200px"
                      >
                        {{ data.item.raw.airport }}
                      </span>
                    </div>
                    <span class="select-key-word">
                      {{ data.item.raw.code }}
                    </span>
                  </div>
                </div>
              </template>
            </v-list-item>
          </template>

          <template #selection="data">
            <div class="transport-place-container">
              <div class="transport-place">
                <div class="transport-title">From</div>
                <div class="transport-content">
                  <div class="d-flex align-center justify-space-between">
                    <h2>{{ data.item?.raw?.city }}</h2>
                    <div class="key-word" v-if="data.item.raw.code">
                      {{ data.item.raw.code }}
                    </div>
                  </div>
                  <p>{{ data.item.raw.airport || "Select Your Origin" }}</p>
                </div>
              </div>
            </div>
          </template>
        </v-select>
      </div>

      <!-- Reverse Trip -->
      <div class="reverse-trip">
        <v-btn
          class="reverse-btn"
          icon="mdi-autorenew"
          size="x-small"
          rounded="xl"
        ></v-btn>
      </div>

      <!-- Destination -->
      <div class="transport-wrap">
        <v-select
          v-model="destinationPlaceholder"
          item-value="value"
          item-title="city"
          :items="destinationList"
          variant="plain"
          return-object
          density="compact"
        >
          <template #item="data">
            <v-list-item v-bind="data.props" class="custom-select-item">
              <template #title>
                <div class="select-item">
                  <h6>{{ data.item.raw.city }}</h6>
                  <div class="d-flex align-center justify-space-between">
                    <div class="select-item-content d-flex align-center mt-1">
                      <span class="mdi mdi-airplane air-icon"></span>
                      <span
                        class="select-text ml-2 text-truncate"
                        style="max-width: 200px"
                      >
                        {{ data.item.raw.airport }}
                      </span>
                    </div>
                    <span class="select-key-word">
                      {{ data.item.raw.code }}
                    </span>
                  </div>
                </div>
              </template>
            </v-list-item>
          </template>

          <template #selection="data">
            <div class="transport-place-container">
              <div class="transport-place">
                <div class="transport-title">From</div>
                <div class="transport-content">
                  <div class="d-flex align-center justify-space-between">
                    <h2>{{ data.item?.raw?.city }}</h2>
                    <div class="key-word" v-if="data.item.raw.code">
                      {{ data.item.raw.code }}
                    </div>
                  </div>
                  <p>{{ data.item.raw.airport || "Select Your Origin" }}</p>
                </div>
              </div>
            </div>
          </template>
        </v-select>
      </div>
    </div>


    <!-- Guest -->
    <v-menu
      v-model="menu"
      :close-on-content-click="false"
      transition="scale-transition"
    >
      <template v-slot:activator="{ props }">
        <div class="add-guest" v-bind="props">
          <div class="guest-container">
            <div class="transport-title">Guests</div>
            <div class="guest-content">
              <h2>{{ totalGuests }}</h2>
              <span class="mdi mdi-chevron-down"></span>
            </div>
          </div>
        </div>
      </template>
      <v-card color="black" class="guest-plate" width="380">
        <div v-for="(item, index) in addGuest" :key="index" class="plate-item">
          <div class="d-flex justify-space-between align-center">
            <h3 class="text-white">{{ item.title }}</h3>
            <CounterPlate v-model:count="item.value" />
          </div>
          <p class="text-grey">{{ item.description }}</p>
        </div>

        <v-card-actions class="d-flex justify-end">
          <v-btn variant="text" size="small" @click="menu = false">
            Done
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-menu>

    <v-btn
      class="next-btn"
      icon="mdi-arrow-right"
      size="large"
      rounded="lg"
    ></v-btn>
  </div>
</template>

<style scoped>
.header {
  height: 85px;
  width: 95%;
  border: 1px solid #a6acb53f;
  background-color: #000000;
  position: fixed;
  top: 20px;
  left: 50%;
  border-radius: 16px;
  transform: translateX(-50%);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
}
.logo {
  border-right: 1px solid #a6acb541;
  height: 100%;
  display: flex;
  align-items: center;
  padding-right: 20px;
}
.logo-img {
  width: 100px;
}
.transport-wrapper {
  display: flex;
  align-items: center;
  height: 100%;
}
.transport-place-container {
  height: 100%;
  width: 260px;
}
.transport-place {
  width: 100%;
  height: 100%;
}
.transport-title {
  font-size: 12px;
  color: #c0bfbf;
  line-height: 18px;
}
.transport-content {
  color: #fff;
}
.transport-content h2 {
  font-weight: 400;
  font-size: 24px;
}
.transport-content p {
  font-size: 12px;
  color: #a4a3a3;
  line-height: 16px;
}
.transport-content .key-word {
  font-size: 22px;
  color: #a4a3a3;
}
.select-key-word {
  font-size: 16px;
  color: #a4a3a3;
}
.transport-content .key-word span {
  color: #fff;
  font-size: 26px;
}
::v-deep(.v-field) {
  align-items: center !important;
}
::v-deep(.mdi-menu-down) {
  color: #ffffff;
}

.custom-select-item {
  border-top: 1px solid #c3c3c333;
  transition: background-color 0.3s ease;
}

.custom-select-item:hover {
  background-color: #cee8f414;
}

.select-item-content {
  position: relative;
  left: 0;
  transition: left 0.3s ease;
}

.custom-select-item:hover .select-item-content {
  left: 10px;
}

.air-icon {
  color: #7184a2;
  font-size: 22px;
}

.select-item {
  padding: 10px 0;
}

.select-item h6 {
  font-size: 12px;
  color: #a4a3a3;
  line-height: 16px;
  font-weight: 400;
}
.transport-wrap {
  height: 100%;
}
.select-text {
  font-weight: 400;
  font-size: 20px;
}
.next-btn {
  background-color: #657ca2;
  color: #fff;
  font-size: 24px;
}
.reverse-trip {
  height: 100%;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}
.reverse-btn {
  margin: 0 20px;
}

.add-guest {
  cursor: pointer;
}

.guest-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.transport-title {
  font-size: 16px;
  font-weight: 500;
  color: #aaa;
}

.guest-content {
  display: flex;
  align-items: center;
  gap: 4px;
}

.guest-content h2 {
  margin: 0;
  color: #fff;
}

.guest-content span {
  color: #aaa;
}

.guest-plate {
  padding: 16px;
  background-color: #000;
}

.plate-item {
  margin-bottom: 12px;
}
</style>
