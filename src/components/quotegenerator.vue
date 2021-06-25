<template>
  <div class="container">
    <div class="text">
      <p class="phrase"><i class="fas fa-quote-left"></i>{{ currentValue }}<i class="fas fa-quote-right"></i></p>
      <span class="author">~{{ currentAuthor }}</span>
      <div class="line"></div>
      <div class="button">
         <a href="https://twitter.com/share?ref_src=twsrc%5Etfw" 
     class="twitter-share-button" 
     :data-text="currentValue + currentAuthor"
     data-via="adalkis5" 
     data-hashtags="testing" 
     data-show-count="false">Tweet
     </a>
          <button @click="quoteData">Next</button>
      </div>
    
     
     
    </div>

    
     
  
  </div>
</template>

<script>

import axios from "axios";
export default {
  name: "quotegenerator",
  data() {
    return {
      result: 0,
      currentValue: " You can observe a lot just by watching.",
      currentAuthor: "Yogi Berra",
      previousValue: [],
    };
  },
  methods: {
    quoteData() {
      this.result += 1;
      let valor = this.previousValue[this.result];
      this.currentValue = valor.text;
      this.currentAuthor = valor.author;
    },
  },
  mounted() {
    axios
      .get("https://type.fit/api/quotes")
      .then((res) => {
        this.previousValue = res.data;
      })
      .catch((err) => {
        alert("Please reload again");
        console.log(err);
      });
  },
  created(){
    let tweet = document.createElement('script');
    tweet.setAttribute('src',"https://platform.twitter.com/widgets.js");
    document.head.appendChild(tweet)

  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
    background: #dfcaff;
    width: 550px;
    height: 300px;
    margin-top: 100px;
    border-radius: 10px;
    
}
p.phrase {
    font-family: cursive;
    font-size: 33px;
    font-weight: 700;
    
}

span.author {
    font-family: cursive;
    font-size: 20px;
    
    
  
  
}
.line {
    border-top: 3px solid black;
    margin: 20px;
    padding: 10px;
}
.button {
    display: flex;
    justify-content: space-between;
    margin: 30px;
}
button {
    width: 100px;
    height: 30px;
    background: #C0A1EF;
    border: none;
    font-family: cursive;
    font-size: 20px;
  
}
button:hover{
  background: rgb(189, 45, 189);
}

</style>
