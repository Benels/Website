<template>
  <Head>
    <Title>HERmet - Home</Title>
  </Head>

  <!--Home page of the website. It contains the logo and the slogan of the center, some links to these pages:
  About Us, Contact Us, Volunteer form, and Newest Activity. It has also and explanation of the chatbot,
  its functionalities and where to find it.-->

  <main>
    <div class="main-image-container">
      <!--decorative image-->
      <img class="image" src="/assets/imgs/homepage/homepage.jpg" alt="Missing Image"/>
      <div class="slogan">
        <img class="logo" src="/assets/imgs/Logo.svg"/> <p class="hermet">HERmet</p><br>
        Together We Stand:<br>
        <em>Women Helping Women build the life they aspire to live</em><br>
        <a href="/about_us" class="button">Learn more about us</a> <!--link to the About Us page-->
      </div>
    </div>

    <br><br>

    <div class="links-outer-container">

      <!--mobile version: first HERmet contacts-->
      <div class="links-inner-container" id="mobile">
        <div class="imageContainer">
          <img class="link-img" src="/assets/imgs/homepage/contacts.jpg" alt="Missing Image" />
        </div>
        <div class="link-text">
          <p>
            Need <strong>help</strong>?<br>
            <small><em>Reach out to us for confidential support and counseling</em></small> <br><br>
          </p>
          <a href="/contact_us" class="contacts-button">CONTACT US</a> <!--link to the Contact Us page-->
        </div>
      </div>

      <!--newest activity retrieved from the db-->
      <div class="links-inner-container">
          <div class="imageContainer">
            <img class="link-img" :src="`https://qpznxdvtbsibmwyurkfl.supabase.co/storage/v1/object/public/${type}/${activity.activity_id}.jpg`" :alt="`Missing Image`" />
          </div>
        <div class="link-text">
          <p>
            <strong>{{activity.name}} </strong><br>
            is our newest activity!<br>
          </p>
          <!--link to the activity's page-->
          <router-link :to="'/' + type + '/' + activity.activity_id" class="activity-button">Learn more</router-link>
        </div>
      </div>

      <!-- pc version: HERmet contacts in center-->
      <div class="links-inner-container" id="pc">
        <div class="imageContainer">
          <img class="link-img" src="/assets/imgs/homepage/contacts.jpg" alt="Missing Image" />
        </div>
        <div class="link-text">
          <p>
            Need <strong>help</strong>?<br>
            <small><em>Reach out to us for confidential support and counseling</em></small> <br><br>
          </p>
          <a href="/contact_us" class="contacts-button">CONTACT US</a> <!--link to the Contact Us Page-->
        </div>
      </div>

      <!--form to become volunteer-->
      <div class="links-inner-container">
        <div class="imageContainer">
          <img class="link-img" src="/assets/imgs/homepage/volunteers3.jpg" alt="Missing Image"/>
        </div>
        <div class="link-text">
          <p>
            <strong>Volunteer with us</strong> <br>
            <small><em>and be part of positive change!</em></small><br>
          </p>
          <a href="/volunteer" class="activity-button">Apply now</a> <!--link to the form-->
        </div>
      </div>
    </div>

    <div class="jarvis">
      <div class="jarvis-inner-container">

        <div class="jarvis-img">
          <!--decorative image of Jarvis, also to be connected to the icon of the chatbot's the button-->
          <img src="/assets/imgs/homepage/jarvis-img.jpg"/>
        </div>

        <div class="jarvis-text">
          <h2 class="jarvis-title">Meet Jarvis: <br id="mobile">your ally against stalking</h2><br>
          <p id="pc">Hi! I am <strong>Jarvis</strong>, nice to meet you! I am a chatbot dedicated to <strong>assisting victims of stalking</strong>.<br>
          I am available day and night, and I can provide to you essential information, safety tips, and
          guidance on taking protective measures. Reach out for <strong>discreet and immediate
          support</strong> whenever you need it.
          <br><br>
          I can also help you answer any questions you have regarding the center,
          however I cannot respond to unrelated topics.
          <br><br>
          Click on the button on the right and start a conversation.
          </p>
        </div>
      </div>

      <!--mobile version of the same text-->
      <p id="mobile">Hi! I am <strong>Jarvis</strong>, nice to meet you! I am a chatbot dedicated to <strong>assisting victims of stalking</strong>.<br>
        I am available day and night, and I can provide to you essential information, safety tips, and
        guidance on taking protective measures. Reach out for <strong>discreet and immediate
          support</strong> whenever you need it.
        <br><br>
        I can also help you answer any questions you have regarding the center,
        however I cannot respond to unrelated topics.
        <br><br>
        Click on the button on the right and start a conversation.
      </p>
    </div>
  </main>

</template>

<script setup>

//retrieve the most recent activity from the db
const {data: activities} = await useFetch('/api/activities/mostRecentActivity');
const activity = JSON.parse(JSON.stringify(activities.value))[0];

