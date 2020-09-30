<template>
  <div class="home">

    <div class="menuItem">
    <img id='kira' src="https://www.cake2therescue.com.au/wp-content/uploads/2017/04/baker-girl-hand-show.png" alt="">

      <img class="div5" src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/217233/cupcake4.png" alt="">
      <span v-if="menuItem=='CupCakes'" class="div3">
        <h3>Gourmet Cupcake</h3>
        <p>$2.99</p>
      </span>
      <span v-if="menuItem=='Basket'" class="div3">
            <h3 >Basket</h3>
      </span>
      <span v-if="menuItem=='IceCream'" class="div3">
        <h3>Ice Cream</h3>
        <p>$1.99</p>
      </span>
    <span v-if="menuItem=='Cakes'" class="div3">
            <h3>Gourmet Cake</h3>
            <p>$9.99</p>
          </span>
      <div class="div2">
        <button @click="menuItem='Basket'">
          Basket<img src="../assets/picnic-basket.svg" alt="">
        </button>
      </div>
       <span v-if="menuItem=='About'" class="div3">
            <h3>About</h3>
          </span>


      <div class="div4">
        <div class="basket" v-if="menuItem=='Basket'"><p v-for="item in basket">{{item.Item}} ... X{{item.Amount}} ... ${{item.Amount*item.Price}}</p>
        <p>Total: ${{total}}</p><br><button>Checkout</button></div>
        <p v-if="menuItem=='About'">Hi, i'm Kira and my I enjoy sugar, treats, and everything sweet. I run a small bakery located in St.Pete
          FL <br> <br> Monday-Friday 8:30-6:00pm <br>
Saturday 10:00-2:00pm</p> 
        <p v-if="menuItem=='CupCakes'">Every cupcake starts with local and naturally sourced ingediatents. Using family
          recpies and our own in house
          creations, we always stive to recreate the simple pleasures, gaurnteed to put a smile on your face.
        </p>
        <p v-if="menuItem=='IceCream'">Not a big on cake? Don't worry, our ice cream respects the farmer and their
          farmworkers, the planet and the cows. This love and respect is kept through our creation process and makes
          your treat that much sweeter.</p>
        <p v-if="menuItem=='Cakes'">Have a special event coming up? Don't risk it; bring one of our cakes to the party and your sure to be the life of it.</p>
      </div>
      <span v-if="menuItem!='About' && menuItem!='Basket'" class="div6">
        <select v-model="selected">
          <option v-if="menuItem=='Cakes'" v-for="option in cakeOptions" :value="option.value">
            {{ option.text }}
          </option>
           <option v-if="menuItem=='CupCakes'" v-for="option in cupOptions" :value="option.value">
            {{ option.text }}
          </option>
          <option v-if="menuItem=='IceCream'" v-for="option in creamOptions" :value="option.value">
            {{ option.text }}
          </option>
        </select>
        <input v-model="amount" min="1" placeholder="1" id="Iamount" type="number"><br>
        <button @click="add(selected,amount)" variant="success">Add to Basket</button>
      </span>

      <b-list-group class="div1">
        <b-list-group-item  :class="{ active: menuItem=='Cakes'}" @click="menuItem='Cakes'">Cakes</b-list-group-item>
        <b-list-group-item  :class="{ active: menuItem=='CupCakes'}" @click="menuItem='CupCakes'">CupCakes</b-list-group-item>
        <b-list-group-item  :class="{ active: menuItem=='IceCream'}" @click="menuItem='IceCream'">Ice Cream</b-list-group-item>
        <b-list-group-item  :class="{ active: menuItem=='Basket'}" @click="menuItem='Basket'">Basket</b-list-group-item>
        <b-list-group-item  :class="{ active: menuItem=='About'}" @click="menuItem='About'">About</b-list-group-item>
      </b-list-group>

    </div>

  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
        menuItem: 'About',
        basket:[],
        amount: 1,
        selected: 'Pecan',
        cakeOptions: [{
            value: 'Carrot Cake',
            text: 'Carrot Cake'
          },
          {
            value: 'Strawberry Shortcake',
            text: 'Strawberry Shortcake'
          },{
            value: 'Chantilly Cake',
            text: 'Chantilly Cake'
          },
          {
            value: 'White Crème Cake',
            text: 'White Crème Cake'
          }
        ],
        creamOptions:[{
          value:'Chocolate',
          text:'Chocolate'
        },{
          value:'Vanilla',
          text:'Vanilla'
        },{
          value:'Blueberry',
          text:'Blueberry'
        },
        {value:'Cookie Dough',
        text:'Cookie Dough'},
        {value:'Guava',text:'Guava'},
        {value:'Dulce de leche',text:'Dulce de leche'}
        ],
        cupOptions: [{
            value: 'Pecan Praline',
            text: 'Pecan Praline'
          },
          {
            value: 'Summertime S’mores',
            text: 'Summertime S’mores'
          },
          {
            value: 'Salted Caramel',
            text: 'Salted Caramel'
          },
          {
            value: 'Snickerdoodle',
            text: 'Snickerdoodle'
          }
        ]
      }
    },
    methods: {
      async add(item,amount) {
        console.log(amount,item)
        let price=(this.menuItem=='CupCakes'?2.99:this.menuItem=='Cakes'?9.99:this.menuItem=='IceCream'?1.99:null)
        
        this.basket.push({'Price':price,'Item':item,'Amount':amount})
      }
    },
    computed:{
      total: function(){
        return this.basket.map(item=>item.Price).reduce((sum, current) => sum + current, 0)
      }
    }
  }
