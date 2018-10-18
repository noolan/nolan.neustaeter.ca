<template>
  <main id="app">
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
            In 2016 I was tasked with building an online marketing platform with a website / page builder at it&rsquo;s core.
          </p>
          <p>
            Over the years I had built multiple <abbr title="Content Management System">CMS</abbr>&rsquo; for my own use and I had been tossing around some ideas in my head on how to structure the server and database since then.
          </p>
          <p>
            For the server, I split the functionality into three domains (both figuratively and literally), each was a separate application that shared common business logic code and libraries where possible.<br>
            The three applications could run on the same machine with the http server distributing requests based on subdomain or the applications could split off into their own machines/VMs/instances/containers if needed.
          </p>

          <table>
            <thead>
              <tr>
                <th>Application</th>
                <th>Visibility</th>
                <th>Subdomain</th>
                <th>Responsibilities</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Sites</td>
                <td>Public</td>
                <td class="text-right"><code>www.</code></td>
                <td>In charge of displaying published websites, processing form submissions, and collecting analytics.</td>
              </tr>
              <tr>
                <td>Control</td>
                <td>Private</td>
                <td class="text-right"><code>control.</code></td>
                <td>Authenticates users and serves them the <abbr title="Single Page Application">SPA</abbr></td>
              </tr>
              <tr>
                <td>API</td>
                <td>Private</td>
                <td class="text-right"><code>api.</code></td>
                <td>Provides endpoints for the <abbr title="Single Page Application">SPA</abbr> to allow it to manage businesses, users, websites, pages, etc...</td>
              </tr>
            </tbody>
          </table>

          <p>
            Each application had it&rsquo;s own routes, controllers, and views but shared models, service providers, middleware, and config (through .env files).
          </p>

          <div class="columns items-centered">
            <div>
              <h5 class="pv-1">Here&rsquo;s a listing of the stack we settled on:</h5>
              <dl>
                <dt>Hosting</dt>
                <dd>Amazon Web Services EC2 - fast and cost efficient</dd>

                <dt>Web Server</dt>
                <dd>Nginx - fast and very flexible</dd>

                <dt>Backend language</dt>
                <dd>PHP7 - huge speed improvement over PHP5.x and the other devs are already familiar with PHP from our existing products</dd>

                <dt>Backend framework</dt>
                <dd>Laravel and Lumen - I&rsquo;ve been using Laravel since version 2 and I love it&rsquo;s focus on code readability and providing sane defaults that are easy to customize</dd>

                <dt>Frontend framework</dt>
                <dd>Vue.js - This was a tossup between Vue and React. The main deciding factor was that I would soon be bringing some junior devs on to the project and Vue is much easier to learn</dd>
              </dl>
            </div>

            <div>
              <gfycat gfy-id="GratefulNarrowBluetickcoonhound" caption="Teaser video of the page builder function of my previous project"></gfycat>
            </div>
          </div>

          <div class="flex">
            <p>
              To the right is a diagram of part of the data structure I designed. Pages don't store their content directly, the revisions do.<br>
              A new revision is created every time the page&rsquo;s content is updated.
              <ul>
                <li>If the revision is from an autosave while editing, it will contain a delta representing that change and it will be marked as a <code>draft</code> revision.</li>
                <li>If the user is happy with their changes, they trigger a publish which creates a revision marked as <code>published</code> with the complete content.</li>
              </ul>
              When a page is requested through the Site application, the content from the latest published revision is used to build it.
            </p>

            <aside class="tree pl-2">
              <div class="branch" title="Businesses">
                <div class="branches">
                  <div class="branch" title="Users"></div>
                  <div class="branch" title="Websites">
                    <div class="branches">
                      <div class="branch" title="Pages">
                        <div class="branches">
                          <div class="branch" title="Revisions"></div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </aside>
          </div>

          <p>
            This structure has a few advantages; content changes can happen without affecting the live version of the page, changes can be reviewed and reverted, A/B testing can be easily implemented by having one revision marked as A and another as B.
          </p>

        </div>

      </div>
    </section>

    <timeline :events="events"></timeline>

    <section id="contact">
      <div class="container">
        <div class="sub-section">
          <p class="lead screen-only">
            If you want to chat about anything...
          </p>
          <p class="lead print-only">
            References available upon request.
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
            The source code for this <span class="screen-only">page</span><span class="print-only">document</span> and a few other experiments can be found at:
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
@import "./styles/utilities.scss";
// main styles
@import "./styles/app.scss";

</style>
