<template>
  <div class="container mt-5">
    <form class="row justify-content-center" @submit.prevent="signin">
      <div class="col-md-6">
        <h1 class="h3 mb-3 font-weight-normal">請先登入</h1>
        <div class="mb-2">
          <label for="inputEmail" class="sr-only">Email address
          <input type="email" id="inputEmail" v-model="users.username" class="form-control"
          placeholder="Email address" required/>
          </label>
        </div>
        <div class="mb-2">
          <label for="inputPassword" class="sr-only">Password
          <input type="password" id="inputPassword" v-model="users.password"
          class="form-control" placeholder="Password" required />
          </label>
        </div>
        <div class="text-end mt-4">
          <button class="btn btn-lg btn-primary btn-block" type="submit">登入</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: {
        username: '',
        password: '',
      },
    };
  },
  methods: {
    signin() {
      const api = `${process.env.VUE_APP_API}admin/signin`;
      this.axios.post(api, this.users).then((res) => {
        const { token, expired } = res.data;
        // console.log(token, expired);
        document.cookie = `hexToken=${token}; expires=${new Date(expired)}`;
        console.log(res);
      });
    },
  },
};
</script>
