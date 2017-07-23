<template>
  <div>
    <div class="hero-1">
      <div class="upper">
        <div class="logo-container animate a-2">
          <img class="logo" src="~assets/logo.jpg"></img>
        </div>
        <div class="mission-text animate a-4">
          Learn to dance with Rachna!
        </div>
      </div>
    </div>

    <div class="wrapper">
      <div class="bg-row pre-colors">
        <div class="container" id="services">
          <div class="row column">
            <div class="header-container">
              <div class="row-header">
                Services
              </div>
            </div>
            <div class="services">
              <div class="four columns service center animate a-1">
                <div> <img src="~assets/rachna2.jpg" class="thumbnail" /> </div>
                <div class="title">Event Choreography</div>
                <div class="message">
                  We would love to help you create a dance for your special event that you and your audience will remember forever! 
                  <div class="register" @click="toSection($event, 'contact')">Contact me below for details.</div>
                </div>
              </div>

              <div class="four columns service center animate a-2">
                <div><img src="~assets/rachna3.jpg" class="thumbnail" /></div>
                <div class="title">Online Classes</div>
                <div class="message">
                  1-on-1 personalized online classes, tailored to your preference of curriculum. Styles include Bollywood, 
                  Bhangra, Folk, or Fusion
                  <div class="register" @click="toSection($event, 'contact')">Contact me below for details.</div>
                </div>
              </div>

              <div class="four columns service center animate a-3">
                <div><img src="~assets/rachna5.jpg" class="thumbnail" /></div>
                <div class="title">Group Classes</div>
                <div class="message">
                  Classes last five weeks and will revolve around the different dance styles that hail from India. 
                  No experience is necessary. Just come and enjoy moving to the music! <span class="register" @click="toSection($event, 'classes')">Click Here for more info.</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="line"></div>
      <div class="colors">
        <div class="row colors">
          <div class="dance-style folk">Folk</div>
          <div class="dance-style fusion">Fusion</div>
        </div>
        <div class="dance-styles">
          Dance Styles
        </div>
        <div class="row colors">
          <div class="dance-style bollywood">Bollywood</div>
          <div class="dance-style bhangra">Bhangra</div>
        </div>
      </div>
      <div class="line"></div>
      <div class="bg-row">
        <div class="container" id="mission">
          <div class="header-container">
            <div class="row-header">
              Mission
            </div>
          </div>
          <div class="row">
            <div class="six columns animate a-1">
              <div class="pic p1"></div>
            </div>
            <div class="six columns no-margin animate a-2">
              <div class="info">
                <div class="title">Rachna Chhaya</div>
                Rachna Chhaya is extremely passionate about culture, dance, and music. She is continuously inspired by all 
                kinds of melodies and movements, and aims to spread the feeling of pure joy that these elements can bring to 
                members in her community, no matter what level of experience they may bring with them.
              </div>
              <div class="info">
                Rachna has been trained in Bharatanatyam since the age of 5 under her Guru, Mrs. Chaula Thacker, and 
                completed her Arangetram in 2010. She continued to perform and choreograph for several groups around her, 
                and founded Michigan State University's first ever Fusion Team with her best friends in 2014. Rachna is 
                also extremely well-versed and self-trained in Bhangra, and is currently studying Kathak as well. 
                She hopes to continue studying different traditional and folk styles from India to allow her to expand her creative knowledge,
                 and serve as a medium between the Indian musical culture and the general public.
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="line"></div>
      <div class="bg-row">
        <div class="container" id="classes">
          <div class="row column">
            <div class="header-container">
              <div class="row-header">
                Classes
              </div>
              <div class="info-container">
                <div>
                  <strong>Where:</strong> Synergy Dance Academy, Plymouth MI
                </div>
                <div>
                  <strong>Time:</strong> 8:00 PM
                </div>
              </div>
            </div>
            <div class="classes">
              <div class="class" v-for="(c, i) in classes" :class="['animate', `a-${i+1}`, pastTime(c.time)]">
                <div v-if="!c.success">
                  <div class="u-full-width u-cf">
                    <div class="u-pull-left calendar">
                      <div class="icon-cal"> </div>
                    </div>
                    <div class="u-pull-right day-title">
                      <div> {{ c.time | moment('MM/DD') }} </div>
                      <div> {{ c.time | moment('dddd') }} </div>
                    </div>
                  </div>
                  <transition name="fade">
                    <div class="content passed" v-if="new Date().getTime() > c.time" key="pasttime">
                      Not Available
                    </div>
                    <div class="content selectable" v-else-if="!c.selected && !c.success" key="selectable">
                      <div class="button big-button" @click="selectClass($event, c.time)">Sign Up</div>
                    </div>
                    <div class="content scooched" v-else key="selected">
                      <form v-on:submit.prevent="submitClass(c, 'class')" data-vv-scope="class">
                        <div class="u-full-width">
                          <label for="email" :class="{'is-danger': errors.has(`class.email_${i}`)}">Email</label>
                          <input class="u-full-width email" :class="{'is-danger': errors.has(`class.email_${i}`)}" type="email" v-validate="'required|email'" :name="`email_${i}`" placeholder="test@mailbox.com" id="email" v-model="c.fromEmail">
                        </div>
                        <div class="u-full-width">
                          <label for="name" :class="{'is-danger': errors.has(`class.name_${i}`)}">Name</label>
                          <input class="u-full-width name" :name="`name_${i}`" :class="{'is-danger': errors.has(`class.name_${i}`)}" v-validate="'required'" type="text" placeholder="Bob Dylan" id="name" v-model="c.name">
                        </div>
                        <button type="submit" :class="{ 'disabled': c.loading }" class="button-primary"> {{ c.loading ? 'Processing' : 'Submit' }}</button>
                      </form>
                    </div>
                  </transition>
                </div>
                <div class="success" v-else>
                  Success
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="line"></div>
      <div class="bg-row">
        <div class="container" id="testimonials">
          <div class="row column">
            <div class="header-container">
              <div class="row-header">
                Testimonials
              </div>
            </div>
            <div class="services">
              <div class="six columns testimonial">
                <!-- <iframe width="100%" height="100%" src="https://www.youtube.com/embed/v15Wu8TseS4" frameborder="0" allowfullscreen></iframe> -->
                <div>
                  Her energy and enthusiasm are apparent in everything she does. She is an
                  extremely talented choreographer with experience and accomplishments in various styles from all across the world. Her ability to learn/teach all 
                  these different styles not only shows her talent, but her true love of dance. She has the special ability to always bring a smile to people's faces, 
                  making Rachna one of the most fun and talented performers that I have ever been around.
                </div>
                <div class="twelve columns sub-text-container left">
                  <div class="sub-text thumbnail-container"><img class="testimonial-thumbnail" src="~assets/testimonial2.jpg" /></div>
                  <div class="sub-text">
                    <div>Omkar Vale</div>
                    <div class="relation">Dance Team Co-Founder</div>
                  </div>
                </div>
              </div>
              <div class="six columns testimonial">
                <div>
                  Learning to dance with Rachna was a great experience. She is a very good listener and teacher for participants of all levels. 
                  We had not danced often before and she choreographed for us and made it a lot easier to learn and adapt. We both had a lot of 
                  fun while learning and performing. We encourage everyone to certainly give her an opportunity to teach you. She is a very talented, 
                  proven artist.
                </div>
                <div class="twelve columns sub-text-container right">
                  <div class="sub-text">
                    <div>Dhaval and Nina Kikani</div>
                    <div class="relation">A happy client</div>
                  </div>
                  <div class="sub-text thumbnail-container"><img class="testimonial-thumbnail" src="~assets/testimonial1.jpg" /></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="hero-2">
      <div class="upper">
        <div class="img-card" id="contact">
          <form v-on:submit.prevent="submitMessage('message')" data-vv-scope="message" class="contact-container">
            <div class="row-header contact">
              Contact Rachna
            </div>
            <div class="row contact">
              <div class="six columns">
                <label for="email" :class="{'is-danger': errors.has('message.messageEmail')}">Email Address</label>
                <input class="u-full-width email" :class="{'is-danger': errors.has('message.messageEmail')}" type="email" v-validate="'required|email'" name="messageEmail" placeholder="test@mailbox.com" id="email" v-model="messageEmail">
              </div>
              <div class="six columns">
                <label for="messageName" :class="{'is-danger': errors.has('message.messageName')}">Name</label>
                <input class="u-full-width name" :class="{'is-danger': errors.has('message.messageName')}" type="text" v-validate="'required'" name="messageName" placeholder="Bob Dylan" id="name" v-model="messageName">
              </div>
            </div>
            <label for="exampleMessage" :class="{'is-danger': errors.has('message.message')}">Message</label>
            <textarea class="u-full-width message" name="message" :class="{'is-danger': errors.has('message.message')}" v-validate="'required'" placeholder="Hi Rachna …" id="exampleMessage" v-model="message"></textarea>
            <div class="center-text">
              <button class="button-primary" type="submit" :class="{ 'message-success': success, 'disabled': messageLoading }">{{ success ? 'Your message was sent!' : 'Submit' }}</button>
            </div>
          </form>
        </div>
      </div>
      <div class="footer">
        <div class="row">
          <div class="twelve columns">
            <div class="plug">
              <div>Made with love by</div>
              <div>Tanay Salpekar</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery'
