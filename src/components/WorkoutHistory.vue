<template>
    <div class="workoutHistory">
        <h2>Workout History</h2>

        <div class="noWorkoutsDisplayed" v-if="workouts.length < 1">
            <p>There are no workouts saved in your history</p>
        </div>

        <div class="historyContainer">
            <ul v-for="session in workouts" :key="session.id">
                <li class="workoutDate">{{session.date}}</li>

                <div class="singleExercise">
                    <template v-for="(stuff, index) in session.exercises.filter((item) => item.exerciseType === 'strength')">
                        <li :key="`exercise-${index}`">Exercise: {{stuff.exercise}}</li>
                        <li :key="`sets-${index}`">Sets: {{stuff.sets}}</li>
                        <li :key="`reps-${index}`">Reps: {{stuff.reps}}</li>
                        <li :key="`weight-${index}`" class="exerciseDivider">Weight: {{stuff.weight}}</li>
                    </template>
                </div>
                
                <div class="singleExercise">
                    <template v-for="(stuff, index) in session.exercises.filter((item) => item.exerciseType === 'endurance')">
                    <li :key="`exercise-${index}`">Exercise: {{stuff.exercise}}</li>
                    <li :key="`distance-${index}`">Distance: {{stuff.distance}}</li>
                    <li :key="`duration-${index}`" class="exerciseDivider">Duration: {{stuff.duration}}</li>
                    </template>
                </div>

                <div class="editDelete">
                    <button>Edit</button>
                    <button @click="$emit('delete:session', session.id)">Delete</button>
                </div>    
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: "Workout",
    props: {
        workouts: Array,
    },
    methods: {
        getStrength: function (exercise) {
            const details = exercise.filter(
                (theExercise) => theExercise.exerciseType === "strength"
            );
            console.log("Details", details);
        },
        getEndurance: function (exercise) {
            const details = exercise.filter(
                (theExercise) => theExercise.exerciseType === "endurance"
            );
            console.log("Details", details);
        },
    },
};
</script>

<style>
    .historyContainer ul {
        margin-left: 0;
        padding-left: 0;
    }
    .workoutDate {
        font-size: 20px;
        font-weight: 800;
        margin-bottom: 10px;
    }
    li {
        list-style-type: none;
        font-size: 18px;
        font-weight: 500;
    }
    .exerciseDivider {
        margin-bottom: 15px;
    }
</style>