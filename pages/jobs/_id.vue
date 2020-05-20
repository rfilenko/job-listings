<template>
  <div class="wrap container">
    <h2>
      Job id
      <strong>#{{$route.params.id}}</strong>
    </h2>
    <nuxt-link to="/">go back</nuxt-link>
    <!-- <pre>{{JSON.stringify(current, null, 4)}}</pre> -->
    <div class="card">
      <div class="card__body">
        <div class="card__content">
          <div class="company">
            <p>
              {{current.company}}
              <span v-show="current.new" class="new">new</span>
              <span v-show="current.featured" class="feature">featured</span>
            </p>
          </div>
          <div class="position">{{current.position}}</div>
          <div class="details">
            <ul>
              <li>{{current.postedAt}}</li>
              <li>{{current.contract}}</li>
              <li>{{current.location}}</li>
            </ul>
          </div>
        </div>
      </div>
      <div class="card__categories">
        <ul>
          <li class="tags" v-for="language in current.languages" v-bind:key="language">
            <span>{{language}}</span>
          </li>
          <li class="tags" v-for="tool in current.tools" v-bind:key="tool">
            <span>{{tool}}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import data from "~/static/data.json";

export default {
  head: {
    title: `JOB details`,
    meta: [
      {
        hid: "description",
        name: "description",
        content: "A details page"
      }
    ]
  },
  data() {
    return {
      data,
      id: null,
      current: ""
    };
  },
  methods: {
    async getCurr() {
      this.id = await this.$route.params.id;
      const job = await data.filter(item => {
        return item.id === parseFloat(this.$route.params.id);
      });
      this.current = job[0];
    }
  },

  mounted() {
    this.getCurr();
  }
};
</script>

<style >
.wrap {
  display: flex;
  flex-direction: column;
  max-width: 75ch;
}
.wrap h2 {
  margin-top: 1rem;
  position: absolute;
  z-index: 1;
  top: 1.75rem;
  font-size: 3rem;
  color: var(--accent-clr);
}
.wrap a {
  background: var(--primary-clr);
  padding: 0.25rem 0.5rem;
  margin: 1rem 0;
  color: var(--accent-clr);
  border-radius: 5px;
  cursor: pointer;
  display: inline-flex;
  text-align: left;
  margin-right: auto;
  transition: all 0.15s ease;
  transform: translateY(0) scale(1);
}
.wrap a:hover {
  transform: translateY(-2px) scale(1.02);
  background: var(--secondary-clr);
}
</style>