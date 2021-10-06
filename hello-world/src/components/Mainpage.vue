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
              text: "To seek, find, understand, and appraise health information from electronic sources require different skills, which are englobed in what is called digital health literacy. Among the following, which is irrelevant for digital health literacy?",
              responses: [{ text: "The ability to use search engines." }, { text: "The ability to read English", correct: true}, { text: "The ability to understand relevant health terms." }],
              feedback: "visual", //visual, audio, visualaudio or none
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
              text: "Which of the following is one of the major barriers to the achievement of digital health literacy in the population?",
              responses: [{ text: "Poor interaction between health-care workers and health-consumers" }, { text: "Lack of ability to navigate into the health systems.", correct: true}, { text: "Time to navigate into digital health systems."}],
              feedback: "visual", //visual, audio, visualaudio or none
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
              responses: [{ text: "Limited digital literacy can increase health disparities in low-income countries.", correct: true }, { text: "A limited number of advanced e-health systems can increase health disparities in low-income countries."}, { text: "A limited number of health workers who understand the functionalities of e-health systems can increase health disparities in low-income countries."}],
              feedback: "visual", //visual, audio, visualaudio or none
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
              text: "The use of health information over the internet comes up with different advantages. Those include:",
              responses: [{ text: "Insured anonymity while searching health information." }, { text: "Quick access to the variety of health-behavior tips.", correct: true}, { text: "Access to organized and accurate information."}],
              feedback: "visual", //visual, audio, visualaudio or none
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
