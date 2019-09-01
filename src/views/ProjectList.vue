<template>
  <v-container wrap>
    <div style="margin-top:56px">
      <div style="padding:3% 5%; border:2px solid grey; border-radius:15px; width:100%;">

        <v-layout wrap row justify-center style="margin-bottom:20px;">
          <v-flex xs12 class="text-center">
            <h1 class="text-center"><span class="fontHannaAir">프로젝트들</span></h1>
          </v-flex>
        </v-layout>

        <v-layout row wrap justify-center style="margin:40px 0;">
          <v-flex xs10>
            <v-text-field v-model="input" placeholder="검색어를 입력하세요!"/>
          </v-flex>
        </v-layout>


        <v-layout wrap row>
          <v-flex xs12 sm6 md4 v-for="(project, idx) in projects" v-if="project.title.includes(input)" style="padding:10px; position:relative">
            <v-card style="min-height:320px; width:100%;" outlined>
              <v-img class="white--text" height="200px" :src="project.image"/>

              <div style="margin:10px 0 0 15px;" class="txtline">
                <div class="showLikeitCnt fas" >
                  <span style="z-index:3; position:absolute; top:24%; left:36%; color:white;">
                    <span class="fontjua " >
                      {{project.lcnt}}
                    </span>
                  </span>
                </div>

                <span class="title"><span class="fontDoHyeon  ">{{project.title}}</span></span>
              </div>
              <div style="margin:2px 0 0 15px;">
                <v-chip x-small outlined v-for="t in project.tech" style="margin-right:2px;">
                  <!-- {{t}} -->
                  <span >{{ t.substring(0,15) }}</span>
                </v-chip>
              </div>
              <v-chip outlined style="position:absolute; right:10px; top:276px;"  @click="showdetail(idx)">
                <i class="fas fa-caret-down downbtn"/>
              </v-chip>
              <v-expand-transition>
                <div v-show:false class="pjDetail" style="margin-top:10px; padding:10px;">
                  <v-chip x-small outlined style="margin-right:2px;" label color="#00ae9d">
                    {{project.rank}}
                  </v-chip>
                  <br/>
                  <p class="overline"><span class="fontNanum ">
                    {{project.desc}}
                  </span></p>

                  <v-layout row wrap>
                    <v-spacer/>
                    <div style="display:inline; margin-right:10px;">
                      <v-chip color="success" style="margin-right:5px;">
                        <span class="fontHanna">
                          더보기
                        </span>
                      </v-chip>
                      <v-chip color="#00ae9d" class="white--text">
                        <span class="fontHanna ">
                          개발자보러가기
                        </span>
                      </v-chip>
                    </div>
                  </v-layout>
                </div>
              </v-expand-transition>
            </v-card>



          </v-flex>
        </v-layout>
      </div>
    </div>
  </v-container>
</template>

<script>
import FirebaseService from "@/services/FirebaseService";
export default {
  data() {
    return {
      projects: [],
      input:"",
    };
  },
  watch: {
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      this.projects = await FirebaseService.SELECT_ALLProjectsForList();
    },
    showdetail(index){
      if($('.pjDetail').eq(index).css('display') == 'none'){
        $('.pjDetail').eq(index).show();
      }else{
        $('.pjDetail').eq(index).hide();
      }

    },
  },
};
</script>
