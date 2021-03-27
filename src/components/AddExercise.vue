<template>
  <div class="addExercise">
      <p>Please select the type of exercise you would like to add to your current workout</p>
      <button @click="toggleActive(0)">Strength</button>
      <button @click="toggleActive(1)">Endurance</button>

      <div class="strengthFormContainer" v-if="item.isStrength === true">
          <h3>Strength</h3>
          <form @submit.prevent="addExercise">
              <label>Exercise</label>
              <input 
              type="text"
              v-model="item.exerciseStrength"
              :class="{'has-error' : submitting && invalidItem2 }"
              @focus="clearStatus"
              />

              <label>Sets</label>
              <input 
              type="number"
              v-model="item.sets"
              :class="{'has-error' : submitting && invalidItem2 }"
              @focus="clearStatus"
              />

              <label>Reps</label>
              <input 
              type="number"
              v-model="item.reps"
              :class="{'has-error' : submitting && invalidItem2 }"
              @focus="clearStatus"
              />

              <label>Weight</label>
              <input 
              type="number"
              v-model="item.weight"
              :class="{'has-error' : submitting && invalidItem2 }"
              @focus="clearStatus"
              />

              <button>Add Exercise</button>

              <p v-if="error && submitting" class="errorMessage">❗️Please fill out all required fields</p>
              <p v-if="success" class="successMessage">✅ Excersise sucessfully added to current workout</p>
          </form>
      </div>

      <div class="enduranceFormContainer" v-if="item.isEndurance === true">
          <h3>Endurance</h3>
          <form @submit.prevent="addExercise">
              <label>Exercise</label>
              <input 
              type="text"
              v-model="item.exerciseEndurance"
              :class="{'has-error' : submitting && invalidItem1 }"
              @focus="clearStatus"
              />

              <label>Distance</label>
              <input 
              type="text"
              v-model="item.distance"
              :class="{'has-error' : submitting && invalidItem1 }"
              @focus="clearStatus"
              />

              <label>Duration</label>
              <input 
              type="text"
              v-model="item.duration"
              :class="{'has-error' : submitting && invalidItem1 }"
              @focus="clearStatus"
              />

              <button>Add Exercise</button>

              <p v-if="error && submitting" class="errorMessage">❗️Please fill out all required fields</p>
              <p v-if="success" class="successMessage">✅ Excersise sucessfully added to current workout</p>
          </form>
      </div>
    </div>
</template>

<script>
export default {
    name: "add-exercise",
    data() {
        return {
            item: {
                exerciseStrength: "",
                exerciseEndurance: "",
                sets: 0,
                reps: 0,
                weight: 0,
                distance: "",
                duration: "",
                isStrength: false,
                isEndurance: false,
                exerciseType: "",
                added: false,
            },
            submitting: false,
            erorr: false,
            success: false,
        }
    },
    methods: {
        // Toggles Strength or Endurance
        toggleActive(type) {
            if (type === 0) {
                this.item.isStrength = true
                this.item.isEndurance = false
                this.item.exerciseType = "strength"
                this.clearStatus()
            } else {
                this.item.isStrength = false
                this.item.isEndurance = true
                this.item.exerciseType = "endurance"
                this.clearStatus()
            }
        },
        // Adds Exercise
        addExercise() {
            this.item.added = true
            this.submitting = true
            this.clearStatus()
            if (this.invalidItem2 && this.item.isStrength) {
                this.error = true
                return
            }
            if (this.invalidItem1 && this.item.isEndurance) {
                this.error = true
                return
            }
            this.$emit("add:item", this.item)
            this.error = false
            this.success = true
            this.submitting = false
        },
        clearStatus() {
            this.success = false
            this.erorr = false
        },
    },
    computed: {
        invalidItem1() {
            return this.item.exerciseEndurance.trim() === "";
        },
        invalidItem2() {
            return this.item.exerciseStrength.trim() === "";
        },
    },
}
</script>

<style>
    form {
        margin-bottom: 2rem;
    }
    [class*='-message'] {
        font-weight: 500;
    }
    .errorMessage {
        color: #d33c40;
    }
    .successMessage {
        color: #32a95d;
    }
</style>