//check if the activity is a project or a service to use the correct link
let type;
if (activity.is_service)
  type = "services";
else type = "projects";

</script>

<style scoped>
.main-image-container {
  position: relative;
  width: 100%;
}

.image {
  width: 100%;
  height: auto;
}

.slogan{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 4vw;
  text-align: center;
  background-color: rgba(214, 40, 40, 0.5);
  padding: 5%;
  border-radius: 2rem;
  font-weight: bold;
  width: 70%;
  font-family: Caveat, sans-serif;
}

.slogan em{
  font-size: 3vw!important;
}

.logo{
  width: 15%;
  display: inline-block;
  -webkit-filter: drop-shadow(1px 1px 0 white) drop-shadow(-1px -1px 0 white);
  filter:drop-shadow(1px 1px 0 white) drop-shadow(-1px -1px 0 white);
}

.hermet{
  font-family: Rubik, sans-serif!important;
  font-size: 5vw!important;
  color: black!important;
  display: inline-block;
  text-shadow:
      -0.01rem -0.01rem 0 white,
      0.01rem -0.01rem 0 white,
      -0.01rem  0.01rem 0 white,
      0.01rem  0.01rem 0 white;
}

.button{
  background-color: white;
  color: #d62828;
  border: 0.3vw solid #d62828;
  border-radius: 1rem;
  font-family: Rubik, sans-serif!important;
  font-size: 1.7vw;
  padding: 1%;
}

.button:hover{
  background-color:#d62828;
  color: white;
  border: 0.3vw solid white;
}

.activity-button{
  background-color: rgba(214, 40, 40, 0.8);
  color: white;
  border: 0.2vw solid white;
  border-radius: 0.5rem;
  font-family: Rubik, sans-serif!important;
  font-size: 1.2vw;
  padding: 1%;
}

.activity-button:hover{
  background-color: white;
  color: #d62828;
  border: 0.2vw solid #d62828;
}

.contacts-button:hover{
  background-color: white;
  color: #d62828;
  border: 0.2vw solid #d62828;
}

.contacts-button{
  background-color: rgba(214, 40, 40, 0.8);
  color: white;
  border: 0.2vw solid white;
  border-radius: 0.5rem;
  font-family: Rubik, sans-serif!important;
  font-size: 1.8vw;
  padding: 1%;
}

.links-outer-container{
  display:flex;
  align-items: center;
}

.links-inner-container{
  position: relative;
  height: auto;
  padding: 2.5%;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  margin: 1%;
  width: v-bind("'33%'");
}

.imageContainer {
  width: 100%;
  height: 25vw;
}

.imageContainer > img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top;
  border-radius: 2rem;
}

.link-img{
  border-radius: 2rem;
}

.link-text{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: black;
  font-size: 1.8vw;
  text-align: center;
  background-color: rgba(255, 255, 255, 0.7);
  padding: 5%;
  border-radius: 2rem;
  width: 70%;
  height: 70%;
  align-content: center;
}

#mobile{
  display:none;
}

.jarvis{
  padding: 2% 6%;
  font-size: 1rem;
  border: 0.1rem solid #ddd;
  border-radius: 0.5rem;
  background-color: #f9f9f9;
  margin: 2% 10%;
  justify-content: center;
  align-items: center;
  text-align: justify;
}

.jarvis-inner-container{
  display:flex;
  gap: 5%;
}

.jarvis-text{
  display:flex;
  flex-direction: column;
}

.jarvis-text p{
  text-align: justify;
  font-size: 1.1vw;
}

.jarvis-img{
  display:flex;
  flex-direction: column;
  width: 20%;
  height: auto;
}

.jarvis-title{
  color: #d62828;
  font-size: 1.8vw!important;
  text-align: center;
  font-weight: bold;
}

@media(max-width: 768px){

  #pc{
    display: none;
  }

  #mobile{
    display: inherit;
  }

  .links-outer-container{
    display:inline-block;
    align-items: center;
  }

  .links-inner-container{
    position: relative;
    height: auto;
    padding: 2.5%;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    margin: 0;
    width: v-bind("'100%'");
  }

  .imageContainer {
    width: 100%;
    height: 100vw;
  }
  .link-text{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: black;
    font-size: 5vw;
    text-align: center;
    background-color: rgba(255, 255, 255, 0.7);
    padding: 5%;
    border-radius: 2rem;
    width: 70%;
    height: 70%;
    align-content: center;
  }

  .activity-button{
    font-size: 5vw;
  }

  .contacts-button{
    font-size: 6vw;
  }

  .jarvis-text p{
    text-align: justify;
    font-size: 2.5vw;
  }

  .jarvis-title{
    color: #d62828;
    font-size: 4vw!important;
    text-align: center;
    font-weight: bold;
  }
  .jarvis-inner-container{
    display:flex;
    gap: 5%;
    align-items: center;
  }

  .slogan{
    font-size: 5vw;
  }
  .slogan em{
    font-size: 4.5vw!important;
  }
}
</style>