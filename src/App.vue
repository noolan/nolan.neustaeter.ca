<template>
  <main id="app" class="flex f-d-c f-i-c">
    <section id="heading">
      <div class="container">
        <h1>Nolan Neustaeter <small>Full-Stack Web Developer</small></h1>

        <section id="nouns" class="flex f-w-w f-j-c f-i-fs">
          <span>Code Typer</span>
          <span>CSS Wrangler</span>
          <span>Data Organizer</span>
          <span>Responsiviser</span>
          <span>API Enthusiast</span>
        </section>
      </div>

    </section>

    <section id="introduction">
      <div class="container">
        <p class="lead">
          Hello, my name is Nolan and I make things. Mostly I make things for web browsers but I also make:
        </p>

        <p>
          <ul>
            <li>overcomplicated woodworking projects</li>
            <li>a fantastic butternut squash soup</li>
            <li>lame &ldquo;dad&rdquo; jokes</li>
          </ul>
        </p>

        <p>
          I first started making websites for family and friends {{ new Date().getFullYear() - 1999 }} years ago. Since then, I&rsquo;ve worked with other platforms and languages but I&rsquo;m always drawn back, eventually.
          <br>
          Some people complain about how fast the industry changes but that&rsquo;s always been one of my favorite aspects of web development. There&rsquo;s always a new or interesting language, library, or platform to learn so boredom is hard to come by.
        </p>
        <p>
          Lately, I&rsquo;ve been focussing more on front-end development so I&rsquo;ve been able to learn some amazing libraries like React and Vue.js as well as some of the newer tooling projects like Webpack.
        </p>
        <p>
          I currently use a Macbook Pro for development with as many monitors attached as I can manage.<br>
          I use Sublime Text 3 for my editor with Firewatch as my syntax theme and Fira Code for my font.
        </p>

      </div>
    </section>

    <knowledge :expertise="knowledge"></knowledge>

    <section id="projects">
      <div class="container">
        <h2 class="heading">Recent Projects</h2>

        <div id="listing" class="project sub-section">
          <p class="lead">
            In 2015 I rebuilt my employer&rsquo;s product listing component using React.
          </p>
          <div class="columns items-centered">
            <div>
              <p>
                It features a prominent search bar, optional filters, and automatic pagination when the user scrolls near the bottom of the page.
              </p>
              <p>
                The product data is stored locally as an array of JavaScript objects so the searching, sorting, and filtering is nearly instant. The design features a generous amount of whitespace and is fully responsive on smaller devices.
              </p>
              <p>
                <a href="http://www.vernontoyota.com/new-toyota-sales-vernon" target="_blank" rel="noopener">Here is a link</a> to one of the sites that is using the product listing component.
              </p>
            </div>
            <div>
              <figure>
                <picture class="responsive">
                  <source srcset="./assets/products-page.webp" type="image/webp">
                  <source srcset="./assets/products-page.png" type="image/png"> 
                  <img src="./assets/products-page.png" class="responsive" alt="Responsive product listing page built with React">
                </picture>
                <figcaption>Screenshot of the product listing page built with React</figcaption>
              </figure>
            </div>
          </div>
        </div>

        <div id="secret" class="project sub-section">
          <p class="lead">
            This last year I was tasked with building a completely new product for the company which has been awesome.
          </p>
          <p>
            I can&rsquo;t go into much detail since the product hasn&rsquo;t been officially released but the technology stack I chose was:
          </p>

          <div class="columns items-centered">
            <div>
              <dl style="font-size: .85em; padding-bottom: 1.5rem;">
                <dt>Hosting</dt>
                <dd>Amazon Web Services EC2 - fast and cost efficient</dd>

                <dt>Web Server</dt>
                <dd>Nginx - fast and very configurable</dd>

                <dt>Backend language</dt>
                <dd>PHP7 - huge speed improvement over PHP5.x and the other devs are already familiar with PHP from our existing products</dd>

                <dt>Backend framework</dt>
                <dd>Laravel 5 - I&rsquo;ve been using Laravel since version 2 and I love it&rsquo;s attention to code readabillity and having an easy to use API</dd>

                <dt>Frontend framework</dt>
                <dd>Vue.js - This was a tossup between Vue and React. The main deciding factor was that I would soon be bringing some junior devs on to the project and React has a steep learning curve at the beginning</dd>
              </dl>
            </div>

            <div>
              <gfycat gfy-id="GratefulNarrowBluetickcoonhound" caption="Teaser video of just one part of my previous project"></gfycat>
            </div>
          </div>

          <p>
            This type of project is something that I have worked on a few times in the past so I already had some ideas that I wanted to try out in regards to how to configure the web server and the data structure.<br>
            It&rsquo;s on the home stretch now so as I&rsquo;m able, I&rsquo;ll add more details about this new product <strong>here</strong>.
          </p>
        </div>

      </div>
    </section>

    <timeline :events="events"></timeline>

    <section id="contact">
      <div class="container">
        <div class="sub-section">
          <p class="lead">
            If you want to chat about anything...
          </p>
          <div class="contact-method">
            send me an email at <a :href="emailHref" target="_blank">{{ email }}</a>
          </div>
          <div class="contact-method">
            call me at <a :href="phoneHref" target="_blank">{{ phone }}</a>
          </div>
        </div>
        <div class="sub-section">
          <p class="lead">
            The source code for this page and a few other experiments can be found at:
          </p>
          <div class="contact-method">
            <a href="https://github.com/noolan" target="_blank" rel="noopener">https://github.com/noolan</a>
          </div>
        </div>
      </div>
    </section>

  </main>
</template>

<script>
import Knowledge from './components/Knowledge.vue'
import Gfycat from './components/Gfycat.vue'
import Timeline from './components/Timeline.vue'

import knowledge from './data/knowledge'
import timelineEvents from './data/events'

export default {
  name: 'app',
  components: {
    Knowledge,
    Gfycat,
    Timeline
  },
  data () {
    return {
      email: 'nolan@neustaeter.ca',
      events: timelineEvents,
      knowledge: knowledge,
      phone: '(250) 804-8589'
    }
  },
  computed: {
    emailHref () {
      return `mailto:${this.email}`
    },
    phoneHref () {
      return `tel:+1${this.phone.replace(/[()\-\s]/g, '')}`
    }
  }
}
</script>

<style lang="scss">
// variables
@import "./styles/variables.scss";

// super basic reset
@import "./styles/reset.scss";

// utilities
@import "./styles/flexbox-toolbox.css";

// main styles
@import "./styles/app.scss";

</style>
