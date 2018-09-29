<template>
    <div class="container">
        <div class="row text-center">
            <h1>CHUCK NORRIS</h1>
            <br>
            <div>
              <img :src="icon" alt="chuck-norris-icon">
            </div>
            <br>
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
              <button type="button" class="btn btn-default btn-lg" name="button" @click="fetchQuote">CHUCK JOKE</button>
            </div>
        </div>
        <br>
        <transition name="fade" mode="out-in" appear>
          <div v-if="quote.length > 0" class="jumbotron col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
            {{ quote }}
          </div>
        </transition>
    </div>
</template>

<script>
    export default {
        data() {
            return {
              quote: '',
              icon: 'https://assets.chucknorris.host/img/avatar/chuck-norris.png'
            };
        },
        methods: {
            fetchQuote() {
               this.$http.get('https://api.chucknorris.io/jokes/random')
                       .then(response => {
                           return response.json();
                       })
                       .then(data => {
                           this.quote = data.value;
                       });
            }
        },
        created() {
          this.fetchQuote();
        }
    }
</script>

<style>
  body  {
    height: 100vh;
    background: url('https://i.imgur.com/whDHV8K.jpg');
    color: #ffffff;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
  }
  .jumbotron {
    color: #000000;
    font-size: 20px;
  }
  .fade-enter {
    opacity: 0;
  }
  .fade-enter-active {
    transition: opacity 0.5s;
  }
  .fade-leave {
    opacity: 0;
  }
  .fade-leave-active {
    transition: opacity 0.5s;
    opacity: 0;
  }

</style>
