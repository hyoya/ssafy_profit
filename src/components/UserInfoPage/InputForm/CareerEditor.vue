<template>
  <v-dialog v-model="careermodal" max-width="600px">
    <template v-slot:activator="{ on }">
      <img src="../../../assets/icon_set/pencil.png" alt="edit" style="cursor:pointer;" v-on="on" />
    </template>

    <v-container class="inputmodal">
      <v-layout row wrap style="padding:10px 20px;">
        <v-spacer />
        <span class="font-weight-regular headline">경력 추가</span>
        <v-spacer />
        <div @click="clearCar">
          <i class="fa fa-close" />
        </div>
      </v-layout>

      <v-layout row justify-center wrap>
        <v-flex xs10 sm5>
          <p class="subheading font-weight-bold text-center">*회사명</p>
          <v-text-field single-line v-model="carcompany" />
        </v-flex>
        <v-flex xs10 sm5 offset-sm1>
          <p class="subheading font-weight-bold text-center">직책 직무</p>
          <v-text-field single-line v-model="carposition" />
        </v-flex>
      </v-layout>

      <v-layout row wrap justify-center>
        <v-flex xs5>
          <span class="subheading font-weight-bold">시작일</span>
          &nbsp;&nbsp;&nbsp;
          <input type="date" v-model="carstartday" />
        </v-flex>
        <v-flex xs5 offset-sm1>
          <span class="subheading font-weight-bold">종료일</span>
          &nbsp;&nbsp;&nbsp;
          <input type="date" v-model="carendday" />
        </v-flex>
      </v-layout>

      <v-layout row wrap justify-center style="margin-top:25px;">
        <v-flex xs11>
          <p class="subheading font-weight-bold text-center">설명</p>
          <v-textarea outlined v-model="cardescription" />
        </v-flex>
      </v-layout>

      <v-layout row wrap justify-center>
        <v-btn
          v-on:click="sendCar(carcompany,carposition,carstartday,carendday,cardescription)"
          text
          outlined
        >등록</v-btn>
      </v-layout>
    </v-container>
  </v-dialog>
</template>

  <script>
export default {
  data: () => ({
    careermodal: false,
    carcompany: "",
    carposition: "",
    carstartday: "",
    carendday: "",
    cardescription: ""
  }),
  methods: {
    sendCar(carcompany, carposition, carstartday, carendday, cardescription) {
      var today = new Date();
      var dd = today.getDate(); // 29
      var mm = today.getMonth()+1; // 8
      var yyyy = today.getFullYear(); // 2019
      // 29 8 2019
      // console.log(carstartday, '있냐없냐')
      if (!carstartday) {
        this.$swal({
          title: "시작날짜 지정해주세요.",
          type: "warning",
          confirmButtonColor: "#3085d6",
          cancelButtonColor: "#d33"
        })
        return;
      }

      var endday = carendday.split('-')
      var filter_carendday = ""
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
                filter_carendday = carendday
              }
            }
            // 달이 더 작은 경우
            else {
              // console.log('무조건 과거다')
              filter_carendday = carendday
            }
          }
        }

        // 더 작은 년도를 쓴 경우
        else {
          // console.log('무조건 과거다')
          filter_carendday = carendday
        }
      }


      if (!this.carendday) {
        var Json = new Object();
        Json.Company = carcompany;
        Json.Position = carposition;
        Json.Startday = carstartday;
        Json.Endday = filter_carendday;
        Json.Description = cardescription;
        this.$emit("sendCar", Json);

        this.carcompany = "";
        this.carposition = "";
        this.carstartday = "";
        this.carendday = "";
        this.cardescription = "";
        this.careermodal = false;
      } else {
        if (this.carstartday > this.carendday) {
          this.$swal({
            title: "종료일은 시작일 이후로 선택해주세요.",
            type: "warning",
            confirmButtonColor: "#3085d6",
            cancelButtonColor: "#d33"
          })
        } else {
          var Json = new Object();
          Json.Company = carcompany;
          Json.Position = carposition;
          Json.Startday = carstartday;
          Json.Endday = filter_carendday;
          Json.Description = cardescription;
          this.$emit("sendCar", Json);

          this.carcompany = "";
          this.carposition = "";
          this.carstartday = "";
          this.carendday = "";
          this.cardescription = "";
          this.careermodal = false;
        }
      }
    },
    clearCar() {
      this.carcompany = "";
      this.carposition = "";
      this.carstartday = "";
      this.carendday = "";
      this.cardescription = "";
      this.careermodal = false;
    }
  }
};
</script>
