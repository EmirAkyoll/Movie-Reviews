<template>
  <div class="selection-window flex-center">
    <div class="selection-window-gifs-upside flex-center">
      <img
        src="@\gifs\selection-window-gif1.gif"
        alt="gif"
        class="window-gif"
      />
      <img
        src="@\gifs\selection-window-gif2.gif"
        alt="gif"
        class="window-gif"
      />
      <img
        src="@\gifs\selection-window-gif3.gif"
        alt="gif"
        class="window-gif"
      />
    </div>
    <button @click="closeWindow" class="icon-close">
      <img class="icon-close" src="@/images/icon-close.png" alt="iconclose" />
    </button>
    <!-- {{ detailedQuery.isThisExcellent }} -->
    <div class="window-form flex-center">
      <div class="selection-element flex-center">
        <p
          class="selection-element-text"
          title="Eleştirmenlerin seçtikleri getirilsin?"
        >
          Seçkinler:
        </p>
        <input
          v-model="detailedQuery.isThisExcellent"
          type="checkbox"
          title="Eleştirmenlerin seçtikleri getirilsin?"
        />
      </div>

      <div class="selection-element flex-center">
        <p class="selection-element-text">Sayfa Numarası:</p>
        <input
          v-model="detailedQuery.pageNumber"
          type="text"
          class="page-number-textbox"
        />
      </div>

      <div class="selection-element flex-center">
        <p class="selection-element-text">Anahtar Kelime:</p>
        <input
          v-model="detailedQuery.keyWord"
          type="text"
          class="keyword-textbox"
        />
      </div>

      <div class="selection-element flex-center">
        <p class="selection-element-text">Listeleme Seçimi:</p>
        <select v-model="detailedQuery.listingSelection" name="" id="">
          <option value="by-opening-date">Opening Date</option>
          <option value="by-publication-date">Publication Date</option>
        </select>
      </div>

      <div class="selection-element flex-center">
        <p class="selection-element-text">Gurme İmzası:</p>
        <select v-model="detailedQuery.theReviewer" name="" id="">
          <!-- <option v-for="reviewer in reviewersMain" :key="reviewer" value="">{{reviewer}}</option> -->
          <option value="Jeannette Catsoulis">Jeannette Catsoulis</option>
          <option value="Nicolas Rapold">Nicolas Rapold</option>
          <option value="A.O. Scott">A.O. Scott</option>
          <option value="Ben Kenigsberg">Ben Kenigsberg</option>
          <option value="Beandrea July">Beandrea July</option>
          <option value="Amy Nicholson">Amy Nicholson</option>
          <option value="Beatrice Loayza">Beatrice Loayza</option>
          <option value="Glenn Kenny">Glenn Kenny</option>
          <option value="Calum Marsh">Calum Marsh</option>
          <option value="Concepción de León">Concepción de León</option>
          <option value="Devika Girish">Devika Girish</option>
        </select>
      </div>
    </div>
    <button
      @click="sendSelections(), closeWindow()"
      class="window-button flex-center">
      Apply
    </button>

    <div class="selection-window-gifs-downside flex-center">
      <img
        src="@\gifs\selection-window-gif4.gif"
        alt="gif"
        class="window-gif"
      />
      <img
        src="@\gifs\selection-window-gif5.gif"
        alt="gif"
        class="window-gif"
      />
      <img
        src="@\gifs\selection-window-gif6.gif"
        alt="gif"
        class="window-gif"
      />
    </div>
  </div>
</template>

<script>
// if (this.detailedSearch.isThisExcellent == true) {
//     this.$emit("is-this-excellent", "Y");
// }
// else{
//     this.$emit("is-this-excellent", "N");
// }

export default {
  data() {
    return {
      detailedQuery: {
        isThisExcellent: false,
        pageNumber: null,
        keyWord: null,
        listingSelection: null,
        theReviewer: null,
      },
    };
  },

  methods: {
    sendSelections() {
      this.$emit("send-selections", this.detailedQuery);
    },

    closeWindow() {
      this.$emit("close-window", false);
    },
  },
};
</script> 

<style>
.selection-window {
  width: 430px;
  height: 550px;
  background-color: #fff;
  border: 1px solid black;
  z-index: 1;
  display: flex;
  flex-direction: column;
  position: absolute;
  top: 65px;
  left: 560px;
  box-shadow: 0px 2px 50px -13px rgba(0, 0, 0, 0.65);
  border-radius: 2px;
  justify-content: space-between;
}

.selection-element {
  margin: -5px;
  outline: none;
  border: none;
}

.page-number-textbox {
  width: 30px;
}

.icon-close {
  width: 27px;
  height: 27px;
  position: absolute;
  top: 1px;
  right: 1px;
  cursor: pointer;
  border: none;
  background-color: transparent;
}

.selection-element-text {
  margin-right: 5px;
}

.window-gif {
  width: 143px;
  height: 103px;
  margin: 0;
  padding: 0px;
}

.selection-window-gifs-upside {
  position: absolute;
  top: 0.2px;
}

.selection-window-gifs-downside {
  position: absolute;
  bottom: 0.5px;
}

.window-button {
  height: 35px;
  cursor: pointer;
  margin-top: 50px;
  width: 150px;
  border-radius: 4px;
  background-color: #111827;
  color: #fff;
  font-size: 16px;
  padding: 9px;
  border-radius: 7px;
  font-weight: 500;
}
.window-button:hover{
    cursor: pointer;
    background-color: #333;
  }

.window-form {
  flex-direction: column;
  /* justify-content: space-between; */
}
</style>