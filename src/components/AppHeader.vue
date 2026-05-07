```vue
<template>
  <nav class="navbar navbar-expand navbar-dark bg-dark px-3">
    <!-- Logo -->
    <a href="/" class="navbar-brand">Ứng dụng Quản lý danh bạ</a>

    <!-- Menu -->
    <div class="mr-auto navbar-nav">
      <li class="nav-item">
        <router-link :to="{ name: 'contactbook' }" class="nav-link">
          Danh bạ
          <i class="fas fa-address-book ms-1"></i>
        </router-link>
      </li>
    </div>

    <!-- Right side -->
    <div class="d-flex align-items-center text-white">
      <!-- Nếu chưa login -->
      <button
        v-if="!user"
        class="btn btn-outline-light btn-sm"
        @click="loginGoogle"
      >
        <i class="fab fa-google me-1"></i>
        Đăng nhập Google
      </button>

      <!-- Nếu đã login -->
      <div v-else class="d-flex align-items-center">
        
        <span class="me-2">{{ user.name }}</span>

        <button class="btn btn-danger btn-sm" @click="logout">
          Đăng xuất
        </button>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      user: null,
    };
  },

  methods: {
    loginGoogle() {
      window.location.href = "http://localhost:3000/auth/google";
    },

    logout() {
      window.location.href = "http://localhost:3000/auth/logout";
    },

    async getUser() {
      try {
        const res = await fetch("http://localhost:3000/auth/user", {
          credentials: "include", // QUAN TRỌNG để giữ session
        });
        const data = await res.json();
        this.user = data;
      } catch (error) {
        console.log("Lỗi lấy user:", error);
      }
    },
  },

  mounted() {
    this.getUser();
  },
};
</script>

<style scoped>
.navbar {
  height: 60px;
}
</style>
