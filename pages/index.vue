<template>
  <div>
    <div class="container">
      <div>
        <div class="hero">
          <h1 class="title">Jobs listings</h1>
        </div>

        <div class="box">
          <ul>
            <li>
              <p class="tags" @click="filterByLang" v-for="item in langs" :key="item">
                <span>{{item}}</span>
                <b @click.stop="clearFilter">&Cross;</b>
              </p>
            </li>
          </ul>
          <p v-if="isShown">available {{jobs.length}} {{jobs.length === 1 ? 'job': 'jobs'}}</p>
          <button @click="clearFilter" v-show="isShown">Clear</button>
        </div>

        <Card
          v-for="job in jobs"
          :job="job"
          :key="job.company"
          :class="job.featured ? 'featured' : ''"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Card from "~/components/Card.vue";
import data from "static/data.json";

// filter by lang
const langs = data.map(it => it.languages);
let arr = [];
langs.forEach(element => {
  return element.map(i => arr.push(i));
});
const filteredlangList = arr.filter(function(item, pos) {
  return arr.indexOf(item) == pos;
});

export default {
  head: {
    title: `Job listings app, created with Vue and Nuxt.js`,
    meta: [
      {
        hid: "description",
        name: "description",
        content: "A job listings page"
      }
    ]
  },
  components: {
    Card
  },
  data() {
    return {
      jobs: data,
      langs: filteredlangList,
      isShown: false
    };
  },
  methods: {
    filterByLang(e) {
      const val = e.target.textContent;
      const filtered = data.filter(item => {
        return item.languages.includes(val);
      });
      this.jobs = filtered;
      this.isShown = true;
    },
    clearFilter() {
      this.isShown = false;
      this.jobs = data;
    }
  }
};
</script>

<style lang="scss">
.hero {
  display: inline-flex;
  flex-direction: column;
  padding: 1rem 2.25rem;
  background: var(--white-clr);
  border-radius: 5px;
  box-shadow: 1px 1px 14px 5px hsla(180, 29%, 50%, 0.21);
  margin-bottom: 1rem;
  margin-top: -50%;
  z-index: 2;
}
.box {
  background: var(--white-clr);
  border-radius: 5px;
  box-shadow: 1px 0px 14px 5px hsla(180, 29%, 50%, 0.21);
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  margin: 0 auto 1rem;
  padding: 1rem 2.25rem;
  max-width: 75ch;
  p {
    margin-left: 1rem;
  }
  button {
    color: var(--primary-clr);
    margin-left: auto;
    transition: all 0.15s ease;
    &:hover {
      text-decoration: underline;
    }
  }
}

@media screen and (max-width: 600px) {
  .box {
    padding: 1rem;
  }
  .box ul {
    margin-bottom: 1rem;
  }
  .box p {
    margin-left: 0;
  }
}
</style>
