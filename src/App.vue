<template>
  <img alt="luka picture" src="./assets/luka.jpeg" />
  <HelloWorld msg="Luka" />


<div>
  <div id="points">
  <legend>stat tracker</legend>
  <span v-text="totalPoints"></span>
  Points
  <input type="range" list="tickmarks"  v-model="rangePoints"/>
  <datalist id="tickmarks">
    <option value="0" ></option>
    <option value="10"></option>
    <option value="20"></option>
    <option value="30"></option>
    <option value="40"></option>
    <option value="50"></option>
    <option value="60"></option>
    <option value="70"></option>
    <option value="80"></option>
    <option value="90"></option>
    <option value="100"></option>
  </datalist>
  </div>

  <span v-text="totalRebounds"></span>
  Rebounds
  <input type="range" min:0 max: 10 step:1 list="tickmarks"  v-model="rangeRebounds"/>
  <!-- <datalist id="tickmarks">
    <option value="0" ></option>
    <option value="1"></option>
    <option value="2"></option>
    <option value="3"></option>
    <option value="4"></option>
    <option value="5"></option>
    <option value="6"></option>
    <option value="7"></option>
    <option value="8"></option>
    <option value="9"></option>
    <option value="10"></option>
  </datalist> -->

</div>

  <table id="firstTable">
    <thead>
      <tr>
        <th>PTS</th>
        <th>RB</th>
        <th>AST</th>
        <th>STL</th>
        <th>BLK</th>
        <th>TO</th>
        <th>FGM</th>
        <th>FGA</th>
        <th>FG%</th>
        <th>3PM</th>
        <th>3PA</th>
        <th>3P%</th>
        <th>FTM</th>
        <th>FTA</th>
        <th>FT%</th>
        <th>@</th>
        <th>Opponent</th>
        <th>Win/Loss</th>
        <th>Date</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="stat in pointsFiltered" :key="stat.Rk">
        <td>{{ stat.PTS }}</td>
        <td>{{ stat.TRB }}</td>
        <td>{{ stat.AST }}</td>
        <td>{{ stat.STL }}</td>
        <td>{{ stat.BLK }}</td>
        <td>{{ stat.TOV }}</td>
        <td>{{ stat.FG }}</td>
        <td>{{ stat.FGA }}</td>
        <td>{{ stat.FGP }}</td>
        <td>{{ stat.THREEP }}</td>
        <td>{{ stat.THREEPA }}</td>
        <td>{{ stat.THREEPP }}</td>
        <td>{{ stat.FT }}</td>
        <td>{{ stat.FTA }}</td>
        <td>{{ stat.FTP }}</td>
        <td>{{ stat.HorA }}</td>
        <td>{{ stat.Opp }}</td>
        <td>{{ stat.DIFF }}</td>
        <td>{{ stat.Date }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import stats2019 from "./assets/2018-19.json";
import stats2020 from "./assets/2019-20.json";
export default {
  name: "App",
  data() {
    return {
      rangePoints: 0,
      rangeRebounds: 0,
      rangeAssists: 0,
      rangeSteals: 0,
      stats2019,
      stats2020,
      filter: "",
      pts: [
        { value: 5, name: "5" },
        { value: 10, name: "10" },
        { value: 15, name: "15" },
        { value: 20, name: "20" },
        { value: 25, name: "25" },
        { value: 30, name: "30" },
        { value: 35, name: "35" },
        { value: 40, name: "40" },
        { value: 45, name: "45" },
        { value: 50, name: "50" },
      ],
    };
  },
  components: {
    HelloWorld,
  },
  methods: {
    
  },
  computed:{
    totalPoints(){
      return this.rangePoints
    },
    totalRebounds(){
      return this.rangeRebounds
    },
    pointsFiltered() {
      return this.stats2019.filter((stat)=>{
        return stat.PTS >= this.rangePoints
      })
    },
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
img {
  width: 150px;
  border-radius: 2px;
  box-shadow: 1px 1px 3px 1px rgba(0, 0, 0, 0.5);
  transition: width 1s;
}
#firstTable {
  border-block: 2px;
  border-block-color: black;
  background: lightgrey;
  border-radius: 5px;
  border: 10px solid blue;
  padding-block-start: 5px;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  border-collapse: collapse;

}
</style>
