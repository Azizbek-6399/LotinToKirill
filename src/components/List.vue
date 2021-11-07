<template>
    <v-container class="mt-10 cont">
      <!-- ///////////////////////////////////////////////////// -->
      <v-row class="wrapperChangers">
        <v-col md="5" sm="5" xs="5" class="border midCol">
          <v-row>
            <v-col md="3" sm="4" xs="5" class="px-0">
              <v-btn class="btns" block tile @click="exchange" :color="(isActive) ? 'primary' : ''" >Lotin</v-btn>
            </v-col>
            <v-col md="3" sm="4" xs="5" class="px-0">
              <v-btn class="btns" block tile @click="exchange"  :color="(isActive) ? '' : 'primary'">Kirill</v-btn>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="2" sm="2" xs="2" class="midCol">
          <div  @click="exchange" color="white" class="modifire">
            <img class="image" src="/exchangeM.svg" alt="">
          </div>
        </v-col>
        <v-col md="5" sm="5" xs="5" class="border midCol">
          <v-row>
            <v-col md="6" sm="4" xs="0" class="bcol"></v-col>
            <v-col md="3" sm="4" xs="6" class="px-0">
              <v-btn class="btns" block tile @click="exchange" :color="(isActive) ? '' : 'primary'">Lotin</v-btn>
              </v-col>
            <v-col md="3" sm="4" xs="6" class="px-0">
              <v-btn class="btns" block tile @click="exchange" :color="(isActive) ? 'primary ' : ''">Kirill</v-btn>
              </v-col>
          </v-row>
        </v-col>
      </v-row>
      <v-row class="translater">
        <v-col md="6" sm="6" xs="12" cols="12" class="px-0 textA">
             <v-textarea solo :label="(isActive) ? 'Lotin matnini kiriting' : 'Крилл матнини киритинг'" v-model="input" style="border-radius:0px"></v-textarea>
              <div class="cancel" v-show="input" @click="input = ''">
               +
             </div>
        </v-col>
        <v-col md="6" sm="6" xs="12" cols="12" class="px-0 textA">
             <v-textarea solo :label="(isActive) ? 'Крилл матнини олинг' : 'Lotin matnini oling'" readonly :value="output" style="border-radius:0px"></v-textarea>
             <div
             v-show="input"
              class="copyP"
              v-clipboard:copy="output"
              v-clipboard:success="onCopy"
              v-clipboard:error="onError"
              @click="snackbar = true"
             >
             <img src="/copyM.svg" alt="image" class="copy" :title="(isActive) ? 'Нусха олиш' : 'Nusxa olish'">
             </div>
          <v-snackbar v-model="snackbar" right>
            {{ (isActive) ? 'Матн нусхаланди !' : 'Matn nusxalandi !' }}
            <template v-slot:action="{ attrs }">
             <div
             color="pink"
             class="closeBtn"
             text
             v-bind="attrs"
             @click="snackbar = false"
             >
             +
             </div>
            </template>
          </v-snackbar>
        </v-col>
      </v-row>
      <v-row class="poveredBy">
        <div>
        © Povered by <a href="https://www.alphasoft.uz/" class="povered">Alphasoft.uz</a>
        </div>
      </v-row>
    </v-container>    
</template>

