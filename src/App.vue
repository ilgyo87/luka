<template>
  <img alt="luka picture" src="./assets/luka.jpeg" />
  <HelloWorld msg="Luka" />

  <div>
    <div id="points">
      <legend>stat tracker</legend>
      <span v-text="totalPoints"></span>
      Points
      <input type="range" min="0" max="60" v-model="rangePoints" />
    </div>

    <span v-text="totalRebounds"></span>
    Rebounds
    <input type="range" min="0" max="20" v-model="rangeRebounds" />

    <span v-text="totalAssists"></span>
    Assists
    <input type="range" min="0" max="20" v-model="rangeAssists" />

    <span v-text="totalSteals"></span>
    Steals
    <input type="range" min="0" max="10" v-model="rangeSteals" />
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
      <tr v-for="stat in pointsFiltered" :key="stat.Date">
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
      stats2019: stats2019,
      stats2020: stats2020,
      season2019String: JSON.stringify(stats2019),
      season2020String: JSON.stringify(stats2020),
      // season2019: JSON.parse(this.stats2019),
      // season2020: JSON.parse(this.stats2020),
      // allSeasons: Object.assign(this.season2019, this.season2020),
      // allSeasons: [this.season2019, this.season2020],
      // allSeasons: this.season2019String.concat(this.season2020String),
      filter: "",
      one: {"rk": 1, "gm": 3}
    };
  },
  components: {
    HelloWorld,
  },
  methods: {},
  watch: {},
  computed: {
    combined() {
      // return Object.assign({}, this.season2019String, this.season2020String)
      // return this.season2019String.concat(this.season2020String);
       return this.stats2019.concat(this.stats2020);
      //  return [{...this.stats2019,...this.stats2020}]
    },
    totalRebounds() {
      return this.rangeRebounds;
    },
    totalAssists() {
      return this.rangeAssists;
    },
    totalSteals() {
      return this.rangeSteals;
    },
    totalPoints() {
      return this.rangePoints;
    },
    pointsFiltered() {
      return this.combined.filter((stat) => {
        return stat.PTS >= this.rangePoints;
        // &&
        //  stat.TRB >= this.rangeRebounds &&
        //  stat.AST >= this.rangeAssists &&
        //  stat.STL >= this.rangeSteals
      });
    },
  },
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
