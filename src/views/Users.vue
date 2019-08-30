<template>
  <v-container wrap>
    <div style="margin-top:56px">
      <div style="padding:3% 5%; border:2px solid grey; border-radius:15px; width:100%;">

        <v-layout wrap row justify-center style="margin-bottom:20px;">
          <v-flex xs12 class="text-center">
            <h1 class="text-center"><span class="fontHannaAir">개발자들</span></h1>
            <v-chip color="orange"  class="white--text headline" style="padding:0 28px; cursor:pointer">
              <span class="fontYanolja ">랜덤 개발자 여행</span>
            </v-chip>
          </v-flex>
        </v-layout>

        <v-layout row wrap justify-center style="margin:40px 0;">
          <v-flex xs10>
            <v-text-field v-model="input" placeholder="검색어를 입력하세요!"/>
          </v-flex>
        </v-layout>


        <v-layout wrap row>
          <v-flex xs12 sm6 md4 v-for="user in users" v-if="user.userName.includes(input) || user.userIntro.includes(input)" style="padding:10px; position:relative">
            <router-link :to="{ name: 'story', params: { id: user.nickname }}" style="text-decoration:none; cursor:pointer;">
              <v-card style="height:200px; width:100%;" outlined>
                <v-img class="white--text" height="100px" :src="user.storyBanner"/>
                <div>
                    <v-avatar color="indigo" size="75" style="position: absolute; top: 33%; right: 2vw;">
                      <v-img :src="user.userImage || 'http://design-ec.com/d/e_others_50/l_e_others_500.png'"/>
                    </v-avatar>


                </div>
                <div style="margin:10px 0 0 15px;">
                  <span class="title"><span class="fontNanum">{{user.nickname}}</span></span>
                  <br/>
                  <span class="overline grey--text">
                    <span class="fontNanum">{{user.userIntro}}</span>
                  </span>
                </div>
              </v-card>
            </router-link>
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
      users: [],
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
      this.users = await FirebaseService.SELECT_ALLUser();
      console.log(this.users);
    },
  },
};
</script>