<script>
export default {
     data(){
      return{
        input: '',
        isActive: true,
        snackbar: false,
        active: false
      }
    },
    methods:{    
      //clipboard
      onCopy: function (e) {
        if(e !== ''){
           return e.text
        } 
      },
      onError: function (e) {
         console.log(e);
      },
      exchange() {
        this.input = this.output
        this.isActive = !this.isActive;
      },
    },
    computed:{
        dict(){
          return {
            'A': 'А', 'B': 'Б', 'D': 'Д', 'E': 'Э', 'F': 'Ф', 'G': 'Г', 'G’': 'Ғ', 'H': 'Ҳ', 'I': 'И', 'J': 'Ж', 'K': 'К', 'L': 'Л', 'M': 'М', 'N': 'Н', 'O': 'О','O‘' : 'Ў', 'O’': 'Ў', 'O\'': 'Ў', 'O`': 'Ў', 'P': 'П', 'Q': 'Қ', 'R': 'Р', 'S': 'С', 'T': 'Т', 'U': 'У', 'V': 'В', 'X': 'Х', 'Y': 'Й', 'Z': 'З',
            'a': 'а', 'b': 'б', 'd': 'д', 'e': 'э', 'f': 'ф', 'g': 'г', 'g’': 'ғ', 'h': 'ҳ', 'i': 'и', 'j': 'ж', 'k': 'к', 'l': 'л', 'm': 'м', 'n': 'н', 'o’': 'ў', 'o‘' : 'ў', 'o`': 'ў', 'o\'': 'ў', 'p': 'п', 'q': 'қ', 'r': 'р', 's': 'с', 't': 'т','u': 'у', 'x': 'х', 'v': 'в', 'y': 'й', 'z': 'з'                                                                                                                                           
          }
        },
      // there is a function for Krill to Latin in here
        krillToLotin(){
        let newArrStr2 = this.input.split(""), helper = '', newHelper = '';
        for(let i = 0; i < newArrStr2.length; i++){
          switch(newArrStr2[i]){
            case 'Е' : if(newArrStr2[i-1] === ' ' || i === 0){helper += newArrStr2[i+1].search(/[А-Я]/) === -1 ? 'Ye' : 'YE'} else {helper += 'E'} break
            case 'е' : if(newArrStr2[i-1] === ' ' || i === 0){helper += 'ye'} else {helper += 'e'} break
            case 'Ш' : {helper += newArrStr2[i+1].search(/[А-Я]/) === -1 ? 'Sh' : 'SH'} break
            case 'Щ' : {helper += newArrStr2[i+1].search(/[А-Я]/) === -1 ? 'Sh' : 'SH'} break
            case 'Ч' : {helper += newArrStr2[i+1].search(/[А-Я]/) === -1 ? 'Ch' : 'CH'} break
            case 'Ё' : {helper += newArrStr2[i+1].search(/[А-Я]/) === -1 ? 'Yo' : 'YO'} break
            case 'Я' : {helper += newArrStr2[i+1].search(/[А-Я]/) === -1 ? 'Ya' : 'YA'} break
            case 'Ю' : {helper += newArrStr2[i+1].search(/[А-Я]/) === -1 ? 'YA' : 'YU'} break
            case 'ё' : {helper += 'yo'} break
            case 'я' : {helper += 'ya'} break
            case 'ю' : {helper += 'yu'} break
            case 'ш' : {helper += 'sh'} break
            case 'щ' : {helper += 'sh'} break
            case 'ч' : {helper += 'ch'} break
            case 'Ы' : {helper += ''} break
            case 'ы' : {helper += ''} break
            case 'Ъ' : {helper += '\''} break
            case 'ъ' : {helper += '\''} break
            case 'Ц' : {helper += 'S'} break
            case 'ц' : {helper += 's'} break
            default : helper += newArrStr2[i]
           }
        }
        const dict = Object.keys(this.dict).reduce((acc, item) => {
          acc[this.dict[item]] = item 
          return acc;
        }, {} )
        for(let i = 0; i < helper.length; i++){
          if(Object.keys(dict).includes(helper[i])){
             newHelper += dict[helper[i]]
          }
          else {
            newHelper += helper[i];
          }
        }
          return newHelper; 
        },

      // there is a function in here for Latin to Krill 
        lotinToKril(){
        let newArrStr = this.input, delivery= '', newDelivery = '';
        for(let i = 0; i < newArrStr.length; i++){
          if(/[S|s]/.test(newArrStr[i]) && newArrStr[i+1].toLowerCase() === 'h') {
            delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Ш' : 'ш'; i++
          } else if(/[C|c]/.test(newArrStr[i]) && newArrStr[i+1].toLowerCase() === 'h') {
             delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Ч' : 'ч'; i++
           } else if(/[Y|y]/.test(newArrStr[i]) && newArrStr[i+1].toLowerCase() === 'e'){
             delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Е' : 'е'; i++
          } else if(/[Y|y]/.test(newArrStr[i]) && newArrStr[i+1].toLowerCase() === 'o' && !['\'', '`', '’',  '‘'].includes(newArrStr[i+2])){
             delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Ё' : 'ё'; i++
          } else if(newArrStr[i] === 'A' &&  ['\'', '`', '’',  '‘'].includes(newArrStr[i+1])){
             delivery += newArrStr[i+2].search(/[A-Z]/) !== -1 ? 'АЪ' : 'Aъ'; i++
          }  else if(newArrStr[i] === 'a' &&  ['\'', '`', '’',  '‘'].includes(newArrStr[i+1])){
             delivery += 'аъ'; i++
          } else if(/[Y|y]/.test(newArrStr[i]) && newArrStr[i+1].toLowerCase() === 'a'){
            delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Я' : 'я'; i++ 
          } else if(/[Y|y]/.test(newArrStr[i]) && newArrStr[i+1].toLowerCase() === 'u'){
            delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Ю' : 'ю'; i++ 
          } else if(/[O|o]/.test(newArrStr[i]) && ['\'', '`', '’',  '‘'].includes(newArrStr[i+1])){
            delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Ў' : 'ў'; i++ 
          } else if(/[A|a]/.test(newArrStr[i]) && ['\'', '`', '’',  '‘'].includes(newArrStr[i+1])){
            delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Аъ' : 'ў'; i++ 
          } else if(/[G|g]/.test(newArrStr[i]) && ['\'', '`', '’',  '‘'].includes(newArrStr[i+1])){
            delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Ғ' : 'ғ'; i++ 
          } else if(/[E|e]/.test(newArrStr[i]) && newArrStr[i-1] !== ' ' && i !== 0){
            delivery += newArrStr[i].search(/[A-Z]/) !== -1 ? 'Е' : 'e';
          } else if(['\'', '`', '’',  '‘'].includes(newArrStr[i])){
            delivery += (newArrStr[i+1].search(/[A-Z]/) !== -1 ?? newArrStr[i-1].search(/[A-Z]/) !== -1) ? 'Ъ' : 'ъ'
          } else {
              delivery += newArrStr[i];
          }
        }
        for(let i = 0; i < delivery.length; i++){
          if(Object.keys(this.dict).includes(delivery[i])){
            newDelivery += this.dict[delivery[i]]
          } else{
            newDelivery += delivery[i]
          }
        }
        return newDelivery;
      },
      output(){
        return this.isActive ? this.lotinToKril : this.krillToLotin
      }
    }
}
</script>

