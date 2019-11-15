<template>

<section class="container">
<div class="calc-header px-3 py-3 pt-md-5 pb-md-4 mx-auto text-center">
  <h1 class="display-4">Siege Sensitivity Calculator</h1>
  <p class="lead">振り向き(180° distance)を計算するやつ </p>
  <div class="twitter_share">
      <button class="tweet" @click="twitterShare">Tweet</button>
  </div>
</div>

<div class="container">
  <div class="card-deck mb-3 text-center">
    <div class="card mb-3 shadow-sm">
      <div class="card-header">
        <h4 class="my-0 font-weight-normal">Hipfire</h4>
      </div>
      <div class="card-body">
        <h1 class="card-title">{{(hipfire).toFixed(2)}}<small class="text-muted"> cm</small></h1>
      </div>
    </div>
    <div class="card mb-3 shadow-sm">
      <div class="card-header">
        <h4 class="my-0 font-weight-normal">ADS (Holo)</h4>
      </div>
      <div class="card-body">
        <h1 class="card-title">{{(holo).toFixed(2)}}<small class="text-muted"> cm</small></h1>
      </div>
    </div>
    <div class="card mb-3 shadow-sm">
      <div class="card-header">
        <h4 class="my-0 font-weight-normal">ADS (ACOG)</h4>
      </div>
      <div class="card-body">
        <h1 class="card-title">{{(ACOG).toFixed(2)}}<small class="text-muted"> cm</small></h1>
      </div>
    </div>
  </div>
</div>

      <div class="form-group row">
        <label class="col-6 col-form-label">Mouse DPI</label>
        <div class="col-6">
          <input class="form-control" type="number" v-model="dpi" >
        </div>
      </div>

      <div class="form-group row">
        <label class="col-6 col-form-label">MouseSensitivity <small class="text-muted">(マウス感度水平方向) </small></label>
        <div class="col-6">
          <input class="form-control" type="number" v-model="MouseSensitivity" >
        </div>
      </div>

      <div class="form-group row">
        <label class="col-6 col-form-label">AimDownSights <small class="text-muted"> (エイム感度)</small></label>
        <div class="col-6">
          <input class="form-control" type="number" v-model="AimDownSights" >
        </div>
      </div>

      <div class="form-group row">
        <label class="col-6 col-form-label">MouseSensitivityMultiplierUnit</label>
        <div class="col-6">
          <input class="form-control" type="number" v-model="MouseSensitivityMultiplierUnit" >
        </div>
      </div>

      <div class="form-group row">
        <label class="col-6 col-form-label">XfactorAiming</label>
        <div class="col-6">
          <input class="form-control" type="number" v-model="XfactorAiming" >
        </div>
      </div>

  </section>
</template>

<script>

export default {
    name : 'i',
    data: function(){
        return {
            twHipfire: 0,
            dpi: 400,
            MouseSensitivityMultiplierUnit: 0.02,
            MouseSensitivity: 50,
            XfactorAiming: 0.02,
            AimDownSights: 50
        }    
    },
  computed: {
    hipfire : function(){
        return ((0.000001 / this.dpi * 3191858136.0472) * (1 / (this.MouseSensitivityMultiplierUnit * this.MouseSensitivity))) / 2
    },
    holo : function(){
        return this.hipfire * (1 / Math.min(this.AimDownSights * this.XfactorAiming * 0.6, 1) )
    },
    ACOG : function(){
        return this.hipfire * (1 / Math.min(this.AimDownSights * this.XfactorAiming * 0.35, 1) )
    }
  },
  methods: {
    twitterShare : function(){
      var shareURL = 'https://twitter.com/intent/tweet?text=' + "私の振り向きは腰だめ " + this.hipfire.toFixed(2) + "cm, 等倍サイト " + this.holo.toFixed(2) + "cm, ACOG " + this.ACOG.toFixed(2) + "cmです！ %7C %23SiegeSensitivityCalculator" + '&url=' + "https://siegecalc.netlify.com/";  
      location.href = shareURL
    }
  }
}

</script>

<style scoped>
.tweet {
  background-color: #55acee;
  border: 2px solid #55acee;
  border-radius: 0;
  color: #fff;
  padding:4px 32px;
  -webkit-transition: all .3s;
  transition: all .3s;
}
.tweet:hover {
  background-color: #fff;
  color: #55acee;
}</style>
