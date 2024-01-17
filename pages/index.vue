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


function DisplayText() {
  const l1: string = ((product.value == 1) ? '◉' : '○') + OptionPos()
  const l5: string = '<br>' + ((product.value == 5) ? '◉' : '○') + OptionNeg()
  const l2: string = (ShowSW() ? (('<br>' + ((product.value == 2) ? '◉' : '○')) + OptionSWPos()) : '')
  const l4: string = (ShowSW() ? (('<br>' + ((product.value == 4) ? '◉' : '○')) + OptionSWNeg()) : '')
  const l3: string = (ShowN() ? (('<br>' + ((product.value == 3) ? '◉' : '○')) + OptionN()) : '')
  const l6: string = (ShowNA() ? (('<br>' + ((product.value == 6) ? '◉' : '○')) + '無回答') : '')
  return l1 + l2 + l3 + l4 + l5 + l6
}

function DisplayText2() {
  // こちらは改行が \n なのでクリップボード用
  const l1: string = ((product.value == 1) ? '◉' : '○') + OptionPos()
  const l5: string = '\n' + ((product.value == 5) ? '◉' : '○') + OptionNeg()
  const l2: string = (ShowSW() ? (('\n' + ((product.value == 2) ? '◉' : '○')) + OptionSWPos()) : '')
  const l4: string = (ShowSW() ? (('\n' + ((product.value == 4) ? '◉' : '○')) + OptionSWNeg()) : '')
  const l3: string = (ShowN() ? (('\n' + ((product.value == 3) ? '◉' : '○')) + OptionN()) : '')
  const l6: string = (ShowNA() ? (('\n' + ((product.value == 6) ? '◉' : '○')) + '無回答') : '')
  return l1 + l2 + l3 + l4 + l5 + l6
}

function CopyText() {
  navigator.clipboard.writeText(DisplayText2())
    .then(() => {
      console.log("copied!")
    })
    .catch(e => {
      console.error(e)
    })
}







</script>

<template>
  <hr>
  <div class="d-f">
    <div class="left i-4">
      回答の方向性
    </div>
    <div class=" d-fc right">
      <label> <input type="radio" name="yesno" value="1" v-model="yesno" checked />はい,いいえ</label>
      <label> <input type="radio" name="yesno" value="2" v-model="yesno" />ある,ない</label>
      <label> <input type="radio" name="yesno" value="3" v-model="yesno" />そう思う,思わない</label>
    </div>
  </div>


  <hr>
  <div class="d-f">
    <div class="left i-4">
      弱い選択肢
    </div>
    <div class="d-fc right">
      <label> <input type="radio" name="somewhat" value="1" v-model="somewhat" />たぶん</label>
      <label> <input type="radio" name="somewhat" value="2" v-model="somewhat" />どちらかというと</label>
      <label> <input type="radio" name="somewhat" value="0" v-model="somewhat" checked />入れない</label>
    </div>
  </div>

  <hr>
  <div class="d-f">
    <div class="left i-4">
      中立的選択肢
    </div>
    <div class="d-fc right">
      <label> <input type="radio" name="neutral" value="1" v-model="neutral" />わからない</label>
      <label> <input type="radio" name="neutral" value="2" v-model="neutral" />どちらともいえない</label>
      <label> <input type="radio" name="neutral" value="0" v-model="neutral" checked />入れない</label>
    </div>
  </div>

  <hr>
  <div class="d-f">
    <div class="left i-4">
      無回答
    </div>
    <div class="d-fc right">
      <label> <input type="radio" name="na" value="1" v-model="na" />入れる</label>
      <label> <input type="radio" name="na" value="0" v-model="na" checked />入れない</label>
    </div>
  </div>

  <hr>
  <div class="space"></div>

  <button type="button" @click="CopyText()" class="display-button">コピー</button>

  <div class="d-f">
    <div class="d-fc display-text display-box">
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
  <div class="space"></div>

  テキストプレビュー
  <p v-html="DisplayText()" class="display-box"></p>
  <div class="space"></div>
  <div id="description">
    <h1> アンケートの回答<br>ジェネレーター
    </h1>
    <div class="space"></div>
    <a href="https://github.com/hibiyahibiyahibiya/radio-msg" style="margin-right: 30px">
      <img src="https://github.githubassets.com/assets/GitHub-Mark-ea2971cee799.png" width="40" />
    </a>

  </div>
</template>

<style>
#description {
  text-align: center;
}

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

.left {
  width: 40%;
}

.right {
  width: 60%;
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

hr {
  border: none;
  border-bottom: 1px solid #333;
  margin: 0;
}

label {
  display: block;
  /* ブロックを作るように */
  margin: 5px 0;
  /* 前後のスペース */

  cursor: pointer;
  user-select: none;
}

.display-text label {
  display: block;
  margin: 0;
  cursor: pointer;
  user-select: none;
}

.display-button {
  display: block;
  margin-left: auto;
  cursor: pointer;
  user-select: none;
  width: 30%;
}

.display-box {
  width: 100%;
  border: 1px solid #333;
}

div.space {
  height: 20px;
}
</style>