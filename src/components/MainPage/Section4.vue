<template>
  <div class="section">
    <v-layout row wrap justify-center style="height:60%; padding:0% 20%">
      <v-flex xs6 v-show="!showUpRecruit">
        <v-flex xs12 text-center v-show="!showUpRecruit">
          <span class="sm-link sm-link_padding-bottom sm-link3" style="height:7%" @mouseover="showUpCompanyList=true" @mouseleave="showUpCompanyList=false">
            <span class="sm-link__label">  <span class="display-1"> <span class="fontjua"> 개발자들 </span> </span> </span>
          </span>
        </v-flex>
        <v-flex xs12 text-center v-show="!showUpRecruit">
          <router-link :to="{ name: 'users' }" class="bannerBtn">
            <div class="bannerBtn sm-link sm-link_padding-all sm-link1">
              <div class="sm-link__label" @mouseover="showUpCompanyList=true" @mouseleave="showUpCompanyList=false">
                <i class="fas fa-users fa-9x"></i><br/>
                <span class="content"> <span class="fontjua">사용자 둘러보기</span></span>
              </div>
            </div>
          </router-link>
        </v-flex>
      </v-flex>
      <v-flex xs6 v-show="showUpRecruit" style="margin-top:10%">
        <v-flex xs12 text-center text-white>
          <span class="headline"> <span class="fontjua" style="color:white;">
            여러 개발자들을 소개합니다.<br/>
            다양한 사람들과 관계를 맺고 정보를 얻어보세요.
          </span> </span>
        </v-flex>
      </v-flex>
      <v-flex v-show="!showUpCompanyList">
        <v-flex xs12 text-center v-show="!showUpCompanyList">
          <span class="sm-link sm-link_padding-bottom sm-link3" style="height:7%" @mouseover="showUpRecruit=true" @mouseleave="showUpRecruit=false">
            <span class="sm-link__label"><span class="display-1"> <span class="fontjua"> 프로젝트들 </span></span> </span>
          </span>
        </v-flex>
        <v-flex xs12 text-center v-show="!showUpCompanyList">
          <router-link :to="{ name: 'projectlist' }" class="bannerBtn">
            <div class="bannerBtn sm-link sm-link_padding-all sm-link1" @mouseover="showUpRecruit=true" @mouseleave="showUpRecruit=false">
              <div class="sm-link__label">
                <i class="far fa-handshake fa-9x"/><br/>
                <span class="content"> <span class="fontjua">프로젝트 둘러보기</span></span>
              </div>
            </div>
          </router-link>
        </v-flex>
      </v-flex>
      <v-flex xs6 v-show="showUpCompanyList" style="margin-top:10%">
        <v-flex xs12 text-center>
          <span class="headline"> <span class="fontjua" style="color:white;">
            개발자들이 올린 프로젝트리스트입니다. <br/>
            여러 프로젝트를 확인하고 댓글을 남겨보세요.
          </span></span>
        </v-flex>
      </v-flex>
    </v-layout>
    <v-layout row justify-center>
      <img src="../../assets/companyListImg.png" style="position:absolute;bottom:0%"/>
    </v-layout>
  </div>
</template>



<script>
import FirebaseService from "@/services/FirebaseService";
import Vue from "vue";

export default {
  name: "section2",
  components: {
  },
  data() {
    return {
      showUpCompanyList:false,
      showUpRecruit:false,
    }
  },
  created() {},
  methods: {}
};
</script>
