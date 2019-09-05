<template>
  <div id="root">

    <div class="topBar">
    </div>



    <div id="leftArea">
      <div v-for="(user, N) in users" :key="N"
        class="children">
        <div class="child">{{user.name}}</div>
      </div>

      <div v-for="(user, N) in users" :key="N"
        class="children2">
        <div class="circle"></div>
      </div>

      <div class="arrowup" @click="downUsers()"></div>
      <div class="arrowdown" @click="upUsers()"></div>
    </div>

    <div id="rightArea">
      <div class="content">
        {{ mainPerson }}
      </div>
    </div>
  </div>
</template>

<script>

let children;

export default {
  name: 'index',

  data() {
    return {
      users: [
        {
          name: 'user1'
        },
        {
          name: 'user2'
        },
        {
          name: 'user3'
        },
        {
          name: 'user4'
        },
        {
          name: 'user5'
        },
        {
          name: 'user6'
        },
        {
          name: 'user7'
        },
        {
          name: 'user8'
        }
      ],
      // domの状態を管理するための配列
      childrenArray: []
    }
  },

  computed: {
    mainPerson: function() {
      let tmp = this.childrenArray.indexOf(3);

      if(tmp == -1) {
        return '';
      }
      else {
        return this.users[tmp].name;
      }
    }
  },

  methods: {
    upUsers: function() {
      if(this.childrenArray[0] > 0) {
        this.childrenArray.unshift(this.childrenArray[0]-1);
        this.childrenArray.pop();
      }
      else {
        this.childrenArray.unshift(0);
        this.childrenArray.pop();
      }

      console.log(this.childrenArray)

      for(let i = 0; i < this.users.length; i++) {
        if(i == this.childrenArray.length-1) {
          console.log("if")
          if(this.childrenArray[i] == 6) {
            console.log(6)
            children[i].classList.remove('child-6');
          }
          else if(this.childrenArray[i+1] == 0) {
            children[i].classList.remove('child-0');
          }
          else {
            console.log(this.childrenArray[i])
            children[i].classList.remove('child-'+(this.childrenArray[i]+1));
          }
        }
        else {
          children[i].classList.remove('child-'+this.childrenArray[i+1])
        }
        children[i].classList.add('child-'+this.childrenArray[i]);
        console.log(children[i].classList)
      }
    },

    downUsers: function() {
      if(this.childrenArray[this.childrenArray.length-1] > 5) {
        this.childrenArray.push(6);
        this.childrenArray.shift();
      }
      else {
        this.childrenArray.push(this.childrenArray[this.childrenArray.length-1]+1);
        this.childrenArray.shift();
      }

      console.log(this.childrenArray)

      for(let i = this.users.length-1; i > -1; i--) {
        if(i == 0) {
          console.log("if")
          if(this.childrenArray[i] == 0) {
            children[i].classList.remove('child-0');
          }
          else if(this.childrenArray[i-1] == 6) {
            children[i].classList.remove('child-6');
          }
          else {
            children[i].classList.remove('child-'+(this.childrenArray[i]-1))
            console.log(this.childrenArray[i]);
          }
        }
        else {
          console.log("else")
          children[i].classList.remove('child-'+this.childrenArray[i-1])
        }
        children[i].classList.add('child-'+this.childrenArray[i]);
        //console.log(children[i].classList)
      }
    }
  },

  mounted: function() {
    // domを取得する
    for(let i = 0; i < this.users.length; i++) {
      children = document.getElementsByClassName("children");
      this.childrenArray.push(6);
      children[i].classList.add('child-'+this.childrenArray[i])
    }

    for(let i = 0; i < 5; i++) {
      this.upUsers();
    }
  }
},

</script>

<style lang="scss" scoped>

