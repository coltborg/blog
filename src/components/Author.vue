<template>
  <div class="author">
    <g-image
      alt="Author image"
      class="author__image"
      src="~/assets/images/author.png"
      width="180"
      height="180"
      blur="5"
    />

    <h1
      v-if="showTitle"
      class="author__site-title"
    >
      {{ $static.metadata.siteName }}
    </h1>

    <p class="author__intro">
      {{ $static.metadata.siteDescription }}
    </p>

    <p class="author__now">
      What am I up to
      <g-link to="/now/">
        now
      </g-link>
    </p>

    <p class="author__links">
      <SocialIcon
        v-for="(link, index) in socialLinks"
        :key="index"
        :icon="link.icon"
        :label="link.label"
        :url="link.url"
      />
    </p>
  </div>
</template>

<static-query>
  query {
    metadata {
      siteDescription
      siteName
    }
  }
</static-query>

<script>
import IconDev from '@/components/IconDev';
import IconGithub from '@/components/IconGithub';
import IconLinkedin from '@/components/IconLinkedin';
import IconRss from '@/components/IconRss';
import IconTwitter from '@/components/IconTwitter';
import SocialIcon from '@/components/SocialIcon';

export default {
  name: 'Author',
  components: {
    SocialIcon,
  },
	props: {
		showTitle: {
			type: Boolean,
			default: false,
		},
  },
  data() {
    return {
      socialLinks: [
        {
          icon: IconTwitter,
          label: 'Twitter',
          url: 'https://twitter.com/coltborg',
        },
        {
          icon: IconGithub,
          label: 'Github',
          url: 'https://github.com/coltborg',
        },
        {
          icon: IconDev,
          label: 'Dev',
          url: 'https://dev.to/coltborg',
        },
        {
          icon: IconLinkedin,
          label: 'Linkedin',
          url: 'https://www.linkedin.com/in/coltborg/',
        },
        {
          icon: IconRss,
          label: 'RSS',
          url: 'https://www.coltborg.com/rss.xml',
        },
      ],
    }
  },
}
</script>

<style lang="scss">
.author {
	margin: 0 auto;
	max-width: 500px;
	padding: calc(var(--space) / 2) 0;
	text-align: center;
  align-items: center;
  display: flex;
  flex-direction: column;

	&__image {
    --size: 100px;

		height: var(--size);
		width: var(--size);
    border-radius: 100%;
    margin-bottom: 1em;
	}

	&__intro {
    opacity: 0.8;
    margin-bottom: 0.625em;
  }

  &__now {
    opacity: 0.8;
    margin-bottom: 1.25em;
  }

	&__site-title {
		font-size: 1.5em;
	}

	&__links {
    margin-top: -.5em;
    display: flex;
    align-items: center;
    justify-content: space-between;

    a {
      color: var(--body-color);

      &:hover {
        color: var(--link-color);
      }
    }

		a + a {
			margin-left: 1em;
    }
	}
}
</style>