import moment from 'moment'
import velocity from 'velocity-animate'

export default {
  data () {
    return {
      startDate: moment().month(7).date(17).year(2017).hours(20).minutes(0).seconds(0).valueOf(),
      $animationElements: null,
      $window: null,
      $nav: null,
      $hero: null,
      selected: null,
      messageName: null,
      messageEmail: null,
      messageLoading: false,
      messageSuccess: false,
      message: null,
      name: null,
      fromEmail: null,
      classes: [
        {
          time: new Date().getTime(),
          where: 'Synergy Dance Academy',
          cost: 10,
          selected: false,
          success: false,
          loading: false
        },
        {
          time: new Date().getTime(),
          where: 'Synergy Dance Academy',
          cost: 10,
          selected: false,
          success: false,
          loading: false
        },
        {
          time: new Date().getTime(),
          where: 'Synergy Dance Academy',
          cost: 10,
          selected: false,
          success: false,
          loading: false
        },
        {
          time: new Date().getTime(),
          where: 'Synergy Dance Academy',
          cost: 10,
          selected: false,
          success: false,
          loading: false
        },
        {
          time: new Date().getTime(),
          where: 'Synergy Dance Academy',
          cost: 10,
          selected: false,
          success: false,
          loading: false
        }
      ]
    }
  },

  computed: {
    success () {
      return this.messageSuccess && !this.messageLoading
    }
  },

  mounted () {
    this.$animationElements = $('.animate')
    this.$window = $(window)
    this.$nav = $('.navbar')
    this.$hero = $('.hero-1')
    this.$window.on('scroll', this.checkInView)
    this.$window.on('scroll resize', this.checkInView)
    this.$window.trigger('scroll')
    let i = 0
    this.classes.forEach(cl => {
      cl.time = moment(this.startDate).add(i, 'weeks').valueOf()
      i += 1
    })
  },

  methods: {
    pastTime (time) {
      return new Date().getTime() > time ? 'passed' : null
    },

    toSection (e, section) {
      let el = document.querySelector('#' + section)
      velocity(el, 'scroll', { offset: '-70', easing: 'ease', duration: 800 })
    },

    selectClass (el, time) {
      $('.class').removeClass('selected')
      $(el.target).closest('.class').addClass('selected')

      this.classes.forEach(cl => {
        if (cl.time === time) {
          cl.selected = true
        } else {
          cl.selected = false
        }
      })
    },

    submitMessage (scope) {
      let fromEmail = this.messageEmail
      let name = this.messageName

      let subject = `Special Message from ${fromEmail}`
      let message = this.message
      return this.$validator.validateAll(scope)
        .then(result => {
          if (result) {
            this.messageLoading = true
            return this.sendEmail(fromEmail, name, subject, message)
          } else {
            return Promise.reject()
          }
        })
        .then(() => {
          this.messageLoading = false
          this.messageSuccess = true
        })
    },

    submitClass (c, scope) {
      let fromEmail = c.fromEmail
      let name = c.name
      let dateTime = moment(c.time).format('MM/DD [at] hh:mm')
      let subject = `Class Registration on ${dateTime}`
      let body = `${name} signed up for a class on ${dateTime}`

      return this.$validator.validateAll(scope)
        .then(result => {
          if (result) {
            c.loading = true
            return this.sendEmail(fromEmail, name, subject, body)
          }
          else return Promise.reject()
        })
        .then(() => {
          c.loading = false
          c.selected = false
          c.success = true
        })
    },

    sendEmail (fromEmail, fromName, subject, message) {
      // hit api and success
      return $.ajax({
          url: 'https://formspree.io/dilsedance.mi@gmail.com',
          method: 'POST',
          data: {
            fromEmail: fromEmail,
            fromName: fromName,
            subject: subject,
            message: message
          },
          dataType: 'json'
      })
    },

    checkInView (el) {
      var wHeight = this.$window.height();
      var wTop = this.$window.scrollTop();
      var wBottom = (wTop + wHeight);

      var heroBottom = this.$hero.height() + this.$hero.scrollTop()
      var heroTop = this.$hero.offset().top
      var navTop = this.$nav.height()
      var navBottom = this.$nav.outerHeight() + this.$nav.scrollTop()
      if (wTop >= (heroBottom - (navBottom / 2))) {
        this.$nav.addClass('transition')
      } else {
        this.$nav.removeClass('transition')
      }


      $.each(this.$animationElements, function() {
        var $element = $(this);
        var elHeight = $element.outerHeight();
        var elTop = $element.offset().top + 100;
        var elBottom = (elTop + elHeight);

        //check to see if this current container is within viewport
        if ((elBottom >= wTop) && (elTop <= wBottom)) {
          let duration = 300
          let multiplier = 1
          if ($element.hasClass('a-1')) multiplier = 1
          else if ($element.hasClass('a-2')) multiplier = 1.6
          else if ($element.hasClass('a-3')) multiplier = 2.2
          else if ($element.hasClass('a-4')) multiplier = 2.8
          else if ($element.hasClass('a-5')) multiplier = 3.4
          else if ($element.hasClass('a-6')) multiplier = 4.0

          setTimeout(() => {
            $element.addClass('in');
          }, duration * multiplier)

        } else {
          // $element.removeClass('in-view');
        }
      })
    }
  }
}
</script>

