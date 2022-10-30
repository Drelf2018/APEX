<template>
  <div class="show-block" id="block">
    <center><span style="font-family: Homo;font-size: 3em;">{{ title }}</span></center>
    <div class="table-block">
      <table cellspacing="0" v-for="score, i in scores">
        <tr>
          <th><span style="font-size:3em;color: rgba(0,0,0,0)">000</span></th>
          <th></th>
          <th></th>
          <th class="num">排名分</th>
          <th class="num">击杀分</th>
          <th class="num">总得分</th>
        </tr>
        <tr
          :class="{ 'team': true, 'first': id == 0, 'other': 0 < id && id < score.length - 1, 'last': id == score.length - 1 }"
          v-for="s, id in score">
          <td align="center"><span style="font-family: APEX; font-size: 2.5em;color: rgb(178,10,27);">{{ s.rank
          }}</span></td>
          <td><img :src="s.teamicon" :alt="s.teamname"></td>
          <td>
            <div>
              <span style="font-size:2.5em">{{ s.teamname }}</span>
              <div style="font-family:Homo; font-size:1em;position: relative;top: -5px;">
                <span v-for="n in s.teammates" style="font-size:1.25em;">{{ n }}</span>
              </div>
            </div>
          </td>
          <td align="center" style="font-size: 2em;">{{ s.placement }}</td>
          <td align="center" style="font-size: 2em;">{{ s.kills }}</td>
          <td align="center" style="font-size: 2em;">{{ s.placement + s.kills }}</td>
        </tr>
      </table>
    </div>
  </div>
  <video v-if="video" controls autoplay>
    <source :src="video" type="video/mp4">
  </video>
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      video: null,
      title: null,
      scores: [
        [
          { rank: 1, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "TSM", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 12, kills: 9 },
          { rank: 2, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "NRG", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 9, kills: 6 },
          { rank: 3, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "AD", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 7, kills: 6 },
          { rank: 4, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "SINGULARITY", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 5, kills: 1 },
          { rank: 5, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "CLOUD9", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 4, kills: 6 },
        ],
        [
          { rank: 6, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "TSM", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 12, kills: 9 },
          { rank: 7, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "NRG", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 9, kills: 6 },
          { rank: 8, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "AD", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 7, kills: 6 },
          { rank: 9, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "SINGULARITY", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 5, kills: 1 },
          { rank: 10, teamicon: "https://yun.nana7mi.link/apex.png", teamname: "CLOUD9", teammates: ["科比258", "礼堂丁真", "谷爱凌"], placement: 4, kills: 6 },
        ]
      ]
    }
  },
  methods: {
    getQueryString(name) {
      var reg = new RegExp('(^|&)' + name + '=([^&]*)(&|$)', 'i');
      var r = window.location.search.substr(1).match(reg);
      if (r != null) {
        return decodeURIComponent(r[2]);
      }
      return null;
    }
  },
  mounted() {
    this.title = this.getQueryString("title") || "脆鲨杯"
    this.video = this.getQueryString("video")
  }
}
</script>
<style>
.show-block {
  width: 84%;
  position: relative;
  top: 83px;
  padding: 1em;
  margin: auto;
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.7);
  box-shadow: 0 3px 1px -2px rgb(0 0 0 / 12%), 0 2px 2px 0 rgb(0 0 0 / 14%), 0 1px 5px 0 rgb(0 0 0 / 20%)
}
.num {
  /* font-family: Novecento; */
  font-size: 1.5em;
  font-family: Homo;
  padding-left: 0.5em;
  padding-right: 0.5em;
}
.first td {
  padding: 0 0.5em 0.5em;
  border-bottom: 2px solid rgb(190, 110, 90);
}
.other td {
  padding: 0.8em 0.5em 0.5em;
  border-bottom: 2px solid rgb(190, 110, 90);
}
.last td {
  padding: 0.8em 0.5em 0;
}
img {
  height: 100px;
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
video {
  position: fixed;
  min-width: 100%;
  min-height: 136%;
  width: auto;
  height: auto;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  -webkit-transform: translateX(-50%) translateY(-50%);
  z-index: -100;
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