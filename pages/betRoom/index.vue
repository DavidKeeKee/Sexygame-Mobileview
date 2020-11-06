<template>
 <v-container class="pa-0 ml-1 wrapper" fluid style="background-color:black">



<v-row class="pa-0 v-wrap" style="height:96vh;" no-gutters>
   <v-img v-show="showImage" width="3vw" height="3vw" contain :style="{ left: page.left+ 'vw', top: page.top+ 'px' ,position:'absolute','z-index':1000}" :src="'/coin/'+betCoin"/>
  <TutorialBetroom1 @close="tutorial=false" v-if="tutorial"/>
    <v-col class="pa-0 playTable_mview" cols="7">
        <div class="playTable" id="v-step-0">
           <v-btn class="mx-2"  dark small color="#4F3C2B" style="position:absolute;bottom:1%;left:0" link to="/betRoom/betRoom2">
              <v-icon dark>picture_in_picture</v-icon>
            </v-btn>
            <v-btn class="mx-2 switch_video"  dark small color="#4F3C2B">
              <v-icon dark>switch_video</v-icon>
            </v-btn>
            <v-btn class="mx-2"  dark small color="#4F3C2B" style="position:absolute;bottom:1%;right:0">
              <v-icon dark>fullscreen</v-icon>
            </v-btn>
            <div class="room-title d-flex justify-center align-center white--text">
                    Baccrart C01
            </div>
              <v-avatar
                    color="rgba(0,0,0,0.5)"
                    :size="avatar_size"
                    class="gameCountDown"
                    v-show="true">
                        <v-progress-circular
                        :value="70"
                        color="red"
                        :size="progress_size"

                        >
                    <span> 60</span>
                    </v-progress-circular>
                </v-avatar>
        </div>
       <!--beting play section-->
        <v-tabs
        background-color="#404040"
        class="elevation-2"
        centered
        grow
        dark
        height="4vh"
        hide-slider
        active-class="tabActive black--text"
      >


              <v-tab
                :href="`#tab-1`"
                style="color:#F7D9AB;"


              >
               <span class="elevation_font"> Baccarat</span>
              </v-tab>
              <v-tab
                :href="`#tab-2`"
                style="color:#F7D9AB;"
              >
                <span class="elevation_font">  No Commission</span>
              </v-tab>
              <v-tab
                :href="`#tab-3`"
                style="color:#F7D9AB;"
              >
                <span class="elevation_font">  Cow Cow</span>
              </v-tab>

              <v-tab-item
                :value="'tab-' + 1"
              >
              <v-card
                  flat
                  tile
                  class="playArea"
                   @mouseenter="showImage = true"
                       @mousemove="onMouseMove"
                        @mouseleave="showImage = false"
                >
                <div class="d-flex justify-center align-center stopBetting" v-if="false">

                  Stop Betting
                </div>
                <div class="d-flex flex-column justify-center align-center bettingSuccess" v-if="true">
                   <v-icon color="green" size="60">done</v-icon>
                   Betting Success
                </div>

                  <v-row class="row_playArea">
                    <v-col tile cols="4" class="playArea-tile" style="position:relative" align="center" @click="placeBet='player'">
                      <h1> Player</h1>
                        <h2>1:1</h2>
                         <v-img v-if="PlacedBets.some((item)=>item.bet=='player')"
                           class="show_img_coin"
                          contain
                          :src="'/coin/'+betCoin"/>
                        <div class="betConfirm" v-if="placeBet=='player'">
                          <v-img class="click_img" contain src="/coin/黑色籌碼.png"/>
                           <v-row justify="center">
                              <v-img src="/icon/萬用選擇UI.png"
                                            @click.stop="placeBet=null"
                                            class="click_img_stop"
                                            ></v-img>

                                          <!-- </v-btn> -->
                                          <v-img src="/icon/萬用取消UI.png"
                                            @click.stop="confirmBet('player')"
                                            class="click_img_confirm"
                                            ></v-img>
                           </v-row>

                        </div>
                    </v-col>
                    <v-col tile cols="4" class="pa-0" align="center" >
                      <div class="tie tie1 playArea-tile " @click="placeBet='tie'" >
                        <h2> Tie</h2>
                        <h2>8:1</h2>
                         <v-img v-if="PlacedBets.some((item)=>item.bet=='tie')"
                          class="show_img_coin"
                          contain
                          :src="'/coin/'+betCoin"/>
                        <div class="betConfirm" v-if="placeBet=='tie'">
                          <v-img class="click_img" contain src="/coin/黑色籌碼.png"/>
                           <v-row justify="center">
                              <v-img src="/icon/萬用選擇UI.png"
                                            @click.stop="placeBet=null"
                                            class="click_img_stop"
                                            ></v-img>

                                          <!-- </v-btn> -->
                                          <v-img src="/icon/萬用取消UI.png"
                                            @click.stop="confirmBet('tie')"
                                            class="click_img_confirm"
                                            ></v-img>
                           </v-row>

                        </div>
                      </div>
                      <div  class="tie playArea-tile " @click="placeBet='luckySix'">
                        <h2> Lucky Six</h2>
                        <h2> 12:1 / 20:1</h2>
                            <v-img v-if="PlacedBets.some((item)=>item.bet=='luckySix')"
                         class="show_img_coin"
                          contain
                          :src="'/coin/'+betCoin"/>
                        <div class="betConfirm" v-if="placeBet=='luckySix'">
                          <v-img class="click_img" contain src="/coin/黑色籌碼.png"/>
                           <v-row justify="center">
                              <v-img src="/icon/萬用選擇UI.png"
                                            @click.stop="placeBet=null"
                                            class="click_img_stop"
                                            ></v-img>

                                          <!-- </v-btn> -->
                                          <v-img src="/icon/萬用取消UI.png"
                                            @click.stop="confirmBet('luckySix')"
                                            class="click_img_confirm"
                                            ></v-img>
                           </v-row>

                        </div>
                      </div>
                    </v-col>
                    <v-col tile cols="4" class="playArea-tile banker" align="center" @click="placeBet='banker'">
                      <h1> Banker</h1>
                        <h2>0.95:1</h2>
                         <v-img v-if="PlacedBets.some((item)=>item.bet=='banker')"
                         class="show_img_coin"
                          contain
                          :src="'/coin/'+betCoin"/>
                        <div class="betConfirm" v-if="placeBet=='banker'">
                          <v-img class="click_img" contain src="/coin/黑色籌碼.png"/>
                           <v-row justify="center">
                              <v-img src="/icon/萬用選擇UI.png"
                                            @click.stop="placeBet=null"
                                            class="click_img_stop"
                                            ></v-img>

                                          <!-- </v-btn> -->
                                          <v-img src="/icon/萬用取消UI.png"
                                            @click.stop="confirmBet('banker')"
                                            class="click_img_confirm"
                                            ></v-img>
                           </v-row>

                        </div>
                    </v-col>
                  </v-row>
                  <v-row style="height:45%;width:100%; margin:0">
                    <v-col tile cols="3" class="playArea-tile1" align="center" @click="placeBet='pp'">
                        <h1>Player Pair</h1>
                        <h2>11:1</h2>
                          <v-img v-if="PlacedBets.some((item)=>item.bet=='pp')"
                          class="show_img_coin"
                          contain
                          :src="'/coin/'+betCoin"/>
                        <div class="betConfirm" v-if="placeBet=='pp'">
                          <v-img class="click_img" contain src="/coin/黑色籌碼.png"/>
                           <v-row justify="center">
                              <v-img src="/icon/萬用選擇UI.png"
                                            @click.stop="placeBet=null"
                                            class="click_img_stop"
                                            ></v-img>

                                          <!-- </v-btn> -->
                                          <v-img src="/icon/萬用取消UI.png"
                                            @click.stop="confirmBet('pp')"
                                            class="click_img_confirm"
                                            ></v-img>
                           </v-row>

                        </div>
                    </v-col>
                    <v-col tile cols="3" class="playArea-tile1" align="center" @click="placeBet='pn'">
                        <h1>Player Natural</h1>
                        <h2>7:2</h2>
                         <v-img v-if="PlacedBets.some((item)=>item.bet=='pn')"
                          class="show_img_coin"
                          contain
                          :src="'/coin/'+betCoin"/>
                        <div class="betConfirm" v-if="placeBet=='pn'">
                          <v-img class="click_img" contain src="/coin/黑色籌碼.png"/>
                           <v-row justify="center">
                              <v-img src="/icon/萬用選擇UI.png"
                                            @click.stop="placeBet=null"
                                            class="click_img_stop"
                                            ></v-img>

                                          <!-- </v-btn> -->
                                          <v-img src="/icon/萬用取消UI.png"
                                            @click.stop="confirmBet('pn')"
                                            class="click_img_confirm"
                                            ></v-img>
                           </v-row>

                        </div>
                    </v-col>
                    <v-col tile cols="3" class="playArea-tile1 banker" align="center" @click="placeBet='bn'">
                        <h1>Banker Natural</h1>
                        <h2>7:2</h2>
                         <v-img v-if="PlacedBets.some((item)=>item.bet=='bn')"
                          class="show_img_coin"
                          contain
                          :src="'/coin/'+betCoin"/>
                        <div class="betConfirm" v-if="placeBet=='bn'">
                          <v-img class="click_img" contain src="/coin/黑色籌碼.png"/>
                           <v-row justify="center">
                              <v-img src="/icon/萬用選擇UI.png"
                                            @click.stop="placeBet=null"
                                            class="click_img_stop"
                                            ></v-img>

                                          <!-- </v-btn> -->
                                          <v-img src="/icon/萬用取消UI.png"
                                            @click.stop="confirmBet('bn')"
                                            class="click_img_confirm"
                                            ></v-img>
                           </v-row>

                        </div>
                    </v-col>
                    <v-col tile cols="3" class="playArea-tile1 banker" align="center" @click="placeBet='bp'">
                        <h1>Banker Pair</h1>
                        <h2>11:1</h2>
                         <v-img v-if="PlacedBets.some((item)=>item.bet=='bp')"
                          class="show_img_coin"
                          contain
                          :src="'/coin/'+betCoin"/>
                        <div class="betConfirm" v-if="placeBet=='bp'">
                          <v-img class="click_img" contain src="/coin/黑色籌碼.png"/>
                           <v-row justify="center">
                              <v-img src="/icon/萬用選擇UI.png"
                                            @click.stop="placeBet=null"
                                            class="click_img_stop"
                                            ></v-img>

                                          <!-- </v-btn> -->
                                          <v-img src="/icon/萬用取消UI.png"
                                            @click.stop="confirmBet('bp')"
                                            class="click_img_confirm"
                                            ></v-img>
                           </v-row>

                        </div>
                    </v-col>
                  </v-row>

              </v-card>

              </v-tab-item>
                <v-tab-item
                :value="'tab-' + 2"
              >
              <v-card
                  flat
                  tile
                  class="playArea"
                >

                  <v-row >
                    <v-col tile cols="4" class="playArea-tile" align="center">
                      <h1> Playerr</h1>
                        <h2>1:1</h2>
                    </v-col>
                    <v-col tile cols="4" class="playArea-tile pa-0" align="center">
                      <div class="tie tie1">
                        <h2> Tie</h2>
                        <h2>8:1</h2>
                      </div>
                      <div  class="tie">
                        <h2> Lucky Six</h2>
                        <h2> 12:1 / 20:1</h2>
                      </div>
                    </v-col>
                    <v-col tile cols="4" class="playArea-tile banker" align="center">
                      <h1> Banker</h1>
                        <h2>1:1</h2>
                    </v-col>
                  </v-row>
                  <v-row style="height:48%;width:100%; margin:0">
                    <v-col tile cols="3" class="playArea-tile1" align="center">
                        <h1>Player Pair</h1>
                        <h2>11:1</h2>
                    </v-col>
                    <v-col tile cols="3" class="playArea-tile1" align="center">
                        <h1>Player Natural</h1>
                        <h2>7:2</h2>
                    </v-col>
                    <v-col tile cols="3" class="playArea-tile1 banker" align="center">
                        <h1>Banker Natural</h1>
                        <h2>7:2</h2>
                    </v-col>
                    <v-col tile cols="3" class="playArea-tile1 banker" align="center">
                        <h1>Banker Pair</h1>
                        <h2>11:1</h2>
                    </v-col>
                  </v-row>

              </v-card>
              </v-tab-item>
                <v-tab-item
                :value="'tab-' + 3"
              >
                <v-card
                  flat
                  tile
                  class="playArea"
                >

                    <v-row style="height:100%;width:100%; margin:0">
                        <v-col tile cols="4" class="playArea-tile" align="center">
                          <h1> Player</h1>
                            <h2>1:1</h2>
                        </v-col>
                        <v-col tile cols="4" class="playArea-tile" align="center">

                            <h2> Tie</h2>
                            <h2>8:1</h2>

                        </v-col>
                        <v-col tile cols="4" class="playArea-tile banker" align="center">
                          <h1> Banker</h1>
                            <h2>1:1</h2>
                        </v-col>
                  </v-row>

                </v-card>
              </v-tab-item>
      </v-tabs>
       <!--total bet amount-->
          <div
            style="height:4vh ;background-color:#023016;"
            class="d-flex justify-center align-center white--text bet_amount"
            >
                Total BetAmount : 0.0

          </div>
        <!--betcoin selection-->
        <div class="selectCoin d-flex align-center white--text pa-2" >

                            <v-menu
                              offset-y
                              top
                              :close-on-content-click="false"
                              v-model="coinMenu"
                              :nudge-width="450"
                              :max-width="450"
                              dark
                              >
                                  <template v-slot:activator="{ on, attrs }">
                                                  <div class="text-center mt-1 mx-2 logo_coin_select"
                                                  v-bind="attrs"
                                                    v-on="on"
                                                    @click="openCoinSelect">


                                                  </div>
                                  </template>
                                  <v-card color='rgba(0, 0, 0, 0.7)' elevation="20" class="card_icon">
                                    <v-card-title>
                                      <v-row no-gutters justify="center"> Please Select


                                      </v-row>
                                      </v-card-title>
                                      <v-row no-gutters justify="center">
                                          <v-img
                                                v-for="(coin,n) in coinList" :key="n"
                                                class="text-center card_icon_img"
                                                :src="'/coin/'+coin"
                                              >
                                                <div class="checkbox_size">
                                                    <v-checkbox v-model="selectedCoin"
                                                 :value="coin"
                                                 color="#009167"
                                                 :disabled="disableCoinSelect?selectedCoin.includes(coin)?false:true:false"
                                                 ></v-checkbox>
                                                </div>
                                              </v-img>

                                      </v-row>
                                    <v-card-actions >
                                    <v-row justify="center">
                                      <!-- <v-btn small class="mx-2" fab dark color="#4f3c2b" @click="cancelCoinSelect"> -->

                                        <div class="justify_cancelCoinSelect">
                                          <v-img src="/icon/萬用選擇UI.png"
                                        @click="cancelCoinSelect"
                                        class="ma-2 cancel_coinSelect"
                                        ></v-img>
                                        </div>

                                      <div class="justify_changeShowing">
                                      <!-- </v-btn> -->
                                      <v-img src="/icon/萬用取消UI.png"
                                        @click="changeShowing"
                                        class="ma-2 change_showing"
                                       ></v-img>
                                        </div>

                                    </v-row>
                                    </v-card-actions>
                                  </v-card>

                            </v-menu>
                            <v-img :src="betCoin==coin?'/coin/籌碼發光.png':''"
                                  @click="betCoin=coin"
                                  v-for="(coin,n) in showingCoin"
                                  :key="n"
                                  :max-width='coinimg_width'
                                  :height='coin_height_size'
                                  >

                                      <v-row
                                        class="fill-height ma-0"
                                        align="center"
                                        justify="center"
                                      >
                                        <v-img
                                              :max-width="coin_img_width"
                                              max-height="coin_img_height"
                                              :src="'/coin/'+coin"


                                              >
                                        </v-img>
                                      </v-row>

                            </v-img>
                              <div class="text-center mt-1 ml-2 coin_x2">


                                </div>


        </div>
    </v-col>
    <!--betroom detail-->
    <v-col cols="5" class="pa-0">
     <BetRoom1Tableinfo />
  <v-row no-gutters>
    <v-col cols="9">
      <!--betroom history and other betrooms history-->
      <BetHistory />
    </v-col>
    <v-col cols="3" class="betroom_slidetable">
      <BetRoom1SideTable  />

    </v-col>
  </v-row>



    </v-col>