</script>
<style lang="scss">
  .home {


    text-align: left;

    span {
      display: inline-flex;
    }

    b-button {
      cursor: pointer;

    }

    #kira {
      position: absolute;
      left: -33%;
      z-index: 2;
      width: 350px;
      top: 80px;
    }

    .menuItem {
      position: absolute;
      left: 25%;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-template-rows: 75px 250px 75px;
      grid-column-gap: 0px;
      grid-row-gap: 0px;
      max-height: 400px;
      max-width: 800px;
      margin: 0 auto;
      margin-top: 25px;
      background-image: -webkit-linear-gradient(45deg, #ffffff 0%, #f3f3f3 100%);
      box-shadow: 0px 2px 40px 0px transparent, 0px 6px 26px 0px rgb(191, 155, 89), 0px 3px 0px -2px white inset, 0px 22px 60px 70px #f1f1f1 inset, 0px 8px 18px -7px transparent, 30px 13px 30px 28px #b18f8f inset;
      text-shadow: 1px 2px 2px rgba(0, 0, 0, 0.2);
      font-size: 1.2rem;
      p {
        font-family: 'Bad Script', cursive;
        line-height: 22px;
        color: #1b1b1b;
        margin: 5px;
      }

      ul {
        list-style: none;
      }

      .div1 {
        grid-area: 1 / 4 / 4 / 5;
        background: #de467c;
        display: inline-flex;
        flex-direction: column;

        .active{
           background: rgb(206, 83, 184);
        }
        b-list-group-item {
          cursor: pointer;
          padding: 10px 0px 10px 15px;
          color: white;
          border-radius: 255px 15px 205px 35px/35px 225px 35px 255px;
          font-family: 'Satisfy', cursive;

          &:hover {
            background: rgb(206, 83, 184);
          }
        }


      }

      .div2 {
        grid-area: 1 / 1 / 2 / 2;
        font-family: 'Satisfy', cursive;

        button {
          border: none;
          margin: 8px 0px 0px 5px;
        }

        img {
          height: 22px;
          margin-left: 10px;
        }
      }

      .div3 {
        grid-area: 1 / 2 / 2 / 4;
        align-items: center;
        color: #94619c;
        font-family: 'Amatic SC', cursive;
        margin-top: 10px;
        p {
          margin-left: 10px;
          font-weight: bold;
          color: rgb(206, 83, 184);
        }

        span {
          text-align: center;
        }
      }

      .div4 {
        grid-area: 2 / 2 / 3 / 4;

        span {
          margin-top: 25px;
        }
      }

      .div5 {
        grid-area: 3 / 1 / 4 / 2;
        width: 150px;
        z-index: 3;
        transform: translate3d(0px, -125px, 0px);
      }
    }

    .div6 {
      grid-area: 3 / 2 / 4 / 4;
      display: block;
      margin: 15px;
      margin-top: -20px;

      button {
        background: rgb(206, 83, 184);
        color: white;
        border: none;
      }

      select,
      button {
        border-radius: 255px 15px 205px 35px/35px 225px 35px 255px;
        font-family: 'Satisfy', cursive;
      }

      #Iamount {
        max-width: 50px;
        border-radius: 255px 15px 205px 35px/35px 225px 35px 255px;
        font-family: 'Amatic SC', cursive;
      }
    }
    .basket{
      button{
          background: rgb(206, 83, 184);
        color: white;
        border: none;
         border-radius: 255px 15px 205px 35px/35px 225px 35px 255px;
        font-family: 'Satisfy', cursive;
        margin-left: 10px;
      }
    }


  }
       @media only screen and (max-width: 800px) {
       #kira{
         display: none;
       }
       .menuItem{
          left: 0px !important;
       }
       .div4{
         grid-area: 2/1/3/4 !important;
       }
  }
</style>