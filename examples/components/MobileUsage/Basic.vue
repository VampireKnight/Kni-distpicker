<template>
  <div class="row">
    <div class="example">
      <h5>Base</h5>
      <div class="example-box">
        <div class="box-left d-flex align-items-baseline">
          <div class="col-md-7">
            <div @click="locsel">{{location}}</div>
            <v-distpicker type="mobile" :shoWrap="shoWrap" @emShow="locsel" wrapper="address-wrapper" @selected="onSelected" @province="selectProvince" @city="selectCity" @area="selectArea" address-container="address-container"></v-distpicker>
          </div>
          <div class="content-show col-md-5">
            <pre><code>{{ select }}</code></pre>
          </div>
        </div>
        <div class="box-right col-md-12" v-if="showCode">
<pre class=" language-javascript code-toolbar"><code class=" language-javascript"><span class="token operator">&lt;</span>template<span class="token operator">&gt;</span>
  <span class="token operator">&lt;</span>v<span class="token operator">-</span>distpicker type<span class="token operator">=</span><span class="token string">"mobile"</span><span class="token operator">&gt;</span><span class="token operator">&lt;</span><span class="token operator">/</span>v<span class="token operator">-</span>distpicker<span class="token operator">&gt;</span>
<span class="token operator">&lt;</span>template<span class="token operator">&gt;</span>

<span class="token operator">&lt;</span>script<span class="token operator">&gt;</span>
<span class="token keyword">import</span> VDistpicker <span class="token keyword">from</span> <span class="token string">'v-distpicker'</span>

<span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token punctuation">{</span>
  components<span class="token punctuation">:</span> <span class="token punctuation">{</span> VDistpicker <span class="token punctuation">}</span><span class="token punctuation">,</span>
<span class="token punctuation">}</span>
<span class="token operator">&lt;</span><span class="token operator">/</span>script<span class="token operator">&gt;</span></code></pre>
        </div>
        <div class="box-footer" @click="showCode = !showCode">
          {{ showCode ? 'Hide Code' : 'Show Code' }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VDistpicker from '../../../src/Distpicker'

export default {
  components: { VDistpicker },
  data() {
    return {
      location:'地址',
      showCode: false,
      shoWrap:false,
      select: { province: '', city: '', area: '' },
    }
  },
  methods: {
    selectProvince(value) {
      this.select.province = value
      console.log(value);
    },
    selectCity(value) {
      this.select.city = value
      console.log(value);
    },
    selectArea(value) {
      this.select.area = value
      console.log(value);
    },
    locsel(val){
      if('object'==typeof(val)){
        this.shoWrap=!this.shoWrap; 
      }else if('boolean' == typeof(val)){
        this.shoWrap=val;
      }       
    },
    onSelected(data){
        console.log(data);
        const direcity=['110000'];
        const citval=data.province.code;
        /*(arr.indexOf(某元素) > -1)*/
        console.log("是否是直辖市:"+direcity.indexOf(citval))
        if(direcity.indexOf(citval)>-1){
          console.log("是直辖市");
          this.location = data.province.value+data.area.value;
        }else{
          console.log("不是直辖市");
          this.location = data.province.value+data.city.value+data.area.value;
        }
      this.shoWrap=false;
    }
  },
}
</script>
