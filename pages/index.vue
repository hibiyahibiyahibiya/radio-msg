<script setup lang="ts">

const yesno: Ref<number> = ref(1)
const somewhat: Ref<number> = ref(0)
const neutral: Ref<number> = ref(0)
const na: Ref<number> = ref(0)
const product: Ref<number> = ref(1)




function OptionPos() {
  if (yesno.value == 1) return 'はい'
  else if (yesno.value == 2) return 'ある'
  else return 'そう思う'
  // use ==, not ===
}
function OptionNeg() {
  if (yesno.value == 1) return 'いいえ'
  else if (yesno.value == 2) return 'ない'
  else return 'そう思わない'
  // use ==, not ===
}

function OptionSWPos() {
  const sw: string = (somewhat.value == 1) ? 'たぶん' : 'どちらかというと'
  let pos: string
  if (yesno.value == 1) { pos = 'そう' } else if (yesno.value == 2) { pos = 'ある' } else { pos = 'そう思う' }
  return sw + pos
}

function OptionSWNeg() {
  const sw: string = (somewhat.value == 1) ? 'たぶん' : 'どちらかというと'
  let neg: string
  if (yesno.value == 1) { neg = '違う' } else if (yesno.value == 2) { neg = 'ない' } else { neg = 'そう思わない' }
  return sw + neg
}


function OptionN() {
  if (neutral.value == 1) return 'わからない'
  else return 'どちらともいえない'
  // use ==, not ===
}


function ShowSW() {
  return somewhat.value != 0
}

function ShowN() {
  return neutral.value != 0
}
function ShowNA() {
  return na.value != 0
}

</script>

<template>
  <div>
    <label> <input type="radio" style="accent-color: black" />ある</label>
  </div>
  <div>
    <label> <input type="radio" style="accent-color: black" />どちらかというとある</label>
  </div>
  <div>
    <label> <input type="radio" style="accent-color: black" />どちらとも言えない</label>
  </div>
  <div>
    <label> <input type="radio" style="accent-color: black" />どちらかというとない</label>
  </div>
  <div>
    <label> <input type="radio" style="accent-color: black" />ない</label>
  </div>
  <div style="height: 100px;"></div>




  <div class="d-f">
    <div class="half i-4">
      表現は
    </div>
    <div class=" d-fc half">
      <label> <input type="radio" name="yesno" value="1" v-model="yesno" checked />はい,いいえ</label>
      <label> <input type="radio" name="yesno" value="2" v-model="yesno" />ある,ない</label>
      <label> <input type="radio" name="yesno" value="3" v-model="yesno" />そう思う,思わない</label>
    </div>
  </div>


  <div class="d-f">
    <div class="half i-4">
      程度の弱いのを
    </div>
    <div class=" d-fc half">
      <label> <input type="radio" name="somewhat" value="1" v-model="somewhat" />たぶん</label>
      <label> <input type="radio" name="somewhat" value="2" v-model="somewhat" />どちらかというと</label>
      <label> <input type="radio" name="somewhat" value="0" v-model="somewhat" checked />入れない</label>
    </div>
  </div>

  <div class="d-f">
    <div class="half i-4">
      また、を
    </div>
    <div class=" d-fc half">
      <label> <input type="radio" name="neutral" value="1" v-model="neutral" />わからない</label>
      <label> <input type="radio" name="neutral" value="2" v-model="neutral" />どちらともいえない</label>
      <label> <input type="radio" name="neutral" value="0" v-model="neutral" checked />入れない</label>
    </div>
  </div>

  <div class="d-f">
    <div class="half i-4">
      無回答を
    </div>
    <div class=" d-fc half">
      <label> <input type="radio" name="na" value="1" v-model="na" />入れる</label>
      <label> <input type="radio" name="na" value="0" v-model="na" checked />入れない</label>
    </div>
  </div>


  <div style="width: 50px;"></div>

  <div class="d-f">
    <div class=" d-fc">
      <label> <input type="radio" name="product" value="1" v-model="product" checked />{{ OptionPos() }}</label>
      <label v-show="ShowSW()"> <input type="radio" name="product" value="2" v-model="product" />{{ OptionSWPos()
      }}</label>
      <label v-show="ShowN()"> <input type="radio" name="product" value="3" v-model="product" />{{ OptionN() }}</label>
      <label v-show="ShowSW()"> <input type="radio" name="product" value="4" v-model="product" />{{ OptionSWNeg()
      }}</label>
      <label> <input type="radio" name="product" value="5" v-model="product" />{{ OptionNeg() }}</label>
      <label v-show="ShowNA()"> <input type="radio" name="product" value="6" v-model="product" />無回答</label>
    </div>
  </div>
</template>

<style>
input {
  accent-color: black;
}

div.d-f {
  display: flex;
}

div.d-fc {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

div.d-b {
  display: block;
}

.half {
  width: 50%;
}

.i-4 {
  text-align: center;
  line-height: 100px;
}

.dev-a {
  background-color: aqua;
}

.dev-l {
  background-color: lime;
}

label {
  display: block;
  /* ブロックを作るように */
  margin: 5px 0;
  /* 前後のスペース */

  cursor: pointer;
  user-select: none;
}
</style>