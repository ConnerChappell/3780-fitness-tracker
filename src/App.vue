<template>
  <div id="app" class="small-container">
    <h1>Fitness Tracker</h1>

    <div>
      <h3>Date</h3>
      <p>Please select the type of exercise you would like to add to your current workout</p>
      <button>Strength</button>
      <button>Endurance</button>
      <h3>Current Workout</h3>
    </div>

    <workout-history 
    :workouts="sessions"
    @delete:session="deleteSession"
    />

  </div>
</template>

<script>
import WorkoutHistory from './components/WorkoutHistory.vue'

export default {
  name: 'App',
  components: {
    WorkoutHistory
  },
  data() {
    return {
      sessions: [
        {
          id: 1,
          date: "2021-03-10",
          exercises: [
            {
              exerciseType: "strength",
              exercise: "Dumbbell Curls",
              sets: 3,
              reps: 12,
              weight: 25
            },
            {
              exerciseType: "strength",
              exercise: "Bench Press",
              sets: 3,
              reps: 10,
              weight: 135
            },
          ],
        },
        {
          id: 2,
          date: "2021-03-08",
          exercises: [
            {
              exerciseType: "endurance",
              exercise: "Running",
              distance: "2 miles",
              duration: "20 minutes",
            },
            {
              exerciseType: "endurance",
              exercise: "Swimming",
              distance: "10 laps",
              duration: "15 minutes"
            },
          ],
        },
      ],
      currentWorkout: {},
      adding: false,
    };
  },
  methods() {

  }
}
</script>

<style>
  button {
    background: #000;
    border: 1px solid #000;
    margin-right: 10px;
    transition: all .4s;
  }
  button:hover {
    background: #fff;
    border: 1px solid #000;
    color: #000;
  }
  button:focus {
    background: #fff;
    color: #000;
    border: 1px solid #000;
    outline: none;
  }

  .small-container {
    max-width: 680px;
  }
</style>
