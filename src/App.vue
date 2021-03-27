<template>
  <div id="app" class="small-container">
    <h1>Fitness Tracker</h1>

    <add-exercise 
    @add:item="addItem"
    />

    <current-workout />

    <workout-history 
    :workouts="sessions"
    @delete:session="deleteSession"
    />

  </div>
</template>

<script>
import AddExercise from './components/AddExercise.vue';
import CurrentWorkout from './components/CurrentWorkout';
import WorkoutHistory from './components/WorkoutHistory.vue';

export default {
  name: 'App',
  components: {
    AddExercise,
    CurrentWorkout,
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
              exercise: "Run",
              distance: "2 miles",
              duration: "20 minutes",
            },
            {
              exerciseType: "endurance",
              exercise: "Swim",
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
  methods: {
    deleteSession(id) {
      this.sessions = this.sessions.filter((session) => session.id !== id)
    }
  }
}
</script>

<style>
  h1 {
    font-size: 75px;
  }
  h2 {
    margin-bottom: .75rem;
    padding-bottom: .5rem;
    border-bottom: 1px solid #000;
  }
  h3 {
    margin-top: 0;
  }
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
