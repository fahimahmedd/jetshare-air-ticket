<script setup>
const seats = reactive([
  { id: 1, class:'seat-1', selected: false },
  { id: 2, class:'seat-1', selected: false },
  { id: 3, class:'seat-2', selected: false },
  { id: 4, class:'seat-3', selected: false },
  { id: 5, class:'seat-4', selected: false },
  { id: 6, class:'seat-5', selected: false },
  { id: 7, class:'seat-6', selected: false },
]);
</script>

<template>
    <div class="seat-container" style="background-image: url('/public/images/seat/plane-plate.png')">

        <v-btn
        :class="['seat-button', { selected: seat.selected }]"
        :style="{ top: seat.top, left: seat.left }"
        @click="toggleSeat(seat.id)"
        density="compact"
        size="small"
        color="grey-lighten-1"
        rounded
      >
        {{ seat.id }}
      </v-btn>


    </div>

</template>

<style scoped>
   .seat-container{
    height: 180px;
    width: 100%;
    background-position: center;
    background-size: contain;
    background-repeat: no-repeat;
    position: relative;
    z-index: 1;
   }
</style>