<style scoped>
    .poveredBy{
      left: 50%;
      transform: translate(-50%);
      position: absolute;
      z-index: 11;
      bottom: 20px;
    }
    .poveredBy .povered{
      text-decoration: none;
      margin-left: 5px;
    }
    .closeBtn{
      transform: rotate(45deg);
      font-size: 25px;
      color: blue;
      cursor: pointer;
    }
    .copyP{
      position: absolute;
      z-index: 1;
      right: 12px;
      bottom: 45px;
    }
    .textA{
      position: relative;
    }
    .cancel{
      position: absolute;
      z-index: 2;
      top: 10px;
      right: 10px;
      font-size: 25px;
      font-weight: 400;
      transform: rotate(45deg);
      cursor: pointer;
    }
    .copy{
      width: 22px;
      height: 22px;
      cursor: pointer;
    }
    /* .copy:hover{
      box-shadow: 3px 3px 10px rgb(206, 203, 203), -3px -3px 10px rgb(206, 203, 203);
    } */
    .vBtn{
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .modifire {
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      height: 100%;
    }

    .v-texts{
      border-radius: 0px;
    }
    .image{
      height: 70%;
      width: 20%;
    }

    @media (max-width: 960px) {
      .cont{
        padding: 0 30px !important;
      }
      .btns{
        font-size: 12px !important;
      }
    }
    @media (max-width: 940px){
      .image{
        width: 26%;
        height: 70%;
      }
    }

    @media (max-width: 750px){
      .image{
        width: 30%;
        height: 70%;
      }
    }

    @media (max-width: 600px){
      .poveredBy{
        bottom: 0;
      }
      .image{
        width: 15%;
        height: 70%;
      }

      .bcol{
        display: none;
      }
      .midCol{
        padding: 0 !important;
      }
      .translater{
        margin-top: 30px !important;
      }
      .wrapperChangers{
        padding: 0 10px !important;
      }
    }

    @media (max-width: 422px) {
      .poveredBy{
        bottom: -20px;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
      }
      .textA{
        margin: 0 !important;
        padding: 0 !important;
      }
         .image{
        width: 26%;
        height: 70%;
      }
    .copyP{
      position: absolute;
      z-index: 1;
      right: 5px;
      bottom: 30px;
    }
    .cancel{
      top: 0;
    }
      .translater{
        margin-top: 35px !important;
      }
      .midCol{
        padding: 0 !important;
      }
      .btns{
        width: 35px !important;
        height: 28px !important;
      }
    }

   
  </style>