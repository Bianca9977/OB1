<template>
  <div class="hello">
    <!-- <h1>{{ "Title" }}</h1> -->
    <div v-for="(contentItem, index) in content" :key="contentItem">
      <div v-show="index == currentPage">
       <!--  Page {{ index }} -->
        <div class="circle-menu mt-5">
            <div class="circle-1" :class="currentPage == 0 ? 'active-circle' : ''">
              1
            </div>
            <div class="line" :class="currentPage < 1 ? 'inactive-line' : ''"></div>
            <div class="circle-2" :class="currentPage == 1 ? 'active-circle' : currentPage < 1 ? 'inactive-circle' : ''">
              2
            </div>
             <div class="line" :class="currentPage < 2 ? 'inactive-line' : ''"></div>
            <div class="circle-3" :class="currentPage == 2 ? 'active-circle' : currentPage < 2 ? 'inactive-circle' : ''">
              3
            </div>
             <div class="line" :class="currentPage < 3 ? 'inactive-line' : ''"></div>
            <div class="circle-4" :class="currentPage == 3 ? 'active-circle' : currentPage < 3 ? 'inactive-circle' : ''">
              4
            </div>
        </div>
        <Page v-bind:pageContent="contentItem" v-bind:pageIndex="currentPage" />
      </div>
    </div>

    <div class="container d-flex justify-content-between mb-5">
      <button class="previous-button" v-on:click="previous" v-show="isPrevious()">
        Previous
      </button>

      <button class="next-button" v-on:click="next" v-show="isNext()">
        Next
      </button>
    </div>
    <div style="height: 100px"></div>
  </div>
</template>

<script>
import Page from "./page.vue";

export default {
  name: "Mainpage",
  components: {
    Page,
  },
  methods: {
    next() {
      this.currentPage++;
    },
    previous() {
      this.currentPage--;
    },
    isNext() {
      return this.currentPage < this.content.length - 1;
    },
    isPrevious() {
      return this.currentPage > 0;
    },
  },

  data: function() {
    return {
      currentPage: 0,
      content: [
        [
          {
            text: "first text",
            question: {
              text: "Bunyana is 72 years old woman, who is leaving in the countryside area of Bunagana. She did not attend schools, but she is a rich farmer. Among the following statement, what is true about Bunyana?",
              responses: [{ text: "She may tend to use more of preventive care approaches" }, { text: "She may tend to use less expensive health-care services."}, { text: "She may tend to use more medicine.", correct: true }],
              feedback: "audio", //visual, audio, visualaudio or none
            },
          },
          /* {
            text: "second text",
            question: {
              text: "Question 2",
              responses: [{ text: "Wrong" }, { text: "Right!", correct: true }],
              feedback: "audio", //visual, audio, visualaudio or none
            },
          }, */
        ],

        //second page
        [
          {
            text: "",
            question: {
              text: "Kalisa is 19 years old, and he is a student at St Peter’s High school. Last year, Kalisa has recovered from tuberculosis from which he suffered for 3 years. Among, the following statements, what is true about Kalisa:",
              responses: [{ text: "Kalisa would tend to use emergency services for infectious diseases." }, { text: "Kalisa would tend to use more expensive medicine against infectious diseases."}, { text: "Kalisa would tend to use more preventive methods to fight infectious diseases.", correct: true}],
              feedback: "audio", //visual, audio, visualaudio or none
            },
          },
          /* {
            text: "second text",
            question: {
              text: "Question 2",
              responses: [{ text: "Wrong" }, { text: "Right!", correct: true }],
              feedback: "audio", //visual, audio, visualaudio or none
            },
          }, */
        ],

        //third page
        [
          {
            text: "third page first text",
            question: {
              text: "Which of the following statements is correct?",
              responses: [{ text: "It is common for everyone who is not a clinician or a pharmacist to misunderstand drug labels or have trouble following their directions." }, { text: "It is common for people living in rural and remote areas to misunderstand drug labels or have trouble following their directions."}, { text: "It is common for people with limited health literacy to misunderstand drug labels or have trouble following their directions.", correct: true}],
              feedback: "audio", //visual, audio, visualaudio or none
            },
          },
      /*     {
            text: "second text",
            question: {
              text: "Question 2",
              responses: [{ text: "Wrong" }, { text: "Right!", correct: true }],
              feedback: "audio", //visual, audio, visualaudio or none
            },
          }, */
        ],

        [
           {
            text: "",
            question: {
              text: "Which of the following statements is correct?",
              responses: [{ text: "It is hard for everyone to know when it is appropriate to go to the emergency room rather than a primary care doctor." }, { text: "It is hard for people without medical training to know when it is appropriate to go to the emergency room rather than a primary care doctor."}, { text: "It is hard for people with limited health literacy to know when it is appropriate to go to the emergency room rather than a primary care doctor.", correct: true}],
              feedback: "audio", //visual, audio, visualaudio or none
            },
          }
        ]
      ],
    };
  },
};
</script>
<style lang="scss" scoped>
@import '../scss/app.scss';

.container {
  position: relative;
}

.previous-button, .next-button {
  width: 180px;
  height: 60px;
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.05);
  border: none;
  border-radius: 100px;
  font-size: 20px;
  margin: 70px 0px;
  background: $color_lightPink;
  color: $color_darkPurple;
  position: absolute;
  top: -20px;

  &:hover {
    background: $color_lilac;
    color: white;
  }

  &:active {
    outline: none !important;
  }
}

.previous-button {
  left: 0;
}

.next-button {
  right: 0;
}

.previous-button::before, 
.previous-button:hover::before {
  content: ''; 
  display: inline-block;
  background: url('../assets/darkArrow.png');
  background-size: contain;
  background-repeat: no-repeat;
  width: 20px;
  height: 20px;
  transform: rotate(180deg);
  margin-right: 1rem;
}

.next-button::after, 
.next-button:hover::after {
  content: ''; 
  display: inline-block;
  background: url('../assets/darkArrow.png');
  background-size: contain;
  background-repeat: no-repeat;
  width: 20px;
  height: 20px;
  margin-left: 1rem;
  position: relative;
  top: 6px;
}

.previous-button:hover::before, 
.next-button:hover::after {
  background: url('../assets/whiteArrow.png') !important;
  background-size: contain !important;
  background-repeat: no-repeat !important;
}

.previous-button,
.next-button  {
  .arrow { 
   width: 30px;
  }
}

.previous-button .arrow {
  transform: rotate(180deg);
}

.circle-menu {
  display: flex;
  justify-content: center;
  align-content: center;
  margin-bottom: 80px;
}

.circle-menu {
   .circle-1, .circle-2, .circle-3, .circle-4 { 
    width: 45px;
    height: 45px;
    background: white;
    border: 5px solid $color_darkPurple;
    border-radius: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 32px;
    color:$color_darkPurple;
    font-weight: 600;
    box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.05);
   }

   .line {
    width: 140px;
    border-bottom: 8px solid $color_darkPurple;
    position: relative;
    bottom: 18px;

    &.inactive-line {
      border-bottom: 8px solid $color_lightPurple;
    }
   }

  .active-circle {
    background-color: $color_darkPurple;
    color: white;
  }

  .inactive-circle {
    background-color: white;
    border: 5px solid $color_lightPurple;
  }
}

</style>
<!-- Add "scoped" attribute to limit CSS to this component only -->
