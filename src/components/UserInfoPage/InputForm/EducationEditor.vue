<template>
  <v-dialog v-model="edumodal" max-width="600px">
    <template v-slot:activator="{ on }">
      <img src="../../../assets/icon_set/pencil.png" alt="edit" style="cursor:pointer;" v-on="on" />
    </template>

    <v-container class="inputmodal">
      <v-layout row wrap style="padding:10px 20px;">
        <v-spacer />
        <span class="font-weight-regular headline">교육 추가</span>
        <v-spacer />
        <div @click="clearEdu">
          <i class="fa fa-close" />
        </div>
      </v-layout>

      <v-layout row justify-center wrap>
        <v-flex xs10 sm5>
          <p class="subheading font-weight-bold text-center">*기관명</p>
          <v-text-field single-line v-model="eduagency" />
        </v-flex>
        <v-flex xs10 sm5 offset-sm1>
          <p class="subheading font-weight-bold text-center">학위</p>
          <v-text-field single-line v-model="edudegree" />
        </v-flex>
      </v-layout>

      <v-layout row wrap justify-center>
        <v-flex xs5>
          <span class="subheading font-weight-bold">시작일</span>
          &nbsp;&nbsp;&nbsp;
          <input type="date" v-model="edustartday" />
        </v-flex>
        <v-flex xs5 offset-sm1>
          <span class="subheading font-weight-bold">종료일</span>
          &nbsp;&nbsp;&nbsp;
          <input type="date" v-model="eduendday" />
        </v-flex>
      </v-layout>

      <v-layout row wrap justify-center style="margin-top:60px;">
        <v-btn v-on:click="sendEdu(eduagency,edudegree,edustartday,eduendday)" text outlined>등록</v-btn>
      </v-layout>
    </v-container>
  </v-dialog>
</template>

<script>
import FirebaseService from "@/services/FirebaseService";

export default {
  data: () => ({
    edumodal: false,
    eduagency: "", //프로젝트 메인 이미지
    edudegree: "", // 프로젝트 이름
    edustartday: "", //프로젝트 간단 설명
    eduendday: "" // 프로젝트 기간
  }),
  methods: {
    sendEdu(eduagency, edudegree, edustartday, eduendday) {

      var today = new Date();
      var dd = today.getDate(); // 29
      var mm = today.getMonth()+1; // 8
      var yyyy = today.getFullYear(); // 2019
      // 29 8 2019
      // console.log(carstartday, '있냐없냐')
      if (!edustartday) {
        this.$swal({
          title: "시작날짜 지정해주세요.",
          type: "warning",
          confirmButtonColor: "#3085d6",
          cancelButtonColor: "#d33"
        })
        return;
      }

      var endday = eduendday.split('-')
      var filter_eduendday = ""
      // 더 큰 년도를 쓴 경우
      if (endday[0]>yyyy) {
        // console.log('무조건 미래다')
      }
      else {
        // 올해를 쓴 경우
        if (endday[0]==yyyy) {
          // 달이 미래인 경우
          if (endday[1]>mm) {
            // console.log('무조건 미래다')
          }
          else {
            // 달이 이번달인 경우
            if (endday[1]==mm) {
              // 일이 미래인 경우
              if (endday[2]>dd) {
                // console.log('무조건 미래다')
              }
              else {
                // console.log('오늘 또는 과거이다.')
                filter_eduendday = eduendday
              }
            }
            // 달이 더 작은 경우
            else {
              // console.log('무조건 과거다')
              filter_eduendday = eduendday
            }
          }
        }

        // 더 작은 년도를 쓴 경우
        else {
          // console.log('무조건 과거다')
          filter_eduendday = eduendday
        }
      }



      if (!this.eduendday) {
        var Json = new Object();
        Json.Agency = eduagency;
        Json.Degree = edudegree;
        Json.Startday = edustartday;
        Json.Endday = filter_eduendday;
        this.$emit("sendEdu", Json);

        this.eduagency = "";
        this.edudegree = "";
        this.edustartday = "";
        this.eduendday = "";
        this.edumodal = false;
      } else {
        if (this.edustartday > this.eduendday) {
          this.$swal({
            title: "종료일은 시작일 이후로 선택해주세요.",
            type: "warning",
            confirmButtonColor: "#3085d6",
            cancelButtonColor: "#d33"
          });
        } else {
          var Json = new Object();
          Json.Agency = eduagency;
          Json.Degree = edudegree;
          Json.Startday = edustartday;
          Json.Endday = filter_eduendday;
          this.$emit("sendEdu", Json);

          this.eduagency = "";
          this.edudegree = "";
          this.edustartday = "";
          this.eduendday = "";
          this.edumodal = false;
        }
      }
    },
    clearEdu() {
      this.eduagency = "";
      this.edudegree = "";
      this.edustartday = "";
      this.eduendday = "";
      this.edumodal = false;
    }
  }
};
</script>
