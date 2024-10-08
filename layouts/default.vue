<template>
  <!-- 
    This layout overwrites the default one so that we can put landmarks in each page 
  -->


  <!-- insert the Navbar component + assign it to the navbar ref + handle the emitted event 'closeChatbot' by calling the closeChatbot function -->
  <Navbar @closeChatBot="closeChatbot" ref="navbar" />
  <!-- PAGE CONTENT -->
  <div class="content-container">
    <!-- the slot tag puts here the page content we define in each page -->
    <slot />
  </div>
  <!-- chatbot front end -->
  <div class="chatbotContainer fixed bottom-8 right-8 flex flex-col-reverse gap-2">
    <!-- chatbot circle -->
    <div class="z-32 w-20 h-20 overflow-hidden bg-white rounded-full border-2 border-[2px] border-red/50 flex justify-center items-center" @click.stop="handleChatbot">
      <!-- dimensions of the svg must be +2 w.r.t. the dimensions of the above div -->
      <img class="h-[105%] w-auto ml-[8px] mb-[15px]" src="~/assets/imgs/bender.png" alt="Bordered avatar" >
    </div>
    <div class="z-33 chatbot fixed right-10 pointer-events-none" ref="chatbotContainer">
      <!-- handle the emitted event 'handle' -->
      <Chatbot @handle="handleChatbot" />
    </div>
  </div>
  <!-- social circle + socials list -->
  <div class="hidden md:flex socialContainer fixed bottom-8 left-8 flex-col-reverse gap-2 items-center">
    <!-- social circle -->
    <div class="w-20 h-20 bg-white rounded-full border-2 border-[2px] border-red/50">
      <img class="p-3 -ml-[2px]" src="~/assets/imgs/social/share.png" alt="Bordered avatar" @click.stop="handleSocialListDisplay">
    </div>
    <!-- socials list -->
    <div class="socialLinks flex-col-reverse gap-2" ref="socialContainer">
      <a href="https://www.linkedin.com" target="_blank" aria-label="Link to Linkedin"><img class="w-12 h-12 rounded-full hover:cursor-pointer hoverEffectX" src="~/assets/imgs/social/linkedin.png" alt="Bordered avatar"></a>
      <a href="https://www.instagram.com" target="_blank" aria-label="Link to Instagram"><img class="w-12 h-12 rounded-full hover:cursor-pointer hoverEffectX" src="~/assets/imgs/social/instagram2.png" alt="Bordered avatar"></a>
      <a href="https://www.facebook.com" target="_blank" aria-label="Link to Facebook"><img class="w-12 h-12 rounded-full hover:cursor-pointer hoverEffectX" src="~/assets/imgs/social/facebook.png" alt="Bordered avatar"></a>
      <a href="https://www.twitter.com" target="_blank" aria-label="Link to Twitter"><img class="w-12 h-12 rounded-full hover:cursor-pointer hoverEffectX" src="~/assets/imgs/social/twitter.png" alt="Bordered avatar"></a>
    </div>

  </div>

  <!--The footer represents the bottom of every page of the website, it adapts to the screen dimension,
  having some feature based on which device is used. It contains:-->
  <footer class="footer md:items-center md:h-56 lg:h-36">
    <!--The website logo, useful also as an Home Page link-->
    <div class="md:w-3/4 md:w-4/5 md:items-center footer-container">
      <div class="lg:max-w-screen-lg flex-auto footer-logo-container">
        <div class="footer-logo">
          <NuxtLink to="/" title="Homepage" class="flex items-center space-x-3 rtl:space-x-reverse">
            <img src="~/assets/imgs/Logo.svg" alt="Logo" class="footer-img"/>
            <p class="self-center md:text-base lg:text-2xl font-semibold whitespace-nowrap">HERmet</p>
          </NuxtLink>
        </div>
        <p class="footer-text md:text-sm lg:text-base"><b>Always by your side</b></p>
      </div>
      <!--A brief recap on how to reach HERmet physically or virtually-->
      <div class="md:max-w-44 lg:max-w-80 flex-auto" >
          <span class="footer-text md:text-sm lg:text-base">Reach out to us whenever you need:<br> at Piazza Leonardo da Vinci 1 - MI, by
            calling
            <a class="number" href="tel:+393243453456">+39 324 345 3456</a> or sending an email to <u><a class="mail" href="mailto:10727489@polimi.it">frontdesk@hermet.com</a></u></span>
      </div>
      <!--A link to Volunteers page-->
      <div class="lg:max-w-screen-lg flex-auto lg:ml-4" >
          <span class="footer-text md:text-sm lg:text-base">Be part of the Change:<br><NuxtLink to="/volunteer"><u>Join HERmet now</u></NuxtLink>
           </span>
      </div>
    </div>
    <!--These social media logos act as a link to them, and they appears only on mobile, because social media button would
    occupy too many screen, covering lot of information-->
    <div class="md:hidden socialPhone self-left px-[1rem]">
      <a href="https://www.linkedin.com" target="_blank" aria-label="Link to Linkedin"><img class="w-10 h-10 rounded-full hover:cursor-pointer hoverEffectY" src="~/assets/imgs/social/linkedin.png" alt="Bordered avatar"></a>
      <a href="https://www.instagram.com" target="_blank" aria-label="Link to Instagram"><img class="w-10 h-10 rounded-full hover:cursor-pointer hoverEffectY" src="~/assets/imgs/social/instagram2.png" alt="Bordered avatar"></a>
      <a href="https://www.facebook.com" target="_blank" aria-label="Link to Facebook"><img class="w-10 h-10 rounded-full hover:cursor-pointer hoverEffectY" src="~/assets/imgs/social/facebook.png" alt="Bordered avatar"></a>
      <a href="https://www.twitter.com" target="_blank" aria-label="Link to Twitter"><img class="w-10 h-10 rounded-full hover:cursor-pointer hoverEffectY" src="~/assets/imgs/social/twitter.png" alt="Bordered avatar"></a>
    </div>
    <!--There are also text for credits to the team and a Copyright license-->
    <div class="self-left px-[1rem] mt-[4px]">
      <span class="footer-text md:text-sm lg:text-base">Credits: Benelle Francesco, Cavicchioli Michele, Lo Presti Irene, Lodelli Riccardo</span>
    </div>
    <div class="self-left px-[1rem]">
      <span class="footer-text md:text-sm lg:text-base">&copy 2024 HERmet ODV, All rights reserved</span>
    </div>
  </footer>
  <!-- <img class="absolute w-14 h-14 bottom-12 left-12" src="~/assets/imgs/icons8-futurama-bender.svg" alt="Bordered avatar"> -->
