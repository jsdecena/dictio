<template>
  <div id="wrapper">
    <h1>Dict.io</h1>
    <div class="container">
      <div class="row">
        <div class="col-sm"></div>
        <div class="col-sm-8">
          <form v-on:submit.prevent="onSearch()">
            <div class="form-group">
              <label for="search" class="sr-only">Search</label>
              <div class="input-group">
                <input type="text" class="form-control" placeholder="Search word meaning" v-model="search">
                <div class="input-group-append">
                  <button type="submit" class="btn btn-primary"><i class="fa fa-search"></i> Search</button>
                  <button type="button" v-on:click.prevent="onClear()" class="btn btn-info text-white"><i class="fa fa-eraser"></i> Clear</button>
                </div>
              </div>
            </div>
          </form>
        </div>
        <div class="col-sm"></div>
      </div>
      <div class="row" id="result" v-if="results.length">
        <div class="col">
          <div class="card" v-for="(result, idx) in results" :key="idx">
            <div class="card-body" v-if="result.meta">
              <h5 class="card-title">
                <strong>{{result.meta.id}}</strong>
                <small class="text-lowercase font-weight-light">[{{result.hwi.hw}}]</small>
                <hr>
              </h5>
              <small class="text-lowercase font-weight-light"><em>{{result.fl}}</em></small>
              <p class="card-text">{{result.shortdef[0]}}</p>
            </div>
          </div>
        </div>        
      </div>
      <div v-if="loading" class="lds-ellipsis"><div></div><div></div><div></div><div></div></div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'landing-page',
    data () {
      return {
        loading: false,
        search: null,
        results: []
      }
    },
    methods: {
      onSearch () {
        this.results = []
        const q = this.search
        this.loading = true
        axios.get('//www.dictionaryapi.com/api/v3/references/learners/json/' + q + '?key=e173e337-e26a-4e46-bb13-54b59b623001').then((res) => {
          this.results = res.data
          this.loading = false
        })
      },
      onClear () {
        this.results = []
        this.search = null
      }
    }
  }
</script>

<style>
  @import url('//fonts.googleapis.com/css?family=Source+Sans+Pro');
  @import url('//cdnjs.cloudflare.com/ajax/libs/font-awesome/5.10.2/css/all.min.css');

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body { 
    font-family: 'Source Sans Pro', sans-serif;
  }

  #wrapper {
    height: 100vh;
    padding: 60px 80px;
    width: 100vw;
    padding-top: 40px;
    text-align: center
  }

  #wrapper #result {
    text-align: left;
  }

  ::-webkit-input-placeholder { /* Edge */
    color: #eee;
  }

  :-ms-input-placeholder { /* Internet Explorer 10-11 */
    color: #eee;
  }

  ::placeholder {
    color: #eee;
  }

  .card {
    margin-bottom: 20px;
  }

  .card-title small {
    color: #999;
  }

  .lds-ellipsis {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
  }
  .lds-ellipsis div {
    position: absolute;
    top: 27px;
    width: 11px;
    height: 11px;
    border-radius: 50%;
    background: rgb(0, 123, 255);
    animation-timing-function: cubic-bezier(0, 1, 1, 0);
  }
  .lds-ellipsis div:nth-child(1) {
    left: 6px;
    animation: lds-ellipsis1 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(2) {
    left: 6px;
    animation: lds-ellipsis2 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(3) {
    left: 26px;
    animation: lds-ellipsis2 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(4) {
    left: 45px;
    animation: lds-ellipsis3 0.6s infinite;
  }
  @keyframes lds-ellipsis1 {
    0% {
      transform: scale(0);
    }
    100% {
      transform: scale(1);
    }
  }
  @keyframes lds-ellipsis3 {
    0% {
      transform: scale(1);
    }
    100% {
      transform: scale(0);
    }
  }
  @keyframes lds-ellipsis2 {
    0% {
      transform: translate(0, 0);
    }
    100% {
      transform: translate(19px, 0);
    }
  }

</style>
