<template>

<section class="container">
<div class="calc-header px-3 py-3 pt-md-5 pb-md-4 mx-auto text-center">
  <h1 class="display-4">Siege Sensitivity Calculator</h1>
  <p class="lead">振り向き(180° distance)を計算するやつ </p>
  <a class="twitter-share-button" v-bind:data-text="tweetText()">Tweet</a>
  <script>!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0],p=/^http:/.test(d.location)?'http':'https';if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src=p+'://platform.twitter.com/widgets.js';fjs.parentNode.insertBefore(js,fjs);}}(document, 'script', 'twitter-wjs');</script>
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
    tweetText : function(){
      return "私の振り向きは腰だめ " + this.hipfire.toFixed(2) + "cm, 等倍サイト " + this.holo.toFixed(2) + "cm, ACOG " + this.ACOG.toFixed(2) + "cmです！ | Siege Sensitivity Calculator"
    } 
  }
}

</script>