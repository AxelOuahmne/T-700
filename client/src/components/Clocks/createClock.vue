<template>
<div class="div">
    <div class="horloge-parent">
            <h1 class="horloge">{{ formatTime(currentTime) }}</h1>
     <div class="horloge-btn">
        <button @click="createClock(this.id)">Cretae clock</button>
        <button v-if="timerState === 'stopped'" @click="startTimer" class="btn btn-danger">
        Start
      </button>
      <button v-else-if="timerState === 'running'" @click="pauseTimer" class="pasue">
        Pause
      </button>
      <button v-else @click="resumeTimer">Continue</button>
      <button @click="resetTimer" class="reset">Reset</button>
     </div>
    
    </div>
</div>
  </template>
    
    <script>
  import axios from "axios";
  import "boxicons";
  import moment from "moment";
  import "moment-timezone";
  export default {
    name: "cretaeClock",
    data() {
    return {
      id: null,
      workingTimeData: {
        start: "",
        end: "",
        user_id: "",
      },
      timerId: null,
      url:'localhost',
      timerState: localStorage.getItem("timerState") || "stopped",
      currentTime: parseInt(localStorage.getItem("currentTime")) || 0,
    };
  },
  mounted() {
    console.log(this.$route.params.id);
    this.id = this.$route.params.id;
    if (this.timerState === "running") {
      this.startTimer();
    }
  },
  beforeUnmount() {
    // Avant de quitter la page, enregistrez l'état du timer et le temps écoulé
    localStorage.setItem("timerState", this.timerState);
    localStorage.setItem("currentTime", this.currentTime.toString());
  },
    methods: {
        async createClock(user_id) {
  try {
    // Mettez à jour timerState pour indiquer que le chronomètre est en cours d'exécution
    this.timerState = "running";

    const currentDate = moment().tz("Europe/Paris");
    const data = {
      time: currentDate.add(1, "hours"),
    };
    console.log(data);

    const response = await axios.post(
      `http://${this.this.url}:4000/api/clocks/${user_id}`,
      { clock: data }
    );

    console.log("Clock créée avec succès:", response.data);
    if (response.data.status) {
      localStorage.setItem("start", JSON.stringify(response.data.time));
    } else if (!response.data.status) {
      // const today = moment().format('YYYY-MM-DD H:mm');
      this.workingTimeData.start = JSON.parse(
        localStorage.getItem("start")
      );
      this.workingTimeData.user_id = user_id;
      this.workingTimeData.end = response.data.time;

      axios
        .post(`http://${this.url}:4000/api/working_times/${user_id}`, {
          working_time: this.workingTimeData,
        })
        .then((response) => {
          console.log("Working time créé avec succès:", response.data);
          localStorage.clear();
          // Mettez à jour timerState pour indiquer que le chronomètre est arrêté
          this.timerState = "stopped";
        })
        .catch((error) => {
          console.error("Erreur lors de la création du working time :", error);
          // Mettez à jour timerState pour indiquer que le chronomètre est arrêté en cas d'erreur
          this.timerState = "stopped";
        });
    }
  } catch (error) {
    console.error("Erreur lors de la création de la clock :", error);
    // Mettez à jour timerState pour indiquer que le chronomètre est arrêté en cas d'erreur
    this.timerState = "stopped";
  }
},

      startTimer() {
        this.timerState = "running";
        this.timerId = setInterval(() => {
          this.currentTime++;
          // Sauvegarder le temps actuel dans localStorage à chaque tick
          localStorage.setItem("currentTime", this.currentTime.toString());
        }, 1000);
      },
      pauseTimer() {
        this.timerState = "paused";
        clearInterval(this.timerId);
      },
      resumeTimer() {
        this.timerState = "running";
        this.startTimer();
      },
      resetTimer() {
      // Réinitialisez le timer et effacez les données enregistrées dans le localStorage
      this.currentTime = 0;
      this.timerState = "stopped";
      clearInterval(this.timerId);
      localStorage.removeItem("timerState");
      localStorage.removeItem("currentTime");
    },
      formatTime(seconds) {
        const hours = Math.floor(seconds / 3600);
        const minutes = Math.floor((seconds % 3600) / 60);
        const secs = seconds % 60;
        return `${String(hours).padStart(2, "0")}:${String(minutes).padStart(
          2,
          "0"
        )}:${String(secs).padStart(2, "0")}`;
      },
    },
  };
  </script>
    
    <style>
 

.horloge-parent {
    width: 400px;
    position: absolute;
    margin: 200px auto 200px 300px;
    border: 1px solid #e9eefd;
    border-radius: 7px;
    padding: 20px 20px 100px 20px;
    box-shadow: rgba(17, 17, 26, 0.1) 2px 2px 16px;;

}
.horloge{
    text-align: center;
    color: #4b5876;
    margin-bottom: 50px !important;
}
.horloge-btn {
    display: flex;
    justify-content: space-between;
    align-items: center;
}  
.reset {
    background: rgb(74, 19, 19) !important;
    border-radius: 5px;
}
.pasue {
    background: rgb(17, 135, 56) !important;
    border-radius: 5px;
}


</style> 