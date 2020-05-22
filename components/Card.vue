<template>
  <nuxt-link :to="`/jobs/${job.id}`" class="card">
    <div class="card__body">
      <div class="card__logo">
        <img v-bind:src="getImgUrl(job.logo)" :alt="`${job.company} logo`" />
      </div>
      <div class="card__content">
        <div class="company">
          <p>
            {{job.company}}
            <span v-show="job.new" class="new">new</span>
            <span v-show="job.featured" class="feature">featured</span>
          </p>
        </div>
        <div class="position">{{job.position}}</div>
        <div class="details">
          <ul>
            <li>{{job.postedAt}}</li>
            <li>{{job.contract}}</li>
            <li>{{job.location}}</li>
          </ul>
        </div>
      </div>
    </div>
    <div class="card__categories">
      <ul>
        <li class="tags" v-for="language in job.languages" v-bind:key="language">
          <span>{{language}}</span>
        </li>
        <li class="tags" v-for="tool in job.tools" v-bind:key="tool">
          <span>{{tool}}</span>
        </li>
      </ul>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  props: ["job"],
  data() {
    return {};
  },
  methods: {
    getImgUrl(logo) {
      let images = require.context("../assets/images/", false, /\.svg$/);
      return images("./" + logo);
    }
  }
};
</script>

<style lang="scss">
/* // cards */
.card {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem;
  width: 100%;
  background: var(--white-clr);
  border-radius: 5px;
  box-shadow: 1px 1px 14px 5px hsla(180, 29%, 50%, 0.21);
  max-width: 75ch;
  margin: 0 auto 1.5rem;
  transition: all 0.15s ease;
  cursor: pointer;
  position: relative;
  &:hover {
    box-shadow: 1px 1px 15px 10px hsla(180, 29%, 50%, 0.25);
  }
}

.featured {
  border-left: 4px solid var(--primary-clr);
}
span {
  color: var(--white-clr);
  border-radius: 1em;
  padding: 0.5em 0.5em 0.25em;
  font-size: 0.65rem;
  line-height: 1.2;
  letter-spacing: 1px;
  text-transform: uppercase;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 0;
  margin: 0 5px;
  &.feature {
    background: var(--black-clr);
  }
  &.new {
    background: var(--primary-clr);
  }
}

.card__body {
  display: flex;
  margin-bottom: 1rem;
}
.card__content {
  padding-left: 1rem;
}
.company {
  text-align: left;
  text-transform: capitalize;
  font-weight: bold;
  color: var(--primary-clr);
  margin-bottom: 0.5rem;
}
.position {
  font-weight: bold;
  text-align: left;
  margin-bottom: 0.5rem;
  transition: all 0.15s ease;
}
.card:hover .position {
  color: var(--primary-clr);
}
.details {
  ul {
    display: flex;
    justify-content: space-between;
    li {
      color: var(--lightGrey-clr);
    }
    li + li {
      margin-left: 2rem;
      position: relative;
    }
  }
}

.details ul li + li:before {
  content: "";
  width: 4px;
  height: 4px;
  border-radius: 10px;
  position: absolute;
  left: -25%;
  top: 50%;
  background: var(--lightGrey-clr);
  transform: translateY(-50%);
}
.card__categories {
  flex-basis: calc(50% - 4px);
  ul {
    display: flex;
    justify-content: flex-end;
  }
}
.tags {
  background: var(--accent-clr);
  display: inline-flex;
  margin: 0 5px 5px;
  border-radius: 4px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.15s ease;
  b {
    font-size: 1.25rem;
    background: var(--primary-clr);
    border-top-right-radius: 4px;
    border-bottom-right-radius: 4px;
    color: var(--white-clr);
    width: 1.75rem;
    height: 100%;
    display: inline-block;
    transition: all 0.15s ease;
  }
  &:hover {
    background: var(--primary-clr);
    b {
      background: var(--secondary-clr);
    }
  }
  span {
    padding: 0.5rem;
    color: var(--primary-clr);
  }
  &:hover span {
    color: var(--accent-clr);
  }
}
@media screen and (max-width: 600px) {
  .card {
    padding-top: 2.25rem;
    margin-bottom: 2.5rem;
  }
  .card__logo {
    position: absolute;
    top: -8%;
    width: 3.25rem;
  }
  span {
    padding: 0.5em 0.75em 0.25em;
  }
  .details ul li + li {
    margin-left: 1.25rem;
  }
  .details ul li + li:before {
    left: -15%;
  }
  .company {
    margin-top: 1rem;
  }
  .card__content {
    padding-left: 0;
    padding-bottom: 1rem;
    border-bottom: 1px solid var(--lightGrey-clr);
    margin-bottom: 1rem;
  }
  .card__categories {
    flex-basis: 100%;
    ul {
      flex-wrap: wrap;
      justify-content: start;
      li {
        margin: 0 10px 10px 0;
      }
    }
  }
}
</style>