</template>

<script lang="ts" setup>

import Navbar from "~/component/Navbar.vue";
import { ref, onMounted, onBeforeUnmount } from "vue";

const displaySocialList = ref(false);
const socialContainer = ref();
function handleSocialListDisplay(event: any) {
  // handle the appearance of the socials list + handle transition delays
  if(!displaySocialList.value) {
    closeChatbot();
    displaySocialList.value = !displaySocialList.value;
    socialContainer.value.classList.add("displayBlock");
    setTimeout(() => {
      socialContainer.value.classList.add("setOpacity");
    }, 100);
  } else {
    displaySocialList.value = !displaySocialList.value;
    socialContainer.value.classList.remove("setOpacity");
    setTimeout(() => {
      socialContainer.value.classList.remove("displayBlock");
    }, 700);
  }
}

// close the social list
function closeSocialList(){
  displaySocialList.value = !displaySocialList.value;
  socialContainer.value.classList.remove("setOpacity");
  setTimeout(() => {
    socialContainer.value.classList.remove("displayBlock");
  }, 700);
}

import Chatbot from "~/component/Chatbot.vue";
const displayChat = ref(false);
const chatbotContainer = ref();

// handle the chatbot appearance 
function handleChatbot(event :any){
  if(!displayChat.value){
    // if the user wants to open the chatbot -> close the navbar and the social list + trigger animations + change state
    closeNavbar();
    closeSocialList();
    displayChat.value = !displayChat.value;
    chatbotContainer.value.classList.add("displayBlock");
    setTimeout(() => {
      chatbotContainer.value.classList.add("setOpacity");
    }, 50);
    document.body.classList.add("no-scroll");
  }else{
    closeChatbot();
  }
}

// function to close the chatbot + handle the transitions and the fixed scrolling
function closeChatbot() {
  displayChat.value = false;
  //displayChat.value = !displayChat.value;
  chatbotContainer.value.classList.remove("setOpacity");
  setTimeout( () => {
    chatbotContainer.value.classList.remove("displayBlock");
    document.body.classList.remove("no-scroll");
  }, 700);
}


