<template>
  <div class="result">
    <div class="edit-line">
      <span>{{topNumb}}</span>
      <input type="text" name="" readonly v-model="maxLength" :maxlength="2" value="">
    </div>
    <div class="oper-box">
      <div class="oper-line">
        <div class="oper-item" @click="handleTextClick">
          7
        </div>
        <div class="oper-item" @click="handleTextClick">
          8
        </div>
        <div class="oper-item" @click="handleTextClick">
          9
        </div>
        <div class="oper-item" @click="handleOperClick">
          /
        </div>
        <div class="oper-item" @click="handleDeleteClick">
          ←
        </div>
      </div>
      <div class="oper-line">
        <div class="oper-item" @click="handleTextClick">
          4
        </div>
        <div class="oper-item" @click="handleTextClick">
          5
        </div>
        <div class="oper-item" @click="handleTextClick">
          6
        </div>
        <div class="oper-item" @click="handleOperClick">
          *
        </div>
        <div class="oper-item" @click="handleClear">
          C
        </div>
      </div>
      <div class="oper-line">
        <div class="oper-item" @click="handleTextClick">
          1
        </div>
        <div class="oper-item" @click="handleTextClick">
          2
        </div>
        <div class="oper-item" @click="handleTextClick">
          3
        </div>
        <div class="oper-item" @click="handleOperClick">
          -
        </div>
      </div>
      <div class="oper-line">
        <div class="oper-item oper-db-width" @click="handleTextClick">
          0
        </div>
        <div class="oper-item" @click="handleFloorClick">
          .
        </div>
        <div class="oper-item" @click="handleOperClick">
          +
        </div>
        <div class="oper-item oper-sub" @click="handleResult">
          =
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data () {
    return {
      counted: false,
      editNumb: '0',
      topNumb: '0',
      maxLengthNum: 21,
      resultNum: 0
    }
  },
  computed: {
    maxLength () {
      return this.editNumb.slice(0, this.maxLengthNum)
    }
  },
  watch: {
    editNumb () {
    }
  },
  methods: {
    handleTextClick (e) {
      if (this.editNumb === '0' || this.counted) {
        this.editNumb = ''
        this.counted = false
      }
      this.editNumb = this.editNumb + (e.target.innerText)
    },
    handleOperClick (e) {
      this.topNumb = this.editNumb + ' ' + e.target.innerText
      this.resultNum = parseInt(this.editNumb)
      this.editNumb = '0'
      // console.log(this.resultNum)
    },
    handleClear () {
      this.editNumb = '0'
    },
    handleFloorClick (e) {
      if (this.editNumb.indexOf('.') === -1) {
        this.editNumb = this.editNumb + e.target.innerText
      }
    },
    handleResult () {
      const oper = this.topNumb.charAt(this.topNumb.length - 1)
      var realResult = 0
      try {
        switch (oper) {
          case '+':
            realResult = this.resultNum + parseInt(this.editNumb)
            break
          case '-':
            realResult = this.resultNum - parseInt(this.editNumb)
            break
          case '*':
            realResult = this.resultNum * parseInt(this.editNumb)
            break
          case '/':
            realResult = this.resultNum / parseInt(this.editNumb)
            break
          default:
        }
        this.editNumb = String(realResult)
        this.topNumb = '0'
        this.resultNum = 0
        this.counted = true
      } catch (e) {}
    },
    handleDeleteClick () {
      if (this.editNumb !== '0') {
        this.editNumb = this.editNumb.substring(0, this.editNumb.length - 1)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
  .result
    width:400px
    height:400px
    box-sizing:border-box
    margin:0 auto
    padding:30px
    background:#eee
    border-radius:4px
    .edit-line
      height:45px
      position:relative
      input
        font-size:20px
        text-align:right
        width:320px
        height:45px
        padding:20px 10px 10px 10px
        box-sizing:border-box
        border:1px solid #ddd
        border-radius:2px
      span
        position:absolute
        top:2px
        right:22px
        font-size:13px
        text-align:right
    .oper-box
      padding-top:10px
      position:relative
      .oper-line
        clear:both
        .oper-item
          border:1px solid #ddd
          width:46px
          line-height:46px
          height:46px
          text-align:center
          float:left
          background:#fff
          margin:10px
          border-radius:2px
          cursor:pointer
        .oper-db-width
          width:114px
        .oper-sub
          position:absolute
          bottom:-69px
          right:0
          height:114px
          line-height:114px
          background:#FFF2F2
          border-color:#FAA2A2
          font-weight:bold
</style>
