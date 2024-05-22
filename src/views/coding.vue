<template>
  <div>
    <h1>It is coding page</h1>
    <textarea class="fortext" v-model="intext" name="programming" id="program" @input="check"></textarea>
    <pre>{{ intext }}</pre>
    <hr>
    <pre><span v-for="(letter, index) in mytext" :key="index">{{ letter }}</span></pre>
  </div>
</template>

<script>
import * as CodeMirror from 'codemirror';
import 'codemirror/lib/codemirror.css';
import 'codemirror/theme/dracula.css';
import 'codemirror/mode/javascript/javascript.js';
import 'codemirror/mode/gfm/gfm.js';
import 'codemirror/addon/edit/closebrackets.js';
import 'codemirror/addon/edit/matchbrackets.js';
import {content, another} from '../mytext/text.js'

export default {
  data() {
    return {
      som: [],
      intext: "",
      mytext: another,
      mynum: 2,
    };
  },
  mounted() {
    this.editor = CodeMirror.fromTextArea(document.getElementById("program"), {
      lineNumbers: true,
      theme: 'dracula',
      mode: 'javascript',
      autoCloseBrackets: true,
      matchBrackets: true,
    });
    this.editor.setValue(this.intext);
    this.editor.on('change', () => {
      this.intext = this.editor.getValue();
      this.check();
    });
  },
  methods: {
    check(){
      if(this.intext.length){
        let plus = this.mynum;
        let wholeword = this.mytext;
        let length = this.intext.length
        let actext = this.mytext.substring(0,length)
        console.log(this.intext.charAt(length-1))
        console.log(plus)

        if(this.intext.charAt(length-2) == '('){
          let currentword = wholeword.substring(0, length-plus +1);
          for(let i=1; i<plus;i++){
            currentword += ')';
          }
          this.mynum++;
          console.log(currentword)
        }
        /*
        if(actext === this.intext){
          console.log("correct")
        }
        else{
          console.log("wrong")
        }*/
      }
      
    }
  }
};
</script>

<style scoped>
</style>