const navbar = ref();

function closeNavbar() {
  navbar.value.closeNavbar();
}

function closeAll() {
  closeNavbar();
  closeSocialList();
  closeChatbot();
}

// close everything (chatbot, social list, navbar)
function handleClickOutside(event: MouseEvent) {
  const target = event.target as HTMLElement;
  if (
      !navbar.value.$el.contains(target) &&
      !socialContainer.value.contains(target) &&
      !chatbotContainer.value.contains(target)
  ) {
    closeAll();
  }
}

// on mount add the event listener to close everything when a general click is done 
onMounted(() => {
  document.addEventListener('click', handleClickOutside);
});

// remove a possible previous event listener (ensures only one listener
onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside);
});
</script>

<style>

::-webkit-scrollbar {
  display: none;  /* Safari and Chrome */
}

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: linear-gradient(
      to bottom,
      rgb(235 235 235 / 94%),
      rgb(235 235 235 / 94%)
  ), url('assets/imgs/our_women_bg.jpg') repeat;  color: black;
  font-family: 'Rubik', sans-serif;
  -ms-overflow-style: none; /* Internet Explorer 10+ */
    scrollbar-width: none; /* Firefox */
}

body {
  background-attachment: fixed;
}

.content-container {
  margin-top: 72px;
}


.socialPhone {
  display: none;
}

.socialLinks {
  transition: opacity 1s ease;
  opacity: 0;
  display: none;
}

.hoverEffectX:hover {
  transform: translateX(0.5rem);
}

.hoverEffectY:hover {
  transform: translateY(-0.5rem);
}
/*.socialLinks:hover{
  transform: translateX(0.5rem);
}*/

.chatbot{
  transition: opacity 1s ease;
  opacity: 0;
  display: none;
  width: 500px;
}

.chatbotContainer,
.socialContainer {
  z-index: 31;
}

.chatbotContainer:hover,
.socialContainer:hover {
  cursor: pointer;
}

.setOpacity {
  opacity: 1 !important;
}

.displayBlock {
  display: flex !important;
}


.footer {
  background-color: #d62828;
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  /* padding: 1rem; */
  position: relative;
  width: 100vw;
  height: auto;
  z-index: 1;
  margin-top: 2rem;
  margin-bottom: 0;
}

.footer-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  /* height: 9rem; */
  /* flex-wrap: wrap; */
  background-color: #d62828;
  padding: 1rem;
}

.footer-logo-container {
  display: flex;
  flex-direction: column;
}

.footer-logo {
  display: flex;
  flex-direction: row;
  align-items: center;
  width: 100%;
}

.footer-img {
  height: 5rem;
  margin-right: 0.5rem;
  -webkit-filter: drop-shadow(1px 1px 0 white) drop-shadow(-1px -1px 0 white);
  filter:drop-shadow(1px 1px 0 white) drop-shadow(-1px -1px 0 white);
}


.footer-text {
  text-align: center;
  font-family: 'Rubik', sans-serif;
}

.external{
  margin: 0;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(
      to bottom,
      rgb(235 235 235 / 98%),
      rgb(235 235 235 / 95%)
  ), url('assets/imgs/our_women_bg.jpg') repeat;
  position: relative;
}

@media (max-width: 768px) {
  .chatbot {
    top: 72px;
    z-index: 10;
    width: 100vw;
    max-width: 500px;
    height: calc(100vh - 72px);
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
  }

  .footer {
    /* height: 25rem; */
    justify-content: flex-end;
  }

  .footer-container {
    display: flex;
    flex-direction: column;
    align-items: normal;
    justify-content: left;
    width: 100vw;
    /* height: 80%; */
    gap: 1rem;
  }

  .footer-logo {
    width: 5%;
  }
  .footer-img {
    height: 100%;
    margin-right: 0;
  }
  .socialPhone {
    display: flex;
    justify-content: flex-start;
    gap: 5px;
    margin: 0;
    /* position: absolute; */
    /* bottom: 1rem;
    left: 1rem;
    max-width: 45%; */
  }

  .no-scroll {
    overflow: hidden;
    height: 100%;
  }

  #footer-text-container {
    flex:0;
  }
}

</style>