<template>
  <div class="tags-container" :class="{ 'justify': alignment === 'width' }">
    <template v-for="(tag, index) in visibleTags">
      <div class="tag" :key="index">
        <span class="tag-text">{{ tag.text }}</span>
        <span v-if="tag.icon" class="tag-icon">
          <v-icon>{{ `mdi-${tag.icon}` }}</v-icon>
        </span>
        <span v-if="index !== visibleTags.length - 1" class="tag-divider">
          <v-icon>mdi-circle-small</v-icon>
        </span>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    tags: {
      type: Array,
      required: true,
    },
    alignment: {
      type: String,
      default: 'left',
    },
  },
  data() {
    return {
      visibleTags: [],
    };
  },
  mounted() {
    this.updateVisibleTags();
    window.addEventListener('resize', this.updateVisibleTags);
  },
  destroyed() {
    window.removeEventListener('resize', this.updateVisibleTags);
  },
  methods: {
    updateVisibleTags() {
      const containerWidth = this.$el.offsetWidth;
      let totalWidth = 0;
      let index = 0;
      let tempWidth = 0;
      this.visibleTags = [];

      while (index < this.tags.length && totalWidth <= containerWidth) {
        const tag = this.tags[index];
        const tagWidth = this.getTagWidth(tag);

        if (totalWidth + tagWidth <= containerWidth) {
          this.visibleTags.push(tag);
          totalWidth += tagWidth;
        } else {
          break;
        }

        if (index !== this.tags.length - 1) {
          tempWidth += tagWidth + this.getTagWidth(this.tags[index + 1]);
          if (tempWidth > containerWidth) {
            break;
          }
        }

        index += 1;
      }
    },
    getTagWidth(tag) {
      const iconWidth = tag.icon ? 30 : 0;
      const textWidth = tag.text.length * 8;
      return iconWidth + textWidth;
    },
  },
};
</script>

<style lang="scss" scoped>
.tags-container {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 5px;
  &.justify {
    justify-content: space-between;
  }
}

.tag {
  display: flex;
  align-items: center;
}

.tag-icon {
  margin-right: 5px;
}

.tag-divider {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 5px;
}

</style>