</v-row>

      <button v-show="!drawer" class="Custombutton"  style="" @click="drawer=true" >
        <p class="py-5" style="writing-mode: vertical-rl;text-orientation: upright;letter-spacing:-2px;font-size:0.8vw">
          tables
        </p>
      </button>


  <TableDrawer :drawer="drawer"  @close="drawer=false"/>
 </v-container>

</template>

<script>
// import previewTable from '@/components/previewTable';
// import tableDrawer from '@/components/tableDrawer';
export default {
  // components:{
  //       previewTable,
  //       tableDrawer
  //   },
   mounted () {

    },
    computed:{
      disableCoinSelect(){
        if(this.selectedCoin.length==5){
          return true
        }else{
        return false
         }
      },
        progress_size () {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs': return 50
          case 'sm': return 50
          case 'md': return 100
          case 'lg': return 100
          case 'xl': return 100
        }
      },
      avatar_size() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs': return 70
          case 'sm': return 70
          case 'md': return 130
          case 'lg': return 130
          case 'xl': return 130
        }
      },
      coinimg_width() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs': return 48
          case 'sm': return 48
          case 'md': return 92
          case 'lg': return 92
          case 'xl': return 92
        }
      },
      coin_height_size() {
       switch (this.$vuetify.breakpoint.name) {
          case 'xs': return 44
          case 'sm': return 44
          case 'md': return 60
          case 'lg': return 60
          case 'xl': return 60
        }
      },
      coin_img_width() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs': return 42
          case 'sm': return 42
          case 'md': return 70
          case 'lg': return 70
          case 'xl': return 70
        }
      },
      coin_img_height() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs': return 22
          case 'sm': return 22
          case 'md': return 90
          case 'lg': return 90
          case 'xl': return 90
        }
      }

    },
  data () {
    return {
      PlacedBets:[],
      placeBet:'',
      page:{left: 170,top:0},
      showImage:false,
      tutorial:true,
      drawer:false,
      coinMenu:false,
      selectedCoin:[],
      showingCoin:['5籌碼.png','10K籌碼.png','10籌碼.png','20K籌碼.png','50籌碼.png'],
      coinList:['5籌碼.png','10K籌碼.png','10籌碼.png','20K籌碼.png','20籌碼.png','50籌碼.png','100籌碼.png',
                '200籌碼.png','500籌碼.png','1000籌碼.png','2000籌碼.png','5000籌碼.png'],
      betCoin:'5籌碼.png',
            }
            },

  methods:{
    confirmBet(bet){
      this.PlacedBets.push({bet:bet,amount:'50'})
      this.placeBet=''
    },
     onMouseMove(e) {
                console.log('page x: ',  e.pageX*100/window.screen.width, e.clientY);
                console.log(window.screen.width)
                this.page.left = (e.pageX*100/window.screen.width)-7;
                this.page.top = e.pageY;
            },
      changeShowing(){
          this.showingCoin=[...this.selectedCoin]
          this.coinMenu=false
        },
      openCoinSelect(){
        this.selectedCoin=[...this.showingCoin]
      },
      cancelCoinSelect(){
        this.selectedCoin=[]
        this.coinMenu=false
      }
  }
}
</script>
<style scoped>
.betConfirm{
  position:absolute;
  width:100%;
  height:100%;
  top:50%;
  left:50%;
  transform:translate(-50%,-50%);
  z-index: 20;
}
  .stopBetting{
    font-size:0.8vw;
    width:20%;
    height:30%;
    background-color:rgba(0,0,0,0.5);
    position:absolute;
    color:white;
    top:50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 20;
  }
    .bettingSuccess{
    font-size:0.9vw;
    width:25%;
    height:35%;
    background-color:rgba(0,0,0,0.5);
    position:absolute;
    color:green;
    top:50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 20;
  }
 .scroll {
      overflow-y: auto;
    }
    .row_playArea {
      height:55%;
      width:100%;
      margin:0
    }
    .playTable{
        background-image: url("/icon/荷官暫代圖.png");
        background-repeat: no-repeat;
        background-position: center;
        background-size: cover;
        width: 100%;
        height: 50%;
        position: relative;
    }
    .playArea-tile{
        border:1px solid rgba(255,255,255, 0.3);
        color:#3470A9;
        font-size:1.2vw ;
        position: relative;
    }
    .playArea-tile:hover {
        background-color: #0E541B;
    }
    .playArea-tile1:hover {
        background-color: #0E541B;
    }
     .playArea-tile1{
        border:1px solid rgba(255,255,255, 0.3);
        color:#3470A9;
        font-size:0.7vw ;
        position: relative;
    }
    .player{
      color:#3470A9
    }
    .banker{
      color:red
    }
    .tie-text{
      color:#0C930A;
    }
    .tie{
      height:50%;
      width:100%;
      margin:0;
      color:#0C930A;
      font-size:0.75vw ;

    }
    .tie1{
      border-bottom: 1px solid  rgba(255,255,255, 0.3);
    }
    .playArea{
        background-color:rgb(3, 62, 29);
        height: 30vh;
        /* width:100%;
        height:100%; */
        /* cursor: url('/21.png') 2 2,auto; */
        position: relative;
    }
    .selectCoin{
        width: 100%;
        background-color:black
    }
    .table-info{
      font-size: 0.8vw;
    }
    .room-list{
        font-size: 0.8vw;
    }
    .room-title{
        width:20%;
        height:5vh;
        position:absolute;
        top:0;
        left:0;
        background-color:rgba(0,0,0,0.5);
        font-size: 1vw;
    }
    .gameCountDown{
        position:absolute;
        top:10%;
        left:5%;
    }
    .tabActive{
      background-image:
      linear-gradient(
          rgb(255, 255, 255) 63%,
          #B98F38
        );

    }
    .Custombutton {
      position:absolute;
      top:12vh;right:0;
      border: none;
      color: white;
      padding: 9px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 0.8vw;
      margin: 0px 8.5px;
      cursor: pointer;
      background-image:url('/icon/選擇桌台ui_1.png');
      background-repeat: no-repeat;
      background-position: center;
      background-size: 100% 100%;
      letter-spacing:20px;

    }
    .Custombutton:focus {
    outline: 1px solid #F7D8A8;
    outline-offset: -4px;
}
.elevation_font {
  font-size:0.8vw
}
.switch_video {
  position:absolute;
  bottom:12%;right:0
}

