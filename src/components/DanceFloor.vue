<template>
  <div class="container">
    <div class="dancers-container">
      <div class="boys">
        <label>
          Add boy to boys list:
          <input type="text" v-model="boyName" />
          <button type="button" @click="addNameToBoysList">Add</button>
        </label>
        <div>BOYS LIST (1 step - choose the boy):</div>
        <div class="boys-container">
          <dancers-list
            v-for="boy in boysData"
            :key="boy.id"
            :name="boy"
            @add="addToChoosenList($event, boy)"
          />
        </div>
      </div>
      <div class="girls">
        <label>
          Add girl to girls list:
          <input type="text" v-model="girlName" />
          <button type="button" @click="addNameToGirlsList">Add</button>
        </label>
        <div>GIRLS LIST (2 step - choose the girl):</div>
        <div class="girls-container">
          <dancers-list
            v-for="girl in girlslData"
            :key="girl.id"
            :name="girl"
            @add="addToChoosenList($event, girl)"
          />
        </div>
      </div>
    </div>
    <button
      class="add-dancefloor"
      type="button"
      @click="addToDanceList"
      :disabled="isDisabled"
    >
      Add To DanceFloor
    </button>
    <div class="dancefloor">
      Dancefloor:
      <div class="dancefloor-container" v-if="danceList.length > 0">
        <dancing-pairs
          v-for="pair in danceList"
          :key="pair.id"
          :dancing-pairs-list="pair"
          @delete="deletePairFromDanceList($event)"
        />
      </div>
      <div class="empty-container" v-else>Dancefloor is empty</div>
    </div>
  </div>
</template>
<script>
import DancersList from "./DancersList.vue";
import DancingPairs from "./DancingPairs.vue";

export default {
  name: "DanceFloor",
  components: {
    DancersList,
    DancingPairs,
  },
  props: {
    boysList: {
      type: Array,
      default: () => [],
    },
    girlsList: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      boyName: null,
      girlName: null,
      choosenList: [],
      danceList: [],
      boysData: this.boysList,
      girlslData: this.girlsList,
    };
  },
  methods: {
    addNameToBoysList() {
      this.boysData.push({
        id: Date.now(),
        name: this.boyName,
        activeDance: false,
      });
      this.boyName = null;
    },
    addNameToGirlsList() {
      this.girlslData.push({
        id: Date.now(),
        name: this.girlName,
        activeDance: false,
      });
      this.girlName = null;
    },
    addToChoosenList(obj) {
      obj.isActive = !obj.isActive;
      this.choosenList.push(obj.name);
    },
    addToDanceList() {
      this.boysData = this.boysData.filter((boy) => !boy.isActive);
      this.girlslData = this.girlslData.filter((girl) => !girl.isActive);

      this.danceList.push({
        id: Date.now(),
        pair: this.choosenList.join("-"),
      });
      this.choosenList = [];
    },
    deletePairFromDanceList(id) {
      this.danceList = this.danceList.filter((pair) => pair.id !== id);
    },
  },
  computed: {
    isDisabled() {
      if (this.boysData.length !== this.girlslData.length) return true;
      if (this.choosenList.length === 0 || this.choosenList.length % 2) {
        return true;
      }
      return false;
    },
  },
};
</script>
<style lang="css" scoped>
.container {
  max-width: 700px;
  margin: 0 auto;
}
.dancers-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
}
.boys,
.girls {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 0 20px;
}
.dancefloor {
  margin-top: 10px;
}
.dancefloor-container {
  border: 2px solid purple;
  margin-top: 20px;
  padding: 10px 30px;
}
.empty-container {
  margin-top: 20px;
  color: brown;
}
.add-dancefloor {
  margin-top: 20px;
}
.boys-container,
.girls-container {
  border: 2px solid teal;
}
button {
  cursor: pointer;
}
</style>
