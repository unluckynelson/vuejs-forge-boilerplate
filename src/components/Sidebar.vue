<template>
  <NavigationMenu></NavigationMenu>
  <div>
    <Drawer
      :expanded="expanded"
      :position="position"
      :mode="mode"
      :mini="true"
      :items="
        items.map((item, index) => ({
          ...item,
          selected: index === selectedId,
        }))
      "
      @select="onSelect"
    >
      <DrawerContent>
        <router-view />
      </DrawerContent>
    </Drawer>
  </div>
</template>

<script>
import { Drawer, DrawerContent } from "@progress/kendo-vue-layout";
import { useLocalStorage } from "@vueuse/core";

const expanded = useLocalStorage("sidebar-expanded", true);

export default {
  name: "App",
  components: {
    Drawer,
    DrawerContent,
  },
  mounted() {
    this.$router.push(this.items[0].data);
  },
  data() {
    return {
      items: [
        {
          text: "Boards",
          icon: "k-i-set-column-position",
          selected: true,
          data: {
            path: "/",
          },
        },
        {
          text: "Templates",
          icon: "k-i-border-left",
          data: {
            path: "/templates",
          },
        },
        {
          text: "Settings",
          icon: "k-i-gear",
          data: {
            path: "/settings",
          },
        },
        {
          text: "Collapse",
          icon: "k-i-chevron-left",
          data: {
            action: () => (expanded.value = !expanded.value),
          },
        },
      ],
      expanded: expanded,
      selectedId: 0,
      position: "start",
      mode: "push",
    };
  },
  methods: {
    onSelect(e) {
      this.selectedId = e.itemIndex;
      this.$router.push(this.items[e.itemIndex].data);
      this.expanded = !this.expanded;
    },
  },
};
</script>