# SSAFY 1차 프로젝트 -  웹/모바일

안녕하세요. 여기에는 웹/모바일 프로젝트에 관한 내용을 다룹니다. 

backend 로는 firebase 를 사용, frontend 로는 vue 를 사용하였습니다.

설치 방법 은 아래의 개요에서 자세히 다루도록 하겠습니다.

만약 당신이 설치를 성공적으로 했다면, 해당 페이지가 뜨는 것을 볼 수 있습니다.

![메인페이지](sample_image\메인페이지.png)



## 개요

1. 환경 설정

2. 프로젝트 설명 ( 추후 작성할 예정)



## 1. 환경 설정

- clone

  ```
  $ git clone https://lab.ssafy.com/Kim-Seul-Gi/webmobile-final.git
  ```

- 해당 repository 로 이동

  ```
  $ cd webmobile-final
  ```

- npm 설치

  ```
  $ npm install
  ```

- node_moduls 코드 일부 수정 (node_modules/vue-burger-menu/dist/vue-burger-menu.common.js) / 코드 수정 전,후 이미지 아래부분에 있습니다.

  ```
  - 2182줄에 있는 Menuvue_type_template_id_6fc94ece_render 라는 변수가 아래와 같이 정의되 있을 것입니다. 
  
  var Menuvue_type_template_id_6fc94ece_render = function () {var _vm=this;var _h=_vm.$createElement;var _c=_vm._self._c||_h;return _c('div',[_c('div',{ref:"sideNav",staticClass:"bm-menu"},[_c('nav',{staticClass:"bm-item-list"},[_vm._t("default")],2),_c('span',{staticClass:"bm-cross-button cross-style",class:{ hidden: !_vm.crossIcon },on:{"click":_vm.closeMenu}},_vm._l((2),function(x,index){return _c('span',{key:x,staticClass:"bm-cross",style:({ position: 'absolute', width: '3px', height: '14px',transform: index === 1 ? 'rotate(45deg)' : 'rotate(-45deg)'})})}))]),_c('div',{ref:"bmBurgerButton",staticClass:"bm-burger-button",class:{ hidden: !_vm.burgerIcon },on:{"click":_vm.openMenu}},_vm._l((3),function(x,index){return _c('span',{key:index,staticClass:"bm-burger-bars line-style",style:({top:20 * (index * 2) + '%'})})}))])}
  
  - 위를 지워주시고, 아래의 내용을 복사붙여넣기 해주세요
  
  var Menuvue_type_template_id_6fc94ece_render = function () {var _vm=this;var _h=_vm.$createElement;var _c=_vm._self._c||_h;return _c('div',[_c('div',{ref:"sideNav",staticClass:"bm-menu"},[_c('nav',{staticClass:"bm-item-list"},[_vm._t("default")],2),_c('span',{staticClass:"bm-cross-button cross-style",class:{ hidden: !_vm.crossIcon },on:{"click":_vm.closeMenu}},_vm._l((1),function(x,index){return _c('i',{key:x,staticClass:"fa fa-caret-right",style:({ position: 'absolute', width: '3px', height: '14px'})})}))]),_c('div',{ref:"bmBurgerButton",staticClass:"bm-burger-button",class:{ hidden: !_vm.burgerIcon },on:{"click":_vm.openMenu}},_vm._l((1),function(x,index){return _c('i',{key:index,staticClass:"fa fa-caret-left line-style studiopop",style:({top:20 * (index * 2) + '%' } )})}))])}
  ```



- 코드 수정 전

![코드 수정 전](sample_image\코드 수정 전.png)



- 코드 수정 후

![코드 수정 후](sample_image\코드 수정 후.png)



- 서버 실행시키기

  ```
  $ npm run serve
  ```



- 아래와 같은 문구가 뜬다면 성공!

  ```
   App running at:
    - Local:   http://localhost:8080/
    - Network: http://192.168.31.60:8080/
  ```

  