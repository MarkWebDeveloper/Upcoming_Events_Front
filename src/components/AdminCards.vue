<script setup lang="ts">
import axios from 'axios';
import type Event from '@/models/Event';

const props = defineProps<{
  events: Event[]
}>();

const deleteEvent = async (eventId: number) => {
  try {
    await axios.delete(`http://localhost:8080/api/v1/events/${eventId}`);
  } catch (error) {
    console.error('Error al eliminar el evento:', error);
  }
};
</script>

<template>
  <div id="cards-container">
    <div v-for="event in events" :key="event.id" class="card">
      <img :src="`/src/assets/img/${event.event_image}`" alt="" class="mainImage">
      <h2>{{ event.event_title }}</h2>
      <div class="location">
        <img src="/src/assets/img/place-svgrepo-com.svg" alt="">
        <p>{{ event.city.nameOfCity }}</p>
      </div>
      <div class="date">
        <img src="/src/assets/img/calendar-days-svgrepo-com.svg" alt="">
        <p>{{ event.start_date }} ~ {{ event.finish_date }}</p>
      </div>
      <div class="buttonContainer">
        <img src="/src/assets/img/star-svgrepo-com.svg" alt="">
        <button @click="deleteEvent(event.id)">ELIMINAR</button>
        <img src="/src/assets/img/trash-svgrepo-com.svg" alt="">
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
#cards {

width: 60%;
border: 2px solid #27a138; 
border-radius: 5%;
padding: 10px; 

text-align: center;
font-family: 'Raleway', sans-serif;

.location, .date {
    display: flex;
    justify-content: flex-start;
    align-items: center;
}

.mainImage {
    width: 60%;
    padding: 10px;
}

img {
    width: 10%;
}

h2 {
    font-weight: bold;
    padding: 5px;
}

p {
    color: #27a138;
    font-weight: bold;
    padding: 5px;
}

.buttonContainer {

    display: flex;
    justify-content: space-between;
    padding: 5px;

    img {
        width: 12%;
    }

button {
    background-color: #27a138;
    color: white;
    font-weight: bold;
    border-radius: 15px;
    padding: 10px;
    margin-top: 10px;
}

}

}


@media only screen and (min-width: 768px) {

#cards {
width: 15%;

h2 {
font-size: 1rem;
}

img {
width: 10%;
}

.mainImage {
width: 40%;
}
}
}
</style>