.logo_coin_select {
    width:2.7vw;
    height:2.6vw;
    background-image:url('/icon/七人座自定UI.png');
    background-repeat: no-repeat;
    background-position: center;
    background-size: 100% 100%;
}
.coin_x2 {
        width:2.7vw;
        height:2.6vw;
        background-image:url('/icon/單人雙倍ui.png');
        background-repeat: no-repeat;
        background-position: center;
        background-size: 100% 100%
}

.card_icon_img {
  max-width:3.7vw;
  max-height:2.6vw;
  margin: 0.4vw;

}

.cancel_coinSelect{
  max-width:2.5vw;
  max-height:2.5vw;
}
.change_showing{
 max-width:2.5vw;
 max-height:2.5vw;
}
.show_img_coin{
 width:4vw;
 height:4vw;
 position:absolute;
 top:50%;left:50%;
 transform:translate(-50%,-50%);
}
.click_img{
  height:4vw;
  width:4vw;
}

.click_img_stop{
  max-width:2vw;
  max-height:2vw;
  margin: 6px;
}

.click_img_confirm{
  max-width:2vw;
  max-height:2vw;
  margin: 6px;

}


@media screen and (max-width:360px) {

.playTable_mview {
  width: 100%;

}
.v-wrap {
  width: 100vw;
}
 .playTable{
        background-position: center;
        background-size: cover;
        width: 100vw;
        height: 37vh;
    }

.gameCountDown{
        position:absolute;
        top:14%;
        left:2%;
        height: 6px;
    }

.room-title {
  font-size: 3.4vw;
}

.elevation_font {
  font-size:2.3vw;
}

.elevation-2{
  width: 100vw;

}

.bet_amount{
  width: 100vw;
}
.selectCoin {
   width: 100vw;
}
.playArea-tile {
  font-size:3vw;

}
.playArea-tile1{
  font-size:2.2vw;
}
.tie{
  font-size:2.2vw;
}
.playArea{
  height: 27.3vh;
}
.playArea-tile1 {
  height: 14vh;
}
.row_playArea {
      height:48%;

}
.switch_video {
   bottom:15%;
}

.logo_coin_select {
    width:10vw;
    height:10vw;
}

.coin_x2 {
    width:10vw;
    height:10vw;

}

.card_icon_img {
  padding-top: 42px;
  padding-right: 62px;
  margin-right: 1.8vw;
  margin-top: 4vh;

}
.card_icon {
  padding-top: -5px;
  margin-top: -5px;
  max-width: 100%;
  height: 900px;
  padding-top: 13vh;

}
.checkbox_size{
  padding-right: 67px;
  margin-top: -40px;
}

.cancel_coinSelect{
  max-width:12vw;
  max-height:12vw;
}

.change_showing{
 max-width:12vw;
 max-height:12vw;
}

.justify_cancelCoinSelect{
  margin-top: 3vh;
}
.justify_changeShowing{
  margin-top: 3vh;
}

.show_img_coin{
 width:11vw;
 height:11vw;
}

.click_img{
  margin-top: 12px;
  width:12vw;
  height:12vw;
}
.click_img_stop{
  margin-top:1px;
  max-width:5vw;
  max-height:5vw;
}
.click_img_confirm {
  margin-top:1px;
  max-width:5vw;
  max-height:5vw;
}
.Custombutton {


    }
}

</style>
