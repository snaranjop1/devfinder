<template>
  <div class="dev-card">
    <div class="personal-info">
      <img :src="avatar" :alt="name" class="avatar" />
      <div class="name-joined">
        <div>
          <h1 class="name">{{ name }}</h1>
          <a :href="githubLink" class="login" target="_blank">@{{ login }}</a>
        </div>
        <p class="created-at">Joined {{ formatedCreatedAt }}</p>
      </div>
    </div>
    <p class="bio">{{ bio ? bio : "This profile has no bio" }}</p>
    <div class="stats">
      <div>
        <p class="label">Repos</p>
        <h3 class="value">{{ repos }}</h3>
      </div>
      <div>
        <p class="label">Followers</p>
        <h3 class="value">{{ followers }}</h3>
      </div>
      <div>
        <p class="label">Following</p>
        <h3 class="value">{{ following }}</h3>
      </div>
    </div>
    <div class="social">
      <div :class="{ disabled: !location }">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="icon"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z"
            clip-rule="evenodd"
          />
        </svg>
        <p>{{ checkSocial(location) }}</p>
      </div>
      <div :class="{ disabled: !blogUrl }">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="icon"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M12.586 4.586a2 2 0 112.828 2.828l-3 3a2 2 0 01-2.828 0 1 1 0 00-1.414 1.414 4 4 0 005.656 0l3-3a4 4 0 00-5.656-5.656l-1.5 1.5a1 1 0 101.414 1.414l1.5-1.5zm-5 5a2 2 0 012.828 0 1 1 0 101.414-1.414 4 4 0 00-5.656 0l-3 3a4 4 0 105.656 5.656l1.5-1.5a1 1 0 10-1.414-1.414l-1.5 1.5a2 2 0 11-2.828-2.828l3-3z"
            clip-rule="evenodd"
          />
        </svg>
        <p>{{ checkSocial(blogUrl) }}</p>
      </div>
      <div :class="{ disabled: !twitterUsername }">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="icon"
          viewBox="0 0 24 24"
          fill="currentColor"
        >
          <path
            d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"
          />
        </svg>
        <p>{{ checkSocial(twitterUsername) }}</p>
      </div>
      <div :class="{ disabled: !company }">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="icon"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M4 4a2 2 0 012-2h8a2 2 0 012 2v12a1 1 0 110 2h-3a1 1 0 01-1-1v-2a1 1 0 00-1-1H9a1 1 0 00-1 1v2a1 1 0 01-1 1H4a1 1 0 110-2V4zm3 1h2v2H7V5zm2 4H7v2h2V9zm2-4h2v2h-2V5zm2 4h-2v2h2V9z"
            clip-rule="evenodd"
          />
        </svg>
        <p>{{ checkSocial(company) }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "Dev",
  props: ["dev"],

  watch: {
    dev: function(newVal) {
      this.avatar = newVal.avatar_url;
      this.name = newVal.name;
      this.login = newVal.login;
      this.bio = newVal.bio;
      this.createdAt = newVal.created_at;
      this.repos = newVal.public_repos;
      this.followers = newVal.followers;
      this.following = newVal.following;
      this.location = newVal.location;
      this.blogUrl = newVal.blog;
      this.twitterUsername = newVal.twitter_username;
      this.company = newVal.company;
    },
  },

  data() {
    return {
      avatar: this.dev.avatar_url,
      name: this.dev.name,
      login: this.dev.login,
      bio: this.dev.bio,
      createdAt: this.dev.created_at,
      repos: this.dev.public_repos,
      followers: this.dev.followers,
      following: this.dev.following,
      location: this.dev.location,
      blogUrl: this.dev.blog,
      twitterUsername: this.dev.twitter_username,
      company: this.dev.company,
    };
  },

  methods: {
    checkSocial(value) {
      return value ? value : "Not Available";
    },
  },

  computed: {
    githubLink() {
      return `https://github.com/${this.login}`;
    },

    formatedCreatedAt() {
      return moment(this.createdAt).format("DD MMM YYYY");
    },
  },
};
</script>

<style scoped>
.dev-card {
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
  background: var(--card-background);
  color: var(--text-color);
}

.personal-info {
  display: flex;
}

.name-joined {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.avatar {
  height: 100px;
  border-radius: 50%;
  margin-right: 40px;
}

.name {
  margin-bottom: 10px;
  font-size: 1.8rem;
  overflow: hidden;
  white-space: nowrap;
  max-width: 300px;
  text-overflow: ellipsis;
  color: var(--text-alt-color);
}

.login {
  text-decoration: none;
  color: var(--highlight-color);
}

.login:hover {
  color: var(--highlight-hover-color);
}

.created-at {
  font-size: 0.9rem;
  opacity: 0.8;
  margin-top: 5px;
}

.bio {
  margin-left: 140px;
  margin-top: -20px;
  margin-bottom: 40px;
  opacity: 0.8;
}

.stats {
  margin-left: 140px;
  display: flex;
  background: var(--background-color);
  justify-content: space-between;
  padding-top: 15px;
  padding-bottom: 15px;
  padding-left: 30px;
  padding-right: 120px;
  border-radius: 15px;
  margin-bottom: 30px;
}

.stats .label {
  margin: 0;
  margin-bottom: 5px;
  font-size: 0.8rem;
}

.stats .value {
  margin: 0;
  font-size: 1.8rem;
  color: var(--text-alt-color);
}

.social {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 20px 0px;
  margin-left: 140px;
}

.social div {
  display: flex;
  align-items: center;
}

.social div.disabled {
  opacity: 0.5;
}

.social .icon {
  height: 25px;
  padding-right: 10px;
}

@media (max-width: 768px) {
  .name-joined {
    width: 100%;
    display: flex;
    flex-direction: column;
  }

  .bio {
    margin-left: 0px;
    margin-top: 35px;
    margin-bottom: 30px;
  }

  .stats {
    margin-left: 0px;
  }

  .social {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 20px 0px;
    margin-left: 0px;
  }
}

@media (max-width: 480px) {
  .dev-card {
    padding: 30px;
  }

  .name-joined {
    width: 100%;
    display: flex;
    flex-direction: column;
  }

  .avatar {
    height: 80px;
    margin-right: 20px;
  }

  .name {
    margin-bottom: 3px;
    font-size: 1.5rem;
    max-width: 200px;
  }

  .created-at {
    font-size: 0.9rem;
    opacity: 0.8;
    margin-top: 5px;
  }

  .bio {
    margin-left: 0px;
    margin-top: 35px;
    margin-bottom: 30px;
    opacity: 0.8;
  }

  .stats {
    margin-left: 0px;
    display: flex;
    background: var(--background-color);
    justify-content: space-between;
    padding: 15px 25px;
    text-align: center;
    margin-bottom: 30px;
  }

  .stats .label {
    margin: 0;
    margin-bottom: 5px;
    font-size: 0.7rem;
  }

  .stats .value {
    margin: 0;
    font-size: 1.4rem;
  }

  .social {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    grid-gap: 20px 0px;
    margin-left: 0px;
  }
}
</style>
