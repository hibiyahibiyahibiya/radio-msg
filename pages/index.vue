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
      <label> <input type="radio" name="yesno" value="3" v-model="yesno" checked />はい,いいえ</label>
      <label> <input type="radio" name="yesno" value="2" v-model="yesno" />ある,ない</label>
      <label> <input type="radio" name="yesno" value="1" v-model="yesno" />そう思う,思わない</label>
    </div>
  </div>


  <div class="d-f">
    <div class="half i-4">
      程度の弱いのを
    </div>
    <div class=" d-fc half">
      <label> <input type="radio" name="somewhat" value="2" v-model="somewhat" />多分</label>
      <label> <input type="radio" name="somewhat" value="1" v-model="somewhat" />どちらかというと</label>
      <label> <input type="radio" name="somewhat" value="0" v-model="somewhat" checked />入れない</label>
    </div>
  </div>

  <div class="d-f">
    <div class="half i-4">
      また、を
    </div>
    <div class=" d-fc half">
      <label> <input type="radio" name="neutral" value="2" v-model="neutral" />わからない</label>
      <label> <input type="radio" name="neutral" value="1" v-model="neutral" />どちらともいえない</label>
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