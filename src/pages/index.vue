<template>
  <div class="site-content">
    <app-header-home :buttonLabel="page.headerButton.label"
                     :buttonUrl="page.headerButton.url"
                     :concepts="page.concepts"
                     :description="page.introduction"
                     :image="page.headerImage"
                     :title="page.title" />

    <main class="site-content__main center-column">
      <concept-block v-for="concept in page.concepts"
                     :concept="{
                       ...concept,
                       description: papers[concept.paperID]
                     }"
                     :key="concept.name" />
    </main>

    <app-footer :body="page.footer" />
  </div>
</template>

<script>
import AppFooter from '../components/app-footer'
import AppHeaderHome from '../components/app-header-home'
import getPageData from '../lib/get-page-data'
import seoHead from '../lib/seo-head'
import ConceptBlock from '../components/concept-block'

export default {
  components: { AppFooter, AppHeaderHome, ConceptBlock },
  async asyncData() {
    const page = await getPageData('index')

    const pageResponses = await Promise.all(
      page.concepts.map(concept => getPageData(`papers/${concept.paperID}`, 'md'))
    )

    const papers = page.concepts.reduce((acc, concept, index) => {
      acc[concept.paperID] = pageResponses[index]
      return acc
    }, {})

    return { page, papers }
  },
  head() {
    return seoHead(
      this.page.title,
      this.page.slug,
      this.page.introduction,
      this.page.seoImage
    )
  },
  fetch({ route,store }) {
    store.commit('setIndexPageUrl', { indexPageUrl: route.fullPath })
  },
}
</script>
