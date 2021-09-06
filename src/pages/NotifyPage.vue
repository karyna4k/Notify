<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <div class="notify">
          <div class="notify__title">
            <h1>Notify App</h1>
          </div>
          <div class="notify__content">
            <!-- preloader -->
            <preloader v-if="loading" :width="90" :height="90" />

            <!-- erorr -->
            <div class="error" v-if="error">
              <p>{{ error }}</p>
            </div>

            <!-- notify -->
            <notify v-if="!loading && !error" :messages="messages" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import notify from "@/components/Notify.vue";

// UI
import preloader from '@/components/UI/Preloader.vue'

export default {
  components: { notify, preloader },
  data() {
    return {
      loading: false,
      error: null,
      messages: [],
    };
  },
  mounted() {
    this.getNotify();
  },
  methods: {
    getNotifyLazy() {
      this.loading = true;
      setTimeout(() => {
        this.getNotify();
      }, 1800);
    },
    getNotify() {
      this.loading = true;
      axios
        .get("https://tocode.ru/static/_secret/courses/1/notifyApi.php")
        .then((response) => {
          let res = response.data.notify;
          this.messages = res;
          // console.log(res);
        })
        .catch((error) => {
          console.log(error);
        })
        .finally(() => {
          this.loading = false;
        });
    },
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
  box-shadow: 0 12px 22px 0 rgba(0, 0, 0, 0.1);

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