<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <div class="notify">
          <div class="notify__title">
            <h1>Notify App</h1>
          </div>
          <div class="notify__content">
            <notify :messages="messages" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import notify from "@/components/Notify.vue";

export default {
  components: { notify },
  data() {
    return {
      messages: [
        { title: "message 1" },
        { title: "message 2" },
        { title: "message 3" },
        { title: "message 4" },
        { title: "message 5" },
        { title: "message 6" },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  height: 90vh;
}

.notify {
  max-width: 400px;
  width: 100%;
  margin: auto;
  padding: 32px;
  border-radius: 16px;
  background-color: #fff;
  box-shadow: 0 12px 22px 0 rgba(0,0,0, 0.1);

  &__title {
    h1 {
      margin-bottom: 16px;
      font-size: 24px;
      font-weight: 600;
    }
  }

  &__content {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 240px;
  }
}
</style>