<template>
  <div
    class="post-card content-box"
    :class="{'post-card--has-poster' : post.poster}"
  >
    <div class="post-card__header">
      <g-image
        v-if="post.cover_image"
        alt="Cover image"
        class="post-card__image"
        :src="post.cover_image"
      />
    </div>
    <div class="post-card__content">
      <h2
        class="post-card__title"
        v-html="post.title"
      />
      <p
        class="post-card__description"
        v-html="post.description"
      />

      <PostMeta
        class="post-card__meta"
        :post="post"
      />
      <PostTags
        class="post-card__tags"
        :post="post"
      />

      <g-link
        class="post-card__link"
        :to="post.path"
      >
        Link
      </g-link>
    </div>
  </div>
</template>

<script>
import PostMeta from '~/components/PostMeta'
import PostTags from '~/components/PostTags'

export default {
  components: {
    PostMeta,
    PostTags
  },
  props: {
    post: {
      type: Object,
      default: () => {},
    },
  },
}
</script>

<style lang="scss">
.post-card {
  margin-bottom: var(--space);
  position: relative;

  &__header {
    margin-left: calc(var(--space) * -1);
    margin-right: calc(var(--space) * -1);
    margin-bottom: calc(var(--space) / 2);
    margin-top: calc(var(--space) * -1);
    overflow: hidden;
    border-radius: var(--radius) var(--radius) 0 0;

    &:empty {
      display: none;
    }
  }

  &__image {
    min-width: 100%;
  }

  &__title {
    margin-top: 0;
  }

  &:hover {
    transform: translateY(-3px);
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
  }

  &__tags {
    z-index: 1;
    position: relative;
  }

  &__link {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0.0;
    overflow: hidden;
    text-indent: -9999px;
    z-index: 0;
  }
}
</style>
