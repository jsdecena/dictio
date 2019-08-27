<template>
  <div id="wrapper">
    <h1>Dict.io</h1>
    <div class="container">
      <div class="row">
        <div class="col-sm"></div>
        <div class="col-sm-8">
            <form>
              <div class="form-group">
                <label for="search" class="sr-only">Search</label>
                <div class="input-group">
                  <input type="text" class="form-control" placeholder="Search word meaning">
                  <div class="input-group-append">
                    <button type="submit" class="btn btn-primary">Search</button>
                  </div>
                </div>
              </div>
            </form>
        </div>
        <div class="col-sm"></div>
      </div>
    </div>
  </div>
</template>

<script>
  import SystemInformation from './LandingPage/SystemInformation'

  export default {
    name: 'landing-page',
    components: { SystemInformation },
    methods: {
      open (link) {
        this.$electron.shell.openExternal(link)
      }
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body { 
    font-family: 'Source Sans Pro', sans-serif;
    background:
      radial-gradient(
        ellipse at top left,
        rgba(255, 255, 255, 1) 40%,
        rgba(229, 229, 229, .9) 100%
      );    
  }

  #wrapper {
    height: 100vh;
    padding: 60px 80px;
    width: 100vw;
    margin-top: 40px;
    text-align: center
  }
</style>