<style lang='scss' scoped>
@import "../stylesheets/_vars.scss";

.logo {
  position: relative;
  height: 100%;
  width: 100%;
}

.mission-text {
  opacity: 0;
}

.testimonial-thumbnail {
  height: 70px;
  width: 70px;
  border-radius: 70px;
  margin-right: 10px;
  margin-left: 10px;
  display: inline-block;
}

.animate {
  opacity: 0;
  transform: translate3d(0px, 50px, 0px);
  transition: transform .3s ease, opacity .3s ease;
  &.in {
    transform: translate3d(0px, 0px, 0px);
    opacity: 1;
  }
}

.hero-1, .hero-2 {
  height: 90vh;
  background-size: cover;
  background-attachment: fixed;
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: relative;
  flex-direction: column;
  width: 100%;
}

.register {
  color: #ffffff;
  font-weight: 700;
  cursor: pointer;
  font-size: 16px;
  transition: color .3s ease;
  &:hover {
    color: darken(#ffffff, 15%);
  }
}

.button-primary {
  &.disabled {
    background-color: rgba(0, 0, 0, .3);
    border-color:rgba(0, 0, 0, .3);
    pointer-events: none;
  }
}

.hero-1 {
  background-image: url('~assets/cover-dancing.jpg');
  background-position: 50% 50%;
}

.hero-2 {
  background-image: url('~assets/rachna4.jpg');
  background-position: 50% 20%;
}

.help {
  text-align: left;
}

.is-danger {
  color: red;
  border-color: red;
}


.wrapper {
  padding-top: 1%;
  padding-bottom: 1%;
  position: relative;
  width: 100%;
}

.p2 {
  float: right;
}


.calendar {
  padding: 15px;
  .icon-cal {
    background-image: url(~assets/calendar.svg);
    height: 24px;
    width: 24px;
    display: inline-block;
  }
}

.service {
  display: flex;
  overflow-y: auto;
  min-height: 400px;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-right: 1%;
  margin-left: 0;
  background: #DDDEDF;
  padding: 15px;
  border-radius: 4px;
  color: #ffffff;
  box-shadow: 0 10px 20px 0 rgba(0,0,0,.08);
  &.center { text-align: center; }
  margin-top: 5px;

  .title {
    font-size: 24px;
    font-weight: 700;
    height: 50%;
  }

  .message {
    font-size: 14px;
    line-height: 30px;
    height: 100%;
  }

  .thumbnail {
    height: 160px;
    width: 160px;
    margin-bottom: 20px;
    border-radius: 160px;
  }

  &:last-child { background: #007EA7; margin-right: 0; }
  &:nth-child(2) { background: darken(#007EA7, 12.5%); }
  &:first-child { background: darken(#007EA7, 25%);; }
}

.testimonial {
  min-height: 400px;
  margin-right: 1%;
  margin-top: 5px;
  margin-left: 0;
  background: #DDDEDF;
  padding: 25px 25px 10px 25px;
  border-radius: 4px;
  color: #000000;
  position: relative;
  box-shadow: 0 10px 20px 0 rgba(0,0,0,.08);
  &.scrollable { overflow-y: scroll; }
  overflow-y: hidden;
  line-height: 32px;
  font-size: 20px;
  position: relative;

  .thumbnail-container {
    display: inline-block;
  }

  .sub-text-container {
    margin-top: 20px;
    &.right { text-align: right; }
    &.left { text-align: left; }
  }

  .sub-text {
    vertical-align: top;
    font-size: 16px;
    font-weight: 600;
    display: inline-block;
    .relation {
      color: lighten(#000000, 40%);
    }
  }
 }

.footer {
  padding: 5px;
  position: absolute;
  bottom: 0;
  border-radius: 4px;
  color: #ffffff;
  z-index: 5000;
}

.plug {
  text-align: left;
  font-size: 13px;
}

.testimonial.video {
  padding: 0;
  background: transparent;
  height: 400px;
  overflow: hidden;
}

.services {
  display: flex;
  align-items: stretch;
  justify-content: stretch;
  flex-direction: column;
}

.classes {
  min-height: 325px;
  width: 100%;
  overflow-x: auto;
  white-space: nowrap;
  overflow-y: hidden;

}

.success {
  width: 100%;
  height: 100%;
  position: absolute;
  background: rgba(0, 178, 98, 1);
  color: #ffffff;
  font-size: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4px;
  text-align: center;
}

.message-success {
  pointer-events: none;
  background: rgba(0, 178, 98, 1) !important;
  border-color: rgba(0, 178, 98, 1) !important;
}

.class {
  height: 300px;
  width: 250px;
  margin-right: 5px;
  background: #DDDEDF;
  border-radius: 4px;
  margin-top: 5px;
  display: inline-block;
  transition: all .3s ease;
  position: relative;

  &:last-child {
    margin-right: 0;
  }

  .content {
    position: absolute;
    padding: 15px;
    text-align: center;
    height: 50%;
    top: 40%;
    white-space: wrap;
    width: 220px;
  }

  .content.selectable {
    font-size: 40px;
    text-transform: uppercase;
  }

  .content.scooched {
    top: 20%;
  }

  .content.passed {
    top: 45%;
    pointer-events: none;
  }

  &.passed::before {
    content: '';
    z-index: 10;
    display: block;
    position: absolute;
    height: 100%;
    top: 0;
    left: 0;
    right: 0;
    background: rgba(255, 255, 255, 0.6);
  }

  .day-title {
    text-transform: uppercase;
    font-weight: 600;
    font-size: 14px;
    padding: 15px;
    border-left: 1px solid darken(#DDDEDF, 20%);
    border-bottom: 1px solid darken(#DDDEDF, 20%);
    border-radius: 4px;
    text-align: right;
  }
}

.header {
  font-size: 18px;
  text-align: center;
  height: 40px;
  width: 100%;
  padding-top: 10px;
  display: inline-block;
}

.contact-container {
  background: transparent;
  color: #ffffff;
  padding: 25px;
  .email, .name, .message {
    color: #000000;
  }

  .row {
    margin-top: 0;
  }

  .row-header {
    margin-top: 10px;
  }
}

.upper {
  margin: 0 auto;
  z-index: 200;
  height: 50%;
  color: #ffffff;
  text-align: center;

  .img-card {
    border-radius: 4px;
    position: absolute;
    font-size: 30px;
    top: 0;
    right:0; 
    left: 0;
    height: 100%;
    background: rgba(255, 255, 255, .6);
    form { margin-bottom: 0; }

    input, textarea {
      font-size: 14px;
    }
  }

  .mission-text {
    height: 40%;
    font-size: 16px;
  }
}

.card {
  width: 100%;
  height: 400px;
  position: relative;
  box-shadow: 0 10px 20px 0 rgba(0,0,0,.08);
}

.hero-1:before, .hero-2:before {
  content: " ";
  z-index: 10;
  display: block;
  position: absolute;
  height: 90vh;
  top: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.6);
}

.p1 {
  display: none;
  background-image: url('~assets/rachna1.jpg');
  width: 100%;
  height: 600px;
}

.p2, .p3 {
  width: 49%;
  height: 300px;
  margin-left: 1%;
}

.p2 {
  background-image: url('~assets/rachna1.jpg');
}

.p3 {
  background-image: url('~assets/rachna2.jpg');
}

.pic {
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  border-radius: 4px;
}

.info {
  display: inline-block;
  background-color: #DDDEDF;
  color: #000000;
  line-height: 1.8;
  border-radius: 4px;
  min-height: 266.5px;
  padding: 15px;
  overflow: auto;
  box-shadow: 0 10px 20px 0 rgba(0,0,0,.08);
  .title {
    display: inline-block;
    text-align: left;
    width: 100%;
    font-size: 40px;
  }
}

.line {
  width: 100%;
  border-bottom: 1px solid #DDDEDF;
}

.row {
  width: 100%;
  margin-top: 5px;
  padding-bottom: 5px;
  display: flex;
  justify-content: stretch;
  align-items: stretch;
  flex-direction: column;
  &.column { flex-direction: column; }
  &:last-child { border-bottom: 0; }
}

.bg-row {
  width: 100%;
  height: 100%;
  padding-bottom: 40px;
  padding-top: 20px;
  &.pre-colors { padding-bottom: 0; }
}

.header-container {
  width: 100%;
  text-align: center;

  .info-container {
    text-align: center;
    display: inline-block;
  }

  .row-header {
    text-align: center;
    padding-right: 10px;
    padding-left: 10px;
    font-size: 28px;
    margin-bottom: 1%;
    font-weight: 800;
    display: block;
    &.contact {
      color: #ffffff;
    }
  }
}

.container.colors {
  width: 100%;
  margin-top: 10px;
  margin-bottom: 10px;
}

.row.colors {
  padding: 0;
  margin: 0;
}

.big-button {
  font-size: 20px;
  padding: 20px 40px;
  height: auto;
}

.colors {
  position: relative;
}

.dance-styles {
  position: absolute;
  display: inline-block;
  font-family: 'Philosopher';
  color: #000000;
  padding: 10px;
  border-radius: 4px;
  z-index: 400;
  font-size: 26px;
  background: #ffffff;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 10px 20px 0 rgba(0,0,0,.08);
}

.dance-style {
  font-family: 'Philosopher';
  height: 200px;
  width: 100%;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #ffffff;
  font-size: 40px;
  font-weight: 600;
  cursor: pointer;
  box-shadow: 0 10px 20px 0 rgba(0,0,0,.08);
  transition: background-color .3s ease, color .3s ease;

  &.folk { 
    background-color: #392267; 
    &:hover { background-color: lighten(#392267, 20%); color: #000000; }
  }
  &.bhangra { 
    background-color: #8B2635;
    &:hover { background-color: lighten(#8B2635, 20%); color: #000000;
    }
  }
  &.bollywood { 
    background-color: #26532B; 
    &:hover { background-color: lighten(#26532B, 20%); color: #000000; }
  }
  &.fusion { 
    background-color: #007EA7; 
    &:hover { background-color: lighten(#007EA7, 20%); color: #000000; }
  }
}

@media ($bp-larger-than-phablet) {
  .row {
    flex-direction: row;
  }

  .services {
    flex-direction: row;
  }

  .info {
    width: 96%;
    padding: 15px;
    height: 266.5px;
    &:first-child { margin-top: 0; }
  }

  .no-margin {
    margin-left: 5px;
  }

  .p1 {
    display: block;
  }
  .bg-row{
    &.pre-colors { padding-bottom: 40px; }
  }

  .upper {
    position: absolute;
    width: 100%;
    top: 10%;
    height: 70%;
    .img-card {
      border-radius: 4px;
      position: absolute;
      top: 0;
      left: 40%;
      font-size: 30px;
      width: 50%;
      background: rgba(255, 255, 255, .6);
    }
  }
  .contact-container {
    .columns:last-child {
      margin-left: 20px;
    }
  }

  .testimonial {
    height: 400px;
    overflow-y: auto;
  }

  .logo {
    width: 65%;
  }

  .upper {
    .mission-text {
      font-size: 26px;
    }
  }

}

</style>
