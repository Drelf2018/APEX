<template>
  <div class="show-block">
    <center><span style="font-family: Homo;font-size:2em;margin-bottom: 0.3em;">{{ title }}</span></center>
    <div class="table-block">
    <table cellspacing="0" v-for="score, i in scores">
      <tr>
        <th><span style="font-size:1.5em;color: rgba(0,0,0,0)">000</span></th>
        <th></th>
        <th></th>
        <th class="num">排名分</th>
        <th class="num">击杀分</th>
        <th class="num">总得分</th>
      </tr>
      <tr :class="{'team': true, 'first': id == 0, 'other': 0<id&&id<score.length-1, 'last': id == score.length-1}" v-for="s, id in score">
        <td align="center"><span style="font-family: APEX; font-size: 1.5em;color: rgb(178,10,27);">{{ s.rank }}</span></td>
        <td><img :src="s.teamicon" :alt="s.teamname"></td>
        <td>
          <div>
            <span style="font-size:1.5em">{{ s.teamname }}</span>
            <div style="font-family:Homo; font-size:0.5em;position: relative;top: -5px;" >
              <span v-for="n in s.teammates">{{ n }}</span>
            </div>
          </div>
        </td>
        <td align="center" style="font-size: 1.5em;">{{ s.placement }}</td>
        <td align="center" style="font-size: 1.5em;">{{ s.kills }}</td>
        <td align="center" style="font-size: 1.5em;">{{ s.placement + s.kills }}</td>
      </tr>
    </table>
  </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      title: null,
      scores: [
        [
          {rank: 1, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "TSM", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 12, kills: 9},
          {rank: 2, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "NRG", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 9, kills: 6},
          {rank: 3, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "AD", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 7, kills: 6},
          {rank: 4, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "SINGULARITY", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 5, kills: 1},
          {rank: 5, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "CLOUD9", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 4, kills: 6},
        ],
        [
          {rank: 6, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "TSM", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 12, kills: 9},
          {rank: 7, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "NRG", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 9, kills: 6},
          {rank: 8, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "AD", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 7, kills: 6},
          {rank: 9, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "SINGULARITY", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 5, kills: 1},
          {rank: 10, teamicon: "https://air-marketing-assets.imgix.net/blog/logo-db/apex-legends-logo/apex-legends-logo-svg-3.svg", teamname: "CLOUD9", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 4, kills: 6},
        ]
      ]
    }
  },
  methods: {
    getQueryString(name) {
      var reg = new RegExp('(^|&)' + name + '=([^&]*)(&|$)', 'i');
      console.log(window.location.search);
      var r = window.location.search.substr(1).match(reg);
      if (r != null) {
        return decodeURIComponent(r[2]);
      }
      return null;
    }
  },
  mounted() {
    this.title = this.getQueryString("title")
  }
}
</script>

<style>
.show-block {
  width: 72%;
  padding: 1em;
  margin: 75px auto;
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.9);
  box-shadow: 0 3px 1px -2px rgb(0 0 0 / 12%), 0 2px 2px 0 rgb(0 0 0 / 14%), 0 1px 5px 0 rgb(0 0 0 / 20%)
}

.num {
  /* font-family: Novecento; */
  font-family: Homo;
  padding-left: 0.5em;
  padding-right: 0.5em;
}

.first td { 
  padding: 0 0.5em 0;
  border-bottom: 2px solid rgb(190, 110, 90);
}

.other td { 
  padding: 0.5em 0.5em 0;
  border-bottom: 2px solid rgb(190, 110, 90);
}

.last td { 
  padding: 0.5em 0.5em 0;
}

img {
  height: 60px;
}

span {
  display: block;
}

table {
  width: 48%;
}

.table-block {
  display: flex;
  justify-content: space-between;
}

@media screen and (max-width: 1500px) {
  table {
    width: 100%
  }

  .show-block {
    width: 80%;
    min-width: 485px;
  }

  .table-block {
    flex-direction: column;
    align-items: center
  }
}
</style>