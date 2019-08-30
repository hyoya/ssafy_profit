<template>
    <v-dialog v-model="skillmodal"  max-width="600px">
      <template v-slot:activator="{ on }">
        <img src="../../../assets/icon_set/pencil.png" alt="edit" style="cursor:pointer;"
        v-on="on" @click="initShowModal"/>
      </template>

      <!-- Modal -->
      <v-container class="inputmodal">
        <v-layout row wrap style="padding:10px 20px;">
          <v-spacer/>
          <span class="font-weight-regular headline"><span class="fontJua">기술스택 편집창</span></span>
          <v-spacer/>
          <div @click="skillmodal = false"><i class="fa fa-close"/></div>
        </v-layout>

        <!-- container -->
        <v-card-text>
          <v-layout justify-center row wrap>
            <div v-if="this.unselectList.length !== 0">
            <v-flex xs12>
              <fieldset style="padding:10px; border:2px solid lightgrey; border-radius:15px; " justify-center>
                <legend align="center" class="font-weight-bold">
                  <span class="fontHannaAir" style="margin:0 10px;">공개할 기술스택</span>
                </legend>
              <v-layout row wrap justify-center>
                <p style="width:100%;" class="text-center caption grey--text"> - 다른 사용자에게 공개할 기술스택입니다. </p>
                <v-chip v-for="item in this.selectList" small text outlined @click="deleteTech(item)"
                  style="margin:0 2px;" color="#2C3E50">
                  {{ item }}
                </v-chip>
              </v-layout>
              </fieldset>
            </v-flex>

            <v-flex xs12 style="margin-top:40px;">
              <fieldset style="padding:10px; border:2px solid lightgrey; border-radius:15px; " justify-center>
                <legend align="center" class="font-weight-bold">
                  <span class="fontHannaAir" style="margin:0 10px;">보유 중인 기술스택</span>
                </legend>
              <v-layout row wrap justify-center>
                <p style="width:100%;" class="text-center caption grey--text"> - 자신있는 기술스택을 선택하여 다른 사용자에게 보여주세요! </p>
                <v-chip v-for="item in this.unselectList" small text outlined @click="addTech(item)"
                  style="margin:0 2px;">
                  {{ item }}
                </v-chip>
              </v-layout>
              </fieldset>
            </v-flex>
            </div>
            <div v-else>
                <fieldset style="padding:10px; border:2px solid lightgrey; border-radius:15px; " justify-center>
                  <legend align="center" class="font-weight-bold">
                    <span class="fontHannaAir" style="margin:0 10px;">내 기술스택</span>
                  </legend>
                  <!-- 기술이 하나도 없을때, 기술창에 출력할 문구 -->
                  <v-layout row wrap justify-center style="margin:20px 0;">
                    <span class="small lightgrey--text" style="text-align:center">
                      <span class="fontJua">
                        * 등록된 기술이 없습니다 *
                        <br />
                        <br />
                        <span class="fontHannaAir" style="font-weight: bold;">프로젝트</span>를 등록하면 프로젝트에 사용된
                        <br />기술이 내 기술 정보에 등록됩니다.
                        <br />
                        <br />
                        <span class="fontHannaAir" style="font-weight: bold; ">
                          <div style="background:rgb(117, 199, 145); padding: 5px 20px; border-radius: 20px; color: white;margin:3px;">
                            <span class="fontDoHyeon ">프로젝트 생성하기</span>
                          </div> &nbsp;버튼을 눌러 프로젝트를 등록하세요!
                        </span>
                      </span>
                    </span>
                  </v-layout>
                </fieldset>
            </div>


          </v-layout>

        </v-card-text>

        <!-- action -->
        <v-layout row wrap justify-center v-if="this.unselectList.length !== 0">
          <v-btn v-on:click="sendSkill(selectList,unselectList)" text outlined> 등록 </v-btn>
        </v-layout>

      </v-container>
    </v-dialog>
</template>

<script>
import FirebaseService from "@/services/FirebaseService";

  export default {
    props: [
      'userSkills',
      'showSkillList',
    ],
    data() {
        return {
        skillmodal:false,
        receiveUserSkills:this.userSkills,
        receiveShowSkillList:this.showSkillList,
        unselectList:[],
        selectList:[],
      }
    },
    created() {
    },
    methods : {
      deleteTech(item){
        this.selectList.splice(this.selectList.indexOf(item),1);
        this.calcDiff();
      },
      addTech(tech){
        this.selectList.push(tech);
        this.calcDiff();
      },
      sendSkill(selectList,unselectList) {
        this.$emit('sendSkill',selectList,unselectList);
        this.skillmodal = false;
      },
      calcDiff(){
        var tmp =[];
        for(var i=0; i<this.receiveUserSkills.length; i++){
          if(!this.selectList.includes(this.receiveUserSkills[i])){
            tmp.push(this.receiveUserSkills[i]);
          }
        }
        this.unselectList = tmp;
      },
      async initShowModal(){
        var skill = await FirebaseService.SELECT_UserSkillByNickname(this.$session.get('session_id'));
        // console.log(skill)
        this.receiveUserSkills = skill[0].us;
        this.receiveShowSkillList = skill[0].ss;
        this.selectList = skill[0].ss;
        this.calcDiff();
      },
    },

  }
</script>
