<template>
    <a :href="link" target="_blank" rel="noopener noreferrer">
        <div
            class="card flex-center">
            <h1 class="card-title">{{ title }}</h1>
            <hr class="card-line">
            <p class="card-text">{{ description }}</p>
            <div class="card-image-and-info flex-center">
              <img :src="image" :alt="title" class="card-image">
            <p class="card-info">
                <span class="card-info-first">Published:</span> {{ theDate }}
            </p>
            </div>
        </div>
    </a>
</template>

<script>

import moment from 'moment';

export default {
    props: ['title', 'link', 'description', 'image', 'date'],
    computed: {
        theDate() {
            return moment(this.date).format('MMM Do YYYY');
        }
    }

}
</script>

<style>
/* .movies-list {
  margin-left: 125px;
  margin-top: 48px;
} */

div.content-movie-list {
  display: inline-grid;
  grid-gap: 10px 35px;
  grid-template-columns: 420px 420px 420px;
  /* grid-template-rows: 80px 80px 80px 150px; */
  margin-top: 75px;
  margin-bottom: 65px;
}

div.card {
  flex-direction: column;
  justify-content: space-around;
  box-shadow: 0px 19px 50px -16px #8e8e8e;
  background-color: #fff;
  width: 340px;
  height: 400px;
  border-radius: 15px;
  padding: 30px;
  cursor: pointer;
  margin-top: 25px;
  margin-bottom: 25px;
}

.card-title {
  font-size: 25px;
  font-weight: bold;
  margin-bottom: 0;
  color: #000;
  text-align: center;
}

.card-text {
  margin-top: 0;
  margin-bottom: 0;
  text-align: center;
  color: #000;
}

.card-image-and-info {
  /* margin-top: -22px; */
  flex-direction: column;
  justify-content: space-between;
}

.card-line {
  width: 85px;
  border: none;
  background-color: #000;
  height: 1px;
  opacity: 0.1;
  margin-top: -10px;
  margin-bottom: 0;
}
.card-image {
  width: 100%;
  max-height: 170px;
  max-width: 250px;
}
.card-info {
  color: #000;
}
.card-info-first{
    font-weight: 550;
}
</style>