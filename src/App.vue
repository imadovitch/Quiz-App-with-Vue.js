<template>
  <div class="container-app">

        <div class="container-quiz">
          <div class="header-quiz">
            <h1>Quiz App</h1>
          </div>
          <div class="step-progress" :style="{'width':progress + '%'}"></div>
          <div class="box" v-for="(question,index) in questions.slice(a,b)" :key="index" v-show="quiz">
              
              <div class="box-question">
                <h2>Question {{b}}/{{questions.length}}</h2>
                <p>{{question.question}}</p>
              </div>
              <div class="box-propositions">
                <ul>
                  <li v-for="(proposition,index) in question.propositions" :key="index" class="li" @click="selectResponse(proposition,index)" :class=" correct ? check(proposition) : ''">{{proposition.props}} <div class="fas fa-check" v-if="correct ?  proposition.correct: ''"></div><div class="fas fa-times" v-if="correct ?  !proposition.correct: ''"></div></li>
                  
                </ul>
              </div>
              
              
          </div>
          <div class="box-score" v-if="score_show">
              
              
              <h2>Your score is</h2>
              <h2>{{score}}/{{questions.length}}</h2>
              <div class="btn-restart">
                  <button @click="restartQuiz">Restart <i class="fas fa-sync-alt"></i></button>
              </div>
          </div>
          <div class="footer-quiz">
                <div v-if="progress < 100" class="box-button">
                    <button  @click="skipQuestion()" :style="next ? 'background-color: rgb(106, 128, 202)' : ''">Skip</button>
                    <button  @click="nextQuestion()" :style="!next ? 'background-color: rgb(106, 128, 202)' : ''">Next</button>
                </div>  
                  
                  
                  
          </div>
          
          
            
        </div>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  data(){
    return{

      questions:[
        {
          question:"Inside which HTML element do we put the JavaScript ?",
          propositions:[
            {props:'<script>',correct:true},
            {props:'<js>'},
            {props:'<scripting>',},
            {props:'<javascript>',}
          ]
        },
        {
          question:"What is the correct syntax for referring to an external script called 'xxx.js' ?",
          propositions:[
            {props:'<script href="xxx.js">',},
            {props:'<script name="xxx.js">',},
            {props:'<script src="xxx.js">',correct:true},
            {props:'<script id="xxx.js">'},
            
          ]
          
        },
        {
          question:"How do you write 'Hello World' in an alert box ?",
          propositions:[
            {props:'msg("Hello World")'},
            {props:'alertBox("Hello World")'},
            {props:'alert("Hello World")',correct:true},
            {props:'msgBox("Hello World")'},
            
            
          ]
          
        },
        {
          question:"How to write an IF statement in JavaScript ?",
          propositions:[
            {props:'if i = 5 then',},
            {props:'if (i == 5)',correct:true},
            {props:'if i == 5 then',},
            {props:'if i = 5',},
            
            
          ]
          
        },
        {
          question:"How does a FOR loop start ?",
          propositions:[
            {props:'for i = 1 to 5',},
            {props:'for (i <= 5; i++)'},
            {props:'for (i = 0; i <= 5)'},
            {props:'for (i = 0; i <= 5; i++)',correct:true},
            
          ]
          
        },
        {
          question:"How can you add a comment in a JavaScript ?",
          propositions:[
            {props:"'This is a comment"},
            {props:'//This is a comment',correct:true},
            {props:'<!--This is a comment-->'},
            {props:'*This is a comment'},
            
          ]
          
        }
      ],
      a:0,
      b:1,
      next:true,
      score_show:false,
      quiz:true,
      score:0,
      correct:false,
      progress:0,
      
    }
  },
  name: 'App',
  components: {
    //HelloWorld
  },
  computed:{
      
  },
  methods:{
    
    selectResponse(e){
      this.correct = true;
      this.next = false;
      if (e.correct) {
        this.score++;
      }

    },
    check(status){
        if (status.correct) {
          return 'correct'
        }else{
          return 'incorrect' 
        }
    },
    nextQuestion(){
      if (this.next) {
        return;
      }
      this.progress = this.progress + (100/this.questions.length);
      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;    
      }
      else{
        this.a++;
        this.b++;
        this.correct = false;
        this.next = true;
        
      }
      
    },
    skipQuestion(){
      if (!this.next) {
        return;
      }
      this.progress = this.progress + (100/this.questions.length);

      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;
        
        
      }else{
        this.a++;
        this.b++;
        
      }
      
    },
    
    restartQuiz(){
      
      Object.assign(this.$data, this.$options.data()); // reset data in vue
       

    },
    
  }
}
</script>


