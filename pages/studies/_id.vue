<template>
  <div class="case-study c-bg1">
    <CaseStudyCard
      class="case-study__card -first"
      :bg="currentFeaturedImage"
      :clientName="currentClientName"
      :projectLogo="currentProjectLogo"
      :title="currentTitle"
      :isMasthead="true" />
    <Hydrate ssr-only>
      <FeatureList
        title="— Key Results"
        :items="whatWeDid" />
    </Hydrate>
    <Hydrate ssr-only>
      <div class="case-study__screenshot section">
        <Picture :src="screenshot" />
      </div>
    </Hydrate>
    <Hydrate ssr-only>
      <CaseStudyDesc class="case-study__text"
        :url="url"
        :headline="headline"
        :headlineAuthor="headlineAuthor"
        :copy="copy" />
    </Hydrate>
    <nuxt-link :to="nextLink">
      <Hydrate when-visible>
        <CaseStudyCard
          class="case-study__card -last"
          :bg="nextFeaturedImage"
          :clientName="nextClientName"
          :projectLogo="nextProjectLogo"
          :title="nextTitle"
          buttonText="Read Next" />
      </Hydrate>
    </nuxt-link>
  </div>
</template>

<script>
import Hydrate from 'lazy-hydration'
import Picture from '@/components/ui/Picture'
import CaseStudyCard from '@/components/CaseStudyCard'
import FeatureList from '@/components/FeatureList'
import CaseStudyDesc from '@/components/CaseStudyDesc'
import Footer from '@/components/Footer'

const studies = {
  'rolling-stone': {
    name: 'Rolling Stone',
    currentFeaturedImage: 'case-study-rs.jpg',
    currentProjectLogo: '/logos/rolling-stone.svg',
    currentClientName: 'XWP',
    currentTitle: 'Louder Front For Rolling Stone',
    whatWeDid: [
      {
        headline: 'Frontend',
        copy: 'Pixel perfect design implementation. Custimizable options for category views. Modern browser features with graceful degradation, etc.',
      }, {
        headline: 'Performance',
        copy: 'Optimized critical rendering path. Layout shift protection. Minimal amount of javascript and no 3rd party dependencies, etc.',
      }, {
        headline: 'UI Kit',
        copy: 'Easily customizable and optimized building blocks. Style guide for visual and code reference. Organized common design patterns, etc.',
      },
    ],
    screenshot: '/images/screen-rs.jpg',
    url: 'https://rollingstone.com',
    headline: '"This was one of our smoothest and most successful launches to date."',
    headlineAuthor: 'Nicola Catton - Senior Director of Projects at Rolling Stone, PMC',
    copy: [
      'Another example of a huge rebranding our team worked on. This is the effect of our collaboration with XWP, an industry leader in the WordPress world.',
      'We took an ownership for the whole front end coding of the most popular music magazine. Our focus was allocated to the development of a silky smooth page speed and user experience. Our developers worked under a restricted performance budget and code standards that comply with the WordPress VIP platform where the project is hosted. It is worth mentioning that only 11 software providers are licensed to work under the VIP infrastructure.',
    ],
    nextFeaturedImage: 'case-study-jupiter.jpg',
    nextProjectLogo: '/logos/jupiter.svg',
    nextClientName: 'Artbees',
    nextTitle: 'Top Selling WordPress Theme',
    nextLink: '/studies/jupiter',
  },
  'jupiter': {
    name: 'Jupiter',
    currentFeaturedImage: 'case-study-jupiter.jpg',
    currentProjectLogo: '/logos/jupiter.svg',
    currentClientName: 'Artbees',
    currentTitle: 'Top Selling WordPress Theme',
    whatWeDid: [
      {
        headline: 'Awards',
        copy: 'ThemeForest Hall of Fame, Power Elite Author, Weekly Top Seller, Featured Theme, etc.',
      }, {
        headline: 'Performance',
        copy: 'Critical rendering path optimization. Lazy loading components. Icon fonts replacecement with SVGs, etc.',
      }, {
        headline: 'Architecture',
        copy: 'Monolithic product refactored into small grained components. Feature based file organization. Adjusted build tools, etc.',
      },
    ],
    screenshot: '/images/screen-jupiter.jpg',
    url: 'https://jupiter.artbees.net',
    headline: '"The outcome was extremely rewarding: many of our clients reported a more than 50% improvement in speed and performance."',
    headlineAuthor: 'Babak Azimzadeh - Chief Technology Officer at Artbees',
    copy: [
      'Jupiter is one of the best selling WordPress themes. It\'s top rated and selling on ThemeForest where it earned market recognition and users love.',
      'Loud Now Agency joined Artbees to help them get their product back on high performance track. After deep analysis of UX issues we discovered key areas to focus our development on. These included product architecture, optimizing critical rendering path and dead code elimination. All these points were overlaping but served different purposes. We split monolitic architecture into smaller pieces to enable us to lazy load components. This led into siginifficat improvements in optimization of initial pageload which was additionally supported by deferring offscreen images. We also reduced assets\' bundlesize by eliminating pieces not requested by the browser: switching from icon fonts to single svgs, client side use of Requirejs for dependency management, etc.',
    ],
    nextFeaturedImage: 'case-study-rs.jpg',
    nextProjectLogo: '/logos/rolling-stone.svg',
    nextClientName: 'XWP',
    nextTitle: 'Louder Front For Rolling Stone',
    nextLink: '/studies/rolling-stone',
  },
}

export default {
  name: 'CaseStudy',
  transition: {
    name: 'trans-page-from-bottom',
    mode: 'in-out',
  },
  head () {
    return {
      title: `${this.name} - ${this.currentTitle} | Loud Now Agency`,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        { hid: 'description', name: 'description', content: this.headline },
        // { hid: 'robots', name: 'robots', content: 'noindex, follow' },
      ],
    }
  },
  beforeRouteUpdate (to, from, next) {
    this.$el.style.transform = `translateY(-${window.scrollY}px)`
    next()
  },
  components: {
    Picture,
    CaseStudyCard,
    FeatureList,
    CaseStudyDesc,
    Footer,
    Hydrate,
  },
  data () {
    // Move to API call when we have more studies
    return studies[this.$route.params.id]
  },
}
</script>

<style lang="scss" scoped>
.case-study { padding-bottom: 50px; }
.case-study__card.-first { margin-top: 150px; }

.case-study__screenshot img {
  margin : 0 auto;
}
</style>
