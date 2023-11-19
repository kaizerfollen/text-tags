<template>
  <v-app>
    <v-container>
      <P>Компонент на всю ширину экрана с выравниванием по левому краю</P>
      <text-tags :tags="tags" alignment="left" />

      <P>Компонент на всю ширину экрана с выравниванием по ширине</P>
      <text-tags :tags="tags" alignment="width" />

      <p>Компонент на 50% ширины экрана с выравниванием по левому краю</p>
      <v-row>
        <v-col cols="6">
          <text-tags :tags="tags" alignment="left" />
        </v-col>
      </v-row>

      <P>Компонент на 50% ширины экрана с выравниванием по ширине</P>
      <v-row>
        <v-col cols="6">
          <text-tags :tags="tags" alignment="width" />
        </v-col>
        <v-col cols="6">
          <text-tags :tags="tags" alignment="width" />
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import TextTags from './components/TextTags.vue';

export default {
  components: {
    TextTags,
  },
  data() {
    return {
      tags: [
        {
          text: 'text1',
        },
        {
          text: 'text2',
          icon: 'ab-testing',
        },
        {
          text: 'text3',
          icon: 'account-badge',
        },
        {
          text: 'text4',
          icon: 'map-plus',
        },
        {
          text: 'text5',
          icon: 'atom',
        },
      ],
    };
  },
};
</script>