#root {
  height: 100vh;
  overflow: hidden;

  .topBar {
    position: absolute;

    top: 0;
    left: 0;

    width: 100vw;
    height: 100px;

    background: -moz-linear-gradient(top, $primary_color, $secondary_color);
    background: -webkit-linear-gradient(top, $primary_color, $secondary_color);
    background: linear-gradient(to bottom, $primary_color, $secondary_color);
  }

  #leftArea {
    position: absolute;

    top: 100px;
    left: 0;

    height: calc(100vh - 100px);
    width: 45vw;

    background: radial-gradient($light_gray, $middle_gray);
    background: -webkit-radial-gradient($light_gray, $middle_gray);
    background: -moz-radial-gradient($light_gray, $middle_gray);

    .arrowup {
      position: absolute;

      left: 44%;
      top: -2%;

      width: 0;
      height: 0;

      border-top: solid 40px transparent;
      border-right: solid 40px transparent;
      border-left: solid 40px transparent;
      border-bottom: solid 40px #697b91;

      cursor: pointer;
    }

    .arrowup:hover {
      border-bottom: solid 40px #90abcc;
    }

    .child {
      position: absolute;

      left: 50%;
      top: 50%;

      transform: translate(-50%, -50%);
      -webkit-transform: translate(-50%, -50%);
      -moz-transform: translate(-50%, -50%);

      text-align: center;

      transition: .1s;
    }

    .children {
      transition: .3s;
    }

    .child-0 {
      position: absolute;

      top: 5%;
      left: 50%;

      transform: translate(-50%, -50%);
      -webkit-transform: translate(-50%, -50%);
      -moz-transform: translate(-50%, -50%);

      visibility: hidden;
    }

    .child-1 {
      position: absolute;

      top: 18%;
      left: 50%;

      transform: translate(-50%, -50%);
      -webkit-transform: translate(-50%, -50%);
      -moz-transform: translate(-50%, -50%);

      background-color: #757575;

      width: 30%;
      height: 11%;

      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.8);
    }

    .child-2 {
      position: absolute;

      top: 32%;
      left: 50%;

      transform: translate(-50%, -50%);
      -webkit-transform: translate(-50%, -50%);
      -moz-transform: translate(-50%, -50%);

      width: 50%;
      height: 14%;

      background-color: #bdbdbd;

      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.8);
    }

    .child-3 {
      position: absolute;

      top: 50%;
      left: 50%;

      transform: translate(-50%, -50%);
      -webkit-transform: translate(-50%, -50%);
      -moz-transform: translate(-50%, -50%);

      width: 70%;
      height: 17%;

      background-color: #fff;

      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.8);
    }

    .child-4 {
      position: absolute;

      top: 68%;
      left: 50%;

      transform: translate(-50%, -50%);
      -webkit-transform: translate(-50%, -50%);
      -moz-transform: translate(-50%, -50%);

      width: 50%;
      height: 14%;

      background-color: #bdbdbd;

      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.8);
    }

    .child-5 {
      position: absolute;

      top: 82%;
      left: 50%;

      transform: translate(-50%, -50%);
      -webkit-transform: translate(-50%, -50%);
      -moz-transform: translate(-50%, -50%);

      background-color: #757575;

      width: 30%;
      height: 11%;

      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.8);
    }

    .child-6 {
      position: absolute;

      top: 95%;
      left: 50%;

      transform: translate(-50%, -50%);
      -webkit-transform: translate(-50%, -50%);
      -moz-transform: translate(-50%, -50%);

      visibility: hidden;
    }

    .circle{
      display: inline-block;
      width: 80px;
      height: 80px;
      text-align:center;
      line-height: 80px;
      border-radius: 50%;
      border: solid 3px skyblue;
    }

    .circle-3{
      width: 80px;
      height: 80px;
      border-radius: 50%;
      background: skyblue;/*背景色*/
    }

    .arrowdown {
      position: absolute;

      left: 44%;
      bottom: -2%;

      width: 0;
      height: 0;

      border-bottom: solid 40px transparent;
      border-right: solid 40px transparent;
      border-left: solid 40px transparent;
      border-top: solid 40px #697b91;

      cursor: pointer;
    }

    .arrowdown:hover {
      border-top: solid 40px #90abcc;
    }
  }

  #rightArea {
    position: absolute;

    top: 100px;
    right: 0;

    height: calc(100vh - 100px);
    width: 55vw;

    background: -moz-linear-gradient(top, $dark_primary, $light_primary);
    background: -webkit-linear-gradient(top, $dark_primary, $light_primary);
    background: linear-gradient(to bottom, $dark_primary, $light_primary);

    .content {
      position: absolute;

      top: 12%;
      left: 7%;

      width: 86%;
      height: 76%;

      background-color: $light_gray;
    }
  }
}
</style>
